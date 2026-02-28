### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 三方模型应用

# 三方模型应用

更新时间：2026-02-11 02:07:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能描述

API详情

请求参数

响应参数

示例

请求示例

响应示例

请求示例（流式SSE）

响应示例（流式SSE）

**重要**

历史文档仅适用于阿里云百炼1.0版本的API和SDK调用。考虑到旧版功能已停止迭代更新，我们强烈建议您升级至最新版API和SDK，具体详情请参考 [新版本升级说明](https://help.aliyun.com/zh/model-studio/new-version-upgrade "")。

## **功能描述**

本文主要介绍如何使用API调用阿里云百炼的第三方模型应用，包括从模型广场中创建的第三方大模型应用（如Llama2-7B、Llama2-13B、ChatGLM2-6B、百川2-7B和姜子牙-13B）。

**说明**

首先，请参考文档 [获取 AccessKey 与 AgentKey](https://help.aliyun.com/zh/model-studio/get-accesskey-appid-and-agentkey "") 获取AK/SK、Agent Key和AppId。如果是RAM账号，请参考文档 [RAM子账号使用方式和授权操作](https://help.aliyun.com/zh/model-studio/use-and-authorize-ram-user "") 进行授权操作。

其次， 调用API需要获取到临时Token，请参照 [创建Token](https://help.aliyun.com/zh/model-studio/create-token-to-generate-api "")。

**重要**

千问-摘要增强版模型应用不支持MaxTokens字段。

## API详情

请求地址： [https://bailian.aliyuncs.com/v2/app/completions](https://bailian.aliyuncs.com/v2/app/completions)

请求方式：POST

请求数据格式：JSON

### **请求参数**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| 参数名 | 参数类型 | 是否必填 | 说明 | 示例值 |
| **请求头** |
| Content-Type | string | 是 | 请求类型 | application/json; charset=utf-8 |
| Accept | string | 否 | 流式响应时，需要携带此请求头，非流式响应不需要携带。 | text/event-stream |
| Authorization | string | 是 | API临时Token。 | Bearer cc\*\*\*\*\*\*\*m3 |
| **请求Body** |
| RequestId | string | 是 | 请求唯一标识，请确保RequestId不重复。 | 30\*\*\*\*\*\*\*\*\*\*869 |
| SessionId | string | 否 | 对话历史的会话唯一标识。传入SessionId后，将在云端记录对话历史，调用大模型将自动携带存储的对话历史。请确保SessionId不重复，并且SessionId和History二选一即可。 | 40\*\*\*\*\*\*\*\*\*\*213 |
| AppId | string | 是 | 阿里云百炼应用唯一标识。 | ea\*\*\*\*\*541 |
| Stream | boolean | 否 | 是否流式输出，默认为否。 | false |
| Prompt | string | 否 | 提示词。 | 中国封建王朝经历多少年？ |
| History |  | 否 | 对话历史。SessionId和History二选一即可，如果同时传入SessionId和History，则只有History会生效。 | \[{"User": "太阳是恒星吗？", "Bot": "是的"}\] |
| History\[x\].User | string | 是 | 对话历史的用户消息。 | 太阳是恒星吗？ |
| History\[x\].Bot | string | 是 | 对话历史大的模型消息。 | 是的 |
| TopP | float | 否 | 生成时，核采样方法的概率阈值。例如，取值为0.8时，仅保留累计概率之和大于等于0.8的概率分布中的token，作为随机采样的候选集。取值范围为（0,1.0)，取值越大，生成的随机性越高；取值越低，生成的随机性越低。默认值为0.8。注意，取值不要大于等于1 | 0.8 |
| Parameters | Parameter | 否 | 模型参数设置。 |  |
| Parameters.TopK | int | 否 | 生成时，采样候选集的大小。例如，取值为50时，仅将单次生成中得分最高的50个token组成随机采样的候选集。取值越大，生成的随机性越高；取值越小，生成的确定性越高。注意：如果top\_k参数为空或者top\_k的值大于100，表示不启用top\_k策略，此时仅有top\_p策略生效，默认是空。 | 50 |
| Parameters.Seed | int | 否 | 生成时使用的随机数种子，用于控制模型生成内容的随机性。seed支持无符号64位整数，默认值为1234。在使用seed时，模型将尽可能生成相同或相似的结果，但目前不保证每次生成的结果完全相同。 | 65535 |
| Parameters.Temperature | float | 否 | 用于控制随机性和多样性的程度。具体来说，temperature值控制了生成文本时对每个候选词的概率分布进行平滑的程度。较高的temperature值会降低概率分布的峰值，使得更多的低概率词被选择，生成结果更加多样化；而较低的temperature值则会增强概率分布的峰值，使得高概率词更容易被选择，生成结果更加确定。<br>取值范围： \[0, 2)，系统默认值1.0。不建议取值为0，无意义。 | 1.0 |\
| Parameters.MaxTokens | int | 否 | 用于限制模型生成token的数量，max\_tokens设置的是生成上限，并不表示一定会生成这么多的token数量。其中qwen-turbo 最大值和默认值为1500， qwen-max、qwen-max-1201 、qwen-max-longcontext 和 qwen-plus最大值和默认值均为2000。 | 1500 |\
| Parameters.Stop | list\[string\] | 否 | stop参数用于实现内容生成过程的精确控制，在生成内容即将包含指定的字符串或token\_ids时自动停止，生成内容不包含指定的内容。<br>例如，如果指定stop为"你好"，表示将要生成"你好"时停止；如果指定stop为\[37763, 367\]，表示将要生成"Observation"时停止。 | \["结束", "停止"\] |\
\
### **响应参数**\
\
|     |     |     |\
| --- | --- | --- |\
| 字段名 | 字段类型 | 说明 |\
| **公共响应参数** |\
| Success | boolean | 是否成功（true: 成功，false: 失败）。 |\
| Code | string | 错误代码。 |\
| Message | string | 错误消息。 |\
| RequestId | string | 请求唯一标识。 |\
| Data | object | 文本生成结果。 |\
| **响应数据** |\
| ResponseId | string | 大模型的responseId。 |\
| SessionId | string | 对话历史的会话唯一标识。 |\
| Text | string | 本次模型调用的输出内容。 |\
| Usage | list | 应用级别的token消耗。 |\
| Usage\[x\].InputTokens | int | 本次请求输入内容的token数。 |\
| Usage\[x\].OutputTokens | int | 本次请求输出内容的token数。 |\
\
## **示例**\
\
### **请求示例**\
\
```shell\
curl -X "POST" "https://bailian.aliyuncs.com/v2/app/completions" \\
-H 'Content-Type: application/json; charset=utf-8' \\
-H 'Authorization: Bearer <token>' \\
-H 'Accept-charset: utf-8' \\
-d '{\
  "RequestId": "<RequestId>",\
  "AppId": "<AppId>",\
  "Prompt": "那边有什么推荐的旅游景点",\
  "History": [\
    {\
      "User": "我想去北京",\
      "Bot": "北京是一个非常值得去的地方"\
    }\
  ]\
}' --verbose\
```\
\
### **响应示例**\
\
```json\
{\
  "Success": true,\
  "Data": {\
    "ResponseId": "3a8a7****************3f455e4eb",\
    "Text": "北京作为中国的首都和历史文化名城，拥有众多知名且具有丰富文化历史底蕴的旅游景点，以及现代化的休闲娱乐场所。以下是一些推荐的旅游景点： 包括城楼、纪念堂、人民英雄纪念碑、国家博物馆等，这里是中华人民共和国的象征。此外，还有许多其他值得游览的地方，如雍和宫、地坛公园、国家大剧院、798艺术区等等，具体可根据个人兴趣和行程安排选择。在计划行程时，也可以参考马蜂窝旅游网或携程旅游攻略提供的最新信息和推荐线路。",\
    "Usage": [\
      {\
        "InputTokens": 15,\
        "OutputTokens": 383,\
        "ModelId": "qwen-plus-v1"\
      }\
    ]\
  },\
  "RequestId": "f0a953cc-*************-f32e606985d7"\
}\
```\
\
### **请求示例（流式SSE）**\
\
```shell\
curl -X "POST" "https://pre-bailian.aliyuncs.com/v2/app/completions" \\
-H 'Content-Type: application/json; charset=utf-8' \\
-H 'Authorization: Bearer <Token>' \\
-H 'Accept: text/event-stream' \\
-H 'Accept-charset: utf-8' \\
-d '{\
  "RequestId": "<RequestId>",\
  "AppId": "<AppId>",\
  "Prompt": "那边有什么推荐的旅游景点",\
  "Stream": true,\
  "History": [\
    {\
      "User": "我想去北京",\
      "Bot": "北京是一个非常值得去的地方"\
    }\
  ]\
}' --verbose\
```\
\
### **响应示例（流式SSE）**\
\
```json\
data: {\
  "Data": {\
    "Success": true,\
    "ResponseId": "568c3a75************c876819e479",\
    "Text": "北京有许多著名的旅游景点，如故宫、长城、颐和园、圆明园等。此外，还有各种特色胡同、小吃和文化遗产，如北京胡同、相声、京剧等。您可以根据自己的兴趣和时间安排游览路线。",\
    "Usage": [\
      {\
        "InputTokens": 45,\
        "OutputTokens": 88,\
        "ModelId": "bailian-summary"\
      }\
    ]\
  },\
  "RequestId": "f0a953cc-***************-f32e606985d7"\
}\
```