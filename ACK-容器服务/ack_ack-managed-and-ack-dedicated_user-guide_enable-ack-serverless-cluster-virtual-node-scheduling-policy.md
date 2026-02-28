### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[节点与节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/nodes-and-node-pools/)[虚拟节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/virtual-node-overview/)[调度Pod至虚拟节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-and-introduction-of-virtual-node-scheduling-scheme-ack/)开启集群虚拟节点调度策略

# 开启集群虚拟节点调度策略

更新时间：2025-03-06 03:21:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：调度Pod至虚拟节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-and-introduction-of-virtual-node-scheduling-scheme-ack/)[下一篇：调度至Arm虚拟节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/schedule-workloads-to-arm-based-virtual-nodes)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

注意事项

步骤一：确认组件已安装且版本适用

步骤二：确认已开启调度功能

开启虚拟节点调度策略后，ACK集群中的应用可以通过使用Kubernetes原生的Pod间亲和、地域间拓扑打散或节点亲和实现高可用、低时延等能力。

## **前提条件**

已创建v1.22版本及以上的ACK托管集群Pro版。具体操作，请参见[创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/ "")、 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。

## **注意事项**

- Pod上设置的对于其他Pod的反亲和，可能导致本Pod无法调度，请谨慎使用。

- Pod上设置的对于虚拟节点的反亲和，可能导致Pod无法调度，请在提交Pod时进行检查。

- Pod调度时，会进行库存查询以及集群状态更新。相较于未开启此功能，单个Pod的处理速度约有1秒的差异。目前，并发调度的吞吐量极限约为每秒300个Pod。若对Pod调度速度以及并发吞吐量有需求，请谨慎开启。


## 步骤一：确认组件已安装且版本适用

虚拟节点开启调度策略依赖于Kube Scheduler以及ACK Virtual Node两个组件，且两个组件的版本需符合要求。请按照以下步骤确认组件安装情况以及版本。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**运维管理** \> **组件管理**。

3. 在 **核心组件** 区域，确认以下组件已安装且版本符合要求。如果不符，请单击卡片右下角的 **安装** 或 **升级**。


   - Kube Scheduler：5.9及以上

   - ACK Virtual Node：v2.10.0及以上


## 步骤二：确认已开启调度功能

1. 单击Kube Scheduler组件卡片右下角的 **配置**。

2. 确认已勾选 **开启虚拟节点调度**，单击 **确定**。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7520262071/p747539.png)