---
title: supotato - classify class-dump headers tool
layout: post
guid: urn:uuid:e579485d-f42b-471b-9902-a6d81eecb2d5
tags:
  - 工具
---

class-dump 出的头文件这么多，supotato 可以根据头文件的`前2个字符`形成个简单的分类报告。

[GitHub](https://github.com/everettjf/supotato)

---


## 例子

例如 class-dump 出以下的头文件：

[Here](https://github.com/everettjf/supotato/tree/master/example/headers)

运行supotato：

```sh
$ supotato -i headers -o .
```

得到这个简单的分类：

[Here](https://github.com/everettjf/supotato/blob/master/example/result.txt)


下面是真实的例子（闲鱼头文件列表的分类）：

[Here](https://github.com/everettjf/supotato/blob/master/example/lots.txt).


## 参数

```
$ supotato -h
usage: supotato [-h] [-i INPUT] [-o OUTPUT] [-s SORTBY] [-d ORDER]
                [-p PREFIXLENGTH]

Generate a simple report for header files in your directory

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        directory that header(.h) files in.
  -o OUTPUT, --output OUTPUT
                        file (or directory) path to put txt report in.
  -s SORTBY, --sortby SORTBY
                        prefix or count . Means sort by prefix or count.
  -d ORDER, --order ORDER
                        desc or asc.
  -p PREFIXLENGTH, --prefixlength PREFIXLENGTH
                        prefix length for classify , default to 2.

```

```
$ supotato -i /Users/xxx/wechat/headers/ -o /Users/xxx/wechat/ -s prefix -order desc -p 3
```


# 计划

如果能自动猜测出使用了哪些第三方库，岂不是更好。

思路如下：

- 获取cocoapods的数据库（公开的）
- 遍历所有cocoapods的库，获取最新版本的文件，获取10个文件作为特征。
- 遍历class-dump的头文件，查找。

思路很简单，但如何更快速的判断出，需要优化。

**此feature开发中，即将上线**




