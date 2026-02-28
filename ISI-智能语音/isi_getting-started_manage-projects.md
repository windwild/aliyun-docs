### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[快速入门](https://help.aliyun.com/zh/isi/getting-started/)管理项目

# 管理项目

更新时间：2025-11-05 00:52:34

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here)[下一篇：获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token-1/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

创建项目

配置项目

语音识别

语音合成

编辑项目

删除项目

智能语音交互中的一个项目代表一个业务场景，由于各个场景的词汇各异，如果您有多个业务场景，可以创建多个项目，并根据各项目业务特点做个性化配置。本文为您介绍如何创建以及配置管理智能语音交互项目。

## **前提条件**

已开通智能语音交互服务。具体操作，请参见 [步骤3：开通服务](https://help.aliyun.com/zh/isi/getting-started/start-here#603bae7139cmk "")。

## 创建项目

1. 登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/overview)。

2. 在左侧导航栏单击 **全部项目**。

3. 在 **我的所有项目** 页面，单击 **创建项目**。

4. 在 **创建项目** 对话框中，填写 **项目名称**、选择 **项目类型**，选填 **项目场景描述**。

项目类型包括： **语音识别+语音合成** **+语音分析**、 **仅语音识别**、 **仅语音合成**、 **设备端解决方案**


> 项目类型仅用于简化控制台配置，不会限制 API 功能。例如，选择“仅语音识别”时，API仍可调用语音合成服务。

5. 创建完成后，可以在 **我的所有项目** 页面查看已创建的项目，以及项目对应的Appkey。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6162716071/p762423.png)


## **配置项目**

### **语音识别**

当 **项目类型** 为 **仅语音识别** 或 **语音识别 \+ 语音合成 \+ 语音分析** 时，项目配置操作如下。

1. 单击目标项目右侧的 **项目功能配置**。

2. 在 **语音识别ASR** 区域，选择基础模型或者自学习模型。

   - 单击 **修改配置**，根据使用场景选择基础模型，在线测试无问题后，单击 **确认使用**。

     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6162716071/p762480.png)

   - 如果基础模型无法满足业务需求，您可以通过设置热词或者定制模型实现个性化配置。具体操作请参见 [语言模型定制](https://help.aliyun.com/zh/isi/developer-reference/overview-2 "") 和 [热词](https://help.aliyun.com/zh/isi/developer-reference/overview-1 "")。

     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6162716071/p762482.png)

### **语音合成**

当 **项目类型** 为 **仅语音合成** 或 **语音识别 \+ 语音合成 \+ 语音分析** 时，项目配置操作如下。

在 **语音合成TTS** 模块下，选择语音合成模型并配置基础参数（语速、语调、音量）。发布上线后，将与项目Appkey绑定。如果您的应用程序中没有设置这些参数值，将使用控制台的默认值。

1. 单击目标项目右侧的 **项目功能配置**。

2. 在 **语音合成TTS** 区域，单击 **修改配置**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6162716071/p762488.png)

3. 选择发音人，在 **基础参数** 区域配置合适的语速、语调和音量。

4. 在右侧的 **测试** 模块试听播放效果。

5. 单击 **确认使用**。确认后，模型立即生效。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6162716071/p762489.png)


## **编辑项目**

单击目标项目右侧的 **编辑**，修改项目名称或场景描述。

## **删除项目**

单击目标项目右侧的 **删除**，即可删除该模型。

**警告**

已删除的项目将不可找回，请谨慎操作。