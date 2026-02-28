### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)弹性伸缩

# 弹性伸缩概述

更新时间：2025-08-28 21:39:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用External Metrics API获取成本数据](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/using-the-external-metrics-api-to-obtain-cost-data)[下一篇：使用容器水平伸缩（HPA）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/horizontal-pod-autoscaling)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用前说明

工作负载伸缩和计算资源伸缩

工作负载伸缩方案

计算资源伸缩方案

计费说明

常见问题

相关文档

如果您业务的资源需求不易预测或有周期性变化（例如Web应用、游戏服务、在线教育等），推荐您在集群中启用弹性伸缩。根据负载需求情况，工作负载伸缩支持自动调整应用Pod的副本数量或资源配置，计算资源伸缩支持自动调整节点资源，从而平稳应对流量峰值并降低成本。

## 使用前说明

- 本文面向集群运维人员、开发人员等介绍ACK集群的弹性伸缩方案（工作负载伸缩和节点伸缩）。建议您已了解社区工作负载伸缩方案（例如 [HPA](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)、 [VPA](https://github.com/kubernetes/autoscaler/tree/vpa-release-0.8/vertical-pod-autoscaler) 等）和节点伸缩方案（例如 [Cluster Autoscaling](https://kubernetes.io/docs/concepts/cluster-administration/cluster-autoscaling/)）的相关内容等。

- 如果您的集群为大规模集群（通常为超过500个节点或者10,000个Pod的集群），请参见 [规划集群资源弹性速率](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/suggestions-on-how-to-work-with-large-ack-pro-clusters#04a151487eqwt "") 了解相关使用建议，以确保集群和控制面的稳定性。


## 工作负载伸缩和计算资源伸缩

ACK的弹性伸缩提供以下两种维度的方案。

- 工作负载伸缩：调度层弹性方案，作用于Pod，通过增减Pod副本数量或调整Pod资源配置来适应负载变化。例如，HPA支持根据工作负载流量自动调整工作负载Pod的副本数，调整的副本数会改变当前负载占用的调度容量，从而实现调度层的伸缩。

- 计算资源伸缩：资源层弹性方案，包括节点伸缩方案和虚拟节点方案，支持根据Pod的调度情况和资源使用情况动态地添加或移除计算资源。


推荐您将两种方案搭配使用，既能通过调整工作负载Pod副本数来提高资源利用率，又能在集群维度通过调整计算资源容量来保证Pod总能获得足够的计算资源。

### 工作负载伸缩 **方案**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7551346571/CAEQURiBgICX39almhkiIDA0Y2EyMDA4MjBmZDQ4YWQ4YmY1ODRkZTZiMzQzZWM44592458_20240814161451.715.svg)

Kubernetes支持使用`kubectl scale`命令手动调整工作负载Pod的数量，但需要运维人员自行判断，仅适用于临时性的副本数管理。您可以参见下表选择方案，享受ACK工作负载伸缩方案在成本控制、稳定性保障和资源容量灵活管理等维度提供的支持。

| **方案** | **介绍** | **扩缩依据的指标** | **使用场景** | **相关文档** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **方案** | **介绍** | **扩缩依据的指标** | **使用场景** | **相关文档** |
| HPA | 在业务负载上升时快速扩容Pod副本来缓解压力，在业务负载变小时适当缩容以节省资源，是最常用的应用弹性方案。 | - 资源指标（CPU、内存使用率）<br>  <br>- 其他 [自定义指标](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#scaling-on-custom-metrics) | 服务波动较大、服务数量多且需要频繁扩缩容的在线业务场景，例如电商服务、在线教育、金融服务等。 | [使用容器水平伸缩（HPA）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/horizontal-pod-autoscaling#task-1830087 "") |
| CronHPA | 类似Crontab的策略，定时对Pod进行扩缩容，可配置时区、执行的日期、跳过执行的日期（例如节假日），支持和HPA协同使用。 | 定时扩缩容 | 业务流量有明显高峰时段、应用程序需要在特定时间执行任务等场景。 | - [使用容器定时水平伸缩（CronHPA）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cronhpa#task-2391975 "")<br>  <br>- [实现CronHPA与HPA的协同](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/make-cronhpa-compatible-with-hpa "") |
| VPA | 监控Pod的资源消耗模式，灵活推荐CPU和内存资源分配的配置，并在适当的情况下自动进行调整，而不调整Pod的副本数量。 | 推荐并自动调整Pod中容器的CPU及内存的Request和Limit | 需要稳定资源配置的有状态应用的扩容、大型单体应用等场景，通常是在Pod出现异常恢复时生效。 | [使用容器垂直伸缩（VPA）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/vertical-pod-autoscaling#task-2455855 "") |
| KEDA | 支持丰富的事件源，为工作负载提供事件驱动的自动伸缩能力。 | 事件数量，例如队列长度 | 需要即时弹性的场景，尤其是基于事件源的离线作业场景，例如音视频离线转码、事件驱动作业、流式数据处理等。 | [事件驱动弹性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-keda "") |
| AHPA | 根据业务历史指标，自动、主动识别弹性周期并对容量进行预测，提前进行弹性规划，解决弹性滞后的问题。 | - 资源指标（CPU、内存、GPU使用率）<br>  <br>- 流量指标（QPS、RT）<br>  <br>- 其他自定义指标 | 业务流量有明显周期性的场景，例如直播、在线教育、游戏服务等。 | [弹性伸缩预测（AHPA）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ahpa-overview-1/ "") |

此外，您也可以使用UnitedDeployment来定义工作负载。UnitedDeployment通过弹性单元Subset来灵活、便捷地管理多个同质的工作负载，动态分配在各Subset上的工作负载副本数量。您可以将UnitedDeployment和上述工作负载伸缩方案搭配使用，实现工作负载的灵活扩缩容与调度，例如多种计算资源混合使用场景。更多信息，请参见 [基于UnitedDeployment实现工作负载的伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-the-uniteddeployment-controller-in-ack-clusters "")。

### **计算资源伸缩方案**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7551346571/CAEQURiBgMD8zculmhkiIDVjOTRiNDg3ODhlYjRkODBiNmE2NjNmMWVhNDQ0Mzlj4592458_20240814160030.932.svg)

在业务量波动大、需要快速响应的场景下，集群需要一种能够根据工作负载变化情况自动调整计算资源的方案，以在提高系统弹性的同时降低运维成本。计算伸缩方案提供的组件会监听Pod是否处于调度失败的状态，以判断是否需要新增ECS节点或ECI Pod资源。

您可以参见 [节点伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-scaling/ "") 了解节点伸缩的功能原理。

**重要**

下表提供的资源交付数据仅为理论值（参考值），实际数据以您的操作环境为准。

| **方案** | **介绍** | **使用场景** | **资源交付速度** | **相关文档** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **方案** | **介绍** | **使用场景** | **资源交付速度** | **相关文档** |
| 节点自动伸缩 | 当集群的容量规划无法满足应用Pod调度时，自动调整节点的数量。 | 全场景通用，面向在线业务、深度学习等场景，适用于扩容规模较小（例如开启弹性的节点池数量少于20，或对应节点池中的节点数量少于100），工作负载批次较为稳定，以单次伸缩为主等业务场景。 | 以100节点为一个交付批次为例：<br>- 标准模式：120s<br>  <br>- 极速模式：60s<br>  <br>- 标准模式- [Qboot镜像](https://help.aliyun.com/zh/alinux/product-overview/alibaba-cloud-linux-overview#section-to6-5lp-7d6 "")：90s<br>  <br>- 极速模式- [Qboot镜像](https://help.aliyun.com/zh/alinux/product-overview/alibaba-cloud-linux-overview#section-to6-5lp-7d6 "")：45s | [启用节点自动伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-scaling-of-nodes#task-1893824 "") |
| 节点即时弹性 | 在节点自动伸缩的基础上，节点即时弹性在伸缩速度和效率、资源交付确定性等方面 [更具优势](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-scaling/#b4fb6d551dcou "")，还支持根据ECS实例的库存查看健康度。 | 全场景通用， 集群规模较大（例如弹性节点池中节点数大于100，或弹性节点池数大于20）、对资源交付速度有更高要求、期望灵活实现多实例规格和跨可用区自动伸缩、对高级调度策略（例如TopologySpread Constraints）有需求。 | 以100节点为一个交付批次为例：<br>- ContainerOS极速扩容：45s<br>  <br>- 标准模式：103s<br>  <br>- 极速模式：暂未支持 | - [启用节点即时弹性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-node-instant-scaling "")<br>  <br>- [查看节点即时弹性健康度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/view-the-status-of-node-instant-elastic "") |
| 虚拟节点 | 无需节点运维和容量规划，支持单集群超大Pod容量（最多可支持50000个Pod），突发业务流量场景下能够扩容工作负载Pod，实现每分钟10000 Pod弹性能力。 | 全场景通用，尤其适用于任务和定时任务、数据计算、AI、突发业务等场景。 | 以1000个Pod作为一个交付批次为例：<br>- 未开启镜像缓存：30s<br>  <br>- 开启 [镜像缓存](https://help.aliyun.com/zh/eci/user-guide/overview-of-image-caches-1 "")：15s | [将Pod调度到ECI上运行](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-the-virtual-node-controller-and-use-it-to-create-elastic-container-instance-based-pods#task-1443354 "") |

## **计费说明**

弹性伸缩功能本身不收费，但弹性伸缩组件会占用Pod资源（节点伸缩的情况下需要至少保留一个节点）。节点伸缩方案下，扩容节点资源产生的计费会正常收取。更多信息，请参见 [计费概述](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/product-overview/ack-pro-cluster-billing "")。

## **常见问题**

如您在使用弹性伸缩功能时遇到问题，可参见 [弹性伸缩FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-faq-about-auto-scaling/ "") 进行排查。

**展开查看** **节点自动伸缩** **的FAQ索引**

|     |     |     |
| --- | --- | --- |
| **分类** | **二级分类** | **跳转链接** |
| 节点自动伸缩的扩缩容行为 | [已知限制](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#0578d5906a4ve "") |
| [扩容行为相关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#3d73c9bce2x1y "") | - [cluster-autoscaler组件使用哪些调度策略来判断不可调度Pod能否调度到开启了弹性的节点池？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#5e458ca0fdeyz "")<br>  <br>- [cluster-autoscaler组件可模拟判断的资源有哪些？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#9081e1305c7f2 "")<br>  <br>- [为什么节点自动伸缩组件无法弹出节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#4bd69dc0fda87 "")<br>  <br>- [如果一个伸缩组内配置了多资源类型的实例规格，弹性伸缩时如何计算这个伸缩组的资源呢？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#29a70230fdx9t "")<br>  <br>- [弹性伸缩时，如何在多个开启弹性的节点池之间进行选择？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#5679b320fde95 "")<br>  <br>- [开启弹性的节点池如何配置自定义资源？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#fff85a7068y34 "")<br>  <br>- [为什么为节点池设置自动扩缩容失败？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#b348c46bdcxb1 "") |
| [缩容行为相关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#d965c40777nu9 "") | - [为什么cluster-autoscaler组件无法缩容节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#51d75430fdnp3 "")<br>  <br>- [如何启用或禁用特定DaemonSet的驱逐？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#section-kg5-cli-y3i "")<br>  <br>- [什么类型的Pod可以阻止cluster-autoscaler组件移除节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#4000d01068gao "") |
| [拓展支持相关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#4d35a60fc8vqv "") | [cluster-autoscaler组件是否支持CRD？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#b5fff6905c7fv "") |
| 自定义的扩缩容行为 | [通过Pod控制扩缩容行为](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#c3186b2465my5 "") | - [如何延迟cluster-autoscaler组件对不可调度Pod的扩容反应时间？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#c7d74de068d5w "") |
| [通过节点控制扩缩容行为](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#9008f67409m0b "") | - [如何指定节点不被cluster-autoscaler组件缩容？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#9197847068xlh "")<br>  <br>- [如何通过Pod Annotation影响cluster-autoscaler组件的节点缩容？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#section-mwn-b6z-apt "") |
| cluster-autoscaler组件相关 | - [如何升级cluster-autoscaler组件至最新版本？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#bb7882f068f94 "")<br>  <br>- [哪些操作会触发cluster-autoscaler组件自动更新？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#60a012b0effpp "")<br>  <br>- [ACK托管集群已经完成了角色授权，但节点伸缩活动仍然无法正常运行？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-auto-scaling#cfae8542e6jyf "") |

**展开查看** **节点即时弹性** **的FAQ索引**

|     |     |     |
| --- | --- | --- |
| **分类** | **二级分类** | **跳转链接** |
| 节点即时弹性的扩缩容行为 | [已知限制](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#dbbc106bc8vq9 "") |
| [扩容行为相关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#8cdf6cea0camp "") | - [节点即时弹性可模拟判断的资源类型有哪些？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#9c9ecbb2acns7 "")<br>  <br>- [节点即时弹性是否支持根据Pod Request资源在节点池中扩容合适资源的实例规格？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#4137b11f51wpg "")<br>  <br>- [节点池配了多个实例规格，节点即时弹性默认如何选择？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#b075558334gwl "")<br>  <br>- [使用节点即时弹性时，如何实时感知节点池中的实例规格库存变化？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#4331ccfc84sau "")<br>  <br>- [如何优化节点池配置，尽量避免库存不足而导致扩容失败？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#137ca271cat5s "")<br>  <br>- [为什么节点即时弹性无法弹出节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#b273b386cdm60 "")<br>  <br>- [开启节点即时弹性的节点池如何配置自定义资源？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#VvAtw "") |
| [缩容行为相关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#3b166483bd2uz "") | - [为什么节点即时弹性无法缩容节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#b30d4d1e9d3o6 "")<br>  <br>- [什么类型的Pod可以阻止节点即时弹性移除节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#ed53341b2943s "") |
| 自定义的扩缩容行为 | [通过Pod控制扩缩容行为](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#cbf256126a6as "") | [如何通过Pod控制节点即时弹性的节点缩容？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#e47756a141fsu "") |
| [通过节点控制扩缩容行为](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#c963086718o0w "") | - [节点即时弹性在缩容过程中如何指定需要删除的节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#7f37a07acft6o "")<br>  <br>- [如何指定节点不被节点即时弹性缩容？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#ed6ea25edd6ik "")<br>  <br>- [节点即时弹性能否仅缩容空节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#c34be0edbad6p "") |
| [节点即时弹性组件相关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#af50f8b5d0lih "") | - [是否有操作会触发节点即时弹性组件的自动更新？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#ea3469c40bxi6 "")<br>  <br>- [ACK托管集群已经完成了角色授权，但节点伸缩活动仍然无法正常运行？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-instant-scaling#6da5a6c089zxs "") |

**展开查看** **工作负载伸缩** **（包括HPA、CronHPA等）的FAQ索引**

- [HPA的监控数据current字段为何显示为unknown？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#section-7l1-a7b-adu "")

- [HPA扩缩容失败，指标获取异常怎么办？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#45cdf68a9e6bg "")

- [为何HPA在滚动时扩容出了多余的Pod？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#section-oxl-0ov-og8 "")

- [HPA到达阈值为何不进行扩缩容？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#section-1tg-5jx-p4h "")

- [HPA采集周期如何配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#section-i3r-lgt-w1n "")

- [CronHPA是否兼容HPA？如何兼容HPA？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#section-ilk-54c-4f6 "")

- [如何解决HPA启动时CPU或内存飙高造成扩容出多余Pod的多弹现象？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#section-2cl-008-8x0 "")

- [为什么HPA审计日志数值未达阈值但扩缩了？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#section-zx5-fzq-ah4 "")

- [HPA缩容时，能够决定Pod缩容的顺序吗？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#42aaf3d9a6t6z "")

- [HPA使用率指标单位的含义是什么？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#23537b1cb2y2v "")

- [如果执行kubectl get hpa后发现target一栏为unknown怎么办？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#d377a7a0689xh "")

- [如何查找HPA支持的指标名称？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#0ffcaa9068yr7 "")

- [自定义了Nginx Ingress日志格式后如何进行适配操作？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-workload-auto-scaling#72a7267068sa0 "")


## 相关文档

- 在一些预安装或者高性能场景下，您可能期望使用弹性性能优化的操作系统镜像，提高复杂场景下弹性伸缩的便捷性，请参见 [弹性优化之自定义镜像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-custom-images "")。

- 如需收集弹性伸缩的日志，请参见 [收集系统插件日志](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/collect-log-files-of-system-components#task-2136935 "")。

- 推荐您在配置工作负载时结合 [工作负载推荐配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/recommended-configurations-for-high-reliability "") 中的使用建议。

- 在Serverless容器场景下，Knative支持基于请求数或并发数扩缩容，当请求为零时可将Pod副本数量自动缩容至零，更多信息，请参见 [Knative](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/knative-overview/ "")、 [基于流量请求数实现服务自动扩缩容](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-automatic-scaling-for-pods-based-on-the-number-of-requests "")。