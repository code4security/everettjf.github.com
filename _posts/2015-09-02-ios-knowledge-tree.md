---
layout: post
title: "(编写中)iOS 知识树"
description:
headline:
modified: 2015-09-02
category: iOS
tags: [iOS]
image:
  feature:
comments: true
mathjax:
---

*文章于2015年9月2日开始编写，暂未编写完成……*

2015年3月份，做了不到2个月的iOS开发。中间停止了2个多月。
一直到2015年8月13日，来到北京，正式开始iOS开发。

本文将把我从C++转为iOS开发的过程中遇到的各种知识点罗列出来。

# 开发环境

1. MacBook Pro ：各种配置都够用啦。
1. Xcode ：必备IDE。
1. Xcode Command Line Tools ：内置各种工具。
1. XcodePlugins
  - http://alcatraz.io/ 插件管理器，必备，方便安装其他插件。
  - XVim ：vim插件
  - VVDocumenter-Xcode ： 方便生成各种注释
  - KSImageNamed ：代码中预览图片
  - FuzzyAutocomplete ：自动完成的模糊匹配，瞬间让Xcode好用起来。
  - XToDo
  - ColorSenseRainbow
1. XcodeSnippets ：常用代码片段用github管理起来。
1. CocoaPods ：第三方库少不了用，做C++这几年都手动配置头文件、生成路径、链接库，没注意C++里有这么出名的工具。

# 语言

1. Objective-C
2. @dynamic

# 界面开发

1. UIView
1. UIButton
1. UILabel
1. UITextEdit
1. UITextView
1. UIScrollView
1.  代码写界面：入门很好的一篇文章。http://www.cocoachina.com/bbs/read.php?tid=131516
1. UITableView

# 特殊知识
1. MVC
1. MVVM
1. KVC (Key Value Coding)
1. KVO (Key Value Observing)
  - NSMutableArray特殊对待
  - KVC是基础知识
1. Toll-Free Bridging
1. Bitcode
1. Method Swizzing
1. 关联对象
2. Objective C++
3. 消息转发机制（12条）
4. 缓存delegate（23条）
5. Unittest Specta/Expecta or Kiwi
6. 

# 第三方库

1. AFNetworking
1. Marsonry
1. CocoaLumberjack

# 调试

1. PLCrashReporter
1. KSCrash
1. Exception Catch Internals

# 发布

1. ipa文件
1. 代码签名
1. fastlane工具包
1. Jenkins持续集成配置

# 逆向
1. todo

# 常用站点
1. GitHub
1. CocoaChina
1. Code4app

# 牛人博客

# 书
1. 《马上着手开发 iOS 应用程序 (Start Developing iOS Apps Today)》 ：苹果官方文档，入门必看。
1. 《Objective-C程序设计》 ：有C++基础，很快就看完了。
1. 《iOS开发指南：从零基础到App Store上架》 ：感觉很基础，也很啰嗦（讲解细致），
找几个例子练习以下，以后边用边查。
1. 《精通iOS开发》：补充iOS开发知识体系
1. 《iOS开发进阶》：说是进阶，但都是些实用工具，适合iOS开发一两个月之后看。
能很快看完，但工具需要多多使用，慢慢熟练。
1. 《Effective Objective-C 2.0》 ：（在看，挺愉快轻松）
1. 《Objective-C编程之道》：（在看）
1. 《iOS应用逆向工程》：（在浏览）
1. 《深入解析Mac OS X & iOS操作系统》：（在浏览）能了解很多实现原理。
1. 《大话移动APP测试，Android与iOS应用测试指南》：（还未看）
