### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[产品概述](https://help.aliyun.com/zh/sae/product-overview/)[动态与公告](https://help.aliyun.com/zh/sae/product-overview/announcements-and-updates/)[功能发布记录](https://help.aliyun.com/zh/sae/product-overview/function-release-record/)功能发布记录（2023年~2024年）

# 功能发布记录（2023年~2024年）

更新时间：2025-03-06 00:21:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：功能发布记录（2025年~2026年）](https://help.aliyun.com/zh/sae/product-overview/release-notes-2025)[下一篇：功能发布记录（2018~2022年）](https://help.aliyun.com/zh/sae/product-overview/release-notes-from-2018-to-2022)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

2024年11月30日

2024年10月30日

2024年09月05日

2024年08月29日

2024年08月05日

2024年07月12日

2024年05月21日

2024年03月30日

2024年01月30日

2023年12月19日

2023年12月07日

2023年11月14日

2023年10月25日

2023年10月24日

2023年09月30日

2023年08月07日

2023年03月30日

2023年01月09日

功能发布历史记录

本文介绍Serverless 应用引擎 SAE（Serverless App Engine）2023年至2024年发布涉及的功能新增、优化、重要问题修复及对应的文档，帮助您了解SAE的发布动态。

## 2024年11月30日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 云原生API网关 | 新增 | 新增APIG云原生API网关集成，并支持MSE Nacos和SAE K8s Service两种注册中心。 | [为应用设置路由规则（API网关）](https://help.aliyun.com/zh/sae/set-up-a-cloud-native-api-gateway-for-your-application "") |
| Kubernetes YAML | 新增 | - Kubernetes YAML支持在SAE中进行灰度应用发布。<br>  <br>- Kubernetes YAML支持使用Jar包部署应用。 | [使用saectl工具管理应用](https://help.aliyun.com/zh/sae/use-saectl-tool-to-configure-an-application "") |
| 部署Python应用 | 优化 | 使用代码包部署Python应用时，启动命令为必填项。 | [使用ZIP包部署PHP应用](https://help.aliyun.com/zh/sae/deploy-a-php-application-by-using-a-zip-package-in-the-sae-console-2-0 "") |
| CPU Burst功能 | 优化 | 支持CPU Burst放大倍数为2倍。 | [开启CPU Burst功能](https://help.aliyun.com/zh/sae/enable-cpu-burst-function-only-applicable-to-standard-edition-and-professional-edition "") |

## **2024年10月30日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| .Net Core Runtime | 新增 | 新增` .Net Core Runtime`，支持 3.1、5.0、6.0、7.0、8.0 等多种版本，并提供代码包和镜像两种不同部署方式。 | - [.NET Core ZIP打包说明](https://help.aliyun.com/zh/sae/net-core-zip-packaging-instructions "")<br>  <br>- [使用ZIP包部署.NET Core应用](https://help.aliyun.com/zh/sae/deploy-net-core-applications-using-zip-packages "") |
| Kubernetes YAML | 新增 | 支持通过Kubernetes YAML发布及部署应用。 | [saectl工具](https://help.aliyun.com/zh/sae/saectl-tool/ "") |
| Python语言应用监控 | 新增 | 微服务应用支持Python语言应用监控，提供面向应用的实时监控，如请求数、错误数、耗时、实例GC等信息，同时支持调用链分析功能，可以满足不同场景的自定义诊断需求。 | [为Python应用安装探针](https://help.aliyun.com/zh/sae/install-the-arms-agent-for-a-python-application "") |
| ALB网关路由 | 新增 | ALB网关路由支持添加HTTP头部字段。 | [为应用设置路由规则（ALB）](https://help.aliyun.com/zh/sae/set-routing-rules-for-an-application-alb/ "") |

## 2024年09月05日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| SAE1.0 开服 | 新增 | 国际站新增开服地域。<br>支持美国（弗吉尼亚）地域。 | [开服地域](https://help.aliyun.com/zh/sae/product-overview/regions-supported-by-sae#concept-123268-zh "") |

## 2024年08月29日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 接入 Github/Gitee 组织仓库 | 新增 | web 源码部署支持接入Github/Gitee 组织仓库. | [基础开发](https://help.aliyun.com/zh/sae/foundation-development "") |
| 删除版本 | 新增 | 支持批量删除版本. | 无 |
| 应用监控 | 新增 | web 应用的应用监控功能支持关闭. | [启停应用监控](https://help.aliyun.com/zh/sae/enable-or-disable-application-monitoring "") |
| Golang语言应用监控 | 新增 | SAE支持Go语言监控. | [为Golang应用安装探针](https://help.aliyun.com/zh/sae/installing-probes-for-golang-applications "") |
| 微服务监控 | 新增 | 微服务应用支持 Go 语言应用监控，提供面向应用的实时监控，如请求数、错误数、耗时、实例GC、堆内存等信息，同时支持调用链分析功能，可以满足不同场景的自定义诊断需求。 | [为Golang应用安装探针](https://help.aliyun.com/zh/sae/installing-probes-for-golang-applications "") |
| 对接 ARMS 高级版 | 新增 | 支持 SAE 无缝对接了 ARMS 应用监控，您可以开启高级监控获得ARMS 的 APM（Application Performance Management）功能，对您的应用进行高性能管理。 | [开通ARMS高级版监控](https://help.aliyun.com/zh/sae/advanced-monitoring-new "") |
| 镜像 demo 示例 | 优化 | web应用新demo示例。 | 无 |
| 自动服务注册 | 新增 | 选择MSE Nacos作为服务注册中心时，支持自动服务注册，无需再在代码中配置 MSE Nacos注册中心的地址，实现代码无侵入。 | 无 |

## 2024年08月05日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 微服务治理 | 优化 | 解决泳道组中不同泳道path/路由必须保持一致，不能灵活设置的问题。 | 无 |
| 对接云安全中心 | 新增 | 支持微服务应用绑定云安全中心的Serverless资产，以高效保障SAE微服务应用免受安全威胁。 | [邀测：云安全中心的Serverless资产如何绑定微服务应用](https://help.aliyun.com/zh/sae/how-to-bind-a-microservice-application-to-a-serverless-asset-in-security-center "") |

## 2024年07月12日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 固定分配 CPU 类型 | 新增 | Web应用下线固定分配CPU类型。 | [【产品变更】SAE Web始终分配固定CPU功能模块下线通知](https://help.aliyun.com/zh/sae/product-overview/product-change-sae-web-always-assigns-fixed-cpu-function-module-offline-notification "") |

## **2024年05月21日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 权限助手 | 新增 | Web上线权限助手能力，提供应用/命名空间等更细粒度的读写权限控制。 | 无 |
| 标签路由 | 新增 | SAE集成了MSE云原生网关的标签路由功能，可以根据请求信息将请求转发到应用的不同灰度版本，并且支持流量按照配置的权重进行分流。其中，基于MSE云原生网关的全链路灰度功能需要依赖该标签路由功能来实现。 | [为应用设置路由规则（MSE）](https://help.aliyun.com/zh/sae/set-up-routing-rules-for-an-application-mse/ "") |
| 全链路灰度 | 新增 | SAE微服务集成了MSE全链路灰度功能，该功能可将多个应用的灰度版本隔离成一个独立的运行环境（即泳道），将满足规则的请求流量路由到对应泳道应用，实现快速搭建跨多个应用的验证环境，为开发测试降本增效。 | - [基于MSE云原生网关实现全链路灰度](https://help.aliyun.com/zh/sae/full-link-gray-scale-based-on-mse-cloud-native-gateway "")<br>  <br>- [基于Java服务网关实现全链路灰度](https://help.aliyun.com/zh/sae/implementation-of-full-link-gray-based-on-java-service-gateway "") |
| 体验优化 | 优化 | 控制台升级新版本：<br>为了确保所有SAE用户都能享受到极致流畅的体验，针对SAE旧版控制台同步进行了升级优化。升级后，用户登录SAE时，将直接进入新版控制台。新版控制台对存量历史应用没有任何影响，且可以实现对旧版控制台所有功能的操作，且在一段时间内用户依然可以切换到旧版控制台进行使用。 | 无 |
| 体验优化 | 优化 | 为了优化存量客户的使用体验（让存量单体应用的客户无需感知复杂的微服务概念和配置，让微服务的客户更加聚焦的使用完整的微服务能力）：<br>- 原旧版控制台中SpringBoot、PHP、Python等应用在新版控制台中被划分到**应用管理** \> **Web应用** \> **始终固定分配CPU**列表进行管理。<br>  <br>- 原旧版控制台中微服务应用（SpringCloud、Dubbo等）在新版控制台中被划分到**应用管理** \> **微服务应用**列表进行管理。 | 无 |
| 批量定时启停 | 新增 | Web新增支持批量应用的定时启停。 | 无 |

## **2024年03月30日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 统一概览页 | 优化 | 除微服务外，新增Web应用的计量统计。 | [概览页](https://saenext.console.aliyun.com/overview) |
| 体验优化 | 优化 | Web应用：<br>- 同一个VPC下，SAE 2.0多个应用间直接互访的体验。<br>  <br>- 请求数指标的监控延时。<br>  <br>- Webshell体验优化。 | - [通过私网访问应用](https://help.aliyun.com/zh/sae/access-applications-through-the-private-network "")<br>  <br>- [查看基础监控数据](https://help.aliyun.com/zh/sae/view-basic-monitoring-data-web "")<br>  <br>- [版本管理](https://help.aliyun.com/zh/sae/version-management "") |
| 微服务治理菜单 | 优化 | 与MSE保持一致，功能方面没有任何变化。<br>- 原 **无损上下线**、 **灰度规则**、 **限流降级** 调整到 **流量治理** 菜单下。<br>  <br>- 原 **限流降级** 菜单下 **应用概览**、 **接口详情**、 **节点详情** 调整到 **微服务治理** 菜单下。<br>  <br>- 原 **限流降级** 更名为 **流量防护**。 | [微服务治理](https://help.aliyun.com/zh/sae/microservice-governance/ "") |

## **2024年01月30日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 价格计算器 | 新增 | 提供SAE价格计算器，方便客户自助计算Web应用和微服务应用的TCO成本。 | [价格计算器](https://saenext.console.aliyun.com/cn-hangzhou/price-calculator) |
| 固定分配CPU模式 | 新增 | Web应用支持固定分配CPU模式，适用于稳定流量的业务或者一些后台任务、异步处理工作等。 | [基本概念](https://help.aliyun.com/zh/sae/product-overview/terms#bbfd0a4fabyyz "") |
| 支持Codeup代码仓库 | 新增 | 内置的源码部署能力支持Codeup代码仓库，Codeup用户直接使用SAE进行持续部署。 | [支持接入的代码平台](https://help.aliyun.com/zh/sae/foundation-development#ee2046503f95l "") |
| 构建触发模式 | 新增 | 源码构建的触发类型除Push到指定分支外，新增支持基于Tag/Release和手动触发多种方式。 | [触发器事件](https://help.aliyun.com/zh/sae/foundation-development#f854e2703fuhj "") |
| MSE微服务治理试用版 | 新增 | SAE支持MSE微服务治理试用版，方便用户免费体验MSE微服务治理的全量能力。 | [微服务治理](https://help.aliyun.com/zh/sae/microservice-governance/ "") |
| 体验优化 | 优化 | - 欠费超期文案优化。<br>  <br>- 源码部署构建详情页信息展示优化。 | [基础开发](https://help.aliyun.com/zh/sae/foundation-development "") |

## **2023年12月19日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| SAE 2.0商用 | 新增 | SAE 2.0正式商用，调整原计费项（vCPU和内存）并新增计费项（请求次数和公网出口访问）。 | - [计费概述](https://help.aliyun.com/zh/sae/product-overview/billing-new "")<br>  <br>- [【产品变更】SAE 2.0商用及SAE计费项变更通知](https://help.aliyun.com/zh/sae/product-overview/product-change-sae-2-0-commercial-and-sae-billing-item-change-notice "") |

## **2023年12月07日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 代码包部署Web应用 | 新增 | 除镜像和源码仓库外，新增支持以WAR、JAR代码包的方式部署Web应用。 | [通过代码包部署Web应用](https://help.aliyun.com/zh/sae/deploy-a-web-application-through-a-code-package "") |
| 体验优化 | 优化 | - 优化事件中心的告警信息直接透出应用名称。<br>  <br>- 修复微服务治理功能开启后需要重启应用等问题。 | - [事件订阅](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/event-subscription-2/ "")<br>  <br>- [微服务治理](https://help.aliyun.com/zh/sae/microservices-governance/ "") |

## **2023年11月14日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 开服 | 新增 | SAE 2.0支持华北2（北京）地域。 | [开服地域](https://help.aliyun.com/zh/sae/product-overview/regions-supported-by-sae "") |

## **2023年10月25日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 开服 | 新增 | SAE 2.0支持华东1（杭州）、华东2（上海）地域。 | [开服地域](https://help.aliyun.com/zh/sae/product-overview/regions-supported-by-sae "") |

## **2023年10月24日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 开服 | 新增 | SAE 2.0支持华北3（张家口）、华南1（深圳）地域。 | [开服地域](https://help.aliyun.com/zh/sae/product-overview/regions-supported-by-sae "") |
| 微服务应用无缝迁移至SAE 2.0 | 新增 | 微服务应用无缝迁移至SAE 2.0，在2.0控制台可以完成微服务应用的生命周期管理。 | [应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/ "") |
| 集成MSE限流降级 | 新增 | 微服务自动集成新版的限流降级能力，通过技术优化将微服务应用启动效率提升50%以上。 | - [设置限流降级](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/configure-throttling-and-downgrade "")<br>  <br>- [【产品变更】SAE限流降级功能从集成AHAS变更为MSE](https://help.aliyun.com/zh/sae/product-overview/product-change-sae-current-limit-degradation-function-changed-from-integrated-ahas-to-mse "") |
| 微服务小流量预热 | 新增 | 微服务治理新增服务小流量预热能力，在应用刚启动阶段通过小流量帮助应用在处理大量请求前完成初始化，避免由于应用内部资源初始化不彻底而出现请求阻塞、报错等问题。 | - [设置无损上下线](https://help.aliyun.com/zh/sae/configure-graceful-start-and-shutdown "")<br>  <br>- [【产品变更】SAE集成的MSE微服务治理功能商用通知](https://help.aliyun.com/zh/sae/product-overview/product-change-commercial-notice-of-non-destructive-up-and-down-line-and-gray-rule-function "") |

## 2023年09月30日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 命名空间管理能力 | 新增 | 新增命名空间管理能力，支持在SAE 2.0的同一个命名空间内同时创建微服务应用和Web应用。支持同命名空间、跨命名空间的应用复制。 | [管理命名空间](https://help.aliyun.com/zh/sae/manage-namespaces-2-0 "") |
| 集成ARMS应用监控基础版能力 | 新增 | 集成ARMS应用监控基础版能力，提供接口RT、QPS、错误数、JVM、线程池等各种监控指标和调用链查看，方便定位线上问题。 | [设置应用监控](https://help.aliyun.com/zh/sae/set-up-application-monitoring "") |
| 自定义域名对接WAF | 新增 | 支持自定义域名对接按量付费经济版的Web 应用防火墙 WAF（Web Application Firewall），在SAE 2.0上一站式使用Web 应用防火墙的安全防护能力。 | [通过自定义域名访问应用](https://help.aliyun.com/zh/sae/access-apps-through-a-custom-domain-name "") |
| 集成MSE云原生网关 | 新增 | 微服务集成MSE云原生网关，方便微服务用户一站式使用SAE和MSE网关能力。 | - [MSE云原生网关使用约束](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/limits-of-mse-cloud-native-gateway "")<br>  <br>- [为应用配置路由规则（MSE）](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/configure-routing-rule-for-an-application-by-using-a-cloud-native-gateway "") |
| 体验优化 | 优化 | - 新增构建镜像推送到平台ACR仓库，支持在构建记录列表中查询新建应用版本的映射关系。<br>  <br>- 优化创建Web应用、新建版本时实例启动失败的错误信息透出体验，优化停止应用体验，提供内网默认域名的访问体验。<br>  <br>- 优化Web应用RAM用户无其他产品权限时的报错信息。 | - [通过源码部署Web应用](https://help.aliyun.com/zh/sae/deploy-web-applications-from-source-code/ "")<br>  <br>- [应用访问](https://help.aliyun.com/zh/sae/sae-2-application-access/ "") |

## **2023年08月07日**

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 2.0公测版上线 | 新增 | 应用管理：秒级完成创建发布应用，通过默认域名、自定义域名访问应用。一键灰度应用，通过调整流量比例来切流。 | - [应用部署](https://help.aliyun.com/zh/sae/sae-2-web-only-application-deployment/ "")<br>  <br>- [通过自定义域名访问应用](https://help.aliyun.com/zh/sae/access-apps-through-a-custom-domain-name "")<br>  <br>- [版本管理](https://help.aliyun.com/zh/sae/version-management "")<br>  <br>- [流量配置](https://help.aliyun.com/zh/sae/traffic-configuration "") |
| 新增 | 极致弹性：百毫秒级弹性伸缩，根据流量自适应调整资源使用，无请求时CPU不计费。 | [自动弹性](https://help.aliyun.com/zh/sae/automatic-elasticity-wen "") |
| 新增 | 平台工程：提供S2A（Source to Application）等平台工程能力，研发提效。 | [2.0公测版](https://help.aliyun.com/zh/sae/sae-2-0/) |
| 新增 | 运维管理：提供日志管理、Webshell操作、应用/版本/实例级别的监控能力，方便用户管理运维应用。 | - [日志管理（SLS）](https://help.aliyun.com/zh/sae/log-management-sls "")<br>  <br>- [版本管理](https://help.aliyun.com/zh/sae/version-management "")<br>  <br>- [查看基础监控数据](https://help.aliyun.com/zh/sae/view-basic-monitoring-data-web "") |

## 2023年03月30日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 支持SSL控制台同步证书到SAE | 新增 | 支持SSL控制台同步证书到SAE，大概率避免因SSL证书过期导致SAE侧没同步更新而出现覆盖的问题。 | - [基于CLB配置应用服务访问](https://help.aliyun.com/zh/sae/configure-application-access-based-on-clb-instances/#concept-2383398 "")<br>  <br>- [基于ALB/CLB/MSE配置网关路由（Ingress）访问](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/configuring-gateway-routing-for-application-access-based-on-alb-and-clb-instances/#concept-2457109 "") |
| 弹性能力增强 | 优化 | 优化手动扩缩时定时策略执行时机，解决定时弹性开启阶段临时执行手动扩容失效的问题。 | - [手动扩缩](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/manually-scale-instances#task-2106628 "")<br>  <br>- [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/configure-an-auto-scaling-policy#task-1942230 "") |
| 健康检查能力增强与提示 | 优化 | 健康检查新增成功/失败阈值设置，优化健康检查失败时常见诊断方法提示。 | [健康检查最佳实践](https://help.aliyun.com/zh/sae/best-practices-for-health-checks#task-2308598 "") |
| 微服务配置提示 | 优化 | 增加无法注册/获取配置的排错提示、注册中心客户端版本推荐的提示，避免客户侧的环境变量被系统覆盖。 | [SAE微服务相关概念和能力](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/concepts-and-capabilities-related-to-sae-microservices#concept-2233976 "") |
| SLB计费提示 | 优化 | 新建SLB时优化付费方式为按规格付费的提示，复用SLB时增加部分SLB不能复用的提示。 | [计费概述](https://help.aliyun.com/zh/sae/product-overview/billing-new#concept-96732-zh "") |
| 重启应用后恢复弹性规则 | 优化 | 支持重启应用后自动/手动恢复弹性规则。 | [管理应用生命周期](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/manage-the-lifecycle-of-an-application#concept-113076-zh "") |
| 应用列表透出实例规格 | 优化 | 应用列表增加实例规格的透出，方便您进行整体的成本优化决策。 | - [管理应用生命周期](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/manage-the-lifecycle-of-an-application#concept-113076-zh "")<br>  <br>- [SAE实例规格](https://help.aliyun.com/zh/sae/product-overview/sae-instance-types#concept-2281239 "") |
| 应用发布策略 | 优化 | 优化应用发布策略不透明的展示。 | [升级和回滚应用](https://help.aliyun.com/zh/sae/upgrade-and-roll-back-applications/#topic-1898724 "") |
| ALB网关路由配置 | 优化 | 转发规则配置中域名非必填，和Nginx 、ALB的使用体验保持一致。 | [ALB使用约束](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/limits-of-alb#concept-2313830 "") |
| 事件中心 | 优化 | 新增拉取镜像失败事件、CLB配置冲突检查事件和网关路由配置冲突检查事件。 | [事件订阅](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/event-subscription#task-2227761 "") |
| 默认系统标签 | 优化 | 每个新增/重新部署后的应用，将自动带上命名空间系统标签（控制台不可见，仅账单可见），在阿里云账单系统启用后可用于分账。 | [企业分账](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/split-bills#task-2426200 "") |

## 2023年01月09日

| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| 开服 | 新增 | 西南1（成都）地域开服。 | [开服地域](https://help.aliyun.com/zh/sae/product-overview/regions-supported-by-sae#concept-123268-zh "") |
| 应用监控和告警能力 | 新增 | 基于eBPF技术，SAE提供无侵入的应用监控和告警能力，支持任意语言和任意框架。 | - [应用概览](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/application-overview "")<br>  <br>- [告警管理概述](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/alert-management-overview "") |
| 云效部署SAE Job | 新增 | 支持通过云效部署SAE Job，打通CD流程。 | - [部署Java任务模板至SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-java-job-template-to-sae#task-2284438 "")<br>  <br>- [部署PHP任务模板至SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-php-job-template-to-sae#task-2284812 "")<br>  <br>- [部署PHP ZIP任务模板至SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-php-job-template-to-sae-by-using-a-zip-package#task-2284823 "")<br>  <br>- [部署Golang任务模板至SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-go-job-template-to-sae#task-2284824 "")<br>  <br>- [部署Node.js任务模板至SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-nodejs-job-template-to-sae#task-2284825 "")<br>  <br>- [部署Python任务模板至SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-python-job-template-to-sae#task-2284822 "") |
| CLB支持UDP协议 | 新增 | CLB新增支持UDP协议。 | [为应用绑定CLB](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/bind-clb-for-application#task-122997-zh "") |
| 应用监控和服务治理功能（邀测） | 新增 | 针对高版本JDK17，SAE通过白名单方式支持应用监控和服务治理功能，提供服务、接口、调用链等级别的监控能力。 | [应用监控](https://help.aliyun.com/zh/sae/application-monitoring/#concept-2279956 "") |
| 体验优化 | 优化 | 优化弹性功能的使用体验，包括弹性指标含义、聚合算法解释、弹性指标可见性、手动扩容后可选自动恢复弹性功能等。 | - [手动扩缩](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/manually-scale-instances#task-2106628 "")<br>  <br>- [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/configure-an-auto-scaling-policy#task-1942230 "") |

## 功能发布历史记录

SAE 2022年及之前的功能发布记录，请参见 [功能发布记录（2018~2022年）](https://help.aliyun.com/zh/sae/product-overview/release-notes-from-2018-to-2022#concept-2294168 "")。