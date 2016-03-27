---
layout: post
title: UITableView-FDTemplateLayoutCell 学习笔记
excerpt: "动态高度，每个iOS程序员必须迈过的坎"
date: 2016-03-24
tags: [源码学习]
comments: true
---




# Basic Information
 - Name : UITableView-FDTemplateLayoutCell
 - Site : https://github.com/forkingdog/UITableView-FDTemplateLayoutCell
 - Repo : https://github.com/forkingdog/UITableView-FDTemplateLayoutCell
 - Revision : e3ee86ce419d18d3ff735056f1474f2863e43003
 - Description : 
简单易用的UITableViewCell自动高度。
作者的博客文章 http://blog.sunnyxx.com/2015/05/17/cell-height-calculation/


# Global Note
简单易用，但在一些复杂界面（例如聊天窗口）中使用时还是需要考虑更多优化问题。


# File Notes

## 0. UITableView+FDTemplateLayoutCell.h

 - Path : /Classes/UITableView+FDTemplateLayoutCell.h
 - Line : 35 - 35
 - Note : 

{% highlight oc %}
- (__kindof UITableViewCell *)fd_templateCellForReuseIdentifier:(NSString *)identifier;
{% endhighlight %}


__kindof XXXClass 可以这么用


## 1. UITableView+FDTemplateLayoutCell.h

 - Path : /Classes/UITableView+FDTemplateLayoutCell.h
 - Line : 28 - 28
 - Note : 

{% highlight oc %}
@interface UITableView (FDTemplateLayoutCell)
{% endhighlight %}


UITableView的extension


## 2. UITableView+FDTemplateLayoutCell.h

 - Path : /Classes/UITableView+FDTemplateLayoutCell.h
 - Line : 87 - 99
 - Note : 

{% highlight oc %}
@interface UITableViewCell (FDTemplateLayoutCell)

/// Indicate this is a template layout cell for calculation only.
/// You may need this when there are non-UI side effects when configure a cell.
/// Like:
///   - (void)configureCell:(FooCell *)cell atIndexPath:(NSIndexPath *)indexPath {
///       cell.entity = [self entityAtIndexPath:indexPath];
///       if (!cell.fd_isTemplateLayoutCell) {
///           [self notifySomething]; // non-UI side effects
///       }
///   }
///
@property (nonatomic, assign) BOOL fd_isTemplateLayoutCell;
{% endhighlight %}


使用 UITableViewCell 模板Cell计算高度，通过 fd_isTemplateLayoutCell 可在Cell内部判断当前是否是模板Cell。可以省去一些与高度无关的操作。


## 3. UITableView+FDTemplateLayoutCell.m

 - Path : /Classes/UITableView+FDTemplateLayoutCell.m
 - Line : 221 - 229
 - Note : 

{% highlight oc %}
@implementation UITableViewCell (FDTemplateLayoutCell)

- (BOOL)fd_isTemplateLayoutCell {
    return [objc_getAssociatedObject(self, _cmd) boolValue];
}

- (void)setFd_isTemplateLayoutCell:(BOOL)isTemplateLayoutCell {
    objc_setAssociatedObject(self, @selector(fd_isTemplateLayoutCell), @(isTemplateLayoutCell), OBJC_ASSOCIATION_RETAIN);
}
{% endhighlight %}


使用runtime增加属性的实现。

SEL类型的_cmd ， 每个方法内部都有，表示方法自身。
因此，可以NSStringFromSelector(_cmd)返回当前方法名称。

使用 get的SEL（也就是_cmd）作为objc_getAssociatedObject的key。值得学习。但要注意set中也要用相同的key，也就是@selector(fd_isTemplateLayoutCell)。





## 4. UITableView+FDTemplateLayoutCell.m

 - Path : /Classes/UITableView+FDTemplateLayoutCell.m
 - Line : 36 - 43
 - Note : 

