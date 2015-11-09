---
layout: post
title: "ShellExecuteA和ShellExecuteW 以及ShellExecuteExW 之间的一些小“秘密”"
excerpt: "这个……"
tags: [随笔]
date: 2010-10-17
modified: 
comments: true
---



最近女朋友总是爱玩偷菜的游戏，还一个页面一个页面的打开，我就提出用wg偷吧~

下载了个wg，结果女友每次用都弹出一对“乱七八糟”的网页，于是我就想弄个程序给他阻止了。

 

进入正题：

 

背景：一般vc打开网页，使用ShellExecute函数。

 

方案：通过挂钩WH_GETMESSAGE注入所有进程，通过使用detours拦截ShellExecute函数。

 

实现发现的现象：

1、

方法：拦截ShellExecuteW 函数（看了windows核心编程，记得A函数都是通过W函数实现的），

结果：wg程序仍然弹出网页；

 

2、

看了看wg程序的导入段，ShellExecuteA函数；

于是想，ShellExecuteA应该是会调用ShellExecuteW的，难道不调用吗？

方法：自己写了另外一个Dialog程序，使用ShellExecuteA打开网页，竟然没有拦截到。而使用ShellExecuteW能拦截到。

由此想到，ShellExecuteA 不是通过ShellExecuteW实现的。

 

3、

方法：拦截ShellExecuteA和ShellExecuteW。

结果：仍然弹出网页。

 

4、

方法：【只】 拦截ShellExecuteExW函数。

结果：【发现ShellExecuteW竟然是通过ShellExecuteExW实现的】，而ShellExecuteA是自己实现的。

而，ShellExecuteExA 也能拦截到。

也就是ShellExecuteExA是通过ShellExecuteExW实现的。

 

5、

方法：【只】拦截ShellExecuteExA函数。

结果：通过ShellExecuteExW可以打开网页，也就是没有拦截到。

 

----------------------------------

 

总结：

1、ShellExecuteA 是自己实现的流程，而不是通过ShellExecuteW实现。

2、ShellExecuteW是通过ShellExecuteExW实现的。

3、ShellExecuteExA是通过ShellExecuteExW实现的。

 

发现这个小“秘密”（或许文档中有，我没注意），与大家分享哈……