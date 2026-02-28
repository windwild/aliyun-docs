### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[动态与公告](https://help.aliyun.com/zh/ack/product-overview/announcements-and-updates/)[组件变更](https://help.aliyun.com/zh/ack/product-overview/components/)【组件升级】cluster-autoscaler升级公告

# 【组件升级】cluster-autoscaler升级公告

更新时间：2025-01-12 22:19:24

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：【组件公告】关于1.26.6和1.28.1版本的csi-plugin和csi-provisioner组件兼容性问题](https://help.aliyun.com/zh/ack/product-overview/csi-plugin-and-csi-provisioner-component-compatibility-issues-for-versions-1-26-6-and-1-28-1)[下一篇：【组件升级】云原生应用管理套件ack-kruise组件升级公告-安全CVE相关升级](https://help.aliyun.com/zh/ack/product-overview/ack-kruise-updates-cve-updates)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

影响范围

解决方案

如何查看cluster-autoscaler组件版本

Kubernetes 1.22版本后ServiceAccount Token存在过期风险。详细信息，请参见 [【产品变更】升级1.22版本后ServiceAccount Token过期解决方案](https://help.aliyun.com/zh/ack/product-overview/solution-to-serviceaccount-token-expiration-after-upgrading-122-version "")。集群使用的cluster-autoscaler组件版本为v1.3.9以下时，系统不会自动重新加载并更新Token，可能带来Token过期风险。Token过期后，cluster-autoscaler组件将无法工作，请升级组件版本。

## 影响范围

使用了版本为v1.3.9以下的cluster-autoscaler组件的集群。v1.3.9及以上版本默认已修复，无需升级。

如何查看cluster-autoscaler组件版本，请参见 [如何查看cluster-autoscaler组件版本](https://help.aliyun.com/zh/ack/product-overview/cluster-autoscaler-update#3202c02068anf "")。

## **解决方案**

对于已开启集群自动弹性伸缩的集群，您使用的cluster-autoscaler组件版本为v1.3.9以下时，可通过以下方式升级cluster-autoscaler。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点池**。

3. 单击 **集群自动弹性伸缩** 右侧的 **编辑**。

4. 在 **集群自动弹性伸缩配置** 页面，单击 **确定**，即可升级cluster-autoscaler至最新版本。


## **如何查看cluster-autoscaler组件版本**

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **无状态**。

3. 在 **无状态** 页面，设置 **命名空间** 为 **kube-system**，然后搜索 **cluster-autoscaler**。查看cluster-autoscaler镜像版本，若镜像版本为v1.3.9以下，则需要升级。![1.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8759107961/p726419.jpg)