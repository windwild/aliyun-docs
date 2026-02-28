### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[其他](https://help.aliyun.com/zh/ack/product-overview/others/)aliyun-acr-acceleration-suite

# aliyun-acr-acceleration-suite

更新时间：2025-03-17 22:36:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：sandboxed-container-helper](https://help.aliyun.com/zh/ack/product-overview/sandboxed-container-helper)[下一篇：managed-kube-proxy-windows](https://help.aliyun.com/zh/ack/product-overview/managed-kube-proxy-windows)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

变更记录

2025年03月

2024年07月

2024年07月

2024年07月

2024年02月

2023年09月

2022年08月

2022年06月

2021年03月

2020年11月

本文介绍aliyun-acr-acceleration-suite组件的功能并展示该组件变更记录。

## 组件介绍

aliyun-acr-acceleration-suite是提供镜像按需加载加速能力的客户端插件，以DaemonSet形式部署在Worker节点上。通过配合使用ACR的加速镜像自动转换功能，您可以在业务部署中使用加速镜像，实现镜像数据免全量下载和在线解压，大幅提升应用分发效率，享受卓越的弹性体验。

**说明**

支持在版本≥1.16.9的托管版、专有版，≥1.26.3的ACK Edge集群和ACK Serverless集群、ACK灵骏集群和容器计算服务ACS上使用加速镜像。且创建集群时操作系统为Alibaba Cloud Linux 2.1903、Alibaba Cloud Linux 3.2104、Alibaba Cloud Linux 3.2104 LTS 64 bit ARM edition、Alibaba Cloud Linux UEFI 2.1903、CentOS 7.9。

## 使用说明

关于aliyun-acr-acceleration-suite的更多信息，请参见 [按需加载容器镜像](https://help.aliyun.com/zh/acr/user-guide/load-resources-of-a-container-image-on-demand#task-1955391 "")。

## 变更记录

### 2025年03月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.10 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/aliyun-acr-acceleration-suite:v0.3.0.1-e2dd3e0-aliyun | 2025年03月17日 | 组件支持Webhook的容器不会调度到灵骏节点池。 | 此次升级不会对业务造成影响。 |

### 2024年07月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.9 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/aliyun-acr-acceleration-suite:v0.3.0.1-e2dd3e0-aliyun | 2024年07月17日 | 组件支持灵骏集群。 | 此次升级不会对业务造成影响。 |

### 2024年07月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.8 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/aliyun-acr-acceleration-suite:v0.3.0.1-e2dd3e0-aliyun | 2024年07月17日 | 组件支持边缘集群。 | 此次升级不会对业务造成影响。 |

### 2024年07月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.7 | registry-cn-hangzhou-vpc.ack.aliyuncs.com/acs/aliyun-acr-acceleration-suite:v0.3.0.1-e2dd3e0-aliyun | 2024年07月17日 | 支持Webhook修改多架构镜像为对应的加速镜像版本。 | 此次升级不会对业务造成影响。 |

### 2024年02月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.6 | registry-vpc.cn-hangzhou.aliyuncs.com/acr-toolkit/aliyun-acr-acceleration-suite:v0.3.0.0-dd959f1-aliyun | 2024年02月19日 | - 仅修改部署模板，支持组件Pod高优先级调度。<br>  <br>- 支持Arm节点安装组件。 | 此次升级不会对业务造成影响。 |

### **2023年09月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.5 | registry-vpc.cn-hangzhou.aliyuncs.com/acr-toolkit/aliyun-acr-acceleration-suite:v0.3.0.0-dd959f1-aliyun | 2023年09月07日 | 组件RBAC权限优化。 | 此次升级不会对业务造成影响。 |

### **2022年08月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.3 | registry-vpc.cn-hangzhou.aliyuncs.com/acr-toolkit/aliyun-acr-acceleration-suite:v0.3.0.0-127f0eb-aliyun | 2022年08月02日 | - 支持ACK集群Containerd运行时使用按需加载镜像加速能力。<br>  <br>- 支持ACK virtual-node和ACK Serverless场景下使用按需加载镜像加速能力。 | 此次升级不会对业务造成影响。 |

### **2022年06月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.2 | registry-vpc.cn-hangzhou.aliyuncs.com/acr-toolkit/aliyun-acr-acceleration-suite:v0.2.0.0-b01f3302-aliyun | 2022年06月08日 | - 修复ACK 1.22集群上镜像拉取密钥同步失败问题。<br>  <br>- Mutating Webhook移除对update操作的支持，预防非预期行为。<br>  <br>- 增强aliyun-acr-acceleration-suite组件的稳定性：<br>  <br>  - 设置Pod资源`requests/limits`；<br>    <br>  - Webhook超时时间调整到5s；<br>    <br>  - Webhook cache TTL调整到60s。 | 此次升级不会对业务造成影响。 |

### **2021年03月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.0 | registry-vpc.cn-hangzhou.aliyuncs.com/acr-toolkit/aliyun-acr-acceleration-suite:v0.2.0.0-b745758c-aliyun | 2021年03月15日 | - Mutating Webhook增加就绪和存活HTTP探针。<br>  <br>- 支持Workload维度打加速标签以启用按需加载能力。标签key为`k8s.aliyun.com/image-accelerate-mode`，标签value为`on-demand`。<br>  <br>  <br>  <br>  **说明**<br>  <br>  <br>  <br>  <br>  <br>  关于设置按需加载的具体操作，请参见 [按需加载容器镜像](https://help.aliyun.com/zh/acr/user-guide/load-resources-of-a-container-image-on-demand#task-1955391 "")。 | 此次升级不会对业务造成影响。 |

### **2020年11月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.1.0 | registry.cn-hangzhou.aliyuncs.com/acs/aliyun-acr-acceleration-suite:v0.1.0.0-00e2f5e1-aliyun | 2020年11月19日 | 主要提供相关镜像存储插件管理、镜像仓库服务的访问配置，以及Pod加速镜像自动注入等功能。 | 建议在业务低峰期进行安装和升级。 |