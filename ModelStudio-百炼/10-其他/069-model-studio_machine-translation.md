### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[文本生成](https://help.aliyun.com/zh/model-studio/core-concepts/)[专项模型](https://help.aliyun.com/zh/model-studio/specialized-models/)翻译能力（Qwen-MT）

# 翻译能力（Qwen-MT）

更新时间：2026-01-29 04:47:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作方式

模型选型

快速开始

流式输出

提升翻译效果

术语干预

翻译记忆

领域提示

自定义提示词

应用于生产环境

支持的语言

API参考

Qwen-MT模型是基于Qwen3模型优化的机器翻译大语言模型，支持92个语种（包括中、英、日、韩、法、西、德、泰、印尼、越、阿等）互译，且提供了术语干预、领域提示、记忆库等能力，提升模型在复杂应用场景下的翻译效果。

## 工作方式

1. **传入待翻译内容**：`messages` 数组中有且仅有一个 `role` 为 `user` 的消息，其 `content` 为待翻译文本。

2. **设置语种**：参考 [支持的语言](https://help.aliyun.com/zh/model-studio/machine-translation#038d2865bbydc "")，在 `translation_options` 中设置源语种 (`source_lang`) 和目标语种 (`target_lang`)。若需自动检测源语种，可将 `source_lang` 设为 `auto`。


> 指明源语种有利于提升翻译准确率。



> Qwen-MT 模型也支持通过 [自定义提示词](https://help.aliyun.com/zh/model-studio/machine-translation#42ac4e67d6bnf "") 设置语种。


以 OpenAI 与 DashScope 的 Python SDK 为例，介绍如何调用 Qwen-MT 模型。

OpenAI 兼容

DashScope

```python
# 导入依赖与创建客户端...
completion = client.chat.completions.create(
    model="qwen-mt-flash",    # 选择模型
    # messages 有且仅有一个 role 为 user 的消息，其 content 为待翻译文本
    messages=[{"role": "user", "content": "我看到这个视频后没有笑"}],
    # 由于 translation_options 非 OpenAI 标准参数，需要通过 extra_body 传入
    extra_body={"translation_options": {"source_lang": "Chinese", "target_lang": "English"}},
)
```

```python
# 导入依赖...
response = dashscope.Generation.call(
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    model="qwen-mt-flash",  # 选择模型
    messages=[{"role": "user", "content": "我看到这个视频后没有笑"}],  # messages: role为user, content为待翻译文本
    translation_options={"source_lang": "Chinese", "target_lang": "English"},  # 配置翻译选项
    result_format="message"
)
```

**使用限制：**

- **仅支持单轮翻译**：模型专为翻译任务设计，不支持多轮对话。

- **不支持设置 System Message**：不支持通过 `system` 角色的消息来设定全局行为。翻译配置通过 `translation_options` 中定义。


## **模型选型**

- **通用场景，** 可选择 `qwen-mt-flash` **。** 它在效果、速度、成本三者间取得了平衡，并支持增量流式输出。

- 若追求 **最高翻译质量**，用于专业领域，请选择 `qwen-mt-plus`。

- 若追求 **最快响应速度**，用于实时性强的简单场景，请选择 `qwen-mt-lite`。


各模型详细对比如下：

| **模型** | **推荐场景** | **效果** | **速度** | **成本** | **支持的语言** | **支持增量流式输出** |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型** | **推荐场景** | **效果** | **速度** | **成本** | **支持的语言** | **支持增量流式输出** |
| qwen-mt-plus | 专业领域、正式文书、论文、技术报告等对译文质量要求高的场景 | 最好 | 标准 | 较高 | 92种 | 不支持 |
| qwen-mt-flash | **通用首选**，适用于网站/App内容、商品描述、日常沟通、博客文章等场景 | 较好 | 较快 | 较低 | 92种 | 支持 |
| > qwen-mt-turbo | turbo模型后续不再更新，建议选用效果与功能均更优的flash模型 | 良好 | 较快 | 较低 | 92种 | 不支持 |
| qwen-mt-lite | 实时聊天、弹幕翻译等对延迟敏感的简单场景 | 基础 | 最快 | 最低 | 31种 | 支持 |

模型的上下文、价格等信息请参见[模型列表](https://help.aliyun.com/zh/model-studio/models#b51e22f4b036h "")；并发限流条件请参考[限流](https://help.aliyun.com/zh/model-studio/rate-limit#19090eae8arxa "")。

## **快速开始**

此处以将`“我看到这个视频后没有笑”`翻译为英文的简单场景为例。

您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。如果通过OpenAI SDK或DashScope SDK进行调用，还需要 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

OpenAI兼容

DashScope

**请求示例**

Python

curl

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    # 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    # 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)
messages = [\
    {\
        "role": "user",\
        "content": "我看到这个视频后没有笑"\
    }\
]
translation_options = {
    "source_lang": "auto",
    "target_lang": "English"
}

completion = client.chat.completions.create(
    model="qwen-mt-flash",
    messages=messages,
    extra_body={
        "translation_options": translation_options
    }
)
print(completion.choices[0].message.content)
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen-mt-flash",
    "messages": [{"role": "user", "content": "我看到这个视频后没有笑"}],
    "translation_options": {
      "source_lang": "auto",
      "target_lang": "English"
      }
}'
```

**响应示例**

```plaintext
I didn't laugh after watching this video.
```

**请求示例**

**重要**

DashScope Java SDK 版本需要不低于 2.20.6。

Python

Java

curl

Python

```python
import os
import dashscope

# 若使用新加坡地域的模型，请释放下列注释
# dashscope.base_http_api_url = "https://dashscope-intl.aliyuncs.com/api/v1"
messages = [\
    {\
        "role": "user",\
        "content": "我看到这个视频后没有笑"\
    }\
]
translation_options = {
    "source_lang": "auto",
    "target_lang": "English",
}
response = dashscope.Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-mt-flash",
    messages=messages,
    result_format='message',
    translation_options=translation_options
)
print(response.output.choices[0].message.content)
```

Java

```java
// DashScope SDK 版本需要不低于 2.20.6
import java.lang.System;
import java.util.Collections;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.aigc.generation.TranslationOptions;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;

public class Main {
    // 若使用新加坡地域的模型，请释放下列注释
    // static {Constants.baseHttpApiUrl="https://dashscope-intl.aliyuncs.com/api/v1";}
    public static GenerationResult callWithMessage() throws ApiException, NoApiKeyException, InputRequiredException {
        Generation gen = new Generation();
        Message userMsg = Message.builder()
                .role(Role.USER.getValue())
                .content("我看到这个视频后没有笑")
                .build();
        TranslationOptions options = TranslationOptions.builder()
                .sourceLang("auto")
                .targetLang("English")
                .build();
        GenerationParam param = GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-mt-flash")
                .messages(Collections.singletonList(userMsg))
                .resultFormat(GenerationParam.ResultFormat.MESSAGE)
                .translationOptions(options)
                .build();
        return gen.call(param);
    }
    public static void main(String[] args) {
        try {
            GenerationResult result = callWithMessage();
            System.out.println(result.getOutput().getChoices().get(0).getMessage().getContent());
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.err.println("错误信息："+e.getMessage());
            e.printStackTrace();
        } finally {
            System.exit(0);
        }
    }
}
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/text-generation/generation
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation \
-H "Authorization: $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "model": "qwen-mt-flash",
  "input": {
    "messages": [\
      {\
        "content": "我看到这个视频后没有笑",\
        "role": "user"\
      }\
    ]
  },
  "parameters": {
    "translation_options": {
      "source_lang": "auto",
      "target_lang": "English"
    }
  }
}'
```

**响应示例**

```plaintext
I didn't laugh after watching this video.
```

## **流式输出**

流式输出可以实时返回翻译内容，减少用户等待时间。当前仅qwen-mt-flash和qwen-mt-lite支持流式增量输出，每次返回仅包含新生成的内容，可通过`incremental_output`参数开启。qwen-mt-plus与qwen-mt-turbo仅支持非增量流式输出，每次返回当前已经生成的整个序列，最后返回的数据为生成的完整结果。详情请参见 [流式输出](https://help.aliyun.com/zh/model-studio/stream "")。

OpenAI兼容

DashScope

**请求示例**

Python

curl

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    # 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)
messages = [{"role": "user", "content": "我看到这个视频后没有笑"}]
translation_options = {"source_lang": "Chinese", "target_lang": "English"}

completion = client.chat.completions.create(
    model="qwen-mt-flash",
    messages=messages,
    stream=True,
    stream_options={"include_usage": True},
    extra_body={"translation_options": translation_options},
)
for chunk in completion:
    if chunk.choices:
        content = chunk.choices[0].delta.content or ""
        print(content, end="", flush=True)
    else:
        print("\n"+"="*20+"usage 消耗"+"="*20)
        print(chunk.usage)
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen-mt-flash",
    "messages": [{"role": "user", "content": "我看到这个视频后没有笑"}],
    "stream": true,
    "translation_options": {
      "source_lang": "Chinese",
      "target_lang": "English"
      }
}'
```

