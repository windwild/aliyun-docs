### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[成本套件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-suite/)集成与拓展

# 成本洞察数据模型介绍

更新时间：2025-02-13 04:28:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

相关概念

成本数据模型

集群资产成本

Pod分摊成本

命名空间、应用成本

相关文档

在ACK集群中，Pod作为最小的可部署单元，是衡量集群成本的关键因素。但不同Pod可能有不同的资源配置、调度策略和生命周期，导致其成本估算较为复杂。ACK提供一种通用性的成本数据模型定义和计算方法，帮您准确地衡量云上ACK集群的成本，并将成本分摊给不同维度（集群、命名空间、应用等）的业务单元。

## 相关概念

下表为本文涉及的概念及解释。

|     |     |
| --- | --- |
| **概念** | **说明** |
| 集群总成本 | 运行一个ACK集群所需的全部成本。 |
| 集群资产成本 | 集群下所有云资源账单的总和。 |
| 集群间接成本 | 管理ACK集群所需的额外费用或间接开销，例如集群管理费用。 |
| 集群分配成本 | 集群中已分配的空间按比例分摊集群资产成本时，分摊的成本数额。 |
| 集群闲置成本 | 集群中未被分配的空间按比例分摊集群资产成本，分摊的成本数额。 |
| Pod分摊成本 | 一个Pod在特定周期内分摊集群资产成本的数额。 |

一个ACK集群的总成本包括集群资产成本和集群间接成本：`集群总成本 = 集群资产成本 + 集群间接成本`。

集群资产成本可以进一步区分为集群分配成本和集群闲置成本：`集群资产成本 = 集群分配成本 + 集群闲置成本`。

集群分配成本由Pod成本分摊确定，表示集群内所有Pod分摊的成本总和，是集群资产成本中已被分配的部分：`集群分配成本 = Σ （集群下Pod分摊成本）`

关系如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0198349371/CAEQRxiBgMD0uqHUgRkiIDFlNjZjZTg3Y2Y2MzRkYTE5OTBiZDcyNWI1NzRjNjdm4259974_20240313142406.644.svg)

## **成本数据模型**

### 集群资产成本

一个ACK集群通常包含节点、负载均衡、磁盘等基础云资源，以及Prometheus、NAT网关等可选云资源。集群资产成本是集群关联云资源的账单总和。

- 集群自动创建的云资源：在ACK集群中，可以通过集群ID的唯一标签（`ack.aliyun.com:<集群ID>`）来拆分集群关联云资源的全部账单，在账单累加后得到集群的总资产成本。

- 非集群自动创建的云资源：可以为这些云资源手动添加集群ID的资源标签，使其纳入集群资产成本统计范围。


### Pod分摊成本

#### **计算公式**

Pod通常并不直接出账，需要从集群资产成本中按比例拆算Pod分摊的成本，从而准确聚合集群不同维度的业务账单。因此，计算一个Pod的分摊成本时，核心是计算一个Pod在集群中的成本占比。

`Pod分摊成本 = Pod成本占比 * 集群资产成本`

Pod成本占比是Pod模拟成本在待分摊总成本的占比。

`Pod成本占比 = Pod模拟成本 / 待分摊总成本`

Pod模拟成本由Pod模拟单价和时长决定。要计算一个Pod的模拟单价，需要考虑Pod上各资源（例如CPU、内存、GPU）的分配量以及资源单价。

`Pod模拟成本 = Pod模拟单价 * 时长`

`Pod模拟单价 = Σ（资源单价 * 资源分配量 ）`

* * *

资源单价是决定Pod成本的核心因素，在不同场景可能存在多种单价定价方式。您可以直接从云服务商获取（已知资源单价），也可以自定义资源单价（未知资源单价）进行内部成本核算。

#### **示例一：已知计算资源单价**

例如，在常见的通过计算资源估算Pod成本的场景下，您可以参见以下公式完成Pod成本的分摊：

`Pod成本占比 = Pod模拟成本 / Σ（集群下Node成本）`

`Pod模拟成本 = （CPU单价 * CPU分配量 + 内存单价 * 内存分配量 + GPU单价 * GPU分配量 ）* 时长`

#### **示例二：未知计算资源单价**

对于未直接提供计算资源单价的场景（例如阿里云ECS直接提供了节点总价格），需要使用权重分摊模型拆分计算。权重分摊的方式给模型自定义带来更多灵活度。

`Pod计算资源的单价 = 资源权重 * 节点单价 / 节点资源总量`

`Σ（资源权重） = 1`

此时，资源权重是决定资源价值的核心因素。ACK默认使用资源调度水位来决定该资源在集群中的“昂贵”程度，即根据资源调度水位的占比确定资源的推荐权重。您也可以根据实际情况自定义权重数值。

### **命名空间、应用成本**

参见前文完成Pod分摊成本的计算后，您可以通过聚合Pod分摊成本，进一步计算命名空间、应用（工作负载）的成本。

命名空间是一组具有相同字段的Pod的聚合。

`命名空间成本 = Σ（命名空间下Pod的分摊成本）`

工作负载是命名空间下具有相同Label的Pod的聚合。

`工作负载成本 = Σ（相同Label Pod的分摊成本）`

## **相关文档**

- 您可以通过HTTP API命令查看上报数据，便于您基于成本数据进行二次开发，请参见 [通过API获取成本数据概述](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-calling-an-api-to-query-cost-insights-data "")。

- 您可以基于集群调度水位估算Pod成本，包括单资源（CPU、内存）估算和权重混合（CPU-内存混合）的资源估算，请参见 [成本估算策略介绍](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-allocation-model-overview "")。