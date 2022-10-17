# 开始迁移 (通过本地)

文中存放迁移数据的目录均定为 `/mnt/tmp` , 如您自行指定了目录. 请适当修改命令中的目录路径

## 导出软件镜像
:::tip

预计时长 10~20 分钟, 取决于硬盘速度
:::
在业务停机前, 您可以先导出 Docker 镜像库中的镜像文件.

可通过以下脚本进行实现

```shell
mkdir /mnt/tmp
mkdir /mnt/tmp/docker_image
docker image ls | tail -n +2 | while read image;do
    name=$(echo $image | awk '{print $1}')
    version=$(echo $image | awk '{print $2}')
    id=$(echo $image | awk '{print $3}')

    if [ "$version" == "<none>" ];then
        continue
    fi;
    hash_name=$(echo $image$id | md5sum | awk '{print $1}')
    echo "Saving $name (#$id) to /mnt/tmp/docker_image/$hash_name.img..."
    docker save $id | gzip > /mnt/tmp/docker_image/$hash_name.img
done;
```

## 复制 Docker 配置

通过以下命令复制运行时的 Docker 配置
```
cp -r /root/.docker /mnt/tmp/docker_user_config
```

## 业务停机

您可以通过以下命令来停止 Docker 系统服务来进行业务停机

```shell
systemctl stop docker.service
```
:::tip

如中途需要复原业务, 可通过以下命令启动 Docker 系统服务

```shell
systemctl start docker.service
```
:::

## 复制数据到硬盘上

### 控制中心
快速复制 (跳过镜像文件)
```shell
rsync -a --info=progress2 --exclude '/home/dcim/core/storage/slow' /home/dcim/core /mnt/tmp/core
```

完整复制
```shell
rsync -a --info=progress2 /home/dcim/core /mnt/tmp/core
```

### 受控
快速复制 (跳过镜像文件)
```shell
rsync -a --info=progress2 --exclude '/home/dcim/agent/storage/slow' /home/dcim/agent /mnt/tmp/agent
```

完整复制
```shell
rsync -a --info=progress2 /home/dcim/agent /mnt/tmp/agent
```

## 新服务器上操作

请使用命令: `mkdir /mnt/tmp` 创建恢复数据的目录, 用于挂载迁移数据的硬盘

并将迁移数据的硬盘挂载到目录 `/mnt/tmp` 上, 再继续操作

CheatSheet (命令速查表):

| 用途           | 命令                                |
| -------------- | ----------------------------------- |
| 列出所有块设备 | `lsblk`                               |
| 挂载硬盘       | `mount 存储迁移数据的硬盘 /mnt/tmp` |

## 还原数据

### Docker 用户配置文件
无返回则说明执行完成
```shell
cp -r /mnt/tmp/docker_user_config /root/.docker
```

### Docker 软件镜像还原
```shell
ls -1 /mnt/tmp/docker_image | while read image;do
    docker load $image
done
```

### 复制数据到硬盘上

#### 控制中心
```shell
mkdir -p /home/dcim/core
rsync -a --info=progress2 /mnt/tmp/core /home/dcim/core
```

#### 受控
```shell
mkdir -p /home/dcim/agent
rsync -a --info=progress2 /mnt/tmp/agent /home/dcim/agent
```

### 启动业务
#### 控制中心
```shell
cd /home/dcim/core
docker-compose up -d
```

#### 受控
```shell
cd /home/dcim/agent
docker-compose up -d
```