---
title: Docker项目-自建一个加密鸽——cryptgeon
date: 2022/12/23 12:45
tags: [Docker]
categories: [Docker]
---
## 1. 介绍

cryptgeon是一个安全的、开源的共享笔记或文件服务，其灵感来源于PrivNote。

后台是用Rust写的，前台是用Svelte和Typecript。

GitHub 开源项目，支持Docker搭建。

### 1.1 特点

咕咕这边简单在网上也抄搜集了一些特点，供大家参考（翻译自GitHub的README）：

GitHub完全开源，可以免费使用
Docker搭建，10分钟搞定
在浏览器中加密，服务器端无法解密内容
可以设置浏览次数或指定分享时间，超出次数（最大可设置100次）或者时间后（最长可设置360分钟），文件永久消失（服务器所有者也无法看到）
文件存在内存中，没有持久性
支持黑暗模式
1.2 工作原理

每个笔记都会生成一个的ID（256位）和密钥256（位）。这个ID用于保存和检索笔记。

然后，在客户端用密钥以GCM模式对笔记进行AES加密，之后后发送到服务器。

数据只存储在内存中，不会持久化到硬盘上（意味着重启数据会丢失）。

## 2. 项目展示

GitHub原项目地址：https://github.com/cupcakearmy/cryptgeon（205 star）

Demo地址：https://cryptgeon.nicco.io

官方Docker地址：https://hub.docker.com/r/cupcakearmy/cryptgeon



## 3. 搭建环境

服务器：腾讯香港轻量应用服务器24元/月VPS一台展示用的服务器是Netcup特价款，本期搭建用的是Vultr的服务器，按小时计费，可随时销毁（最好是选非大陆的服务器）（腾讯轻量购买链接）Hetzner注册免费得25欧试用金有效期一个月
系统：Debian 10（DD脚本 非必需DD用原来的系统也OK）
域名一枚，并做好解析到服务器上（域名购买、域名解析 视频教程）
安装好Docker、Docker-compose（相关脚本）
【非必需】提前安装好宝塔面板海外版本aapanel，并安装好Nginx（安装地址）
【非必需本教程采用】安装好Nginx Proxy Manager（相关教程）

## 4.搭建

服务器初始设置，参考
```
sudo -i # 切换到root用户

apt update -y  # 升级packages

apt install wget curl sudo vim git  # Debian系统比较干净，安装常用的软件
```
创建一下安装的目录：
```
mkdir -p /root/data/docker_data/cryptgeon

cd /root/data/docker_data/cryptgeon

nano docker-compose.yml
```
docker-compose.yml填入以下内容：
```
# docker-compose.yml
version: '3.8'

services:
  redis:
    image: redis:7-alpine

  app:
    image: cupcakearmy/cryptgeon:latest
    depends_on:
      - redis
    environment:
      SIZE_LIMIT: 4 MiB
    ports:
      - 8080:5000
```
下面是旧版的，有时无法创建加密内容，建议用上面新版yaml文件
```
version: '3.7'

services:
  memcached:
    image: memcached:1-alpine
    entrypoint: memcached -m 256M -I 8M   # Limit to 128 MB Ram, 4M per entry, customize at free will. （限制最大使用128M的内存，每条项目最大使用4M内存，可以自己修改）

  app:
    image: cupcakearmy/cryptgeon:latest
    depends_on:
      - memcached
    environment:
      SIZE_LIMIT: 8M  # 这边的4M要与上面对应
    ports:
      - 8080:5000   # 冒号左边的端口8080可以改成任意你没有用过的端口
```
查看端口是否被占用，输入：
```
lsof -i:8080  #查看8080端口是否被占用，如果被占用，重新自定义一个端口
```
如果出现：
```
-bash: lsof: command not found
```
运行：
```
apt install lsof  #安装lsof
```
如果端口没有被占用，可以运行：
```
docker-compose up -d 
```
访问：http:服务ip:8080 即可。

注意：
1、不知道服务器IP，可以直接在命令行输入：curl ip.sb，会显示当前服务器的IP。
2、遇到访问不了的情况，请在宝塔面板的防火墙和服务商的后台防火墙里打开对应端口。

## 5.更新
```
cd /root/data/docker_data/cryptgeon  # 进入docker-compose所在的文件夹
docker-compose pull    # 拉取最新的镜像
docker-compose up -d   # 重新更新当前镜像
```
利用Docker-compose搭建的应用，更新非常容易～
## 6.卸载
```
sudo -i
cd /root/data/docker_data/cryptgeon  # 进入docker-compose所在的文件夹
docker-compose down    # 停止容器，此时不会删除映射到本地的数据
cd ~
rm -rf /root/data/docker_data/cryptgeon  # 完全删除映射到本地的数据
```
## 7.反向代理（必须）
此项目和别的项目不同，必须采用https形式，否则浏览器无法加密，无法使用。
7.1 利用Nginx Proxy Manager

在添加反向代理之前，确保你已经完成了域名解析，不会的可以看这个：域名一枚，并做好解析到服务器上（域名购买、域名解析 视频教程）

之后，登陆Nginx Proxy Manager（不会的看这个：安装Nginx Proxy Manager（相关教程））

注意：
Nginx Proxy Manager（以下简称NPM）会用到80、443端口，所以本机不能占用（比如原来就有Nginx）
注意填写对应的域名、IP和端口，按文章来的话，应该是8080
IP填写：

如果Nginx Proxy Manager和cryptgeon在同一台服务器上，可以在终端输入：
```
ip addr show docker0
```
查看对应的Docker容器内部IP。

否则直接填cryptgeon所在的服务器IP就行
再次打开，勾选这些：
然后就可以用域名来安装访问了。
## 8. 结尾

祝大家用得开心，有问题可以去GitHub提Issues，也可以在评论区互相交流探讨。

同时，有能力给项目做翻译的同学，也欢迎积极加入到项目中来，贡献自己的一份力量！

## 9. 参考资料

GitHub原项目地址：https://github.com/cupcakearmy/cryptgeon（205 star）

Demo地址：https://cryptgeon.nicco.io

官方Docker地址：https://hub.docker.com/r/cupcakearmy/cryptgeon