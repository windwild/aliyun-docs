### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 容器服务ACK发行版概述

# 容器服务ACK发行版概述

更新时间：2023-07-10 00:29:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：【产品公告】关于停止维护Nginx Ingress Controller组件的公告](https://help.aliyun.com/zh/ack/product-overview/product-announcement-announcement-on-end-of-maintenance-for-nginx-ingress-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

和容器服务ACK的区别

产品优势

核心功能

集群创建

集群运维

高性能网络

本地存储管理

快速开始

组件介绍

基础组件

容器运行时

集群安装工具

网络插件

存储插件

社区

## 简介

容器服务ACK发行版，是阿里云针对异构IaaS环境发布的Kubernetes发行版，使用者可通过阿里云ACR免费获取完整内容并获得社区支持。其核心组件经过阿里云容器服务ACK和阿里巴巴集团核心业务场景的大规模生产环境验证和安全检查，具备安全性与可靠性。

容器服务ACK发行版作为完整的Kubernetes发行版，通过阿里云开源的应用打包交付工具 [Sealer](https://github.com/alibaba/sealer)，可以简单、快速地交付到离线环境，帮助使用者更简单、敏捷地管理自己的集群。核心组件同时支持X86和ARM硬件架构，所包含的高性能网络插件 [Hybridnet](https://github.com/alibaba/hybridnet)，可以确保容器服务ACK发行版能够丝滑运行于多样化的基础设施之上。同时，容器服务ACK发行版可以被注册到阿里云容器服务ACK上，实现资源管理、策略合规、流量管控一致，让使用者获得和线上容器服务ACK集群一致的用户体验。

## 和容器服务ACK的区别

容器服务ACK发行版和容器服务ACK的主要区别在于，后者部署在阿里云弹性计算服务器上，并且由阿里云容器服务ACK进行管理，而容器服务ACK发行版的集群则由用户自己管理，可以部署在离线环境、其他云服务商甚至自己的PC上。

容器服务ACK发行版作为容器服务ACK的下游，会紧跟后者的发版节奏，具体发版策略请参阅 [常见问题](https://help.aliyun.com/zh/ack/faq#topic-2170575 "")。

## 产品优势

**安全可靠**：核心组件来自阿里云容器服务ACK，并保持同步更新。这些核心组件经历了数十万商业用户和阿里集团核心业务场景的严苛生产验证，安全性与可靠性经过实践检验。

**敏捷易用**：容器服务ACK发行版深度结合阿里云开源的集群应用打包交付工具Sealer，分钟级实现集群的自动化部署、扩缩容、升级等集群生命周期管理功能。

**一致体验**：ACK容器服务ACK发行版集群可以被容器服务ACK平滑地管理，实现资源管理一致、策略合规一致、流量管控一致、应用部署一致；同时，容器服务ACK所支持的应用解决方案也能无差别的部署在发行版集群内。

**多样兼容**：核心组件同时支特X86和ARM硬件架构，同时容器服务ACK发行版包含的高性能网络插件Hybridnet，又使得网络环境的多样性成为可能，最终确保其能够丝滑运行于多样化的基础设施之上。

## 核心功能

### 集群创建

- 支持单节点非高可用、三节点高可用、etcd/apiserver分离（规划中）多种部署形态。

- 支持环境预检和部署完成后的集群验证（规划中）。

- 支持在ECS、VMware、VirtualBox、ZStack、OpenStack、裸金属等多种IaaS上部署。

- 支持在Redhat系、Debian系、Open Anolis、Kylin、Windows（规划中）等多种OS上部署。

- 支持在x86、arm64（规划中）等多种架构上部署。


### 集群运维

- 支持节点扩缩容、节点替换。

- 支持运行时集群健康检查（规划中）。

- 支持备份/恢复（规划中）、Kubernetes版本升级（规划中）。


### 高性能网络

- 支持underlay 和 overlay 容器混合部署，兼具 “通过隧道网络与底层网络环境部署完全解耦” 和“通过非隧道高性能网络与底层网络灵活对接” 两大优势。

- 灵活的IP管理策略、自由的网段动态扩缩容以及丰富的 IP 指定特性。

- 直观、全面的网络资源审计。

- 多集群网络能力支持。


### 本地存储管理

- 支持本地存储池管理、存储卷动态分配、存储卷扩容、存储卷快照。

- 支持存储调度算法扩展。

- 支持存储卷监控。


## 快速开始

```shell
# 获取sealer工具
wget -c http://sealer.oss-cn-beijing.aliyuncs.com/sealers/sealer-v0.5.2-linux-amd64.tar.gz && \
        tar -xvf sealer-v0.5.2-linux-amd64.tar.gz -C /usr/bin

# 获取容器服务ACK发行版制品并拉起集群
sealer run ack-agility-registry.cn-shanghai.cr.aliyuncs.com/ecp_builder/ackdistro:v1.20.4-ack-1 -m ${master_ip1}[,${master_ip2},${master_ip3}] [ -n ${worker_ip1}...] -p password

# 检查集群
kubectl get cs
```

更多内容请参见 [User Guide](https://github.com/AliyunContainerService/ackdistro/blob/main/docs/user-guide/getting-started_zh.md)。

## 组件介绍

### 基础组件

包括apiserver、scheduler、kcm、kubelet、kube-proxy、coredns、metrics-server、kubectl、kubeadm等。

### 容器运行时

包括docker、containerd、nvidia-docker等组件。

### 集群安装工具

即 [Sealer](https://github.com/alibaba/sealer?spm=5176.25695502.J_6725771560.1.67f754edVGlgxa)，已开源。

### 网络插件

即 [Hybridnet](https://github.com/alibaba/hybridnet?spm=5176.25695502.J_6725771560.2.67f754edVGlgxa)，支持underlay与overlay，项目已开源。

### 存储插件

即 [open-local](https://github.com/alibaba/open-local?spm=5176.25695502.J_6725771560.3.67f754edVGlgxa)，支持本地磁盘调度，项目已开源。

## 社区

请参见 [容器服务ACK发行版社区](https://github.com/AliyunContainerService/ackdistro)。