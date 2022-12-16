# 平台授权问题

* ##   服务器时间

您可以检查服务器时间是否有问题. 为了安全性, 授权服务器只接受时间相差 +- 30 秒内的授权请求.

服务器通常预装 NTP 时间同步工具, 您可以通过以下命令来查看是否安装.

### 检查服务器校时软件

以下命令/软件选其一即可

#### systemd-timesyncd
```
systemctl status systemd-timesyncd
```

#### chronyd
```
systemctl status chronyd
```

### 安装服务器校时软件

以下命令/软件选其一即可

#### systemd-timesyncd

##### CentOS / RedHat / RockyLinux / AlmaLinux
```
yum install -y systemd-timesyncd
```

##### Debian / Ubuntu
```
apt update && apt install -y systemd-timesyncd
```

#### chronyd

##### CentOS / RedHat / RockyLinux / AlmaLinux
```
yum install -y chrony
```

##### Debian / Ubuntu
```
apt update && apt install -y chrony
```

* ##  许可证更新

DCIM导航栏>>设置>>系统设置>>授权信息  

当更改DCIM 平台所用域名，以及所用IP时则需要进行及时更新许可证信息，以确保授权验证正常通讯，具体操作详情价如下图所示。

![](./image/license%2000.png)

将新证书进行上传即可更新授权到新的域名或者是IP.