**响应示例**

```
I didn’t laugh after watching this video.
====================usage 消耗====================
CompletionUsage(completion_tokens=9, prompt_tokens=56, total_tokens=65, completion_tokens_details=None, prompt_tokens_details=None)
```

**请求示例**

Python

Java

curl

Python

```python
import os
import dashscope

# 若使用新加坡地域的模型，请释放下列注释
# dashscope.base_http_api_url = "https://dashscope-intl.aliyuncs.com/api/v1"
messages = [\
    {\
        "role": "user",\
        "content": "我看到这个视频后没有笑"\
    }\
]
translation_options = {
    "source_lang": "Chinese",
    "target_lang": "English",
}
response = dashscope.Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-mt-flash",
    messages=messages,
    result_format='message',
    stream=True,
    # 推荐设置incremental_output为True以获取增量输出，当前仅qwen-mt-flash支持
    incremental_output=True,
    translation_options=translation_options
)
for chunk in response:
    print(chunk.output.choices[0].message.content, end="", flush=True)
```

Java

```java
// DashScope SDK 版本需要不低于 2.20.6
import java.lang.System;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.aigc.generation.TranslationOptions;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;
import java.util.Arrays;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import io.reactivex.Flowable;

public class Main {
    // 若使用新加坡地域的模型，请释放下列注释
    // static {Constants.baseHttpApiUrl="https://dashscope-intl.aliyuncs.com/api/v1";}
    private static final Logger logger = LoggerFactory.getLogger(Main.class);
    private static void handleGenerationResult(GenerationResult message) {
        String content = message.getOutput().getChoices().get(0).getMessage().getContent();
        System.out.print(content);
    }
    public static void streamCallWithMessage(Generation gen, Message userMsg)
            throws NoApiKeyException, ApiException, InputRequiredException {
        GenerationParam param = buildGenerationParam(userMsg);
        Flowable<GenerationResult> result = gen.streamCall(param);
        result.blockingForEach(message -> handleGenerationResult(message));
    }
    private static GenerationParam buildGenerationParam(Message userMsg) {
        TranslationOptions options = TranslationOptions.builder()
                .sourceLang("auto")
                .targetLang("English")
                .build();
        return GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-mt-flash")
                .resultFormat(GenerationParam.ResultFormat.MESSAGE)
                .translationOptions(options)
                // 开启增量输出，当前仅qwen-mt-flash支持
                .incrementalOutput(true)
                .messages(Arrays.asList(userMsg))
                .build();
    }
    public static void main(String[] args) {
        try {
            Generation gen = new Generation();
            Message userMsg = Message.builder().role(Role.USER.getValue()).content("我看到这个视频后没有笑").build();
            streamCallWithMessage(gen, userMsg);
        } catch (ApiException | NoApiKeyException | InputRequiredException  e) {
            logger.error("An exception occurred: {}", e.getMessage());
        }
        System.exit(0);
    }
}
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/text-generation/generation
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation \
-H "Authorization: $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-H "X-DashScope-SSE: enable" \
-d '{
  "model": "qwen-mt-flash",
  "input": {
    "messages": [\
      {\
        "content": "我看到这个视频后没有笑",\
        "role": "user"\
      }\
    ]
  },
  "parameters": {
    "translation_options": {
      "source_lang": "Chinese",
      "target_lang": "English"
  },
  "incremental_output":true
}'
```

**响应示例**

```plaintext
I didn't laugh after watching this video.
```

> qwen-mt-plus、qwen-mt-turbo模型不支持增量式流式输出。

## **提升翻译效果**

