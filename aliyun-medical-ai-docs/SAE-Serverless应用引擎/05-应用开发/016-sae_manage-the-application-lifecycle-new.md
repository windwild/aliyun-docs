### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/)管理应用生命周期

# 管理应用生命周期

更新时间：2025-02-07 02:54:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：管理和使用保密字典（K8s Secret）](https://help.aliyun.com/zh/sae/managing-and-using-a-confidential-dictionary-k8s-secret)[下一篇：单批发布应用](https://help.aliyun.com/zh/sae/single-batch-release-for-an-application)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

操作入口

查看应用基础信息

计量数据

应用信息

实例列表

弹性伸缩

查看应用配置

查看应用状态

更新应用

回退历史版本

手动扩缩应用

自动扩缩应用

启停应用

重启应用

删除应用

启停应用监控

在应用托管至SAE后，您可以对应用执行更新、扩缩容、启停、删除和监控启停等应用生命周期管理操作。

## 操作入口

登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

## 查看应用基础信息

在 **基础信息** 页面，您可查看与管理应用程序相关的所有关键信息。详细信息如下：

### 计量数据

在 **计量数据** 区域，您可查看 **本月CU使用量**、 **本月CPU资源使用量**、 **本月Memory资源使用量**、 **实时CPU资源使用量** 和 **实时Memory资源使用量**，您可进一步分析这些数据以更好地管理和优化您的资源分配。

### 应用信息

- 在 **应用信息** 区域，您可以查看应用名、命名空间和应用ID等基本信息。此外，您还可以进行 **实例规格** 的变更、切换 **安全组**、切换vSwitch、管理 **应用标签** 和 **应用描述**。具体操作，请参见 [应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/ "") 目录下的文档。

- 在 **应用访问设置** 区域，为了控制和管理外部如何访问部署在SAE上的应用程序，提供了两种访问方式：

  - **基于CLB访问**：通过绑定公网CLB获得在公网中访问SAE应用的能力，也可以通过绑定私网CLB实现同VPC内所有应用间的互相访问。具体信息，请参见 [为应用绑定CLB](https://help.aliyun.com/zh/sae/sae-2-bind-clb-for-application "")。

  - **基于K8s Service Name访问**：您可查看 **服务名称**、 **端口** 和 **协议**。
- 在 **网关路由设置** 区域，您可以进行 **添加转发策略**。具体操作，请参见 [配置网关路由（Ingress）访问](https://help.aliyun.com/zh/sae/configuring-gateway-routing-ingress-access/ "") 目录下的文档。


### 实例列表

在 **实例列表** 页签，展示了在该服务下所创建的所有应用实例。每个实例都代表了一个独立运行的应用环境。您可以查看各个应用的实例ID、vSwitch和IP地址等信息。此外，您还可以对实例进行管理操作，如查看实时日志、查看事件和删除等，帮助您高效地管理和维护其无服务器应用。具体操作，请参见 [应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/ "") 目录下的文档。

### 弹性伸缩

在 **弹性伸缩** 页签，您可以查看 **实例数随弹性指标变化** 的趋势图，以便了解资源使用情况。详细信息，请参见 [弹性可观测](https://help.aliyun.com/zh/sae/elastic-observability "")。此外，您还可以进行添加弹性策略或开启闲置模式，以进一步优化成本和性能。具体操作，请参见 [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new "") 和 [闲置模式](https://help.aliyun.com/zh/sae/idle-mode-new "")。

### 查看应用配置

在 **基础信息** 页面，单击 **查看应用配置**，在 **查看当前配置信息** 对话框，查看应用的详细配置信息。

## 查看应用状态

在 **基础信息** 页面，您可以查看应用的启停状态，并进行相应的修改。具体操作，请参见 [启停应用](https://help.aliyun.com/zh/sae/manage-the-application-lifecycle-new#section-2cm-p15-u7c "")。

## 更新应用

操作入口在不同场景下有差异：

对正在运行的应用进行变更

对已停止的应用进行变更

**警告**

重新部署应用后，该应用将会被重启。为避免业务中断等不可预知的错误，请在业务低峰期执行部署操作。

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在目标应用的 **基础信息** 页面，单击 **部署应用**。


1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在目标应用的 **基础信息** 页面，单击 **修改应用配置**。


当应用实例数大于1时，您可以选择以下发布策略来发布更新后的应用：

- [灰度发布应用](https://help.aliyun.com/zh/sae/perform-a-canary-release-for-an-application "")

- [分批发布应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/perform-a-phased-release-for-an-application#concept-110456-zh "")

- [单批发布应用](https://help.aliyun.com/zh/sae/single-batch-release-for-an-application "")


## 回退历史版本

在 **基础信息** 页面，单击 **回退历史版本**，在 **回退历史版本** 页面，选择版本并设置发布策略。具体操作，请参见 [回退历史版本](https://help.aliyun.com/zh/sae/roll-back-an-application-to-an-earlier-version "")。

## 手动扩缩应用

在 **基础信息** 页面，单击 **手动扩缩**。具体操作，请参见 [手动扩缩](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/manual-scaling "")。

**说明**

- 扩容时，如果扩容的实例数与原应用的实例数总和，大于应用的资源使用限制，则扩容失败。如果需要继续增加应用实例，请加入钉群（钉群号：32874633）申请额度。

- 如果您的扩容缩为非紧急需求，建议使用 [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new "")。


## 自动扩缩应用

在 **基础信息** 页面的 **弹性伸缩** 页签，在弹性伸缩区域单击 **添加弹性策略**。具体操作，请参见 [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new "")。

## 启停应用

单应用的启停步骤如下所示。关于多应用的启停步骤，请参见 [一键启停应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/use-the-one-click-start-and-stop-feature-to-manage-applications#task-1893212 "")。

- **停止应用**：在 **基础信息** 页面，单击 **停止应用**，在弹出的 **提示** 对话框，单击 **确认**，停止应用运行。



当应用处于运行状态时，可以根据业务需求随时停止应用。停止应用时，该应用的最小存活实例数设置为0，实例数设置为0，其所使用的计算资源将停止计费或者计量。





**警告**





应用停止后，如果您的应用运行时还依赖其他产品或者服务，例如绑定SLB和使用VPC，该部分产品或者服务仍处于计费状态。

- **启动应用**：在 **基础信息** 页面，单击 **启动应用**，在弹出的 **启动应用** 对话框，单击 **确认**，启动处于停止状态的应用。

当应用处于停止状态时，您可以根据需求启动该应用。应用启动后，启动的实例数恢复为停止前所配置值，同时重新开始计量或计费。


## 重启应用

对于正在运行的应用实例，在 **基础信息** 页面，选择**更多** \> **重启应用**，在弹出的 **重启应用** 对话框，根据页面提示操作。

- 已启用弹性策略：设置 **重启应用后恢复自动弹性方式**，并单击 **确认**。

- 未启用弹性策略：设置 **最小存活实例数**，并单击 **确认**。


**说明**

在应用程序正常、业务异常运行时，请勿手动重启整个应用，您需要先使用健康检查功能对应用实例状态进行诊断。如果检查结果表明实例状态不健康，会自动重启实例。 具体操作，请参见 [设置健康检查](https://help.aliyun.com/zh/sae/set-health-check-2-0 "")。

## 删除应用

在 **基础信息** 页面，选择**更多** \> **删除应用**，在弹出的 **删除应用** 对话框，单击 **确认**，删除已经部署的应用。

**警告**

如果您的应用运行时还依赖其他产品或者服务，例如绑定CLB和配置VPC，那么删除前请确认所依赖的产品或者服务是否需要继续使用，若不需要则停止该服务，停止计费。

## 启停应用监控

在 **基本信息** 页面右上角，启停应用监控。具体操作，请参见 [启停应用监控](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/enable-or-disable-application-monitoring-for-an-application#task-2106259 "")。

- **开启应用监控**：单击**更多** \> **开启应用监控**，在弹出的 **开启应用监控** 对话框，单击 **确认**，开启应用监控。

- **停止应用监控**：单击**更多** \> **停止应用监控**，在弹出的 **关闭应用监控** 对话框，单击 **确认**，关闭应用监控。