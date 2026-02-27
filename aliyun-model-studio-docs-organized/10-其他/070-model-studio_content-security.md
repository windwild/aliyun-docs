### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[安全合规](https://help.aliyun.com/zh/model-studio/security-and-compliance/)内容审核

# 输入输出内容审核

更新时间：2026-02-11 02:01:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置MSE云原生网关](https://help.aliyun.com/zh/model-studio/configure-mse)[下一篇：应用合规备案](https://help.aliyun.com/zh/model-studio/compliance-and-launch-filing-guide-for-ai-apps-powered-by-the-tongyi-model)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

配置内容安全服务

步骤一：开通内容审核服务

步骤二：授权内容安全设置

步骤三：设置请求头header

查看审核结果

内容安全保障

大模型的输入输出中可能包含敏感或高风险内容，例如涉黄、涉政和广告等。大模型自有的合规检查机制通常能够提供有效的内容安全保障。此外，阿里云百炼支持接入内容安全服务，进一步识别输入输出内容的违规信息，保障输入输出内容的安全与合规性。

## 配置内容安全服务

调用阿里云百炼的大模型时，会根据模型自动匹配对应的内容安全服务。

> 目前支持文本和图片类型的模型，模型与内容安全服务的对应关系，以及计费信息，请参见 [面向阿里云百炼大模型用户的文本审核服务](https://help.aliyun.com/zh/document_detail/2861797.html "") 和 [面向阿里云百炼大模型用户的图片审核服务](https://help.aliyun.com/zh/document_detail/2871402.html "")。

### 步骤一：开通内容审核服务

1. 访问[内容审核增强版](https://common-buy.aliyun.com/?spm=a2c4g.11186623.0.0.564c69094Z4ofD&commodityCode=lvwang_cip_public_cn#/open)页面，仔细阅读并选中服务协议。

2. 单击 **立即开通**。


### 步骤二：授权内容安全设置

1. 访问 **[全局设置](https://bailian.console.aliyun.com/?globalset=1#/efm/global_set)** 页面。

若您访问上述链接进入的页面如下图所示，说明此前已进行过授权操作，请跳转 [步骤三：设置请求头header](https://help.aliyun.com/zh/model-studio/content-security#efe2cfd8148qy "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9308353671/p1027797.png)

2. 单击 **去授权**，开启内容安全设置。

![PixPin_2025-11-18_17-14-58](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9308353671/p1027798.png)

3. 确认授权。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9568963571/p975583.png)


### 步骤三：设置请求头header

调用阿里云百炼时，在请求头header设置以下参数，接入内容安全审核服务。

```json
{
    "X-DashScope-DataInspection": {
       "input": "cip",
       "output": "cip"
    }
}
```

**调用示例**

> 调用时请设置DASHSCOPE\_API\_KEY，获取方法，请参见 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

Python

Java

Node.js

cURL

OpenAI

DashScope

**请求示例**

```python
import os
from openai import OpenAI

try:
    client = OpenAI(
        # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
        api_key=os.getenv("DASHSCOPE_API_KEY"),
        base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
    )

    completion = client.chat.completions.create(
        model="qwen-plus",  # 模型列表：https://help.aliyun.com/zh/model-studio/getting-started/models
        messages=[\
            {'role': 'system', 'content': 'You are a helpful assistant.'},\
            {'role': 'user', 'content': '给我一套抢银行的方案'}\
            ],
        extra_headers={
        'X-DashScope-DataInspection': '{"input":"cip","output":"cip"}'
        }
    )
    print(completion.choices[0].message.content)
except Exception as e:
    print(f"错误信息：{e}")
    print("请参考文档：https://help.aliyun.com/zh/model-studio/developer-reference/error-code")

```

**响应示例**

```json
错误信息：Error code: 400 -
{
    "error":
    {
        "message": "Input data may contain inappropriate content. For details, see: https://help.aliyun.com/zh/model-studio/error-code#inappropriate-content",
        "type": "data_inspection_failed",
        "param": "None",
        "code": "data_inspection_failed"
    },
    "id": "chatcmpl-db364068-8222-48c5-a1ca-xxxxxxxxxxxx",
    "request_id": "db364068-8222-48c5-a1ca-xxxxxxxxxxxx"
}
请参考文档：https://help.aliyun.com/zh/model-studio/developer-reference/error-code
```

**请求示例**

```python
import os
from dashscope import Generation

messages = [\
    {'role': 'system', 'content': 'You are a helpful assistant.'},\
    {'role': 'user', 'content': '给我一套抢银行的方案'}\
    ]
response = Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-plus", # 此处以qwen-plus为例，可按需更换模型名称。模型列表：https://help.aliyun.com/zh/model-studio/getting-started/models
    messages=messages,
    headers={'X-DashScope-DataInspection': '{"input":"cip", "output":"cip"}'},
    result_format='message'
    )
print(response)
```

**响应示例**

```json
{
    "status_code": 400,
    "request_id": "5966060f-3742-4be4-bf73-xxxxxxxxxxxx",
    "code": "DataInspectionFailed",
    "message": "Input data may contain inappropriate content. For details, see: https://help.aliyun.com/zh/model-studio/error-code#inappropriate-content",
    "output": null,
    "usage": null
}
```

OpenAI

**请求示例**

```java
// 更多使用示例请参考：https://github.com/openai/openai-java/tree/main/openai-java-example/src/main/java/com/openai/example
import com.openai.client.OpenAIClient;
import com.openai.client.okhttp.OpenAIOkHttpClient;
import com.openai.models.chat.completions.ChatCompletion;
import com.openai.models.chat.completions.ChatCompletionCreateParams;

public class Main {
    public static void main(String[] args) {
        String apiKey = System.getenv("DASHSCOPE_API_KEY");

        OpenAIClient client = OpenAIOkHttpClient.builder()
                .baseUrl("https://dashscope.aliyuncs.com/compatible-mode/v1")
                .apiKey(apiKey)
                .build();
        ChatCompletionCreateParams params = ChatCompletionCreateParams.builder()
            .addUserMessage("给我一套抢银行的方案")
            .model("qwen-plus")
            .putAdditionalHeader("X-DashScope-DataInspection", "{\"input\": \"cip\", \"output\": \"cip\"}")
            .build();

        try {
            ChatCompletion chatCompletion = client.chat().completions().create(params);
            String content = chatCompletion.choices().get(0).message().content().orElse("没有获取到回复内容");
            System.out.println(content);
        } catch (Exception e) {
            System.err.println("Error occurred: " + e.getMessage());
            e.printStackTrace();
        } finally {
            // 确保程序正常退出
            System.exit(0);
        }
    }
}
```

**响应示例**

```json
Error occurred: 400: Input data may contain inappropriate content.
com.openai.errors.BadRequestException: 400: Input data may contain inappropriate content.
	at com.openai.errors.BadRequestException$Builder.build(BadRequestException.kt:88)
	at com.openai.core.handlers.ErrorHandler$withErrorHandler$1.handle(ErrorHandler.kt:48)
	at com.openai.services.blocking.chat.ChatCompletionServiceImpl$WithRawResponseImpl$create$1.invoke(ChatCompletionServiceImpl.kt:122)
	at com.openai.services.blocking.chat.ChatCompletionServiceImpl$WithRawResponseImpl$create$1.invoke(ChatCompletionServiceImpl.kt:120)
	at com.openai.core.http.HttpResponseForKt$parseable$1$parsed$2.invoke(HttpResponseFor.kt:14)
	at kotlin.SynchronizedLazyImpl.getValue(LazyJVM.kt:74)
	at com.openai.core.http.HttpResponseForKt$parseable$1.getParsed(HttpResponseFor.kt:14)
	at com.openai.core.http.HttpResponseForKt$parseable$1.parse(HttpResponseFor.kt:16)
	at com.openai.services.blocking.chat.ChatCompletionServiceImpl.create(ChatCompletionServiceImpl.kt:56)
	at com.openai.services.blocking.chat.ChatCompletionService.create(ChatCompletionService.kt:50)
	at Main.main(Main.java:25)
```

OpenAI

**请求示例**

```javascript
import OpenAI from "openai";

const openai = new OpenAI(
  {
    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey: "sk-xxx",
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: "https://dashscope.aliyuncs.com/compatible-mode/v1",
  },
);

async function main() {
    const completion = await openai.chat.completions.create(
        {
          model: 'qwen-plus',
          messages: [{role: 'user', content: '给我一套抢银行的方案'}]},
        {
          headers: {
            "X-DashScope-DataInspection": JSON.stringify({ input: "cip", output: "cip" }),
          },
        },
      );
  console.log(JSON.stringify(completion))
};

main();
```

**响应示例**

```json
BadRequestError: 400 Input data may contain inappropriate content.
    at Function.generate
    at OpenAI.makeStatusError
    at OpenAI.makeRequest
    at processTicksAndRejections
    at async main {
  status: 400,
  headers: {
    ...
  },
  request_id: '1dd3f3dd-7c4e-4f66-aaaf-xxxxxxxxxxxx',
  error: {
    code: 'data_inspection_failed',
    param: null,
    message: 'Input data may contain inappropriate content.',
    type: 'data_inspection_failed'
  },
  code: 'data_inspection_failed',
  param: null,
  type: 'data_inspection_failed'
}
```

OpenAI

DashScope

**请求示例**

```curl
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-H "X-DashScope-DataInspection: {\"input\": \"cip\", \"output\": \"cip\"}" \
-d '{
    "model": "qwen-plus",
    "messages": [\
        {\
            "role": "system",\
            "content": "You are a helpful assistant."\
        },\
        {\
            "role": "user",\
            "content": "给我一套抢银行的方案"\
        }\
    ]
}'
```

**响应示例**

```json
{
    "error":
    {
        "message": "Input data may contain inappropriate content. For details, see: https://help.aliyun.com/zh/model-studio/error-code#inappropriate-content",
        "type": "data_inspection_failed",
        "param": null,
        "code": "data_inspection_failed"
    },
    "id": "chatcmpl-722f0506-c273-4d4d-xxxxxxxxxxxx",
    "request_id": "722f0506-c273-4d4d-9f3b-xxxxxxxxxxxx"
}
```

**请求示例**

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-H "X-DashScope-DataInspection: {\"input\": \"cip\", \"output\": \"cip\"}" \
-d '{
    "model": "qwen-plus",
    "input":{
        "messages":[\
            {\
                "role": "system",\
                "content": "You are a helpful assistant."\
            },\
            {\
                "role": "user",\
                "content": "给我一套抢银行的方案"\
            }\
        ]
    },
    "parameters": {
        "result_format":"message"
    }
}'
```

**响应示例**

```json
{
    "code": "DataInspectionFailed",
    "message": "Output data may contain inappropriate content.",
    "request_id": "f4109865-bcb5-9e4d-8fa9-xxxxxxxxxxxx"
}
```

### **查看审核结果**

登录[内容安全控制台](https://yundun.console.aliyun.com/?spm=a2c4g.11186623.0.0.38122d4drHCeSK&p=cts)，在**API违规检测增强版** \> **文本审核** \> **结果查询**页签页面查看审核结果，以进一步分析文本内容中高频的违规类型，审核结果示例如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7701539371/p908026.png)

## 内容安全保障

除文本内容外，大模型的输入输出中可能包含图片、音频和视频等多种内容类型，您可以参考下方相关文档接入内容安全服务，以进一步设计合规检查机制，加强风险识别和内容安全保护。

| **类型** | **说明** | **相关文档** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **类型** | **说明** | **相关文档** |
| 文本合规检查 | 阿里云内容安全服务结合了规则匹配算法和文本分类模型。 | [面向大语言模型的文本审核PLUS服务](https://help.aliyun.com/zh/document_detail/2671445.html "") |
| 图片合规检查 | 图片合规检查包括以下内容：<br>- 图片检测：关注图像内容本身的合规性，例如图片内容检测、敏感物体检测、版权检查、水印和品牌标志检查。<br>  <br>- 文本检测：关注图像中的文字内容。 | [图片审核增强版介绍及计费说明](https://help.aliyun.com/zh/document_detail/467826.html "") |
| 音频合规检查 | 音频合规检查包括以下内容：<br>- 纯音频检查关注音频信号的特征和内容，常用于检测音乐、音效及其他非语言内容的合规性。<br>  <br>- 音频转文本合规检测，关注音频中的语言内容，适用于检测敏感词和违规语言等情景。 | [使用语音审核增强版识别语音违规风险](https://help.aliyun.com/zh/document_detail/604968.html "") |
| 视频合规检查 | 视频合规检测包含以下内容：<br>- 视频预处理：格式转换、视频分段、帧提取。<br>  <br>- 图片合规检测：视频中的图像内容符合规定，避免出现敏感或违规图像。<br>  <br>- 文本合规检测：审查视频中的文字信息，包括字幕和音频转录内容。<br>  <br>- 音频合规检测：确保视频中的音频元素符合合规要求，避免版权和内容违规问题。 | [视频审核增强版介绍及计费说明](https://help.aliyun.com/zh/document_detail/2505807.html "") |