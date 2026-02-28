### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 开始节点

# 开始节点

更新时间：2025-07-22 22:46:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

定义

前置条件

节点配置

输入字段

## **定义**

开始节点是每个工作流应用不可或缺的预设组成部分。它负责收集并传递后续工作流节点所需的初始信息，例如用户输入的内容和上传的文件，确保整个应用的流程顺畅运行。

## **前置条件**

[创建AI Studio服务](https://help.aliyun.com/zh/cap/user-guide/create-an-ai-studio-service/ "")

### 节点配置

在开始节点的设置页，您可以看到 **输入字段** 配置。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2597323571/p983610.png)

### 输入字段

**输入字段** 功能由应用开发者设置，旨在引导应用使用者主动提供更多必要信息。例如，在周报应用中，您可以要求用户提前提供姓名、工作日期区间、工作详情等背景信息。这些预置信息能显著提高大型语言模型（LLM）生成回答的质量。

单击 **输入字段** 右侧的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2597323571/p983617.png)，我们支持以下四种类型的输入变量，所有变量均可设置为必填项：

- **文本：** 用于短文本输入，用户可自行填写内容，最大长度为 256 个字符。

- **段落：** 用于长文本输入，允许用户输入较长的内容。

- **下拉选项：** 由应用开发者预设固定选项，用户只能从中选择，无法自行填写。

- **数字：** 仅允许用户输入数字。


配置完成后，单击 **保存**，单击 **测试运行**，用户在使用应用前将按照输入项指引，向LLM提供必要信息。更多的信息将有助于LLM提升问答效率。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2597323571/p983626.png)