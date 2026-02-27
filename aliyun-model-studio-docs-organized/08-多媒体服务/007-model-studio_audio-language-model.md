### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[多模态](https://help.aliyun.com/zh/model-studio/multimodal/)[音频理解](https://help.aliyun.com/zh/model-studio/audio-understanding/)音频理解-Qwen-Audio

# 音频理解（Qwen-Audio）

更新时间：2026-02-11 02:38:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

效果示例

支持的模型

快速开始

核心能力

语音对话

传入本地文件（Base64 编码或文件路径）

更多用法

使用限制

支持的音频文件

音频文件输入方式

应用于生产环境

API参考

错误码

常见问题

如何选择文件上传方式？

如何压缩音频文件到满足要求的大小？

千问Audio是阿里云研发的大规模音频语言模型，能够理解多种音频（包括说话人语音、自然声音、音乐、歌声等）。模型的核心能力包括音频转录、提取内容摘要、情感分析、音频事件检测及语音聊天等。

**重要**

- **适用地域：** 本文档仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，推理计算资源仅限于中国内地。如需使用模型，需使用北京地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)。

- **仅供免费体验：** 千问 Audio 模型当前仅提供免费体验， **免费额度用完后不可调用且不支持付费**，对于生产级应用，推荐使用 [千问Omni](https://help.aliyun.com/zh/model-studio/qwen-omni "") 作为替代模型。


## 效果示例

| **应用场景** | **输入示例** | **输出结果** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **应用场景** | **输入示例** | **输出结果** |
| **语音识别与分析**<br>- 识别人类语音 **：** 除了语音转文本，还能分析说话人的性别、年龄段、口音、情绪、意图等。<br>  <br>- 识别自然声音**：**例如汽车喇叭声、钟声、雷声、破碎玻璃声等。<br>  <br>- 识别音乐 **：** 分许音乐，识别音乐中的乐器、节奏、调性、风格等。 | `这段音频里说了什么？说话者是男是女？大致什么年龄？用的是什么语言或方言？听起来什么情绪？` | `这段音频的原始内容是:'这是一封来自四川攀枝花钢铁厂的信'，说话者为男性，年龄大约30岁，使用西南官话-重庆话。听起来情绪平静。` |
| **音频问答**<br>基于音频内容进行提问和回答，例如定位特定信息在音频中出现的时间点。 | `"阿里"出现在这段音频中的什么位置?` | `"阿里" 从第1.53秒开始出现，至第1.87秒结束。` |
| **语音聊天**<br>在不提供任何文本指令的情况下，模型可以直接对语音内容做出回应。 |  | `你可以尝试使用耳塞或者寻找一个相对安静的工作环境来帮助你集中注意力。` |

## 支持的模型

商业版模型

开源版模型

|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **版本** | **上下文长度** | **最大输入** | **最大输出** | **输入成本** | **输出成本** | **免费额度**<br>[（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| **（Token数）** | **（每百万Token）** |
| qwen-audio-turbo | 稳定版 | 8,000 | 6,000 | 1,500 | 目前仅供免费体验。<br>> 免费额度用完后不可调用，推荐使用 [Qwen-Omni](https://help.aliyun.com/zh/model-studio/qwen-omni "") 作为替代模型 | 10万Token<br>有效期：阿里云百炼开通后90天内 |
| qwen-audio-turbo-latest | 最新版 | 8,192 | 6,144 | 2,048 |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **上下文长度** | **最大输入** | **最大输出** | **输入成本** | **输出成本** | **免费额度**<br>[（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| **（Token数）** | **（每千Token）** |
| qwen2-audio-instruct<br>> 相比qwen-audio-chat提升了音频理解能力，且新增了语音聊天能力。 | 8,000 | 6,000 | 1,500 | 目前仅供免费体验。<br>> 免费额度用完后不可调用，推荐使用 [Qwen-Omni](https://help.aliyun.com/zh/model-studio/qwen-omni "") 作为替代模型 | 10万Token<br>有效期：阿里云百炼开通后90天内 |
| qwen-audio-chat |

**音频转换为Token的规则**

每一秒钟的音频对应25个Token。若音频时长不足1秒，则按 25 个Token计算。

## 快速开始

**前提条件**

- 您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

- 如果通过DashScope SDK进行调用，需要 [安装最新版SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


千问Audio模型仅支持通过API调用，暂不支持在阿里云百炼的控制台在线体验。

以下是理解在线音频（通过URL指定，非本地音频）的示例代码。了解 [如何传入本地文件](https://help.aliyun.com/zh/model-studio/audio-language-model#572995b8e2hmp "") 和 [音频文件的限制](https://help.aliyun.com/zh/model-studio/audio-language-model#b6409a628enjc "")。

Python

Java

curl

```python
import dashscope
import os

messages = [\
    {\
        "role": "user",\
        "content": [\
            {"audio": "https://dashscope.oss-cn-beijing.aliyuncs.com/audios/welcome.mp3"},\
            {"text": "这段音频在说什么?"}\
        ]\
    }\
]

response = dashscope.MultiModalConversation.call(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-audio-turbo",
    messages=messages,
    result_format="message"
    )
print("输出结果为：")
print(response["output"]["choices"][0]["message"].content[0]["text"])
```

**响应示例**

```json
输出结果为：
这段音频说的是:'欢迎使用阿里云'
```

```java
import java.util.Arrays;
import java.util.Collections;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversation;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationParam;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationResult;
import com.alibaba.dashscope.common.MultiModalMessage;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.exception.UploadFileException;
import com.alibaba.dashscope.utils.JsonUtils;

public class Main {
    public static void simpleMultiModalConversationCall()
            throws ApiException, NoApiKeyException, UploadFileException {
        MultiModalConversation conv = new MultiModalConversation();
        MultiModalMessage userMessage = MultiModalMessage.builder()
                .role(Role.USER.getValue())
                .content(Arrays.asList(
                        Collections.singletonMap("audio", "https://dashscope.oss-cn-beijing.aliyuncs.com/audios/welcome.mp3"),
                        Collections.singletonMap("text", "这段音频在说什么?")))
                .build();
        MultiModalConversationParam param = MultiModalConversationParam.builder()
                 // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-audio-turbo")
                .message(userMessage)
                .build();
        MultiModalConversationResult result = conv.call(param);
        System.out.println("输出结果为：\n" + result.getOutput().getChoices().get(0).getMessage().getContent().get(0).get("text"));
    }
    public static void main(String[] args) {
        try {
            simpleMultiModalConversationCall();
        } catch (ApiException | NoApiKeyException | UploadFileException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**响应示例**

```json
输出结果为：
这段音频说的是:'欢迎使用阿里云'
```

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H 'Content-Type: application/json' \
-d '{
    "model": "qwen-audio-turbo",
    "input":{
        "messages":[\
            {\
                "role": "user",\
                "content": [\
                    {"audio": "https://dashscope.oss-cn-beijing.aliyuncs.com/audios/welcome.mp3"},\
                    {"text": "这段音频在说什么?"}\
                ]\
            }\
        ]
    }
}'
```

**响应示例**

```json
{
    "output": {
        "choices": [\
            {\
                "finish_reason": "stop",\
                "message": {\
                    "role": "assistant",\
                    "content": [\
                        {\
                            "text": "这段音频说的是:'欢迎使用阿里云'"\
                        }\
                    ]\
                }\
            }\
        ]
    },
    "usage": {
        "audio_tokens": 85,
        "output_tokens": 10,
        "input_tokens": 33
    },
    "request_id": "1341c517-71bf-94f5-862a-18fbddb332e9"
}
```

## **核心能力**

### **语音对话**

在不提供任何文本指令的情况下，模型可以直接对语音内容做出回应。例如：如果音频中包含内容“这种环境下适合做什么”，模型会回复适合做的事情。

> 目前`qwen-audio-turbo-latest、qwen2-audio-instruct`模型支持语音聊天。

Python

Java

curl

```python
import dashscope
import os

messages = [\
    {\
        "role": "user",\
        "content": [\
            {"audio": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20240916/kvkadk/%E6%8E%A8%E8%8D%90%E4%B9%A6.wav"}\
        ]\
    }\
]

response = dashscope.MultiModalConversation.call(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model='qwen2-audio-instruct',
    messages=messages)
print("输出结果为：")
print(response["output"]["choices"][0]["message"].content[0]["text"])
```

**响应示例**

```json
输出结果为：
当然可以，文学类的书籍种类繁多，根据你的兴趣和偏好，我可以给你一些建议。你喜欢哪种类型的文学作品呢？比如是 现代文学、古典文学、科幻小说、历史小说、诗歌、散文等等。
```

```java
import java.util.Arrays;
import java.util.Collections;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversation;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationParam;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationResult;
import com.alibaba.dashscope.common.MultiModalMessage;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.exception.UploadFileException;
import com.alibaba.dashscope.utils.JsonUtils;

public class Main {
    public static void simpleMultiModalConversationCall()
            throws ApiException, NoApiKeyException, UploadFileException {
        MultiModalConversation conv = new MultiModalConversation();
        MultiModalMessage userMessage = MultiModalMessage.builder()
                .role(Role.USER.getValue())
                .content(Arrays.asList(Collections.singletonMap("audio","https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20240916/kvkadk/%E6%8E%A8%E8%8D%90%E4%B9%A6.wav")))
                .build();
        MultiModalConversationParam param = MultiModalConversationParam.builder()
                 // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-audio-turbo")
                .message(userMessage)
                .build();
        MultiModalConversationResult result = conv.call(param);
        System.out.println("输出结果为：\n" + result.getOutput().getChoices().get(0).getMessage().getContent().get(0).get("text"));
    }
    public static void main(String[] args) {
        try {
            simpleMultiModalConversationCall();
        } catch (ApiException | NoApiKeyException | UploadFileException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**响应示例**

```json
输出结果为：
当然可以，文学类的书籍种类繁多，根据你的兴趣和偏好，我可以给你一些建议。你喜欢哪种类型的文学作品呢？比如是 现代文学、古典文学、科幻小说、历史小说、侦探小说、小说、诗歌、散文、戏剧等等。
```

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H 'Content-Type: application/json' \
-d '{
    "model": "qwen-audio-turbo",
    "input":{
        "messages":[\
            {\
                "role": "system",\
                "content": [\
                    {"text": "You are a helpful assistant."}\
                ]\
            },\
            {\
                "role": "user",\
                "content": [\
                    {"audio": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20240916/kvkadk/%E6%8E%A8%E8%8D%90%E4%B9%A6.wav"}                ]\
            }\
        ]
    }
}'
```

**响应示例**

```json
{
    "output": {
        "choices": [\
            {\
                "finish_reason": "stop",\
                "message": {\
                    "role": "assistant",\
                    "content": [\
                        {\
                            "text": "当然可以，不过需要先了解你的兴趣方向。你更喜欢哪种类型的文学作品呢？比如小说、散文、诗歌等。"\
                        }\
                    ]\
                }\
            }\
        ]
    },
    "usage": {
        "audio_tokens": 237,
        "output_tokens": 29,
        "input_tokens": 28
    },
    "request_id": "ae407255-2fed-9e5a-90e6-6dab3178e913"
}
```

### **传入本地文件（Base64 编码或文件路径）**

千问 Audio 提供两种本地文件上传方式：Base64 编码上传和文件路径直接上传。可根据文件大小、SDK类型选择上传方式，具体建议请参见 [如何选择文件上传方式](https://help.aliyun.com/zh/model-studio/audio-language-model#01743dffabulk "")。

文件路径传入

Base64 编码传入

直接向模型传入文件路径。仅 DashScope Python 和 Java SDK 支持，不支持 HTTP 方式。请您参考下表，结合您的编程语言与操作系统指定文件的路径。两种方式均需满足 [支持的音频文件](https://help.aliyun.com/zh/model-studio/audio-language-model#f1a704e20bxby "") 中的要求。

**指定文件的路径**

|     |     |     |     |
| --- | --- | --- | --- |
| **系统** | **SDK** | **传入的文件路径** | **示例** |
| Linux或macOS系统 | Python SDK | file://{文件的绝对路径} | file:///home/images/test.mp3 |
| Java SDK |
| Windows系统 | Python SDK | file://{文件的绝对路径} | file://D:/images/test.mp3 |
| Java SDK | file:///{文件的绝对路径} | file:///D:/images/test.mp3 |

Base64 编码，将文件转换为 Base64 编码字符串，再传入模型。

**传入 Base64 编码字符串的步骤**

1. 文件编码：将本地音频文件转换为 Base64 编码；

2. 构建 [Data URL](https://www.rfc-editor.org/rfc/rfc2397)，格式如下：`data:;base64,{base64_audio}`。`base64_audio`为上一步生成的 Base64 字符串；

3. 调用模型：通过`audio`参数传递`Data URL`并调用模型。


文件路径传入

Base64 编码传入

> 传入文件路径仅支持 DashScope Python 和 Java SDK方式调用，不支持 HTTP 方式。

Python

Java

```python
from dashscope import MultiModalConversation

# 将 ABSOLUTE_PATH/welcome.mp3 替换为本地音频的绝对路径，
# 本地文件的完整路径必须以 file:// 为前缀，以保证路径的合法性，例如：file:///home/images/test.mp3
audio_file_path = "file://ABSOLUTE_PATH/welcome.mp3"
messages = [\
    {\
        "role": "system",\
        "content": [{"text": "You are a helpful assistant."}]},\
    {\
        "role": "user",\
        # 在 audio 参数中传入以 file:// 为前缀的文件路径\
        "content": [{"audio": audio_file_path}, {"text": "音频里在说什么?"}],\
    }\
]

response = MultiModalConversation.call(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen-audio-turbo",
    messages=messages)

print("输出结果为：")
print(response["output"]["choices"][0]["message"].content[0]["text"])
```

**响应示例**

```json
输出结果为：
这段音频说的是:'欢迎使用阿里云'。
```

```java
import java.util.Arrays;
import java.util.HashMap;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversation;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationParam;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationResult;
import com.alibaba.dashscope.common.MultiModalMessage;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.exception.UploadFileException;
import com.alibaba.dashscope.utils.JsonUtils;

public class Main {
    public static void callWithLocalFile()
            throws ApiException, NoApiKeyException, UploadFileException {

        // 请将 ABSOLUTE_PATH/welcome.mp3 替换为本地音频文件的绝对路径
        // 本地文件的完整路径必须以 file:// 为前缀，以保证路径的合法性，例如：file:///home/images/test.mp3
        // 当前测试系统为macOS。如果您使用Windows系统，请用"file:///ABSOLUTE_PATH/welcome.mp3"代替

        String localFilePath = "file://ABSOLUTE_PATH/welcome.mp3";
        MultiModalConversation conv = new MultiModalConversation();
        MultiModalMessage userMessage = MultiModalMessage.builder().role(Role.USER.getValue())
                .content(Arrays.asList(new HashMap<String, Object>(){{put("audio", localFilePath);}},
                        new HashMap<String, Object>(){{put("text", "音频里在说什么?");}}))
                .build();
        MultiModalConversationParam param = MultiModalConversationParam.builder()
                // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-audio-turbo")
                .message(userMessage)
                .build();
        MultiModalConversationResult result = conv.call(param);
        System.out.println("输出结果为：\n" + result.getOutput().getChoices().get(0).getMessage().getContent().get(0).get("text"));
    }
    public static void main(String[] args) {
        try {
            callWithLocalFile();
        } catch (ApiException | NoApiKeyException | UploadFileException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**响应示例**

```json
输出结果为：
音频中说的是：'欢迎使用阿里云'
```

Python

Java

curl

```python
import os
import base64
from dashscope import MultiModalConversation

# 编码函数： 将本地文件转换为 Base64 编码的字符串
def encode_audio(audio_file_path):
    with open(audio_file_path, "rb") as audio_file:
        return base64.b64encode(audio_file.read()).decode("utf-8")

# 请将 ABSOLUTE_PATH/welcome.mp3 替换为本地音频的绝对路径
audio_file_path = "ABSOLUTE_PATH/welcome.mp3"
base64_audio = encode_audio(audio_file_path)

messages = [\
    {\
        "role": "system",\
        "content": [{"text": "You are a helpful assistant."}]},\
    {\
        "role": "user",\
        # 以 Base64 编码方式传入本地文件时，必须要以data:为前缀，以保证文件 URL 的合法性。\
        # 在 Base64 编码数据（base64_audio）前需要包含"base64"，否则也会报错。\
        "content": [{"audio":f"data:;base64,{base64_audio}"},\
                    {"text": "音频里在说什么? "}],\
    }\
]

response = MultiModalConversation.call(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model="qwen2-audio-instruct",
    messages=messages
    )

print(response.output.choices[0].message.content[0])
```

**响应示例**

```json
输出结果为：
这段音频说的是:'欢迎使用阿里云'。
```

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

import java.util.Arrays;
import java.util.Base64;
import java.util.HashMap;

import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversation;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationParam;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationResult;
import com.alibaba.dashscope.common.MultiModalMessage;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.exception.UploadFileException;

public class Main {

    private static String encodeAudioToBase64(String audioPath) throws IOException {
        Path path = Paths.get(audioPath);
        byte[] audioBytes = Files.readAllBytes(path);
        return Base64.getEncoder().encodeToString(audioBytes);
    }

    public static void callWithLocalFile()
            throws ApiException, NoApiKeyException, UploadFileException,IOException{
        // 请将 ABSOLUTE_PATH/welcome.mp3 替换为本地文件的实际路径
        String localFilePath = "ABSOLUTE_PATH/welcome.mp3";
        String base64Audio = encodeAudioToBase64(localFilePath);

        MultiModalConversation conv = new MultiModalConversation();
        MultiModalMessage userMessage = MultiModalMessage.builder().role(Role.USER.getValue())
                 // 以 Base64 编码方式传入本地文件时，必须要以data:为前缀，以保证文件 URL 的合法性。
                 // 在 Base64 编码数据（base64_audio）前需要包含"base64"，否则也会报错。
                .content(Arrays.asList(new HashMap<String, Object>(){{put("audio", "data:;base64," + base64Audio);}},
                        new HashMap<String, Object>(){{put("text", "音频里在说什么?");}}))
                .build();
        MultiModalConversationParam param = MultiModalConversationParam.builder()
                 // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-audio-turbo")
                .message(userMessage)
                .build();
        MultiModalConversationResult result = conv.call(param);
        System.out.println("输出结果为：\n" + result.getOutput().getChoices().get(0).getMessage().getContent().get(0).get("text"));
    }
    public static void main(String[] args) {
        try {
            callWithLocalFile();
        } catch (ApiException | NoApiKeyException | UploadFileException | IOException e) {
            System.out.println(e.getMessage());
        }
        System.exit(0);
    }
}
```

**响应示例**

```json
输出结果为：
音频中说的是：'欢迎使用阿里云'
```

- 将文件转换为 Base64 编码的字符串的方法可参见 [示例代码](https://help.aliyun.com/zh/model-studio/audio-language-model#7eadbfb83dryz "")；

- 为了便于展示，代码中的`"data:;base64,SUQzBAAAAAAAI1RTU0UAAAAPAAADTGF2ZjU4LjI5...."` ，该Base64 编码字符串是截断的。在实际使用中，请务必传入完整的编码字符串。


```curl
curl -X POST https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H 'Content-Type: application/json' \
-d '{
    "model": "qwen-audio-turbo",
    "input":{
        "messages":[\
            {\
                "role": "system",\
                "content": [\
                    {"text": "You are a helpful assistant."}\
                ]\
            },\
            {\
                "role": "user",\
                "content": [\
                    {"audio": "data:;base64,SUQzBAAAAAAAI1RTU0UAAAAPAAADTGF2ZjU4LjI5...."},\
                    {"text": "这段音频在说什么?"}\
                ]\
            }\
        ]
    }
}'
```

### **更多用法**

- [多轮对话](https://help.aliyun.com/zh/model-studio/multi-round-conversation "")

- [流式输出](https://help.aliyun.com/zh/model-studio/stream "")


## **使用限制**

### **支持的音频文件**

- **文件大小：**
  - 以公网 URL 和本地路径传入时：音频文件大小不超过10 MB

  - 以 Base64 编码传入时，编码后的字符串大小不超过 10MB。
- **音频时长：** 音频的时长限制为不超过30秒，如果超过30秒，模型仅处理前30秒的内容。

- **文件格式：** 支持常见编码的音频格式，例如AMR、WAV（CodecID: GSM\_MS）、WAV（PCM）、3GP、3GPP、AAC、MP3等。

- **支持的语言：**中文、英语、粤语、法语、意大利语、西班牙语、德语和日语。


### **音频文件输入方式**

- **公网URL**：提供一个公网可访问的文件地址，支持 HTTP 或 HTTPS 协议。可将本地文件 [上传至OSS](https://help.aliyun.com/zh/oss/user-guide/console-quick-start "") 或 [上传文件获取临时URL](https://help.aliyun.com/zh/model-studio/get-temporary-file-url "")，获取公网 URL。

- **Base64编码传入：** 将文件转换为 Base64 编码字符串。

- **本地文件路径传入：** 直接传入本地文件的路径。


## **应用于生产环境**

因千问 Audio 模型仅供免费体验，存在调用额度限制且不提供付费选项，若计划在生产环境中使用音频理解功能，建议迁移至 [千问Omni](https://help.aliyun.com/zh/model-studio/qwen-omni "") 模型。

- **迁移优势**




| **对比项** | **千问 Audio** | **千问Omni** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **对比项** | **千问 Audio** | **千问Omni** |
| **商业支持** | 仅 **免费体验**，无付费选项 | **支持付费**，可用于生产环境 |
| **功能** | 音频理解能力 | 包含音频在内的全模态能力 |
| **地域限制** | 仅支持北京地域 | 支持国际版（新加坡）和中国大陆版（北京）地域 |

- **迁移方法**

千问Omni模型的使用方法与千问 Audio不同，请参见操作指南 [全模态](https://help.aliyun.com/zh/model-studio/qwen-omni "")。


## API参考

关于千问Audio 模型的输入输出参数，请参见 [千问](https://help.aliyun.com/zh/model-studio/qwen-api-reference/ "")。

## 错误码

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。

## 常见问题

### **如何选择文件上传方式？**

推荐综合考虑SDK 类型、文件大小以及网络稳定性来选择最合适的上传方式。

|     |     |     |
| --- | --- | --- |
| **音频文件规格** | **DashScope SDK（Python、Java）** | **DashScope HTTP** |
| 大于 7MB 小于 10 MB | 传入本地路径 | 仅支持公网 URL，建议使用[阿里云对象存储服务](https://www.aliyun.com/product/oss) |
| 小于 7MB | 传入本地路径 | Base64 编码 |

### **如何压缩音频文件到满足要求的大小？**

- 在线工具：使用 [Compresss](https://www.compresss.com/cn/compress-audio.html) 等在线工具压缩音频文件。

- 代码实现：使用FFmpeg工具，更多用法请参见 [FFmpeg官网](https://ffmpeg.org/download.html)。















```bash
# 基础转换命令示例
# -i，作用：输入文件路径，常用值示例：input.mp3

# -b:a，作用： 设置音频比特率 ，
    # 一般取值有64kbps(低质量，适合语音、低带宽流媒体)、128k（中等质量，适合日常音频、播客）、192kbps（高质量，适合音乐、广播）
    # 比特率越高，音质越好，文件体积越大

# -ar，作用：设置音频采样率，表示每秒采样的次数，
# 一般取值为8000Hz、22050Hz、44100 Hz(标准采样率)
# 采样率越高，文件体积越大

# -ac，作用：设置音频通道数。一般取值有 1（单声道），2（立体声），单声道文件体积更小

# -y，作用：覆盖已存在文件(无需值)# output.mp4，作用：输出文件路径

ffmpeg -i input.mp3 -b:a 128k -ar 44100 -ac 1 output.mp3 -y
```