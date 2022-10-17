# 基础环境安装
数据中心管理系统的两套软件均基于容器化封装, 本文将使用 Docker 作为容器管理引擎

## Docker 安装
### Debian
```
apt update && apt install docker.io docker-compose -y
```
### 其他 Linux
#### 默认安装
```shell
export CHANNEL=stable
bash <(curl -sSL https://get.docker.io) 
```

#### 指定镜像到中国大陆
```shell
export CHANNEL=stable
bash <(curl -sSL https://get.docker.io) --mirror 'AzureChinaCloud'
```