### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[实践教程](https://help.aliyun.com/zh/functioncompute/fc-2-0/use-cases/)[基于Source构建第三代应用的集成方案](https://help.aliyun.com/zh/functioncompute/fc-2-0/use-cases/integrate-3rd-party-applications-by-using-event-sources/)Teambition集成

# Teambition集成

更新时间：2025-09-10 05:32:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SAP BTP系统集成](https://help.aliyun.com/zh/functioncompute/fc-2-0/use-cases/integrate-sap-btp)[下一篇：Dynatrace](https://help.aliyun.com/zh/functioncompute/fc-2-0/use-cases/integrate-dynatrace)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

步骤一：创建Teambition系统源

步骤二：新增报警媒介

步骤三：触发事件

步骤四：结果验证

本文介绍如何基于事件总线EventBridge的HTTP Source和Teambition进行集成对接。

## 背景信息

Teambition是一款团队协作工具。面向企业和团队提供数字化协同办公服务。事件总线EventBridge支持将Teambition的事件进行快速集成，实现对注册用户的通知和异常事件的处理功能。

## 前提条件

- [开通事件总线EventBridge并授权](https://help.aliyun.com/zh/eventbridge/getting-started/activate-eventbridge-and-grant-permissions-to-a-ram-user#task-1947668 "")

- [创建自定义总线](https://help.aliyun.com/zh/eventbridge/user-guide/manage-custom-event-buses#section-sfl-pcs-6rh "")

- [注册Teambition账号](https://account.teambition.com/login)


## 步骤一：创建Teambition系统源

在 [事件总线EventBridge控制台](https://eventbridge.console.aliyun.com/) 创建事件源 **HTTP/HTTPS 触发**，参数配置如下。更多信息，请参见 [自定义事件源HTTP/HTTPS触发](https://help.aliyun.com/zh/eventbridge/user-guide/create-a-custom-event-source-of-the-http-or-https-events-type#task-2189835 "")。

- **请求类型**：选择 **HTTPS**。

- **请求方法**：选择 **POST**。

- **安全配置**：选择 **无需配置**。


创建完成后，您可以在事件源列表找到刚才创建的自定义事件源，然后单击 **详情** 查看配置信息。其中 **公网请求 URL** 可以作为事件源的接入Webhook地址。![pic-1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7744708761/p411255.png)

## 步骤二：新增报警媒介

1. 登录 [Teambition控制台](https://open.teambition.com/)。

2. 单击 **立即创建**，在 **创建应用** 对话框，设置 **应用类型**、 **应用名称** 和 **应用描述**，单击 **创建**。

3. 在左侧菜单栏，选择**应用开发** \> **Webhook 配置**。

4. 在 **Webhook 配置** 页面，单击 **添加**，填写 [步骤一：创建Teambition系统源](https://help.aliyun.com/zh/functioncompute/fc-2-0/use-cases/integrate-teambition#section-sd4-jl0-p2x "") 中获取的 **公网请求 URL**，单击 **保存**。


## 步骤三：触发事件

1. 在 **Webhook 配置** 页面，在添加的公网请求URL右侧，单击 **发送验证**。


## 步骤四：结果验证

1. 登录 [事件总线EventBridge控制台](https://eventbridge.console.aliyun.com/)。
2. 在顶部菜单栏，选择地域。
3. 在左侧导航栏，单击 **事件总线**。
4. 在 **事件总线** 页面，选择目标自定义事件总线，在其操作列，单击 **事件追踪** 查看事件详情。