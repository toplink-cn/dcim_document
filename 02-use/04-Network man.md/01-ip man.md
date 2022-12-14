# IP管理设置

## IP分组

### - IP分组基本介绍

IP分组用于管理Toplink DCIM IP资产，便于IP的分类管理，分类依据可以按照IP供应商、IP使用类型（如CN2 、DDOS、PCCW等），等进行新建立分组名称，具体如下图所示。

![](./img/network%20ip%20group%20man%2000.png)


###  添加管理**IP分组**

DCIM导航栏>>网络管理>>ip分组>>添加  

添加以及管理ip分组可以直接在ip分组中进行设置，具体操作详情，如下图所示。

![](./img/network%20ip%20group%20man%2001.png)

## IP管理

###  添加&修改IP段

DCIM导航栏>>网络管理>>ip管理>>添加ip段  

在添加IP段时可按照拥有IP的最大掩码段进行录入，具体录入页面详情如下图所示。

![](./img/network%20ip%20man%2000.png)

:::tip **添加IP字段详解**

**标签：**设置待录入段的标签，一般设置为ip段的名称。  
**IP添加规则：**可以选择以ip段的方式进行添加，或者是按照自定义的方式进行添加。  
**IP段：**ip加掩码的形式进行录入添加，如192.168.0.0/24。  
**开始ip：**系统会根据掩码进行自动计算起始ip地址。  
**结束ip：**系统会根据掩码进行自动计算结束ip地址。  
**子网掩码：**系统会进行填充掩码号。  
**VLAN：**IP段所归属的vlan号，没有设置的话可以默认为0。  
**网关：**添加ip段的网关，可以选择第一个或者是最后一个ip作网关，也可以选择暂不设置。  
**DNS1  &  DNS2 ：**设置此ip段的dns,在使用此ip进行自动装系统时，会将此dns 设置到系统系统中。  
**网关设备：**此ip段是归属于哪个网关设备，直接进行选择关联就好。  
**机房：**此ip段是在哪个数据中心进行录入使用的。  
**自动分配：**在自动上架时，是否允许系统进行自动分配此ip段。  
**自动拆分/24：**大范围掩码段，如 **/18 、/16**可以设置录入后进行自动拆分为/24为单位的掩码段。  
**锁定：**是否锁定此ip段，锁定之后则不能进行分配分割等操作。  
**分组：**选择此IP段所归属的分组。  
**类型：**选择此ip的类型，如公网，ipmi，内网等 。  
**自定义标签：**ip段支持管理者进行自定义标签，以及标签内容。  
**备注：**给ip段进行填写备注，便于后续的管理和使用。  

:::

### 分割IP段

DCIM导航栏>>网络管理>>ip管理>>分割

分割IP段便于IP段的管理，以及将小网段进行分配至指定的服务器，具体操作如下所示。

![](./img/network%20ip%20man%2001.png)

分割具体的操作，，如下图所示。

![](./img/network%20ip%20man%2002.png)

:::tip **字段详解**

**子网掩码：**可以记性选择方需要细分的掩码。  
**网关：**可以选择分割之后的IP段所使用的网关。  

:::

###  补全IP地址

若IP段段中IP地址不完整，或者录入时有缺失，此时在IP段详IP地址页面 **[操作]**栏就会显示 **[补全]**。点击即可进行补全此IP段。详情详情如下图所示。

![](./img/network%20ip%20man%2003.png)

:::tip **字段详解**

**自动：**可以进行自动补全所缺失的全部IP地址。
**手动：**可以根据需要进行手动补全所缺失的IP地址。

:::


### 分配IP段

分配IP段至服务器时，有两种方式：一种是在IP段管理中进行分配，一种是在是在服务详情中进行添加IP。  

IP段管理中分配IP至设备，可以选择分配至服务器或者用户，具体如下图所示。

![](./img/network%20ip%20man%2004.png)


服务器详情中进行添加ip，具体如下图所示。


![](./img/network%20ip%20man%2005.png)

###  设置IP段所述网关设备


平台中IP段可以关联对应的网关设备，已达到在分配和删除IP段时，能够进行自主的添加和删除路由。具体IP段关联网关设备有两种方式。如下所示。  

IP管理中进行修改时，选择网关设备。

![](./img/network%20ip%20man%2007.png)


网关设备修改详情中进行关联ip段。

![](./img/network%20ip%20man%2008.png)
