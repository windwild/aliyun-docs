### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[工具包/框架](https://help.aliyun.com/zh/model-studio/toolkits-and-frameworks/)OpenAI兼容-Responses

# OpenAI Responses接口兼容

更新时间：2026-02-24 07:00:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenAI兼容-Chat](https://help.aliyun.com/zh/model-studio/compatibility-of-openai-with-dashscope)[下一篇：OpenAI兼容-Completions](https://help.aliyun.com/zh/model-studio/completions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

支持的模型

服务地址

代码示例

基础调用

多轮对话

流式输出

调用内置工具

从 Chat Completions 迁移到 Responses API

1\. 更新端点地址和 base\_url

2\. 更新响应处理

3\. 简化多轮对话管理

4\. 使用内置工具

常见问题

相关文档

阿里云百炼的通义千问模型支持 OpenAI 兼容 Responses 接口。作为Chat Completions API的演进版本，Responses API能够以更简洁的方式提供智能体原生功能。

**相较于OpenAI Chat Completions API 的优势：**

- **内置工具**：内置联网搜索、网页抓取、代码解释器、文搜图、图搜图等工具，可在处理复杂任务时获得更佳效果，详情参考 [调用内置工具](https://help.aliyun.com/zh/model-studio/compatibility-with-openai-responses-api#11cd08d0ffnxw "")。

- **更灵活的输入**：支持直接传入字符串作为模型输入，也兼容 Chat 格式的消息数组。

- **简化上下文管理**：通过传递上一轮响应的 `previous_response_id`，无需手动构建完整的消息历史数组。


输入输出参数说明请参考 [OpenAI Responses API参考](https://help.aliyun.com/zh/model-studio/qwen-api-via-openai-responses "")。

## 前提条件

您需要先 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。若通过 OpenAI SDK 进行调用，需要 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

## 支持的模型

当前支持`qwen3.5-plus`、`qwen3.5-plus-2026-02-15`、`qwen3.5-flash`、`qwen3.5-flash-2026-02-23`、`qwen3.5-397b-a17b`、`qwen3.5-122b-a10b`、`qwen3.5-27b`、`qwen3.5-35b-a3b`、`qwen3-max`、`qwen3-max-2026-01-23`。

## 服务地址

华北2（北京）

新加坡

SDK 调用配置的`base_url`：`https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1`

HTTP 请求地址：`POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses`

SDK 调用配置的`base_url`：`https://dashscope-intl.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1`

HTTP 请求地址：`POST https://dashscope-intl.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses`

## 代码示例

### **基础调用**

最简单的调用方式，发送一条消息并获取模型回复。

Python

Node.js

curl

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用百炼 API Key 将下行替换为：api_key="sk-xxx"
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1",
)

response = client.responses.create(
    model="qwen3.5-plus",
    input="你能做些什么？"
)

# 获取模型回复
# print(response.model_dump_json())
print(response.output_text)
```

```nodejs
import OpenAI from "openai";

const openai = new OpenAI({
    // 若没有配置环境变量，请用百炼 API Key 将下行替换为：apiKey: "sk-xxx"
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: "https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
});

async function main() {
    const response = await openai.responses.create({
        model: "qwen3.5-plus",
        input: "你能做些什么？"
    });

    // 获取模型回复
    console.log(response.output_text);
}

main();
```

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "你能做些什么？"
}'
```

**响应示例**

> 以下为API返回的完整响应。

```json
{
    "created_at": 1771225825,
    "id": "0c842a11-c7d1-45da-b7ec-4e668c389xxx",
    "model": "qwen3.5-plus",
    "object": "response",
    "output": [\
        {\
            "id": "msg_0bdb8ab9-f1de-4db6-82c8-6c1185b91xxx",\
            "summary": [\
                {\
                    "text": "Thinking Process:\n\n1.  **Analyze the Request ...",\
                    "type": "summary_text"\
                }\
            ],\
            "type": "reasoning"\
        },\
        {\
            "content": [\
                {\
                    "annotations": [],\
                    "text": "你好！作为一个人工智能助手，我可以协助你完成多种任务。以下是我的一些主要能力：\n\n1.  **文字创作与编辑**\n    *   撰写邮件、文章、报告、故事或社交媒体文案。\n    *   润色、改写或总结现有的文本内容。\n\n2.  **编程与技术支持**\n    *   编写、调试或解释代码（支持多种编程语言，如 Python、JavaScript、C++ 等）。\n    *   提供技术概念的解释和解决方案建议。\n\n3.  **知识问答与学习**\n    *   回答各领域的问题（我的知识更新至 2026 年）。\n    *   协助学习新概念、制定学习计划或解答习题。\n\n4.  **语言翻译**\n    *   支持多种语言之间的互译，帮助你跨越语言障碍。\n\n5.  **数据分析与整理**\n    *   协助整理信息、提取关键点或进行逻辑分析。\n    *   帮助格式化数据或生成表格结构。\n\n6.  **创意与头脑风暴**\n    *   提供创意灵感、策划方案或建议。\n    *   陪你聊天，提供情感支持或生活建议。\n\n有什么具体需要我帮忙的吗？随时告诉我！",\
                    "type": "output_text"\
                }\
            ],\
            "id": "msg_c8bb3db1-d235-44e7-9704-55b584022xxx",\
            "role": "assistant",\
            "status": "completed",\
            "type": "message"\
        }\
    ],
    "parallel_tool_calls": false,
    "status": "completed",
    "tool_choice": "auto",
    "tools": [],
    "usage": {
        "input_tokens": 49,
        "input_tokens_details": {
            "cached_tokens": 0
        },
        "output_tokens": 1384,
        "output_tokens_details": {
            "reasoning_tokens": 1110
        },
        "total_tokens": 1433,
        "x_details": [\
            {\
                "input_tokens": 49,\
                "output_tokens": 1384,\
                "output_tokens_details": {\
                    "reasoning_tokens": 1110\
                },\
                "total_tokens": 1433,\
                "x_billing_type": "response_api"\
            }\
        ]
    }
}
```

### **多轮对话**

通过 `previous_response_id` 参数自动关联上下文，无需手动构建消息历史，当前响应`id`有效期为7天。

> `previous_response_id` 应传入上一轮响应中的顶层 `id` （`f0dbb153-117f-9bbf-8176-5284b47f3xxx`，UUID格式），而不是 `output` 数组内消息的 `id` （`msg_56c860c4-3ad8-4a96-8553-d2f94c259xxx`）。

Python

Node.js

curl

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1",
)

# 第一轮对话
response1 = client.responses.create(
    model="qwen3.5-plus",
    input="我的名字是张三，请记住。"
)
print(f"第一轮回复: {response1.output_text}")

# 第二轮对话 - 使用 previous_response_id 关联上下文，响应id有效期为7天
response2 = client.responses.create(
    model="qwen3.5-plus",
    input="你还记得我的名字吗？",
    previous_response_id=response1.id
)
print(f"第二轮回复: {response2.output_text}")
```

```nodejs
import OpenAI from "openai";

const openai = new OpenAI({
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: "https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
});

async function main() {
    // 第一轮对话
    const response1 = await openai.responses.create({
        model: "qwen3.5-plus",
        input: "我的名字是张三，请记住。"
    });
    console.log(`第一轮回复: ${response1.output_text}`);

    // 第二轮对话 - 使用 previous_response_id 关联上下文，响应id有效期为7天
    const response2 = await openai.responses.create({
        model: "qwen3.5-plus",
        input: "你还记得我的名字吗？",
        previous_response_id: response1.id
    });
    console.log(`第二轮回复: ${response2.output_text}`);
}

main();
```

```curl
# 第一轮对话
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "我的名字是张三，请记住。"
}'

