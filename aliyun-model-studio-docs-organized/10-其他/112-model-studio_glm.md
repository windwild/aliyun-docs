### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[对话](https://help.aliyun.com/zh/model-studio/chat/)GLM

# GLM

更新时间：2026-02-25 20:49:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Kimi-月之暗面](https://help.aliyun.com/zh/model-studio/kimi-api-by-moonshot-ai)[下一篇：MiniMax-阿里云](https://help.aliyun.com/zh/model-studio/minimax-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型列表

快速开始

模型功能

参数默认值

计费说明

常见问题

Q：如何配置 Dify？

错误码

本文介绍了在阿里云百炼平台通过API调用 GLM 系列模型的方法。每个模型各有100万免费Token。

## **模型列表**

GLM 系列模型是智谱AI专为智能体设计的混合推理模型，提供思考与非思考两种模式。

| **模型名称** | **上下文长度** | **最大输入** | **最大思维链长度** | **最大回复长度** |
| --- | --- | --- | --- | --- |
| **（Token数）** |
| --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型名称** | **上下文长度** | **最大输入** | **最大思维链长度** | **最大回复长度** |
| **（Token数）** |
| glm-5 | 202,752 | 202,752 | 32,768 | 16,384 |
| glm-4.7 | 169,984 |
| glm-4.6 |
| glm-4.5 | 131,072 | 98,304 |
| glm-4.5-air |

> 以上模型非集成第三方服务，均部署在阿里云百炼服务器上。

## **快速开始**

glm-5 是 GLM 系列最新模型，支持通过`enable_thinking`参数设置思考与非思考模式。运行以下代码快速调用思考模式的 glm-5 模型。

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
    model="glm-5",
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

让我仔细思考用户提出的这个看似简单但实际上很有深度的问题。

从语言特点来看，用户使用的是中文，这意味着我应该用中文来回应。这是一个最基础的自我介绍问题，但背后可能包含着多层次的含义。

首先需要明确的是，作为一个语言模型，我应该诚实地说明自己的身份和本质。我既不是人类，也不具备真正的情感意识，而是一个由深度学习技术训练的AI助手。这是最基本的事实。

其次，考虑到用户可能的需求场景，他们或许想了解：
1. 我能提供什么样的服务
2. 我的专业领域是什么
3. 我的局限性在哪里
4. 如何与我更好地互动

在回答中，我应该既表达友好和开放的态度，又保持专业和准确。要说明自己擅长的主要领域，比如知识问答、写作辅助、创意支持等，但同时也要坦诚地指出自己的局限性，比如缺乏真实的情感体验。

此外，为了让回答更加完整，我还应该表达出愿意帮助用户解决问题的积极态度。可以适当引导用户提出更具体的问题，这样可以更好地展现自己的能力。

考虑到这是一个开放式的开场白，回答时既要简洁明了，又要包含足够的信息量，让用户对我的基本情况有一个清晰的认识，同时为后续的对话奠定良好的基础。

最后，语气应该保持谦逊和专业，既不过于技术化，也不显得过分随意，让用户感到舒适和自然。
====================完整回复====================

我是智谱AI训练的GLM大语言模型，旨在为用户提供信息和帮助解决问题。我被设计用来理解和生成人类语言，可以回答问题、提供解释或参与各类话题讨论。

我不会存储您的个人数据，我们的对话是匿名的。有什么我能帮您了解或探讨的话题吗？
====================Token 消耗====================

CompletionUsage(completion_tokens=344, prompt_tokens=7, total_tokens=351, completion_tokens_details=None, prompt_tokens_details=None)
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
            model: 'glm-5',
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

让我仔细思考用户的问题"你是谁"。这需要从多个角度来分析和回应。

首先，这是一个基础的身份认知问题。作为GLM大语言模型，需要准确表达自己的身份定位。应该清晰地说明自己是由智谱AI开发的AI助手。

其次，思考用户提出这个问题的可能意图。他们可能是初次接触，想了解基本功能；也可能想确认是否能提供特定帮助；或者只是想测试回应方式。因此需要给出一个开放且友好的回答。

还要考虑回答的完整性。除了身份介绍，也应该简要说明主要功能，如问答、创作、分析等，让用户了解可以如何使用这个助手。

最后，要确保语气友好亲和，表达出乐于帮助的态度。可以用"很高兴为您服务"这样的表达，让用户感受到交流的温暖。

基于这些思考，可以组织一个简洁明了的回答，既能回答用户问题，又能引导后续交流。
====================完整回复====================

我是GLM，由智谱AI训练的大语言模型。我通过大规模文本数据训练，能够理解和生成人类语言，帮助用户回答问题、提供信息和进行对话交流。

我会持续学习和改进，以提供更好的服务。很高兴能为您解答问题或提供帮助！有什么我能为您做的吗？
====================Token 消耗====================

{ prompt_tokens: 7, completion_tokens: 248, total_tokens: 255 }
```

### **示例代码**

curl

```curl
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "glm-5",
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
    model="glm-5",
    messages=messages,
    result_format="message",  # 设置结果格式为 message
    enable_thinking=True,     # 开启思考模式
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

让我仔细思考用户提出的"你是谁"这个问题。首先需要分析用户提问的意图，这可能是初次接触时的好奇，也可能是想了解我的具体功能和能力。

从专业角度，我应该清晰地表达自己的身份 - 作为一个GLM大语言模型，需要说明自己的基本定位和主要功能。要避免过于技术化的表述，而是用通俗易懂的方式解释。

同时，也要考虑到用户可能关心的一些实际问题，比如隐私保护、数据安全等。这些都是用户在使用AI服务时非常关注的点。

另外，为了展现专业性和友好度，可以在介绍的基础上主动引导对话方向，询问用户是否需要特定的帮助。这样既能让用户更好地了解我，也能为后续对话做好铺垫。

最后，要确保回答简洁明了，重点突出，让用户快速理解我的身份和用途。这样的回答既能满足用户的好奇心，又能展现专业性和服务意识。
====================完整回复====================

我是智谱AI开发的GLM大语言模型，旨在通过自然语言处理技术为用户提供信息和帮助。我通过大规模文本数据训练，能够理解和生成人类语言，回答问题、提供知识支持和参与对话。

我的设计目标是成为有用的AI助手，同时确保用户隐私和数据安全。我不存储用户的个人信息，并且会持续学习和改进以提供更优质的服务。

有什么我能帮您解答的问题或需要协助的任务吗？
====================Token 消耗====================

{"input_tokens": 8, "output_tokens": 269, "total_tokens": 277}
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
                .model("glm-5")
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
让我思考一下如何回答用户的问题。首先，这是一个关于身份识别的简单问题，需要清晰直接地回答。

作为一个大语言模型，我应该准确说明自己的基本身份信息。这包括：
- 名称：GLM
- 开发者：智谱AI
- 主要功能：语言理解和生成

考虑到用户的提问可能源于初次接触，我需要用通俗易懂的方式介绍自己，避免使用过于技术性的术语。同时，也应该简要说明自己的主要能力，这样可以帮助用户更好地了解如何与我互动。

我还应该以友好开放的态度表达，欢迎用户提出各种问题，这样可以为后续对话打下良好基础。不过介绍要简洁明了，不需要过于详细，以免给用户造成信息负担。

最后，为了促进进一步交流，可以主动询问用户是否需要特定帮助，这样能够更好地服务于用户的实际需求。
====================完整回复====================
我是GLM，由智谱AI开发的大语言模型。我通过海量文本数据训练而成，能够理解和生成人类语言，回答问题、提供信息和进行对话。

我的设计目的是帮助用户解决问题、提供知识和支持各类语言任务。我会不断学习和更新，以提供更准确、有用的回答。

有什么我能帮您解答或探讨的问题吗？
```

### **示例代码**

curl

```curl
curl -X POST "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-H "X-DashScope-SSE: enable" \
-d '{
    "model": "glm-5",
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

## **模型功能**

| **模型** | [多轮对话](https://help.aliyun.com/zh/model-studio/multi-round-conversation "") | [Function Calling](https://help.aliyun.com/zh/model-studio/qwen-function-calling#dd5a3dca390k9 "") | [结构化输出](https://help.aliyun.com/zh/model-studio/qwen-structured-output "") | [联网搜索](https://help.aliyun.com/zh/model-studio/web-search "") | [前缀续写](https://help.aliyun.com/zh/model-studio/partial-mode "") | [上下文缓存](https://help.aliyun.com/zh/model-studio/context-cache "") |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型** | [多轮对话](https://help.aliyun.com/zh/model-studio/multi-round-conversation "") | [Function Calling](https://help.aliyun.com/zh/model-studio/qwen-function-calling#dd5a3dca390k9 "") | [结构化输出](https://help.aliyun.com/zh/model-studio/qwen-structured-output "") | [联网搜索](https://help.aliyun.com/zh/model-studio/web-search "") | [前缀续写](https://help.aliyun.com/zh/model-studio/partial-mode "") | [上下文缓存](https://help.aliyun.com/zh/model-studio/context-cache "") |
| glm-5 | 支持 | 支持 | 支持<br>> 仅非思考模式 | 不支持 | 不支持 | 支持<br>> 当前仅支持隐式缓存 |
| glm-4.7 | 支持 | 支持 | 支持<br>> 仅非思考模式 | 不支持 | 不支持 | 不支持 |
| glm-4.6 | 支持 | 支持 | 支持<br>> 仅非思考模式 | 不支持 | 不支持 | 不支持 |
| glm-4.5 | 支持 | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| glm-4.5-air | 支持 | 支持 | 支持 | 不支持 | 不支持 | 不支持 |

## **参数默认值**

| **模型** | **enable\_thinking** | **temperature** | **top\_p** | **top\_k** | **repetition\_penalty** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **模型** | **enable\_thinking** | **temperature** | **top\_p** | **top\_k** | **repetition\_penalty** |
| glm-5 | true | 1.0 | 0.95 | 20 | 1.0 |
| glm-4.7 | true | 1.0 | 0.95 | 20 | 1.0 |
| glm-4.6 | true | 1.0 | 0.95 | 20 | 1.0 |
| glm-4.5 | true | 0.6 | 0.95 | 20 | 1.0 |
| glm-4.5-air | true | 0.6 | 0.95 | 20 | 1.0 |

## **计费说明**

按照模型的输入与输出 Token 计费，价格详情请参考 [GLM](https://help.aliyun.com/zh/model-studio/models#glm4.5 "")。

> 思考模式下，思维链按照输出 Token 计费。

## **常见问题**

### **Q：如何配置** [Dify](https://cloud.dify.ai/apps)？

A：目前暂无法在 Dify 上集成阿里云百炼的 GLM 系列模型。推荐您通过 **通义千问** 卡片使用 Qwen3 模型。更多细节请参见 [Dify](https://help.aliyun.com/zh/model-studio/dify "")。

## **错误码**

如果执行报错，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。