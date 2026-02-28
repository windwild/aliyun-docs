### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)产品简介

# 什么是阿里云容器服务Kubernetes版

更新时间：2025-03-26 06:29:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：关于ASK正式更名为容器服务 Serverless 版（ACK Serverless）公告](https://help.aliyun.com/zh/ack/product-overview/renaming-of-ask-to-ack-serverless)[下一篇：功能发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

产品介绍

产品优势

相关文档

阿里云容器服务 Kubernetes 版 ACK（Container Service for Kubernetes）是全球首批通过Kubernetes一致性认证的服务平台，提供高性能的容器应用管理服务，支持企业级Kubernetes容器化应用的生命周期管理，让您轻松高效地在云端运行Kubernetes容器化应用。本文介绍什么是容器服务 Kubernetes 版以及其下不同的集群类型。

## **产品介绍**

容器服务ACK提供多种集群类型，包括ACK托管集群、ACK Serverless集群、ACK Edge集群等。

| **集群类型** | **说明** | **简介** | **计费** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **集群类型** | **说明** | **简介** | **计费** |
| 容器服务 Kubernetes 版 | 容器服务 Kubernetes 版的ACK托管集群提供ACK托管集群Pro版和ACK托管集群基础版。ACK托管集群Pro版是在ACK托管集群基础版的基础上发展而来的集群类型，继承了原托管版集群的所有优势，例如控制面托管、控制面高可用等，同时进一步增强了集群的可靠性、安全性和调度性，并且支持赔付标准的SLA，适合生产环境下有着大规模业务，对稳定性和安全性有高要求的企业客户。 | [什么是容器服务 Kubernetes 版](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/what-is-ack "") | [ACK托管和专有集群计费说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/ack-pro-cluster-billing "") |
| 容器服务 Serverless 版 | 无服务器Kubernetes容器服务。在ACK Serverless集群中，您无需购买节点即可直接部署容器应用，无需对集群进行节点维护和容量规划，并且根据应用配置的CPU和内存资源量进行按需付费。ACK Serverless集群提供完善的Kubernetes兼容能力，同时降低了Kubernetes使用门槛，让您更专注于应用程序，而不是管理底层基础设施。 | [什么是容器服务 Serverless 版](https://help.aliyun.com/zh/ack/serverless-kubernetes/product-overview/ask-overview "") | [ACK Serverless集群计费说明](https://help.aliyun.com/zh/ack/serverless-kubernetes/product-overview/ack-serverless-cluster-billing-instructions "") |
| 容器服务 Edge 版 | 容器服务 Edge 版是针对边缘计算场景推出的云边一体化协同托管方案。在云端提供一个标准、安全、高可用的Kubernetes集群，整合阿里云虚拟化、存储、网络和安全等能力，并简化集群运维工作，让您专注于容器化应用的开发与管理。 | [什么是容器服务 Edge 版](https://help.aliyun.com/zh/ack/ack-edge/product-overview/ack-edge-overview#title-snn-7jd-y4h "") | [ACK Edge集群计费说明](https://help.aliyun.com/zh/ack/ack-edge/product-overview/billing-of-ack-edge-clusters "") |
| 容器服务灵骏版 | 容器服务灵骏版是针对智能计算灵骏提供的集群类型，提供全托管和高可用控制面的标准Kubernetes集群服务，支持以灵骏计算节点作为Kubernetes集群的工作节点。 | [什么是容器服务灵骏版](https://help.aliyun.com/zh/ack/ack-lingjun-managed-clusters/product-overview/overview-14#title-k0o-8m2-4us "") | [ACK灵骏集群计费说明](https://help.aliyun.com/zh/ack/ack-lingjun-managed-clusters/product-overview/billingofacklingjun "") |
| 云原生AI套件 | 以容器服务为底座的云原生AI技术和产品方案。<br>- 向下封装对各类异构资源的统一管理，向上提供标准Kubernetes集群环境和API，以运行各核心组件，实现资源运维管理、AI任务调度和弹性伸缩、数据访问加速、工作流编排、大数据服务集成、AI作业生命周期管理、AI制品管理、统一运维等功能。<br>  <br>- 向上针对AI生产流程中的主要环节，支持AI数据集管理，AI模型开发、训练、评测，以及模型推理服务等。 | [云原生AI套件概述](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/cloud-native-ai-suite-overview "") | [云原生AI套件计费说明](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/cloud-native-ai-suite-free-open-instructions "") |
| 分布式云容器平台 | 面向混合云、多集群、分布式计算、容灾等场景推出的企业级云原生平台。支持连接并管理您任何地域、任何基础设施上的Kubernetes集群，从云端、到边缘、到IDC。提供一致的管理和社区兼容的API，支持对计算、网络、存储、安全、监控、日志、作业、应用、流量等进行统一运维管控。 | [ACK One概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/product-overview/ack-one-overview "") | [ACK One计费说明](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/product-overview/ack-one-billing "") |

## **产品优势**

相较于自建的Kubernetes集群，容器服务 Kubernetes 版集群在应用、网络、存储、安全等多个方面均提供能力兼容与增强，无需您自行探索和开发，大大降低集群管理和运维成本。下表列举主要对比项。

| **对比项** | **自建Kubernetes集群** | **容器服务 Kubernetes 版集群** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **对比项** | **自建Kubernetes集群** | **容器服务 Kubernetes 版集群** |
| 集群管理 | - 用户手动部署集群并自行开发。 用户自行探索和开发。 | - 通过控制台一键创建集群，支持GPU实例和裸金属服务器，支持创建跨AZ高可用的集群。<br>  <br>- 提供容器优化的OS镜像，提供稳定测试和安全加固的Kubernetes和Docker版本。<br>  <br>- 支持多集群管理，支持跨AZ高可用集群，支持集群联邦管理。 |
| 应用管理 | 用户自行探索和开发。 | - 支持灰度发布，支持蓝绿发布。<br>  <br>- 支持应用监控、应用弹性伸缩。<br>  <br>- 内置应用商店，支持Helm应用一键部署；支持服务目录，简化云服务集成。 |
| 网络管理 | - 需要挑选社区网络插件进行适配。<br>  <br>- 用户自行探索和开发。 | - 提供针对阿里云优化的高性能VPC/ENI网络插件，性能优于普通网络方案20%。<br>  <br>- 支持容器访问策略和容器带宽限制。 |
| 存储管理 | 用户自行探索和开发。 | - 支持阿里云云盘、本地盘、NAS、CPFS和OSS，提供标准的CSI驱动。<br>  <br>- 支持存储卷自动创建、迁移。 |
| 运维管理 | 手动运维控制面。 | - 支持Kubernetes新版本一键升级，支持集群组件生命周期管理、支持集群手动和自动弹性伸缩。<br>  <br>- 提供高性能日志采集Agent，提供大量日志dashboard看板 。<br>  <br>- 支持托管的Prometheus监控体系，默认内置多数大盘。<br>  <br>- Pro版集群提供多AZ高可用自动伸缩的托管的控制面，同时提供控制面可观测能力。 |
| 安全管理 | 自行构建安全能力。 | - 支持镜像扫描/镜像签名。<br>  <br>- 支持容器运行时安全检测。<br>  <br>- 支持Secret数据落盘加密。<br>  <br>- 支持操作系统等保加固和阿里云OS加固。 |
| 服务保障 | - 需要组建专门团队。<br>  <br>- 无SLA保障。 | - 阿里云专业容器团队作为技术支持，为集群提供及时的稳定性和安全响应。<br>  <br>- 历经阿里大规模实践，是目前中国最大规模的公共云容器服务之一。<br>  <br>- CNCF白金会员，已通过一致性验证。<br>  <br>- 2019年Forrester报告中国排名第一。2023年入选Gartner®容器管理魔力象限领导者象限，也是亚洲地区唯一入选该象限的云服务商。<br>  <br>- ACK托管集群Pro版提供赔付保障的SLA。 |

## **相关文档**

- [开服地域](https://help.aliyun.com/zh/ack/product-overview/supported-regions "")

- [使用须知及高危风险操作说明](https://help.aliyun.com/zh/ack/product-overview/before-you-start "")

- [配额与限制](https://help.aliyun.com/zh/ack/product-overview/limits "")

- [相关协议](https://help.aliyun.com/zh/ack/support/agreement/)（容器服务 Kubernetes 版的服务条款和服务等级协议SLA说明）