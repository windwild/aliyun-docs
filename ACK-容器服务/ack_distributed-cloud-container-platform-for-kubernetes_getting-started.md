### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[分布式云容器平台ACK One](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/)快速入门

# 快速入门

更新时间：2025-02-27 05:05:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ACK One计费说明](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/product-overview/ack-one-billing)[下一篇：授权概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/authorization-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

快速使用流程

快速使用方式

注册集群

舰队管理

分布式工作流Agro集群

备份中心

本文介绍分布式云容器平台ACK One的快速使用流程、使用方式和文档使用指引，帮助您快速上手ACK One。

## 前提条件

已开通分布式云容器平台ACK One，且授权默认角色和开通相关云产品。具体操作，请参见 [ACK One服务角色策略内容](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/manage-the-service-linked-role-for-ack-one#task-2197225 "")。

## 快速使用流程

ACK One的快速使用流程如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0370560471/CAEQOxiBgMC2hpn88xgiIDc5OTA3NjkyOWJjYjRkNjNiNmU3MzJjOGQ1MjdmMTMy3963382_20230830144006.372.svg)

## 快速使用方式

ACK One主要包含以下产品能力，包括 [注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/getting-started#1 "")、 [舰队管理](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/getting-started#2 "")、 [分布式工作流Argo集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/kubernetes-clusters-for-distributed-argo-workflows/ "")、 [备份中心](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/getting-started#4 "")，每个产品能力可以单独使用，也可以组合集成使用，可根据需求灵活选用。

### 注册集群

注册集群帮助您将云下Kubernetes集群接入云端，快速搭建混合云集群，可以将本地数据中心Kubernetes集群或其他云厂商Kubernetes集群接入阿里云容器服务管理平台，进行统一管理。

| **功能** | **描述** | **参考文档** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **功能** | **描述** | **参考文档** |
| 创建注册集群并接入本地数据中心集群 | 注册集群是用于将本地数据中心Kubernetes集群或其他云厂商Kubernetes集群接入阿里云容器服务管理平台统一管理的集群形态。 | - [注册集群概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/overview-9#concept-2424510 "")<br>  <br>- [创建注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-ack-one-registered-clusters "") |
| 云上弹性 | 扩展本地数据中心自建Kubernetes集群使用云上计算资源进行弹性扩缩容。例如，手动或自动扩缩容云上ECS或神龙裸金属，并添加为本地数据中心自建Kubernetes集群的云上计算节点等。 | - [使用自定义节点添加脚本](https://help.aliyun.com/zh/ack/create-a-script-to-add-cluster-nodes#task-2056862 "")<br>  <br>- [创建与管理节点池](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-and-manage-node-pools#task-2057212 "")<br>  <br>- [配置自动弹性伸缩](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/configure-auto-scaling#task-2057257 "")<br>  <br>- [通过虚拟节点将Pod调度到ECI上运行](https://help.aliyun.com/zh/ack/scale-out-elastic-container-instances#task-2489901 "")<br>  <br>- [将alibaba-cloud-metrics-adapter接入注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/deploy-alibaba-cloud-metrics-adapter-in-a-registered-cluster#task-2384472 "") |
| 可观测性 | 注册集群支持事件中心、Ingress图表、日志采集、ARMS-应用监控、ARMS-Prometheus、Node Problem Detector（NPD）、Metrics Adapter。 | - [将日志服务接入注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/enable-log-service-for-an-external-kubernetes-cluster#task-2384185 "")<br>  <br>- [将事件中心接入注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-a-kubernetes-event-center-for-an-external-kubernetes-cluster#task-2423452 "")<br>  <br>- [将报警配置功能接入注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/set-up-alerting-for-an-external-kubernetes-cluster#task-2056339 "")<br>  <br>- [将应用实时监控服务ARMS接入注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/enable-arms-for-a-registered-kubernetes-cluster#task-2384472 "")<br>  <br>- [将阿里云Prometheus接入注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/enable-prometheus-service-for-a-registered-cluster#task-2423515 "")<br>  <br>- [集群成本洞察](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/cluster-cost-insights#task-2078815 "") |
| 安全管理 | 注册集群支持RAM统一身份认证和RBAC权限管理、基于日志服务（SLS）的集群审计和配置巡检功能。 | - [启用集群API Server审计功能](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-cluster-auditing-in-registered-clusters#task-2112966 "")<br>  <br>- [使用配置巡检功能检查注册集群Workload安全隐患](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-the-inspection-feature-to-check-for-security-risks-in-the-workloads-of-a-registered-kubernetes-cluster#task-2552179 "") |
| 服务治理 | 支持将MSE接入注册集群的应用中。 | - [将MSE接入注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/connect-registered-clusters-to-mse#task-2078397 "") |
| 协同调度 | 通过为注册集群安装ack-co-scheduler组件的方式，以实现在您的本地集群中使用阿里云容器服务ACK的调度能力，让您能够便捷地使用容器服务对于大数据、AI等应用扩展出的差异化能力，提高应用的运行效率。 | - [通过ack-co-scheduler组件实现协同调度](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-ack-co-scheduler-to-coordinate-resource-scheduling "")<br>  <br>- [通过ack-co-scheduler实现多级弹性调度](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-ack-co-scheduler-to-achieve-multilevel-resource-scheduling "") |

### 舰队管理

舰队管理中的舰队是由ACK托管的，可以管理任意环境的Kubernetes集群，为企业提供一致的云原生应用管理体验。

| **功能** | **描述** | **参考文档** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **功能** | **描述** | **参考文档** |
| 开启舰队管理功能 | 通过舰队管理功能，您可以实现由ACK One舰队完成多集群间工作负载、应用、配置信息的调度分发。 | - [舰队管理概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/fleet-management-overview "")<br>  <br>- [开启舰队管理功能](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/enable-fleet-management "") |
| 管理关联集群 | 开启舰队管理功能后，您可以为舰队添加关联集群，实现由舰队作为统一入口的应用与负载的分发。 | [管理关联集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/manage-associated-clusters#task-2194861 "") |
| GitOps | 您可以在ACK One舰队中开启GitOps，通过Git repository对应用编排、Helm编排等实现版本管理，同时支持应用一次编排的多集群持续发布。 | - [GitOps快速入门](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/work-with-gitops#task-2253464 "")<br>  <br>- [登录GitOps系统](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/log-on-to-the-gitops-system#task-2264099 "")<br>  <br>- [仓库管理](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/manage-git-repositories#task-2264111 "")<br>  <br>- [使用GitOps管理集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-gitops-to-manage-ack-clusters#task-2264113 "")<br>  <br>- [Application管理](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-gitops-to-manage-applications#task-2264114 "")<br>  <br>- [使用ApplicationSet创建多个应用](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-an-applicationset-to-create-multiple-applications#task-2264115 "") |
| 多集群网关 | ACK One多集群网关是阿里云面向混合云、多集群的应用容灾和南北向流量管理推出的解决方案，帮助您快速实现混合云、多集群的应用同城/异地容灾系统以及流量的管理和治理。 | - [多集群网关概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/multi-cluster-gateway-overview "")<br>  <br>- [ALB多集群网关概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/alb-multi-cluster-gateway-overview "")<br>  <br>- [管理网关](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/manage-multi-cluster-gateways "")<br>  <br>- [MSE多集群网关管理南北流量](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-multi-cluster-gateways-to-manage-north-south-traffic "") |
| 多集群服务 | 通过多集群服务功能，让您无需创建负载均衡，即可实现Kubernetes服务的跨集群访问。 | - [多集群服务概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/mcs-overview#task-2233318 "")<br>  <br>- [通过命令行管理多集群服务](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/manage-multi-cluster-services-by-using-the-cli#task-2233321 "") |
| 作业分发 | ACK One多集群作业分发是阿里云面向多集群和混合云场景提供的多集群AI作业调度和分发的能力。您可以利用ACK One多集群作业分发能力，将任务调度到多个集群，以满足您的资源需求。 | [Spark作业的多集群调度与分发](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/multi-cluster-scheduling-and-distribution-of-spark-jobs "") |
| 监控管理 | 多集群全局监控基于单集群Prometheus的监控指标，聚合汇总多个集群的监控指标，并提供多集群全局的监控大盘，让您可以在一个监控大盘上获取多个关联集群的监控指标。 | - [全局监控](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/global-monitoring#task-2224527 "")<br>  <br>- [多集群统一报警管理](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/multi-cluster-alert-management#task-2258560 "")<br>  <br>- [多集群报警差异化配置](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/override-alerting-configurations-for-multi-cluster-management#task-2273632 "") |

### 分布式工作流Agro集群

| **功能** | **描述** | **参考文档** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **功能** | **描述** | **参考文档** |
| 创建工作流集群并获取集群Kubeconfig | 工作流集群采用无服务器模式，使用阿里云弹性容器实例ECI运行工作流，通过优化Kubernetes集群参数，实现大规模工作流的高效弹性调度，同时配合抢占式ECI实例，优化成本。 | [创建工作流集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-a-workflow-cluster "") |
| 创建工作流 | 工作流集群基于开源Argo Workflow项目构建，您可以参考开源文档自定义工作流。 | - [创建工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-a-workflow "")<br>  <br>- [使用指定ECS规格运行工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/run-a-workflow-using-a-specified-ecs-specification "") |
| 访问Agro Server控制台 | 开启Argo Server功能访问工作流集群，您可通过Argo Server API自动化提交工作流，或者通过开源Argo UI管理工作流。 | - [开启Argo Server访问工作流集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/enable-argo-server-for-a-workflow-cluster "")<br>  <br>- [开通Argo Server公网访问](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/enable-public-access-to-the-argo-server "") |
| 事件驱动 | 工作流集群支持事件驱动功能，可通过监控事件触发工作流自动运行，您可以使用该功能构建事件驱动的自动化系统。 | - [开启事件驱动功能](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/turn-on-event-driven-functions "")<br>  <br>- [通过轻量消息队列（原 MNS）触发工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-mns-messages-to-trigger-workflows "")<br>  <br>- [通过向OSS上传文件触发工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/trigger-a-workflow-by-uploading-a-file-to-oss "") |
| 可观测性 | 工作流集群支持集成阿里云ARMS Prometheus服务和阿里云日志服务SLS。通过Prometheus监控大盘可查看集群的运行状态和重要指标；通过日志服务可将工作流运行时Pod产生的日志进行收集和上报，便于您随时查看日志信息。 | - [使用Prometheus监控服务](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/monitoring-services-with-prometheus "")<br>  <br>- [使用日志服务](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/configure-log-service "") |

### 备份中心

备份中心为无状态或有状态应用的备份、恢复与迁移提供了一站式的解决方案，特别是对混合云、多集群的有状态应用提供了数据容灾和应用迁移能力。

| **功能** | **描述** | **参考文档** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **功能** | **描述** | **参考文档** |
| 开启备份中心 | 备份中心为无状态或有状态应用的备份、恢复与迁移提供了一站式的解决方案，特别是对混合云，多集群的有状态应用提供了数据容灾和应用迁移能力。 | - [备份中心](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/backup-center-overview/#task-2510869 "")<br>  <br>- [安装migrate-controller备份服务组件并配置权限](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/install-migrate-controller-and-grant-permissions#task-1955156 "") |
| 备份与恢复应用与数据 | 备份中心为集群内的有状态应用提供灾难备份和恢复能力，对于Kubernetes集群内的有状态应用的崩溃一致性、应用一致性及跨地域的灾难恢复提供了一站式的解决方案。 | [集群内备份和恢复应用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/back-up-and-restore-applications-in-an-ack-cluster#task-1993430 "") |
| 跨集群迁移应用 | 备份中心为集群内的有状态应用提供灾难备份和恢复能力，对于Kubernetes集群内的有状态应用的崩溃一致性，应用一致性，跨地域的灾难恢复提供了一站式的解决方案。 | - [同地域跨集群迁移应用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/migrate-applications-across-clusters-in-the-same-region#task-1994278 "")<br>  <br>- [跨地域跨集群迁移应用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/migrate-applications-across-clusters-in-different-regions#task-2287013 "")<br>  <br>- [自建Kubernetes集群应用迁移至线上ACK集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/migrate-applications-from-self-managed-kubernetes-clusters-to-ack-clusters "")<br>  <br>- [将其他云厂商Kubernetes集群应用迁移至ACK集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/migrate-applications-from-external-kubernetes-clusters-to-ack "") |