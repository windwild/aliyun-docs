### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/)ACK托管集群网络规划

# ACK托管集群网络规划

更新时间：2026-02-04 04:05:30

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：容器网络插件Terway与Flannel对比](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-between-terway-and-flannel)[下一篇：使用Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

网络规模规划

地域和可用区

VPC数量

交换机数量

集群规模

网络通信规划

单VPC内单集群

单VPC内多集群

多集群跨VPC互联

云上集群与IDC通信

容器网络插件规划

功能规划

网段规划

相关文档

建议您提前规划集群的规模、网络功能需求、专有网络VPC相关配置（VPC自身、交换机等）和集群网络相关配置（容器网络插件CNI、容器网段、服务网段等），确保网络资源的高效利用，为后续业务扩展预留充足空间。本文介绍如何在阿里云专有网络VPC环境中规划符合业务需求的ACK托管集群网络结构。

## **网络规模规划**

### **地域和可用区**

在同一地域内，各可用区之间内网互通。各可用区之间可以实现故障隔离，即一个可用区出现故障时，不会影响其他可用区的正常运行。同一可用区内实例之间的网络延时更小，其用户访问速度更快。您可以综合考虑以下因素来进行地域和可用区规划。

|     |     |
| --- | --- |
| **考虑因素** | **选择说明** |
| 业务场景对时延的要求 | 业务最终服务的用户和资源部署地域的距离越近，网络时延越低，访问速度越快。 |
| 服务支持的地域和可用区 | 不同的阿里云云服务在每个地域/可用区的服务支持情况不同，库存售卖存在差异，建议您在选择地域/可用区时，确保云服务可用。 |
| 成本 | 不同地域的云服务价格可能会有所不同，建议您根据预算选择合适的地域。 |
| 高可用容灾 | 如果您的应用需要较高的容灾能力，您可选择在同一地域的不同可用区内进行部署以实现同城容灾。您也可选择在多地域部署以实现跨城容灾，满足更高的容灾能力需求。 |
| 合规性 | 您需要根据所在国家或地区的数据本地化要求与经营性备案政策选择符合合规要求的地域。 |

VPC是地域级别的资源，不支持跨地域部署。当您有多地域部署需求时，必须使用多个VPC。您可以使用VPC对等连接、云企业网等产品实现跨地域VPC间互通。VPC中的交换机是可用区级别的资源，有以下事项您需要注意：

- 当您因为云服务库存因素选择多个可用区时，您需要提前预留足够的地址段，并考虑到可用区绕行可能造成延时增加；

- 部分地域仅提供1个可用区，例如华东5 （南京-本地地域-关停中），若您有同城容灾需求，建议您谨慎考虑选择该地域。


**说明**

关于ACK各产品开服地域的信息，请参见 [开服地域](https://help.aliyun.com/zh/ack/product-overview/supported-regions "")。

### **VPC数量**

VPC为您提供安全灵活的网络环境，不同VPC之间完全隔离，同一VPC内私网互通。您可以按需规划您的VPC数量。

|     |     |
| --- | --- |
|  | **适合场景** |
| 单VPC | - 业务规模较小，仅部署在一个地域且不同业务之间没有网络隔离需求；<br>  <br>- 初次使用VPC，推荐使用单个VPC用于快速上手以了解产品功能；<br>  <br>- 关注成本，不希望管理跨VPC通信的复杂配置与潜在费用。 |
| 多VPC | - 业务规模较大，需要部署在不同地域；<br>  <br>- 单地域的多个业务系统存在网络隔离需求；<br>  <br>- 业务架构复杂，涉及的众多服务与团队需要独立VPC管理各自资源。 |

**说明**

每个用户在单个地域内可创建的VPC数量默认为10个。您可以前往 [配额管理页面](https://vpc.console.aliyun.com/quota) 或 [配额中心](https://quotas.console.aliyun.com/products/vpc/quotas?query=vpc_quota_instances_num) 提升配额。

### **交换机数量**

交换机是可用区级别的资源，VPC中的所有云服务都部署在交换机中。交换机划分有助您合理规划IP地址资源，同一VPC内的交换机默认私网互通。

|     |     |
| --- | --- |
| **考虑因素** | **选择说明** |
| 基于业务场景对时延的要求 | 同一地域不同可用区之间的网络通信延迟很小，但系统调用复杂、跨可用区调用等原因可能会增加系统的网络延迟。 |
| 高可用和容灾 | 使用一个VPC时，建议您尽量使用至少两个交换机，并且将两个交换机部署在不同可用区以实现跨可用区容灾。使用多个可用区部署不同业务，统一配置并管理安全管控规则，能够显著提升系统的高可用性和容灾能力。 |
| 业务规模与业务划分 | 通常情况下，您可以根据业务模块进行交换机规划，将不同业务模块部署在不同交换机。例如，您可创建多个交换机将Web层、逻辑层和数据层服务部署在不同交换机以实现标准Web应用架构的托管。 |

您可以根据以下原则规划交换机：

- 使用一个VPC时，也请尽量使用至少两个交换机，并且将两个交换机分布在不同可用区，这样当其中一个可用区的交换机发生故障时，可以切换到另一个可用区的交换机，从而实现跨可用区容灾。

同一地域内不同可用区之间的网络通信延迟很小，但也需要经过业务系统的适配和验证。由于系统调用复杂、跨可用区调用等原因可能会增加系统的网络延迟。建议您对系统进行优化及适配，以满足您对高可用和低延迟的实际需求。

- 具体使用多少个交换机还和系统规模、系统规划有关。通常情况下，您可以根据业务属性在VPC内进行交换机规划。例如，对于直接访问公网的业务部署在一个公有交换机中，其他业务可以根据业务类型进行划分。使用多个可用区部署不同业务有利于安全管控规则的配置与统一管理。


**说明**

单个VPC支持创建的交换机的数量默认为150个，您可以前往 [配额管理页面](https://vpc.console.aliyun.com/quota) 或 [配额中心](https://quotas.console.aliyun.com/products/vpc/quotas?query=vpc_quota_vswitches_num) 提升配额。

### **集群规模**

|     |     |     |     |
| --- | --- | --- | --- |
| **集群节点规模** | **适用场景** | **VPC规划** | **可用区规划** |
| 小于100个节点 | 非核心业务 | 单VPC | 1个（推荐2个及以上） |
| 100个节点及以上 | 一般业务，需要多可用区 | 单VPC | 2个及以上 |
| 100个节点及以上 | 核心业务，对可靠性有较高要求、需要多地域 | 多VPC | 2个及以上 |

## **网络通信规划**

### **单VPC内单集群**

在创建VPC时，VPC的网段就已经确定，创建集群时要为Pod和服务指定一个与这个VPC地址范围不重叠的新网络段。这样就能确保集群内的网络通信，不会与外部的VPC网络发生冲突。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8295910771/CAEQVRiBgICnv9.EqxkiIDRjZjA1NGU3ZDgxMzQ4YmM5ODFkNzQwMTk1NGU4ZGIz4553391_20240801095024.466.svg)

### **单VPC内多集群**

一个VPC下创建多个集群。

- VPC地址是在创建VPC时已经确定。创建集群时，每个集群内的VPC网段、服务网段和Pod网段彼此间不能重叠。

- 所有集群之间的Pod网段不能重叠，但服务网段（虚拟网段）可以重叠。

- 在默认的网络模式下（Flannel），Pod的报文需要通过VPC路由转发，ACK托管集群会自动在VPC路由上配置到每个Pod网段的路由表。


**说明**

这种情况下集群部分互通，一个集群的Pod可以直接访问另一个集群的Pod和ECS，但不能访问另一个集群内部的服务（如Cluster IP类型的服务仅可在集群内部访问，如需暴露服务可以使用LoadBalancer类型的服务或Ingress等方式）。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8295910771/CAEQVRiBgICjiZGkqxkiIDA3MjNjYWVlNmJlNTQ3YTNiNWQ4YWMzYTUwODMzNTJl4553391_20240801095024.466.svg)

### **多集群跨VPC互联**

在如下使用场景中，建议您规划集群跨多个VPC互联。

多地域部署系统

多业务系统隔离

大规模业务系统构建

VPC是地域级别的资源，不支持跨地域部署。当您有多地域部署系统的需求时，必须使用多个VPC和多个集群。您可以通过使用 [VPC对等连接](https://help.aliyun.com/zh/vpc/vpc-peer-to-peer-connection "")、 [VPN网关](https://help.aliyun.com/zh/vpn/product-overview/what-is-vpn-gateway "")、 [云企业网](https://help.aliyun.com/zh/cen/product-overview/what-is-cen/ "") 等产品实现跨地域VPC间互通。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8295910771/CAEQVRiBgMDLl9ftqhkiIDM1YmMyNmJkMGNkMjQ0ZTBiMWIzNjhiNTliNDQwZDFk3794106_20230720103741.872.svg)

如果在一个地域的多个业务系统需要通过VPC进行严格隔离，例如生产环境和测试环境具备不同的安全和业务部署诉求，生产集群和测试集群分别部署到不同VPC可以提供更好的逻辑隔离与安全保障。您同样可以通过使用 [VPC对等连接](https://help.aliyun.com/zh/vpc/vpc-peer-to-peer-connection "")、 [VPN网关](https://help.aliyun.com/zh/vpn/product-overview/what-is-vpn-gateway "")、 [云企业网](https://help.aliyun.com/zh/cen/product-overview/what-is-cen/ "") 等产品实现同地域VPC间互通。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8295910771/CAEQVRiBgICd2N2EqxkiIDI5MTkyOGViMDI5OTQyNDU4YjY5Y2RkMTk5OWJhNWNm3794106_20230720103741.872.svg)

如果您的业务架构复杂，涉及的众多服务与团队需要独立VPC管理各自集群和资源，以提高灵活性和可管理性，建议您规划多个VPC和多个集群。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8295910771/CAEQVRiBgMDrsMWsqxkiIGJlZWE2OWVhODgwNzQ0ZThhYmY1NTczYWMyNTRhYzQ04537623_20240724152005.068.svg)

**重要**

为了避免在多集群跨VPC互联场景中出现IP冲突导致的路由错误等问题，新创建的集群需遵循以下网络规划要求：

- 不能和各个VPC的网段重叠

- 不能和其他集群的网段重叠

- 不能和其他集群Pod的网段重叠

- 不能和其他集群服务的网段重叠


### **云上集群与IDC通信**

与 [多集群跨VPC互联](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-cluster-network-planning#f3c93d46cdn14 "") 场景类似，同样存在VPC里部分地址段路由到IDC，集群的Pod地址就不能和这部分地址重叠。如果IDC里需要访问集群里的Pod地址，同样需要在IDC端配置边界路由器VBR的路由表。

![image](<Base64-Image-Removed>)

## 容器网络插件规划

ACK托管集群支持Terway和Flannel两种容器网络插件CNI，使用不同的插件会直接影响到支持的功能和网络配置的方式。如Terway支持NetworkPolicy，提供了基于策略的网络控制，而Flannel不支持；Terway容器网段是从VPC中分配的，而Flannel容器网段为指定的虚拟网段。

**重要**

容器网络插件需要在创建集群时进行安装，且集群创建后不支持更改。建议在明确网络功能需求之后，再选择适合您业务的网络插件。

### **功能规划**

| **对比项** | **Terway** | **Flannel** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **对比项** | **Terway** | **Flannel** |
| NetworkPolicy网络策略 | 支持 [在ACK集群使用网络策略](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-network-policies "")。 | 不支持。 |
| IPv4/IPv6双栈 | 支持 [为Pod配置IPv6公网带宽](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/allocate-ipv6-internet-bandwidth-to-a-pod "")。 | 不支持。<br>**说明**<br>ACK使用的是经过修改以适配阿里云云上环境的Flannel插件，并不与开源社区保持完全同步。ACK Flannel的更新记录，请参见 [Flannel](https://help.aliyun.com/zh/ack/product-overview/flannel "")。 |
| Pod固定IP | 支持 [为Pod配置固定IP及独立虚拟交换机、安全组](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-a-static-ip-address-a-separate-vswitch-and-a-separate-security-group-for-each-pod "")。 | 不支持。 |
| Pod绑定EIP | 支持 [为Pod挂载独立公网EIP](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/associate-an-eip-with-a-pod-1 "")。 | 不支持。 |
| 多集群互访 | 支持，多个集群的Pod之间只要设置安全组开放端口就可以互相通信。 | 不支持。 |

关于Terway和Flannel两种容器网络插件功能的详细对比，请参见 [容器网络插件Terway与Flannel对比](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-between-terway-and-flannel "")。

### **网段规划**

Terway网络模式

Flannel网络模式

![terway](<Base64-Image-Removed>)

**Terway配置示例**

- **Terway** **单可用区配置**


|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **专有网络网段** | **交换机网段** | **Pod交换机网段** | **服务网段** | **最大可分配Pod地址数** |
| 192.168.0.0/16 | 可用区I<br>192.168.0.0/19 | 192.168.32.0/19 | 172.21.0.0/20 | 8192 |

- **Terway多可用区配置**


|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **专有网络网段** | **交换机网段** | **Pod交换机网段** | **服务网段** | **最大可分配Pod地址数** |
| 192.168.0.0/16 | 可用区I 192.168.0.0/19 | 192.168.32.0/19 | 172.21.0.0/20 | 8192 |
| 可用区J 192.168.64.0/19 | 192.168.96.0/19 |


配置Terway模式网络时，需要设置的参数及注意事项如下：

- **专有网络**

  - 推荐您使用192.168.0.0/16、172.16.0.0/12、10.0.0.0/8三个RFC标准私网网段及其子网作为VPC的主IPv4网段，网段掩码有效范围为8～28位（不同的私网网段范围不同）。填写示例：`192.168.0.0/16`。



    **说明**





    若您有使用公网网段作为VPC网段等特殊需求，请前往 [配额中心](https://quotas.console.aliyun.com/white-list-products/csk/quotas) 提交`ack.white_list/supportVPCWithPublicIPRanges`配额申请。

  - 如果有多VPC场景或VPC与本地数据中心构建混合云场景，建议您使用RFC标准私网网段的子网作为VPC的网段且掩码不超过16位，且多个VPC间、VPC和本地数据中心的网段不能冲突。

  - IPv6网段在VPC开启IPv6后由VPC分配。如果您需要使用IPv6容器网络，请选择Terway网络插件。
- **交换机**

ECS使用的交换机，用于节点间网络通信。在VPC里创建交换机时指定的网段，必须是当前VPC网段的子集（可以和VPC网段一样，但不能超过）。配置网段时，请注意：

  - 交换机下ECS所分配到的地址，就是从这个交换机网段内获取的，推荐选择IP数量充足的交换机。

  - 一个VPC下，可以创建多个交换机，但交换机网段不能重叠。

  - **交换机** 和对应的 **Pod交换机** 需要在一个可用区内。
- **Pod交换机**

Pod地址从该交换机分配，用于Pod网络通信。Pod是Kubernetes内的概念，每个Pod具有一个IP地址。在VPC里创建交换机时指定的网段，必须是当前VPC网段的子集。配置网段时，请注意：

  - Terway网络模式下，Pod分配的Pod IP就是从这个交换机网段内获取的，推荐选择IP数量充足的交换机。

  - 该网段不能和 **服务网段** 重叠。
- **服务网段**



**重要**





服务网段创建成功后不能修改。





服务（Service）是Kubernetes内的概念，对应的是Service类型为ClusterIP时服务使用的地址，每个服务有自己的地址。配置网段时，请注意：

  - 服务地址只在Kubernetes集群内使用，不能在集群外使用。

  - 服务网段不能和 **交换机网段** 重叠。

  - 服务网段不能和 **Pod交换机网段** 重叠。
- **服务IPv6网段**

开启IPv6双栈后，您需要为服务配置IPv6网段。配置网段时，请注意：

  - 必须使用ULA地址，地址段范围需在fc00::/7内，且地址前缀长度在112~120之间。

  - 推荐和 **服务网段** 保持相同的可用地址数量。

![Flannel示意图](<Base64-Image-Removed>)

**Flannel网段配置示例**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **专有网络网段** | **交换机网段** | **容器网段** | **服务网段** | **最大可分配Pod地址数** |
| 192.168.0.0/16 | 192.168.0.0/24 | 172.20.0.0/16 | 172.21.0.0/20 | 65536 |

配置Flannel模式网络时，需要设置的参数及注意事项如下：

- **专有网络**

  - 推荐您使用192.168.0.0/16、172.16.0.0/12、10.0.0.0/8三个RFC标准私网网段及其子网作为VPC的主IPv4网段，网段掩码有效范围为8～28位（不同的私网网段范围不同）。填写示例：`192.168.0.0/16`。



    **说明**





    若您有使用公网网段作为VPC网段等特殊需求，请前往 [配额中心](https://quotas.console.aliyun.com/white-list-products/csk/quotas) 提交`ack.white_list/supportVPCWithPublicIPRanges`配额申请。

  - 如果有多VPC场景或VPC与本地数据中心构建混合云场景，建议您使用RFC标准私网网段的子网作为VPC的网段且掩码不超过16位，且多个VPC间、VPC和本地数据中心的网段不能冲突。

  - IPv6网段在VPC开启IPv6后由VPC分配。如果您需要使用IPv6容器网络，请选择Terway网络插件。
- **交换机**

ECS使用的交换机，用于节点间网络通信。在VPC里创建交换机时指定的网段，必须是当前VPC网段的子集（可以和VPC网段一样，但不能超过）。配置网段时，请注意：

  - 交换机下ECS所分配到的地址，就是从这个交换机网段内获取的。

  - 一个VPC下，可以创建多个交换机，但交换机网段不能重叠。
- **容器网段**



**重要**





容器网段创建成功后不能修改。





Pod地址从该网段内分配，用于Pod网络通信。Pod是Kubernetes内的概念，每个Pod具有一个IP地址。配置网段时，请注意：


  - 非VPC交换机，为虚拟网段。

  - 该网段不能和 **交换机网段** 重叠。

  - 该网段不能和 **服务网段** 重叠。


例如，VPC网段用的是172.16.0.0/12，Kubernetes的容器网段就不能使用172.16.0.0/16、172.17.0.0/16等，因为这些地址都包含在172.16.0.0/12里。

- **服务网段**



**重要**





服务网段创建成功后不能修改。





服务（Service）是Kubernetes内的概念，对应的是Service类型为ClusterIP时服务使用的地址，每个服务有自己的地址。配置网段时，请注意：

  - 服务网段只在Kubernetes集群内使用，不能在集群外使用。

  - 服务网段不能和 **交换机网段** 重叠。

  - 服务网段不能和 **容器网段** 重叠。

## 相关文档

- 其他相关规划：

  - 当您的ACK托管集群 [使用VPC附加网段](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-a-vswitch-to-a-cluster-based-on-a-secondary-cidr-block "") 或扩展新可用区后，需配置相应的网络规则以确保新增网段的业务正常运行。例如，在NAT网关中添加SNAT规则以允许从新网段访问公网资源（如拉取镜像），并在安全组中配置合适的访问规则。

  - 当您的业务规模扩大，需要综合考虑业务权限隔离、业务系统隔离等方面来进行统一账号架构设计。详细内容，请参见 [账号规划](https://help.aliyun.com/zh/vpc/vpc-network-planning#a199f7077fj2h "")。

  - 您可以结合网络连接场景与安全分层进行安全能力规划。详细内容，请参见 [安全能力规划](https://help.aliyun.com/zh/vpc/vpc-network-planning#8c802b37717l5 "")。

  - 您可以根据业务架构进行容灾能力规划，以保障数据的安全性和业务的持续性。详细内容，请参见 [容灾能力规划](https://help.aliyun.com/zh/vpc/vpc-network-planning#2ae807b5b32in "")。
- 集群网络通信：

  - 您可以使用弹性公网IP EIP暴露ACK托管集群的API Server，使集群API Server具有公网访问能力。详细内容，请参见 [实现从公网访问API Server](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/control-public-access-to-the-api-server-of-a-cluster "")。

  - 如果集群内部服务需要访问外部公网资源，例如拉取公网镜像、更新依赖库等，您可以为集群配置SNAT网关以开启访问公网能力。详细内容，请参见 [为集群开启访问公网能力](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-an-existing-ack-cluster-to-access-the-internet "")。
- 关于ACK托管集群相关网络问题，请参见 [网络管理FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-network-management#task-1545837 "")。