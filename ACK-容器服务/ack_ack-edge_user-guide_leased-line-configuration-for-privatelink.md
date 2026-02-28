### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/)[操作指南](https://help.aliyun.com/zh/ack/ack-edge/user-guide/)[网络管理](https://help.aliyun.com/zh/ack/ack-edge/user-guide/network-management-overview/)专线接入配置私网连接

# 专线接入配置私网连接

更新时间：2025-08-17 21:32:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：专线环境下的网元配置](https://help.aliyun.com/zh/ack/ack-edge/user-guide/network-element-configuration-in-leased-line-environment)[下一篇：如何选择网络插件](https://help.aliyun.com/zh/ack/ack-edge/user-guide/how-to-choose-a-network-plug-in)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

操作步骤

创建系统组件容器镜像的终端节点

创建ACK集群管控地址的终端节点

配置域名解析

本文介绍如何通过配置私网连接（PrivateLink）为ACK Edge集群边缘节点安全、高效地访问ACK和ACR等云服务，解决网络冲突和无固定IP等问题。

## **背景信息**

ACK Edge集群支持通过专线接入网络。在集群接入过程中，边缘节点通常需要访问若干云服务的内网地址，可能会遇到如下问题：

- 100网段冲突：云服务通常默认使用 `100.64`段的IP地址。如果本地数据中心（IDC）也采用了同一网段，将不可避免地遭遇地址冲突，影响正常访问。

- 无固定访问IP：容器服务ACK的管控侧地址无法使用一个固定的访问IP。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0370845571/CAEQYBiBgMC3vt3SwhkiIGUyMWU3OGIwNjI2MDQ3YjA5MDRhNDdiYzIyZGRhNDc25503436_20250728104440.732.svg)

私网连接可帮助您在阿里云VPC内，通过专有网络安全、稳定地访问跨VPC的服务。配置私网连接能够有效解决前述网络冲突和无固定IP的问题。

ACK Edge相关的云产品均支持私网连接。本文主要介绍ACR和ACK两个云产品的配置方法，其它云产品的根据以下表格参阅。

