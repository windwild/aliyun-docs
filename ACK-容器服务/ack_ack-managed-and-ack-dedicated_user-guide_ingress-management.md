### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/)[Ingress管理](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ingress-management-2/)APIG Ingress管理

# APIG Ingress管理

更新时间：2026-01-14 07:39:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

Ingress基本概念

APIG Ingress功能介绍

APIG Ingress使用说明

APIG Ingress工作原理

组成部分

工作原理

相关文档

云原生API网关（APIG Ingress）是基于开源网关Higress的企业版产品，兼容Nginx Ingress，适用于API管理及微服务场景。

## Ingress基本概念

在Kubernetes集群中，Ingress作为集群内服务对外暴露的访问接入点，提供七层负载均衡能力，几乎承载着集群内服务访问的所有流量。Ingress是Kubernetes中的一个资源对象，用于管理集群外部访问集群内部服务的方式。通过配置Ingress资源，可实现不同的转发规则，从而根据不同的规则设置访问集群内不同的Service所对应的后端Pod。标准的Ingress资源仅支持配置HTTP流量的规则，无法配置一些高级特性，例如负载均衡的算法、Session Affinity等。这些高级特性都需要由Ingress实现者（Nginx Ingress、APIG Ingress）提供支持。

## APIG Ingress功能介绍

- [管理APIG Controller组件](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/managing-apig-controller-components "")

- [为APIG Controller授权](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/authorize-for-apig-controller "")

- [创建并使用APIG Ingress对外暴露服务](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/access-container-service-and-container-computing-through-apig-ingress "")

- [APIG Ingress支持的Annotation](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/annotations-supported-by-higress-ingress-gateways "")

- [APIG Ingress高级用法](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/advanced-usage-of-apig-ingress "")

- [Nginx Ingress和APIG Ingress网关对比](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/comparison-between-nginx-ingress-gateways-and-apig-ingress-gateways "")

- [配置ApigConfig](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/configure-apigconfig "")


## APIG Ingress使用说明

APIG Ingress是在云原生API网关之上提供更为强大的Ingress流量管理方式，是MSE云原生网关的升级版，兼容Nginx Ingress以及50多个Nginx Ingress的Annotation，覆盖90%以上的Nginx Ingress业务场景，支持多服务版本同时灰度发布、灵活的服务治理能力以及全方位的安全防护保障，能够满足大规模云原生分布式应用的流量治理诉求。APIG Ingress在兼容Nginx Ingress注解的同时，推出了额外的注解来增强流量治理和安全防护能力。更多信息，请参见 [APIG Ingress高级用法](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/advanced-usage-of-apig-ingress "")。

集群中部署APIG Controller后，该组件会监听ApigConfig资源，动态管理云原生API网关实例的生命周期、全局参数配置以及Ingress资源的监听选项。由云原生API网关负责监听和转换K8s集群中的Ingress资源为自身所需的流量治理配置，完成内部服务对外暴露。具体操作，请参见 [创建并使用APIG Ingress对外暴露服务](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/access-container-service-and-container-computing-through-apig-ingress "")。

**重要**

APIG Ingress是MSE Ingress的升级版，在同时支持APIG Ingress与MSE Ingress的地域，ACK控制台将只显示APIG Ingress相关选项，已使用MSE Ingress的用户不受影响，仍可继续新建和管理MSE Ingress。如需使用MSE Ingress，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)，联系APIG团队。

## APIG Ingress工作原理

### 组成部分

- **APIG Controller**：

  - APIG Controller本身不是网络数据平面，它是管理云原生API网关实例以及配置的控制平面。即APIG Controller不处理任何业务请求流量，它位于流量旁路，管理着处理业务流量的云原生API网关实例。

  - 在集群中 [安装APIG Controller组件](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/managing-apig-controller-components "")，通过使用该组件提供的ApigConfig的CRD资源以声明式配置的方式来管理云原生API网关实例，以及设置网关对Ingress资源的监听选项。
- **云原生API网关**：

云原生API网关由APIG Controller根据用户配置的ApigConfig资源创建，包含控制面（Control Plane）和数据面（Data Plane）。

  - 控制面（Control Plane）：控制面监听已关联的容器服务集群中的Ingress、IngressClass、Service等资源，经内部解析之后实时下发给网关数据面。

  - 数据面（Data Plane）： 数据面是流量治理配置的实施者，按照控制面下发的治理规则处理外部请求，并转发到后端目标服务。

### 工作原理

APIG Controller负责监听集群中创建的ApigConfig资源，实时动态维护该资源对应的云原生API网关实例的生命周期以及该网关与容器服务集群的关联性。

云原生API网关的控制面通过关联的容器服务集群的API Server获取Ingress资源的变化，然后动态更新云原生API网关的路由规则。当云原生API网关收到请求时，匹配Ingress转发规则并将请求转发到后端Service所对应的Pod。

Kubernetes中Service、Ingress、IngressClass、ApigConfig和APIG Controller存在以下关系：

- **Service**：是后端真实服务的抽象，一个Service可以代表多个相同的后端服务。

- **Ingress**：是反向代理规则，用来规定HTTP和HTTPS请求应该被转发到哪个Service上。例如，根据请求中不同的Host和URL路径，使请求转发到不同的Service上。

- **IngressClass**：是Ingress处理器的描述，用于在K8s集群中声明一个Ingress处理器实现，关联该IngressClass的Ingress资源会被该Ingress处理器解析。此外，需要通过IngressClass的Parameter字段关联一个ApigConfig（云原生API网关），用于实施被解析的Ingress资源描述的流量管理规则。

- **ApigConfig**：是由APIG Controller提供的CRD，用于描述云原生API网关实例的基本信息。

- **APIG Controller**：本身不是网络数据平面，它是管理云原生API网关实例以及配置的控制平面。APIG Controller负责监听集群中的ApigConfig资源，协调云原生API网关实例用于实施Ingress资源描述的流量管理规则。


下图是APIG Controller工作示意图。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4534938671/CAEQaxiBgICr6fL03BkiIGI3MDg1Y2ZmZTY2NTQwMjQ5M2QxN2M4N2Y5NjcwNmM06163959_20260108180857.380.svg)

## **相关文档**

- 如需了解如何安装APIG Controller，请参见 [管理APIG Controller组件](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/user-guide/managing-apig-controller-components "")。

- 有关APIG Ingress版本说明，请参见 [APIG Ingress 版本说明](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/product-overview/apig-ingress-version "")。

- APIG Ingress支持的地域请参见 [开服地域](https://help.aliyun.com/zh/api-gateway/cloud-native-api-gateway/product-overview/regions "")。