标准翻译能应对日常沟通等简单需求，但在面对专业、高要求的翻译任务时可能遇到以下问题：

- **术语不统一**：产品名或行业术语翻译错误。

- **风格不匹配**：译文风格不符合法律、营销等特定领域的规范。


可通过术语干预、翻译记忆与领域提示功能解决这些问题。

### **术语干预**

当文本包含品牌名、产品名或专业术语时，为保证翻译的准确性和一致性，可通过 `terms` 字段提供一个术语表，引导模型参考术语表进行翻译。

术语的定义与传入方法为：

1. **定义术语**

创建一个JSON数组，并将其赋值给 `terms` 字段。数组中的每一个对象代表一条术语，格式如下：















```json
{
       "source": "术语",
       "target": "提前翻译好的术语"
}
```

2. **传入术语**

通过`translation_options`参数传入定义好的 `terms`术语数组。


OpenAI兼容

DashScope

**请求示例**

Python

curl

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    # 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    # 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)

messages = [\
    {\
        "role": "user",\
        "content": "而这套生物传感器运用了石墨烯这种新型材料，它的目标物是化学元素，敏锐的“嗅觉”让它能更深度、准确地体现身体健康状况。"\
    }\
]

# --- 第一次请求：不使用 terms 参数 ---
print("--- [不使用 terms] 的翻译结果 ---")
translation_options_without_terms = {
    "source_lang": "auto",
    "target_lang": "English"
}

completion_without_terms = client.chat.completions.create(
    model="qwen-mt-plus",
    messages=messages,
    extra_body={
        "translation_options": translation_options_without_terms
    }
)
print(completion_without_terms.choices[0].message.content)

print("\n" + "="*50 + "\n") # 用于分割，方便对比

# --- 第二次请求：使用 terms 参数 ---
print("--- [使用 terms] 的翻译结果 ---")
translation_options_with_terms = {
    "source_lang": "Chinese",
    "target_lang": "English",
    "terms": [\
        {\
            "source": "生物传感器",\
            "target": "biological sensor"\
        },\
        {\
            "source": "身体健康状况",\
            "target": "health status of the body"\
        }\
    ]
}

completion_with_terms = client.chat.completions.create(
    model="qwen-mt-plus",
    messages=messages,
    extra_body={
        "translation_options": translation_options_with_terms
    }
)
print(completion_with_terms.choices[0].message.content)
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "model": "qwen-mt-plus",
  "messages": [\
    {\
      "role": "user",\
      "content": "而这套生物传感器运用了石墨烯这种新型材料，它的目标物是化学元素，敏锐的“嗅觉”让它能更深度、准确地体现身体健康状况。"\
    }\
  ],
  "translation_options": {
    "source_lang": "Chinese",
    "target_lang": "English",
    "terms": [\
      {\
        "source": "生物传感器",\
        "target": "biological sensor"\
      },\
      {\
        "source": "身体健康状况",\
        "target": "health status of the body"\
      }\
    ]
  }
}'
```

**响应示例**

加入术语后，翻译结果与传入的术语一致：“ **生物传感器**”（biological sensor）和“ **身体健康状况**”（the health status of the body）。

```plaintext
--- [不使用 terms] 的翻译结果 ---
This set of biosensors uses graphene, a new material, whose target substance is chemical elements. Its sensitive "sense of smell" allows it to more deeply and accurately reflect one's health condition.

==================================================

--- [使用 terms] 的翻译结果 ---
This biological sensor uses a new material called graphene. Its target is chemical elements, and its sensitive "sense of smell" enables it to reflect the health status of the body more deeply and accurately.
```

**请求示例**

Python

Java

curl

Python

```python
import os
import dashscope

# 若使用新加坡地域的模型，请释放下列注释
# dashscope.base_http_api_url = "https://dashscope-intl.aliyuncs.com/api/v1"
messages = [\
    {\
        "role": "user",\
        "content": "而这套生物传感器运用了石墨烯这种新型材料，它的目标物是化学元素，敏锐的“嗅觉”让它能更深度、准确地体现身体健康状况。"\
    }\
]
translation_options = {
    "source_lang": "Chinese",
    "target_lang": "English",
    "terms": [\
        {\
            "source": "生物传感器",\
            "target": "biological sensor"\
        },\
        {\
            "source": "身体健康状况",\
            "target": "health status of the body"\
        }\
    ]
}
response = dashscope.Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-mt-plus",
    messages=messages,
    result_format='message',
    translation_options=translation_options
)
print(response.output.choices[0].message.content)
```

Java

```java
// DashScope SDK 版本需要不低于 2.20.6
import java.lang.System;
import java.util.Collections;
import java.util.Arrays;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.aigc.generation.TranslationOptions;
import com.alibaba.dashscope.aigc.generation.TranslationOptions.Term;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;

