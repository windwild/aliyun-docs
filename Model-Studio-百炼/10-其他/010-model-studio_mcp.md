### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[模型推理](https://help.aliyun.com/zh/model-studio/model-inference/)[文本生成](https://help.aliyun.com/zh/model-studio/core-concepts/)[工具调用](https://help.aliyun.com/zh/model-studio/tool-calls/)MCP

# MCP

更新时间：2026-02-24 06:59:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：知识检索](https://help.aliyun.com/zh/model-studio/file-search)[下一篇：长上下文（Qwen-Long）](https://help.aliyun.com/zh/model-studio/long-context-qwen-long)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用方式

支持的模型

快速开始

流式输出

参数说明

计费说明

模型上下文协议（Model Context Protocol, MCP）可帮助大模型使用外部工具与数据，相比 Function Calling，MCP 更灵活且易于使用。本文介绍通过 Responses API接入 MCP 的方法。

## **使用方式**

使用 Responses API，在 `tools` 参数中配置MCP Server信息。

> 查找与开通 MCP 服务，请参见 [开通云部署 MCP 服务](https://help.aliyun.com/zh/model-studio/official-and-third-party-mcp#47ed5b5cff6hs "")。

> 仅支持配置SSE协议的 MCP Server。

> 最多添加 10 个 MCP Server。

```python
# 导入依赖与创建客户端...
mcp_tool = {
    "type": "mcp",
    "server_protocol": "sse",
    "server_label": "my-mcp-service",
    "server_description": "MCP 服务功能描述，帮助模型理解使用场景。",
    "server_url": "https://your-mcp-server-endpoint/sse",
    "headers": {
        "Authorization": "Bearer YOUR_TOKEN"
    }
}

response = client.responses.create(
    model="qwen3.5-plus",
    input="你的问题...",
    tools=[mcp_tool]
)

print(response.output_text)
```

## **支持的模型**

- 千问Plus：`qwen3.5-plus`、`qwen3.5-plus-2026-02-15`

- 千问Flash：`qwen3.5-flash`、`qwen3.5-flash-2026-02-23`

- 千问开源：`qwen3.5-397b-a17b`、`qwen3.5-122b-a10b`、`qwen3.5-27b`、`qwen3.5-35b-a3b`。


仅支持通过 Responses API 调用。

## **快速开始**

以接入高德地图 MCP 服务为例，展示如何通过 Responses API 调用 MCP 工具。需要先开通 [高德地图MCP服务](https://bailian.console.aliyun.com/cn-beijing/?tab=app#/mcp-market/detail/amap-maps)。

需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

> 请将示例代码中 MCP 工具配置的 `server_url` 和 `headers` 替换为您实际使用的 MCP 服务信息。

Python

Node.js

curl

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx"（不建议）,
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
)

# MCP 工具配置
mcp_tool = {
    "type": "mcp",
    "server_protocol": "sse",
    "server_label": "amap-maps",
    "server_description": "高德地图MCP Server，提供地图、导航、路径规划、天气查询等能力。",
    "server_url": "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",
    "headers": {
        "Authorization": "Bearer " + os.getenv("DASHSCOPE_API_KEY")
    }
}

response = client.responses.create(
    model="qwen3.5-plus",
    input="从北京到上海驾车怎么走？",
    tools=[mcp_tool]
)

print("[模型回复]")
print(response.output_text)
print(f"\n[Token 用量] 输入: {response.usage.input_tokens}, 输出: {response.usage.output_tokens}, 合计: {response.usage.total_tokens}")
```

Node.js

```nodejs
import OpenAI from "openai";
import process from 'process';

const openai = new OpenAI({
    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey: "sk-xxx",
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: "https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
});

async function main() {
    // MCP 工具配置
    const mcpTool = {
        type: "mcp",
        server_protocol: "sse",
        server_label: "amap-maps",
        server_description: "高德地图MCP Server，提供地图、导航、路径规划、天气查询等能力。",
        server_url: "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",
        headers: {
            "Authorization": "Bearer " + process.env.DASHSCOPE_API_KEY
        }
    };

    const response = await openai.responses.create({
        model: "qwen3.5-plus",
        input: "从北京到上海驾车怎么走？",
        tools: [mcpTool]
    });

    console.log("[模型回复]");
    console.log(response.output_text);
    console.log(`\n[Token 用量] 输入: ${response.usage.input_tokens}, 输出: ${response.usage.output_tokens}, 合计: ${response.usage.total_tokens}`);
}

main();
```

curl

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "从北京到上海驾车怎么走？",
    "tools": [\
        {\
            "type": "mcp",\
            "server_protocol": "sse",\
            "server_label": "amap-maps",\
            "server_description": "高德地图MCP Server，提供地图、导航、路径规划、天气查询等能力。",\
            "server_url": "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",\
            "headers": {\
                "Authorization": "Bearer your-api-key"\
            }\
        }\
    ]
}'
```

运行以上代码可获取如下回复：

```plaintext
[模型回复]
从北京到上海驾车，您可以选择以下路线：

1. 推荐路线（京沪高速）
   - 沿G2京沪高速公路一路向南行驶，途经河北、天津、山东、江苏等省市
   - 全程约1,200公里，预计驾驶时间约13–15小时

2. 备选路线（京台高速转沪昆高速）
   - 沿G3京台高速南下，进入安徽后转入G60沪昆高速前往上海
   - 全程约1,250公里，预计驾驶时间约14–16小时

...

[Token 用量] 输入: 55, 输出: 195, 合计: 250
```

## **流式输出**

MCP 工具调用可能涉及多次外部服务交互，建议启用流式输出，实时获取工具调用过程与回复内容。

Python

Node.js

curl

Python

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
)

mcp_tool = {
    "type": "mcp",
    "server_protocol": "sse",
    "server_label": "amap-maps",
    "server_description": "高德地图MCP Server，提供地图、导航、路径规划、天气查询等能力。",
    "server_url": "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",
    "headers": {
        "Authorization": "Bearer " + os.getenv("DASHSCOPE_API_KEY")
    }
}

stream = client.responses.create(
    model="qwen3.5-plus",
    input="从北京到上海驾车怎么走？",
    tools=[mcp_tool],
    stream=True
)

for event in stream:
    # 模型回复开始
    if event.type == "response.content_part.added":
        print("[模型回复]")
    # 流式文本输出
    elif event.type == "response.output_text.delta":
        print(event.delta, end="", flush=True)
    # 响应完成，输出用量
    elif event.type == "response.completed":
        usage = event.response.usage
        print(f"\n\n[Token 用量] 输入: {usage.input_tokens}, 输出: {usage.output_tokens}, 合计: {usage.total_tokens}")
```

Node.js

```nodejs
import OpenAI from "openai";
import process from 'process';

const openai = new OpenAI({
    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey: "sk-xxx",
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: "https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
});

async function main() {
    const mcpTool = {
        type: "mcp",
        server_protocol: "sse",
        server_label: "amap-maps",
        server_description: "高德地图MCP Server，提供地图、导航、路径规划、天气查询等能力。",
        server_url: "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",
        headers: {
            "Authorization": "Bearer " + process.env.DASHSCOPE_API_KEY
        }
    };

    const stream = await openai.responses.create({
        model: "qwen3.5-plus",
        input: "从北京到上海驾车怎么走？",
        tools: [mcpTool],
        stream: true
    });

    for await (const event of stream) {
        // 模型回复开始
        if (event.type === "response.content_part.added") {
            console.log("[模型回复]");
        }
        // 流式文本输出
        else if (event.type === "response.output_text.delta") {
            process.stdout.write(event.delta);
        }
        // 响应完成，输出用量
        else if (event.type === "response.completed") {
            const usage = event.response.usage;
            console.log(`\n\n[Token 用量] 输入: ${usage.input_tokens}, 输出: ${usage.output_tokens}, 合计: ${usage.total_tokens}`);
        }
    }
}

main();
```

curl

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "从北京到上海驾车怎么走？",
    "tools": [\
        {\
            "type": "mcp",\
            "server_protocol": "sse",\
            "server_label": "amap-maps",\
            "server_description": "高德地图MCP Server，提供地图、导航、路径规划、天气查询等能力。",\
            "server_url": "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",\
            "headers": {\
                "Authorization": "Bearer your-api-key"\
            }\
        }\
    ],
    "stream": true
}'
```

运行以上代码可获取如下回复：

```plaintext
[模型回复]
从北京到上海驾车，您可以选择以下路线：

1. 推荐路线（京沪高速）
   - 沿G2京沪高速公路一路向南行驶，途经河北、天津、山东、江苏等省市
   - 全程约1,200公里，预计驾驶时间约13–15小时

...

[Token 用量] 输入: 55, 输出: 195, 合计: 250
```

## **参数说明**

`mcp` 工具支持以下参数：

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **必填** | **说明** |
| `type` | 是 | 固定为 `"mcp"`。 |
| `server_protocol` | 是 | 与 MCP 服务的通信协议，当前仅支持 `"sse"`。 |
| `server_label` | 是 | MCP 服务的标签名称，用于标识该服务。 |
| `server_description` | 否 | MCP 服务的功能描述，供模型理解该服务的能力与适用场景。建议填写以提升模型调用准确性。 |
| `server_url` | 是 | MCP 服务的端点 URL。 |
| `headers` | 否 | 连接 MCP 服务时携带的请求头，例如 `Authorization` 等认证信息。 | | 示例：<br>```json<br>{<br>    "type": "mcp",<br>    "server_protocol": "sse",<br>    "server_label": "amap-maps",<br>    "server_description": "高德地图MCP Server，提供地图、导航、路径规划、天气查询等能力。",<br>    "server_url": "https://dashscope.aliyuncs.com/api/v1/mcps/amap-maps/sse",<br>    "headers": {<br>        "Authorization": "Bearer " + os.getenv("DASHSCOPE_API_KEY")<br>    }<br>}<br>``` |

## **计费说明**

计费包含以下部分：

- **模型推理费用：** 按模型的 Token 用量计费。

- **MCP 服务费用：** 以各 MCP 服务的计费为准。