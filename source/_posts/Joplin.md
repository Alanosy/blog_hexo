---
title: Docker项目-全平台同步笔记软件——Joplin
date: 2022/12/23 12:45
tags: [Docker]
categories: [Docker]
---
## 介绍

Joplin是一个免费、开源的笔记和待办事项的软件。

支持搜索，笔记格式是Markdown（如果你还不知道什么是Markdown，而你又有记录的需求，强烈你看这个视频来了解这个好用的东东——YouTube用户点击这个：【如何优雅地写博客系列】Markdown语法的使用！ 国内用户点击这个：如何优雅地写博客系列！Markdown语法的使用！）

从Evernote（国内叫“印象笔记”）导出的笔记可以导入Joplin，包括格式化的内容（被转换为Markdown）、资源（图片、附件等）和完整的元数据（地理位置、更新时间、创建时间等）。普通的Markdown文件也可以被导入。

笔记可以使用端对端加密与各种云服务安全地同步，包括Nextcloud、Dropbox、OneDrive和Joplin Cloud（今天我们就来分享如何搭建Joplin Cloud）。

全文搜索在所有平台上都可用，以快速找到你需要的信息。

该应用程序可用于Windows、Linux、macOS、Android和iOS。

支持网页剪裁，可以从你的浏览器中保存网页和截图，也可用于火狐和Chrome。

软件开箱即用，我们今天主要来分享一下，如何搭建Joplin Cloud同步服务器。

这个服务器允许你与任何Joplin客户端进行同步，就像你与Dropbox、OneDrive等进行同步一样。

## 搭建
```
sudo -i # 切换到root用户

apt update -y  # 升级packages

apt install wget curl sudo vim git  # Debian系统比较干净，安装常用的软件
```
创建一下安装的目录：
```
mkdir -p /root/data/docker_data/joplin

cd /root/data/docker_data/joplin

nano docker-compose.yml
```
docker-compose.yml填入以下内容：
```
# This is a sample docker-compose file that can be used to run Joplin Server
# along with a PostgreSQL server.
#
# Update the following fields in the stanza below:
#
# POSTGRES_USER
# POSTGRES_PASSWORD
# APP_BASE_URL
#
# APP_BASE_URL: This is the base public URL where the service will be running.
#	- If Joplin Server needs to be accessible over the internet, configure APP_BASE_URL as follows: https://example.com/joplin. 
#	- If Joplin Server does not need to be accessible over the internet, set the the APP_BASE_URL to your server's hostname. 
#     For Example: http://[hostname]:22300. The base URL can include the port.
# APP_PORT: The local port on which the Docker container will listen. 
#	- This would typically be mapped to port to 443 (TLS) with a reverse proxy.
#	- If Joplin Server does not need to be accessible over the internet, the port can be mapped to 22300.

version: '3'

services:
    db:
        image: postgres:13
        volumes:
            - ./data/postgres:/var/lib/postgresql/data
        ports:
            - "5432:5432"  # 左边的端口可以更换，右边不要动！
        restart: unless-stopped
        environment:
            - POSTGRES_PASSWORD=changeme # 改成你自己的密码
            - POSTGRES_USER=username  # 改成你自己的用户名
            - POSTGRES_DB=joplin
    app:
        image: joplin/server:latest
        depends_on:
            - db
        ports:
            - "22300:22300" # 左边的端口可以更换，右边不要动！
        restart: unless-stopped
        environment:
            - APP_PORT=22300
            - APP_BASE_URL=https://your.domain.com # 改成反代的域名
            - DB_CLIENT=pg
            - POSTGRES_PASSWORD=changeme # 与上面的密码对应！
            - POSTGRES_DATABASE=joplin
            - POSTGRES_USER=username  # 与上面的用户名对应！
            - POSTGRES_PORT=5432 # 与上面右边的对应！
            - POSTGRES_HOST=db
```
没问题的话，ctrl+x退出，按y保存，enter确认。

打开防火墙的端口22300、5432
```
lsof -i:5432  #查看5432端口是否被占用，如果被占用，重新自定义一个端口
```
如果出现：
```
-bash: lsof: command not found
```
运行：
```
apt install lsof  #安装lsof
```
如果端口没有被占用，我们接着可以运行：
```
cd /root/data/docker_data/joplin

docker-compose up -d  
```
注意：
1、不知道服务器IP，可以直接在命令行输入：curl ip.sb，会显示当前服务器的IP。
2、遇到访问不了的情况，请在宝塔面板的防火墙和服务商的后台防火墙里打开对应端口。
更新
```
cp -r /root/data/docker_data/joplin /root/data/docker_data/joplin.archive  # 万事先备份，以防万一

cd /root/data/docker_data/joplin  # 进入docker-compose所在的文件夹

docker-compose pull    # 拉取最新的镜像

docker-compose up -d   # 重新更新当前镜像
```
卸载
```
cd /root/data/docker_data/joplin  # 进入docker-compose所在的文件夹

docker-compose down    # 停止容器，此时不会删除映射到本地的数据

rm -rf /root/data/docker_data/joplin  # 完全删除映射到本地的数据
```
