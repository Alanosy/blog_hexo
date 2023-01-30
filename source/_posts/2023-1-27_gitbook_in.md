---
title: Gitbook的搭建过程
date: 2023/1/27 12:03:00
tags: [技术分享]
---
## Gitbook搭建
### 1、安装Nodejs
1.1、ubantu安装
```
apt-get install nodejs npm -y
```
1.2 mac安装
官网下载安装

```
https://nodejs.org/en/
```
1.2 Window安装
官网下载安装

```
https://nodejs.org/en/
```

### 2、 安装Gitbook

```
npm install Gitbook-cli -g
```

### 3、 初始化目录

```
Gitbook init book
```


### 4. 启动Gitbook服务

```
Gitbook serve
```
参数:
&ensp;&ensp;&ensp;&ensp; --port=8081
1
### 5、Gitbook使用篇

Summary


```
# Summary

* [目录](README.md)

* [第一章](notes/1-0.md)

  * [第1节：](notes/1-1.md)

  * [第2节：](notes/1-2.md)

  * [第3节：](notes/1-3.md)

  * [第4节：](notes/1-4.md)

* [第二章](notes/2-0.md)

* [第三章](notes/3-0.md)

* [第四章](notes/4-0.md)
```

生成pdf格式：

```
Gitbook pdf ./ ./mybook.pdf
```

**提示：**
初始化时如果出现TypeError: cb.apply is not a function错误
![在这里插入图片描述](https://img-blog.csdnimg.cn/3dd9626e8ab4411ab8a3a7274ef280ec.png#pic_center)

可以找到提示路径，打开 polyfills.js 文件，找到这个函数。
![在这里插入图片描述](https://img-blog.csdnimg.cn/a1fe881dbfa2456294d542cb96980b2f.png#pic_center)


```
fs.stat = statFix(fs.stat)
fs.fstat = statFix(fs.fstat)
fs.lstat = statFix(fs.lstat)
```
把这三行代码注释掉就解决报错了
这是因为npm版本问题
