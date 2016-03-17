---
layout: post
title: (Writing)YYCache learn
excerpt: “YYCache 学习笔记，使用XSourceNote做笔记”
date: 2016-03-17
tags: [源码学习]
comments: true
---


# Basic Information
 - Name : YYCache
 - Site : https://github.com/ibireme/YYCache
 - Repo : https://github.com/ibireme/YYCache
 - Revision : f433c3455121bd0308cd6f551613c7ec629e937a
 - Description : 
在内存与磁盘上性能都不错的缓存库。

这是作者的设计思路介绍：http://blog.ibireme.com/2015/10/26/yycache/



# Global Note
作者的成长经历值得我们学习，在一年多的iOS开发中提高的很快。

# File Notes
0. /YYCache/YYMemoryCache.h
 - Line : 16 - 30
 - Note : 

{% highlight c %}
/**
 YYMemoryCache is a fast in-memory cache that stores key-value pairs.
 In contrast to NSDictionary, keys are retained and not copied.
 The API and performance is similar to `NSCache`, all methods are thread-safe.
 
 YYMemoryCache objects differ from NSCache in a few ways:
 
 * It uses LRU (least-recently-used) to remove objects; NSCache's eviction method
   is non-deterministic.
 * It can be controlled by cost, count and age; NSCache's limits are imprecise.
 * It can be configured to automatically evict objects when receive memory 
   warning or app enter background.
 
 The time of `Access Methods` in YYMemoryCache is typically in constant time (O(1)).
 */
{% endhighlight %}


 - YYMemoryCache 是内存缓存。 
 - Key是retained，而不是copied。
 - 使用了LRU（最近最少使用）算法。 

1. /YYCache/YYMemoryCache.m
 - Line : 15 - 15
 - Note : 

{% highlight c %}
#import <QuartzCore/QuartzCore.h>
{% endhighlight %}


QuartzCore 这个框架需要研究下。
#TODO#

2. /YYCache/YYMemoryCache.m
 - Line : 18 - 18
 - Note : 

{% highlight c %}
#if __has_include("YYDispatchQueuePool.h")
{% endhighlight %}


可以这么判断是否包含了某个头文件。

3. /YYCache/YYMemoryCache.m
 - Line : 32 - 45
 - Note : 

{% highlight c %}
/**
 A node in linked map.
 Typically, you should not use this class directly.
 */
@interface _YYLinkedMapNode : NSObject {
    @package
    __unsafe_unretained _YYLinkedMapNode *_prev; // retained by dic
    __unsafe_unretained _YYLinkedMapNode *_next; // retained by dic
    id _key;
    id _value;
    NSUInteger _cost;
    NSTimeInterval _time;
}
@end
{% endhighlight %}


双向链表的节点。
cost以及time（最后使用时间）。
_prev 和 _next 是__unsafe_unretained 修饰，被外层的 CFMutableDictionaryRef retained。

@package 修饰符，在framework内部可访问，framework外部不可访问。

4. /YYCache/YYMemoryCache.m
 - Line : 57 - 66
 - Note : 

{% highlight c %}
@interface _YYLinkedMap : NSObject {
    @package
    CFMutableDictionaryRef _dic; // do not set object directly
    NSUInteger _totalCost;
    NSUInteger _totalCount;
    _YYLinkedMapNode *_head; // MRU, do not change it directly
    _YYLinkedMapNode *_tail; // LRU, do not change it directly
    BOOL _releaseOnMainThread;
    BOOL _releaseAsynchronously;
}
{% endhighlight %}


双向链表 定义。头、尾。dic用于存储元素，同时retain元素。

5. /YYCache/YYMemoryCache.m
 - Line : 92 - 92
 - Note : 

{% highlight c %}
    _dic = CFDictionaryCreateMutable(CFAllocatorGetDefault(), 0, &kCFTypeDictionaryKeyCallBacks, &kCFTypeDictionaryValueCallBacks);
{% endhighlight %}


CFMutableDictionaryRef 用法mark。

6. /YYCache/YYMemoryCache.m
 - Line : 101 - 154
 - Note : 

{% highlight c %}

- (void)insertNodeAtHead:(_YYLinkedMapNode *)node {
    CFDictionarySetValue(_dic, (__bridge const void *)(node->_key), (__bridge const void *)(node));
    _totalCost += node->_cost;
    _totalCount++;
    if (_head) {
        node->_next = _head;
        _head->_prev = node;
        _head = node;
    } else {
        _head = _tail = node;
    }
}

- (void)bringNodeToHead:(_YYLinkedMapNode *)node {
    if (_head == node) return;
    
    if (_tail == node) {
        _tail = node->_prev;
        _tail->_next = nil;
    } else {
        node->_next->_prev = node->_prev;
        node->_prev->_next = node->_next;
    }
    node->_next = _head;
    node->_prev = nil;
    _head->_prev = node;
    _head = node;
}

- (void)removeNode:(_YYLinkedMapNode *)node {
    CFDictionaryRemoveValue(_dic, (__bridge const void *)(node->_key));
    _totalCost -= node->_cost;
    _totalCount--;
    if (node->_next) node->_next->_prev = node->_prev;
    if (node->_prev) node->_prev->_next = node->_next;
    if (_head == node) _head = node->_next;
    if (_tail == node) _tail = node->_prev;
}

- (_YYLinkedMapNode *)removeTailNode {
    if (!_tail) return nil;
    _YYLinkedMapNode *tail = _tail;
    CFDictionaryRemoveValue(_dic, (__bridge const void *)(_tail->_key));
    _totalCost -= _tail->_cost;
    _totalCount--;
    if (_head == _tail) {
        _head = _tail = nil;
    } else {
        _tail = _tail->_prev;
        _tail->_next = nil;
    }
    return tail;
}
{% endhighlight %}


双向链表的基本操作。好久不看算法了。贴着吧。

7. /YYCache/YYMemoryCache.m
 - Line : 190 - 198
 - Note : 

{% highlight c %}
- (void)_trimRecursively {
    __weak typeof(self) _self = self;
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(_autoTrimInterval * NSEC_PER_SEC)), dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_LOW, 0), ^{
        __strong typeof(_self) self = _self;
        if (!self) return;
        [self _trimInBackground];
        [self _trimRecursively];
    });
}
{% endhighlight %}


简单的定时器。



# Summarize




---
*Generated by XSourceNote at 2016-03-16 17:33:48 +0000*
