### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[对话](https://help.aliyun.com/zh/model-studio/chat/)DeepSeek-阿里云

# DeepSeek大语言模型

更新时间：2026-02-12 10:16:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DashScope](https://help.aliyun.com/zh/model-studio/qwen-api-via-dashscope)[下一篇：DeepSeek-硅基流动](https://help.aliyun.com/zh/model-studio/siliconflow-deepseek-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型列表

快速开始

其它功能

参数默认值

计费说明

常见问题

免费额度用完后如何购买 Token？

如何接入Chatbox、Cherry Studio或Dify？

可以上传图片或文档进行提问吗？

如何查看Token消耗量及调用次数？

还有哪些使用DeepSeek的方式？

错误码

本文档介绍如何在阿里云百炼平台通过OpenAI兼容接口或DashScope SDK调用DeepSeek系列模型。

**重要**

本文档仅适用于中国大陆版（北京地域）。

## **模型列表**

- 混合思考模型（通过`enable_thinking`参数控制是否思考）：deepseek-v3.2、deepseek-v3.2-exp、deepseek-v3.1

- 仅思考模型（回复前总会思考）：deepseek-r1、deepseek-r1-0528

- 非思考模型：deepseek-v3


deepseek-v3.2 是 DeepSeek 的最新模型，在代码和数学等任务上表现优异，且价格最低， [限流](https://help.aliyun.com/zh/model-studio/rate-limit "") 条件宽松，推荐优先使用。

| **模型名称** | **上下文长度** | **最大输入** | **最大思维链长度** | **最大回复长度** |
| --- | --- | --- | --- | --- |
| **（Token数）** |
| --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型名称** | **上下文长度** | **最大输入** | **最大思维链长度** | **最大回复长度** |
| **（Token数）** |
| deepseek-v3.2<br>> 685B 满血版 | 131,072 | 98,304 | 32,768 | 65,536 |
| deepseek-v3.2-exp<br>> 685B 满血版 |
| deepseek-v3.1<br>> 685B 满血版 |
| deepseek-r1<br>> 685B 满血版 | 16,384 |
| deepseek-r1-0528<br>> 685B 满血版 |
| deepseek-v3<br>> 671B 满血版 | 131,072 | - |

**蒸馏模型**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型名称** | **上下文长度** | **最大输入** | **最大思维链长度** | **最大回复长度** |
| **（Token数）** |
| deepseek-r1-distill-qwen-1.5b<br>> 基于 Qwen2.5-Math-1.5B | 32,768 | 32,768 | 16,384 | 16,384 |
| deepseek-r1-distill-qwen-7b<br>> 基于 Qwen2.5-Math-7B |
| deepseek-r1-distill-qwen-14b<br>> 基于 Qwen2.5-14B |
| deepseek-r1-distill-qwen-32b<br>> 基于 Qwen2.5-32B |
| deepseek-r1-distill-llama-8b<br>> 基于 Llama-3.1-8B |
| deepseek-r1-distill-llama-70b<br>> 基于 Llama-3.3-70B |

> 最大思维链长度是模型在思考模式下，思考过程的最大 Token 数量。

> 以上模型非集成第三方服务，均部署在阿里云百炼服务器上。

> 并发限流请参考 [DeepSeek 限流条件](https://help.aliyun.com/zh/model-studio/rate-limit#f5d967328bgje "")。

## **快速开始**

deepseek-v3.2 是 DeepSeek 系列最新模型，支持通过`enable_thinking`参数设置思考与非思考模式。运行以下代码快速调用思考模式的 deepseek-v3.2 模型。

需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并完成 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。如果通过SDK调用，需要 [安装 OpenAI 或 DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk#8833b9274f4v8 "")。

OpenAI兼容

DashScope

**说明**

`enable_thinking`非 OpenAI 标准参数，OpenAI Python SDK 通过 `extra_body`传入，Node.js SDK 作为顶层参数传入。

Python

Node.js

HTTP

### **示例代码**

```python
from openai import OpenAI
import os

# 初始化OpenAI客户端
client = OpenAI(
    # 如果没有配置环境变量，请用阿里云百炼API Key替换：api_key="sk-xxx"
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)

messages = [{"role": "user", "content": "你是谁"}]
completion = client.chat.completions.create(
    model="deepseek-v3.2",
    messages=messages,
    # 通过 extra_body 设置 enable_thinking 开启思考模式
    extra_body={"enable_thinking": True},
    stream=True,
    stream_options={
        "include_usage": True
    },
)

reasoning_content = ""  # 完整思考过程
answer_content = ""  # 完整回复
is_answering = False  # 是否进入回复阶段
print("\n" + "=" * 20 + "思考过程" + "=" * 20 + "\n")

for chunk in completion:
    if not chunk.choices:
        print("\n" + "=" * 20 + "Token 消耗" + "=" * 20 + "\n")
        print(chunk.usage)
        continue

    delta = chunk.choices[0].delta

    # 只收集思考内容
    if hasattr(delta, "reasoning_content") and delta.reasoning_content is not None:
        if not is_answering:
            print(delta.reasoning_content, end="", flush=True)
        reasoning_content += delta.reasoning_content

    # 收到content，开始进行回复
    if hasattr(delta, "content") and delta.content:
        if not is_answering:
            print("\n" + "=" * 20 + "完整回复" + "=" * 20 + "\n")
            is_answering = True
        print(delta.content, end="", flush=True)
        answer_content += delta.content
```

### **返回结果**

```plaintext
====================思考过程====================

啊，用户问我是谁。这是很常见的开场问题，需要简单清晰地介绍自己的身份和功能。可以用公司背景和核心能力作为开头，让用户快速建立认知。
想到要突出免费属性和文本特长，但避免过度展开细节。最后用开放性问题引导对话继续，符合助手的服务性质。
考虑用企业级AI助手作为定位描述，既专业又亲切。括号里的表情符号可以适当增加亲和力。
====================完整回复====================

你好！我是DeepSeek，由深度求索公司创造的AI助手。

我是一个纯文本模型，虽然不支持多模态识别功能，但我有文件上传功能，可以帮你处理图像、txt、pdf、ppt、word、excel等各种文件，从中读取文字信息来协助你。我完全免费使用，拥有128K的上下文长度，还支持联网搜索功能（需要你在Web/App中手动开启）。

我的知识截止到2024年7月，我会用热情细腻的方式为你提供帮助。你可以通过官方应用商店下载App来使用我。

有什么问题我可以帮你解答吗？无论是学习、工作还是生活上的疑问，我都很乐意协助你！✨
====================Token 消耗====================

CompletionUsage(completion_tokens=238, prompt_tokens=5, total_tokens=243, completion_tokens_details=CompletionTokensDetails(accepted_prediction_tokens=None, audio_tokens=None, reasoning_tokens=93, rejected_prediction_tokens=None), prompt_tokens_details=None)
```

### **示例代码**

```nodejs
import OpenAI from "openai";
import process from 'process';

// 初始化OpenAI客户端
const openai = new OpenAI({
    // 如果没有配置环境变量，请用阿里云百炼API Key替换：apiKey: "sk-xxx"
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: 'https://dashscope.aliyuncs.com/compatible-mode/v1'
});

let reasoningContent = ''; // 完整思考过程
let answerContent = ''; // 完整回复
let isAnswering = false; // 是否进入回复阶段

async function main() {
    try {
        const messages = [{ role: 'user', content: '你是谁' }];

        const stream = await openai.chat.completions.create({
            model: 'deepseek-v3.2',
            messages,
            // 注意：在 Node.js SDK，enable_thinking 这样的非标准参数作为顶层属性传递，无需放在 extra_body 中
            enable_thinking: true,
            stream: true,
            stream_options: {
                include_usage: true
            },
        });

        console.log('\n' + '='.repeat(20) + '思考过程' + '='.repeat(20) + '\n');

        for await (const chunk of stream) {
            if (!chunk.choices?.length) {
                console.log('\n' + '='.repeat(20) + 'Token 消耗' + '='.repeat(20) + '\n');
                console.log(chunk.usage);
                continue;
            }

            const delta = chunk.choices[0].delta;

            // 只收集思考内容
            if (delta.reasoning_content !== undefined && delta.reasoning_content !== null) {
                if (!isAnswering) {
                    process.stdout.write(delta.reasoning_content);
                }
                reasoningContent += delta.reasoning_content;
            }

            // 收到content，开始进行回复
            if (delta.content !== undefined && delta.content) {
                if (!isAnswering) {
                    console.log('\n' + '='.repeat(20) + '完整回复' + '='.repeat(20) + '\n');
                    isAnswering = true;
                }
                process.stdout.write(delta.content);
                answerContent += delta.content;
            }
        }
    } catch (error) {
        console.error('Error:', error);
    }
}

main();
```

### **返回结果**

```plaintext
====================思考过程====================

啊，用户问我是谁，这是很常见的开场问题。需要简单清晰地介绍自己的身份和核心功能，避免过度展开。

可以用公司背景和基本定位作为开头，再列举几个关键能力让用户快速了解我能做什么。最后用开放性问题结束，方便用户继续提问。

想到要突出免费、长上下文和文件处理这些实用特点，语气保持友好但克制，不用表情符号。
====================完整回复====================

你好！我是DeepSeek，由深度求索公司创造的AI助手。

我是一个纯文本模型，拥有128K的上下文处理能力，可以帮你解答各种问题、进行对话交流、协助处理文本任务等。虽然我不支持多模态识别功能，但我可以处理你上传的图像、txt、pdf、ppt、word、excel等文件，从中读取文字信息来帮助你。

我完全免费使用，没有语音功能，但你可以通过官方应用商店下载App来使用我。如果需要联网搜索，记得在Web或App中手动点开联网搜索按键哦。

我的知识截止到2024年7月，会以热情细腻的方式为你提供帮助。有什么问题或需要协助的地方，尽管告诉我吧！我很乐意为你服务。✨
====================Token 消耗====================

{
  prompt_tokens: 5,
  completion_tokens: 243,
  total_tokens: 248,
  completion_tokens_details: { reasoning_tokens: 83 }
}
```

### **示例代码**

curl

```curl
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "deepseek-v3.2",
    "messages": [\
        {\
            "role": "user",\
            "content": "你是谁"\
        }\
    ],
    "stream": true,
    "stream_options": {
        "include_usage": true
    },
    "enable_thinking": true
}'
```

Python

Java

HTTP

### **示例代码**

```python
import os
from dashscope import Generation

# 初始化请求参数
messages = [{"role": "user", "content": "你是谁？"}]

completion = Generation.call(
    # 如果没有配置环境变量，请用阿里云百炼API Key替换：api_key="sk-xxx"
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    model="deepseek-v3.2",
    messages=messages,
    result_format="message",  # 设置结果格式为 message
    enable_thinking=True,
    stream=True,              # 开启流式输出
    incremental_output=True,  # 开启增量输出
)

reasoning_content = ""  # 完整思考过程
answer_content = ""     # 完整回复
is_answering = False    # 是否进入回复阶段

print("\n" + "=" * 20 + "思考过程" + "=" * 20 + "\n")

for chunk in completion:
    message = chunk.output.choices[0].message
    # 只收集思考内容
    if "reasoning_content" in message:
        if not is_answering:
            print(message.reasoning_content, end="", flush=True)
        reasoning_content += message.reasoning_content

    # 收到 content，开始进行回复
    if message.content:
        if not is_answering:
            print("\n" + "=" * 20 + "完整回复" + "=" * 20 + "\n")
            is_answering = True
        print(message.content, end="", flush=True)
        answer_content += message.content

print("\n" + "=" * 20 + "Token 消耗" + "=" * 20 + "\n")
print(chunk.usage)
```

### **返回结果**

```plaintext
====================思考过程====================

哦，用户问我是谁，这是一个很基础的自我介绍问题。需要简洁清晰地说明身份和功能，避免复杂化。可以用公司背景和核心能力作为开头，让用户快速建立认知。
考虑到用户可能是初次接触，可以补充一些典型使用场景和特点，比如免费、长上下文、文件处理等实用信息。结尾加上开放式的帮助邀请，保持友好态度。
不需要过多技术细节，重点突出易用性和实用性。
====================完整回复====================

你好！我是DeepSeek，由深度求索公司创造的AI助手.

我是一个纯文本模型，虽然不支持多模态识别功能，但我有文件上传功能，可以帮你处理图像、txt、pdf、ppt、word、excel等文件，读取其中的文字信息进行分析处理。我完全免费使用，拥有128K的上下文处理能力，还支持联网搜索功能（需要你手动点开联网搜索按键）。

我的知识截止到2024年7月，会以热情细腻的方式为你提供帮助。你可以通过官方应用商店下载我的App来使用我。

有什么问题或者需要帮助的地方，尽管问我吧！我很乐意为你解答各种疑问，协助你处理各种任务。✨
====================Token 消耗====================

{"input_tokens": 6, "output_tokens": 240, "total_tokens": 246, "output_tokens_details": {"reasoning_tokens": 92}}
```

### **示例代码**

**重要**

DashScope Java SDK 版本需要不低于2.19.4。

```java
// dashscope SDK的版本 >= 2.19.4
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import io.reactivex.Flowable;
import java.lang.System;
import java.util.Arrays;

public class Main {
    private static StringBuilder reasoningContent = new StringBuilder();
    private static StringBuilder finalContent = new StringBuilder();
    private static boolean isFirstPrint = true;
    private static void handleGenerationResult(GenerationResult message) {
        String reasoning = message.getOutput().getChoices().get(0).getMessage().getReasoningContent();
        String content = message.getOutput().getChoices().get(0).getMessage().getContent();
        if (reasoning != null && !reasoning.isEmpty()) {
            reasoningContent.append(reasoning);
            if (isFirstPrint) {
                System.out.println("====================思考过程====================");
                isFirstPrint = false;
            }
            System.out.print(reasoning);
        }
        if (content != null && !content.isEmpty()) {
            finalContent.append(content);
            if (!isFirstPrint) {
                System.out.println("\n====================完整回复====================");
                isFirstPrint = true;
            }
            System.out.print(content);
        }
    }
    private static GenerationParam buildGenerationParam(Message userMsg) {
        return GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("deepseek-v3.2")
                .enableThinking(true)
                .incrementalOutput(true)
                .resultFormat("message")
                .messages(Arrays.asList(userMsg))
                .build();
    }
    public static void streamCallWithMessage(Generation gen, Message userMsg)
            throws NoApiKeyException, ApiException, InputRequiredException {
        GenerationParam param = buildGenerationParam(userMsg);
        Flowable<GenerationResult> result = gen.streamCall(param);
        result.blockingForEach(message -> handleGenerationResult(message));
    }
    public static void main(String[] args) {
        try {
            Generation gen = new Generation();
            Message userMsg = Message.builder().role(Role.USER.getValue()).content("你是谁？").build();
            streamCallWithMessage(gen, userMsg);
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.err.println("An exception occurred: " + e.getMessage());
        }
    }
}
```

### **返回结果**

```plaintext
====================思考过程====================

唔，用户问了一个简单的自我介绍问题。这种问题很常见，需要快速清晰地表明身份和功能。考虑用轻松友好的语气介绍自己是DeepSeek-V3，并说明由深度求索公司创造。可以加上能提供的帮助类型，比如解答问题、聊天、学习辅导等，最后用表情符号增加亲和力。不需要过多解释，保持简洁明了就好。
====================完整回复====================

DeepSeek-V3，一个由深度求索公司创造的智能助手！我可以帮助你解答各种问题、提供建议、进行知识查询，甚至陪你聊天！无论是学习、工作还是日常生活中的疑问，尽管问我吧~有什么我可以帮你的吗？
```

### **示例代码**

curl

```curl
curl -X POST "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-H "X-DashScope-SSE: enable" \
-d '{
    "model": "deepseek-v3.2",
    "input":{
        "messages":[\
            {\
                "role": "user",\
                "content": "你是谁？"\
            }\
        ]
    },
    "parameters":{
        "enable_thinking": true,
        "incremental_output": true,
        "result_format": "message"
    }
}'
```

## **其它功能**

| **模型** | [多轮对话](https://help.aliyun.com/zh/model-studio/multi-round-conversation "") | [Function Calling](https://help.aliyun.com/zh/model-studio/qwen-function-calling#dd5a3dca390k9 "") | [联网搜索](https://help.aliyun.com/zh/model-studio/web-search "") | [上下文缓存](https://help.aliyun.com/zh/model-studio/context-cache "") | [结构化输出](https://help.aliyun.com/zh/model-studio/qwen-structured-output "") | [前缀续写](https://help.aliyun.com/zh/model-studio/partial-mode "") |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型** | [多轮对话](https://help.aliyun.com/zh/model-studio/multi-round-conversation "") | [Function Calling](https://help.aliyun.com/zh/model-studio/qwen-function-calling#dd5a3dca390k9 "") | [联网搜索](https://help.aliyun.com/zh/model-studio/web-search "") | [上下文缓存](https://help.aliyun.com/zh/model-studio/context-cache "") | [结构化输出](https://help.aliyun.com/zh/model-studio/qwen-structured-output "") | [前缀续写](https://help.aliyun.com/zh/model-studio/partial-mode "") |
| deepseek-v3.2 | 支持 | 支持 | 支持 | 支持 | 不支持 | 不支持 |
| deepseek-v3.2-exp | 支持 | 支持<br>> 仅支持非思考模式。 | 支持 | 不支持 | 不支持 | 不支持 |
| deepseek-v3.1 | 支持 | 支持<br>> 仅支持非思考模式。 | 支持 | 不支持 | 不支持 | 不支持 |
| deepseek-r1 | 支持 | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| deepseek-r1-0528 | 支持 | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| deepseek-v3 | 支持 | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 蒸馏模型 | 支持 | 不支持 | 不支持 | 不支持 | 不支持 | 不支持 |

## **参数默认值**

| **模型** | **temperature** | **top\_p** | **repetition\_penalty** | **presence\_penalty** | **max\_tokens** | **thinking\_budget** |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型** | **temperature** | **top\_p** | **repetition\_penalty** | **presence\_penalty** | **max\_tokens** | **thinking\_budget** |
| deepseek-v3.2 | 1.0 | 0.95 | - | - | 65,536 | 32,768 |
| deepseek-v3.2-exp | 0.6 | 0.95 | 1.0 | - | 65,536 | 32,768 |
| deepseek-v3.1 | 0.6 | 0.95 | 1.0 | - | 65,536 | 32,768 |
| deepseek-r1 | 0.6 | 0.95 | - | 1 | 16,384 | 32,768 |
| deepseek-r1-0528 | 0.6 | 0.95 | - | 1 | 16,384 | 32,768 |
| 蒸馏版 | 0.6 | 0.95 | - | 1 | 16,384 | 16,384 |
| deepseek-v3 | 0.7 | 0.6 | - | - | 16,384 | - |

- “-” 表示没有默认值，也不支持设置。

- deepseek-r1、deepseek-r1-0528、蒸馏版模型不支持设置以上参数值。

- 参数含义请参考 [OpenAI Chat](https://help.aliyun.com/zh/model-studio/qwen-api-via-openai-chat-completions "")。


## **计费说明**

按照模型的输入与输出 Token 计费，价格详情请参考[模型列表与价格](https://help.aliyun.com/zh/model-studio/models#935bd5ba5cg5d "")。

> 思考模式下，思维链按照输出 Token 计费。

## **常见问题**

### [**免费额度**](https://bailian.console.aliyun.com/\#/model-market/detail/deepseek-r1) **用完后如何购买 Token？**

访问 [费用与成本](https://usercenter2.aliyun.com/home) 中心进行充值，确保您的账户没有欠费即可调用 DeepSeek 模型。

> 调用 DeepSeek 模型会自动扣费，出账周期为一小时，消费明细请前往 **[账单详情](https://billing-cost.console.aliyun.com/finance/expense-report/expense-detail-by-instance)** 进行查看。

### **如何接入** [**Chatbox**](https://chatboxai.app/zh) **、** [**Cherry Studio**](https://cherry-ai.com/) **或** [Dify](https://cloud.dify.ai/apps) **？**

此处以使用较多的工具为例，其它大模型工具接入的方法较为类似。

Chatbox

Cherry Studio

Dify

请参见 [Chatbox](https://help.aliyun.com/zh/model-studio/chatbox "")。

请参见 [Cherry Studio](https://help.aliyun.com/zh/model-studio/cherry-studio "")。

请参见 [Dify](https://help.aliyun.com/zh/model-studio/dify "")。

### 可以上传图片或文档进行提问吗 **？**

DeepSeek 模型仅支持文本输入，不支持输入图片或文档。 [千问VL](https://help.aliyun.com/zh/model-studio/vision "") 模型支持图片输入， [Qwen-Long](https://help.aliyun.com/zh/model-studio/long-context-qwen-long "") 模型支持文档输入。

### **如何查看Token** 消耗 **量** 及 **调用次数？**

模型调用完 **一小时后**，在[模型观测](https://bailian.console.aliyun.com/?tab=model#/model-telemetry)页面设置查询条件（例如，选择时间范围、业务空间等），再在 **模型列表** 区域找到目标模型并单击 **操作** 列的 **监控**，即可查看该模型的调用统计结果。具体请参见 [模型监控](https://help.aliyun.com/zh/model-studio/model-telemetry/ "") 文档。

> 数据按小时更新，高峰期可能有小时级延迟，请您耐心等待。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8923304571/p992752.png)

### **还有哪些使用DeepSeek的方式？**

在百炼平台使用DeepSeek有三种方式：

1. 在线体验：访问 [模型广场](https://bailian.console.aliyun.com/#/model-market)。

2. 通过API或客户端（如Chatbox）调用模型：请参考本文内容。

3. 0代码构建大模型应用：请参考 [智能体应用](https://help.aliyun.com/zh/model-studio/single-agent-application "") 或 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "")。


除此之外，如需自行部署DeepSeek然后再调用，请参考 [技术解决方案](https://www.aliyun.com/solution/tech-solution/deepseek-r1-for-platforms)。

## **错误码**

如果执行报错，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。