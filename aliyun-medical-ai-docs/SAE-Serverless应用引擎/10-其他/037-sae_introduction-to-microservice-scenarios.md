### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [操作指南](https://help.aliyun.com/zh/sae/user-guide/) [应用开发](https://help.aliyun.com/zh/sae/sae-2-application-development/) 微服务场景指引

# 微服务场景指引

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：应用开发](https://help.aliyun.com/zh/sae/sae-2-application-development/)[下一篇：使用Spring Cloud开发应用](https://help.aliyun.com/zh/sae/spring-cloud-development/)

该文章对您有帮助吗？

反馈

Serverless 应用引擎 SAE（Serverless App Engine）支持原生Spring Cloud和Dubbo微服务框架的应用，您可以将基于原生Spring Cloud和Dubbo微服务框架开发的应用迁移、部署到SAE，进行微服务管理。

## 为什么使用SAE服务注册中心

- Spring Cloud

SAE注册中心具备Spring Cloud Alibaba Nacos Discovery注册中心的所有功能。

Spring Cloud Alibaba Nacos Discovery实现了Spring Cloud Registry标准接口，遵循Spring Cloud Registry标准规范。在实现服务注册与发现方面，与Eureka、Consul和ZooKeeper等组件相同。

SAE服务注册中心可以完全代替Eureka、Consul、ZooKeeper和Redis，作为您的微服务应用的服务注册中心。与其相比，SAE还具有以下优势：

  - SAE服务注册中心为共享组件，为您节省了运维、部署ZooKeeper等组件的物理设备成本。

  - SAE服务注册中心在通信过程中增加了鉴权加密功能，为您的服务注册链路进行了安全加固。

  - SAE服务注册中心与SAE其他组件紧密结合，为您提供了整套的微服务解决方案。
- Dubbo

SAE服务注册中心实现了Dubbo所提供的SPI标准的注册中心扩展，完整地支持Dubbo服务注册、路由规则和配置规则等功能。







**说明**

  - 关于Dubbo所提供的SPI标准的注册中心扩展内容，请参见 [注册中心扩展](https://dubbo.apache.org/zh/docs/references/spis/)。

  - 关于Dubbo服务注册，请参见 [注册](https://dubbo.apache.org/zh/docs/references/registry/) 和 [多注册中心](https://dubbo.apache.org/zh/docs/advanced/multi-registry/)。

  - 关于Dubbo路由规则，请参见 [路由规则](https://dubbo.apache.org/zh/docs/examples/routing/)。

  - 关于Dubbo配置规则，请参见 [配置规则](https://dubbo.apache.org/zh/docs/advanced/config-rule/)。


您将应用部署到SAE时，SAE服务注册中心以高优先级自动设置Nacos Server服务端地址和服务端口，以及namespace、access-key、secret-key和context-path等信息，此外无需进行任何额外的配置。

## 原生Spring Cloud应用

- 如果您初次接触原生Spring Cloud应用，希望在SAE上部署原生Spring Cloud应用，您需要在本地完成添加依赖和配置管理等操作，然后将应用部署到SAE。具体操作，请参见 [使用Spring Cloud开发微服务应用并部署至SAE](https://help.aliyun.com/zh/sae/use-spring-cloud-to-develop-microservice-applications-and-deploy-them-on-sae#concept-123010-zh "")。

- 如果您在本地开发了依赖Eureka、Consul、ZooKeeper和Redis等组件实现的服务注册与发现的Spring Cloud应用，希望将该应用部署至SAE，那么只需要将服务注册与发现的组件的依赖和配置替换成Spring Cloud Alibaba Nacos Discovery，无需修改任何业务代码，即可将应用部署到SAE进行微服务托管。具体操作，请参见 [将Spring Cloud应用托管到SAE](https://help.aliyun.com/zh/sae/host-spring-cloud-applications-to-sae#concept-123013-zh "")。


## 原生Dubbo应用

- 如果您初次接触原生Dubbo应用，希望在SAE上部署原生Dubbo应用，您需要在本地完成添加依赖和配置管理等操作，然后将应用部署到SAE。具体操作，请参见 [将Dubbo应用托管到SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/getting-started/host-dubbo-applications-to-sae#task-1426493 "")。

- 如果您在本地开发了依赖Eureka、Consul、ZooKeeper和Redis等组件实现的服务注册与发现的Dubbo应用，希望将该应用部署至SAE，那么只需要将服务注册与发现的组件的依赖和配置替换成edas-dubbo-extension，无需修改任何业务代码，即可将应用部署到SAE进行微服务托管。具体操作，请参见 [将Dubbo应用托管到SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/getting-started/host-dubbo-applications-to-sae#task-1426493 "")。