---
title: 动态网站编程基础
date: 2023/2/22 21:41:23
tags: [考试]
---

简述ASP文件放在服务器端运行的好处

因为发出的是标准的HTML文件所以不会存在浏览器兼容问题
可以很方便帝和服务器交换数据
因为在客户端仅可看到由ASP输出的HTML文件，可以保护源代码不被泄漏


简述使用广告轮显组建需要使用的文件

广告信息文件：记录所有广告信息的文本文件
超链接处理文件：引导客户到乡音广告页面的ASP文件
显示广告文件：防止广告图片的文件


简述Server对象常用的几个方法

MapPath方法
Exectue方法
Transfer方法
URLEncode方法
HTMLEncode方法
CreateObject方法


简述网页设计的一般步骤

设计主题
设计网页端的总体结构
资料的收集和整理
悬着网页的设计方法
主义一些基本问题 如标题要简明、图片最好加说明等


根据链接源的不同，超链接分成哪几类

超链接主要分为文本超链接和图像超链接。
按超链接路径的不同，网页中超链接一般分为一下
3种类型：
内部链接，
锚点链接和
外部链接


网页和网站有什么区别？

网页是王很赞傻姑娘的某一个页面，它是一个以扩展名为html或htm的文件，向浏览者传递信息的载体，以超文本和超媒体为技术，采用html、css】xml、javascript等语言来描述组成页面的 元素，并通过浏览器进行解释，最后吧结果信息通过浏览器在网页上显示出来。
网站是指internet上的一个固定的面向全世界发布消息的地方，由域名和网站空间构成，通常包括主页和其他具有超链接文件的页面


简述ADO对象主要包含的三种对象及主要功能

ADO主要包括Connection,Recordset和Conmand三个对象。
主要功能如下：
Connection对象：打开或链接数据库或数据文件
Recordset对象： 存取数据库的内容
Command对象：对数据库下达行动查询指令或调用存储过程

简述常用的SQL语句

Select语句
Insert语句
Delete语句
Update语句

写出URL包含的3部分内容的作用

第一部分是Scheme，告诉浏览器该如何工作
第二部分是文件所在的主机
第三部分是文件的路径和文件名

编写ASP程序，利用int和Rnd函数产生一个1到10的随机整数

``` ASP
<% option Explicit %>
<html>
<body>
<% Dim intMyRnd Randomize Timer() intMyRnd=int((10*Rnd()+1) [response write](response.write) intMyRnd %>
</body>
</html>

编写ASP程序，计算1到100的累加和

``` ASP
<% option Explicit %>
<html>
<body>
<% Dim IngSum, i IngSum=0 For i=1 to 100 IngSum=IngSum+i Next Response. write IngSum %>
</body>
<htm>
```
编写ASP代码，实现利用for...next循环计算从1到100的平方和
``` ASP
<% Option Explicit %>
<html>
<head>
<title>For...Next循环语句用法示例</title>
</head>
<body>
<% Dim Sum,l Sum=0 For l=1 to 100 Sum=Sum+l2 Response.Write "1到100的平方和="& CStr(Sum) %>
</body>
</html>
```

