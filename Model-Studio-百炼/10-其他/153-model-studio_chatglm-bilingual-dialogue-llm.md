### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) ChatGLM开源双语对话语言模型

# ChatGLM开源双语对话语言模型

更新时间：2026-02-11 02:31:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

数据准备

定制数据格式

超参设置

使用限制

定制任务状态说明

定制任务错误码说明

## **概述**

ChatGLM2模型是由智谱AI出品的大规模语言模型。您可以通过大模型服务平台提供的模型定制功能对平台内置的ChatGLM2模型进行微调。

当前在大模型服务平台提供模型定制能力的ChatGLM2模型来自于ModelScope社区模型：

- [chatglm-6b-v2](https://modelscope.cn/models/ZhipuAI/chatglm2-6b/summary)


您可以使用上述模型名调用 [模型调优 API 参考](https://help.aliyun.com/zh/model-studio/model-training-api-reference#11b621b12bekg "") 创建定制任务，并将定制任务成功后产生的新模型通过 [模型部署API详情](https://help.aliyun.com/zh/model-studio/model-deployment-api "") 部署为一个可调用的服务。

## **数据准备**

对ChatGLM2模型进行定制时，所需的训练数据格式为JSON数据，您可以提供多条JSON样本在一个JSONL文件中，注意每行仅包含一条JSON。

### **定制数据格式**

在准备SFT训练数据阶段的过程中需要构造出对话的结构，需要包含 `Human:` 以及 `Assistant:`两个特殊符值，并且在两个值前均加上换行字符`\n\n`。注意 `\n\n` 与特殊符值间没有额外空格等符号。

同时，将问题或者描述紧跟放在`Human:` 后，将预期返回的答案放在`Assistant:`后， 注意 `Assistant:`与前面的文本仅有`\n\n`，没有额外空格等符号。

具体参考实例如下：

```json
{"text": "\n\nHuman: 谁在文艺复兴时期绘制人体\n\nAssistant: 文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"}
{"text": "\n\nHuman: I need a picture of someone crying.\n\nAssistant: I'm sorry, but as an AI language model, I do not have the ability to display images."}
```

**说明**

**您提供的数据长度应大于您在超参中设置的batch\_size，数据长度指JSONL文件中JSON数据的行数。**

## **超参设置**

无论使用命令行还是通过HTTP API的形式进行模型定制，您均可以设置如下超参数。所有超参数均有默认值。

|     |     |     |     |
| --- | --- | --- | --- |
| 超参 | 类型 | 含义 | 取值范围 |
| n\_epochs | _Integer_ | 训练数据所需的轮数，每一轮epoch，用户所提供的数据会被模型完整学习一遍。 | 正整数 |
| batch\_size | _Integer_ | 单次传递给模型用以训练的数据（样本）个数，一般单次训练数据个数越大，占用显存会越多，同时单步训练速度会越慢，但是训练效果会越好 | \[1,2,4,8,16,32\] |
| learning\_rate | _Float_ | 学习率，决定了每次参数更新时参数应该更新的幅度大小，越大的幅度，会越快收敛，但是也容易导致不稳定，越小的幅度，训练会较稳定，但是收敛会慢一些 | 默认为2e-5 |

### **使用限制**

当您对ChatGLM2模型定制时，模型定制功能会有如下限制存在

- 运行中的定制任务数：1个

- 可创建的定制任务数（不包括失败及取消的）：5个


当超过如上限制后，您的请求会收到HTTP错误码429，并在response中包含特定信息

### **定制任务状态说明**

我们对定制任务设置了多种状态，具体如下

|     |     |
| --- | --- |
| 状态 | 含义 |
| PENDING | 正在准备训练所需资源 |
| RUNNING | 训练正在进行中 |
| SUCCEEDED | 训练成功 |
| FAILED | 训练失败 |
| CANCELED | 训练取消 |

### **定制任务错误码说明**

当定制任务失败时，您可以通过定制任务返回的code信息来判断错误发生的原因。当您收到的错误码不在下方表格所列范围内时，请联系技术支持。

|     |     |     |
| --- | --- | --- |
| 错误码 | 含义 | 处理方案 |
| 13 | 数据格式错误，不应包含空行 | 修正您提供的测试数据 |
| 14 | 数据格式错误，数据不可解析为JSON | 修正您提供的测试数据 |
| 15 | 数据格式错误，数据长度不够训练最低要求 | 您提供的数据集行数应大于您设置的batch\_size，当您未设置该值时，系统会使用默认值16 |