### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/)[实例扩缩容](https://help.aliyun.com/zh/sae/instance-scaling-new/)配置弹性伸缩策略

# 配置弹性伸缩策略

更新时间：2025-03-11 03:11:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：手动扩缩](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/manual-scaling)[下一篇：配置基于Prometheus指标的弹性伸缩策略](https://help.aliyun.com/zh/sae/configure-scaling-policies-based-on-prometheus-metrics)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

视频教程

功能介绍

适用场景

注意事项

前提条件

功能入口

配置弹性伸缩策略

验证弹性策略是否生效

更多操作

在Serverless 应用引擎 SAE（Serverless App Engine）的微服务应用中，为了应对突发的流量高峰，您可以添加弹性策略，以实现应用实例的自动扩缩容。本文主要介绍在微服务应用中如何配置弹性伸缩策略。

## 视频教程

您可以观看以下视频，了解什么是弹性伸缩以及如何在SAE控制台快速使用弹性伸缩策略。

配置弹性伸缩策略

## 功能介绍

SAE扩缩容支持以下方式：

- [手动扩缩](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/manual-scaling "") **：** 当应用扩缩容为紧急需求时，例如突发性的流量高峰，您可以选择手动扩缩方式。

- [自动扩缩](https://help.aliyun.com/zh/sae/sae-auto-scaling-best-practices "") **：** 当应用扩缩容为非紧急需求时，例如周期性的流量高峰，您可以选择自动扩缩方式，即配置弹性伸缩策略。SAE弹性伸缩策略包括定时弹性策略、监控指标弹性策略和混合弹性策略。


配置弹性伸缩策略的全流程如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4607761471/CAEQVRiBgMCNvouQrBkiIGExYWM0ZDUxYTE1MTQ3ZDhhZTBhMmRjMjgwMmQzNTU44959224_20250305111140.327.svg)

## 适用场景

SAE支持配置三种类型的弹性伸缩策略：

- **定时策略：** 适用于资源使用率有周期性规律的应用场景，多用于证券、医疗、政府和教育等行业。

- **监控指标策略：** 适用于突发流量和典型周期性流量的应用场景，多用于互联网、游戏和社交平台等行业。

- **混合弹性策略：** 适用于同时处理兼具周期性资源需求波动与突发流量特点的应用场景，多用于互联网、教育和餐饮等行业。


## 注意事项

- 最多支持创建5条定时策略、一条监控指标策略或一条混合弹性策略，三种策略不能同时使用。

- 弹性策略启用时，请勿手动进行应用生命周期管理操作，例如应用扩缩、部署应用、更改规格、重启应用和停止应用。如果需要对应用进行此类操作，先停用弹性策略，然后再手动执行操作。

- 如果当前应用处于扩容、缩容、部署（单批、分批或灰度）、更改规格、重启和停止等过程，需等待过程完成后，才可添加或启动弹性策略。

- 单应用的实例数上限为50。如需提升额度，请加入钉群（钉群号：32874633），申请开通白名单。


## **前提条件**

[已部署应用](https://help.aliyun.com/zh/sae/sae-application-deployment/ "")。

## **功能入口**

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在目标应用的 **基础信息** 页面，单击 **弹性伸缩** 页签，然后在 **弹性伸缩** 区域单击 **添加弹性策略**。


## **配置弹性伸缩策略**

定时策略

监控指标策略

混合弹性策略

1. 在弹出的 **添加弹性策略** 面板，配置以下参数信息，然后单击 **下一步：预览定时策略**。


|     |     |     |
| --- | --- | --- |
| **参数** | **说明** | **示例** |
| **策略类型** | 选择 **定时策略**。 | 定时策略 |
| **策略名称** | 自定义。 | demo |
| **选择时间** | 时间可以选择长期或短期：<br>   - **短期：** 需要选择开始时间和结束时间。<br>     <br>   - **长期：** 选择长期，则此策略长期有效。 | 长期 |
| **周期** | 周期可以选择每天、每周或每月。 | 每天 |
| **单天内的触发时间** | 选择 **触发时间** 和 **触发时间之后保持的实例数**。<br>**触发时间：** 弹性策略触发的时间。<br>**触发时间之后保持的实例数：** 弹性策略被触发后，扩缩容之后的实例数。 | 触发时间：08：00和20：00<br>触发时间之后保持实例数：10和3 |


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8777237271/p852846.png)

2. 在 **预览定时策略** 导向页，预览特定时间段的实例数，然后单击 **确认**。

3. 添加完定时策略后， **启用** 该策略。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1607761471/p926420.png)