{% highlight oc %}
        static const CGFloat systemAccessoryWidths[] = {
            [UITableViewCellAccessoryNone] = 0,
            [UITableViewCellAccessoryDisclosureIndicator] = 34,
            [UITableViewCellAccessoryDetailDisclosureButton] = 68,
            [UITableViewCellAccessoryCheckmark] = 40,
            [UITableViewCellAccessoryDetailButton] = 48
        };
        contentViewWidth -= systemAccessoryWidths[cell.accessoryType];
{% endhighlight %}


指定索引定义数组的方式。oc的小技巧真不少。


## 5. UITableView+FDTemplateLayoutCell.m

 - Path : /Classes/UITableView+FDTemplateLayoutCell.m
 - Line : 57 - 64
 - Note : 

{% highlight oc %}
        // Add a hard width constraint to make dynamic content views (like labels) expand vertically instead
        // of growing horizontally, in a flow-layout manner.
        NSLayoutConstraint *widthFenceConstraint = [NSLayoutConstraint constraintWithItem:cell.contentView attribute:NSLayoutAttributeWidth relatedBy:NSLayoutRelationEqual toItem:nil attribute:NSLayoutAttributeNotAnAttribute multiplier:1.0 constant:contentViewWidth];
        [cell.contentView addConstraint:widthFenceConstraint];
        
        // Auto layout engine does its math
        fittingHeight = [cell.contentView systemLayoutSizeFittingSize:UILayoutFittingCompressedSize].height;
        [cell.contentView removeConstraint:widthFenceConstraint];
{% endhighlight %}


AutoLayout 计算Size的方法 systemLayoutSizeFittingSize。
这里新增一个宽度的约束，计算高度后再移除掉。 不错的想法。


## 6. UITableView+FDTemplateLayoutCell.m

 - Path : /Classes/UITableView+FDTemplateLayoutCell.m
 - Line : 79 - 81
 - Note : 

{% highlight oc %}
        // Try '- sizeThatFits:' for frame layout.
        // Note: fitting height should not include separator view.
        fittingHeight = [cell sizeThatFits:CGSizeMake(contentViewWidth, 0)].height;
{% endhighlight %}


不使用AutoLayout的情况下，使用sizeThatFits来获取大小。自定义cell需要实现这个函数。


## 7. UITableView+FDTemplateLayoutCell.m

 - Path : /Classes/UITableView+FDTemplateLayoutCell.m
 - Line : 100 - 121
 - Note : 

{% highlight oc %}
- (__kindof UITableViewCell *)fd_templateCellForReuseIdentifier:(NSString *)identifier {
    NSAssert(identifier.length > 0, @"Expect a valid identifier - %@", identifier);
    
    NSMutableDictionary<NSString *, UITableViewCell *> *templateCellsByIdentifiers = objc_getAssociatedObject(self, _cmd);
    if (!templateCellsByIdentifiers) {
        templateCellsByIdentifiers = @{}.mutableCopy;
        objc_setAssociatedObject(self, _cmd, templateCellsByIdentifiers, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
    }
    
    UITableViewCell *templateCell = templateCellsByIdentifiers[identifier];
    
    if (!templateCell) {
        templateCell = [self dequeueReusableCellWithIdentifier:identifier];
        NSAssert(templateCell != nil, @"Cell must be registered to table view for identifier - %@", identifier);
        templateCell.fd_isTemplateLayoutCell = YES;
        templateCell.contentView.translatesAutoresizingMaskIntoConstraints = NO;
        templateCellsByIdentifiers[identifier] = templateCell;
        [self fd_debugLog:[NSString stringWithFormat:@"layout cell created - %@", identifier]];
    }
    
    return templateCell;
}
{% endhighlight %}


关键的函数。

- 给当前TableView关联一个可变字典。
- 每一种 CellIdentifier 一个Key。
- 用于存储模板Cell。
- 模板Cell用于在内存中构建Cell，并对这个模板Cell计算高度。



# Summarize




---
*Generated by [XSourceNote](https://github.com/everettjf/XSourceNote) at 2016-03-27 18:17:27 +0000*
