---
layout: post
title: 实战学习：干掉高德地图版本7.5.4版iOS客户端的反动态调试保护
excerpt: ""
date: 2015-12-20
tags: [iOS逆向]
comments: true
---

学习了 http://www.iosre.com/t/7-2-0-ios/770 和 http://bbs.iosre.com/t/ptrace/371 两篇文章后，上手操作了下。
发现7.5.4版本已经没有了sub函数，而是直接在start中加入了ptrace的动态加载。如下图：


![code](http://7xibfi.com1.z0.glb.clouddn.com/uploads/default/original/2X/3/36d0c61b45367ad359fcd472574bc6da38529425.png)

想来可以直接hook dlsym，当第二个参数为"ptrace"时，返回一个假的ptrace函数。

图中可以看到高德地图并没有判断ptrace的返回值。

关键代码：

~~~
#import <substrate.h>
#import <mach-o/dyld.h>
#import <dlfcn.h>


int fake_ptrace(int request, pid_t pid, caddr_t addr, int data){
	return 0;
}

void *(*old_dlsym)(void *handle, const char *symbol);

void *my_dlsym(void *handle, const char *symbol){
	if(strcmp(symbol,"ptrace") == 0){
		return (void*)fake_ptrace;
	}

	return old_dlsym(handle,symbol);
}

%ctor{
	MSHookFunction((void*)dlsym,(void*)my_dlsym,(void**)&old_dlsym);
}

~~~

自己已测试，还蛮好用。
这是代码，可参考：
https://github.com/everettjf/iOSREPractise/tree/master/AMap754/amaptest