1. 在弹出的 **添加弹性策略** 面板，配置以下参数信息，然后单击 **确认**。


|     |     |     |
| --- | --- | --- |
| **参数** | **说明** | **示例** |
| **策略类型** | 选择 **监控指标策略**。 | 监控指标策略 |
| **策略名称** | 自定义。 | demo |
| **触发条件** | 选择指标类型：<br>   - CPU使用率。<br>     <br>   - 内存使用率。<br>     <br>   - TCP活跃连接数。<br>     <br>   - TCP总连接数。<br>     <br>   - 应用QPS。<br>     <br>   - 应用响应时间（RT）。<br>     <br>   - 公网CLB QPS。<br>     <br>   - 公网CLB响应时间。<br>     <br>   - 私网CLB QPS。<br>     <br>   - 私网CLB响应时间。<br>     <br>**说明**<br>   - 指标类型的聚合方式，请参见控制台说明。<br>     <br>   - 您可以同时设置多个指标类型。 | CPU使用率 |
| 设置目标值。当目标指标类型等于设置的目标值，会触发弹性策略，实现应用实例的自动扩缩容。 | 70% |
| **实例数设置** | 设置 **应用最小实例数**、 **应用最大实例数** 和 **最小存活实例数**。<br>**说明**<br>**最小存活实例数** 为每次滚动更新时最小存活的实例数，可以 **按个数** 进行设置，也可以 **按比例** 进行设置。 | - 应用最小实例数：6<br>     <br>   - 应用最大实例数：50<br>     <br>   - 最小存活实例数：按个数进行设置，设置最小存活实例数为3 |
| **高级设置** | **（非必填项）** 请按照需求配置以下信息：<br>   - **弹性扩容步长**：单位时间内最多扩容的实例数。<br>     <br>   - **弹性缩容步长**：单位时间内最多缩容的实例数。<br>     <br>   - **扩容稳定窗口**：稳定窗口期系统趋于维稳状态。通过自动扩缩算法来保证当需要执行扩容时，使用指定时间间隔内所计算的期望目标实例数中的最小值。<br>     <br>   - **缩容稳定窗口**：稳定窗口期系统趋于维稳状态。通过自动扩缩算法来保证当需要执行缩容时，使用指定时间间隔内所计算的期望目标实例数中的最大值。<br>     <br>   - **禁止缩容**：开启后将永远不会缩容该应用的实例，能有效防止在流量高峰期缩容造成业务风险。默认关闭。 | 请参见 [弹性策略中高级参数的最佳实践](https://help.aliyun.com/zh/sae/best-practices-for-configuring-advanced-parameters-in-auto-scaling-policies "") |


![7CcVilH39K](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0263951471/p925062.png)

2. 添加完监控指标弹性策略后， **启用** 该策略。

![I22ZVFs2G4](<Base64-Image-Removed>)


**说明**

**混合弹性策略** 是混合了 **定时策略** 和 **监控指标策略**。

1. 在添加弹性策略面板，设置以下参数信息。

1. **弹性类型** 选择 **混合弹性策略**，自定义 **策略名称**。

2. **监控指标设置**。请参见 [监控指标策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new#6febc42f45rnb "")。

      ![image](<Base64-Image-Removed>)

3. **非必填项：** 单击 **[高级设置](https://help.aliyun.com/zh/sae/best-practices-for-configuring-advanced-parameters-in-auto-scaling-policies "")**，按需配置以下信息。


      |     |     |     |
      | --- | --- | --- |
      | **配置项** | **说明** | **示例** |
      | **弹性扩容步长** | 单位时间内最多扩容的实例数。 | 3 |
      | **弹性缩容步长** | 单位时间内最多缩容的实例数。 | 2 |
      | **扩容稳定窗口** | 稳定窗口期系统趋于维稳状态。通过自动扩缩算法来保证当需要执行扩容时，使用指定时间间隔内所计算的期望目标实例数中的最小值。 | 300秒 |
      | **缩容稳定窗口** | 稳定窗口期系统趋于维稳状态。通过自动扩缩算法来保证当需要执行扩容时，使用指定时间间隔内所计算的期望目标实例数中的最小值。 | 300秒 |
      | **禁止缩容** | 开启后将永远不会缩容该应用的实例，能有效防止在流量高峰期缩容造成业务风险。默认关闭。 | 开启 |


      ![9d12xgdrlp](<Base64-Image-Removed>)

4. **特殊事件段设置**。请参见 [定时策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new#408cfa0b02jw1 "")。

      ![image](<Base64-Image-Removed>)
2. 在 **预览定时策略** 配置向导，预览特定时间段的实例数，然后单击 **确认**。

3. 添加完混合弹性策略后， **启用** 该策略。

![image](<Base64-Image-Removed>)


## **验证弹性策略是否生效**

要验证弹性策略是否生效，您可以从以下三种方法中任选其一进行测试：

查看当前实例数与目标实例数是否相同

配置公网访问地址进行压测

查看弹性事件

进入目标应用的 **基础信息** 页面，单击 **弹性伸缩** 页签，查看实例数是否与弹性策略设置的实例数相同，如果相同，则表明弹性策略已生效。

![image](<Base64-Image-Removed>)

1. 为应用添加公网访问地址。

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，进入目标微服务应用的 **基础信息** 页面，在 **应用访问设置** 区域单击 **添加公网CLB 访问**。

      ![image](<Base64-Image-Removed>)

2. 在弹出的 **添加公网 CLB 访问** 面板，选择 **新建CLB（按规格计费）**，然后设置 **HTTP端口** 和 **容器端口**，最后单击 **确定**。

      ![image](<Base64-Image-Removed>)

3. **公网访问地址** 添加成功后，复制公网访问地址。

      ![image](<Base64-Image-Removed>)
2. 对应用进行压测。

1. 登录 [性能测试服务 PTS 控制台](https://pts.console.aliyun.com/#/overviewpage)，在概览页面输入公网IP（格式为：`https://公网IP`），然后单击 **压测**。

      ![image](<Base64-Image-Removed>)

2. 在弹出的 **压测配置** 面板，输入 **每秒请求数(RPS)**，然后勾选 **确认本次压测已获得准许并遵守当地法律** 并单击 **启动压测**。

      ![image](<Base64-Image-Removed>)
3. 返回 [SAE控制台](https://saenext.console.aliyun.com/overview)，进入目标应用的 **基础信息** 页面，然后在 **实例列表** 页签查看应用实例数是否进行了自动扩容，如果进行了自动扩容，则表明弹性策略已生效。

![image](<Base64-Image-Removed>)



**说明**





当压测结束后，实例数会进行自动的缩容，此过程需要一定的时间，请您耐心等待。


进入目标应用的 **应用事件** 页面，选择筛选条件为 **来源类型**，并将来源类型设置为 **自动弹性（HorizontalPodAutoscaler）**，以查看因弹性策略触发的变更所产生的事件。

![aad95042a117c2265947af5fb82c4845](<Base64-Image-Removed>)

## 更多操作

1. 进入目标应用的 **基础信息** 页面，单击 **弹性伸缩** 页签。

2. 在 **弹性伸缩** 页签的 **弹性伸缩** 区域，在目标策略的 **操作** 列，按需对策略进行 **启用**、 **停止**、 **编辑**、 **删除** 和查看触发策略所产生的 **事件**。

![image](<Base64-Image-Removed>)