public class Main {
    // 若使用新加坡地域的模型，请释放下列注释
    // static {Constants.baseHttpApiUrl="https://dashscope-intl.aliyuncs.com/api/v1";}
    public static GenerationResult callWithMessage() throws ApiException, NoApiKeyException, InputRequiredException {
        Generation gen = new Generation();
        Message userMsg = Message.builder()
                .role(Role.USER.getValue())
                .content("而这套生物传感器运用了石墨烯这种新型材料，它的目标物是化学元素，敏锐的“嗅觉”让它能更深度、准确地体现身体健康状况。")
                .build();
        Term term1 = Term.builder()
                .source("生物传感器")
                .target("biological sensor")
                .build();
        Term term2 = Term.builder()
                .source("身体健康状况")
                .target("health status of the body")
                .build();
        TranslationOptions options = TranslationOptions.builder()
                .sourceLang("auto")
                .targetLang("English")
                .terms(Arrays.asList(term1, term2))
                .build();
        GenerationParam param = GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-mt-plus")
                .messages(Collections.singletonList(userMsg))
                .resultFormat(GenerationParam.ResultFormat.MESSAGE)
                .translationOptions(options)
                .build();
        return gen.call(param);
    }
    public static void main(String[] args) {
        try {
            GenerationResult result = callWithMessage();
            System.out.println(result.getOutput().getChoices().get(0).getMessage().getContent());
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.err.println("错误信息："+e.getMessage());
        }
        System.exit(0);
    }
}
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/text-generation/generation
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation \
-H "Authorization: $DASHSCOPE_API_KEY" \
-H 'Content-Type: application/json' \
-d '{
  "model": "qwen-mt-plus",
  "input": {
    "messages": [\
      {\
        "content": "而这套生物传感器运用了石墨烯这种新型材料，它的目标物是化学元素，敏锐的“嗅觉”让它能更深度、准确地体现身体健康状况。",\
        "role": "user"\
      }\
    ]
  },
  "parameters": {
    "translation_options": {
      "source_lang": "Chinese",
      "target_lang": "English",
      "terms": [\
        {\
          "source": "生物传感器",\
          "target": "biological sensor"\
        },\
        {\
          "source": "身体健康状况",\
          "target": "health status of the body"\
        }\
      ]
    }
  }
}'
```

**响应示例**

```plaintext
This biological sensor uses graphene, a new material, and its target is chemical elements. Its sensitive "nose" can more deeply and accurately reflect the health status of the human body.
```

### **翻译记忆**

如果您希望模型参考特定的翻译风格或句式，可通过 `tm_list` 字段提供“源文-译文”句对作为示例。模型将在本次翻译任务中模仿这些示例的风格。

1. **定义翻译记忆**

您需要创建一个已翻译句子的JSON数组`tm_list`，每个JSON对象包含源语句与对应的已翻译的语句，格式如下：















```json
{
       "source": "源语句",
       "target": "已翻译的语句"
}
```

2. **传入翻译记忆**

通过`translation_options`参数传入翻译记忆数组。


可参考以下代码实现翻译记忆功能。

OpenAI兼容

DashScope

**请求示例**

Python

curl

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    # 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    # 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)
messages = [\
    {\
        "role": "user",\
        "content": "通过如下命令可以看出安装thrift的版本信息；"\
    }\
]
translation_options = {
    "source_lang": "Chinese",
    "target_lang": "English",
    "tm_list": [\
        {\
            "source": "您可以通过如下方式查看集群的内核版本信息:",\
            "target": "You can use one of the following methods to query the engine version of a cluster:"\
        },\
        {\
            "source": "我们云HBase的thrift环境是0.9.0,所以建议客户端的版本也为 0.9.0,可以从这里下载thrift的0.9.0 版本,下载的源码包我们后面会用到,这里需要先安装thrift编译环境,对于源码安装可以参考thrift官网;",\
            "target": "The version of Thrift used by ApsaraDB for HBase is 0.9.0. Therefore, we recommend that you use Thrift 0.9.0 to create a client. Click here to download Thrift 0.9.0. The downloaded source code package will be used later. You must install the Thrift compiling environment first. For more information, see Thrift official website."\
        },\
        {\
            "source": "您可以通过PyPI来安装SDK,安装命令如下:",\
            "target": "You can run the following command in Python Package Index (PyPI) to install Elastic Container Instance SDK for Python:"\
        }\
    ]
}

completion = client.chat.completions.create(
    model="qwen-mt-plus",
    messages=messages,
    extra_body={
        "translation_options": translation_options
    }
)
print(completion.choices[0].message.content)
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "model": "qwen-mt-plus",
  "messages": [\
    {\
      "role": "user",\
      "content": "通过如下命令可以看出安装thrift的版本信息；"\
    }\
  ],
  "translation_options": {
    "source_lang": "Chinese",
    "target_lang": "English",
    "tm_list":[\
          {"source": "您可以通过如下方式查看集群的内核版本信息:", "target": "You can use one of the following methods to query the engine version of a cluster:"},\
          {"source": "我们云HBase的thrift环境是0.9.0,所以建议客户端的版本也为 0.9.0,可以从这里下载thrift的0.9.0 版本,下载的源码包我们后面会用到,这里需要先安装thrift编译环境,对于源码安装可以参考thrift官网;", "target": "The version of Thrift used by ApsaraDB for HBase is 0.9.0. Therefore, we recommend that you use Thrift 0.9.0 to create a client. Click here to download Thrift 0.9.0. The downloaded source code package will be used later. You must install the Thrift compiling environment first. For more information, see Thrift official website."},\
          {"source": "您可以通过PyPI来安装SDK,安装命令如下:", "target": "You can run the following command in Python Package Index (PyPI) to install Elastic Container Instance SDK for Python:"}\
    ]
  }
}'
```

**响应示例**

```plaintext
You can run the following command to view the version of Thrift that is installed:
```

**请求示例**

Python

Java

curl

Python

```python
import os
import dashscope

# 若使用新加坡地域的模型，请释放下列注释
# dashscope.base_http_api_url = "https://dashscope-intl.aliyuncs.com/api/v1"
messages = [\
    {\
        "role": "user",\
        "content": "通过如下命令可以看出安装thrift的版本信息；"\
    }\
]
translation_options = {
    "source_lang": "Chinese",
    "target_lang": "English",
    "tm_list": [\
        {\
            "source": "您可以通过如下方式查看集群的内核版本信息:",\
            "target": "You can use one of the following methods to query the engine version of a cluster:"\
        },\
        {\
            "source": "我们云HBase的thrift环境是0.9.0,所以建议客户端的版本也为 0.9.0,可以从这里下载thrift的0.9.0 版本,下载的源码包我们后面会用到,这里需要先安装thrift编译环境,对于源码安装可以参考thrift官网;",\
            "target": "The version of Thrift used by ApsaraDB for HBase is 0.9.0. Therefore, we recommend that you use Thrift 0.9.0 to create a client. Click here to download Thrift 0.9.0. The downloaded source code package will be used later. You must install the Thrift compiling environment first. For more information, see Thrift official website."\
        },\
        {\
            "source": "您可以通过PyPI来安装SDK,安装命令如下:",\
            "target": "You can run the following command in Python Package Index (PyPI) to install Elastic Container Instance SDK for Python:"\
        }\
    ]}
response = dashscope.Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-mt-plus",
    messages=messages,
    result_format='message',
    translation_options=translation_options
)
print(response.output.choices[0].message.content)
```

Java

