---
layout: post
title: "使用fastlane实现iOS持续集成"
description:
headline:
modified: 2015-09-08
category: personal
tags: []
image:
  feature:
comments: true
mathjax:
---

# 0x00

以前在Windows上配置过Visual Studio的持续集成，主要以下步骤：
1. hudson搭建。
1. devenv实现命令行下编译整个工程。
1. 配合nsis实现打包。
1. 再签名。
1. ftp上传等步骤。

最近转行iOS开发，首要任务是使用Jenkins（算是hudson的兄弟）配置iOS工程的持续集成。
查找各种资料后，整理出以下几个关键词。
1. jenkins搭建。
1. 使用fastlane中提供的工具修改工程配置。
1. gym 或 ipa 工具编译工程。

# 0x01 目标
配置一台电脑自动获取代码，并定时打包出以下版本的ipa文件。
1. 内部测试版本：使用Developer证书签名的ipa文件。
1. 公开测试版本：使用企业账号的Distribute InHouse证书签名的ipa文件。
1. AppStore版本：使用