# 第二轮对话 - 使用上一轮返回的 id 作为 previous_response_id
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "你还记得我的名字吗？",
    "previous_response_id": "第一轮返回的响应id"
}'
```

**第二轮对话响应示例**

```json
{
  "id": "f0dbb153-117f-9bbf-8176-5284b47f3xxx",
  "created_at": 1769169951.0,
  "model": "qwen3.5-plus",
  "object": "response",
  "status": "completed",
  "output": [\
    {\
      "id": "msg_56c860c4-3ad8-4a96-8553-d2f94c259xxx",\
      "type": "message",\
      "role": "assistant",\
      "status": "completed",\
      "content": [\
        {\
          "type": "output_text",\
          "text": "当然记得，你的名字是张三！",\
          "annotations": []\
        }\
      ]\
    }\
  ],
  "usage": {
    "input_tokens": 73,
    "output_tokens": 10,
    "total_tokens": 83,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens_details": {
      "reasoning_tokens": 0
    }
  }
}
```

**说明：** 第二轮对话的 `input_tokens` 为 73，包含了第一轮的上下文，模型成功记住了名字"张三"。

### **流式输出**

通过流式输出实时接收模型生成的内容，适合长文本生成场景。

Python

Node.js

curl

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1",
)

stream = client.responses.create(
    model="qwen3.5-plus",
    input="请简单介绍一下人工智能。",
    stream=True
)

print("开始接收流式输出:")
for event in stream:
    # print(event.model_dump_json())  # 取消注释以查看原始事件响应
    if event.type == 'response.output_text.delta':
        # 实时打印增量文本
        print(event.delta, end='', flush=True)
    elif event.type == 'response.completed':
        print("\n流式输出完成")
        print(f"总 Token 数: {event.response.usage.total_tokens}")
```

