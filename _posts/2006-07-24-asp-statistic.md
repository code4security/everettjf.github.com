---
layout: post
title: "asp统计网站访问量的方法"
excerpt: "百度博客没有了，把一些有意思和回忆的文章放这里吧"
tags: [随笔]
date: 2006-07-24
modified: 
comments: true
---


先手动创建一个rstj.txt文件，然后在此文件输入一个数字，再在rstj.txt文件的同目录下
创建一个.asp文件，内容如下：

~~~
<% 
Function rstj()
 dim fso,f1,ts,s
 Const ForReading=1
 Set fso=CreateObject("Scripting.FileSystemObject")
 Set ts=fso.OpenTextFile(Server.MapPath("rstj.txt"),ForReading,true,-2)
 s=ts.Readline
 ts.close
 set fso=createobject("scripting.filesystemobject")
 set f1=fso.createtextfile(server.mappath("rstj.txt"),true,true)
 f1.writeline s+1
 f1.close
 Set ts=fso.OpenTextFile(Server.MapPath("rstj.txt"),ForReading,true,-2)
 s=ts.Readline
 rstj=s
 ts.close
End Function
%>
~~~

您是第<%=rstj%>位访问贵站的朋友