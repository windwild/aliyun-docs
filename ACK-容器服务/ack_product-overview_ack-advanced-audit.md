### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[安全](https://help.aliyun.com/zh/ack/product-overview/security-1/)ack-advanced-audit

# ack-advanced-audit组件介绍与发布记录

更新时间：2026-01-27 21:18:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：policy-template-controller](https://help.aliyun.com/zh/ack/product-overview/policy-template-controller)[下一篇：ack-pod-identity-webhook](https://help.aliyun.com/zh/ack/product-overview/ack-pod-identity-webhook)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

变更记录

2026年01月

2025年09月

2025年05月

2024年10月

2024年08月

2024年07月

2023年09月

2023年04月

2023年02月

ack-advanced-audit是实现容器内部操作审计的关键组件。本文介绍ack-advanced-audit组件信息、使用说明及变更记录。

## 组件介绍

ack-advanced-audit组件基于开源项目 [Falco](https://falco.org/)，使用内核提供的eBPF特性，实现了容器内操作的系统调用审计能力。通过ack-advanced-audit组件实现的容器内部操作审计功能，可以方便您审计组织内成员或应用程序进入容器后执行的命令操作。

## 使用说明

关于ack-advanced-audit组件的使用以及限制，请参见 [使用容器内部操作审计功能](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/use-container-auditing#task-2296882 "")。

## 变更记录

### 2026年01月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.9.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:0.9.0 | - 新增支持Alibaba Cloud Linux 4操作系统。<br>  <br>- 升级组件使用的Golang版本为1.25.6，提升组件稳定性。 | 2026年01月21日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |
| 0.8.2 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:0.8.2 | 升级组件使用的Golang版本为1.25.5，提升组件稳定性。 | 2026年01月08日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2025年09月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.8.1 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:0.8.1 | - 新增支持ContainerOS 3.5操作系统。<br>  <br>- 升级组件使用的Golang版本为1.24.6，提升组件稳定性。 | 2025年09月09日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2025年05月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.7.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.7.0.0-g2f5da32d-aliyun | - 新增支持containerd 2.0。<br>  <br>- 升级组件使用的Golang版本为1.24.3，提升组件稳定性。 | 2025年05月26日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2024年10月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.6.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.6.0.0-g05b523f-aliyun | 优化对ContainerOS操作系统的支持。 | 2024年10月30日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |
| 0.5.1 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.5.1.0-ga51258d-aliyun | 优化对Alibaba Cloud Linux 3.2104 U10操作系统的支持。 | 2024年10月17日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2024年08月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.5.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.5.0.0-g18d101a-aliyun | - 优化程序的内存占用。<br>  <br>- 优化对Alibaba Cloud Linux 3.2104 U9.1操作系统的支持。 | 2024年08月23日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2024年07月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.4.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.4.0.0-g9a46887-aliyun | 优化对Ubuntu操作系统的支持。 | 2024年07月31日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2023年09月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.3.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.3.0.21-ge1fbf04-aliyun | - 优化程序性能。<br>  <br>- 优化对Alibaba Cloud Linux 3.8操作系统的支持。 | 2023年09月11日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2023年04月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.2.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.2.0.0-g052ee2b-aliyun | 支持Kubernetes 1.26。 | 2023年04月13日 | 组件异常可能会导致执行`kubectl exec`操作失败。 |

### 2023年02月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| 0.1.0 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/ack-advanced-audit:v0.1.1.47-gcd1dd3d-aliyun | 实现容器内部操作审计功能。 | 2023年02月07日 | 首个版本。 |