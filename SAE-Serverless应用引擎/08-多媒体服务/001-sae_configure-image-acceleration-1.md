### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 设置镜像加速

# 设置镜像加速

更新时间：2024-07-28 23:04:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

背景信息

操作步骤

为应用设置镜像加速

为任务模板设置镜像加速

确认镜像加速是否生效

使用镜像部署应用或任务模板时，您可能会遇到镜像拉取与启动耗时过长、实例启动失败、拉取镜像失败等情况。使用容器镜像服务ACR企业版（ACR EE）时，SAE支持一键开启镜像加速，通过按需加载、缓存加速、构建加速等方式缩短镜像启动时间，提升应用与任务实例的启动速度。

## 前提条件

- [已创建企业版实例](https://help.aliyun.com/zh/acr/user-guide/create-a-container-registry-enterprise-edition-instance#task488 "")。

- [已开启转换镜像加速](https://help.aliyun.com/zh/acr/user-guide/load-resources-of-a-container-image-on-demand#section-87k-i16-i5g "")。

- [已申请开通白名单](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/support/contact-us#concept-2361378 "")。


## 背景信息

阿里云容器镜像服务ACR分为个人版和企业版。其中ACR企业版（ACR EE）提供容器镜像、Helm Chart、Operator等符合OCI规范制品的安全托管及高效分发服务，支持企业生产环境大规模分发、全球多地域分发、云原生DevSecOps分发提效。

更多信息，请参见 [什么是容器镜像服务ACR](https://help.aliyun.com/zh/acr/product-overview/what-is-container-registry#concept-2058233 "") 和 [个人版实例与企业版实例差异化说明](https://help.aliyun.com/zh/acr/product-overview/differences-between-personal-edition-instances-and-enterprise-edition-instances#task-2273273 "")。

## 操作步骤

### 为应用设置镜像加速

该功能可以在创建应用时设置，也可以在更新应用时设置。本文以创建时的操作步骤为例，更新应用时的操作路径，请参见 [更新应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/manage-the-lifecycle-of-an-application#section-3qn-6i4-g2p "")。

1. 登录 [SAE控制台](https://sae.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **应用列表**，在顶部菜单栏选择地域，然后单击 **创建应用**。

3. 在 **应用基本信息** 配置向导，设置应用相关信息，并单击 **下一步：应用部署配置**。

4. 在 **应用部署配置** 配置向导页面，设置应用相关信息。



本文仅介绍关键步骤。



1. **应用部署方式** 选择 **镜像**。

2. 在 **配置镜像** 区域，按需选择镜像类型，设置镜像的具体信息。



      - **我的阿里云镜像**：单击 **镜像服务企业版**，从下拉列表选择目标实例。

      - **公有镜像**：在文本框输入镜像仓库地址，例如`sae-test-registry-vpc.cn-shanghai.cr.aliyuncs.com/sae/acree`，确保应用能够访问公网。

      - **其它阿里云账号私有镜像**： **镜像服务版本** 选择 **镜像服务企业版**，并设置企业版实例的各项信息。


3. 展开 **镜像加速** 区域，打开 **启用镜像加速功能** 开关。
5. 单击 **下一步：确认规格**。

6. 在 **确认规格** 配置向导，查看您所创建应用的详细信息以及配置费用情况，并单击 **确认创建**。



页面会跳转至 **创建完成** 配置向导，您可以单击 **应用详情页** 进入 **基本信息** 页面。


### 为任务模板设置镜像加速

该功能可以在创建任务模板时设置，也可以在更新任务模板时设置。本文以创建时的操作步骤为例，更新任务模板时的操作路径，请参见 [任务模板管理](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/job-template-management#section-lxp-i1z-w0r "")。

1. 登录 [SAE控制台](https://sae.console.aliyun.com/)。

2. 在左侧导航栏，单击 **任务模板列表**，在顶部菜单栏选择地域。
3. 在 **任务模板列表** 页面，单击 **创建任务模板**。
4. 在 **任务基本信息** 配置向导页面，设置相关信息，然后单击 **下一步：部署配置**。
5. 在 **部署配置** 配置向导页面，设置相关信息。



本文仅介绍关键步骤。



1. **任务部署方式** 选择 **镜像**。

2. 在 **配置镜像** 区域，按需选择镜像类型，设置镜像的具体信息。



      - **我的阿里云镜像**：单击 **镜像服务企业版**，从下拉列表选择目标实例。

      - **公有镜像**：在文本框输入镜像仓库地址，例如`sae-test-registry-vpc.cn-shanghai.cr.aliyuncs.com/sae/acree`，确保应用能够访问公网。

      - **其它阿里云账号私有镜像**： **镜像服务版本** 选择 **镜像服务企业版**，并设置企业版实例的各项信息。


3. 展开 **镜像加速** 区域，打开 **启用镜像加速功能** 开关。

4. 单击 **下一步：任务设置**。
6. 在 **任务设置** 配置向导页面，设置相关信息，然后单击 **下一步：确认规格**。
7. 在 **确认规格** 配置向导页面，仔细确认配置信息，然后单击 **确认创建**。
创建完成后，在 **任务模板列表** 页面，查看已创建的任务信息。


### 确认镜像加速是否生效

1. 登录[容器镜像服务控制台](https://cr.console.aliyun.com/)，访问目标企业版实例的 **镜像仓库** 页面，在 **镜像版本** 页面，确认当前部署SAE的镜像版本TAG，是否有对应的镜像版本`${tag}_accelerated`。



具体操作，请参见 [镜像仓库](https://help.aliyun.com/zh/acr/getting-started/build-images-on-container-registry-enterprise-edition-instances#section-7ek-3k0-l1n "")。![sc_view_image_version_on_container_registry_console](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2469930761/p531596.png)

2. 登录 [SAE控制台](https://sae.console.aliyun.com/)，访问目标应用的 **应用事件** 或任务模板的 **事件信息** 页面，确认镜像拉取是否生效。



下图以查看应用事件为例。具体操作，请参见 [查看应用事件](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/view-application-events#task-2325381 "") 和 [查看任务事件](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/job-template-management#section-c7m-zg2-3qz "")。![sc_view_application_event_to_check_accelerated_image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2469930761/p531584.png)