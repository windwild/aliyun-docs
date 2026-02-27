### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/) [函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/) [操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/) [监控报警](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/monitoring/) 实例级别事件

# 实例级别事件

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：实例级别指标](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/instance-level-metrics)[下一篇：链路追踪](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/tracing-analysis/)

该文章对您有帮助吗？

反馈

函数计算提供实例级别的事件，通过实例级别事件您可以了解函数实例完整的生命周期，包括实例构建、销毁的流程以及其中各步骤发生的时间点。本文介绍函数实例的生命周期以及实例级别事件的定义、转移流程、类型和查询方式。

## 函数实例的生命周期

函数实例会根据函数当前的请求调用量动态地按需构建与销毁，每个函数实例的生命周期包括**实例构建（Creating）**、**实例运行（Running）**和**实例销毁（Destroying）**阶段，如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8314615671/CAEQYRiBgMCHkPue3hgiIGRlOWI5ZWNhYWM5NzRiZDhhYWRmYTczODY3NDlkOWRj3963382_20230830144006.372.svg)

### 实例构建（Creating）

实例构建，是指函数计算根据您的函数配置为您构建函数实例，包括加载代码或层加载（或拉取镜像）、启动实例和运行 [Initializer回调程序](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics#p-p69-h0q-wee "")。实例构建步骤示意图如下所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8314615671/CAEQNBiBgMCTiY3q4BgiIGE3NTk3M2U0MjZlMzQ0OGU4NDllYTkxNjhkZGVhYjk43963382_20230830144006.372.svg)

实例构建一般在以下两种情况下发生。

- 弹性扩容：若函数当前的实例已经满载，随着调用请求量的继续增加，函数计算会构建新的实例来处理请求，但会造成冷启动。更多信息，请参见 [函数计算冷启动优化最佳实践](https://help.aliyun.com/zh/functioncompute/fc-2-0/use-cases/best-practice-for-reducing-the-cold-start-latency#concept-2259968 "")。

- 预留配置调整：当您使用弹性管理功能配置了预留实例，函数计算会按照您的配置在调用请求到来之前预先构建实例，避免造成冷启动。关于弹性管理功能，请参见 [弹性管理（含预留模式）](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-provisioned-instances-and-auto-scaling-rules#task-2538034 "")。


### 实例运行（Running）

实例运行期间，会调用您的函数处理程序处理调用请求。您可以设置实例并发度调整实例处理请求的策略，还可以使用PreFreeze回调程序进行编程模型扩展。更多信息，请参见 [函数实例生命周期](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/function-instance-lifecycle#section-ks8-wm2-lfj "")。关于实例并发度，请参见 [设置实例并发度](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-instance-concurrency#task-2552850 "")。

函数计算只在实际请求和回调程序执行时计费，在请求以外的时间段内实例会被冷冻。

### 实例销毁（Destroying）

在此阶段，实例彻底被销毁。您可以使用PreStop回调程序进行编程模型扩展。

实例销毁一般在以下三种情况下发生。

- 实例浅休眠（原闲置）：如果实例在一段时间内没有收到任何调用请求，函数计算会自动回收该实例。

- 预留配置调整：当您缩减预留实例数量时，函数计算会立即为您销毁多余的实例。

- 实例异常：如果实例在构建或运行阶段出现了异常，函数计算会销毁该实例。


## 什么是实例级别事件

事件是一种描述资源状态变化的数据记录。实例是函数计算为执行您的请求而构建的核心资源，函数计算系统会动态地构建与销毁实例，从而弹性地处理您的请求。函数计算将您的实例发生各个重要状态变化的时间点定义为各类事件，并支持在实例详情页面进行可视化展示。通过实例级别事件，您不仅可以观察到实例的生命周期，还可以快速定位由实例导致的请求执行异常。

## 事件的相关状态和转移流程

事件标记了资源状态变化的时间点，因此每种事件分别至少与一种可定义的前置状态和后置状态相关。

函数实例的状态转移以及相关事件示意图如下所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8314615671/CAEQNBiBgICDuo7q4BgiIDA2MmY3M2I4YmE1YTRiNzM5MThhZDc1NTJlNmVjZTk53963382_20230830144006.372.svg)

函数实例的状态如下所示。状态转移相关事件的详细信息，请参见 [事件类型](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/instance-level-events#section-5wz-k3b-6gb "")。

- Creating：您的实例正在构建中。实例会根据函数当前的请求调用量动态地按需构建，该状态包含以下子状态。

  - 镜像拉取（ImagePulling）：正在拉取您的镜像（Custom Container运行环境）。

  - 代码加载（CodePreparing）：正在拉取并挂载您的代码包。

  - 层加载（LayerPreparing）：正在拉取并挂载您的层。

  - 实例启动（RuntimeInitializing）：正在启动您的实例并进行健康检查。

  - Initializer执行（Initializing）：正在执行您的Initializer回调程序。

  - 构建完成（Finished）：您的实例构建完成。

  - 构建失败（Failed）：您的实例构建失败。
- Running：您的实例正在运行中。此状态下的实例会处理函数的调用请求。

- Destroyed：您的实例已经被销毁。实例会根据函数当前的请求调用量动态地按需销毁。

- Error：您的实例当前不能正常处理调用请求，即将被销毁。


## 事件类型

|     |     |     |     |
| --- | --- | --- | --- |
| **事件名称** | **事件等级** | **事件含义** | **解决方案** |
| 实例构建中<br>fc:Instance:Creating | Normal | 函数计算开始为您的请求构建所需实例。 | 不涉及。 |
| 代码加载就绪<br>fc:Instance:PrepareCodeSuccess | Normal | 函数计算成功地将您的代码包拉取并挂载到实例中。<br>**说明** <br>函数计算针对代码包加载过程进行了多种优化，部分条件下，用时极短。 | 不涉及。 |
| 代码加载失败<br>fc:Instance:PrepareCodeFailed | Warning | 函数计算未能成功地将您的代码包拉取并挂载到实例中。 | 请加入钉钉用户群（钉钉群号：**64970014484**）获取技术支持。 |
| 层加载就绪<br>fc:Instance:PrepareLayerSuccess | Normal | 函数计算成功地将层拉取并挂载到实例中。<br>**说明** <br>函数计算针对层加载过程进行了多种优化，部分条件下用时极短，且与代码加载同时进行。 | 不涉及。 |
| 层加载失败<br>fc:Instance:PrepareLayerFailed | Warning | 函数计算未能成功地将层拉取并挂载到实例中。 | 请加入钉钉用户群（钉钉群号：**64970014484**）获取技术支持。 |
| 镜像准备就绪<br>fc:Instance:PullImageSuccess | Normal | 函数计算已成功拉取您的Custom Container实例镜像。 | 不涉及。 |
| 镜像准备失败<br>fc:Instance:PullImageFailed | Warning | 函数计算未能成功拉取您的Custom Container实例镜像。 | 请加入钉钉用户群（钉钉群号：**64970014484**）获取技术支持。 |
| 实例启动成功<br>fc:Instance:RuntimeInitializationSuccess | Normal | 函数计算已成功启动您的实例并完成了健康检查。 | 不涉及。 |
| 实例启动失败<br>fc:Instance:RuntimeInitializationFailed | Warning | 函数计算发现您的实例在启动后未能通过健康检查。 | 建议您参考实例日志并结合Custom Runtime错误排查方法解决该问题。关于Custom Runtime错误排查，请参见 [错误处理](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/troubleshooting#task-2273572 "")。 |
| Initializer执行成功<br>fc:Instance:InitializationSuccess | Normal | 您的Initializer回调程序执行成功。 | 不涉及。 |
| Initializer执行失败<br>fc:Instance:InitializationFailed | Warning | 您的Initializer回调程序执行失败。 | 建议您根据请求日志调整Initializer回调程序的逻辑。 |
| 实例构建成功<br>fc:Instance:CreateSuccess | Normal | 您的实例构建成功，即将开始处理调用请求。 | 不涉及。 |
| 实例构建失败<br>fc:Instance:CreateFailed | Warning | 您的实例构建失败，即将被销毁。 | 不涉及。 |
| 实例已销毁<br>fc:Instance:DestroySuccess | Normal | 您的实例已经被销毁。 | 不涉及。 |

## 查询实例级别事件

开启实例级别指标后，函数计算会收集实例的事件信息。该信息将被投递到您在配置日志时选择的日志仓库中，您可以通过以下方式查看实例级别事件信息。关于开启实例级别指标的具体操作，请参见 [配置实例级别指标](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/instance-level-metrics#section-x2m-9yz-9py "")。

### 通过函数计算控制台查看实例事件

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务。
3. 在 **函数管理** 页面，单击目标函数名称，然后在函数详情页面，依次选择**调用日志** \> **调用请求列表**页签。

   - **通过函数计算控制台查看实例事件**

     单击目标请求的实例ID，在实例详情面板，查看实例级别事件。

     ![check-instance-event](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7587220861/p613714.png)

   - **通过日志服务控制台查看原始事件日志**

     单击目标请求右侧 **操作** 列的 **高级日志**，页面跳转至 [日志服务控制台](https://sls.console.aliyun.com/) 的原始日志页面，根据Topic名称筛选日志。Topic名称格式为`FCInstanceEvents:<your-service-name>/<your-function-name>`。

     ![check-instance-log](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4607220861/p613715.png)