---
layout: post
title: List Wechat source files directory tree
excerpt: "看看微信怎么组织文件的"
date: 2016-11-23
categories: 技术
---
 
* TOC
{:toc}
---
 

项目越大，就越需要合理的组织文件目录层次。

逆向微信的过程中，经常看到一些“输出日志”的方法调用，而且带有完整的路径。例如：

```
/Users/ioscmechine/Desktop/hudson/workspace/release_appstore_6.3.29/WeApp/Core/LocalCache/WAPackageSweeperLogic.mm
```

看来是用了__FILE__宏导致。

用strings把微信（砸壳后）的字符串都存储到一个文件中，

```
$ strings WeChat > strings_wechat.txt
```

也如图：

![](/media/14798364851450.jpg)

写个小脚本把所有`/Users/`开头的字符串提出来，然后分隔，组装成一棵树。

就可以看到微信的一部分文件结构啦。

![](/media/14798366527896.jpg)


[脚本地址](https://github.com/everettjf/MachOExplorer/tree/master/game/wechat_dir_tree)

[输出的微信文件层次](https://github.com/everettjf/MachOExplorer/blob/master/game/wechat_dir_tree/wechat_tree.txt)