```java
// DashScope SDK 版本需要不低于 2.20.6
import java.lang.System;
import java.util.Collections;
import java.util.Arrays;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.aigc.generation.TranslationOptions;
import com.alibaba.dashscope.aigc.generation.TranslationOptions.Tm;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;

public class Main {
    // 若使用新加坡地域的模型，请释放下列注释
    // static {Constants.baseHttpApiUrl="https://dashscope-intl.aliyuncs.com/api/v1";}
    public static GenerationResult callWithMessage() throws ApiException, NoApiKeyException, InputRequiredException {
        Generation gen = new Generation();
        Message userMsg = Message.builder()
                .role(Role.USER.getValue())
                .content("通过如下命令可以看出安装thrift的版本信息；")
                .build();
        Tm tm1 = Tm.builder()
                .source("您可以通过如下方式查看集群的内核版本信息:")
                .target("You can use one of the following methods to query the engine version of a cluster:")
                .build();
        Tm tm2 = Tm.builder()
                .source("我们云HBase的thrift环境是0.9.0,所以建议客户端的版本也为 0.9.0,可以从这里下载thrift的0.9.0 版本,下载的源码包我们后面会用到,这里需要先安装thrift编译环境,对于源码安装可以参考thrift官网;")
                .target("The version of Thrift used by ApsaraDB for HBase is 0.9.0. Therefore, we recommend that you use Thrift 0.9.0 to create a client. Click here to download Thrift 0.9.0. The downloaded source code package will be used later. You must install the Thrift compiling environment first. For more information, see Thrift official website.")
                .build();
        Tm tm3 = Tm.builder()
                .source("您可以通过PyPI来安装SDK,安装命令如下:")
                .target("You can run the following command in Python Package Index (PyPI) to install Elastic Container Instance SDK for Python:")
                .build();
        TranslationOptions options = TranslationOptions.builder()
                .sourceLang("auto")
                .targetLang("English")
                .tmList(Arrays.asList(tm1, tm2, tm3))
                .build();
        GenerationParam param = GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-mt-plus")
                .messages(Collections.singletonList(userMsg))
                .resultFormat(GenerationParam.ResultFormat.MESSAGE)
                .translationOptions(options)
                .build();
        return gen.call(param);
    }
    public static void main(String[] args) {
        try {
            GenerationResult result = callWithMessage();
            System.out.println(result.getOutput().getChoices().get(0).getMessage().getContent());
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.err.println("错误信息："+e.getMessage());
        }
        System.exit(0);
    }
}
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/text-generation/generation
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation \
-H "Authorization: $DASHSCOPE_API_KEY" \
-H 'Content-Type: application/json' \
-d '{
  "model": "qwen-mt-plus",
  "input": {
    "messages": [\
      {\
        "content": "通过如下命令可以看出安装thrift的版本信息；",\
        "role": "user"\
      }\
    ]
  },
  "parameters": {
    "translation_options": {
      "source_lang": "Chinese",
      "target_lang": "English",
      "tm_list":[\
          {"source": "您可以通过如下方式查看集群的内核版本信息:", "target": "You can use one of the following methods to query the engine version of a cluster:"},\
          {"source": "我们云HBase的thrift环境是0.9.0,所以建议客户端的版本也为 0.9.0,可以从这里下载thrift的0.9.0 版本,下载的源码包我们后面会用到,这里需要先安装thrift编译环境,对于源码安装可以参考thrift官网;", "target": "The version of Thrift used by ApsaraDB for HBase is 0.9.0. Therefore, we recommend that you use Thrift 0.9.0 to create a client. Click here to download Thrift 0.9.0. The downloaded source code package will be used later. You must install the Thrift compiling environment first. For more information, see Thrift official website."},\
          {"source": "您可以通过PyPI来安装SDK,安装命令如下:", "target": "You can run the following command in Python Package Index (PyPI) to install Elastic Container Instance SDK for Python:"}\
      ]
  }
}'
```

**响应示例**

```plaintext
You can use the following commands to check the version information of thrift installed;
```

### **领域提示**

如果您希望翻译的风格更符合某个领域的特性，如法律、政务领域翻译用语应当严肃正式，社交领域用语应当口语化，可以通过`translation_options`参数传入领域提示语句。

**重要**

领域提示语句当前只支持英文。

OpenAI兼容

DashScope

**请求示例**

Python

curl

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    # 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    # 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)
messages = [\
    {\
        "role": "user",\
        "content": "第二个SELECT语句返回一个数字，表示在没有LIMIT子句的情况下，第一个SELECT语句返回了多少行。"\
    }\
]

# --- 第一次请求：不使用 domains 参数 ---
print("--- [不使用 domains] 的翻译结果 ---")
translation_options_without_domains = {
    "source_lang": "Chinese",
    "target_lang": "English",
}

completion_without_domains = client.chat.completions.create(
    model="qwen-mt-plus",
    messages=messages,
    extra_body={
        "translation_options": translation_options_without_domains
    }
)
print(completion_without_domains.choices[0].message.content)

print("\n" + "="*50 + "\n") # 用于分割，方便对比

# --- 第二次请求：使用 domains 参数 (您的原始代码) ---
print("--- [使用 domains] 的翻译结果 ---")
translation_options_with_domains = {
    "source_lang": "Chinese",
    "target_lang": "English",
    "domains": "The sentence is from Ali Cloud IT domain. It mainly involves computer-related software development and usage methods, including many terms related to computer software and hardware. Pay attention to professional troubleshooting terminologies and sentence patterns when translating. Translate into this IT domain style."
}

completion_with_domains = client.chat.completions.create(
    model="qwen-mt-plus",
    messages=messages,
    extra_body={
        "translation_options": translation_options_with_domains
    }
)
print(completion_with_domains.choices[0].message.content)
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "model": "qwen-mt-plus",
  "messages": [\
    {\
      "role": "user",\
      "content": "第二个SELECT语句返回一个数字，表示在没有LIMIT子句的情况下，第一个SELECT语句返回了多少行。"\
    }\
  ],
  "translation_options": {
    "source_lang": "Chinese",
    "target_lang": "English",
    "domains": "The sentence is from Ali Cloud IT domain. It mainly involves computer-related software development and usage methods, including many terms related to computer software and hardware. Pay attention to professional troubleshooting terminologies and sentence patterns when translating. Translate into this IT domain style."
  }
}'
```

**响应示例**

```plaintext
--- [不使用 domains] 的翻译结果 ---
The second SELECT statement returns a number indicating how many rows the first SELECT statement would return without the LIMIT clause.

==================================================

--- [使用 domains] 的翻译结果 ---
The second SELECT statement returns a number that indicates how many rows the first SELECT statement would have returned if it had not included a LIMIT clause.
```

**请求示例**

Python

Java

curl

Python

```python
import os
import dashscope

