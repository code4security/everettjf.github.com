---
layout: post
title: "EverettFJ's Practising With ASP.NET 2.0 (1)"
excerpt: "折腾吧"
tags: [随笔]
date: 2008-01-13
modified: 
comments: true
---



很久不学习ASP.NET了,准备把ASP.NET的内容熟悉下,今天把买的<<圣殿祭祀的ASP.NET 2.0 开发详解>> 拿了出来,准备一页一页的做.做好笔记.在这里把笔记发布出来,希望也能对大家有用.

连接数据库时，出现异常：未将对象引用设置到对象的实例。
一般是web.config中的数据库连接字段,与程序中要想取得的字段名称不一致导致的.

例如:

Web.config中:

~~~
<?xml version="1.0" encoding="utf-8"?>

<configuration>

    <connectionStrings>

        <add name="NorthwindConnection" connectionString="DataSource=EVERETT-610220/SQLEXPRESS;initial catalog=Northwind;User ID=sa;Password=fengzi" providerName="System.Data.SqlClient" />

    </connectionStrings>

</configuration>
~~~

而程序中这样引用:

~~~
    try

            {

                //get the configuration settings

                //method1

                ConnectionStringSettings connSettings = WebConfigurationManager.ConnectionStrings["NorthwindConnectionString"];


                string connString = connSettings.ConnectionString;

                Label1.Text = connString;


                //method2

                string conn = WebConfigurationManager.ConnectionStrings["NorthwindConnectionString"].ConnectionString;

                Label2.Text = conn;

            }

            catch (Exception ex)

            {

                Response.Write(ex.Message);

            }
~~~

只要改成相同的就可以了.

加密解密数据库连接字段
加密:

aspnet_regiis -pe "connectionStrings" -app "/FSDotNetTest" -prov "RSAProtectedConfigurationProvider"

解密:

aspnet_regiis -pd "connectionStrings" -app "/FSDotNetTest"


-pe  加密的web.config中的程序段

-app  web应用程序的虚拟目录

-prov 选择哪种加密方式的Provider

-pd  要解密的字段


网站预编译
1.用指令:

Aspnet_Compiler -v FSDotNetTest e:/temp/DotNetTest

-v     虚拟目录参数

FSDotNetTest   虚拟目录的名称

e:/temp/DotNetTest  编译后的程序文件目的位置


2.用API

System.Web.Compilation.ClientBuildManager类


3.VS2005的"发布网站"

勾选 允许更新此预编译站点,那么.aspx的html标签会被保留下来.

一个项目同时使用C#和VB.NET两种语言
在web.config中:

<?xml version="1.0" encoding="utf-8"?>

<configuration>

  <system.web>

    <compilation>

      <codeSubDirectories>

        <add directoryName="cs"/>

        <add directoryName="vb"/>

      </codeSubDirectories>      

    </compilation>

  </system.web>

</configuration>

在App_Code文件夹中加入以上声明中对应的vb和cs两个文件夹.

在cs文件夹下建立

CSharpObject.cs文件,内容:

using System;

using System.Data;

using System.Configuration;

using System.Web;

using System.Web.Security;

using System.Web.UI;

using System.Web.UI.WebControls;

using System.Web.UI.WebControls.WebParts;

using System.Web.UI.HtmlControls;


/// <summary>

/// CSharpObject 的摘要说明

/// </summary>

public class CSharpObject

{

 public CSharpObject()

 {

  //

  // TODO: 在此处添加构造函数逻辑

  //

 }

    public string SayHello() { return "Hello CSharp Object!"; }


}

在vb文件夹下建立VBNetObject.vb文件,内容:

Imports Microsoft.VisualBasic


Public Class VBNetObject

    Public Function SayHello() As String

        Return "Hello VBNetObject!"

    End Function

End Class

直接在aspx.cs文件中:

    protected void Button1_Click(object sender, EventArgs e)

    {

        TextBox1.Text=(new VBNetObject()).SayHello();

    }

    protected void Button2_Click(object sender, EventArgs e)

    {

        TextBox2.Text = (new CSharpObject()).SayHello();

    }

即可.

SQL SERVER 2005 EXPRESS 的管理工具:

SQL Server Management Studio Express (SSMSE)


SQL Server 2005 和 SQL Server 2000的共存安装
如果先安装SQL SERVER 2000 则一定要以 "实例" 安装;

如果后安装 SQL SERVER 2000 ,则SQL SERVER 2000 会被强制以"实例"方式安装.


SQL SERVER 2000在 Windows 2003 下安装后,必须再加上sp3后才能完全运作正常.


命令模式下,SQL Server数据库服务的启用和停止
SQL SERVER 2005

NET START /NET STOP

MSSQLSERVER

SQL SERVER 2000

MSSQL$SQL2000

SQL SERVER 2005 EXPRESS

MSSQL$SQLEXPRESS


ADO.NET程序连接设置
假设主机名是:EFJ

SQL SERVER不是实例:

Data Source=EFJ;initial catalog=northwind;user id=sa;password=fengzi;

SQL SERVER 2000,实例安装:

Data Source=EFJ/SQL2000;initial catalog=northwind;user id=sa;password=fengzi;

2005EXPRESS版本:

Data Source=EFJ/SQLEXPRESS;initial catalog=northwind;user id=sa;password=fengzi;


SQL SERVER 及Windows 验证模式
安装SQL SERVER 2005时,默认是"Windows身份验证",故在第一次连接时必须以"Windows 身份验证"来登录,连接成功后再到[服务器属性]->[安全]->将验证模式更改为[SQL SERVER 及Windows 验证模式],然后重新启动SQL SERVER服务.


远程SQL SERVER 主机要是能被连接,则远程主机的SQL SERVER 验证模式也必须调整为"SQL SERVER 及Windows验证模式".

连接SQL SERVER 所输入的帐号密码是SQL SERVER 内的帐号密码,并非是Windows内的帐号密码.


SQL SERVER Mangement Studio->数据库右键->属性->安全性->服务器身份验证


SQL SERVER 2005联机丛书

Free


导入数据库
附加Attach

分离Detach

*.mdf数据文件,*.ldf  Log文件


数据库内存设置
SQL SERVER 安装后,默认的内存使用上限是整部计算机的内存最大值.

SQL SERVER Mangement Studio->数据库右键->属性->内存->最大服务器内存,更改为256MB等就可以了.





Partial 关键字
多个文件定义一个类

File1.cs

    public partial class Class1

    {

        public string Method2() { return "Method2"; }

    }

File2.cs

    public partial class Class1

    {

        public string Method1() { return "Method1"; }

    }