```nodejs
import OpenAI from "openai";

const openai = new OpenAI({
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: "https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
});

async function main() {
    const stream = await openai.responses.create({
        model: "qwen3.5-plus",
        input: "请简单介绍一下人工智能。",
        stream: true
    });

    console.log("开始接收流式输出:");
    for await (const event of stream) {
        // console.log(JSON.stringify(event));  // 取消注释以查看原始事件响应
        if (event.type === 'response.output_text.delta') {
            process.stdout.write(event.delta);
        } else if (event.type === 'response.completed') {
            console.log("\n流式输出完成");
            console.log(`总 Token 数: ${event.response.usage.total_tokens}`);
        }
    }
}

main();
```

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "请简单介绍一下人工智能。",
    "stream": true
}'
```

**响应示例**

```json
{"response":{"id":"47a71e7d-868c-4204-9693-ef8ff9058xxx","created_at":1769417481.0,"error":null,"incomplete_details":null,"instructions":null,"metadata":null,"model":"","object":"response","output":[],"parallel_tool_calls":false,"temperature":null,"tool_choice":"auto","tools":[],"top_p":null,"background":null,"completed_at":null,"conversation":null,"max_output_tokens":null,"max_tool_calls":null,"previous_response_id":null,"prompt":null,"prompt_cache_key":null,"prompt_cache_retention":null,"reasoning":null,"safety_identifier":null,"service_tier":null,"status":"queued","text":null,"top_logprobs":null,"truncation":null,"usage":null,"user":null},"sequence_number":0,"type":"response.created"}
{"response":{"id":"47a71e7d-868c-4204-9693-ef8ff9058xxx","created_at":1769417481.0,"error":null,"incomplete_details":null,"instructions":null,"metadata":null,"model":"","object":"response","output":[],"parallel_tool_calls":false,"temperature":null,"tool_choice":"auto","tools":[],"top_p":null,"background":null,"completed_at":null,"conversation":null,"max_output_tokens":null,"max_tool_calls":null,"previous_response_id":null,"prompt":null,"prompt_cache_key":null,"prompt_cache_retention":null,"reasoning":null,"safety_identifier":null,"service_tier":null,"status":"in_progress","text":null,"top_logprobs":null,"truncation":null,"usage":null,"user":null},"sequence_number":1,"type":"response.in_progress"}
{"item":{"id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","content":[],"role":"assistant","status":"in_progress","type":"message"},"output_index":0,"sequence_number":2,"type":"response.output_item.added"}
{"content_index":0,"item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","output_index":0,"part":{"annotations":[],"text":"","type":"output_text","logprobs":null},"sequence_number":3,"type":"response.content_part.added"}
{"content_index":0,"delta":"人工智能","item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":4,"type":"response.output_text.delta"}
{"content_index":0,"delta":"（Art","item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":5,"type":"response.output_text.delta"}
{"content_index":0,"delta":"ificial Intelligence，","item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":6,"type":"response.output_text.delta"}
{"content_index":0,"delta":"简称 AI）","item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":7,"type":"response.output_text.delta"}
... (省略中间事件) ...
{"content_index":0,"delta":"领域，正在深刻改变我们的","item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":38,"type":"response.output_text.delta"}
{"content_index":0,"delta":"生活和工作方式","item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":39,"type":"response.output_text.delta"}
{"content_index":0,"delta":"。","item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":40,"type":"response.output_text.delta"}
{"content_index":0,"item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","logprobs":[],"output_index":0,"sequence_number":41,"text":"人工智能（Artificial Intelligence，简称 AI）是指由计算机系统模拟人类智能行为的技术和科学。xxxx","type":"response.output_text.done"}
{"content_index":0,"item_id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","output_index":0,"part":{"annotations":[],"text":"人工智能（Artificial Intelligence，简称 AI）是指由计算机系统模拟人类智能行为的技术和科学。xxx","type":"output_text","logprobs":null},"sequence_number":42,"type":"response.content_part.done"}
{"item":{"id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","content":[{"annotations":[],"text":"人工智能（Artificial Intelligence，简称 AI）是指由计算机系统模拟人类智能行为的技术和科学。它旨在让机器能够执行通常需要人类智能才能完成的任务，例如：\n\n- **学习**（如通过数据训练模型）  \n- **推理**（如逻辑判断和问题求解）  \n- **感知**（如识别图像、语音或文字）  \n- **理解语言**（如自然语言处理）  \n- **决策**（如在复杂环境中做出最优选择）\n\n人工智能可分为**弱人工智能**（专注于特定任务，如语音助手、推荐系统）和**强人工智能**（具备类似人类的通用智能，目前尚未实现）。\n\n当前，AI 已广泛应用于医疗、金融、交通、教育、娱乐等多个领域，正在深刻改变我们的生活和工作方式。","type":"output_text","logprobs":null}],"role":"assistant","status":"completed","type":"message"},"output_index":0,"sequence_number":43,"type":"response.output_item.done"}
{"response":{"id":"47a71e7d-868c-4204-9693-ef8ff9058xxx","created_at":1769417481.0,"error":null,"incomplete_details":null,"instructions":null,"metadata":null,"model":"qwen3.5-plus","object":"response","output":[{"id":"msg_16db29d6-c1d3-47d7-9177-0fba81964xxx","content":[{"annotations":[],"text":"人工智能（Artificial Intelligence，简称 AI）是xxxxxx","type":"output_text","logprobs":null}],"role":"assistant","status":"completed","type":"message"}],"parallel_tool_calls":false,"temperature":null,"tool_choice":"auto","tools":[],"top_p":null,"background":null,"completed_at":null,"conversation":null,"max_output_tokens":null,"max_tool_calls":null,"previous_response_id":null,"prompt":null,"prompt_cache_key":null,"prompt_cache_retention":null,"reasoning":null,"safety_identifier":null,"service_tier":null,"status":"completed","text":null,"top_logprobs":null,"truncation":null,"usage":{"input_tokens":37,"input_tokens_details":{"cached_tokens":0},"output_tokens":166,"output_tokens_details":{"reasoning_tokens":0},"total_tokens":203},"user":null},"sequence_number":44,"type":"response.completed"}
```

### **调用内置工具**

开启内置工具可在处理复杂任务时获得更佳效果，当前网页抓取与代码解释器工具限时免费，支持的工具请参见 [工具调用](https://help.aliyun.com/zh/model-studio/tool-calls/ "")。

Python

Node.js

curl

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1",
)

response = client.responses.create(
    model="qwen3.5-plus",
    input="帮我找一下阿里云官网，并提取首页的关键信息",
    # 建议同时开启内置工具以取得最佳效果
    tools=[\
        {"type": "web_search"},\
        {"type": "code_interpreter"},\
        {"type": "web_extractor"}\
    ],
    extra_body={"enable_thinking": True}
)

# 取消以下注释查看中间过程输出
# print(response.output)
print(response.output_text)
```