# 若使用新加坡地域的模型，请释放下列注释
# dashscope.base_http_api_url = "https://dashscope-intl.aliyuncs.com/api/v1"

messages = [\
    {\
        "role": "user",\
        "content": "第二个SELECT语句返回一个数字，表示在没有LIMIT子句的情况下，第一个SELECT语句返回了多少行。"\
    }\
]
translation_options = {
    "source_lang": "Chinese",
    "target_lang": "English",
    "domains": "The sentence is from Ali Cloud IT domain. It mainly involves computer-related software development and usage methods, including many terms related to computer software and hardware. Pay attention to professional troubleshooting terminologies and sentence patterns when translating. Translate into this IT domain style."
}
response = dashscope.Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-mt-plus",
    messages=messages,
    result_format='message',
    translation_options=translation_options
)
print(response.output.choices[0].message.content)
```

Java

```java
// DashScope SDK 版本需要不低于 2.20.6
import java.lang.System;
import java.util.Collections;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.aigc.generation.TranslationOptions;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;

public class Main {
    // 若使用新加坡地域的模型，请释放下列注释
    // static {Constants.baseHttpApiUrl="https://dashscope-intl.aliyuncs.com/api/v1";}
    public static GenerationResult callWithMessage() throws ApiException, NoApiKeyException, InputRequiredException {
        Generation gen = new Generation();
        Message userMsg = Message.builder()
                .role(Role.USER.getValue())
                .content("第二个SELECT语句返回一个数字，表示在没有LIMIT子句的情况下，第一个SELECT语句返回了多少行。")
                .build();
        TranslationOptions options = TranslationOptions.builder()
                .sourceLang("auto")
                .targetLang("English")
                .domains("The sentence is from Ali Cloud IT domain. It mainly involves computer-related software development and usage methods, including many terms related to computer software and hardware. Pay attention to professional troubleshooting terminologies and sentence patterns when translating. Translate into this IT domain style.")
                .build();
        GenerationParam param = GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-mt-plus")
                .messages(Collections.singletonList(userMsg))
                .resultFormat(GenerationParam.ResultFormat.MESSAGE)
                .translationOptions(options)
                .build();
        return gen.call(param);
    }
    public static void main(String[] args) {
        try {
            GenerationResult result = callWithMessage();
            System.out.println(result.getOutput().getChoices().get(0).getMessage().getContent());
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.err.println("错误信息："+e.getMessage());
        }
        System.exit(0);
    }
}
```

curl

```curl
# ======= 重要提示 =======
# 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/aigc/text-generation/generation
# === 执行时请删除该注释 ===
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation \
-H "Authorization: $DASHSCOPE_API_KEY" \
-H 'Content-Type: application/json' \
-d '{
  "model": "qwen-mt-plus",
  "input": {
    "messages": [\
      {\
        "content": "第二个SELECT语句返回一个数字，表示在没有LIMIT子句的情况下，第一个SELECT语句返回了多少行。",\
        "role": "user"\
      }\
    ]
  },
  "parameters": {
    "translation_options": {
      "source_lang": "Chinese",
      "target_lang": "English",
      "domains": "The sentence is from Ali Cloud IT domain. It mainly involves computer-related software development and usage methods, including many terms related to computer software and hardware. Pay attention to professional troubleshooting terminologies and sentence patterns when translating. Translate into this IT domain style."}
  }
}'
```

**响应示例**

```plaintext
The second SELECT statement returns a number that indicates how many rows were returned by the first SELECT statement without a LIMIT clause.
```

## **自定义提示词**

Qwen-MT 支持通过自定义提示词（如指定语种、风格）引导翻译。此方式与 `translation_options` 参数互斥，若同时使用，`translation_options` 的配置可能不生效。

> 为获得最佳翻译效果，推荐使用 `translation_options` 参数配置翻译选项。

以法律领域的汉译英翻译场景为例：

OpenAI兼容

DashScope

Python

Node.js

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    # 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    # 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)

prompt_template = """
# 角色
你是一名专业的法律翻译专家，精通中文和英文，尤其擅长处理商业合同和法律文件。

# 任务
我需要你将以下中文法律文本翻译成专业、精准、正式的英文。

# 翻译要求
1.  **忠实原文**：严格按照原文的含义和法律意图进行翻译，不得添加或删减信息。
2.  **术语精准**：使用英美法系（Common law）通用的标准法律术语。例如，“甲方”应翻译为 "Party A"，“乙方”应翻译为 "Party B"，“不可抗力”应翻译为 "Force Majeure"。
3.  **语气正式**：保持法律文件固有的严谨、客观和正式的语体。
4.  **语句清晰**：译文必须清晰、无歧义，符合英文法律文书的表达习惯。
5.  **格式保留**：保持原文的段落、编号和基本格式。

# 待翻译文本
{text_to_translate}
"""

# --- 2. 准备待翻译的法律文本 ---
chinese_legal_text = "本合同自双方签字盖章之日起生效，有效期为一年。"
final_prompt = prompt_template.format(text_to_translate=chinese_legal_text)

# --- 3. 构建messages ---
messages = [{"role": "user", "content": final_prompt}]

# --- 4. 发起API请求 ---
completion = client.chat.completions.create(model="qwen-mt-plus", messages=messages)

# --- 5. 打印模型的翻译结果 ---
translation_result = completion.choices[0].message.content
print(translation_result)
```

Node.js

```nodejs
import OpenAI from 'openai';

const client = new OpenAI({
    // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：apiKey: "sk-xxx",
    // 各地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    apiKey: process.env.DASHSCOPE_API_KEY,
    // 以下是北京地域base_url，如果使用新加坡地域的模型，需要将base_url替换为：https://dashscope-intl.aliyuncs.com/compatible-mode/v1
    baseURL: "https://dashscope.aliyuncs.com/compatible-mode/v1",
});

const promptTemplate = `
# 角色
你是一名专业的法律翻译专家，精通中文和英文，尤其擅长处理商业合同和法律文件。

# 任务
我需要你将以下中文法律文本翻译成专业、精准、正式的英文。

