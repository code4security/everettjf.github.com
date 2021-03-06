---
layout: post
title: "vim emacs 常用快捷键对比"
excerpt: "对比下两个神器的快捷键吧，不要再折腾啦"
date: 2015-03-05
categories: 技术
---


习惯了vim快捷键，又了解下emacs。
vim使用spf，emacs使用prelude，体验了两位“大神”。（写多了，这篇文章与这两个没有直接关系，写出了作为笔记）

个人经常使用vim的dd或者yy然后p，感觉emacs的就麻烦了（C-a C-k C-y）
主要是emacs用的很少。

习惯了vim，可以emacs启用evil-mode。
emacs的M-x很强大。

简单整理下常用快捷键的对比，作为笔记。

|------+----------------+------------------+-----------------------------------------------------------|
| star | vim            | emacs            | comment                                                   |
|------+----------------+------------------+-----------------------------------------------------------|
| *    | i              | ---              | 插入模式                                                  |
| *    | :              | ---              | 命令模式                                                  |
| *    | ESC            | ---              | 普通模式                                                  |
|      | h              | C-b              | 左                                                        |
|      | l              | C-f              | 右                                                        |
|      | j              | C-n              | 下                                                        |
|      | k              | C-p              | 上                                                        |
|      | :q             | C-x C-c          | 退出                                                      |
|      | :q!            | C-x c-c n        | 强制退出                                                  |
|      | x              | C-d              | 删除当前单词                                              |
|      | w              | M-f              | 右单词                                                    |
|      | b              | M-b              | 左单词                                                    |
|      | o              |                  | 在光标下一行添加，并开始编辑                              |
|      | O              |                  | 在光标上一行添加，并开始编辑                              |
|      | ^              | C-a              | 移动光标到当前行第一个字符首                              |
|      | $              | C-e              | 行尾                                                      |
|      | 0              |                  | 行首                                                      |
|      | :o             | C-x C-f          | 打开文件                                                  |
|      | :w             | C-x C-s          | 保存文件                                                  |
|      | :wq            |                  | 保存并退出                                                |
|      | a              | ---              | 在光标后开始编辑                                          |
|      | A              |                  | 在行最后开始编辑                                          |
|      | I              |                  | 在行首开始编辑                                            |
|      | C-v            |                  | 垂直选择视图                                              |
|      | C-V            |                  | 垂直选择行视图                                            |
|      | p              |                  | 粘贴                                                      |
|      | y              |                  | 复制                                                      |
|      | dd             |                  | 删除当前行                                                |
|      | dw             |                  | 删除当前单词                                              |
|      | 2dd            |                  | 删除两行                                                  |
|      | u              |                  | 撤销                                                      |
|      | C-r            |                  | 重复                                                      |
|      | d$             |                  | 删除光标到文件最后                                        |
|      | r              |                  | 替换当前字符                                              |
|      | cw             |                  | 删除光标开始的单词，并开始编辑                            |
|      | c$             |                  | 删除到文件最后，并开始编辑                                |
|      | G              | M->              | 最后一行                                                  |
|      | gg             | M-<              | 第一行                                                    |
| *    | ''             |                  | 回到刚才的行                                              |
|      | :400           |                  | 转到400行                                                 |
|      | 400G           |                  | 转到400行                                                 |
|      | %              |                  | 转到匹配的括号                                            |
|      | :s/old/new/g   | M-x repl s ...   | 文本替换                                                  |
|      | :%s/old/new/g  | M-x repl s ...   | 文本替换                                                  |
|      | :%s/old/new/gc | M-x repl s ...   | 文本替换                                                  |
| *    |                | C-v              | 下一屏幕                                                  |
| *    |                | M-v              | 上一屏幕                                                  |
| *    |                | C-l              | 光标行置于屏幕中央                                        |
| *    |                | M-a              | 句首                                                      |
| *    |                | M-e              | 句尾                                                      |
|      |                | C-u 数字 命令    | 重复N次命令（或输入）                                     |
|      |                | C-g              | 终止当前命令输入                                          |
| *    |                | Esc              | 辅助按下M键                                               |
|      |                | C-d              | 删除光标后字符                                            |
|      | db             | M-<DEL>          | 移除光标前单词                                            |
|      | dw             | M-d              | 移除光标后单词                                            |
|      | d$             | C-k              | 移除光标到行尾                                            |
|      | dG             | M-k              | 移除光标到句尾                                            |
|      |                | C-@ 之后 C-w     | 移除选定文字（C-<SPACE>）                                 |
|      |                | C-y              | 召回最近一次“移除”的内容（例如 C-k C-k C-y）              |
|      |                | M-y              | 不断召回上一次“移除”的内容                                |
|      |                | C-/              | 撤销上次命令的影响（与 C-x u 或 C-_ 相同）                |
|      |                | C-x s            | 保存多个缓冲区                                            |
|      |                | C-x C-b          | 缓冲区列表                                                |
|      |                | C-x b 缓冲区名称 | 切换到缓冲区                                              |
|      |                | C-z              | 暂时离开emacs（shell中输入fg或者%emacs再次回来）          |
|      |                | C-x C-c          | 直接退出                                                  |
|      |                | C-s              | 向前搜索（C-g光标回到开始位置，<Return>光标定位到结果上） |
|      |                | C-r              | 向后搜索                                                  |
|      |                | C-x 1            | 保留当前窗口                                              |
|      |                | C-x 2            | 垂直分割窗口                                              |
|      |                | C-x 3            | 水平分割窗口                                              |
|      |                | C-x o            | 移动光标到其他窗口（other）                               |
|      |                | C-M-v            | 向下滚动其他窗口                                          |
|      |                | C-M-<Shift>-v    | 向上滚动其他窗口                                          |
|      |                | C-h c 命令       | 显示命令的简易帮助                                        |
|      |                | C-h k 命令       | 显示命令的详细帮助                                        |
|      |                | C-h i            | 手册                                                      |
| *    |                | C-h b            | 显示所有函数绑定(describe bindings)                       |
|      |                |                  |                                                           |


