---
layout: post
title: 简单的iOS TabPageScrollView开发笔记
excerpt: "开发了个小小小Tab页面的小组件，供iOS初学者学习"
date: 2015-09-26 22:38:41
categories: 技术
---


* TOC
{:toc}

# 背景
看到CocoaPods上这么多好东西，初入iOS开发，也想熟悉熟悉这个流程。
想到最近自己开发的一个简单的Tab页面，尝试完善一下，做的更通用一些，放到CocoaPods上。

# 最终
使用方法及代码见：https://github.com/everettjf/EVTTabPageScrollView

![demo](https://everettjf.github.io/images/extern/EVTTabPageScrollView.gif)


# 步骤

1. 创建模板工程
    参考链接：https://guides.cocoapods.org/making/using-pod-lib-create.html
    ```
    pod lib create MyLibrary
    ```
2. 修改描述、编写库的代码
3. 测试
    ```
    pod lib lint
    pod spec lint
    ```
4. 上传
    ```
    $ pod trunk register orta@cocoapods.org 'Orta Therox' --description='macbook air'
    $ pod trunk push EVTTabPageScrollView.podspec
    ```
    参考链接：https://guides.cocoapods.org/making/getting-setup-with-trunk

# 其他
这个还很简单，仅作为自己试用CocoaPods的例子。


