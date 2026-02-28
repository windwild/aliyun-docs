### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[自学习平台](https://help.aliyun.com/zh/isi/developer-reference/customization-platform/)[热词](https://help.aliyun.com/zh/isi/developer-reference/hotwords/)在控制台创建热词

# 在控制台创建热词

更新时间：2025-05-29 04:02:43

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：热词](https://help.aliyun.com/zh/isi/developer-reference/hotwords/)[下一篇：管理热词](https://help.aliyun.com/zh/isi/developer-reference/manage-hotwords)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

使用限制

创建热词

应用热词

通过智能语音交互控制台中的添加热词功能，开发者可以上传自定义的热词列表，提升其识别准确率。本文为您介绍如何在控制台创建热词。

## **背景信息**

热词包括 **名称类** 和 **业务类**，具体说明如下：

- **名称类**（人名/地名）

目前名称类热词只支持人名和地名。一个词表中只能包含人名或只能包含地名。

- **业务类**

业务领域内特有词汇，一个词表中不限制热词的类别，如“苹果”、“哈士奇”、“小明”可以放在同一热词文件中。


## 前提条件

已开通智能语音交互服务，详情请参见 [开通服务](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-2572187 "")。

## 使用限制

- 目前支持中文词汇以及单个英文词汇。

- 文件为TXT格式，100 KB以内，`UTF-8（无BOM）`编码。

- 每种类别的热词可各创建10组，每组热词表中，每行一个热词，每个热词不超过15个汉字或7个英文单词。如果某个热词既有中文也有英文，则中文字数+英文字母数总共不超过15个，一组热词表最多500行。

如果您有大量热词的添加需求，请使用语言模型定制。具体操作，请参见 [语言模型定制](https://help.aliyun.com/zh/isi/developer-reference/custom-models/ "")。

- 词语中的数字需要按照发音替换为对应的汉字。例如：“58.9元”需要替换为“五十八点九元”。

- 语料中请不要出现除空格、制表符、换行、换页之外的其他特殊字符。


## 创建热词

设置热词后，新建的语音识别请求立即生效。已经运行的识别请求无法使用该热词。

1. 登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/)。

2. 在左侧导航栏选择 **自学习平台** \> **热词**。

3. 在 **热词** 页面，单击 **创建热词**。

4. 在 **添加热词组** 弹框中，输入 **热词组名称**、选择 **热词类别**、上传热词文件，完成后单击 **确定**。


## **应用热词**

1. 登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/)。

2. 在左侧导航栏选择 **全部项目**，单击目标项目右侧的 **项目功能配置**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0992474271/p840456.png)

3. 在 **自学习** 区域，选择已创建的热词，单击 **应用**。即可使用该热词。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0992474271/p840358.png)