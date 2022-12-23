---
title: Docker项目-开源即时聊天应用——Tailchat
date: 2022/12/23 12:45
tags: [Docker]
categories: [Docker]
---
## 服务器前期配置

```
sudo -i # 切换到root用户

apt update -y  # 升级packages

apt install wget curl sudo vim git -y  # Debian系统比较干净，安装常用的软件
```

## 安装Docker
```
curl -L https://get.daocloud.io/docker/compose/releases/download/v2.1.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose

docker-compose --version  #查看docker-compose版本
```

## 创建安装目录
创建一下安装的目录：
```
sudo -i

mkdir -p /root/data/docker_data/tailchat

cd /root/data/docker_data/tailchat
```

## 安装
这边我们直接用docker的方式安装。
```
vim docker-compose.yml
```
英文输入法下，按i
```
version: "3.3"

services:
  # 应用网关
  service-gateway:
    build:
      context: .
    image: tailchat
    restart: unless-stopped
    env_file: docker-compose.env
    environment:
      SERVICES: core/gateway
      PORT: 3000
    depends_on:
      - mongo
      - redis
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.api-gw.rule=PathPrefix(`/`)"
      - "traefik.http.services.api-gw.loadbalancer.server.port=3000"
    networks:
      - internal

  # 用户服务
  service-user:
    build:
      context: .
    image: tailchat
    restart: unless-stopped
    env_file: docker-compose.env
    environment:
      SERVICES: core/user/*
    depends_on:
      - mongo
      - redis
    networks:
      - internal

  # 群组服务
  service-group:
    build:
      context: .
    image: tailchat
    restart: unless-stopped
    env_file: docker-compose.env
    environment:
      SERVICES: core/group/*
    depends_on:
      - mongo
      - redis
    networks:
      - internal

  # 聊天服务
  service-chat:
    build:
      context: .
    image: tailchat
    restart: unless-stopped
    env_file: docker-compose.env
    environment:
      SERVICES: core/chat/*
    depends_on:
      - mongo
      - redis
    networks:
      - internal

  # 文件服务 / 插件注册中心 / 配置服务
  service-file:
    build:
      context: .
    image: tailchat
    restart: unless-stopped
    env_file: docker-compose.env
    environment:
      SERVICES: core/file,core/plugin/registry,core/config
    depends_on:
      - mongo
      - redis
      - minio
    networks:
      - internal

  service-openapi:
    build:
      context: .
    image: tailchat
    restart: unless-stopped
    env_file: docker-compose.env
    environment:
      SERVICES: openapi/app,openapi/oidc/oidc
      OPENAPI_PORT: 3003
      OPENAPI_UNDER_PROXY: "true"
    depends_on:
      - mongo
      - redis
      - minio
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.openapi-oidc.rule=PathPrefix(`/open`)"
      - "traefik.http.services.openapi-oidc.loadbalancer.server.port=3003"
    networks:
      - internal

  # 插件服务(所有插件)
  service-all-plugins:
    build:
      context: .
    image: tailchat
    restart: unless-stopped
    env_file: docker-compose.env
    environment:
      SERVICEDIR: plugins
    depends_on:
      - mongo
      - redis
      - minio
    networks:
      - internal

  # 数据库
  mongo:
    image: mongo:4
    restart: on-failure
    volumes:
      - ./data:/data/db
    networks:
      - internal

  # 数据缓存与中转通讯
  redis:
    image: redis:alpine
    restart: on-failure
    networks:
      - internal

  # 存储服务
  minio:
    image: minio/minio
    restart: on-failure
    networks:
      - internal
    environment:
      MINIO_ROOT_USER: tailchat
      MINIO_ROOT_PASSWORD: com.msgbyte.tailchat
    volumes:
      - ./storage:/data
    command: minio server /data --console-address ":9001"

  # 路由转发
  traefik:
    image: traefik:v2.1
    restart: unless-stopped
    command:
      - "--api.insecure=true" # Don't do that in production!
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entryPoints.web.address=:80"
      - "--entryPoints.web.forwardedHeaders.insecure" # Not good
    ports:
      - 8080:80            # 8080可以改成自己服务器上没有被占用的端口
      - 127.0.0.1:11001:8080     #11001同上
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
    networks:
      - internal
      - default

networks:
  internal:
    name: tailchat-internal
```
按一下esc，然后:wq 保存退出，之后，
```
vim docker-compose.env
```
一样写入下面的内容：
```
LOGGER=true
LOGLEVEL=info
SERVICEDIR=services

TRANSPORTER=redis://redis:6379

CACHER=redis://redis:6379

REDIS_URL=redis://redis:6379
MONGO_URL=mongodb://mongo/tailchat
SECRET=adswddWEQ@4  # 改成自己的密钥

# file
API_URL=https://chat.gugu.ovh   # 改成自己的网站

# minio
MINIO_URL=minio:9000
MINIO_USER=tailchat
MINIO_PASS=com.msgbyte.tailchat

# SMTP
SMTP_SENDER=
SMTP_URI=

# metrics
PROMETHEUS=1
```
按一下esc，然后:wq 保存退出，之后，
```
docker pull moonrailgun/tailchat
docker tag moonrailgun/tailchat tailchat # 修改tag以让配置文件能够识别
```
最后：
```
cd /root/data/docker_data/tailchat    # 确保来到dockercompose文件所在的文件夹下

# 确保配置文件(docker-compose.yml和docker-compose.env)在当前目录下
# 执行以下命令一键启动
docker-compose up -d
```
访问: http://<server ip>:8080 即可打开tailchat

注意部分云服务可能需要手动开放防火墙端口。

在docker-compose.env文件中提供了部分环境变量可供配置。

tailchat 的docker-compose.yml配置默认提供了如下配置:

mongodb: 持久化数据库
redis: KV数据库与消息中转服务
minio: 分布式文件服务