# 翻译要求
1.  **忠实原文**：严格按照原文的含义和法律意图进行翻译，不得添加或删减信息。
2.  **术语精准**：使用英美法系（Common law）通用的标准法律术语。例如，“甲方”应翻译为 "Party A"，“乙方”应翻译为 "Party B"，“不可抗力”应翻译为 "Force Majeure"。
3.  **语气正式**：保持法律文件固有的严谨、客观和正式的语体。
4.  **语句清晰**：译文必须清晰、无歧义，符合英文法律文书的表达习惯。
5.  **格式保留**：保持原文的段落、编号和基本格式。

# 待翻译文本
{text_to_translate}
`;

const chineseLegalText = "本合同自双方签字盖章之日起生效，有效期为一年。";
const finalPrompt = promptTemplate.replace('{text_to_translate}', chineseLegalText);

const messages = [{"role": "user", "content": finalPrompt}];

async function main() {
    const completion = await client.chat.completions.create({
        model: "qwen-mt-plus",
        messages: messages
    });

    const translationResult = completion.choices[0].message.content;
    console.log(translationResult);
}

main();
```

**响应示例**

```plaintext
This Contract shall become effective from the date on which both parties sign and affix their seals, and its term of validity shall be one year.
```

**请求示例**

Python

Java

Python

```python
import os
import dashscope

# 若使用新加坡地域的模型，请释放下列注释
# dashscope.base_http_api_url = "https://dashscope-intl.aliyuncs.com/api/v1"

prompt_template = """
# 角色
你是一名专业的法律翻译专家，精通中文和英文，尤其擅长处理商业合同和法律文件。

# 任务
我需要你将以下中文法律文本翻译成专业、精准、正式的英文。

# 翻译要求
1.  **忠实原文**：严格按照原文的含义和法律意图进行翻译，不得添加或删减信息。
2.  **术语精准**：使用英美法系（Common law）通用的标准法律术语。例如，“甲方”应翻译为 "Party A"，“乙方”应翻译为 "Party B"，“不可抗力”应翻译为 "Force Majeure"。
3.  **语气正式**：保持法律文件固有的严谨、客观和正式的语体。
4.  **语句清晰**：译文必须清晰、无歧义，符合英文法律文书的表达习惯。
5.  **格式保留**：保持原文的段落、编号和基本格式。

# 待翻译文本
{text_to_translate}
"""

# --- 2. 准备待翻译的法律文本 ---
chinese_legal_text = "本合同自双方签字盖章之日起生效，有效期为一年。"
final_prompt = prompt_template.format(text_to_translate=chinese_legal_text)

# --- 3. 构建messages ---
messages = [\
    {\
        "role": "user",\
        "content": final_prompt\
    }\
]

response = dashscope.Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-mt-plus",
    messages=messages,
    result_format='message',
)
print(response.output.choices[0].message.content)
```

Java

```java
// DashScope SDK 版本需要不低于 2.20.6
import java.lang.System;
import java.util.Collections;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;

public class Main {
    // 若使用新加坡地域的模型，请释放下列注释
    // static {Constants.baseHttpApiUrl="https://dashscope-intl.aliyuncs.com/api/v1";}
    public static GenerationResult callWithMessage() throws ApiException, NoApiKeyException, InputRequiredException {
        Generation gen = new Generation();
        String promptTemplate = "# 角色\n" +
                "你是一名专业的法律翻译专家，精通中文和英文，尤其擅长处理商业合同和法律文件。\n\n" +
                "# 任务\n" +
                "我需要你将以下中文法律文本翻译成专业、精准、正式的英文。\n\n" +
                "# 翻译要求\n" +
                "1.  **忠实原文**：严格按照原文的含义和法律意图进行翻译，不得添加或删减信息。\n" +
                "2.  **术语精准**：使用英美法系（Common law）通用的标准法律术语。例如，“甲方”应翻译为 \"Party A\"，“乙方”应翻译为 \"Party B\"，“不可抗力”应翻译为 \"Force Majeure\"。\n" +
                "3.  **语气正式**：保持法律文件固有的严谨、客观和正式的语体。\n" +
                "4.  **语句清晰**：译文必须清晰、无歧义，符合英文法律文书的表达习惯。\n" +
                "5.  **格式保留**：保持原文的段落、编号和基本格式。\n\n" +
                "# 待翻译文本\n" +
                "{text_to_translate}";

        String chineseLegalText = "本合同自双方签字盖章之日起生效，有效期为一年。";
        String finalPrompt = promptTemplate.replace("{text_to_translate}", chineseLegalText);

        Message userMsg = Message.builder()
                .role(Role.USER.getValue())
                .content(finalPrompt)
                .build();

        GenerationParam param = GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-mt-plus")
                .messages(Collections.singletonList(userMsg))
                .resultFormat(GenerationParam.ResultFormat.MESSAGE)
                .build();
        return gen.call(param);
    }
    public static void main(String[] args) {
        try {
            GenerationResult result = callWithMessage();
            System.out.println(result.getOutput().getChoices().get(0).getMessage().getContent());
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.err.println("错误信息："+e.getMessage());
            e.printStackTrace();
        }
        }
    }
```

**响应示例**

```plaintext
This Contract shall become effective from the date on which both parties sign and affix their seals, and its term of validity shall be one year.
```

## **应用于生产环境**

- **控制输入 Token 数量**

Qwen-MT 模型的输入 Token 上限为 8,192。若输入内容较长，可参考以下策略控制输入 Token 数：

  - **分段翻译**：翻译长文本时请分段处理。按语义（如段落或完整句子）分割文本，而非按字符数。这能保证上下文完整性，提升翻译质量。

  - **传入最相关的参考内容：** 术语、翻译记忆和领域提示会作为输入 Token 拼接到提示词中。请仅提供与当前任务最相关的参考内容，避免使用庞大、通用的列表。
- **根据场景设置**`source_lang`

  - 在不确定翻译原文的语种时（如社交聊天场景时存在多语言文本）可设置`source_lang`为`auto`，模型将自动识别源语种。

  - 在语种固定、准确度要求高的场景（如技术文档或操作手册），建议始终指定`source_lang`，明确指定源语种可提升翻译准确率。

## **支持的语言**

下表中的 **英文名** 或 **代码** 用于在发起请求时指定。

> 当不确定源语种时，可为`source_lang`参数赋值`auto`以自动检测。

qwen-mt-plus/flash/turbo 支持的语言 (92种)

qwen-mt-lite 支持的语言 (31种)

