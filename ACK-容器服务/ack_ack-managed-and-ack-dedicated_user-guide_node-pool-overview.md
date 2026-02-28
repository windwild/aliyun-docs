### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/) [ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/) [操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/) [节点与节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/nodes-and-node-pools/) 节点池

# 节点池概述

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：将节点迁移至 cgroup v2](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/migrate-nodes-to-cgroupv2)[下一篇：创建和管理节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool)

该文章对您有帮助吗？

反馈

节点池是具有相同属性的一组节点的逻辑集合，允许对节点进行统一的管理和运维，例如节点升级、弹性伸缩等。ACK还提供多种节点池自动化运维能力，包括OS CVE漏洞自动修复、故障节点自动恢复等，以降低运维成本。

## 节点池介绍

简单来说，节点池是一个配置模板，后续节点池中扩容出的节点都将使用它的配置。一个集群中可以创建多个不同配置和类型的节点池。节点池的配置包含节点的属性，例如节点实例规格、计费类型、可用区（vSwitch）、 [操作系统镜像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-os-images/ "")、CPU架构、标签和污点等。这些属性可以在 [创建节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#section-eq0-lmv-4a7 "") 时指定，也可以在创建后 [编辑](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#9cff721669kc3 "")。

> ACK节点池功能推出前创建的老集群中，可能存在未被节点池管理的游离Worker节点。如仍需要保留这些节点，推荐将其纳入节点池进行管理。具体操作，请参见 [迁移游离节点至节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-free-nodes-to-a-node-pool "")。

可使用单节点池，减少管理和配置的复杂性，也可使用多节点池，实现更精细的资源隔离和不同类型节点的混合部署管理。

|     |     |
| --- | --- |
| **单节点池** | **多节点池** |
| 通过一个节点池管理多个团队或多种工作负载的计算资源，简化操作和维护工作。单节点池可支持以下功能。<br>- 同时管理多个团队的计算资源。<br>  <br>- 配置多种实例类型，例如普通ECS实例、GPU实例、弹性裸金属实例、高性能计算优化型实例等，以满足不同工作负载的需求。<br>  <br>- 在多个可用区中分布节点，提高高可用性。<br>  <br>> 目前不支持混合不同操作系统类型和CPU架构（Arm和x86）的实例。 | 创建多个节点池，为不同工作负载或团队提供独立的计算资源，从而避免资源争用和潜在的安全风险。适用于以下场景。<br>- 租户隔离，为不同团队提供独立的计算资源，也便于计费管理。<br>  <br>- 不同硬件规格（例如CPU架构、GPU、FPGA等）机器的隔离，确保硬件资源的合理分配。<br>  <br>- 增强敏感应用的安全隔离。<br>  <br>- 部署不同的操作系统。 |

使用多节点池时，可通过调度策略定义不同节点池的优先级顺序，以优化资源和成本管理。例如以下场景。

- 控制不同成本的计算资源供给（例如抢占式实例、包年包月实例等）的优先级顺序，以降低成本。

- 根据工作负载需求，按比例分配不同类型的实例，例如x86架构和Arm架构的使用比例。


## 节点池功能

ACK在节点池维度提供多种节点管理能力。如需减少Worker节点运维压力，更关注于上层应用开发，建议开启节点池的托管能力，使用多种自动化运维能力。

### **基础功能**

|     |     |     |
| --- | --- | --- |
| **功能项** | **说明** | **相关文档** |
| 创建、编辑、删除与查看 | - 支持通过控制台创建节点池，配置节点池的基础信息、网络配置、实例规格配置、存储配置、期望节点数等。<br>  <br>- 支持调整已有节点池的部分配置。支持编辑的配置项及操作注意事项，请参见文档了解。<br>  <br>- 节点无需使用时，可删除节点池。节点池是否开启期望节点数以及节点的计费模式会影响节点释放的行为。<br>  <br>- 支持查看节点池详情，包括基本配置信息、资源监控大盘、节点列表、伸缩活动等。 | [创建和管理节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool "") |
| 手动或自动扩缩容 | - 支持通过手动调整节点池的期望节点数，实现节点池的扩缩容，将节点数目维持在期望数量，节省资源成本。<br>  <br>  一些非标准的移除、修改、释放等操作可能导致节点池未按照预期扩容，请参见文档了解。<br>  <br>- 支持配置节点自动伸缩方案，当集群的容量规划无法满足应用Pod调度时，自动扩缩节点资源。 | - [手动扩缩容节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/scale-a-node-pool "")<br>  <br>- [节点伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-scaling/#DAS "") |
| 添加已有节点 | 如购买ECS实例后需将其添加到ACK集群中作为Worker节点，或移除Worker节点后需重新加入节点池，可以使用添加已有节点的功能。此功能存在一些使用限制和注意事项，请参见文档了解。 | [添加已有节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-existing-ecs-instances-to-an-ack-cluster "") |
| 移除节点 | 如果不再需要某些节点，可将节点从集群或节点池中移除。请按标准化操作移除，避免出现预期外行为。 | [移除节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/remove-a-node-11 "") |
| 升级kubelet版本 | > 可通过 [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "") 实现kubelet和运行时的自动升级<br>升级节点池中节点的kubelet版本和containerd版本。 | [升级节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates "") |
| 更换操作系统 | 支持操作系统版本的升级和操作系统类型的更换（例如将EOL的操作系统切换为ContainerOS或Alibaba Cloud Linux）。 | [更换操作系统](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/replace-the-operating-system "") |
| CVE漏洞修复 | > 可开启 [自动化运维能力](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-overview/#807e154b6au5m "")<br>手动执行CVE漏洞的扫描并修复节点操作系统存在的安全漏洞。部分CVE漏洞的修复需要通过重启节点来实现，请参见文档了解功能说明及注意事项。 | [操作系统CVE漏洞手动修复](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cve-patching#4424af2bc2xba "") |
| 自定义节点池kubelet参数 | 在节点池维度自定义节点的kubelet参数配置，调整节点行为，例如调整集群资源预留以调配资源用量等。 | [自定义节点池kubelet配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-the-kubelet-configurations-of-a-node-pool "") |
| 自定义节点池OS参数 | 在节点池维度自定义节点的OS参数配置，以调优系统性能。 | [管理节点池OS参数](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/custom-node-pool-os-parameters "") |
| 成本洞察 | 节点池维度的资源使用情况及成本分布分析，便于节约成本，提升集群资源利用率。 | [成本洞察](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-insights-1/ "") |

### **自动化运维能力**

启用节点池的自动化运维能力能够降低Worker节点的运维负担，让ACK自动化完成某些运维操作，例如操作系统（OS）CVE漏洞自动修复、kubelet自动升级、节点故障自愈等。但如果业务对底层节点的变更比较敏感，无法容忍节点的重启以及业务Pod的迁移，不推荐启用。

#### **准备工作**

- 确保操作系统为 [Alibaba Cloud Linux 3容器优化版](https://help.aliyun.com/zh/alinux/alibaba-cloud-linux-3-container-optimized-images "")、 [ContainerOS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/containeros-overview/ "")、Alibaba Cloud Linux、Red Hat、Ubuntu。

关于ACK集群支持的操作系统镜像介绍及镜像的使用限制，请参见 [操作系统](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-os-images/ "")。

- 使用节点池的自动化运维能力前，需在[容器服务管理控制台](https://cs.console.aliyun.com/)的 **节点池** 页面完成以下操作（配置完成后均支持修改）。


> 关于如何创建和编辑节点池，请参见 [创建和管理节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool "")。




**展开查看操作流程**





  - 为节点池开启托管能力

    - 新建节点池：创建节点池的过程中选择 **托管节点池**。

    - 存量节点池：在节点池列表的 **操作** 列，单击节点池对应的 **更多** \> **开启托管**。
  - 按需启用节点池的自动化运维能力

    包括开启节点自愈、自动升级kubelet、运行时和OS版本、自动修复OS CVE漏洞等。

  - 配置集群维护窗口

    节点池的自动化运维能力需配置集群维护窗口使用，节点池会在集群维护窗口内执行自动化运维任务。

    - 新建节点池：创建节点池的过程中配置 **托管节点池** 的 **集群维护窗口**。

    - 存量节点池：在节点池列表的 **操作** 列，单击存量托管节点池对应的 **更多** \> **托管配置**，配置维护窗口。

#### **功能介绍**

|     |     |
| --- | --- |
| **功能项** | **说明** |
| 节点自愈 | ACK会自动监控节点状态，在节点发生异常时自动执行自愈任务，修复系统和K8s组件异常以及节点实例异常问题，请参见 [开启节点自愈](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-repair "")。 |
| OS CVE漏洞自动修复 | ACK将扫描节点上存在的安全漏洞，根据集群运维窗口排期并执行CVE漏洞修复计划，以提升集群稳定性、安全性、合规性。相关注意事项，请参见 [修复节点池操作系统CVE漏洞](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cve-patching#section-mbq-9wf-3oa "")。 |
| ECS系统事件自动响应 | 支持 [ECS系统事件](https://help.aliyun.com/zh/ecs/user-guide/overview-of-ecs-system-events#DAS "") 的自动响应。目前支持的系统事件类型如下。<br>- 因系统维护实例重启（SystemMaintenance.Reboot）<br>  <br>  <br>  <br>  **自动响应流程**<br>  <br>  <br>  <br>  <br>  <br>1. ACK接收到事件后，同步发送短信或站内信通知。请及时关注。<br>     <br>2. 执行操作前，ACK根据ECS的计划执行时间进行安排：<br>     <br>     - 如果节点池在计划执行时间前有可用的维护窗口，ACK会在维护窗口内执行自动响应流程。<br>       <br>     - 否则，ACK会在ECS计划执行时间的前一个小时执行该流程。<br>3. 流程开始后，ACK针对受影响的ECS实例执行 [节点排水](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-overview/#90e4f297bey1r "")（Drain），尝试将节点上的Pod迁移到其他可用节点，随后重启ECS实例。<br>     <br>**节点排水规则**<br>执行节点排水时，ACK会首先驱逐该节点上所有可安全排水的Pod，对于不能安全排水的Pod，将返回错误信息，并且终止自动响应流程。<br>以下情况的Pod被视为不能安全排水：<br>  - Pod带有Label `goatscaler.io/safe-to-evict=false`。<br>    <br>  - 不受控制器管理的 Pod（即没有 `OwnerReference` 的独立 Pod）。<br>    <br>  - Pod使用了`emptyDir`类型的卷。<br>    <br>由于排水操作会驱逐节点上的Pod，为避免节点维护影响服务的整体可用性，强烈建议：<br>  - 确保服务应用后端采用多副本（Replicas）方式部署在不同节点上。<br>    <br>  - 为重要应用配置 [PodDisruptionBudget（PDB）](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-budgets)，以避免节点上Pod被驱逐后影响服务的整体可用性。 |

> 自2026年01月31日起，托管节点池 kubelet 和容器运行时的自动升级配置入口将下线，可配置 [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "") 来完成节点池的自动升级。详情请参见 [【产品变更】关于托管节点池安全漏洞修复和自动升级的变更公告](https://help.aliyun.com/zh/ack/product-overview/announcement-on-security-vulnerabilithy-fixes-and-automatic-upgrades-for-managed-node-pools "")。

## **节点池生命周期**

ACK集群节点池的生命周期涉及多个阶段和状态，从节点池的创建部署、运行维护（扩容缩容、更新升级、节点移除等），到最终的删除。不同状态的含义和流转如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1981787671/CAEQYxiBgICksfq.0RkiIDkyNDYzNzcyNzMyYTQ1MTQ4NGI2YjU4ZWE4MzYwNTdk4458875_20240620104842.460.svg)

|     |     |
| --- | --- |
| **节点池状态** | **说明** |
| 初始化中（initial） | 正在创建节点池。 |
| 已激活（active） | 成功创建节点池，运行中。 |
| 失败（failed） | 节点池创建失败。 |
| 扩容中（scaling） | 节点池扩容中或正在添加节点。 |
| 更新中（updating） | 节点池配置更新中。 |
| 移除节点中（removing\_nodes） | 正在移除节点池中的节点。 |
| 升级中（upgrading） | 节点池升级中。 |
| 修复中（repairing） | 节点池修复中，例如修复节点池节点、节点池CVE漏洞等。 |
| 删除中（deleting） | 正在删除节点池。 |
| 已删除（deleted，该状态您不可见） | 成功删除节点池。 |
| 删除失败（deleted\_failed） | 节点池删除失败。请重新删除。<br>> 如仍然删除失败，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。 |

## 节点池计费

使用节点池和节点池提供的自动化运维能力不收费，但节点池内ECS实例等云资源由对应的云产品收取费用。

- 关于ECS实例的计费说明，请参见 [计费概述](https://help.aliyun.com/zh/ecs/billing-overview "")。

如需修改节点池中已有节点的付费类型，请参见 [按量付费转包年包月](https://help.aliyun.com/zh/ecs/change-the-billing-method-of-an-ecs-instance-from-pay-as-you-go-to-subscription-1#PAYGtoSubs-china "")。修改节点池的付费类型仅对扩容的新节点生效，不会改变节点池内已有节点的付费类型。

- 关于弹性伸缩组的计费详情，请参见 [弹性伸缩产品计费](https://help.aliyun.com/zh/auto-scaling/product-overview/billing-rules#concept-nw2-h3m-qfb "")。


## **相关术语**

首次使用节点池前，建议了解节点池相关的概念术语。

- 伸缩组：当对节点池进行扩容和缩容时，ACK通过 [弹性伸缩ESS](https://help.aliyun.com/zh/auto-scaling/product-overview/what-is-auto-scaling "") 服务下发扩容和移除节点的操作。节点池与弹性 [伸缩组](https://help.aliyun.com/zh/auto-scaling/user-guide/scaling-group-overview#concept-25880-zh "") 实例为一一对应的关系。一个伸缩组是一个或多个ECS实例（Worker节点）的合集。

- 伸缩配置：节点池底层使用伸缩配置管理节点配置。ESS伸缩配置是弹性伸缩时ECS实例使用的模板。当弹性伸缩触发弹性扩张活动后，弹性伸缩以该伸缩配置为模板自动创建ECS实例。

- 伸缩活动：节点池的每次扩缩容、添加节点、移除节点都会触发伸缩活动。触发伸缩活动后，所有扩容和缩容动作都交由系统自动完成，并留下相关记录。可通过节点池的伸缩活动查看节点池的历史伸缩活动记录。

- 替换系统盘：节点池的某些操作，例如自动添加已有节点、更换容器运行时等，会通过替换节点系统盘（替盘升级）的方式初始化节点。该节点的实例属性不发生改变，例如节点名称、实例ID、IP等，但节点系统盘上的数据将被删除。额外挂载到该节点上的数据盘不受影响。

ACK执行替盘时会进行节点排水操作，遵循 [Pod Disruption Budget（PDB）](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-budgets) 的前提下将节点上的Pod驱逐至其他可用节点。为确保服务高可用性，建议采用多副本部署策略，将工作负载分散在多个节点上，同时为关键业务配置PDB，控制同时中断的Pod数量。

- 原地升级：与替盘升级对应的一种升级方式，直接在原节点上更新替换所需的组件。原地升级不会替换系统盘，也不会重新初始化节点，原节点的数据不受影响。


## 相关文档

- 关于集群支持的Kubernetes资源（例如集群中最大支持的节点数量、Pod数量等）容量上限，请参见 [配额（Quota）](https://help.aliyun.com/zh/ack/product-overview/limits#b5010e1088jx9 "")。

- ACK支持 [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "")。

- 1.24版本的集群将不再支持使用Docker作为内置容器运行时，请迁移至containerd，请参见 [将节点容器运行时从Docker迁移到containerd](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/change-the-container-runtime-from-docker-to-containerd "")。

- 随着集群负载的增加，可启用弹性伸缩方案，动态调整节点资源，请参见 [弹性伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-scaling-overview/ "")。

- 如需指定应用Pod使用的节点池，请参见 [调度应用至指定节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/schedule-an-application-pod-to-a-specific-node-pool#task-1943757 "")。

- ACK托管集群基础版支持的节点上限为10，建议热迁移至ACK托管集群Pro版以获得更大的资源配额，请参见 [热迁移ACK托管集群基础版至ACK托管集群Pro版](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/hot-migration-from-ack-standard-clusters-to-ack-pro-clusters "")。

- 如果在使用节点或节点池的过程中遇到问题，可参见 [节点与节点池FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-management "") 进行自排查。

- ACK提供集群成本管理解决方案，请参见 [成本套件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-suite/ "")。

- 节点池相关的最佳实践，请参见 [节点与节点池最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-nodes-and-node-pools/ "")。