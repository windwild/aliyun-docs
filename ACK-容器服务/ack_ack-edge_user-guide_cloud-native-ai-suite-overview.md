### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/)[操作指南](https://help.aliyun.com/zh/ack/ack-edge/user-guide/)AI套件

# 云原生AI套件概述

更新时间：2025-03-06 03:30:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：收集ACK Edge集群控制平面组件日志](https://help.aliyun.com/zh/ack/ack-edge/user-guide/collect-ack-edge-cluster-control-plane-component-logs)[下一篇：部署AI套件控制台](https://help.aliyun.com/zh/ack/ack-edge/user-guide/deploy-ai-suite-console)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

能力概览

使用方式

云原生AI套件是阿里云容器服务ACK提供的云原生AI技术和产品方案。使用云原生AI套件，您可以充分利用云原生架构和技术，在Kubernetes容器平台上快速定制化构建AI生产系统，并为AI/ML应用和系统提供全栈优化。ACK Edge集群在云上环境保持AI套件完整的能力体验，在云下环境能力有所裁剪。本文将详细介绍不同节点和网络类型下AI套件在ACK Edge集群上的能力和使用限制。

## 使用限制

| **限制项** | **限制条件** |
| --- | --- |

|     |     |
| --- | --- |
| **限制项** | **限制条件** |
| AI套件组件 | 您在使用AI套件特定组件时需要注意组件本身的使用限制，如集群版本，NVIDIA驱动版本等，具体信息，请参见 [AI套件组件介绍](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/component-introduction-and-release-note/ "")。 |
| ACK Edge集群 | 如果您希望在边缘节点上使用云原生AI套件，目前仅支持特定的边缘节点操作系统和GPU型号，具体信息，请参见 [添加边缘节点](https://help.aliyun.com/zh/ack/ack-edge/user-guide/add-an-edge-node#section-ap8-h68-c1p "")。 |

## 能力概览

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1489421471/CAEQQRiBgMDjgrSK9RgiIGY0NDc5MjQxMjgxNTQxMTY5NTdlYzJiZDA3MjRiNjY14106618_20231206181046.980.svg)

ACK Edge集群与ACK托管集群Pro版核心差异主要体现在以下两个方面：

1. 网络连通性：ACK托管集群Pro版要求集群中的节点在同一个VPC内且网络连通。但在ACK Edge集群中情况较为复杂，需要从节点池维度考虑网络情况。不同网络情况下，AI套件能力也不同。

1. 云上节点池：云上节点池的网络情况与ACK托管集群Pro版相同，管理同一个VPC内网络连通的ECS节点。

2. 网络类型为专用型边缘节点池：专用型边缘节点池管理与云上专线连接的边缘节点，实现云上云下的网络互通。

3. 网络类型为基础型边缘节点池：基础型边缘节点池管理通过公网接入的边缘节点，网络连通性无法确定。
2. 节点环境：ACK Edge集群主要用来纳管您的线下资源，与云上ECS相比，节点环境复杂（如GPU型号，GPU驱动，OS版本等），GPU隔离的能力无法支持。


| **AI套件能力** | **对应组件名称** | **云上环境** | **边缘环境** | **操作链接** |
| --- | --- | --- | --- | --- |
| **云上节点池** | **专用型边缘节点池** | **基础型边缘节点池** |
| --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **AI套件能力** | **对应组件名称** | **云上环境** | **边缘环境** | **操作链接** |
| **云上节点池** | **专用型边缘节点池** | **基础型边缘节点池** |
| 弹性 | ack-alibaba-cloud-metrics-adapter | 支持 | 支持 | 支持 | - [基于Kubernetes部署运行模型训练作业](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/run-model-training-jobs-based-on-kubernetes-deployment/#title-2xb-q78-w77 "")<br>  <br>- [容器化弹性推理](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/elastic-inference-services/#title-k0y-86i-7ya "") |
| 加速 | [ack-fluid](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/ack-fluid "") | 支持 | 支持 | 支持 | - [弹性数据集](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/overview-of-fluid/ "")<br>  <br>- [使用Fluid加速边缘节点访问OSS文件](https://help.aliyun.com/zh/ack/ack-edge/user-guide/use-fluid-to-accelerate-access-to-oss-files-from-edge-nodes "") |
| 调度（批量任务调度、GPU共享、GPU拓扑感知） | [ack-ai-installer](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/ack-ai-installer "") | 支持 | 仅不支持GPU显存隔离，剩余均支持 | 仅不支持GPU显存隔离，剩余均支持 | - [使用Gang scheduling](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-gang-scheduling "")<br>  <br>- [使用共享GPU调度能力](https://help.aliyun.com/zh/ack/ack-edge/user-guide/enable-gpu-sharing "")<br>  <br>- [GPU拓扑感知调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-topology-aware-gpu-scheduling/ "") |
| 调度（任务队列） | [ack-kube-queue](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/ack-kube-queue "") | 支持 | 支持 | 支持 | [使用任务队列ack-kube-queue管理AI/ML工作负载](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-ack-kube-queue-to-manage-job-queues "") |
| 交互方式（Arena） | [ack-arena](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/ack-arena "") | 支持 | 支持 | 支持 | [配置Arena客户端](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/install-arena "") |
| 交互方式（控制台） | ack-ai-dashboard<br>[ack-ai-dev-console](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/ack-ai-dev-console "")<br>ack-mysql | 支持 | 支持 | 支持 | - [安装云原生AI套件](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/deploy-the-cloud-native-ai-suite#title-22a-t7e-axv "")<br>  <br>- [部署AI套件控制台](https://help.aliyun.com/zh/ack/ack-edge/user-guide/deploy-ai-suite-console "") |
| 工作流 | [ack-ai-pipeline](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/ack-ai-pipeline "") | 支持 | 支持 | 支持 | [安装云原生AI套件](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/deploy-the-cloud-native-ai-suite#title-nl2-tcp-ayn "") |
| 监控 | ack-arena-exporter | 支持 | 支持 | 支持 | [使用云原生AI监控大盘](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/work-with-ai-dashboards "") |

**说明**

在边缘节点池中，AI套件的加速能力只能在节点间网络互通的边缘节点池使用。

## 使用方式

基于ACK Edge集群的云边架构，我们建议您在使用AI套件的过程中通过节点池来管理不同的资源。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1489421471/CAEQTxiBgMD0_O.kixkiIDU1NGI3YzA1MGJmZTQ4YWU5MGEzNTY0ZjBmMzhjODA34597176_20240816111822.158.svg)

1. 管控节点池：部署AI套件管控组件的云上节点池。

1. 该节点池的节点不需要有GPU资源。

2. 默认会使用ACK Edge集群自动创建的云上节点池 **default-nodepool** 作为管控节点池。

3. 如果您需要开启AI套件的所有功能，该节点池需至少扩容至4个节点，以保证组件有足够的资源可以正常运行。具体操作，请参见 [扩容云上节点](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-and-manage-node-pools#section-6ff-cpv-ip8 "")。
2. 弹性节点池：开启节点 [自动伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-scaling-of-nodes "") 的云上节点池。

如果您有 [弹性推理](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/run-elastic-inference-workloads-on-ecs-instances "") 的需求，可以通过该节点池实现随业务需求动态变化的服务器弹性扩缩容。

3. 边缘节点池：管理线下数据中心中不同类型的节点。

建议您根据节点属性使用 [边缘节点池](https://help.aliyun.com/zh/ack/ack-edge/user-guide/overview-of-cell-based-management-at-the-edge/ "") 来管理一组相关的节点。例如您可以按照CPU架构划分为AMD节点池和Arm节点池，或者按照网络情况划分专线节点池和公网节点池等。