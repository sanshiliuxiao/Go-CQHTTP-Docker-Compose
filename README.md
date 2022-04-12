# Go-CQHTTP-Docker-Compose

## 说明

qq 机器人及其插件的 docker-compose 文件

[go-cqhttp](https://github.com/Mrs4s/go-cqhttp)
[Go-CQHTTP-Docker](https://github.com/xzsk2/Go-CQHTTP-Docker)
[xkbot](https://github.com/flaribbit/xkbot-QQbot)


## 快速使用

```bash

# 登录 linux 服务器， 假设用户为 root

cd ~ && mkdir -p app/qqbot && cd app/qqbot


# 初始化 gocqhttp 
docker run --rm -it --name="gocq" -v $PWD/gocqhttp_bk/:/data zxlt/gocqhttp:v1

# 选 3， 然后 ctrl + c 退出


# 修改 data/config.yml 内容，主要修改 uin (qq 号)，可以不配置密码，通过扫码认证。

vim data/config.yml

###########
  uin: 1233456 # QQ账号
  - ws-reverse:
      # 反向WS Universal 地址
      # 注意 设置了此项地址后下面两项将会被忽略
      universal: ws://xkbot:5700
###########


# 重新登录，会有二维码生成
docker run --rm -it --name="gocq" -v $PWD/gocqhttp_bk:/data zxlt/gocqhttp:v1

# ctrl + c 退出

# 创建 xkbot_s/config.json 文件

mkdir xkbot_s && cd xkbot_s

# 654321 是你的管理 qq 号
echo '{"admin":[654321],"groups":{},"plugins":{}}' > config.json



# 使用 docker-compose 方式 启动 cqhttp 和 xkbot

# 拷贝本仓库的 docker-compose 文件内容
vim docker-compose.yml

# 创建自定义网络
docker network create qq

# 启动
docker-compose up -d
```

### 开启插件功能

`uin` 和 `admin` 两个 qq 号都在同一个群里面，由 `admin` 进行插件的开启， 更多信息查看  [xkbot](https://github.com/flaribbit/xkbot-QQbot) 项目。


在群聊中输入以下命令

```bash
# 查看插件
.bot plugins

# 开启插件
.bot on xxx

# 插件帮助
.bot help xxx

# 关闭插件
.bot off xxx



````


## build

如果想自己体验 build 的过程，可以下载此仓库

```bash

git clone git@github.com:sanshiliuxiao/Go-CQHTTP-Docker-Compose.git

cd Go-CQHTTP-Docker-Compose

docker build  -f .\docker\Dockerfile.gocqhttp -t gocqhttp:v1 .

docker build -f ./docker/Dockerfile.xkbot -t xkbot:v1 .

# 如果想上传到自己的 docker hub 地址, 比如我是 zxlt

docker login


docker tag gocqhttp:v1 zxlt/gocqhttp:v1

docker tag xkbot:v1 zxlt/xkbot:v1

docker push zxlt/gocqhttp:v1

docker push zxlt/xkbot:v1

```
