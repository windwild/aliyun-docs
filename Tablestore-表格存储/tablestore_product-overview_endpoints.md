### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[产品简介](https://help.aliyun.com/zh/tablestore/product-overview/)[基础概念](https://help.aliyun.com/zh/tablestore/product-overview/basic-concepts/)服务地址

# 服务地址

更新时间：2025-01-08 22:31:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：实例](https://help.aliyun.com/zh/tablestore/product-overview/instance-of-tablestore)[下一篇：读写吞吐量](https://help.aliyun.com/zh/tablestore/product-overview/read-and-write-throughput)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

服务地址类型

公网地址

VPC地址

经典网地址

公网（双栈）地址

获取服务地址

每个表格存储实例对应一个服务地址（Endpoint），应用程序进行表和数据操作时需要指定服务地址。不同访问场景下需使用相应的服务地址格式。

**说明**

每个地域对应的RegionID请参见 [地域](https://help.aliyun.com/zh/tablestore/product-overview/regions#concept-dpr-lmj-bfb "")。

## **注意事项**

当前只有华东1（杭州）、华东2（上海）、华北1（青岛）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华南1（深圳）、西南1（成都）和中国香港地域的实例支持公网（双栈）地址。

## 服务地址类型

服务地址包括公网地址、公网（双栈）地址、VPC地址和经典网地址四种类型，通过不同网络访问表格存储实例时需要使用相应服务地址。

| **访问场景** | **选择Endpoint** |
| --- | --- |

|     |     |
| --- | --- |
| **访问场景** | **选择Endpoint** |
| 通过互联网访问 | 根据客户端支持的IP协议，使用 **公网地址** 或者 **公网（双栈）地址**。<br>通过互联网访问的延迟较高，建议选择其他方式进行访问。<br>**重要**<br>- 如果客户端为IPv6协议，则只能使用 **公网（双栈）地址**。<br>  <br>- 如果客户端不支持IPv6协议，则使用 **公网地址** 或者 **公网（双栈）** 地址均可。 |
| 通过专有网络访问 | 使用 **VPC地址**。 |
| 通过经典网络访问 | 使用 **经典网地址**。 |

**说明**

关于专有网络和经典网络的更多信息，请参见 [网络类型](https://help.aliyun.com/zh/ecs/user-guide/network-types#concept-nfj-dz2-5db "")。

### 公网地址

从互联网访问表格存储时可使用公网地址。

**说明**

通过互联网访问表格存储将产生外网下行流量费用。更多信息，请参见 [计费概述](https://help.aliyun.com/zh/tablestore/product-overview/billing-overview/#concept-w4k-2tj-bfb "")。

- 服务地址格式















```http
https://instanceName.RegionID.ots.aliyuncs.com
```

- 示例

华东1（杭州）地域中实例myInstance的服务地址为`https://myInstance.cn-hangzhou.ots.aliyuncs.com`。


### VPC地址

从专有网络访问表格存储时使用VPC地址。

- 服务地址格式















```http
https://instanceName.RegionID.vpc.tablestore.aliyuncs.com
```

- 示例

华东1（杭州）地域中应用程序从VPC访问实例myInstance的服务地址为`https://myInstance.cn-hangzhou.vpc.tablestore.aliyuncs.com`。


### 经典网地址

从同地域经典网络的ECS服务器访问表格存储时使用经典网地址。

**说明**

应用程序从同地域的经典网络ECS服务器上通过内网访问表格存储，可以获得更低的响应延迟，且不会产生外网流量。

- 服务地址格式















```http
https://instanceName.RegionID.ots-internal.aliyuncs.com
```

- 示例

华东1（杭州）地域中从经典网络的ECS服务器访问实例myInstance的服务地址为`https://myInstance.cn-hangzhou.ots-internal.aliyuncs.com`。


### 公网（双栈）地址

从互联网访问表格存储时可使用公网（双栈）地址。

**说明**

通过互联网访问表格存储将产生外网下行流量费用。更多信息，请参见 [计费概述](https://help.aliyun.com/zh/tablestore/product-overview/billing-overview/#concept-w4k-2tj-bfb "")。

- 服务地址格式















```http
https://instanceName.RegionID.tablestore.aliyuncs.com
```

- 示例

华东1（杭州）地域中实例myInstance的服务地址为`https://myInstance.cn-hangzhou.tablestore.aliyuncs.com`。


## 获取服务地址

1. 登录[表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择资源组和地域。

3. 在 **概览** 页面，单击实例名称或在操作栏中单击 **实例管理**。

在 **实例详情** 页签的 **实例访问地址** 即是该实例的Endpoint。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5596836371/p892072.png)