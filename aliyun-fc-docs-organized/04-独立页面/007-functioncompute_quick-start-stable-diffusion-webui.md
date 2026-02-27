### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 快速入门

# 快速入门

更新时间：2025-07-09 23:42:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

一键部署Stable Diffusion项目

发布API

删除项目

Function AI支持一键部署Stable Diffusion图像生成项目，提供从项目开发到API调用的应用全生命周期管理能力。本文介绍如何快速部署并使用Stable Diffusion WebUI文生图项目。

图像生成应用全生命周期包括项目开发阶段和API调用阶段。

- 项目开发阶段：在Function AI一键部署图像生成应用后进入项目开发阶段，在此阶段您可以通过调试提示词与工作流，安装模型与插件，生成实现预期效果的图片或视频。

- API调用阶段：项目开发阶段通过安装模型、插件和依赖，搭建好出图环境，您可以将调试好的工作空间发布成为弹性高可用的API。API调用阶段基于出图环境运行工作流，通过Serverless API弹性高效出图。


## **前提条件**

- [授权RAM用户使用图像生成项目](https://help.aliyun.com/zh/functioncompute/authorize-ram-users-to-use-images-to-generate-projects "")。

- 为了获得更好的使用体验，请确保账户余额大于等于100元。为了节省成本，建议您领取新客户 [试用套餐](https://help.aliyun.com/zh/functioncompute/fc/product-overview/trial-quota-1 "")。


## **一键部署** Stable Diffusion **项目**

1. 登录 [函数计算3.0控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏单击 **Function AI**，在 **Funciton AI** 页面导航栏，单击 **项目**，然后选择**创建项目** \> **创建图像生成**。



**说明**





当左上角显示函数计算FC 3.0时，表示当前控制台为3.0控制台。

2. 选择项目类型为 **Stable Diffusion项目**，设置项目名称，选择 **地域**，其余项目选择默认值，然后单击 **部署项目**。



**说明**





   - GPU 费用采用 Serverless 计费方式，界面显示的预估费用仅供选型参考，以实际业务使用为准。

   - 如果项目面向的用户集中于一个地理分区，推荐您将项目创建在对应的地域。如果当前地域 **GPU规格** 资源不满足您的需求，建议您更换地域。


3. 在弹出的 **项目资源预览** 对话框，确认部署本项目涉及的产品的 [计费说明](https://help.aliyun.com/zh/functioncompute/what-is-a-serverless-development-platform#8495e55060qp6 "") 和资源用途，然后单击 **确认部署**。

   - 部署完成后，自动启动工作空间，进入项目开发阶段，也就是使用WebUI生成图片或视频的调试阶段。

   - 启动工作空间会启动一个GPU实例，您可以下载模型、安装插件，并通过调试提示词与工作流生成图片和视频。

   - 使用完成后，请及时关闭工作空间，关闭工作空间后，函数实例销毁，停止计费，您在下次使用工作空间前需要再次启动工作空间。
4. 在Stable Diffusion项目的工作空间，设置提示词，单击 **Generate**，完成出图。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1698112571/p950502.png)

生成的图片，存放在`output/`目录，您可以选择 **文件管理** 页签，在对应目录下获取。

5. 在Stable Diffusion项目开发界面，选择 **文件管理** 页签，上传自定义模型到`models/`目录。


使用自定义模型，然后根据界面提示调整 **采样方法**， **采样步数**、 **高分辨率修复**、 **图像生成种子** 等参数，生成更符合需求的图片后，您可以 [发布API](https://help.aliyun.com/zh/functioncompute/quick-start-stable-diffusion-webui#bd0dfffd463hl "")。



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1698112571/p953013.png)


## **发布API**

- 发布API可将当前调试好的工作空间（包含Stable Diffusion需要的源码、插件、依赖包）发布。

- 发布API会创建新的函数，您可以配置新的资源规格和弹性策略，基于Serverless API弹性出图。


1. 在项目开发页面，点击右上角的 **发布API**。

2. 在 **初始化 API** 对话窗，选择GPU规格，设置弹性策略，然后单击 **确定**。



**重要**





发布 API 时默认为 API 调用阶段开启快照，用于提前锁定弹性资源，避免冷启动。非出图阶段，将收取少量的快照付费，出图阶段，按照弹性实例计费。如果您持续一段时间内不打算使用Stable Diffusion项目，请及时在 **API调用** 页面的 **配置管理** 页签，设置快照数为0。

3. 发布完成后，选择 **API调用** 页签，您可以通过Curl命令或Postman等第三方工具调用API弹性出图。


## **删除项目**

1. 单击项目名称，进入项目详情页，单击 **删除**。

2. 在弹出的对话框，您可以看到要删除的资源。默认情况下，Function AI会删除项目下的所有服务。如果您希望保留资源，可以 **取消勾选** 指定的服务，删除项目时只会删除 **勾选** 的服务。

3. 勾选 **我已知晓：删除该项目及选中的服务将立刻中断其所服务的线上业务，并且不可恢复，同时将彻底删除其所依赖的云产品资源**，然后单击 **确定删除**。