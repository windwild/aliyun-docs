### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[工具包/框架](https://help.aliyun.com/zh/model-studio/toolkits-and-frameworks/)Anthropic API兼容

# Anthropic API 兼容

更新时间：2026-02-24 12:47:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenAI兼容-Embedding](https://help.aliyun.com/zh/model-studio/embedding-interfaces-compatible-with-openai)[下一篇：LangChain](https://help.aliyun.com/zh/model-studio/use-bailian-in-langchain)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速接入

支持的模型

详细步骤

开通阿里云百炼

配置环境变量

API 调用-文本对话

API 调用-图片解析

API 调用-视频解析

Anthropic API 兼容性详情

HTTP Header

基础字段

Tool 字段

Message 字段

错误码

阿里云百炼的千问系列模型支持 Anthropic API 兼容接口。通过修改以下参数，即可将原有的 Anthropic 应用迁移至阿里云百炼。

- ANTHROPIC\_API\_KEY（或 ANTHROPIC\_AUTH\_TOKEN）：替换为 [百炼 API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

- ANTHROPIC\_BASE\_URL：替换为百炼的兼容端点地址 `https://dashscope.aliyuncs.com/apps/anthropic`。

- 模型名称（model）：替换为百炼支持的模型名称（例如 `qwen3-plus`），详情请参考 [支持的模型](https://help.aliyun.com/zh/model-studio/anthropic-api-messages#07833dedefft7 "")。


**重要**

本文档仅适用于中国大陆版（北京地域）。

## **快速接入**

文本对话

图片解析

视频解析

```python
import anthropic
import os

client = anthropic.Anthropic(
    api_key=os.getenv("ANTHROPIC_API_KEY"),
    base_url=os.getenv("ANTHROPIC_BASE_URL"),
)
# 迁移至百炼：需配置环境变量 ANTHROPIC_API_KEY 和 ANTHROPIC_BASE_URL，并修改下方的 model 参数。
# 参数兼容性请参考 Anthropic API 兼容性详情
message = client.messages.create(
    model="qwen-plus",   # 设置模型为 qwen-plus
    max_tokens=1024,
    # 深度思考，仅支持部分模型，请参阅支持的模型列表
    thinking={
        "type": "enabled",
        "budget_tokens": 1024
    },
    # 流式输出
    stream=True,
    messages=[\
        {\
            "role": "user",\
            "content": [\
                {\
                    "type": "text",\
                    "text": "你是谁？"\
                }\
            ]\
        }\
    ]
)
print("=== 思考过程 ===")
first_text = True
for chunk in message:
    if chunk.type == "content_block_delta":
        if hasattr(chunk.delta, 'thinking'):
            print(chunk.delta.thinking, end="", flush=True)
        elif hasattr(chunk.delta, 'text'):
            if first_text:
                print("\n\n=== 回答 ===")
                first_text = False
            print(chunk.delta.text, end="", flush=True)
```

```python
import anthropic
import os

client = anthropic.Anthropic(
    api_key=os.getenv("ANTHROPIC_API_KEY"),
    base_url=os.getenv("ANTHROPIC_BASE_URL"),
)
# 迁移至百炼：需配置环境变量 ANTHROPIC_API_KEY 和 ANTHROPIC_BASE_URL，并修改下方的 model 参数。
# 使用 qwen-vl-plus 模型进行多模态调用

message = client.messages.create(
    model="qwen-vl-plus",  # 确保使用支持多模态的模型
    max_tokens=1024,
    # 流式输出
    stream=True,
    messages=[\
        {\
            "role": "user",\
            "content": [\
                {\
                    "type": "image",\
                    "source": {\
                        "type": "url",\
                        "url": "https://data-generator-idst.oss-cn-shanghai.aliyuncs.com/dashscope/image/animal_01.jpg",\
                    },\
                },\
                {\
                    "type": "text",\
                    "text": "描述这张图片的内容。"\
                },\
            ],\
        }\
    ],
)

for chunk in message:
    if chunk.type == "content_block_delta":
        if hasattr(chunk.delta, 'text'):
            print(chunk.delta.text, end="", flush=True)
```

```python
import anthropic
import os

client = anthropic.Anthropic(
    api_key=os.getenv("ANTHROPIC_API_KEY"),
    base_url=os.getenv("ANTHROPIC_BASE_URL"),
)
# 迁移至百炼：需配置环境变量 ANTHROPIC_API_KEY （或 ANTHROPIC_AUTH_TOKEN） 和 ANTHROPIC_BASE_URL。
# 修改下方的 model 参数，使用视觉模型（如 qwen-vl-plus）进行多模态调用

message = client.messages.create(
    model="qwen-vl-plus",  # 确保使用支持多模态的模型
    max_tokens=1024,
    # 流式输出
    stream=True,
    messages=[\
        {\
            "role": "user",\
            "content": [\
                {\
                    "type": "video",\
                    "source": {\
                        "type": "url",\
                        "url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20251208/zpupby/3e81ef38-98f0-4d55-bbb6-259334ca18d0.mp4",\
                    },\
                },\
                {\
                    "type": "text",\
                    "text": "描述这段视频的内容。"\
                },\
            ],\
        }\
    ],
)

for chunk in message:
    if chunk.type == "content_block_delta":
        if hasattr(chunk.delta, 'text'):
            print(chunk.delta.text, end="", flush=True)

```

## 支持的模型

百炼提供的 Anthropic API 兼容服务支持以下千问系列模型：

| **模型系列** | **支持的模型名称（model）** |
| --- | --- |

|     |     |
| --- | --- |
| **模型系列** | **支持的模型名称（model）** |
| 千问Max<br>（部分模型支持思考模式） | qwen3-max、qwen3-max-2026-01-23（支持思考模式）、qwen3-max-preview（支持思考模式） [查看更多](https://help.aliyun.com/zh/model-studio/models#d4ccf72f23jh9 "") |
| 千问Plus | qwen3.5-plus、qwen3.5-plus-2026-02-15、qwen-plus、qwen-plus-latest、qwen-plus-2025-09-11 [查看更多](https://help.aliyun.com/zh/model-studio/models#5ef284d4ed42p "") |
| 千问Flash | qwen3.5-flash、qwen3.5-flash-2026-02-23、qwen-flash、qwen-flash-2025-07-28 [查看更多](https://help.aliyun.com/zh/model-studio/models#13ff05e329blt "") |
| 千问Turbo | qwen-turbo、qwen-turbo-latest [查看更多](https://help.aliyun.com/zh/model-studio/models#947fc66bc1ldf "") |
| 千问Coder<br>（不支持思考模式） | qwen3-coder-next、qwen3-coder-plus、qwen3-coder-plus-2025-09-23、qwen3-coder-flash [查看更多](https://help.aliyun.com/zh/model-studio/models#d698550551bob "") |
| 千问VL<br>（不支持思考模式） | qwen3-vl-plus、qwen3-vl-flash、qwen-vl-max、qwen-vl-plus [查看更多](https://help.aliyun.com/zh/model-studio/models#94b18818a6ywy "") |
| 千问开源模型 | qwen3.5-397b-a17b、qwen3.5-120b-a10b、qwen3.5-27b、qwen3.5-35b-a3b |
| 第三方模型 | - kimi-k2.5、kimi-k2-thinking<br>  <br>- glm-5、glm-4.7、glm-4.6<br>  <br>- MiniMax-M2.5、MiniMax-M2.1 |

模型参数及计费规则请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

## 详细步骤

### **开通阿里云百炼**

如果您是首次访问阿里云百炼服务平台，请按照以下步骤进行开通。

1. 登录[阿里云百炼控制台](https://bailian.console.aliyun.com/)。

2. 若页面顶部显示![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8848210571/p968044.png)，需开通阿里云百炼的模型服务，并获得免费额度。如果未显示该消息，则表示您已经开通。


> 首次开通百炼后，您可领取新人免费额度（有效期：百炼开通后90天内），用于模型推理服务。免费额度领取方法和详情，请查看 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 页面。

**说明**

超出额度或期限将产生费用，开启 [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 功能将避免此情况下产生费用，具体费用请以控制台的实际报价和最终账单为准。

### 配置环境变量

要通过兼容 Anthropic API 的方式，来接入阿里云百炼的模型服务，需要配置以下两个环境变量。

1. `ANTHROPIC_BASE_URL`：设置为 https://dashscope.aliyuncs.com/apps/anthropic。

2. `ANTHROPIC_API_KEY`或`ANTHROPIC_AUTH_TOKEN`：设置为 [阿里云百炼 API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。


> `ANTHROPIC_API_KEY`或`ANTHROPIC_AUTH_TOKEN`均可作为接入认证，只需要设置其一即可。本文以`ANTHROPIC_API_KEY`为例。


macOS

Windows

1. 在终端中执行以下命令，查看默认 Shell 类型。















```bash
echo $SHELL
```

2. 根据 Shell 类型设置环境变量，命令如下：






Zsh



Bash

































```bash
# 用百炼 API KEY 替换 YOUR_DASHSCOPE_API_KEY
echo 'export ANTHROPIC_BASE_URL="https://dashscope.aliyuncs.com/apps/anthropic"' >> ~/.zshrc
echo 'export ANTHROPIC_API_KEY="YOUR_DASHSCOPE_API_KEY"' >> ~/.zshrc
```



















```bash
# 用百炼 API Key 替换 YOUR_DASHSCOPE_API_KEY
echo 'export ANTHROPIC_BASE_URL="https://dashscope.aliyuncs.com/apps/anthropic"' >> ~/.bash_profile
echo 'export ANTHROPIC_API_KEY="YOUR_DASHSCOPE_API_KEY"' >> ~/.bash_profile
```

3. 在终端中执行下列命令，使环境变量生效。






Zsh



Bash

































```bash
source ~/.zshrc
```



















```bash
source ~/.bash_profile
```

4. 打开一个新的终端，执行下列命令，查看环境变量是否生效。















```bash
echo $ANTHROPIC_BASE_URL
echo $ANTHROPIC_API_KEY
```


1. 在 Windows 中，可以通过 CMD 或 PowerShell 将阿里云百炼提供的 Base URL 和 [API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 设置为环境变量。






CMD



PowerShell



















1. 在 CMD 中运行以下命令，设置环境变量。















      ```powershell
      # 用百炼 API Key 替换 YOUR_DASHSCOPE_API_KEY
      setx ANTHROPIC_API_KEY "YOUR_DASHSCOPE_API_KEY"
      setx ANTHROPIC_BASE_URL "https://dashscope.aliyuncs.com/apps/anthropic"
      ```

2. 打开一个新的 CMD 窗口，运行以下命令，检查环境变量是否生效。















      ```powershell
      echo %ANTHROPIC_API_KEY%
      echo %ANTHROPIC_BASE_URL%
      ```


1. 在 PowerShell 中运行以下命令，设置环境变量。















      ```powershell
      # 用百炼 API Key 替换 YOUR_DASHSCOPE_API_KEY
      [Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "YOUR_DASHSCOPE_API_KEY", [EnvironmentVariableTarget]::User)
      [Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://dashscope.aliyuncs.com/apps/anthropic", [EnvironmentVariableTarget]::User)
      ```

2. 打开一个新的 PowerShell 窗口，运行以下命令，检查环境变量是否生效。















      ```powershell
      echo $env:ANTHROPIC_API_KEY
      echo $env:ANTHROPIC_BASE_URL
      ```


### API 调用-文本对话

cURL

Python

TypeScript

```curl
curl -X POST "https://dashscope.aliyuncs.com/apps/anthropic/v1/messages" \
  -H "Content-Type: application/json" \
  -H "x-api-key: ${ANTHROPIC_API_KEY}" \
  -d '{
    "model": "qwen-plus",
    "max_tokens": 1024,
    "stream": true,
    "thinking": {
      "type": "enabled",
      "budget_tokens": 1024
    },
    "system": "You are a helpful assistant",
    "messages": [\
        {\
            "role": "user",\
            "content": [\
                {\
                    "type": "text",\
                    "text": "你是谁？"\
                }\
            ]\
        }\
    ]
}'
```

1. **安装 Anthropic SDK**















```bash
pip install anthropic
```

2. **代码示例**















```python
import anthropic
import os

client = anthropic.Anthropic(
       api_key=os.getenv("ANTHROPIC_API_KEY"),
       base_url=os.getenv("ANTHROPIC_BASE_URL"),
)

message = client.messages.create(
       model="qwen-plus",
       max_tokens=1024,
       stream=True,
       system="you are a helpful assistant",
       # 深度思考，仅支持部分模型，请参阅支持的模型列表
       thinking={
           "type": "enabled",
           "budget_tokens": 1024
       },
       messages=[\
           {\
               "role": "user",\
               "content": [\
                   {\
                       "type": "text",\
                       "text": "你是谁？"\
                   }\
               ]\
           }\
       ]
)

print("=== 思考过程 ===")
first_text = True
for chunk in message:
       if chunk.type == "content_block_delta":
           if hasattr(chunk.delta, 'thinking'):
               print(chunk.delta.thinking, end="", flush=True)
           elif hasattr(chunk.delta, 'text'):
               if first_text:
                   print("\n\n=== 回答 ===")
                   first_text = False
               print(chunk.delta.text, end="", flush=True)
```


1. **安装 Anthropic TypeScript SDK**















```bash
npm install @anthropic-ai/sdk
```

2. **代码示例**















```typescript
import Anthropic from "@anthropic-ai/sdk";

async function main() {
     const anthropic = new Anthropic({
       apiKey: process.env.ANTHROPIC_API_KEY,
       baseURL: process.env.ANTHROPIC_BASE_URL,
     });

     const stream = await anthropic.messages.create({
       model: "qwen-plus",
       max_tokens: 1024,
       stream: true,
       // 深度思考，仅支持部分模型，请参阅支持的模型列表
       thinking: { type: "enabled", budget_tokens: 1024 },
       system: "You are a helpful assistant",
       messages: [{\
         role: "user",\
         content: [\
           {\
             type: "text",\
             text: "你是谁？"\
           }\
         ]\
       }]
     });

     console.log("=== 思考过程 ===");
     let firstText = true;

     for await (const chunk of stream) {
       if (chunk.type === "content_block_delta") {
         if ('thinking' in chunk.delta) {
           process.stdout.write(chunk.delta.thinking);
         } else if ('text' in chunk.delta) {
           if (firstText) {
             console.log("\n\n=== 回答 ===");
             firstText = false;
           }
           process.stdout.write(chunk.delta.text);
         }
       }
     }
     console.log();
}

main().catch(console.error);
```


### API 调用-图片解析

cURL

Python

TypeScript

cURL 调用需要手动拼接完整的请求路径，即在 `ANTHROPIC_BASE_URL` 后加上 API 端点 `/v1/messages`。

```curl
curl -X POST "https://dashscope.aliyuncs.com/apps/anthropic/v1/messages" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ANTHROPIC_API_KEY}" \
  -d '{
      "model": "qwen-vl-plus",
      "max_tokens": 1024,
      "stream": true,
      "messages": [\
                    {\
                        "role": "user",\
                        "content": [\
                            {\
                                "type": "image",\
                                "source": {\
                                    "type": "url",\
                                    "url": "https://data-generator-idst.oss-cn-shanghai.aliyuncs.com/dashscope/image/animal_01.jpg"\
                                }\
                            },\
                            {\
                                "type": "text",\
                                "text": "描述这张图片的内容。"\
                            }\
                        ]\
                    }\
                ]
  }'
```

1. **安装 Anthropic SDK**















```bash
pip install anthropic
```

2. **代码示例**















```python
import anthropic
import os

client = anthropic.Anthropic(
       api_key=os.getenv("ANTHROPIC_API_KEY"),
       base_url=os.getenv("ANTHROPIC_BASE_URL"),
)
# 迁移至百炼：需配置环境变量 ANTHROPIC_API_KEY （或 ANTHROPIC_AUTH_TOKEN） 和 ANTHROPIC_BASE_URL。
# 修改下方的 model 参数，使用视觉模型（如 qwen-vl-plus）进行多模态调用

message = client.messages.create(
       model="qwen-vl-plus",  # 确保使用支持多模态的模型
       max_tokens=1024,
       # 流式输出
       stream=True,
       messages=[\
           {\
               "role": "user",\
               "content": [\
                   {\
                       "type": "image",\
                       "source": {\
                           "type": "url",\
                           "url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250414/mqqmiy/animal_01.jpg",\
                       },\
                   },\
                   {\
                       "type": "text",\
                       "text": "描述这张图片的内容。"\
                   },\
               ],\
           }\
       ],
)

for chunk in message:
       if chunk.type == "content_block_delta":
           if hasattr(chunk.delta, 'text'):
               print(chunk.delta.text, end="", flush=True)

```


1. **安装 Anthropic TypeScript SDK**















```bash
npm install @anthropic-ai/sdk
```

2. **代码示例**















```typescript
import Anthropic from "@anthropic-ai/sdk";

async function main() {
     const anthropic = new Anthropic({
       apiKey: process.env.ANTHROPIC_API_KEY,
       baseURL: process.env.ANTHROPIC_BASE_URL,
     });

     // 使用 qwen-vl-plus 模型进行多模态调用
     const stream = await anthropic.messages.create({
       model: "qwen-vl-plus",
       max_tokens: 1024,
       // 流式输出
       stream: true,
       messages: [\
         {\
           role: "user",\
           content: [\
             {\
               type: "image",\
               source: {\
                 type: "url",\
                 url: "https://data-generator-idst.oss-cn-shanghai.aliyuncs.com/dashscope/image/animal_01.jpg",\
               },\
             },\
             {\
               type: "text",\
               text: "描述这张图片的内容。",\
             },\
           ],\
         },\
       ],
     });

     for await (const chunk of stream) {
       if (chunk.type === "content_block_delta") {
         if ('text' in chunk.delta) {
           process.stdout.write(chunk.delta.text);
         }
       }
     }
     console.log();
}

main().catch(console.error);
```


### API 调用-视频解析

cURL

Python

TypeScript

cURL 调用需要手动拼接完整的请求路径，即在 `ANTHROPIC_BASE_URL` 后加上 API 端点 `/v1/messages`。

```curl
curl -X POST "https://dashscope.aliyuncs.com/apps/anthropic/v1/messages" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ANTHROPIC_API_KEY}" \
  -d '{
      "model": "qwen-vl-plus",
      "max_tokens": 1024,
      "stream": true,
      "messages": [\
                    {\
                        "role": "user",\
                        "content": [\
                            {\
                                "type": "video",\
                                "source": {\
                                    "type": "url",\
                                    "url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20251208/zpupby/3e81ef38-98f0-4d55-bbb6-259334ca18d0.mp4"\
                                }\
                            },\
                            {\
                                "type": "text",\
                                "text": "描述这段视频的内容。"\
                            }\
                        ]\
                    }\
                ]
  }'
```

1. **安装 Anthropic SDK**















```bash
pip install anthropic
```

2. **代码示例**















```python
import anthropic
import os

client = anthropic.Anthropic(
       api_key=os.getenv("ANTHROPIC_API_KEY"),
       base_url=os.getenv("ANTHROPIC_BASE_URL"),
)
# 迁移至百炼：需配置环境变量 ANTHROPIC_API_KEY 和 ANTHROPIC_BASE_URL，并修改下方的 model 参数。
# 使用 qwen-vl-plus 模型进行多模态调用

message = client.messages.create(
       model="qwen-vl-plus",  # 确保使用支持多模态的模型
       max_tokens=1024,
       # 流式输出
       stream=True,
       messages=[\
           {\
               "role": "user",\
               "content": [\
                   {\
                       "type": "video",\
                       "source": {\
                           "type": "url",\
                           "url": "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20251208/zpupby/3e81ef38-98f0-4d55-bbb6-259334ca18d0.mp4",\
                       },\
                   },\
                   {\
                       "type": "text",\
                       "text": "描述这段视频的内容。"\
                   },\
               ],\
           }\
       ],
)

for chunk in message:
       if chunk.type == "content_block_delta":
           if hasattr(chunk.delta, 'text'):
               print(chunk.delta.text, end="", flush=True)

```


1. **安装 Anthropic TypeScript SDK**















```bash
npm install @anthropic-ai/sdk
```

2. **代码示例**















```typescript
import Anthropic from "@anthropic-ai/sdk";

async function main() {
     const anthropic = new Anthropic({
       apiKey: process.env.ANTHROPIC_API_KEY,
       baseURL: process.env.ANTHROPIC_BASE_URL,
     });

     // 使用 qwen-vl-plus 模型进行多模态调用
     const stream = await anthropic.messages.create({
       model: "qwen-vl-plus",
       max_tokens: 1024,
       // 流式输出
       stream: true,
       messages: [\
         {\
           role: "user",\
           content: [\
             {\
               type: "video",\
               source: {\
                 type: "url",\
                 url: "https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20251208/zpupby/3e81ef38-98f0-4d55-bbb6-259334ca18d0.mp4",\
               },\
             },\
             {\
               type: "text",\
               text: "描述这段视频的内容。",\
             },\
           ],\
         },\
       ],
     });

     for await (const chunk of stream) {
       if (chunk.type === "content_block_delta") {
         if ('text' in chunk.delta) {
           process.stdout.write(chunk.delta.text);
         }
       }
     }
     console.log();
}

main().catch(console.error);
```


## Anthropic API 兼容性详情

### **HTTP Header**

| **字段** | **是否支持** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **是否支持** |
| x-api-key | 支持 |
| Authorization Bearer | 支持 |
| anthropic-beta/anthropic-version | 不支持 |

### **基础字段**

| **字段** | **是否支持** | **说明** | **示例值** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段** | **是否支持** | **说明** | **示例值** |
| model | 支持 | 模型名称，支持范围见 [支持的模型](https://help.aliyun.com/zh/model-studio/anthropic-api-messages#07833dedefft7 "") | qwen-plus |
| max\_tokens | 支持 | 生成 token 的最大数量 | 1024 |
| container | 不支持 | - | - |
| mcp\_servers | 不支持 | - | - |
| metadata | 不支持 | - | - |
| service\_tier | 不支持 | - | - |
| stop\_sequences | 支持 | 会引发模型停止生成的自定义文本序列 | \["}"\] |
| stream | 支持 | 流式输出 | True |
| system | 支持 | 系统提示词 | You are a helpful assistant |
| temperature | 支持 | 温度系数，用于控制模型生成文本的多样性 | 1.0 |
| thinking | 支持 | 思考模式，开启后模型在生成回复前会先进行推理，以提升回答准确度。部分模型不支持，详见 [支持的模型](https://help.aliyun.com/zh/model-studio/anthropic-api-messages#07833dedefft7 "") | {"type": "enabled", "budget\_tokens": 1024} |
| top\_k | 支持 | 生成过程中采样候选集的大小 | 10 |
| top\_p | 支持 | 核采样的概率阈值，控制模型生成文本的多样性 | 0.1 |

> 由于 temperature 与 top\_p 均可以控制生成文本的多样性，因此建议只设置其中一个值。更多说明，请参见 [文本生成模型概述](https://help.aliyun.com/zh/model-studio/text-generation#ad7b336bec5fw "")。

### **Tool 字段**

**tools**

| **字段** | **是否支持** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **是否支持** |
| name | 支持 |
| input\_schema | 支持 |
| description | 支持 |
| cache\_control | 支持 |

**tool\_choice**

| **值** | **是否支持** |
| --- | --- |

|     |     |
| --- | --- |
| **值** | **是否支持** |
| none | 支持 |
| auto | 支持 |
| any | 支持 |
| tool | 支持 |

### **Message 字段**

| **字段** | **类型** | **子字段** | **是否支持** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **字段** | **类型** | **子字段** | **是否支持** | **说明** |
| content | string | - | 支持 | 纯文本内容。 |
| array, type="text" | text | 支持 | 文本块的内容。 |
| cache\_control | 支持 | 用于控制该文本块的缓存行为。 |
| citations | 不支持 | - |
| array, type="image" | source.type | 支持 | 指定图片来源的类型。有效值为 `"url"` 或 `"base64"`。 |
| source.media\_type | 支持 | 当 `source.type` 为 `"base64"` 时必需。指定图片类型。 |
| source.data | 支持 | 当 `source.type` 为 `"base64"` 时必需。图片的 Base64 编码字符串。 |
| source.url | 支持 | 当 `source.type` 为 `"url"` 时必需。图片的公开可访问 URL 地址。 |
| array, type="video" | source.type | 支持 | 指定视频来源的类型。有效值为 `"url"` 或 `"base64"`。 |
| source.media\_type | 支持 | 当 `source.type` 为 `"base64"` 时必需。指定视频类型。 |
| source.data | 支持 | 当 `source.type` 为 `"base64"` 时必需。视频的 Base64 编码字符串。 |
| source.url | 支持 | 当 `source.type` 为 `"url"` 时必需。视频的公开可访问 URL 地址。 |
| array, type="document" | - | 不支持 | - |
| array, type="search\_result" | - | 不支持 | - |
| array, type="thinking" | - | 不支持 | - |
| array, type="redacted\_thinking" | - | 不支持 | - |
| array, type="tool\_use" | id | 支持 | 工具调用的唯一标识符。 |
| input | 支持 | 调用工具时传入的参数对象。 |
| name | 支持 | 被调用的工具名称。 |
| cache\_control | 支持 | 用于控制该工具调用缓存行为。 |
| array, type="tool\_result" | tool\_use\_id | 支持 | 与本次结果对应的 `tool_use` 的 ID。 |
| content | 支持 | 工具执行后返回的结果，通常为字符串或 JSON 字符串。 |
| cache\_control | 支持 | 用于控制该工具结果的缓存行为。 |
| is\_error | 不支持 | - |
| array, type="server\_tool\_use" | - | 不支持 | - |
| array, type="web\_search\_tool\_result" | - | 不支持 | - |
| array, type="code\_execution\_tool\_result" | - | 不支持 | - |
| array, type="mcp\_tool\_use" | - | 不支持 | - |
| array, type="mcp\_tool\_result" | - | 不支持 | - |
| array, type="container\_upload" | - | 不支持 | - |

## **错误码**

| **HTTP状态码** | **错误类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **HTTP状态码** | **错误类型** | **说明** |
| 400 | invalid\_request\_error | 请求格式或内容存在问题。具体原因可能包括：缺少必要的请求参数、参数值的数据类型不正确等。 |
| 400 | Arrearage | 账户欠费导致服务暂停，请充值后重试。 |
| 403 | authentication\_error | API Key 存在问题。具体原因可能包括：请求头中未提供 API Key、提供的 API Key 不正确等。 |
| 404 | not\_found\_error | 未找到请求的资源。具体原因可能包括：兼容接口拼写有误、请求头中的模型不存在等。 |
| 429 | rate\_limit\_error | 账户达到了速率限制，建议降低请求频率。 |
| 500 | api\_error | 发生了一个通用的服务器内部错误，建议稍后重试。 |
| 529 | overloaded\_error | API 服务器当前负载过高，暂时无法处理新的请求。 |