```nodejs
import OpenAI from "openai";

const openai = new OpenAI({
    apiKey: process.env.DASHSCOPE_API_KEY,
    baseURL: "https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1"
});

async function main() {
    const response = await openai.responses.create({
        model: "qwen3.5-plus",
        input: "帮我找一下阿里云官网，并提取首页的关键信息",
        tools: [\
            { type: "web_search" },\
            { type: "code_interpreter" },\
            { type: "web_extractor" }\
        ],
        enable_thinking: true
    });

    for (const item of response.output) {
        if (item.type === "reasoning") {
            console.log("模型正在思考...");
        } else if (item.type === "web_search_call") {
            console.log(`搜索查询: ${item.action.query}`);
        } else if (item.type === "web_extractor_call") {
            console.log("正在抽取网页内容...");
        } else if (item.type === "message") {
            console.log(`回复内容: ${item.content[0].text}`);
        }
    }
}

main();
```

```curl
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "帮我找一下阿里云官网，并提取首页的关键信息",
    "tools": [\
        {\
            "type": "web_search"\
        },\
        {\
            "type": "code_interpreter"\
        },\
        {\
            "type": "web_extractor"\
        }\
    ],
    "enable_thinking": true
}'
```

**响应示例**

```json
{
    "id": "69258b21-5099-9d09-92e8-8492b1955xxx",
    "object": "response",
    "status": "completed",
    "output": [\
        {\
            "type": "reasoning",\
            "summary": [\
                {\
                    "type": "summary_text",\
                    "text": "用户要求找阿里云官网并提取信息..."\
                }\
            ]\
        },\
        {\
            "type": "web_search_call",\
            "status": "completed",\
            "action": {\
                "query": "阿里云官网",\
                "type": "search",\
                "sources": [\
                    {\
                        "type": "url",\
                        "url": "https://cn.aliyun.com/"\
                    },\
                    {\
                        "type": "url",\
                        "url": "https://www.alibabacloud.com/zh"\
                    }\
                ]\
            }\
        },\
        {\
            "type": "reasoning",\
            "summary": [\
                {\
                    "type": "summary_text",\
                    "text": "搜索结果显示阿里云官网URL..."\
                }\
            ]\
        },\
        {\
            "type": "web_extractor_call",\
            "status": "completed",\
            "goal": "提取阿里云官网首页的关键信息",\
            "output": "通义大模型、完整产品体系、AI解决方案...",\
            "urls": [\
                "https://cn.aliyun.com/"\
            ]\
        },\
        {\
            "type": "message",\
            "role": "assistant",\
            "status": "completed",\
            "content": [\
                {\
                    "type": "output_text",\
                    "text": "阿里云官网关键信息：通义大模型，云计算服务..."\
                }\
            ]\
        }\
    ],
    "usage": {
        "input_tokens": 40836,
        "output_tokens": 2106,
        "total_tokens": 42942,
        "output_tokens_details": {
            "reasoning_tokens": 677
        },
        "x_tools": {
            "web_extractor": {
                "count": 1
            },
            "web_search": {
                "count": 1
            }
        }
    }
}
```

