---
title: Docker项目-自建一个属于自己的免费搜索引擎平台-SearXNG
date: 2022/12/23 12:45
tags: [Docker]
categories: [Docker]
---
```
sudo -i # 切换到root用户

apt update -y  # 升级packages

apt install wget curl sudo vim git -y  # Debian系统比较干净，安装常用的软件
```
## 创建安装目录及docker-compose文件

创建一下安装的目录：
```
mkdir -p /root/data/docker_data/searxng

cd /root/data/docker_data/searxng

git clone https://github.com/searxng/searxng-docker.git

cd searxng-docker/

vim docker-compose.yaml
```
因为官方默认是试用caddy来反代的，有一个问题就是可能会和你网站上的80端口冲突，导致searXNG与你服务器上的其他网站无法共存，我们这边把caddy部分注释掉，改为采用{NginxProxyManager}(https://blog.laoda.de/tags/nginxproxymanager)反代。
```
version: '3.7'

services:
# 我们注释掉caddy的内容
  #  caddy:
  #  container_name: caddy
  #  image: caddy:2-alpine
  #  network_mode: host
  #  volumes:
  #    - ./Caddyfile:/etc/caddy/Caddyfile:ro
  #    - caddy-data:/data:rw
  #    - caddy-config:/config:rw
  #  environment:
  #    - SEARXNG_HOSTNAME=${SEARXNG_HOSTNAME:-http://localhost:80}
  #    - SEARXNG_TLS=${LETSENCRYPT_EMAIL:-internal}
  #  cap_drop:
  #    - ALL
  #  cap_add:
  #    - NET_BIND_SERVICE
  #    - DAC_OVERRIDE

  redis:
    container_name: redis
    image: "redis:alpine"
    command: redis-server --save "" --appendonly "no"
    networks:
      - searxng
    tmpfs:
      - /var/lib/redis
    cap_drop:
      - ALL
    cap_add:
      - SETGID
      - SETUID
      - DAC_OVERRIDE

  searxng:
    container_name: searxng
    image: searxng/searxng:latest
    networks:
      - searxng
    ports:
     - "8180:8080"   # 这个冒号左边的端口可以更改，右边的不要改
    volumes:
      - ./searxng:/etc/searxng:rw
    environment:
      - SEARXNG_BASE_URL=https://${SEARXNG_HOSTNAME:-localhost}/
    cap_drop:
      - ALL
    cap_add:
      - CHOWN
      - SETGID
      - SETUID
      - DAC_OVERRIDE
    logging:
      driver: "json-file"
      options:
        max-size: "1m"
        max-file: "1"
networks:
  searxng:
    ipam:
      driver: default

        #volumes:
        #caddy-data:
        #caddy-config:
```
切换到英文输入法，按下i输入内容。

输入完成之后，切换到英文输入法，按下:wq保存退出。

接着我们来编辑一下.env文件。
```
cd /root/data/docker_data/searxng/searxng-docker

vim .env
```
切换到英文输入法，按下i输入内容。
取消#注释，在上图位置填入你之后需要用到的域名。

第二行的邮件不用管，那个是caddy申请的一个邮件，我们不用caddy。

输入完成之后，切换到英文输入法，按下:wq保存退出。
```
cd /root/data/docker_data/searxng/searxng-docker

sed -i "s|ultrasecretkey|$(openssl rand -hex 32)|g" searxng/settings.yml # 生成一个密钥
```
```
cd /root/data/docker_data/searxng/searxng-docker

docker-compose up -d  
```
更新
```
cp -r /root/data/docker_data/searxng/searxng-docker /root/data/docker_data/searxng/searxng-docker.archive  # 万事先备份，以防万一

cd /root/data/docker_data/searxng/searxng-docker  # 进入docker-compose所在的文件夹

docker-compose pull    # 拉取最新的镜像

docker-compose up -d   # 重新更新当前镜像
```
卸载
```
cd /root/data/docker_data/searxng/searxng-docker  # 进入docker-compose所在的文件夹

docker-compose down    # 停止容器，此时不会删除映射到本地的数据

rm -rf /root/data/docker_data/searxng/searxng-docker  # 完全删除映射到本地的数据
```
