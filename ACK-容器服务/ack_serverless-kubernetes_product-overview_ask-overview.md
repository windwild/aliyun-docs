### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Serverless集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/)[产品概述](https://help.aliyun.com/zh/ack/serverless-kubernetes/product-overview/)什么是容器服务 Serverless 版

# 什么是容器服务 Serverless 版

更新时间：2025-02-17 02:48:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：计费说明](https://help.aliyun.com/zh/ack/serverless-kubernetes/product-overview/ack-serverless-cluster-billing-instructions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

产品简介

核心优势

ACK Serverless集群与ACK集群的对比

应用场景

核心功能

ECI Profile

虚拟节点

Pod配置

网络管理

存储管理

可观测性

镜像管理

弹性伸缩

授权管理

集群管理

组件管理

应用管理

计费说明

使用限制

联系我们

本文介绍阿里云容器服务 Serverless 版的产品简介、核心优势、与ACK集群对比、应用场景、核心功能等信息，帮助您快速了解ACK Serverless集群。

## 产品简介

**重要**

从2025年02月17日起，阿里云容器服务 Serverless 版将对尚未创建过集群的新用户关闭创建集群的入口。您可以通过容器计算服务 ACS（Container Compute Service）使用Serverless容器算力，ACS集群能够支持企业级K8s容器化应用的全生命周期管理，为您提供更强大的功能和更便捷的服务。关于ACS的详细介绍，请参见 [ACS产品简介](https://help.aliyun.com/zh/cs/product-overview/product-introduction "")。

- 对于尚未创建过ACK Serverless集群的新用户，我们已关闭新建ACK Serverless集群的入口。您可以通过以下方式使用Serverless容器算力：

1. 创建ACS集群，并在其中使用Serverless容器算力。详细操作，请参见 [创建ACS集群](https://help.aliyun.com/zh/cs/user-guide/create-an-acs-cluster "")。

2. 在ACK集群Pro版中按需弹性使用Serverless容器算力。详细操作，请参见 [通过ACK托管集群Pro版使用ACS算力](https://help.aliyun.com/zh/cs/user-guide/access-acs-computing-power-in-an-ack-cluster "")。
- 对于正在使用ACK Serverless集群的存量用户，您现有ACK Serverless集群的使用以及在默认额度内的新建操作不受此次变更的任何影响，您可以继续按照现有的帮助文档正常进行相关操作，无需担心业务中断或调整。


关于此次调整的详细内容，请参见 [【产品变更】关于ACK Serverless集群对新用户关闭新建入口的公告](https://help.aliyun.com/zh/ack/product-overview/product-change-announcement-on-deprecation-of-cluster-creation-interface-for-ack-serverless-clusters "")。

容器服务 Serverless 版是阿里云推出的无服务器[Kubernetes](https://www.aliyun.com/getting-started/what-is/what-is-kubernetes "")[容器](https://www.aliyun.com/getting-started/what-is/what-is-container "")服务。在容器服务 Serverless 版提供的ACK Serverless集群中，您无需购买节点即可直接部署容器应用，无需对集群进行节点维护和容量规划，并且根据应用配置的[CPU](https://www.aliyun.com/getting-started/what-is/what-is-cpu "")和内存资源量进行按需付费。ACK Serverless集群提供完善的Kubernetes兼容能力，同时降低了Kubernetes使用门槛，让您更专注于应用程序，而不是管理底层基础设施。

ACK Serverless集群中的Pod基于阿里云弹性容器实例ECI运行在安全隔离的容器运行环境中。每个Pod容器实例底层通过轻量级[虚拟化](https://www.aliyun.com/getting-started/what-is/what-is-virtualization "")安全沙箱技术完全强隔离，容器实例间互不影响。

ACK Serverless集群包括ACK Serverless集群基础版和ACK Serverless集群Pro版。ACK Serverless集群Pro版是在ACK Serverless集群基础版的基础上，针对企业大规模生产环境进一步增强了可靠性、安全性，并且提供可赔付SLA的ACK Serverless集群。关于ACK Serverless集群Pro版的更多信息，请参见 [集群概述](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/ask-pro-cluster-overview#concept-2122705 "")。

什么是容器服务 Serverless 版

## 核心优势

| **核心优势** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **核心优势** | **说明** |
| 开箱即用 | 低门槛快速创建集群，无需管理Kubernetes节点和服务器即可直接部署应用。 |
| 超大容量 | 集群无需额外配置即可轻松获得最多50,000个Pod容量，无需提前规划容量。<br>**重要**<br>在Pod大量关联 Service的情况下，建议保持在20,000个以内。 |
| 秒级弹性 | 始终确保在极短时间内创建出数千Pod，无需担心突发业务流量因Pod创建时延受到影响。 |
| 弹性预测 | 依据历史预测资源用量提前准备，突发业务流量处理更加平滑。 |
| 原生兼容 | 完善的Kubernetes兼容性，支持原生Kubernetes应用和生态，无缝迁移Kubernetes应用。 |
| 安全隔离 | Pod基于 [ECI服务](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/overview-of-elastic-container-instances#task-2423216 "") 创建，每个容器实例底层通过轻量级虚拟化安全沙箱技术完全强隔离，容器实例间互不影响。 |
| 降低成本 | 应用按需创建，按量计费，不运行不计费，没有资源闲置费用，同时Serverless带来更低的运维成本。 |
| 服务集成 | 支持容器应用与阿里云基础服务无缝整合；支持容器与虚拟机应用的互联互通。 |
| [Pro版集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/ask-pro-cluster-overview#concept-2122705 "") | 丰富的产品层次能力，支持更高等级可靠性、SLA和更大集群容量。支持基础版无缝迁移到Pro版。 |

## ACK Serverless集群与ACK集群的对比

如下图所示，左侧为ACK集群，右侧为ACK Serverless集群。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5848779371/CAEQNBiBgICbhqmg4hgiIGE1OWM1ZGVjY2U2OTRlN2NhOTAxNGFhM2E0ZmZhNTMz3963382_20230830144006.372.svg)

## 应用场景

| **应用场景** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **应用场景** | **说明** |
| 应用托管 | ACK Serverless集群中无需管理和维护节点，无需容量规划，极大降低业务的基础设施管理和运维成本。 |
| 突发业务 | 对于有明显的波峰波谷特征的业务负载，例如在线教育、电子商务等行业，ACK Serverless集群的秒级伸缩能力可以显著降低计算成本，减少闲置资源浪费，平滑应对突发流量高峰。更多信息，请参见 [弹性伸缩概述](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/auto-scaling-overview#concept-1962638 "")。 |
| 数据计算 | 面对Spark等数据计算需求，ACK Serverless集群可以在短时间内启动大量Pod及时处理任务，计算结束时Pod自动释放停止计费，极大降低整体计算成本。更多信息，请参见 [通过ACK Serverless创建Spark计算任务](https://help.aliyun.com/zh/ack/serverless-kubernetes/use-cases/use-ask-to-create-spark-tasks#task-2495864 "")。 |
| CI/CD | 基于ACK Serverless集群搭建Jenkins或Gitlab-Runner等持续集成环境，并快速完成应用源码编译、镜像构建和推送以及应用部署的流水线，各持续集成任务之间安全隔离互不影响，同时无需维护固定资源池，降低计算成本。更多信息，请参见 [在ACK Serverless集群中部署Jenkins并完成应用构建和部署](https://help.aliyun.com/zh/ack/serverless-kubernetes/use-cases/deploy-jenkins-in-an-ask-cluster-and-then-create-and-deploy-an-application "")、 [ACK Serverless弹性低成本CI/CD](https://help.aliyun.com/zh/ack/elastic-and-cost-effective-ci-cd-based-on-ask#task-2404873 "")。 |
| 定时任务 | 在ACK Serverless集群中运行定时任务，任务结束后停止计费。无需维护固定资源池，避免资源闲置浪费。更多信息，请参见 [容器定时伸缩（CronHPA）](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/cronhpa#task-2391975 "")。 |

## 核心功能

ACK Serverless集群提供完善的Kubernetes兼容性，除原生Kubernetes功能外，建议您在将生产业务部署到ACK Serverless集群前关注如下功能。

### ECI Profile

ACK Serverless集群底层基于 [ECI服务](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/overview-of-elastic-container-instances#task-2423216 "") 来运行Pod，通过 [配置ECI Profile](https://help.aliyun.com/zh/ack/configure-elastic-container-instance-profile#topic-2073229 "")，您可以更加细粒度地控制Pod及Pod相关的集群行为。ECI Profile本质是位于kube-system命名空间下的名为eci-profile的ConfigMap，主要字段说明如下：

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| vpcId | Pod所在 [专有网络](https://help.aliyun.com/zh/vpc/what-is-vpc#concept-kbk-cpz-ndb "") 的唯一标识。 |
| securityGroupId | 专有[安全组](https://www.aliyun.com/getting-started/what-is/what-is-a-security-group "")的唯一标识。 |
| vSwitchIds | 专有网络内 [交换机](https://help.aliyun.com/zh/vpc/user-guide/overview-of-vpcs-and-vswitches/#concept-sgp-twv-dgb "") 的唯一标识，可配置多个半角逗号（,）间隔。虚拟节点将基于交换机生成。 |
| selectors | Pod选择器。支持基于命名空间和Label选择Pod，并自动追加Annotation或Label。 |
| enableClusterIp | 是否启用ClusterIP。默认为true。 |
| enableLogController | 是否启用阿里云日志控制器。默认为false。 |
| enablePVCController | 是否启用PVC控制器。默认为false。 |
| enablePrivateZone | 是否启用PrivateZone服务发现能力。默认为false。 |
| featureGates | 不稳定功能门禁开关。 |

更多详细说明，请参见 [ECI实例概述](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/overview-of-elastic-container-instances#task-2423216 "")。

### 虚拟节点

使用ACK Serverless集群时，您无需再管理节点，但为了保持与原生Kubernetes的兼容性，您仍可以在集群中看到虚拟节点。虚拟节点拥有超大的计算资源容量，让ACK Serverless集群获得极大的弹性能力，而不必担心突发业务流量。虚拟节点依据eci-profile ConfigMap中的`vSwitchIds`生成，本身不占用任何计算资源。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5848779371/CAEQQRiBgMCSyI2L9RgiIDY2NWI2ZDE3NmMzNjRjMTlhYTE3OGY5ZTkzYjBkZGVm3963382_20230830144006.372.svg)

### Pod配置

在ACK Serverless集群中创建Pod，您可以通过添加Annotation来定制Pod，详情请参见下表：

**重要**

- 下表列举的Annotation仅适用于创建到虚拟节点上的Pod（即ECI实例），调度到普通节点上的Pod不受这些Annotation影响。

- Annotation请添加在Pod的`metadata`下，例如：配置Deployment时，Annotation需添加在`spec.template.metadata`下。

- Pod Annotation的优先级高于ECI Profile中配置的相同功能。


| **参数** | **示例值** | **描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **示例值** | **描述** | **相关文档** |
| k8s.aliyun.com/eci-security-group | sg-bp1dktddjsg5nktv\*\*\*\* | 安全组ID。 | [配置ECI实例所属安全组](https://help.aliyun.com/zh/eci/user-guide/assign-a-security-group-2#topic-1918283 "") |
| k8s.aliyun.com/eci-vswitch | vsw-bp1xpiowfm5vo8o3c\*\*\*\* | 交换机ID，支持指定多个交换机实现多可用区功能。 | [多可用区创建实例](https://help.aliyun.com/zh/eci/user-guide/specify-multiple-zones-to-create-an-elastic-container-instance#topic-1876030 "") |
| k8s.aliyun.com/eci-schedule-strategy | vSwitchOrdered | 多可用区调度策略。取值范围：<br>- vSwitchOrdered：按顺序。<br>  <br>- vSwitchRandom：随机。 |
| k8s.aliyun.com/eci-ram-role-name | AliyunECIContainerGroupRole | RAM角色，赋予ECI访问阿里云产品的能力。 | [设置RAM角色](https://help.aliyun.com/zh/eci/user-guide/pod-annotations-1#section-7be-tel-tpu "") |
| k8s.aliyun.com/eci-use-specs | 2-4Gi,4-8Gi,ecs.c6.xlarge | ECI实例规格，支持指定多规格，包括指定vCPU和内存，或者ECS规格。 | [多规格创建实例](https://help.aliyun.com/zh/eci/user-guide/specify-multiple-specifications-to-create-an-elastic-container-instance#topic-1860149 "") |
| k8s.aliyun.com/eci-spot-strategy | SpotAsPriceGo | 抢占式实例策略。取值范围：<br>- SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。<br>  <br>- SpotWithPriceLimit：设置抢占实例价格上限。 | [创建抢占式实例](https://help.aliyun.com/zh/eci/user-guide/create-a-preemptible-elastic-container-instance#topic-1876161 "") |
| k8s.aliyun.com/eci-spot-price-limit | 0.5 | 抢占式实例价格。<br>**说明**<br>仅当k8s.aliyun.com/eci-spot-strategy设置为SpotWithPriceLimit时有效。 |
| k8s.aliyun.com/eci-cpu-option-core | 2 | CPU物理核心数。 | [自定义CPU选项](https://help.aliyun.com/zh/eci/customize-cpu-options#topic-2020903 "") |
| k8s.aliyun.com/eci-cpu-option-ht | 1 | 每核线程数。 |
| k8s.aliyun.com/eci-reschedule-enable | "true" | 是否开启ECI重调度。 | [ECI Pod Annotation](https://help.aliyun.com/zh/ack/eci-pod-annotation#section-vdd-xk3-ppb "") |
| k8s.aliyun.com/pod-fail-on-create-err | "true" | 创建失败的ECI实例是否体现Failed状态。 | [ECI Pod Annotation](https://help.aliyun.com/zh/ack/eci-pod-annotation#section-z7f-6a1-66z "") |
| k8s.aliyun.com/eci-image-snapshot-id | imc-2zebxkiifuyzzlhl\*\*\*\* | 指定镜像[缓存](https://www.aliyun.com/getting-started/what-is/what-is-cache "")ID。<br>**说明**<br>使用镜像缓存支持手动指定和自动匹配两种方式，建议使用自动匹配方式。 | [使用ImageCache加速创建Pod](https://help.aliyun.com/zh/eci/user-guide/use-imagecache-to-accelerate-the-creation-of-pods#topic-1860150 "") |
| k8s.aliyun.com/eci-image-cache | "true" | 自动匹配镜像缓存。<br>**说明**<br>使用镜像缓存支持手动指定和自动匹配两种方式，建议使用自动匹配方式。 |
| k8s.aliyun.com/acr-instance-id | cri-j36zhodptmyq\*\*\*\* | ACR企业版实例ID。<br>支持跨地域指定ACR企业版实例，此时需在实例ID前加上所属地域，例如"cn-beijing:cri-j36zhodptmyq\*\*\*\*"。 | [免密拉取ACR企业版镜像](https://help.aliyun.com/zh/eci/user-guide/pull-images-from-a-container-registry-enterprise-edition-instance-without-using-a-secret-2#topic-1986148 "") |
| k8s.aliyun.com/eci-eip-instanceid | eip-bp1q5n8cq4p7f6dzu\*\*\*\* | EIP实例ID。 | [为ECI实例绑定EIP](https://help.aliyun.com/zh/eci/user-guide/enable-internet-access#section-9su-qdv-b58 "") |
| k8s.aliyun.com/eci-with-eip | "true" | 是否自动创建并绑定EIP。 |
| k8s.aliyun.com/eip-bandwidth | 5 | EIP带宽。 |
| k8s.aliyun.com/eip-common-bandwidth-package-id | cbwp-2zeukbj916scmj51m\*\*\*\* | 共享带宽包ID。 |
| k8s.aliyun.com/eip-isp | BGP | EIP线路类型，仅按量付费的EIP支持指定。取值范围：<br>- BGP：BGP（多线）线路。<br>  <br>- BGP\_PRO：BGP（多线）精品线路。 |
| k8s.aliyun.com/eip-internet-charge-type | PayByBandwidth | EIP的计量方式。取值范围：<br>- PayByBandwidth：按带宽计费。<br>  <br>- PayByTraffic：按流量计费。 |
| k8s.aliyun.com/eci-enable-ipv6 | "true" | 是否绑定一个IPv6地址。 | [为ECI Pod分配IPv6地址](https://help.aliyun.com/zh/eci/user-guide/assign-an-ipv6-address-to-an-elastic-container-instance#topic-1860116 "") |
| k8s.aliyun.com/eci-ipv6-bandwidth-enable | "true" | 是否开通ECI的IPv6公网通信能力。 |
| k8s.aliyun.com/eci-ipv6-bandwidth | 100M | 设置IPv6地址的公网带宽峰值。 |
| kubernetes.io/ingress-bandwidth | 40M | 入方向带宽。 | [限制ECI实例的出入带宽](https://help.aliyun.com/zh/eci/user-guide/limit-the-bandwidth-of-an-elastic-container-instance#topic-1999563 "") |
| kubernetes.io/egress-bandwidth | 20M | 出方向带宽。 |
| k8s.aliyun.com/eci-extra-ephemeral-storage | 50Gi | 临时存储空间大小。 | [增加临时存储空间大小](https://help.aliyun.com/zh/eci/user-guide/increase-the-capacity-of-the-temporary-storage-space-1#topic-2043552 "") |
| k8s.aliyun.com/eci-eviction-enable | "true" | 设置自动驱逐临时存储空间不足的ECI Pod。 | [设置自动驱逐临时存储空间不足的Pod](https://help.aliyun.com/zh/eci/automatically-evict-pods-whose-temporary-storage-spaces-are-insufficient#topic-2217732 "") |
| k8s.aliyun.com/eci-core-pattern | /pod/data/dump/core | Core dump文件保存目录。 | [查看Core dump文件](https://help.aliyun.com/zh/eci/user-guide/use-coredump-to-analyze-instance-program-exceptions-1#topic-1891689 "") |
| k8s.aliyun.com/eci-ntp-server | 100.100.\*.\* | NTP Server。 | [为Pod配置NTP服务](https://help.aliyun.com/zh/eci/user-guide/configure-the-ntp-service-1#topic-1860142 "") |
| k8s.aliyun.com/plain-http-registry | "harbor\*\*\*.pre.com,192.168.XX.XX:5000,reg\*\*\*.test.com:80" | 自建镜像仓库地址。<br>使用HTTP协议的自建镜像仓库中的镜像创建ECI实例时，需配置该参数，使ECI使用HTTP协议拉取镜像，避免因协议不同而导致镜像拉取失败。 | [使用自建镜像仓库](https://help.aliyun.com/zh/eci/user-guide/use-self-managed-image-repositories#topic-2161955 "") |
| k8s.aliyun.com/insecure-registry | "harbor\*\*\*.pre.com,192.168.XX.XX:5000,reg\*\*\*.test.com:80" | 取值为自建镜像仓库地址。<br>使用自签发证书的自建镜像仓库中的镜像创建ECI实例时，需配置该参数来跳过证书认证，避免因证书认证失败而导致镜像拉取失败。 |

更多详细说明，请参见 [ECI Pod Annotation](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/overview-of-elastic-container-instances#section-lzk-fxi-dkt "")。

### 网络管理

集群中的ECI Pod默认使用Host网络模式，占用交换机[vSwtich](https://www.aliyun.com/getting-started/what-is/what-is-a-vswitch "")的一个弹性网卡ENI资源，与VPC内的ECS、RDS互联互通。

| **类型** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **类型** | **说明** |
| Service | - 支持创建ClusterIP、LoadBalancer类型的Service。<br>  <br>- 不支持NodePort类型的Service、不支持配置Session Affinity。<br>  <br>  <br>  <br>  **说明**<br>  <br>  <br>  <br>  <br>  <br>  ACK Serverless集群中不支持节点相关的功能 |
| Ingress | - SLB Ingress：无需部署Controller直接使用基于SLB七层转发提供的Ingress能力，请参见 [Ingress示例](https://github.com/AliyunContainerService/serverless-k8s-examples/tree/master/ingress-alb)。<br>  <br>- Nginx Ingress：部署Nginx Ingress Controller后可以创建Nginx Ingress，请参见 [ingress-nginx示例](https://github.com/AliyunContainerService/serverless-k8s-examples/tree/master/ingress-nginx)。 |
| 服务发现 | 如果您的集群内部应用需要Service的服务发现功能，请在创建集群时开启PrivateZone或CoreDNS。您也可以在集群创建后 [通过ECI Profile开启PrivateZone](https://help.aliyun.com/zh/ack/serverless-kubernetes/product-overview/ask-overview?spm=a2c4g.11186623.0.i1#section-pef-hq8-5vh "") 或通过 [组件管理](https://help.aliyun.com/zh/ack/manage-system-components#task-z3j-tvk-2gb "") 安装CoreDNS组件。 |
| [弹性公网IP](https://www.aliyun.com/getting-started/what-is/what-is-elastic-ip-address "") | 支持给ECI Pod挂载EIP，可自动创建或者绑定到已有的EIP实例。 |

### 存储管理

Pod支持挂载阿里云[块存储](https://www.aliyun.com/getting-started/what-is/what-is-block-storage "")和[文件存储](https://www.aliyun.com/getting-started/what-is/what-is-file-storage "")。

| **存储方式** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **存储方式** | **说明** |
| 阿里云块存储（Disk） | - 使用Flexvolume方式挂载：无需安装Flexvolume插件。您可以选择指定DiskID挂载，详情请参见 [disk-flexvolume-static.yaml示例](https://github.com/AliyunContainerService/serverless-k8s-examples/blob/master/volumes/disk-flexvolume-static.yaml)；或者您也可以动态创建云盘，详情请参见 [disk-flexvolume-dynamic.yaml示例](https://github.com/AliyunContainerService/serverless-k8s-examples/blob/master/volumes/disk-flexvolume-dynamic.yaml)。<br>  <br>- 使用PV/PVC动态创建云盘后挂载：安装disk-controller后即可动态创建云盘后挂载，详情请参见 [disk-pvc-dynamic.yaml示例](https://github.com/AliyunContainerService/serverless-k8s-examples/blob/master/volumes/disk-pvc-dynamic.yaml)。 |
| 阿里云文件存储（NAS） | - 使用NFS Volume：支持使用NFS方式挂载NAS目录，详情请参见 [nas-nfsvolume.yaml示例](https://github.com/AliyunContainerService/serverless-k8s-examples/blob/master/volumes/nas-nfsvolume.yaml)。<br>  <br>- 使用Flexvolume静态挂载：无需安装Flexvolume插件，直接指定NAS挂载地址，详情请参见 [nas-flexvolume.yaml示例](https://github.com/AliyunContainerService/serverless-k8s-examples/blob/master/volumes/nas-flexvolume.yaml)。<br>  <br>- 使用PV/PVC静态挂载：安装disk-controller后即可使用PVC静态挂载NAS目录挂载，详情请参见 [nas-pvc.yaml示例](https://github.com/AliyunContainerService/serverless-k8s-examples/blob/master/volumes/nas-pvc.yaml)。 |

### 可观测性

| **功能** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **功能** | **说明** |
| 日志 | 在ACK Serverless集群中，您可以通过编辑 [eci-profile](https://help.aliyun.com/zh/ack/configure-elastic-container-instance-profile#topic-2073229 "") 来启用日志服务，之后将开始收集Pod日志，详情请参见 [通过Pod环境变量采集应用日志](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/use-log-service-to-collect-application-logs#task-1830627 "")。 |
| 监控 | 您可以通过组件安装arms-prometheus组件启用集群监控，详情请参见 [阿里云Prometheus监控](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/enable-prometheus-service#task-1962610 "")。 |

### 镜像管理

- ACK Serverless集群支持通过ImageCache来加速创建Pod，这对快速响应您的业务至关重要。关于如何为Pod启用ImageCache，请参见 [使用ImageCache](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/use-image-caches-to-accelerate-the-creation-of-pods#topic-2175725 "")。

- 当您在ACK Serverless集群中创建Pod使用的镜像来自ACR，还可以通过 [配置ACR企业版免密](https://help.aliyun.com/zh/ack/pull-images-from-container-registry-enterprise-edition-instances-without-passwords#topic-2175712 "") 来简化配置。


### 弹性伸缩

ACK Serverless集群中没有真实节点，所以无需考虑节点的容量规划，也无需考虑基于cluster-autoscaler的节点扩容，您只需要关注应用的按需扩容。建议您配置HPA或者CronHPA策略进行Pod的灵活按需扩容，详情请参见 [弹性伸缩概述](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/auto-scaling-overview#concept-1962638 "")。

### 授权管理

如果您的业务Pod需要访问阿里云云产品，您可以通过 [配置RRSA（RAM Roles for Service Accounts）](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/use-rrsa-to-authorize-pods-to-access-different-cloud-services#task-2142941 "") 来通过云产品鉴权。

### 集群管理

| **类型** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **类型** | **说明** |
| 智能运维 | 您可以通过 [智能运维](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-cluster-diagnostics/#task-2101622 "") 来定期检查ACK Serverless集群的健康度，或者进行集群升级或迁移的前置检查。 |
| 升级 | ACK Serverless集群支持集群无缝升级，您无需担心业务受影响。 |
| Pro版 | 提供更高等级可靠性、SLA和更大集群容量。 |
| 迁移 | 支持将试用体验或者早期的ACK Serverless集群基础版无缝迁移到ACK Serverless集群Pro版以获得更高等级保证。 |

### 组件管理

ACK Serverless集群提供多种类型的组件以扩展集群功能，您可以根据业务需求部署、升级和卸载组件。具体操作，请参见 [管理组件](https://help.aliyun.com/zh/ack/manage-system-components#task-z3j-tvk-2gb "")。

#### **组件托管**

为简化集群运维，让您更专注于应用程序，ACK Serverless集群提供部分系统组件托管能力。例如，在ACK Serverless集群中创建的Kubernetes核心组件会被托管，包括Kube Scheduler、Cloud Controller Manager、Kube Controller Manager和Kube API Server等。除Kubernetes核心组件外，ACK Serverless集群会逐步上线存储、网络、监控等系统组件的托管形态。

**重要**

组件托管后仍会在集群中创建ClusterRole、ClusterRoleBinding、ServiceAccount、Service、ConfigMap等对象，这些对象不会占用实际的ECI资源。为确保集群正常运行，请勿修改这些对象。

托管组件由ACK Serverless集群负责部署和维护，但您仍可以在ACK Serverless集群中使用相同的[API](https://www.aliyun.com/getting-started/what-is/what-is-api "")与组件进行交互。托管组件具有如下优势：

- 不占用您账户下的ECI实例资源，节约开销。

- 无需自行部署和维护，自动化机制会确保组件处于最佳运行状态。

- 支持高可用架构。


### 应用管理

支持在[容器服务管理控制台](https://cs.console.aliyun.com/)通过 **应用市场** 安装Helm应用，并通过 **Helm** 页面进行管理。具体操作，请参见 [使用Helm简化应用部署](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-helm-to-simplify-application-deployment/#task-1779943 "")。

## 计费说明

ACK Serverless集群分为ACK Serverless集群基础版和ACK Serverless集群Pro版，不同类型集群的计费项和计费标准不同，详情请参见 [计费说明](https://help.aliyun.com/zh/ack/serverless-kubernetes/product-overview/ack-serverless-cluster-billing-instructions#concept-2122856 "")。

## 使用限制

使用ACK Serverless集群前，需要注意以下使用限制：

- 不支持DaemonSet型工作负载。您可以通过将DaemonSet重新配置为Pod的Sidecar容器来运行。

- 不支持在Pod `manifest`中指定`HostPath`和`HostNetwork`。

- 不支持Privileged特权容器。您可以使用Security Context为Pod添加Capability。



**说明**





特权容器功能正在内测中。如需体验，请提交工单申请。

- 不支持NodePort类型的Service，不支持配置Session Affinity。

- 不支持深圳金融云，不支持政务云。


## 联系我们

欢迎您使用钉钉搜索钉钉群号 **31544226** 加入ACK Serverless集群钉钉群。