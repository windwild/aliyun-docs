### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [操作指南](https://help.aliyun.com/zh/sae/user-guide/) [应用托管](https://help.aliyun.com/zh/sae/application-hosting-2-0/) 应用托管概述

# 应用托管概述

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：应用托管](https://help.aliyun.com/zh/sae/application-hosting-2-0/)[下一篇：插件部署](https://help.aliyun.com/zh/sae/use-plug-ins-to-deploy-applications-new/)

该文章对您有帮助吗？

反馈

Serverless 应用引擎 SAE（Serverless App Engine）向上抽象了应用的概念，支持以代码包和镜像方式部署应用并进行托管。在SAE上，您可以低门槛拥抱容器技术，无需管理和维护集群与服务器，专注于设计和构建应用程序，最大化利用资源完成应用的生命周期管理，以及监控、运维等服务。本文介绍SAE支持的应用类型、部署方式和托管功能。

## 应用部署方式

当应用部署到SAE后，SAE的应用托管能力可以使其更可用、运维更轻量。具体教程，请参考如下视频。

SAE支持部署的主流应用及部署方式，请参考下表。

|     |     |     |
| --- | --- | --- |
| **应用举例** | **部署方式** | **参考文档** |
| 原生Spring Cloud | WAR、JAR、镜像 | [将应用的服务注册与发现中心更改为Nacos](https://help.aliyun.com/zh/sae/host-spring-cloud-applications-to-sae#concept-123013-zh "") |
| 原生Dubbo | WAR、JAR、镜像 | [将Dubbo应用托管到SAE](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/getting-started/host-dubbo-applications-to-sae#task-1426493 "") |
| HSF | WAR、JAR、镜像 | [将HSF应用托管到SAE](https://help.aliyun.com/zh/sae/host-an-hsf-application-to-sae#task-2144422 "") |
| 多语言应用 | 镜像 | [在SAE控制台使用镜像部署多语言应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-applications-in-other-languages-by-using-images-in-the-sae-console#concept-97675-zh "") |
| PHP应用 | 镜像、ZIP | - [在SAE控制台使用镜像部署PHP应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-php-application-by-using-an-image-in-the-sae-console#concept-97675-zh "")<br>  <br>- [在SAE控制台使用ZIP包部署PHP应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-php-application-by-using-a-zip-package-in-the-sae-console#task-2426208 "") |
| Python应用 | 镜像、ZIP | - [在SAE控制台使用镜像部署Python应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/use-an-image-to-deploy-a-python-application-in-the-sae-console#task-2271489 "")<br>  <br>- [在SAE控制台使用ZIP包部署Python应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/deploy-a-python-application-by-using-a-zip-package-in-the-sae-console#task-2271316 "") |

- 从服务框架角度而言，使用Spring Cloud、Dubbo和HSF框架开发的应用都可以部署在SAE中，但因部署方式不同，其应用的运行环境也不同。

  - Spring Cloud和Dubbo应用通过WAR包部署时，选择 **apache-tomcat** 相关版本的运行环境。

  - Spring Cloud和Dubbo应用通过JAR包部署时，选择 **标准Java应用运行环境**。

  - HSF应用通过WAR或JAR包部署时，选择 **EDAS-Container** 相关版本的运行环境。
- 从技术栈语言角度而言，SAE支持托管Java应用、PHP应用、Python应用以及多语言（例如Node.js和Go）应用。

- 从工具角度而言，除控制台部署和API部署外，SAE与很多CI/CD工具、插件集成，CI/CD工具包括Jenkins、Terraform和云效，插件包括Maven、IntelliJ IDEA和Eclipse，可以实现代码提交后自动部署。


**重要**

如果您是第一次将应用部署到SAE，需要在[SAE控制台](https://saenext.console.aliyun.com/)创建应用，以便将业务代码推送到该应用中。

## 应用部署高级设置

应用的高级设置功能包括 [设置启动命令](https://help.aliyun.com/zh/sae/set-startup-command-2-0 "")、 [设置环境变量](https://help.aliyun.com/zh/sae/configure-environment-variables-2-0 "")、 [设置Hosts绑定](https://help.aliyun.com/zh/sae/configure-host-bindings-1 "")、 [设置健康检查](https://help.aliyun.com/zh/sae/set-health-check-2-0 "")、 [日志收集服务](https://help.aliyun.com/zh/sae/log-collection-service-2-0/ "") 和 [持久化存储](https://help.aliyun.com/zh/sae/persistent-storage/ "") 等，您可以在创建应用时设置，也可以在创建应用后（后续部署应用时）依据业务需求设置。如果您选择在应用创建后设置，应用将会重启生效该配置。为避免业务中断等不可预知的错误，请在业务低峰期进行高级设置。

## 应用托管功能

将应用托管到SAE后，您可以对应用进行一键式白屏化的全生命周期管理，简化运维。

|     |     |
| --- | --- |
| **使用场景** | **功能** |
| 资源管理 | 通过命名空间从逻辑上隔离应用，并使用配置项存储应用所需的配置信息。更多信息，请参见 [管理命名空间](https://help.aliyun.com/zh/sae/manage-namespaces-2-0 "")。 |
| 应用部署 | - 创建和部署：完成应用开发后，您可以通过SAE创建并部署应用，并按需为应用设置高级配置。更多信息，请参见 [应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/ "")。<br>  <br>- 插件部署：SAE支持通过Maven、IntelliJ IDEA和Eclipse插件进行部署。更多信息，请参见 [插件部署](https://help.aliyun.com/zh/sae/use-plug-ins-to-deploy-applications-new/ "")。<br>  <br>- CI/CD：应用在迭代升级过程中，需要持续集成（CI）与持续部署（CD）。SAE支持通过云效、Jenkins和Terraform等方式实现CI/CD部署。更多信息，请参见 [CI/CD](https://help.aliyun.com/zh/sae/cicd-deployment-new/ "") 和 [Terraform概述](https://help.aliyun.com/zh/sae/terraform-overview "")。<br>  <br>- 升级和回滚：应用完成创建后，还需不断迭代升级；若升级的版本出现问题，则需要回退版本。更多信息，请参见 [升级和回滚应用](https://help.aliyun.com/zh/sae/sae-2-microservices-upgrading-and-rolling-back-applications/ "")。 |
| 应用设置 | 应用部署到SAE后，您可以按需 [变更实例规格](https://help.aliyun.com/zh/sae/change-the-instance-specifications-of-an-application-2-0 "")、 [切换安全组和vSwitch](https://help.aliyun.com/zh/sae/change-the-security-group-and-vswitch-of-an-application-2-0 "") 等。 |
| 应用访问 | 应用部署到SAE后，其业务通常需要获取公网资源或者跨VPC访问，您可以通过绑定CLB、配置NAT网关+EIP或应用实例绑定EIP等方式实现。更多信息，请参见 [应用访问和流量管理](https://help.aliyun.com/zh/sae/sae-network-related-concepts-and-capabilities/ "")。 |
| 应用运维 | SAE支持通过Webshell完成基本的运维需求，例如通过日志上传下载诊断应用。在实例无法启动时，SAE支持通过一键调试功能定位问题。更多信息，请参见 [应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/ "")。 |
| 一键启停 | SAE支持在同一命名空间内，一键启停开发、测试和预发等环境的应用。更多信息，请参见 [对应用进行批量操作](https://help.aliyun.com/zh/sae/batch-operations-on-applications "")。 |
| 弹性伸缩 | 应用扩缩是通过改变应用的实例数来增加或减少应用的计算容量。您可以在应用的实例负载过高时，以手动方式添加新应用实例，在应用闲置时减少应用实例，高效利用应用资源并降低成本。<br>- 自动弹性：当应用扩缩容为非紧急需求时，例如周期性的流量高峰，您可以选择自动扩缩方式。更多信息，请参见 [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new "")。<br>  <br>- 手动弹性：当应用扩缩容为紧急需求时，例如突发性的流量高峰，您可以选择手动扩缩方式。更多信息，请参见 [手动扩缩](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/manual-scaling "")。 |
| 日志管理 | 在应用的运维过程中，您可以通过日志定位并诊断问题。更多信息，请参见 [日志管理](https://help.aliyun.com/zh/sae/log-management-new/ "")。 |
| 监控与报警 | SAE集成了应用实时监控服务ARMS，为部署在SAE中的应用提供关键指标的监控能力和报警能力。更多信息，请参见 [应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/ "") 和 [告警管理](https://help.aliyun.com/zh/sae/alert-management-overview2-0/ "")。 |
| 分布式配置管理 | SAE支持对应用配置进行集中管理，您可以将应用开发过程中产生的大量的参数和变量等信息，提取到配置文件中并上传至SAE。更多信息，请参见 [配置管理](https://help.aliyun.com/zh/sae/config-management/ "")。 |
| 事件订阅 | 事件中心可以记录实例的状态变更，统一管理SAE生成的事件数据，提供存储、查询和告警等功能。更多信息，请参见 [事件中心](https://help.aliyun.com/zh/sae/event-center-new "")。 |