## 从 Chat Completions 迁移到 Responses API

如果您当前使用的是 OpenAI Chat Completions API，可以通过以下步骤迁移到 Responses API。Responses API 提供了更简洁的接口和更强大的功能，同时保持了与 Chat Completions 的兼容性。

### **1\. 更新端点地址和 base\_url**

需要同时更新两处：

- **端点路径**：从 `/v1/chat/completions` 更新为 `/v1/responses`

- **base\_url**：

  - **华北2（北京）**：从 `https://dashscope.aliyuncs.com/compatible-mode/v1`更新为 `https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1`

  - **新加坡**：从 `https://dashscope-intl.aliyuncs.com/compatible-mode/v1`更新为 `https://dashscope-intl.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1`

Python

Node.js

curl

```python
# Chat Completions API
completion = client.chat.completions.create(
    model="qwen3.5-plus",
    messages=[\
        {"role": "system", "content": "你是一个有帮助的助手。"},\
        {"role": "user", "content": "你好！"}\
    ]
)
print(completion.choices[0].message.content)

# Responses API - 可以使用相同的消息格式
response = client.responses.create(
    model="qwen3.5-plus",
    input=[\
        {"role": "system", "content": "你是一个有帮助的助手。"},\
        {"role": "user", "content": "你好！"}\
    ]
)
print(response.output_text)

# Responses API - 或使用更简洁的格式
response = client.responses.create(
    model="qwen3.5-plus",
    input="你好！"
)
print(response.output_text)
```

```nodejs
// Chat Completions API
const completion = await client.chat.completions.create({
    model: "qwen3.5-plus",
    messages: [\
        { role: "system", content: "你是一个有帮助的助手。" },\
        { role: "user", content: "你好！" }\
    ]
});
console.log(completion.choices[0].message.content);

// Responses API - 可以使用相同的消息格式
const response = await client.responses.create({
    model: "qwen3.5-plus",
    input: [\
        { role: "system", content: "你是一个有帮助的助手。" },\
        { role: "user", content: "你好！" }\
    ]
});
console.log(response.output_text);

// Responses API - 或使用更简洁的格式
const response2 = await client.responses.create({
    model: "qwen3.5-plus",
    input: "你好！"
});
console.log(response2.output_text);
```

