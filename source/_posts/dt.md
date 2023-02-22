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



