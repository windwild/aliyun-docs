### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[产品概述](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/)[产品简介](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/product-introduction-1/)什么是容器服务 Kubernetes 版

# 什么是容器服务Kubernetes版

更新时间：2025-11-28 01:10:30

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：产品优势](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/benefits)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

集群类型

ACK托管集群架构

核心功能

产品架构

关联的阿里云产品

相关链接

容器服务 Kubernetes 版 ACK（Container Service for Kubernetes）是全球首批通过Kubernetes一致性认证的容器服务平台，提供高性能的容器应用管理服务，支持企业级Kubernetes容器化应用的生命周期管理，让您轻松高效地在云端运行Kubernetes容器化应用。

## 集群类型

容器服务 Kubernetes 版提供ACK托管集群（Pro版和基础版）和ACK专有集群。

- ACK托管集群：

  - 提供开箱即用的高可用Kubernetes集群，控制面（控制面组件、Master节点和etcd）由ACK全托管，只需自行创建和运维Worker节点，从而更专注于业务应用的开发和部署。

  - [计费说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/ack-pro-cluster-billing "")：收取Worker节点和其他基础资源费用。 [ACK集群Pro版](https://help.aliyun.com/zh/ack/overview-of-ack-pro-clusters#concept-2558837 "") 额外收取集群管理费用。
- ACK专有集群（已停止新建）：


  - 需自行维护控制面（控制面组件、Master节点和etcd）和Worker节点，并自行规划、维护、升级集群，对集群基础设施拥有更细粒度的控制。适用于有专业 Kubernetes 运维团队，对集群控制面有高度定制化需求的企业级用户。

  - [计费说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/ack-pro-cluster-billing "")：相较于 ACK 托管集群 Pro 版，控制面资源成本更高。


> ACK专有集群已于2024年08月21日起停止创建（ [云盒](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-cloud-box-resources-in-ack-dedicated-clusters "") 场景除外）。推荐在生产环境中使用具有更高可靠性、安全性和调度效率的 [ACK托管集群Pro版](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/ "")。

## ACK托管集群架构

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7220134671/CAEQQRiBgMDc_fCK9RgiIGY5ODExMjIxY2UwYzRmNTc4NTMxYjgwNzUyODU2MTI23963382_20230830144006.372.svg)

ACK托管集群的管控面由ACK管理，提供稳定、高可用、高性能、安全的Kubernetes服务。托管组件包括kube-apiserver、kube-controller-manager、kube-scheduler和etcd。每一个托管集群的管控面包含至少2个kube-apiserver实例和3个etcd实例，并部署在不同的可用区以提供可用区级别的高可用性。ACK管控会持续监控托管组件，保障服务SLA，并且及时修复安全漏洞。

## 核心功能

