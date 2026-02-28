### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[安全](https://help.aliyun.com/zh/ack/product-overview/security-1/)policy-template-controller

# policy-template-controller组件介绍和发布记录

更新时间：2025-09-15 22:36:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ack-kubernetes-webhook-injector](https://help.aliyun.com/zh/ack/product-overview/ack-kubernetes-webhook-injector)[下一篇：ack-advanced-audit](https://help.aliyun.com/zh/ack/product-overview/ack-advanced-audit)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

变更记录

2025年09月

2025年08月

2023年04月

2022年12月

2022年04月

2022年02月

2021年11月

policy-template-controller是实现策略管理功能的关键组件。本文介绍policy-template-controller组件的功能、使用说明和变更记录。

## 组件介绍

policy-template-controller组件是为实现新版容器安全策略管理功能而开发的K8s控制器，能帮助您更好地管理基于模板部署的策略实例和集群的整体治理状态。更多信息，请参见 [配置容器安全策略（新版）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/configure-and-enforce-ack-pod-security-policies#task-2148676 "")。

## 使用说明

关于policy-template-controller组件的使用说明，请参见 [配置容器安全策略（新版）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/configure-and-enforce-ack-pod-security-policies#task-2148676 "")。

## 变更记录

### **2025年09月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.4.1 | registry-cn-hangzhou.ack.aliyuncs.com/acs/policy-template-controller:0.4.1 | 2025年09月08日 | - 升级组件使用的Golang版本为1.23.12，并升级相关软件包依赖。<br>  <br>- 升级依赖系统镜像，提升组件稳定性。 | 此次升级不会对业务造成影响。 |

### **2025年08月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v0.4.0.8-g220be83-aliyun | registry.cn-hangzhou.aliyuncs.com/acs/policy-template-controller:v0.4.0.8-g220be83-aliyun | 2025年08月13日 | 针对 [Auto Mode集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-mode-overview/ "") 新增支持托管版policy-template-controller组件。 | 此次升级不会对业务造成影响。 |

### **2023年04月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v0.4.0.0-gddee19d-aliyun | registry.cn-hangzhou.aliyuncs.com/acs/policy-template-controller:v0.4.0.0-gddee19d-aliyun | 2023年04月18日 | 新增支持Kubernetes 1.26。 | 此次升级不会对业务造成影响。 |

### **2022年12月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v0.3.0.0-g0943d7d-aliyun | registry.cn-hangzhou.aliyuncs.com/acs/policy-template-controller:v0.3.0.0-g0943d7d-aliyun | 2022年12月22日 | - 新增支持1.18及以上版本的ACK Serverless集群。<br>  <br>- 支持通过重启组件容器的方式自动修复被误删的SLS日志库。 | 此次升级不会对业务造成影响。 |

### **2022年04月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v0.2.1.13-g38303f0-aliyun | registry.cn-hangzhou.aliyuncs.com/acs/policy-template-controller:v0.2.1.13-g38303f0-aliyun | 2022年04月07日 | 当前处于灰度发布中。<br>- 修复组件配置不合理导致的Pod所在节点无法自动排水的问题。<br>  <br>- 修复当多个集群使用相同的日志项目时，出现策略实施记录日志收集异常的问题。 | 此次升级不会对业务造成影响。 |

### **2022年02月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v0.2.0.0-g91ade1a-aliyun | registry.cn-hangzhou.aliyuncs.com/acs/policy-template-controller:v0.2.0.0-g91ade1a-aliyun | 2022年02月15日 | - 修复重复同步的问题，减少APIServer请求次数。<br>  <br>- 支持ARM64架构。 | 此次升级不会对业务造成影响。 |

### **2021年11月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v0.1.1.22-gc87e2aa-aliyun | registry.cn-hangzhou.aliyuncs.com/acs/policy-template-controller:v0.1.1.22-gc87e2aa-aliyun | 2021年11月16日 | 实现 [配置容器安全策略（新版）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/configure-and-enforce-ack-pod-security-policies#task-2148676 "") 中所依赖的功能。 | 此次升级不会对业务造成影响。 |