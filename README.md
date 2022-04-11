# Go-CQHTTP-Docker-Compose

## 说明

用于 qq 机器人及其插件的 docker-compose 文件

[go-cqhttp](https://github.com/Mrs4s/go-cqhttp)
[Go-CQHTTP-Docker](https://github.com/xzsk2/Go-CQHTTP-Docker)
[xkbot](https://github.com/flaribbit/xkbot-QQbot)

**注意： 还在编写中，不能使用......** 

## 快速使用

```bash

# 登录 linux 服务器

cd ~ && mkdir -p app/cphttp && cd app/cphttp

mkdir data assets plugins

# 初始化 cqhttp ，选 3， 然后 ctrl + c 退出
docker run --rm -it --name="gocq" -v $PWD/data:/data zxlt/gocqhttp:v1
# 修改 data/config.yml 内容，主要修改 uin (qq 号)，可以不配置密码，通过扫码认证。
vim data/config.yml

# 扫码认证一次即可。
docker run --rm -it --name="gocq" -v $PWD/data:/data zxlt/gocqhttp:v1


# 使用 docker-compose 方式 启动 cqhttp 和 xkbot

# 拷贝本仓库的 docker-compose 文件内容

vim docker-compose.yml
docker network create qq
docker-compose up -d
```

## build

如果想自己体验 build 的过程，可以下载此仓库

```bash

git clone git@github.com:sanshiliuxiao/Go-CQHTTP-Docker-Compose.git

cd Go-CQHTTP-Docker-Compose

docker build  -f .\docker\Dockerfile.gocqhttp -t gocqhttp:v1 .

docker build -f ./docker/Dockerfile.xkbot -t xkbot:v1 .

# 如果想上传到自己的 docker hub 地址, 比如我的用户是 zxlt

docker login


docker tag gocqhttp:v1 zxlt/gocqhttp:v1

docker tag xkbot:v1 zxlt/xkbot:v1

docker push zxlt/gocqhttp:v1

docker push zxlt/xkbot:v1

```