|     |     |     |
| --- | --- | --- |
| **语言** | **英文名** | **代码** |
| 英语 | English | en |
| 简体中文 | Chinese | zh |
| 繁体中文 | Traditional Chinese | zh\_tw |
| 俄语 | Russian | ru |
| 日语 | Japanese | ja |
| 韩语 | Korean | ko |
| 西班牙语 | Spanish | es |
| 法语 | French | fr |
| 葡萄牙语 | Portuguese | pt |
| 德语 | German | de |
| 意大利语 | Italian | it |
| 泰语 | Thai | th |
| 越南语 | Vietnamese | vi |
| 印度尼西亚语 | Indonesian | id |
| 马来语 | Malay | ms |
| 阿拉伯语 | Arabic | ar |
| 印地语 | Hindi | hi |
| 希伯来语 | Hebrew | he |
| 缅甸语 | Burmese | my |
| 泰米尔语 | Tamil | ta |
| 乌尔都语 | Urdu | ur |
| 孟加拉语 | Bengali | bn |
| 波兰语 | Polish | pl |
| 荷兰语 | Dutch | nl |
| 罗马尼亚语 | Romanian | ro |
| 土耳其语 | Turkish | tr |
| 高棉语 | Khmer | km |
| 老挝语 | Lao | lo |
| 粤语 | Cantonese | yue |
| 捷克语 | Czech | cs |
| 希腊语 | Greek | el |
| 瑞典语 | Swedish | sv |
| 匈牙利语 | Hungarian | hu |
| 丹麦语 | Danish | da |
| 芬兰语 | Finnish | fi |
| 乌克兰语 | Ukrainian | uk |
| 保加利亚语 | Bulgarian | bg |
| 塞尔维亚语 | Serbian | sr |
| 泰卢固语 | Telugu | te |
| 南非荷兰语 | Afrikaans | af |
| 亚美尼亚语 | Armenian | hy |
| 阿萨姆语 | Assamese | as |
| 阿斯图里亚斯语 | Asturian | ast |
| 巴斯克语 | Basque | eu |
| 白俄罗斯语 | Belarusian | be |
| 波斯尼亚语 | Bosnian | bs |
| 加泰罗尼亚语 | Catalan | ca |
| 宿务语 | Cebuano | ceb |
| 克罗地亚语 | Croatian | hr |
| 埃及阿拉伯语 | Egyptian Arabic | arz |
| 爱沙尼亚语 | Estonian | et |
| 加利西亚语 | Galician | gl |
| 格鲁吉亚语 | Georgian | ka |
| 古吉拉特语 | Gujarati | gu |
| 冰岛语 | Icelandic | is |
| 爪哇语 | Javanese | jv |
| 卡纳达语 | Kannada | kn |
| 哈萨克语 | Kazakh | kk |
| 拉脱维亚语 | Latvian | lv |
| 立陶宛语 | Lithuanian | lt |
| 卢森堡语 | Luxembourgish | lb |
| 马其顿语 | Macedonian | mk |
| 马加希语 | Maithili | mai |
| 马耳他语 | Maltese | mt |
| 马拉地语 | Marathi | mr |
| 美索不达米亚阿拉伯语 | Mesopotamian Arabic | acm |
| 摩洛哥阿拉伯语 | Moroccan Arabic | ary |
| 内志阿拉伯语 | Najdi Arabic | ars |
| 尼泊尔语 | Nepali | ne |
| 北阿塞拜疆语 | North Azerbaijani | az |
| 北黎凡特阿拉伯语 | North Levantine Arabic | apc |
| 北乌兹别克语 | Northern Uzbek | uz |
| 书面语挪威语 | Norwegian Bokmål | nb |
| 新挪威语 | Norwegian Nynorsk | nn |
| 奥克语 | Occitan | oc |
| 奥里亚语 | Odia | or |
| 邦阿西楠语 | Pangasinan | pag |
| 西西里语 | Sicilian | scn |
| 信德语 | Sindhi | sd |
| 僧伽罗语 | Sinhala | si |
| 斯洛伐克语 | Slovak | sk |
| 斯洛文尼亚语 | Slovenian | sl |
| 南黎凡特阿拉伯语 | South Levantine Arabic | ajp |
| 斯瓦希里语 | Swahili | sw |
| 他加禄语 | Tagalog | tl |
| 塔伊兹-亚丁阿拉伯语 | Ta’izzi-Adeni Arabic | acq |
| 托斯克阿尔巴尼亚语 | Tosk Albanian | sq |
| 突尼斯阿拉伯语 | Tunisian Arabic | aeb |
| 威尼斯语 | Venetian | vec |
| 瓦莱语 | Waray | war |
| 威尔士语 | Welsh | cy |
| 西波斯语 | Western Persian | fa |

|     |     |     |
| --- | --- | --- |
| **语言** | **英文名** | **代码** |
| 英语 | English | en |
| 简体中文 | Chinese | zh |
| 繁体中文 | Traditional Chinese | zh\_tw |
| 俄语 | Russian | ru |
| 日语 | Japanese | ja |
| 韩语 | Korean | ko |
| 西班牙语 | Spanish | es |
| 法语 | French | fr |
| 葡萄牙语 | Portuguese | pt |
| 德语 | German | de |
| 意大利语 | Italian | it |
| 泰语 | Thai | th |
| 越南语 | Vietnamese | vi |
| 印度尼西亚语 | Indonesian | id |
| 马来语 | Malay | ms |
| 阿拉伯语 | Arabic | ar |
| 印地语 | Hindi | hi |
| 希伯来语 | Hebrew | he |
| 乌尔都语 | Urdu | ur |
| 孟加拉语 | Bengali | bn |
| 波兰语 | Polish | pl |
| 荷兰语 | Dutch | nl |
| 土耳其语 | Turkish | tr |
| 高棉语 | Khmer | km |
| 捷克语 | Czech | cs |
| 瑞典语 | Swedish | sv |
| 匈牙利语 | Hungarian | hu |
| 丹麦语 | Danish | da |
| 芬兰语 | Finnish | fi |
| 他加禄语 | Tagalog | tl |
| 波斯语 | Persian | fa |

## API参考

Qwen-MT 模型的输入与输出参数请参考 [Qwen-MT 翻译模型](https://help.aliyun.com/zh/model-studio/qwen-mt-api "")。