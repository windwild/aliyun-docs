### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[动态与公告](https://help.aliyun.com/zh/ack/product-overview/announcements-and-updates/)[组件变更](https://help.aliyun.com/zh/ack/product-overview/components/)【组件升级】升级CCM组件公告

# 【组件升级】升级CCM组件公告

更新时间：2025-01-14 04:50:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：【组件升级】NPD升级公告](https://help.aliyun.com/zh/ack/product-overview/component-upgrades-update-ack-node-problem-detector)[下一篇：【组件升级】CoreDNS升级公告](https://help.aliyun.com/zh/ack/product-overview/update-coredns)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

升级CCM组件

为了提升ACK集群内LoadBalancer服务的稳定性，建议您升级集群的Cloud Controller Manager组件至最新版本。本文介绍如何升级Cloud Controller Manager组件版本。

## 背景信息

- 低于v1.9.3.380版本的Cloud Controller Manager组件存在以下问题，可能会影响ACK集群内LoadBalancer服务的稳定性。


  - 默认服务器组更新异常。

  - 存在同名虚拟服务器组，导致虚拟服务器组更新异常。


更多信息，请参见 [Cloud Controller Manager](https://help.aliyun.com/zh/ack/product-overview/cloud-controller-manager#concept-wk1-grd-qfb "")。

- Cloud Controller Manager（CCM）组件升级检查失败的相关解决方案，请参见[Cloud Controller Manager（CCM）组件升级检查失败](https://help.aliyun.com/document_detail/164988.html)。


## 升级CCM组件

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称或者目标集群右侧 **操作** 列下的 **详情**。

3. 在集群管理页左侧导航栏，选择**运维管理** \> **组件管理**。

4. 在 **组件管理** 页面 **核心组件** 页签下单击 **Cloud Controller Manager** 面板上的 **升级**。





**说明**





若 **Cloud Controller Manager** 面板上无升级按钮，说明CCM组件已是最新版本，无需升级。

5. 在 **提示** 对话框中单击 **确认**。