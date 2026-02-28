### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 配置项目

# 配置项目

更新时间：2022-07-12 23:00:49

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

配置项目

语音识别

语音合成

本文为您介绍如何配置语音识别及语音合成项目。

## 前提条件

已创建项目，请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#topic-1917890 "")。

## 配置项目

在 [智能语音交互控制台](https://nls-portal.console.aliyun.com/) 的 **全部项目** 列表页，单击项目列表右侧 **操作** 栏下的 **项目功能配置**。

![图片 1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9514167561/p303191.png)

### 语音识别

1. 单击 **语音识别ASR** 模块下的 **修改配置**。![图片 5](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9514167561/p303023.png)

2. 在场景列表中选择基础模型或添加 **自学习模型**。自学习模型的使用方法，请参见 [管理定制模型](https://help.aliyun.com/zh/isi/developer-reference/manage-custom-models#topic-2572201 "")。

3. 在 **语音识别ASR** 模块下，您可以配置热词和语言模型，单击应用，详情请参见 [自学习](https://help.aliyun.com/zh/isi/developer-reference/customization-platform/)。


### 语音合成

在 **语音合成TTS** 模块下，选择语音合成模型并配置基础参数（语速、语调、音量）。发布上线后，将与项目Appkey绑定。如果您的应用程序中没有设置这些参数值，将使用控制台的默认值。

1. 选择发音人。更多声音的适用场景请参见 [语音合成接口说明](https://help.aliyun.com/zh/isi/developer-reference/overview-of-speech-synthesis#topic-2572243 "")。

2. 在 **基础参数** 模块配置合适的语速、语调和音量。

3. 在右侧的 **测试** 模块试听播放效果。

4. 单击 **确认使用**。确认后，模型立即生效。
![图片 7](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2715858261/p303040.png)