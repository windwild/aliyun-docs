### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 千问

# 千问

更新时间：2026-02-11 02:31:53

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

**重要**

**千问模型定制API调用需申请体验并通过后才可使用，否则API调用将返回错误状态码。不同规模的千问系列模型申请链接不同，如有需求请分别进行申请。**

## **概述**

千问是阿里云自主研发的超大规模语言模型，能够在用户自然语言输入的基础上，通过自然语言理解和语义分析，在不同领域、任务内为用户提供服务和帮助。模型目前具备的能力包括但不限于：

1. 创作文字，如写故事、写公文、写邮件、写剧本、写诗歌等。

2. 编写代码。

3. 提供各类语言的翻译服务，如英语、日语、法语、西班牙语等。

4. 进行文本润色和文本摘要等工作。

5. 扮演角色进行对话。

6. 制作图表。


当前可以支持fine-tune的模型：

- qwen-turbo：千问超大规模语言模型，支持中文英文等不同语言输入。

- qwen-7b-chat：千问开源模型，支持中文英文等不同语言输入。

- qwen-14b-chat：千问对外开源的14B规模参数量的经过人类指令对齐的chat模型。

- qwen-72b-chat：千问对外开源的72B规模参数量的经过人类指令对齐的chat模型。


## **数据准备**

对千问模型进行定制时，所需的训练数据格式为JSON数据，具体如下，您可以提供多条JSON样本在一个JSONL文件中。注意每行仅包含一条JSON。

### **定制数据格式**

1. messages


用户可以直接采用messages格式的数据集进行微调训练，具体使用方式如下：

```json
{"messages": [{"role": "system", "content": "You are a helpful assistant"}, {"role": "user", "content": "谁在文艺复兴时期绘制人体?"}, {"role": "assistant", "content": "文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"}]}
{"messages": [{"role": "system", "content": "You are a helpful assistant"}, {"role": "user", "content": "I need a picture of someone crying."}, {"role": "assistant", "content": "I'm sorry, but as an AI language model, I do not have the ability to display images."}]}
```

需要注意的是：

- 针对role为system的情况可以空缺，不传。即，可以如下使用方式


```json
{"messages": [{"role": "user", "content": "谁在文艺复兴时期绘制人体?"}, {"role": "assistant", "content": "文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"}]}
```

- role为user和role为assistant需要成对顺序出现，如下是两个错误的示例：


```json
{"messages": [{"role": "system", "content": "You are a helpful assistant"}, {"role": "user", "content": "谁在文艺复兴时期绘制人体?"}, {"role": "user", "content": "还有制造雕塑的有谁？"},{"role": "assistant", "content": "文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"}]}
```

```json
{"messages": [{"role": "system", "content": "You are a helpful assistant"}, {"role": "user", "content": "谁在文艺复兴时期绘制人体?"}, {"role": "assistant", "content": "文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"},{"role": "assistant", "content": "文艺复兴时期的雕塑也非常有名，是否需要我给你推荐？"}]}
```

- user-assistant交流根据历史聊天记录顺序可支持多轮聊天，如下示例：


```json
{"messages": [{"role": "system", "content": "You are a helpful assistant"}, {"role": "user", "content": "谁在文艺复兴时期绘制人体?"}, {"role": "assistant", "content": "文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"},{"role": "user", "content": "那雕塑方面如何呢？"}, {"role": "assistant", "content": "文艺复兴时期的雕塑也非常有名，几位世界级的雕塑大师都出自于这个时期"}]}
```

2. prompt-completion


针对可以被归类为续写任务的场景，利用text-generation任务即可满足要求的情况，或者单轮对话即可完成的任务，可以选择以下方式进行数据准备。要求准备`prompt`以及 `completion`两个参数，具体使用方式如下所示。

```json
{"prompt": "谁在文艺复兴时期绘制人体?", "completion": "文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"}
{"prompt": "I need a picture of someone crying.", "completion": "I'm sorry, but as an AI language model, I do not have the ability to display images."}
```

3. human-assistant (legacy formatting, deprecating)


针对历史用户，可以继续使用该数据格式进行训练任务，新用户建议采用以上两种方式。

在准备SFT训练数据阶段的过程中需要构造出对话的结构，需要包含`Human:`以及`Assistant:`两个特殊符值，并且在两个值前均加上换行字符`\n\n`，注意`\n\n`与特殊符值间没有额外空格等符号。

同时，将问题或者描述紧跟放在`Human:`后，将预期返回的答案放在`Assistant:`后，注意`Assistant:`与前面的文本仅有`\n\n`，没有额外空格等符号。

具体参考实例如下：

```json
{"text": "\n\nHuman: 谁在文艺复兴时期绘制人体\n\nAssistant: 文艺复兴时期是一个关于艺术、文化和学术的复兴运动，在这个时期，许多艺术家都绘制了人体。"}
{"text": "\n\nHuman: I need a picture of someone crying.\n\nAssistant: I'm sorry, but as an AI language model, I do not have the ability to display images."}
```

**说明**

**您提供的数据长度应大于您在超参中设置的batch\_size，数据长度指JSONL文件中，JSON数据的行数。**

## **超参设置**

无论使用命令行还是通过HTTP API的形式进行模型定制，您均可以设置如下超参数。所有超参数均有默认值。

| **超参** | **类型** | **含义** | **取值范围** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **超参** | **类型** | **含义** | **取值范围** |
| n\_epochs | integer | 训练数据所需的轮数，每一轮epoch，用户提供的数据会被模型完整学习一遍。 | 1到10之间的整数，默认为1 |
| batch\_size | integer | 单次传递给模型用以训练的数据（样本）个数，一般单次训练数据个数越大，占用显存会越多，同时单步训练速度会越慢，但是训练效果会越好 | 2或者4，默认为2 |
| learning\_rate | float | 学习率，决定了每次参数更新时参数应该更新的幅度大小，越大的幅度，会越快收敛，但是也容易导致不稳定，越小的幅度，训练会较稳定，但是收敛会慢一些 | 默认为2e-5 |

### **使用限制**

当您对千问模型定制时，模型定制功能会有如下限制存在

- 运行中的定制任务数：1个

- 可创建的定制任务数（不包括失败及取消的）：5个


当超过如上限制后，您的请求会收到HTTP错误码429，并在response中包含特定信息

### **定制任务状态说明**

我们对定制任务设置了多种状态，具体如下

| **状态** | **含义** |
| --- | --- |

|     |     |
| --- | --- |
| **状态** | **含义** |
| PENDING | 正在准备训练所需资源。 |
| RUNNING | 训练正在进行中。 |
| SUCCEEDED | 训练成功。 |
| FAILED | 训练失败。 |
| CANCELED | 训练取消。 |

### **定制任务错误码说明**

当定制任务失败时，您可以通过定制任务返回的code信息来判断错误发生的原因。当您收到的错误码不在下方表格所列范围内时，请联系技术支持。

| **错误码** | **含义** | **处理方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **含义** | **处理方案** |
| 1 | 系统内部错误 | 多数情况下是由于超参设置不合理，建议不设置超参数，使用默认值重试。 |
| 13 | 数据格式错误，不应包含空行 | 修正您提供的测试数据。 |
| 14 | 数据格式错误，数据不可解析为JSON | 修正您提供的测试数据。 |
| 15 | 数据格式错误，数据长度不够训练最低要求 | 您提供的数据集行数应在50行以上。 |