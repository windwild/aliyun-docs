### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用访问和流量管理](https://help.aliyun.com/zh/sae/sae-network-related-concepts-and-capabilities/)[微服务治理](https://help.aliyun.com/zh/sae/microservice-governance/)[流量治理](https://help.aliyun.com/zh/sae/traffic-governance/)管理灰度规则

# 管理灰度规则

更新时间：2025-02-26 03:57:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置无损上下线](https://help.aliyun.com/zh/sae/configure-graceful-start-and-shutdown)[下一篇：系统防护](https://help.aliyun.com/zh/sae/configure-system-protection)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

使用限制

功能入口

创建灰度规则

编辑或删除灰度规则

更多信息

对于部署在SAE的微服务应用，为了确保升级操作的安全性，您可以通过启用灰度发布（即金丝雀发布）的灰度规则进行小规模验证，验证通过后再全量升级应用。

## **前提条件**

- 已 [部署应用](https://help.aliyun.com/zh/sae/sae-application-deployment/ "")。

- 已 [开通MSE微服务治理专业版](https://help.aliyun.com/zh/mse/activate-microservices-governance#task-2140253 "")。



**说明**





使用MSE时会产生单独费用。MSE的计费说明，请参见 [微服务治理计费概述](https://help.aliyun.com/zh/mse/product-overview/billing-overview "") 和 [【产品变更】SAE集成的MSE微服务治理功能商用通知](https://help.aliyun.com/zh/sae/product-overview/product-change-commercial-notice-of-non-destructive-up-and-down-line-and-gray-rule-function "")。


## **使用限制**

仅适用于2023年11月08日起新建的微服务应用。

## **功能入口**

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在左侧导航栏，选择**微服务治理** \> **流量治理**，单击 **灰度规则** 页签。


## **创建灰度规则**

在 **灰度规则** 页面，单击 **新建灰度规则**，在 **新建灰度规则** 面板，配置相关信息，然后单击 **确定**。

**说明**

如果您是第一次使用该功能，需要在该页面单击 **开启微服务治理** 并刷新页面，才能配置灰度规则。

| **配置项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **配置项** | **说明** |
| **规则类型** | - **七层流量灰度（K8s ingress）**：可以实现在灰度批次发布过程中，将特定标记的七层流量打到灰度批次的实例上。<br>  <br>- **微服务流量灰度**：可以实现在灰度批次发布过程中，将特定标记的流量打到灰度批次的实例上。 |
| **规则名称** | 设置灰度规则名称。 |
| **规则描述** | 对灰度规则的自定义描述。 |
| **灰度类型** | 根据内容灰度。 |
| **网关实例（ALB ingress）** | 当 **规则类型** 为 **七层流量灰度（K8s ingress）** 时需要配置。<br>SAE基于ALB实现的网关路由（Ingress），具备根据域名、路径路由到不同应用的能力。您需要先为应用配置ALB实例，并创建路由规则。具体操作，请参见 [为应用设置路由规则（ALB）](https://help.aliyun.com/zh/sae/set-routing-rules-for-an-application-alb/ "")。 |
| **灰度的服务** | 当 **规则类型** 为 **七层流量灰度（K8s ingress）** 时需要配置。<br>选择需要灰度的应用及对应端口。 |
| **框架类型** | 当 **规则类型** 为 **微服务流量灰度** 时需要配置。<br>配置灰度规则应用的框架类型。<br>- **Spring Cloud**：需要设置 **Path**。<br>  <br>- **Dubbo**：需要选择 **服务方法**。 |
| **条件模式** | 当 **规则类型** 为 **微服务流量灰度** 时需要配置。配置灰度规则应用的条件模式。<br>选择 **同时满足下列条件** 或 **满足下列任一条件**。 |
| **条件列表** | 单击 **+添加新的规则条件**，可以添加多条规则。<br>- 微服务灰度流量<br>  <br>  - Spring Cloud：根据参数类型 **Cookie**、 **Header** 或 **Parameter**，设置相应的 **参数**、 **条件** 以及 **值**。<br>    <br>  - Dubbo：根据应用实际情况，设置 **参数**、 **参数值获取表达式**、 **条件** 以及 **值**。<br>- 七层流量灰度<br>  <br>  根据参数类型 **Cookie**、 **Header** 或 **来源ip**，设置对应的 **参数** 与 **值**。 |

针对 **微服务流量灰度**，您还可以单击 **+新建流量规则**，创建多个入口流量规则，多个规则可以同时生效。新增的灰度规则会显示在灰度规则列表中。

## **编辑或删除灰度规则**

在 **灰度规则** 页面，找到目标规则，在其 **操作** 列，按需选择 **编辑** 或 **删除**。

开通MSE微服务治理功能后，即使您已删除灰度规则，MSE仍然在持续计费。您可以参考以下信息，决定是否关闭微服务治理功能。

如果您无需使用微服务治理功能，为避免产生不必要的MSE费用，可以在应用 **基础信息** 页面右上角，选择**更多** \> **关闭微服务治理**，根据页面提示信息，关闭微服务治理功能。

**警告**

关闭微服务治理功能后，除服务列表外，其他微服务治理功能（包括无损上下线、灰度规则和限流降级）将无法使用，且关闭过程中会触发一次应用重启，请自行判断业务风险后再进行操作。

## **更多信息**

创建灰度规则后，您可以为应用配置灰度发布策略，进行新版本测试。以Spring Cloud微服务应用为例，SAE介绍如何灰度发布应用。具体操作，请参见 [灰度发布应用](https://help.aliyun.com/zh/sae/perform-a-canary-release-for-an-application "")。