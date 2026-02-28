### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[网络](https://help.aliyun.com/zh/ack/product-overview/network-3/)Poseidon

# Poseidon 组件的变更记录

更新时间：2025-08-12 22:33:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ACK Extend Network Controller](https://help.aliyun.com/zh/ack/product-overview/ack-extend-network-controller)[下一篇：Sidecar Acceleration using eBPF](https://help.aliyun.com/zh/ack/product-overview/sidecar-acceleration-using-ebpf)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

使用限制

变更记录

2024年07月

2023年09月

2023年07月

Poseidon是ACK自研的容器NetworkPolicy插件。支持Kubernetes标准的NetworkPolicy功能。本文介绍Poseidon组件的基本信息、使用说明和变更记录。

## 组件介绍

Poseidon是ACK自研的容器NetworkPolicy插件。支持Kubernetes标准的NetworkPolicy功能。

## 使用说明

关于在ACK Serverless中使用NetworkPolicy，请参考 [使用网络策略Network Policy](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/using-the-network-policy-networkpolicy#wAicU "")。

## 使用限制

NetworkPolicy功能仅支持在ACK Serverless集群、ACK集群的ECI、ACS CPU 实例中使用。

ACK GlobalNetworkPolicy功能仅在ACK集群ECS实例中使用，集群网络插件需为Terway，并且开启NetworkPolicy功能。

## 变更记录

### 2024年07月

| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| v0.5.2 | 2024年07月29日 | 解决ACK Serverless集群兼容性问题。 | 此次升级不会对业务造成影响。 |
| v0.5.1 | 2024年07月09日 | 解决Namespace Selector可能不生效问题。 | 此次升级不会对业务造成影响。 |
| v0.5.0 | 2024年07月01日 | 支持ACK NetworkPolicy。 | 此次升级不会对业务造成影响。 |

### 2023年09月

| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| v0.3.0 | 2023年09月08日 | NetworkPolicy支持named port。 | 此次升级不会对业务造成影响。 |

### 2023年07月

| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| v0.1.0 | 2023年07月06日 | 支持在ACK Serverless集群中使用NetworkPolicy功能。 | 此次升级不会对业务造成影响。 |