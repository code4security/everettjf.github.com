---
layout: post
title: "emacs新手遇到的坑，以及笔记"
description: "vim新手学习emacs中遇到的坑"
category: emacs
tags: [emacs]
---
{% include JB/setup %}

作为一名windows程序猿、vim、markdown新手。忽然进入另一个“世界，遇到osx、emac、org，遇到了一些坑，记录下来。

## 安装
- MacOS
    <pre>
    brew install emacs --with-cocoa
    brew linkapps emacs

    然后重新打开iTerm2，输入emacs就可以在终端运行emacs了。
    也在Applications里有了emacs项。
    </pre>

## 坑

- windows8.1下emacs24.4部分中文显示为“方块”。
    在.emacs文件中（或者prelude的init.el文件中）加入下面一行：
<pre>
(set-fontset-font "fontset-default" 'gb18030 '("Microsoft YaHei" . "unicode-bmp"))
</pre>

- .emacs文件和.emacs.d文件夹中的init.el同时存在，只有.emacs文件生效。
<pre>
当使用prelude时，需要删除.emacs文件(如何使两者都有效？)
</pre>

- osx10.10.1（界面英文）terminal下使用brew安装emacs，中文显示问号。
<pre>
系统切换为中文，解决。（不切换如何解决，暂不想研究了）
</pre>

- osx下，terminal或iterm下meta按键问题

  - terminal下
<pre>
终端->偏好设置->描述文件->键盘
最下方选择“使用Option键作为Meta键”
</pre>

  - iterm
<pre>
Preferences -> Profiles 然后选择当前的profile -> Keys
最下面都选择+Esc
Left option key acts as : +Esc
Rigth option key acts as : +Esc
</pre>

- 如何找到.emacs文件的存放位置（尤其是windows下）
<pre>
    C-X C-F ~/
</pre>

## 笔记

- prelude推荐

  - Github地址：[https://github.com/bbatsov/prelude](https://github.com/bbatsov/prelude)
  - 其他没有试过，作为新手，prelude给了我能量。
  - 安装prelude
<pre>
git clone git://github.com/bbatsov/prelude.git path/to/local/repo
ln -s path/to/local/repo ~/.emacs.d
cd ~/.emacs.d
</pre>
samples中复制出prelude_modules.el，并启动emacs。

- 关于evil与中文输入法

  - 中文输入法切换与vim本身的各种模式切换太别扭了（这也是想体验下emacs的原因之一吧）
  - 如果编写程序还是可以启用evil
<pre>
启用或关闭evil-mode
M-x evil-mode
</pre>

- osx下交换capslock与ctrl

  - 系统偏好设置->键盘->键盘->修饰键（右下角）

- 按键重复速度

  - 系统偏好设置->键盘->键盘->调整按键重复（到最快）

- 安装主题monokai
很喜欢monokai这个主题
<pre>
M-x package-install
monokai-theme

M-x customize-theme
选择monokai后，save settings，就ok啦。
</pre>

---