```curl
# Chat Completions API
curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "messages": [\
        {"role": "system", "content": "你是一个有帮助的助手。"},\
        {"role": "user", "content": "你好！"}\
    ]
}'

# Responses API - 使用更简洁的格式
curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen3.5-plus",
    "input": "你好！"
}'
```

### **2\. 更新响应处理**

Responses API 的响应结构有所不同。使用 `output_text` 快捷方法获取文本输出，或通过 `output` 数组访问详细信息。

**响应对比**

|     |     |
| --- | --- |
| ```json<br># Chat Completions 响应<br>{<br>  "id": "chatcmpl-416b0ea5-e362-9fec-97c5-0a60b5d7xxx",<br>  "choices": [<br>    {<br>      "finish_reason": "stop",<br>      "index": 0,<br>      "logprobs": null,<br>      "message": {<br>        "content": "你好！很高兴见到你～ 有什么我可以帮你的吗？",<br>        "refusal": null,<br>        "role": "assistant",<br>        "function_call": null,<br>        "tool_calls": null<br>      }<br>    }<br>  ],<br>  "created": 1769416269,<br>  "model": "qwen3.5-plus",<br>  "object": "chat.completion",<br>  "service_tier": null,<br>  "system_fingerprint": null,<br>  "usage": {<br>    "completion_tokens": 14,<br>    "prompt_tokens": 22,<br>    "total_tokens": 36,<br>    "prompt_tokens_details": {<br>      "cached_tokens": 0<br>    }<br>  }<br>}<br>``` | ```json<br># Responses API 响应<br>{<br>  "id": "d69c735d-0f5e-4b6c-9c2a-8cab5eb14xxx",<br>  "created_at": 1769416269.0,<br>  "model": "qwen3.5-plus",<br>  "object": "response",<br>  "status": "completed",<br>  "output": [<br>    {<br>      "id": "msg_3426d3e5-8da7-4dd8-a6a5-7c2cd866xxx",<br>      "type": "message",<br>      "role": "assistant",<br>      "status": "completed",<br>      "content": [<br>        {<br>          "type": "output_text",<br>          "text": "你好！今天是2026年1月26日，星期一。有什么我可以帮你的吗？",<br>          "annotations": []<br>        }<br>      ]<br>    }<br>  ],<br>  "usage": {<br>    "input_tokens": 34,<br>    "output_tokens": 25,<br>    "total_tokens": 59,<br>    "input_tokens_details": {<br>      "cached_tokens": 0<br>    },<br>    "output_tokens_details": {<br>      "reasoning_tokens": 0<br>    }<br>  }<br>}<br>``` |

### **3\. 简化多轮对话管理**

在 Chat Completions 中需要手动管理消息历史数组，而 Responses API 提供了 `previous_response_id` 参数自动关联上下文，当前响应`id`有效期为7天。

Python

Node.js

|     |     |
| --- | --- |
| ```python<br># Chat Completions - 需要手动管理消息历史<br>messages = [<br>    {"role": "system", "content": "你是一个有帮助的助手。"},<br>    {"role": "user", "content": "法国的首都是哪里？"}<br>]<br>res1 = client.chat.completions.create(<br>    model="qwen3.5-plus",<br>    messages=messages<br>)<br># 手动添加响应到历史<br>messages.append(res1.choices[0].message)<br>messages.append({"role": "user", "content": "它的人口是多少？"})<br>res2 = client.chat.completions.create(<br>    model="qwen3.5-plus",<br>    messages=messages<br>)<br>``` | ```python<br># Responses API - 使用 previous_response_id 自动关联<br>res1 = client.responses.create(<br>    model="qwen3.5-plus",<br>    input="法国的首都是哪里？"<br>)<br># 只需传递上一轮的 ID<br>res2 = client.responses.create(<br>    model="qwen3.5-plus",<br>    input="它的人口是多少？",<br>    previous_response_id=res1.id<br>)<br>``` |