- 集群管理

  - 集群创建：您可根据需求创建多种形态集群，选择类型丰富的工作节点，并进行灵活的自定义配置。更多信息，请参见 [创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/#task-skz-qwk-qfb "") 和 [创建ACK专有集群（已停止新建）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-dedicated-cluster/#task-skz-qwk-qfb "")。

  - 集群升级：自动或手动升级集群的Kubernetes版本，统一管理系统组件升级。更多信息，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster#task-1664343 "")、 [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "")。

  - [弹性伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-scaling-overview/#concept-1918532 "")：通过控制台一键垂直扩缩容来快速应对业务波动，同时支持服务级别的亲和性策略和横向扩展。

  - [调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/scheduling-overview/ "")：支持不同弹性资源的混合调度、异构资源的精细化调度、批量计算的任务调度等，提升应用的性能和集群整体资源的利用率。

  - [多集群管理](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/overview-9#concept-2424510 "")：支持线下IDC和多云多区域的集群统一接入，实现混合云应用管理。

  - 授权管理：支持RAM授权和RBAC权限管理。
- 节点池

支持节点池生命周期管理，支持在同一集群中配置不同规格的节点池，例如交换机、运行时、OS、[安全组](https://www.aliyun.com/getting-started/what-is/what-is-a-security-group "")等。更多信息，请参见 [节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-overview/#task-2013378 "")。

- 应用管理

  - 应用创建：支持多种类型应用，从镜像、模板的创建，支持环境变量、应用健康、数据盘、日志等相关配置。

  - 应用全生命周期：支持应用查看、更新、删除，应用历史版本回滚、应用事件查看、应用滚动升级、应用替换升级以及通过触发器重新部署应用。

  - 应用调度：支持节点间亲和性调度、应用间亲和性调度、应用间反亲和性调度三种策略。

  - 应用伸缩：支持手动伸缩应用[容器](https://www.aliyun.com/getting-started/what-is/what-is-container "")实例，HPA自动伸缩策略。

  - 应用发布：支持灰度发布和蓝绿发布。

  - 应用目录：支持应用目录，简化云服务集成。

  - [应用中心](https://help.aliyun.com/zh/ack/application-center-overview#concept-2510869 "")：应用部署后，以统一的视角展现整体应用的拓扑结构，同时对持续部署等场景进行统一的版本管理与回滚。

  - 应用备份和恢复：支持对Kubernetes应用进行备份和恢复。更多信息，请参见 [集群内备份和恢复应用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/back-up-and-restore-applications-in-an-ack-cluster#task-1993430 "")。
- 存储

  - 存储插件：支持CSI存储插件。更多信息，请参见 [存储](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/csi-overview-1/#concept-2005339 "")。

  - 存储卷和存储声明：

    - 支持创建[块存储](https://www.aliyun.com/getting-started/what-is/what-is-block-storage "")、NAS、OSS和CPFS类型的存储卷。

    - 支持持久化存储卷声明（PVC）挂载存储卷。

    - 支持存储卷的动态创建和迁移。

    - 支持以脚本方式查看和更新存储卷和存储声明。
- 网络

  - 支持Terway和Flannel两种容器网络插件。更多信息，请参见 [网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/#concept-tfy-3kq-wfb "")。

  - 支持定义Service和Pod的CIDR。

  - 支持NetworkPolicy，请参见 [在ACK集群使用网络策略](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-network-policies#task-1797447 "")。

  - 支持路由Ingress，请参见 [Ingress管理](https://help.aliyun.com/zh/ack/ingress-management "")。

  - 支持服务发现DNS，请参见 [服务发现DNS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-discovery-dns-1/#task-2038513 "")。
- [GPU](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-5/ "") 支持对各种异构计算资源进行统一调度和运维管理，能够显著提高异构计算集群资源的使用效率。

- [Knative](https://help.aliyun.com/zh/ack/knative-1 "")：一款基于Kubernetes的Serverless框架。部署Knative组件后，您可以利用Knative开展服务管理和事件驱动。

- 运维与安全

  - [可观测性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/observability-overview/#task-2042182 "")：

    - 监控：支持集群、节点、应用、容器实例层面的监控；支持Prometheus插件。

    - 日志：支持集群日志查看；支持应用日志采集；支持容器实例日志查看。

    - 报警：支持容器服务异常事件报警，以及容器场景指标报警。更多信息，请参见 [容器服务报警管理](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/alert-management#task-2056339 "")。
  - 集群巡检与诊断（AIOps）

    - [使用集群检查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-cluster-check/ "")：支持在集群升级、迁移等操作前执行集群检查，确认集群是否符合要求。

    - [使用集群巡检](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-the-cluster-inspection-feature/ "")：扫描集群运行状况，发现集群中存在的潜在风险，例如云资源配额余量、Kubernetes集群关键资源水位等，排查风险项并根据推荐的解决方案修复问题。

    - [使用集群诊断](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-cluster-diagnostics/ "")：提供一键故障诊断能力，包括节点诊断、Pod诊断、Service诊断、Ingress诊断、内存诊断、网络诊断，可以辅助您定位集群中出现的问题。
  - [成本套件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-suite/ "")：支持可视化集群资源使用量及成本分布，以提升集群资源利用率。

  - [安全中心](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/use-security-monitoring-capabilities#task-1930740 "")：支持运行时刻的安全策略管理，应用安全配置巡检和运行时刻的安全监控和告警，提升容器安全整体纵深防御能力。

  - [安全沙箱](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-10/#concept-2329190 "")：可以让应用运行在一个轻量虚拟机沙箱环境中，拥有独立的内核，具备更好的安全隔离能力。适用于不可信应用隔离、故障隔离、性能隔离、多用户间负载隔离等场景。

  - [机密计算](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/tee-based-confidential-computing/#task-2490003 "")：基于Intel SGX提供的可信应用或用于交付和管理机密计算应用的[云原生](https://www.aliyun.com/getting-started/what-is/what-is-cloud-native "")一站式机密计算平台，帮助您保护数据使用中的安全性、完整性和机密性。机密计算可以让您把重要的数据和代码放在一个特殊的可信执行加密环境。

## 产品架构

容器服务 Kubernetes 版产品线的整体架构如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7220134671/CAEQTxiBgIC6xuW7ixkiIDg4YjE0Nzk1YzVmZjQ2MjM4NDQ1YWEwZjE1OTJkZDNh3963382_20230830144006.372.svg)

- [阿里云容器镜像服务ACR](https://help.aliyun.com/zh/acr/product-overview/what-is-container-registry#concept-2058233 "")（Alibaba Cloud Container Registry）：提供云原生资产的安全托管和全生命周期管理，支持多场景下镜像的高效分发，与容器服务ACK无缝集成，打造云原生应用一站式解决方案。

- [阿里云ASM](https://help.aliyun.com/zh/asm/product-overview/what-is-asm#concept-2366983 "")（Service Mesh）：是一个托管式的[微服务](https://www.aliyun.com/getting-started/what-is/what-is-microservice "")应用流量统一管理平台，兼容Istio，支持多个Kubernetes集群统一流量管理，为容器和虚拟机应用服务提供一致性的通信控制。

- [阿里云容器服务 Serverless 版](https://help.aliyun.com/zh/ack/serverless-kubernetes/product-overview/ask-overview#concept-pc2-xyz-xdb "")（Alibaba Cloud Serverless Kubernetes）：是阿里云基于弹性计算架构推出的无服务器Kubernetes容器服务，让您无需管理和维护集群，即可快速创建Kubernetes容器应用。

- [ACK Edge](https://help.aliyun.com/zh/ack/ack-edge/product-overview/ack-edge-overview#task-2478491 "")：基于标准Kubernetes运行环境，提供云、边、端一体的容器应用交付、运维和管控能力，同时加强在边缘业务场景下自治能力。

- [ACK One](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/product-overview/ack-one-overview#concept-2148686 "")：是阿里云面向混合云、多集群、[分布式计算](https://www.aliyun.com/getting-started/what-is/what-is-distributed-computing "")、容灾等场景推出的企业级云原生平台。ACK One可以连接并管理您任何[地域](https://www.aliyun.com/getting-started/what-is/what-is-a-region "")、任何基础设施上的Kubernetes集群，并提供一致的管理和社区兼容的[API](https://www.aliyun.com/getting-started/what-is/what-is-api "")，支持对计算、网络、存储、安全、监控、日志、作业、应用、流量等进行统一运维管控。

- [云原生AI套件](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/product-overview/cloud-native-ai-suite-overview#concept-2038802 "")：通过对数据计算类任务的编排、管理，以及对各种异构计算资源的容器化统一调度和运维，显著提高异构计算集群的资源使用效率和AI工程交付速度。阿里云容器服务ACK以组件化、可拼装、可扩展、可定制的灵活方式，提供了云原生AI能力的产品支持。

- [ACK灵骏集群](https://help.aliyun.com/zh/ack/ack-lingjun-managed-clusters/product-overview/overview-14 "")：容器服务 Kubernetes 版针对智能计算灵骏提供的集群类型，提供全托管和高可用控制面的标准Kubernetes集群服务，支持以灵骏计算节点作为Kubernetes集群的工作节点。


## 关联的阿里云产品

通过ACK集群，您可以为应用业务创建所需的云服务器ECS、网络、存储等阿里云其他产品资源。您可以根据下图创建最小交叉产品集合，获得云原生系统构建、安全合规、微服务、[可观测](https://www.aliyun.com/getting-started/what-is/what-is-observability "")、存储、计算与网络等方面的专业技术支持，适配您集群的开发与运维工作。

建议您关注与容器服务ACK相结合的可观测性方案，即日志与监控产品。对于基础设施监控、容器监控、应用性能监控和业务监控，不同层面可配上对应的可观测性服务。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7220134671/CAEQRhiBgMDRqu6kgRkiIGNhZjNiZjAyYmE3YjRmYjk4YjRjMTM2YWFkOGQ1NjU54450891_20240613171529.187.svg)

关联产品相关说明如下。

| **大类** | **关联产品说明** |
| --- | --- |

|     |     |
| --- | --- |
| **大类** | **关联产品说明** |
| **计算** | 云服务器ECS（以及弹性裸金属EBM、GPU云服务器）：提供节点池工作节点。 |
| 弹性容器实例ECI：提供ACK Serverless集群的容器实例。 |
| 弹性伸缩ESS：支持节点池的配置和弹性伸缩。 |
| **网络** | [专有网络VPC](https://www.aliyun.com/getting-started/what-is/what-is-vpc "")：提供集群私网网络。 |
| [负载均衡](https://www.aliyun.com/getting-started/what-is/what-is-load-balance "")SLB：包括ALB、NLB、CLB，提供集群API Server的访问入口，以及应用服务的访问入口。 |
| NAT网关：提供集群所有节点池的公网访问出口。 |
| [弹性公网IP](https://www.aliyun.com/getting-started/what-is/what-is-elastic-ip-address "")（EIP）：提供节点池内单个工作节点的公网通信能力。 |
| **存储** | 块存储：为工作节点挂载数据盘，为工作负载挂载块存储数据盘。 |
| [文件存储](https://www.aliyun.com/getting-started/what-is/what-is-file-storage "")NAS：为工作负载挂载文件存储。 |
| [对象存储](https://www.aliyun.com/getting-started/what-is/what-is-object-storage "")OSS：为工作负载挂载共享存储。 |
| 文件存储CPFS：为工作负载挂载共享存储。 |
| **安全** | RAM访问控制：结合RBAC，为RAM用户（子账号）设置集群访问权限。 |
| 云安全中心：提供容器运行时安全检测能力。 |
| 密钥管理服务KMS：提供Secret落盘加密的能力。 |
| **可观测性** | Prometheus监控服务：为集群提供Prometheus监控服务以及集群拓扑能力。 |
| 日志服务SLS：为集群提供日志记录服务。 |
| **云原生资产** | 容器镜像服务ACR：为工作负载部署提供镜像仓库。 |
| **其他** | 资源编排ROS：集群资源模板化。 |

## **相关链接**

| **信息项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **信息项** | **说明** |
| 使用须知和限制 | - 为了更好地预估和避免相关的操作风险，在使用ACK前，请参见 [使用须知及高危风险操作说明](https://help.aliyun.com/zh/ack/product-overview/before-you-start "") 了解注意事项和高危操作。<br>  <br>- 使用ACK时涉及的限制，包括容量限制、配额限制等，请参见 [配额与限制](https://help.aliyun.com/zh/ack/product-overview/limits "")。 |
| 动态公告与发布记录 | - ACK产品动态与公告，包括产品变更公告、产品维护公告、CVE漏洞修复公告等，请参见[动态与公告](https://help.aliyun.com/zh/ack/product-overview/announcements-and-updates/)。<br>  <br>- ACK产品发布记录，包括产品功能、支持的Kubernetes版本、操作系统镜像、运行时、组件等内容的发布记录，请参见[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)。 |
| 地域和时区 | ACK支持的地域和时区，请参见 [开服地域](https://help.aliyun.com/zh/ack/product-overview/supported-regions "")、 [支持时区](https://help.aliyun.com/zh/ack/product-overview/supported-time-zones "")。 |
| 快速入门 | 快速体验如何创建与使用ACK集群，例如搭建一款魔方游戏等。更多信息，请参见[快速入门](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/getting-started/)。 |
| Kubernetes版本机制 | ACK会跟随上游的发版节奏进行Kubernetes版本的迭代，请参见 [版本说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/support-for-kubernetes-versions/ "")。 |
| 最佳实践 | 使用ACK集群中不同场景下的最佳实践，包括集群、节点与节点池、网络、应用、Knative、存储、可观测、成本套件、弹性伸缩等方面。更多信息，请参见 [最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/use-cases/best-practices "")。 |
| 开发参考 | 除控制台和kubectl外，您可以通过API、[SDK](https://www.aliyun.com/getting-started/what-is/what-is-sdk "")、CLI和Terraform使用容器服务 Kubernetes 版，请参见[开发参考](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/developer-reference/)。 |
| 产品计费 | ACK集群涉及集群管理费用和相关云产品资源费用，请参见 [计费概述](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/ack-pro-cluster-billing "")。 |
| 学习资料 | - [ACK视频专区](https://help.aliyun.com/zh/ack/videos-3 "")<br>  <br>- [CNCF × Alibaba 云原生技术公开课](https://edu.aliyun.com/course/1651/lesson/list)<br>  <br>- [阿里云云原生容器工程师ACP认证课程](https://edu.aliyun.com/course/2553)<br>  <br>- [Kubernetes官网](https://kubernetes.io/) |
| 服务协议 | - [阿里云容器服务Kubernetes版服务条款](https://help.aliyun.com/zh/ack/support/ack-terms-of-service "")<br>  <br>- [阿里云容器服务Kubernetes版服务等级协议说明](https://help.aliyun.com/zh/ack/support/ack-service-level-agreement "")<br>  <br>- [阿里云容器服务Kubernetes版服务等级协议（本地地域版）](https://help.aliyun.com/zh/ack/support/ack-sla-for-local-regions "") |

如果您在使用容器服务 Kubernetes 版过程中有任何疑问或建议，欢迎您搜索钉群号74560018672加入钉群交流。