| **云产品** | **说明** | **文档连接** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **云产品** | **说明** | **文档连接** |
| 容器镜像服务 | 边缘节点的系统组件镜像需访问 ACR 服务。 | [创建系统组件容器镜像的终端节点](https://help.aliyun.com/zh/ack/ack-edge/user-guide/leased-line-configuration-for-privatelink#ea4426e5a67y3 "") |
| ACK Edge集群 | 边缘节点接入时需访问 ACK 管控地址。 | [创建ACK集群管控地址的终端节点](https://help.aliyun.com/zh/ack/ack-edge/user-guide/leased-line-configuration-for-privatelink#597518f3e2y4x "") |
| 对象存储 | - 边缘节点接入过程中需要从 OSS 下载依赖包。<br>  <br>- ACR 镜像仓库拉取镜像时依赖 OSS。 | [通过PrivateLink私网访问OSS资源](https://help.aliyun.com/zh/oss/user-guide/access-oss-via-privatelink-network "") |
| 日志服务 | 若安装日志组件，需要访问 SLS 管控地址。<br>通过私网连接可安全访问日志服务。 | [通过私网连接（PrivateLink）访问日志服务](https://help.aliyun.com/zh/sls/sls-private-network-connection "") |

## **前提条件**

已 [创建ACK Edge 集群](https://help.aliyun.com/zh/ack/ack-edge/user-guide/create-an-ack-edge-cluster-1 "")，并配置了私网连接。私网连接的费用详情请参见 [私网连接计费说明](https://help.aliyun.com/zh/privatelink/private-link-billing-description "")。

**说明**

ACK 私网连接的配置采用白名单方式开放，请您[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请开通。开通后才能在创建终端节点中选择 ACK/ACR 的终端节点服务。

## 操作步骤

### 创建系统组件容器镜像的终端节点

您可以按照以下步骤操作，完成容器镜像服务终端节点的创建。终端节点创建成功后，您将获得对应可用区的域名和 IP 信息。

**说明**

此处配置的终端节点不支持代理 OSS 请求。如需通过私网连接访问 OSS 资源，请参见 [通过PrivateLink私网访问OSS资源](https://help.aliyun.com/zh/oss/user-guide/access-oss-via-privatelink-network "")。

1. 登录 [终端节点服务控制台](https://vpcnext.console.aliyun.com/endpointservice/eu-central-1/endpointservices)。

2. 在顶部菜单栏处，选择终端节点服务的地域。



**说明**





需与 ACK Edge 集群保持同一地域。本文以 **华东1（杭州）** 为例。

3. 在顶部菜单栏处，选择终端节点服务的地域。

4. 在 **终端节点** 页面，单击 **接口终端节点** 页签，然后单击 **创建终端节点**。

5. 在 **创建终端节点** 页面，根据以下信息配置终端节点，然后单击 **确定创建**。




| **参数** | **描述** | **示例值** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **描述** | **示例值** |
| **节点名称** | 输入自定义终端节点的名称。 | test1 |
| **终端节点类型** | 选择 **接口终端节点**。 | **接口终端节点** |
| **终端节点服务** | 您可以通过以下两种方式设置终端节点服务：<br>   - 单击 **其他终端节点服务**，然后输入终端节点服务的名称，单击 **点击验证**，验证服务合法性。<br>     <br>   - 单击 **选择可用服务**，然后选择目标终端节点服务ID。 | **选择可用服务**，然后在输入框一栏中选择 **终端节点服务ID**，并输入目标ID搜索。<br>**说明**<br>系统ACR镜像仓库配置的终端节点服务 ID 请通过工单向技术支持咨询获取。 |
| **专有网络** | 选择需要创建终端节点的VPC。<br>本文选择Edge 集群的VPC。 | 目标ACK Edge 集群的VPC。 |
| **安全组** | 选择要与终端节点网卡关联的安全组，安全组可以管控VPC到终端节点网卡的数据通信。 | 目标端节点网卡关联的安全组。 |
| **可用区与交换机** | 选择终端节点服务对应的可用区，然后选择该可用区内的交换机。系统会自动在每个交换机下创建一个终端节点网卡。 | 可用区：<br>   - 杭州可用区G<br>     <br>   - 杭州可用区K<br>     <br>交换机：<br>   - 杭州可用区G内的交换机<br>     <br>   - 杭州可用区K内的交换机 |
| **资源组** | 选择终端节点所属的资源组。 | 目标资源组。 |


### **创建** ACK集群 **管控地址的终端节点**

您可以按照以下步骤创建 ACK 集群管控地址的终端节点。创建完成后，您将获得该终端节点在可用区对应的域名和 IP 信息。

1. 在 **终端节点** 页面，单击 **接口终端节点** 页签，然后单击 **创建终端节点**。

2. 在 **创建终端节点** 页面，根据以下信息配置终端节点，然后单击 **确定创建**。




| **参数** | **描述** | **示例值** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **描述** | **示例值** |
| **节点名称** | 输入自定义终端节点的名称。 | test2 |
| **终端节点类型** | 选择 **接口终端节点**。 | **接口终端节点** |
| **终端节点服务** | 您可以通过以下两种方式设置终端节点服务：<br>   - 单击 **其他终端节点服务**，然后输入终端节点服务的名称，单击 **点击验证**，验证服务合法性。<br>     <br>   - 单击 **选择可用服务**，然后选择目标终端节点服务ID。 | **选择可用服务**，然后在输入框一栏中选择 **终端节点服务ID**，并输入目标ID搜索。<br>**说明**<br>ACK Edge集群管控终端节点服务ID请通过工单向技术支持咨询获取。 |
| **专有网络** | 选择需要创建终端节点的VPC。<br>本文选择Edge 集群的VPC。 | 目标ACK Edge 集群的VPC。 |
| **安全组** | 选择要与终端节点网卡关联的安全组，安全组可以管控VPC到终端节点网卡的数据通信。 | 目标端节点网卡关联的安全组。 |
| **可用区与交换机** | 选择终端节点服务对应的可用区，然后选择该可用区内的交换机。系统会自动在每个交换机下创建一个终端节点网卡。 | 可用区：<br>   - 杭州可用区G<br>     <br>   - 杭州可用区K<br>     <br>交换机：<br>   - 杭州可用区G内的交换机<br>     <br>   - 杭州可用区K内的交换机 |
| **资源组** | 选择终端节点所属的资源组。 | 目标资源组。 |


### **配置域名解析**

配置好终端节点后，您需要确保在本地环境中，将 [边缘节点需要访问的域名（出方向）](https://help.aliyun.com/zh/ack/ack-edge/user-guide/network-configuration-for-public-network-access#e58838d46atsp "") 解析到终端节点的域名或IP。例如，若您云下有自建DNS基础设施，可以直接配置CNAME条目，将目标域名指向终端节点所暴露的域名。也可以通过配置PrivateZone 服务来配置域名解析，具体详情请参见 [云下访问云上域名](https://help.aliyun.com/zh/dns/implementation-of-on-cloud-off-cloud-domain-name-resolution-exchange-based-on-intranet-dns-resolution#9af988124dwr7 "")。