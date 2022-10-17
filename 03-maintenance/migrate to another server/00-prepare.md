# 准备工作

在本章中, 我们将假设您的原服务器依旧可用.

该章节将迁移前的所有准备工作以及步骤均按顺序讲述

## 计算迁移时间

登陆原服务器, 进入对应软件数据目录

管理中心: `/home/dcim/core`

被控: `/home/dcim/agent`

进入相应目录, 输入:
```
du -d2 -h 软件数据目录
```
例如:
```
# du -d2 -h /home/dcim/core/
8.0K	    /home/dcim/core/run
69G	        /home/dcim/core/storage/slow - 慢速存储目录 | 系统镜像文件 / Windows 驱动
1.3G	    /home/dcim/core/storage/fast - 快速存储目录 | 数据库 / 日志 / 临时文件
180G	    /home/dcim/core/storage
181.3G	    /home/dcim/core/
```
:::tip

如条件允许, 您可以选择只迁移快速存储目录. 以便业务快速上线

如您通过网络迁移(1000Mbps)

上述例子的快速迁移时间约为:

`1.3GB / 1000Mbps = 10.4 秒`

完整迁移为

`70GB / 1000Mbps = 24 分钟`
:::


## 计划停机时间
迁移服务器十分简单, 但是为了避免新老服务器中的数据出现差异

我们强烈建议您计划停机时间, 以便减少迁移操作中发生的问题


## 清理旧版本软件镜像

在原服务器上输入 `docker image prune` 可清理过时的软件镜像

:::info

该操作会加快迁移速度. 如可能请尽量操作

软件自身会自动清理超过 60 天的软件镜像, 保留旧镜像是为了一些意外情况下需要回滚老版本.

通常情况下可直接清理过时镜像
:::

## 准备新服务器

请按照[安装章节](/docs/dcim/install/intro)中, 准备新的服务器.

## 安装软件
您需要在原和目标服务器中安装 `rsync` 软件

CentOS/RedHat 系系统 (.rpm)
```
yum install rsync -y
```
或
```
dnf install rsync -y
```

Debian/Ubuntu 系系统 (.deb)
```
apt install rsync -y
```

## 准备迁移目录

文中存放迁移数据的目录均定为 `/mnt/tmp`

### 本地迁移
请准备一个 U盘 / 硬盘, 用于存放待迁移的数据

CheatSheet (命令速查表):

| 用途           | 命令                                |
| -------------- | ----------------------------------- |
| 列出所有块设备 | `lsblk`                               |
| 格式化硬盘     | `mkfs.ext4 存储迁移数据的硬盘`      |
| 挂载硬盘       | `mount 存储迁移数据的硬盘 /mnt/tmp` |

### 网络迁移
准备一个目录 (`/mnt/tmp`), 并该目录可存放待迁移的数据