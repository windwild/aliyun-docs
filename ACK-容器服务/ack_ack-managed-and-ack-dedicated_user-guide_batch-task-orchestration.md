### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)批量任务编排

# 批量任务编排概述

更新时间：2025-05-21 03:14:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

Argo Workflows介绍

使用场景

Argo Workflows的优势包括：

使用Argo Workflows

计费说明

联系我们

在批量数据处理、机器学习Pipeline、基础设施自动化、CI/CD等场景中，传统的批量任务编排、流程式编排等系统并不能很好地应对日益复杂的任务编排场景，也无法支撑自动化拓展需求。阿里云提供了兼容云原生工作流引擎Argo Workflows的组件，帮助您降低批量任务的编排复杂度。

## Argo Workflows介绍

[Argo Workflows](https://argoproj.github.io/workflows/) 是一个强大的云原生工作流引擎，专门用于在Kubernetes中定义、管理和调度复杂的工作流。工作流可以包含多个任务，任务之间可以存在依赖关系，这种灵活性降低了任务配置的复杂度。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5461187471/CAEQURiBgMDZ0p7.nRkiIDM0NGFkNWM5NjgwNzRlNjRhNDQ4N2RkZjMzNDExNTYz4814503_20241213173159.037.svg)

### **使用场景**

Argo Workflows可支持批量数据处理、机器学习Pipeline、基础设施自动化、CI/CD等场景，广泛应用于自动驾驶、科学计算、金融量化、数字媒体等行业。

- 批量数据处理：典型应用场景包括大规模高精地图处理、金融量化回测仿真、并行音视频处理、动画渲染等。

- 科学计算：典型应用场景包括复杂科学计算模拟仿真、药物研发训练、基因测序、变异比对检测、能源勘探等。

- 模拟仿真：典型应用场景包括自动驾驶算法仿真、分子动力学模拟、天文数据模拟仿真、金融建模等。

- 机器学习Pipeline：典型应用场景包括机器学习数据预处理、分布式训练、大模型参数调优、模型评估部署等。

- 基础设施自动化：典型应用场景包括云资源自动化管理、资源备份与恢复、节点池迁移、集群迁移升级等。

- CI/CD：典型应用场景包括并行CI Pipeline、多阶段构建和测试、跨云的应用部署、审批流程集成等。


### **Argo Workflows的优势包括：**

- 云原生：专为Kubernetes而设计，每个任务都是一个Pod，充分利用了容器的轻量级和灵活性。

- 轻量可扩展：轻量化，与传统虚拟机（VM）相比，没有额外的开销和限制。借助Kubernetes的调度能力，可并行启动数千个任务，提高处理效率。

- 灵活的编排能力：基于DAG和Step的灵活组合能够支持定制任意复杂的工作流逻辑，并且借助强大的重试和缓存机制，提升工作流的运行成功率。

- 丰富的生态：支持编排各种类型任务，包括Spark、Ray、TensorFlow Job等。结合事件驱动，可以构建全自动化的任务处理平台。


## **使用Argo Workflows**

ACK Argo Workflows兼容社区Argo Workflows并在开源基础上进行增强，您无需修改现有Argo工作流即可实现无缝迁移。ACK的Argo Workflows相比开源基础之上有如下优势：

- 高度弹性，自动扩展，优化计算成本。

- 可靠性高，多可用区负载均衡，调度可靠性高。

- 增强控制面，规模，性能、效率、稳定性、可观测性大幅提升。

- OSS存储管理增强，支持大文件上传、Artifacts GC、流式传输。

- 容器服务技术专家支持，帮助您的业务团队优化工作流，有效提升运行性能、降低成本。


ACK Argo Workflows提供两种使用方式，以满足不同用户的需求：

- Serverless Argo Workflows：若您希望免运维，专注于业务流程编排，并且有大规模、高性能等需求，您需要构建单独的工作流集群，详细操作，请参见 [Serverless Argo Workflows](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/overview-12 "")。

- Argo Workflows组件on ACK：若您已经拥有ACK集群，希望利用已有集群资源，可以使用Argo Workflows组件来编排自己的业务工作流。本文主要介绍Argo Workflows 组件在ACK集群上的使用。


安装Argo Workflows组件后，您便可启用批量任务编排能力。您可以通过阿里云Argo CLI或Argo控制台提交和管理工作流。

不同角色的流程大体如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6461187471/CAEQURiBgMDrh8n7nRkiIDNiM2RkYWNmNmFhYzQ5OGZiNGNjMmJmZWMxYzMzMmYx4814503_20241213143812.665.svg)

| **流程** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **流程** | **说明** |
| 1、准备工作 | 1. 开通ACK服务，请参见 [快速创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/getting-started/quick-start-for-first-time-users "")。<br>   <br>2. 创建ACK集群，请参见 [创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/ "")。 |
| 2、搭建环境 | 1. 您需要安装Argo Workflows组件，在集群中启用批量任务编排能力。<br>   <br>2. ACK提供阿里云Argo CLI或Argo控制台两种方式来创建和管理工作流任务。<br>   <br>   - Argo CLI：安装Argo CLI。<br>     <br>   - Argo控制台：获取访问Argo Server所需的Token，访问控制台。<br>具体操作，请参见 [启用批量任务编排能力](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/component-installation "")。 |
| 3、管理工作流 | （数据工程师）编排并行任务后，您可以通过Argo CLI或Argo控制台进行任务的提交和管理。<br>- 基础使用：如果您是新手用户，可以参见 [创建工作流](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-workflow "") 快速体验如何在ACK集群中创建一个工作流。<br>  <br>- 进阶使用：针对特定业务场景，例如动态DAG Fan-out/Fan-in任务、基因计算工作里、批量数据处理等，您可以参见 [最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/argo-workflows-best-practices/ "") 了解解决方案。 |
| （集群管理员）<br>- 管理集群的资源配额、权限隔离等。例如，您可以指定不同工作流运行在不同的命名空间下，请参见 [向特定命名空间提交工作流](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/submit-a-workflow-to-a-specific-namespace "")。<br>  <br>- 检测工作流的运行状态，例如将工作流日志进行持久化存储等，请参见 [持久化工作流](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/persist-workflows "")。 |

## **计费说明**

批量任务编排功能本身不收取费用。但除 [ACK常规计费](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/ack-pro-cluster-billing "") 外，使用批量任务编排时，Argo Server会自动创建一个按量计费的CLB实例，费用由CLB收取，请参见 [CLB计费概述](https://help.aliyun.com/zh/slb/classic-load-balancer/product-overview/billing-overview/ "")。

## 联系我们

若您有任何产品建议或疑问，请加入钉钉群（钉钉群号：35688562）联系我们。