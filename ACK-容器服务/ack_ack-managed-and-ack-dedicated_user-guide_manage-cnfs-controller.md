### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[存储](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/csi-overview-1/)[存储组件管理](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/storage-component-management/)管理cnfs-controller组件

# 管理cnfs-controller组件

更新时间：2025-12-02 21:14:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

适用范围

安装cnfs-controller组件

安装网络文件系统管理组件cnfs-controller后，即可使用容器网络文件系统CNFS来管理阿里云NAS文件系统和OSS Bucket，从而提升存储卷的性能与QoS控制，并解决传统共享文件系统所面临的容量配额控制不精确、误删文件无法恢复等问题。

## **适用范围**

仅适用于1.26及以上版本的集群。如需升级，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。

## **安装cnfs-controller组件**

1. 在[ACK集群列表](https://cs.console.aliyun.com/)页面，单击目标集群名称，在集群详情页左侧导航栏，单击 **组件管理**。

2. 单击 **存储** 页签，定位cnfs-controller组件，按照页面提示完成安装。