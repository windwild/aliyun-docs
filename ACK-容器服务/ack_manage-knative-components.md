### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[Knative](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/knative-overview/)部署与管理Knative组件

# 部署与管理Knative组件

更新时间：2025-06-26 05:57:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：阿里云Knative和开源Knative对比](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-between-alibaba-cloud-knative-and-open-source-knative)[下一篇：快速部署一个Knative服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-knative-to-deploy-serverless-applications)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

快速部署Knative

相关操作

部署Knative组件

升级Knative Serving组件

相关文档

ACK Knative完全兼容社区Knative，还提供产品化的一键部署能力，无需自行购买资源搭建系统。您可以在控制台快速部署Knative并开启Knative网关，也可以按需安装Knative核心组件和多种add-on。Knative Serving组件也支持在控制台升级。

## 前提条件

已创建1.28及以上版本的ACK托管集群或ACK专有集群，且集群中Worker节点数量大于等于3个。如需升级集群，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。

## 快速部署Knative

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**应用** \> **Knative**。

3. 在 **组件管理** 页签，单击 **一键部署Knative**，选择需要安装的Knative网关，然后单击 **一键部署**。

关于几种Knative网关的选型建议，请参见 [为Knative选择网关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-between-kourier-and-alb-ingresses/ "")。






ALB



MSE



ASM



Kourier



















提供全托管的ALB Ingress能力，基于阿里云应用型负载均衡ALB（Application Load Balancer）之上更为强大的Ingress流量管理方式。具备处理复杂业务路由和证书自动发现的能力，支持HTTP、HTTPS和QUIC协议。使用ALB Ingress时，需至少选择两个虚拟交换机。



关于ALB当前支持的地域和可用区，请参见 [ALB支持的地域与可用区](https://help.aliyun.com/zh/slb/application-load-balancer/product-overview/supported-regions-and-zones#task-2087008 "")。





**重要**





如集群的网络插件为 Flannel，需配置 Knative 对应的Kubernetes Service为NodePort类型。请参见 [前提条件](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/use-alb-ingresses-in-knative#d41e21 "") 完成配置。







提供MSE Ingress能力，MSE Ingress是在MSE云原生网关之上提供更为强大的Ingress流量管理方式，兼容Nginx Ingress以及50多个Nginx Ingress的注解，覆盖90%以上的Nginx Ingress业务场景。支持多服务版本同时灰度发布、灵活的服务治理能力以及全方位的安全防护保障，能够满足大规模云原生分布式应用的流量治理诉求。



阿里云服务网格（Service Mesh，简称ASM）提供一个全托管式的服务网格平台，兼容社区Istio开源服务网格，用于简化服务的治理，包括服务调用之间的流量路由与拆分管理、服务间通信的认证安全以及网格可观测性能力，从而极大地减轻开发与运维的工作负担。



由Knative社区提供的网关，提供基本的服务路由访问能力。Kourier组件部署在用户侧集群，需要您自行维护。





**说明**





在ACK Serverless集群中使用Kourier网关需要开启PrivateZone（或CoreDNS）。






部署成功后，您可以单击 **进入组件管理**，查看组件信息；单击 **进入服务管理**，查看Knative应用信息。![查看部署结果](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2815820661/p477183.png)


### **相关操作**


   - 部署未安装的组件：在 **组件管理** 页签， **状态** 为 **未部署** 的组件的右侧，单击 **部署**，在弹出的对话框中，单击 **确定**。

   - 卸载组件：在 **组件管理** 页签，单击目标组件右侧 **操作** 列下的 **卸载**，在弹出的对话框，单击 **确定**。

   - 卸载Knative：在 **组件管理** 页签，单击右上角的 **一键卸载**，在弹出的对话框，选中 **我已知晓并确认卸载Knative**，单击 **确认**。

## **部署Knative组件**

Knative提供核心组件Knative Serving和Knative Eventing，同时也支持多种add-on组件来扩展Knative服务的功能，包括事件源组件GitHub、Kafka等。您可以通过控制台部署和管理组件。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**应用** \> **Knative**。

3. 在 **状态** 为 **未部署** 的组件右侧，单击 **部署**，然后在弹出的对话框，单击 **确定**。

组件 **状态** 显示为 **已部署** 时，表示部署成功。

对于无需使用的组件，您可以单击目标组件右侧 **操作** 列下的 **卸载**，按照页面指引完成卸载。



**重要**





卸载Knative组件会删除所有的Knative自定义资源（CRD）以及Knative Service资源，请谨慎操作。


## 升级Knative Serving组件

Knative Serving组件是Knative的核心组件，负责管理Serverless工作负载，提供了应用部署、多版本管理、基于请求的自动弹性、灰度发布等能力，而且在没有业务流量时可以将应用实例缩容至0。建议您在业务运行低谷时通过控制台及时升级Knative Serving组件，以使用最新的功能特性和缺陷修复。

> 目前仅支持托管版 Knative 升级操作。关于Knative Serving组件的版本变更记录，请参见 [Knative版本发布说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/knative-version-release-notes1 "")。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

3. 选择 Knative 组件，按照页面指引在组件卡片区域升级组件。

升级完成后，页面将显示升级成功的信息。


## **相关文档**

- 关于如何根据业务类型选择合适的Knative网关，请参见 [为Knative选择网关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-between-kourier-and-alb-ingresses/ "")。

- 您可以参见 [快速部署一个Knative服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-knative-to-deploy-serverless-applications "") 快速部署一个Knative服务。

- 关于如何基于流量请求数实现Knative服务的自动扩缩容，请参见 [基于流量请求数实现服务自动扩缩容](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-automatic-scaling-for-pods-based-on-the-number-of-requests "")。

- 关于如何部署Knative Eventing组件并实现Knative的事件驱动，请参见 [Knative事件驱动](https://help.aliyun.com/zh/ack/knative-eventing "")。