|     |     |
| --- | --- |
| ```nodejs<br>// Chat Completions - 需要手动管理消息历史<br>let messages = [<br>    { role: "system", content: "你是一个有帮助的助手。" },<br>    { role: "user", content: "法国的首都是哪里？" }<br>];<br>const res1 = await client.chat.completions.create({<br>    model: "qwen3.5-plus",<br>    messages<br>});<br>// 手动添加响应到历史<br>messages = messages.concat([res1.choices[0].message]);<br>messages.push({ role: "user", content: "它的人口是多少？" });<br>const res2 = await client.chat.completions.create({<br>    model: "qwen3.5-plus",<br>    messages<br>});<br>``` | ```nodejs<br>// Responses API - 使用 previous_response_id 自动关联<br>const res1 = await client.responses.create({<br>    model: "qwen3.5-plus",<br>    input: "法国的首都是哪里？"<br>});<br>// 只需传递上一轮的 ID<br>const res2 = await client.responses.create({<br>    model: "qwen3.5-plus",<br>    input: "它的人口是多少？",<br>    previous_response_id: res1.id<br>});<br>``` |

### **4\. 使用内置工具**

Responses API 内置了多种工具，无需自行实现。只需在 `tools` 参数中指定即可，当前代码解释器与网页抓取工具限时免费，详情请参见 [工具调用](https://help.aliyun.com/zh/model-studio/tool-calls/ "")。

Python

Node.js

curl

|     |     |
| --- | --- |
| ```python<br># Chat Completions - 需要自己实现工具函数<br>def web_search(query):<br>    # 需要自己实现网络搜索逻辑<br>    import requests<br>    r = requests.get(f"https://api.example.com/search?q={query}")<br>    return r.json().get("results", [])<br>completion = client.chat.completions.create(<br>    model="qwen3.5-plus",<br>    messages=[{"role": "user", "content": "法国现任总统是谁？"}],<br>    functions=[{<br>        "name": "web_search",<br>        "description": "搜索网络信息",<br>        "parameters": {<br>            "type": "object",<br>            "properties": {"query": {"type": "string"}},<br>            "required": ["query"]<br>        }<br>    }]<br>)<br>``` | ```python<br># Responses API - 直接使用内置工具<br>response = client.responses.create(<br>    model="qwen3.5-plus",<br>    input="法国现任总统是谁？",<br>    tools=[{"type": "web_search"}]  # 直接启用网络搜索<br>)<br>print(response.output_text)<br>``` |

|     |     |
| --- | --- |
| ```nodejs<br>// Chat Completions - 需要自己实现工具函数<br>async function web_search(query) {<br>    const fetch = (await import('node-fetch')).default;<br>    const res = await fetch(`https://api.example.com/search?q=${query}`);<br>    const data = await res.json();<br>    return data.results;<br>}<br>const completion = await client.chat.completions.create({<br>    model: "qwen3.5-plus",<br>    messages: [{ role: "user", content: "法国现任总统是谁？" }],<br>    functions: [{<br>        name: "web_search",<br>        description: "搜索网络信息",<br>        parameters: {<br>            type: "object",<br>            properties: { query: { type: "string" } },<br>            required: ["query"]<br>        }<br>    }]<br>});<br>``` | ```nodejs<br>// Responses API - 直接使用内置工具<br>const response = await client.responses.create({<br>    model: "qwen3.5-plus",<br>    input: "法国现任总统是谁？",<br>    tools: [{ type: "web_search" }]  // 直接启用网络搜索<br>});<br>console.log(response.output_text);<br>``` |

|     |     |
| --- | --- |
| ```curl<br># Chat Completions - 需要自己实现工具<br># 这里展示调用外部搜索 API 的示例<br>curl https://api.example.com/search \<br>  -G \<br>  --data-urlencode "q=法国现任总统" \<br>  --data-urlencode "key=$SEARCH_API_KEY"<br>``` | ```curl<br># Responses API - 直接使用内置工具<br>curl -X POST https://dashscope.aliyuncs.com/api/v2/apps/protocols/compatible-mode/v1/responses \<br>-H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>-H "Content-Type: application/json" \<br>-d '{<br>    "model": "qwen3.5-plus",<br>    "input": "法国现任总统是谁？",<br>    "tools": [{"type": "web_search"}]<br>}'<br>``` |

## 常见问题

**Q：如何传递多轮对话的上下文？**

A：在发起新一轮对话请求时，请将上一轮模型响应成功返回的`id`作为 `previous_response_id` 参数传入。

## 相关文档

- [OpenAI Responses](https://help.aliyun.com/zh/model-studio/qwen-api-via-openai-responses "")

- [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")

- [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")