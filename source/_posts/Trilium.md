---
title: Docker项目-个人知识库——Trilium
date: 2022/12/23 12:45
tags: [Docker]
categories: [Docker]
---
## 特点
笔记可以排列成任意深的树。单个笔记可以放在树中的多个位置（请参阅克隆）
丰富的所见即所得笔记编辑功能，包括带有markdown自动格式化功能的表格，图像和数学
支持编辑使用源代码的笔记，包括语法高亮显示
笔记之间快速导航，全文搜索和笔记挂起
无缝笔记版本控制
笔记属性可用于笔记组织，查询和高级脚本编写
同步与自托管同步服务器
具有按笔记粒度的强大的笔记加密
关系图和链接图，用于可视化笔记及其关系
脚本-请参阅高级展示
可用性和性能均能很好地扩展至超过10万个笔记
针对智能手机和平板电脑进行触摸优化的移动前端
夜间主题
Evernote和Markdown导入导出
Web Clipper可轻松保存Web内容
## 项目展示
GitHub原项目地址：https://github.com/zadam/trilium

英文版本客户端下载地址：https://github.com/zadam/trilium/releases

GitHub项目中文版本地址：https://github.com/Nriver/trilium-translation

中文版本客户端下载地址：https://github.com/Nriver/trilium-translation/releases

项目截图地址：https://github.com/zadam/trilium/wiki/Screenshot-tour

中文文档地址：https://github.com/zadam/trilium/blob/master/README-ZH_CN.md

## 搭建环境
服务器：腾讯香港轻量应用服务器24元/月VPS一台展示用的服务器是Netcup特价款，本期搭建用的是Vultr的服务器，按小时计费，可随时销毁（最好是选非大陆的服务器）（腾讯轻量购买链接）
系统：Debian 10（DD脚本 非必需DD用原来的系统也OK）
域名一枚，并做好解析到服务器上（域名购买、域名解析 视频教程）
安装好Docker、Docker-compose（相关脚本）
【非必需】安装好宝塔面板海外版本aapanel，并安装好Nginx（安装地址）
【非必需不过本教程使用】安装好Nginx Proxy Manager（相关教程）

## 搭建方式
服务器初始设置，参考
```
apt update -y  # 升级packages

apt install wget curl sudo vim git  # Debian系统比较干净，安装常用的软件
```
创建一下安装的目录：
```
mkdir -p /root/data/docker_data/trilium

cd /root/data/docker_data/trilium

nano docker-compose.yml

```
docker-compose.yml填入以下内容
```
version: '3'
services:
  trilium-cn:
    image: nriver/trilium-cn
    restart: always
    ports:
      - "8080:8080"
    volumes:
      # 把同文件夹下的 trilium-data 目录映射到容器内
      - ./trilium-data:/root/trilium-data
    environment:
      # 环境变量表示容器内笔记数据的存储路径
      - TRILIUM_DATA_DIR=/root/trilium-data
```
没问题的话，ctrl+x退出，按y保存，enter确认。
然后运行：
```
docker-compose up -d 
```
附英文原版安装（与上方二选一即可）：
```
docker run -itd --restart=always -p 8080:8080 -v ~/trilium-data:/home/node/trilium-data zadam/trilium:[VERSION]
```
访问：http:服务ip:8080 即可。
注意：
1、不知道服务器IP，可以直接在命令行输入：curl ip.sb，会显示当前服务器的IP。
2、遇到访问不了的情况，请在宝塔面板的防火墙和服务商的后台防火墙里打开对应端口。


## 反向代理
在添加反向代理之前，确保你已经完成了域名解析，不会的可以看这个：域名一枚，并做好解析到服务器上（域名购买、域名解析 视频教程）

之后，登陆Nginx Proxy Manager（不会的看这个：安装Nginx Proxy Manager（相关教程））

注意：
Nginx Proxy Manager（以下简称NPM）会用到80、443端口，所以本机不能占用（比如原来就有Nginx）


## 使用教程

### Trilium的使用教程

来自少数派，感谢作者@idelem的分享：

Trilium：超高自由度的个人知识库（基础篇）

Trilium：超高自由度的个人知识库（进阶篇）

Trilium：超高自由度的个人知识库（高级篇）

### 2 界面自定义修改

https://github.com/zadam/trilium/wiki/Themes

### 桌面端下载

英文版本客户端下载地址：https://github.com/zadam/trilium/releases

中文版本客户端下载地址：https://github.com/Nriver/trilium-translation/releases

### 常见问题汇总

https://github.com/Nriver/trilium-translation/blob/main/README_CN.md#笔记数据库在哪

## 结尾

祝大家用得开心，有问题可以去GitHub提Issues，也可以在评论区互相交流探讨。

## 参考资料

https://www.v2ex.com/t/788222