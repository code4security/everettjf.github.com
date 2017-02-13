---
layout: post
title: （Writing)Spacemacs Tutorial
excerpt: ""
date: 2017-02-11
categories: default
---
 
* TOC
{:toc}
---

*这篇文字面向掌握vi基本操作的macOS盆友们*
 
# 背景

官网：http://spacemacs.org/

# 安装

第一步：
首先确保Home目录下没有.emacs文件和.emacs.d目录，可以先执行下面的命令删除。

```
rm -rf .emacs.d
rm .emacs
```

第二步：

```
git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
```

第三步：

运行emacs。
稍等片刻会有三个提问，都回车默认即可。

# 基本概念

```
C-n 表示Ctrl键的同时，按下字母键n。
M-x 表示Option键（alt键）的同时，按下字母键x。
<spc> f f 表示先后按下空格键、字母键f、字母键f。
<ret> 回车。
```

# 基本操作

## 取消命令

```
C-g 如果在输入某个快捷键中途出错，可以用这个取消。
```

## 光标上下左右

```
上 k 或者 C-p
下 j 或者 C-n
左 h 或者 C-b
右 l 或者 C-f
```

（pnbf就是previous、next、backward、forward）

## 打开或新建文件

```
<spc> f f
```

## 保存文件

```
<spc> s s
```

## 多个文件间切换

```
<spc> b b 列出所有打开的文件
```

然后C-n、C-p选择，或者输入字符过滤，最后<ret>。

## 回到上一个打开的文件

```
<spc> <tab>
```

可以多次执行来回切换。

## 分屏，移动焦点，关闭当前分屏

```
<spc> w / 右侧分屏
<spc> w - 下侧分屏
<spc> w V 右侧分屏，并移动焦点到右侧
<spc> w S 下侧分屏，并移动焦点到下侧
<spc> w d 退出当前分屏
<spc> 1 切换到编号1的分屏（2、3、4以此类推，每个分屏左下角有编号）
```


## 如何改变字体大小

```
<spc> z x 弹出选项，=放大，-缩小，0恢复
```


## 打开.spacemacs配置文件

```
<spc> f e d
```

## 搜索、替换

// todo

# 基本配置

## 默认窗口最大化

配置文件中修改以下任意一项

```
dotspacemacs-maximized-at-startup t 最大化
dotspacemacs-fullscreen-at-startup t 全屏最大化
```


## 选择layer





# 日常小需求

## 过滤日志

## 模糊定位文件夹中的文件

## 查找、替换文件夹中的所有文件

## logos 语法

# Javascript 开发



# C++ 开发

# Python 开发

# GTD 时间管理


# 补充

## 安装SourcePro字体



# 参考资料

- https://simpletutorials.com/c/2859/How+to+change+your+.spacemacs+configuration+file

