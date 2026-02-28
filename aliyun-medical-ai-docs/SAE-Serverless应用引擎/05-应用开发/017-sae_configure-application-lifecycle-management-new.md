### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/)设置应用生命周期管理

# 设置应用生命周期管理

更新时间：2025-06-27 10:34:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置健康检查](https://help.aliyun.com/zh/sae/set-health-check-2-0)[下一篇：日志收集服务](https://help.aliyun.com/zh/sae/log-collection-service-2-0/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

功能入口

操作步骤

如果您精通K8s，且需要在应用容器启动前或者关闭前执行相关操作，例如运行前部署资源或者停止前优雅下线应用，可以设置应用生命周期管理。本文主要介绍如何在SAE应用中配置PostStart、PreStop和TerminationGracePeriodSeconds。

## 功能介绍

- Pod hook（容器钩子）是由Kubernetes管理的kubelet组件发起的机制，用于在容器的生命周期的关键阶段执行自定义任务。这些阶段包括容器进程启动前（preStart）和终止前（preStop）。钩子的引入使Kubernetes能够更加灵活和精细地管理容器的生命周期。更多信息，请参见 [Container Lifecycle Hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/)。

  - **启动后处理（PostStart设置）**：是容器生命周期中的一种钩子，该钩子在容器被创建后立刻触发，通知容器它已经被创建。该钩子不需要向其所对应的hook handler传入任何参数。如果该钩子对应的hook handler执行失败，则该容器会被关闭，并根据该容器的重启策略决定是否重启该容器。

  - **停止前处理（PreStop设置）**：是容器生命周期中的一种钩子，该钩子在容器终止前触发，通常用于执行清理操作或优雅地关闭服务。其对应的hook handler必须在Kubernetes向容器发送终止信号（如 SIGTERM）之前完成。无论hook handler的执行结果如何，一旦其完成，Kubernetes将向容器发送SIGTERM信号以终止容器，并根据配置等待一段时间后强制删除容器。
- **优雅下线超时设置（TerminationGracePeriodSeconds）**：其主要作用是为容器的优雅终止提供时间保障，确保应用能够在被强制停止之前完成必要的清理和关闭操作。这不仅有助于提升系统的稳定性和可靠性，还能避免因强制终止导致的数据丢失、请求失败和服务不可用等问题。结合 PreStop钩子可以实现完整的优雅下线流程。


## **功能入口**

操作入口在不同场景下有差异：

创建应用

对正在运行的应用进行变更

对已停止的应用进行变更

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击 **创建应用**。

2. 在 **应用基本信息** 向导页面进行配置后，单击 **下一步：高级设置**。

3. 在 **高级设置** 页面，找到并展开 **应用生命周期管理** 区域。


**警告**

重新部署应用后，该应用将会被重启。为避免业务中断等不可预知的错误，请在业务低峰期执行部署操作。

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在目标应用的 **基础信息** 页面，单击 **部署应用**。

3. 在 **部署应用** 页面，找到并展开 **应用生命周期管理** 区域。


1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在目标应用的 **基础信息** 页面，单击 **修改应用配置**。

3. 在 **修改应用配置** 页面，找到并展开 **应用生命周期管理** 区域。


## 操作步骤

在 **应用生命周期管理** 区域，按需配置 **启动后处理（PostStart设置）**、 **停止前处理（PreStop设置）** 和 **优雅下线超时设置（TerminationGracePeriodSeconds）**。

> 建议您把三者全部进行配置，以实现容器完整的生命周期管控闭环，保障服务平滑启停、资源有序释放及业务零中断。

启动后处理（PostStart设置）

停止前处理（PreStop设置）

优雅下线超时设置（TerminationGracePeriodSeconds）

在 **应用生命周期管理** 区域的 **启动后处理（PostStart设置）** 页签配置PostStart。

**说明**

SAE提供了两种不同的Shell解释器可供您选择，分别是：

- >\_ /bin/sh

- >\_ /bin/bash


例如应用启动前，需要将`Hello from the postStart handler`内容写入`/usr/share/message`文件。

> 在生产环境中，请根据实际业务场景进行配置。本文提供的示例仅为最小化验证配置功能可用性，不可直接用于生产环境。

![oNFSDw9bjS](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2658640471/p920376.png)

**结果验证：**

应用创建或重新部署完成后，使用 **Webshell** 进入应用实例的字符界面，查看`/usr/share/message`文件是否存在并写入了相应的内容。

![R5oYr5WL5f](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2658640471/p920422.png)

在 **应用生命周期管理** 区域的 **停止前处理（PreStop设置）** 页签配置PreStop。

**说明**

SAE提供了两种不同的Shell解释器可供您选择，分别是：

- >\_ /bin/sh

- >\_ /bin/bash


例如在容器终止前执行`Perform cleanup`操作并将其写入到`/cleanup.log`文件中，然后等待100秒以便进行验证。

> 在生产环境中，请根据实际业务场景进行配置。本文提供的示例仅为最小化验证配置功能可用性，不可直接用于生产环境。

![je7qGGznHp](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2658640471/p920481.png)

**结果验证：**

在应用的 **基础信息** 页面，单击 **停止应用**，然后使用 **Webshell** 进入应用实例的字符界面，查看`/cleanup.log`文件是否存在并写入了相应的内容。

![fEznm2T8Jm](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2658640471/p920494.png)

在 **应用生命周期管理** 区域的 **优雅下线超时设置（TerminationGracePeriodSeconds）** 页签配置优雅下线超时时间。

> 如果您设置的优雅下线超时时间小于容器优雅终止的时间（包括PreStop钩子执行耗时和容器处理SIGTERM耗时），则在优雅下线超时时间耗尽时强制终止（信号名称：SIGKILL，退出码：137）容器，导致优雅终止流程中断。例如容器优雅终止的时间为100秒，而设置的优雅超时时间为60秒，那么容器会在优雅终止之前被杀死。

![bXgkgc94CQ](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2658640471/p920575.png)

**结果验证：**

本示例中，设置的优雅超时时间小于容器优雅下线时间，以便结果验证。

在应用的 **基础信息** 页面，单击 **停止应用**，然后使用 **Webshell** 进入应用实例的字符界面，查看容器是否会报137的退出码。

> 容器在优雅下线阶段，容器会一直处于`Terminating`状态，直到超过设置的优雅超时时间。

![51N2ViXRg9](<Base64-Image-Removed>)