### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 创建Argo工作流集群

# 创建Argo工作流集群

更新时间：2026-02-02 07:00:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：阿里云容器Argo工作流集群服务条款](https://help.aliyun.com/zh/ack/ack-argo-workflow-cluster/support/alibaba-cloud-container-argo-workflow-cluster-service-terms)[下一篇：获取集群KubeConfig并通过kubectl工具连接集群](https://help.aliyun.com/zh/ack/ack-argo-workflow-cluster/user-guide/obtain-the-cluster-kubeconfig-and-connect-to-the-cluster-using-kubectl)

该文章对您有帮助吗？

反馈

- 本页导读

适用范围

创建工作流集群

删除工作流集群

相关文档

容器Argo工作流集群采用无服务器模式，使用阿里云容器计算服务ACS运行工作流，通过优化Kubernetes集群参数，实现大规模工作流的高效弹性调度，同时配合BestEffort，优化成本。本文介绍如何创建容器Argo工作流集群。

## 适用范围

- [已开通分布式云容器平台ACK One](https://www.aliyun.com/product/aliware/adcp)。

- 已开通容器计算服务ACS。

- 已 [创建专有网络和交换机](https://help.aliyun.com/zh/vpc/user-guide/create-and-manage-a-vpc#section-znz-rbv-vrx "")

- RAM用户需具有AliyunAdcpFullAccess权限才能创建集群。具体操作，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ack/grant-permissions-to-a-ram-user-1#section-7ls-hxr-q81 "")。


## 创建工作流集群

1. 登录 [容器Argo工作流集群控制台](https://csnew.console.aliyun.com/#/next/argowf)。

2. 单击 **创建工作流集群**，在弹出的面板中填写相关参数，然后单击 **下一步**。完成依赖检查后，单击 **创建集群**。




| **参数** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **描述** |
| **集群名称** | 填写集群的名称。<br>> 长度为1～63个字符，可包含字母、数字、下划线（\_）或中划线（-），且仅允许以字母开头。 |
| **地域** | 选择集群所在的地域。 |
| **专有网络** | 设置集群的专有网络VPC，在下拉列表中选择已创建的VPC。 |
| **虚拟交换机** | 在下拉列表中选择已创建的交换机。 |
| **资源组** | 将集群归属于选择的 [资源组](https://help.aliyun.com/zh/ecs/user-guide/resource-groups#concept-fdn-wtm-cgb "")，便于权限管理和成本分摊。<br>> 一个资源只能归属于一个资源组。 |
| **标签** | 为集群绑定键值对 [标签](https://help.aliyun.com/zh/resource-management/tag/product-overview/tag-overview "")，作为云资源的标识。 |
| **API Server访问** | 无需设置，创建容器Argo工作流集群时会默认自动新建一个按量付费的私网CLB实例作为API Server的内网连接端点。<br>**重要**<br>请勿删除该实例，否则会导致集群API Server无法访问。 |
| **创建并绑定EIP** | 开启后，集群API Server使用的CLB实例将绑定一个弹性公网IP，使集群API Server支持公网访问。 |
| **开启组件及审计日志** | 同时将启用集群API Server审计功能，收集对Kubernetes API的请求以及请求结果。如需后续启用，请参见 [采集ACK集群容器日志](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/collect-text-logs-from-ack-clusters-using-daemonset-deployed-logtail-agents#task-1797722 "")、 [使用集群API Server审计功能](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/work-with-cluster-auditing "")。 |


## 删除工作流集群

**重要**

删除容器Argo工作流集群前，请先删除集群上的工作流，以释放ACS资源。

1. 登录 [容器Argo工作流集群控制台](https://csnew.console.aliyun.com/#/next/argowf)。

2. 在需要删除的集群右侧操作列单击**![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8756100771/p1028718.png)** \> **删除集群**，然后在弹出的提示框中单击 **确定**。


## 相关文档

使用集群前，需 [开启Argo Server并访问工作流控制台](https://help.aliyun.com/zh/ack/ack-argo-workflow-cluster/user-guide/enable-argo-server-for-a-workflow-cluster "")。