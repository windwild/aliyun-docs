### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/)[操作指南](https://help.aliyun.com/zh/ack/ack-edge/user-guide/)[云上弹性](https://help.aliyun.com/zh/ack/ack-edge/user-guide/cloud-elasticity/)虚拟节点Serverless弹性

# 虚拟节点Serverless弹性

更新时间：2025-08-17 21:32:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：启用节点自动伸缩](https://help.aliyun.com/zh/ack/ack-edge/user-guide/auto-scaling-of-nodes)[下一篇：将Pod调度到ECI上运行](https://help.aliyun.com/zh/ack/ack-edge/user-guide/deploy-the-virtual-node-controller-and-use-it-to-create-elastic-container-instance-based-pods)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

为什么使用虚拟节点

虚拟节点是什么

功能优势

使用场景

使用限制

计费说明

快速体验

相关操作

当您需要在短时间内快速创建大量Pod时，云端ECS节点扩容速度可能无法满足要求，而预留额外的ECS节点又会产生资源浪费。借助虚拟节点，您无需提前预留和维护固定资源池，可以直接将Pod调度到虚拟节点上以弹性容器实例ECI来运行，在保障弹性的同时节约资源成本。

## **为什么使用虚拟节点**

### **虚拟节点是什么**

在ACK集群中，节点是运行工作负载的基本单位，提供实际的计算和存储资源。通常，您的ACK集群会有至少一组ECS节点池，创建Pod时，kubelet会将Pod调度到ECS节点上运行。这种架构能很好地应对流量稳定的业务。如果您的业务有不易提前预测的瞬时波峰，尽管ACK支持弹性伸缩，但ECS节点池扩容时，ECS实例的创建和启动本身会有一定的额外耗时。借助虚拟节点，您可以直接调度Pod到[阿里云弹性容器实例ECI（Elastic Container Instance）](https://cn.aliyun.com/product/eci)上运行，降低节点运维操作负担，同时避免产生闲置节点资源，降低成本。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8370845571/CAEQURiBgIDBpp3wlxkiIDA5NGU4N2ZlZjVjNTRkZDZhZTc3YzA3OWMxZmZkZjMx4075777_20231113142006.912.svg)

**重要**

相较于ECS节点，虚拟节点本身不支持自定义Label、Annotation、Taint。

虚拟节点通过 [ack-virtual-node组件](https://help.aliyun.com/zh/ack/product-overview/ack-virtual-node "") 封装计算资源，无需管理底层基础设施即可直接部署工作负载，ack-virtual-node会自动将应用Pod调度到ECI上运行。ECI是Serverless容器运行服务，一个ECI实例相当于一个Pod。使用ECI部署容器应用时，您只需要提供打包好的容器镜像，即可运行容器，并仅为容器实际运行消耗的资源付费。

### **功能优势**

虚拟节点有如下使用优势。

- **免运维**：无需关心底层资源池的创建，减少运维负担。同时，虚拟节点为托管资源，省去Kubernetes节点的常规运维操作，例如系统升级、安全补丁修复等。

- **超大容量**：最多可弹出50,000个Pod，无需提前规划容量。



**重要**





在Pod大量关联Service的情况下，建议保持在20,000个以内。

- **秒级弹性**：在极短时间内创建出数千Pod，无需担心突发业务流量因Pod创建时延受到影响。

- **安全隔离**：Pod基于ECI创建，每个容器实例底层通过轻量级虚拟化安全沙箱技术完全强隔离，容器实例间互不影响。

- **节省成本**：应用按需创建，按量计费，不运行不计费，省去资源闲置费用，同时Serverless带来更低的运维成本。


### **使用场景**

基于虚拟节点本身的特性和优势，其典型使用场景如下所示。

- **在线业务**

对于在线教育、电商等时常出现突发流量的在线业务，支持秒级扩容，避免流量激增扩容不及时可能导致的系统故障，以及平时大量闲置资源造成的浪费。

- **数据处理**

处理Spark、Presto等大批量在线数据并发任务时，可以不再因为成本原因受限于底层资源， 从而导致数据处理任务的并发度受限。支持在短时间内快速弹出数千Pod，满足大数据的在线处理诉求。

- **AI任务**

针对模型训练、模型推理等无需持续运行且需要大量计算资源的AI任务，无需预留资源，按需使用，按秒计费，降低AI推理成本。同时，支持秒级弹性，可以快速响应突发的任务需求。

- **CI/CD测试环境**

针对CI/CD过程中的批量测试任务，例如CI打包、压力测试、仿真测试等，可以借助虚拟节点随时创建和释放容器实例。支持按需使用，按秒计费，实现低成本的大规模资源供应。

- **Job和CronJob**

Job类任务无需持续运行，任务完成后，Job会自动终止，对应的Pod也会被删除。虚拟节点支持在任务完成后自动停止计费并释放计算资源，避免资源闲置浪费。


## **使用限制**

您可以在1.28及以上版本的ACK Edge集群中使用虚拟节点，使用前，请先了解其使用限制。

- 不支持DaemonSet型工作负载。您可以通过将DaemonSet重新配置为Pod的Sidecar容器来运行。

- 不支持在Pod `manifest`中指定`HostPath`和`HostNetwork`。

- 不支持Privileged特权容器。您可以使用Security Context为Pod添加Capability。



**说明**





特权容器功能正在内测中。如需体验，请提交工单申请。

- 不支持NodePort类型的Service，不支持配置Session Affinity。

- 不支持深圳金融云，不支持政务云。


## **计费说明**

虚拟节点本身不收费，在虚拟节点上运行的ECI Pod按照ECI计费规则进行计费。具体请参见 [ECI计费概述](https://help.aliyun.com/zh/eci/product-overview/billing-overview "")。

**说明**

ECI Pod采用按量付费，从Pending状态开始计费，至Succeeded或Failed状态停止计费。更多信息，请参见 [ECI Pod生命周期](https://help.aliyun.com/zh/eci/user-guide/lifecycle-of-an-elastic-container-instance-2 "")。

## **快速体验**

您可以参见 [将Pod调度到ECI上运行](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-the-virtual-node-controller-and-use-it-to-create-elastic-container-instance-based-pods "") 快速体验虚拟节点的基础用法。

## 相关操作

当您升级集群时，系统会自动校验ECI Platform Version和Kubernetes的兼容情况，对于ECI Platform Version和目标Kubernetes版本不兼容的ECI Pod，需要手动删除重建ECI Pod后，才能升级集群的Kubernetes版本。升级集群前，请确保ECI Platform Version与Kubernetes版本兼容。更多信息，请参见 [升级ECI Platform Version](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/eci-platform-version-compatibility-matrix "")。

| **支持的操作** | **说明** | **相关文档** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **支持的操作** | **说明** | **相关文档** |
| 灵活配置Pod | 在集群维度通过编写ECI Profile配置文件（名为eci-profile的ConfigMap）批量配置ECI Pod，例如指定安全组、指定交换区（即ECI Pod所在的可用区）等。配置更新后，ECI Pod无需重启，新建ECI Pod可以即时生效，存量ECI Pod滚动发布后可生效。 | [配置eci-profile](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-an-eci-profile "") |
| 对于ECI某些功能特性，例如指定ECI实例规格、启用镜像缓存以加速Pod创建、为ECI Pod分配IPv6地址、增加临时存储空间大小等，可以通过Pod Annotation来实现。 | [ECI Pod Annotation](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-annotations-1 "") |
| 调度Pod至虚拟节点 | ACK提供多种调度方案。您可以指定应用Pod只调度到虚拟节点，也可以指定Pod优先调度到ECS节点（包年包月或按量付费），并在ECS节点资源不足时再调度至虚拟节点，同时实现逆序缩容。请参见 [调度Pod至虚拟节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-and-introduction-of-virtual-node-scheduling-scheme-ack/ "") 完成调度策略的选型。 | - [开启集群虚拟节点调度策略](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-ack-serverless-cluster-virtual-node-scheduling-policy "")<br>  <br>- [将Pod调度到ECI上运行](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-the-virtual-node-controller-and-use-it-to-create-elastic-container-instance-based-pods "")<br>  <br>- [通过ACK托管集群Pro版使用ACS算力](https://help.aliyun.com/zh/cs/user-guide/access-acs-computing-power-in-an-ack-cluster "")<br>  <br>- [指定ECS和ECI的资源分配](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-eci-scaling "")<br>  <br>- [实现ECI Pod可用区打散以及亲和调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/spread-elastic-container-instance-based-pods-across-zones-and-configure-affinities "") |
| 调度Pod至指定的OS或Arch | ACK集群默认将工作负载Pod调度到x86架构的虚拟节点，并在x86节点资源不足时保持等待x86节点资源。您还可以将工作负载Pod调度至Arm架构的虚拟节点上。 | [调度至Arm虚拟节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/schedule-workloads-to-arm-based-virtual-nodes "") |
| 如果您的容器需要运行在Windows环境中，您可以在集群中添加Windows虚拟节点，并将Pod调度到该虚拟节点上。 | [（邀测）调度Pod到Windows虚拟节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-windows-based-pod "") |
| 虚拟节点最佳实践 | 通过虚拟节点运行Job任务的方式，您可以用最小的运维成本（无需调整节点数量）来应对集群计算资源高峰压力。 | [基于ECI运行Job任务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-an-elastic-container-instance-to-run-a-job "") |
| 您可以在ACK集群中使用弹性容器实例ECI运行Spark作业。通过使用ECI弹性资源并配置合适的调度策略，您可以按需创建ECI Pod，并按资源使用量按需付费，从而有效减少资源闲置带来的成本浪费，进而更加经济高效地运行Spark作业。 | [使用ECI弹性资源运行Spark作业](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/use-cases/use-eci-elastic-resources-to-run-spark-jobs-efficiently "") |
| 借助虚拟节点组件（ACK Virtual Node）仅为调度到虚拟节点上的Pod自动注入Sidecar容器，来解耦虚拟节点Pod的Sidecar容器与业务容器。 | [向虚拟节点Pod注入Sidecar容器](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/injecting-a-sidecar-container-into-a-virtual-node-pod "") |
| 通过修改Prometheus监控配置来采集指定虚拟节点的Metrics。 | [采集指定虚拟节点的Metrics](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/collect-the-metrics-of-a-specified-virtual-node "") |
| 虚拟节点支持服务发现功能，目前支持Intranet service、Headless service、ClusterIP service。 | [虚拟节点基于云解析PrivateZone的服务发现](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-alibaba-cloud-dns-privatezone-to-implement-service-discovery-on-virtual-nodes "") |
| 虚拟节点FAQ | 虚拟节点使用常见问题。 | [虚拟节点FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/virtual-node-faq "") |

、