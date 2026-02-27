### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 快速开始

# 快速开始

更新时间：2026-02-11 02:10:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

MiniMax

快速开始

前提条件

示例代码

了解更多

本文向您介绍快速开始MiniMax大语言模型调用的方法。

## MiniMax

**说明**

支持的领域 / 任务：复杂语言理解、深度推理、文本生成

MiniMax-abab6.5系列模型是MiniMax推出的万亿参数大语言模型，可以很好地满足复杂生产力以及多语言人设对话场景需求，最大支持245k上下文窗口，在知识、推理、数学、编程、指令遵循等各项测试中接近行业最领先的大模型水平。

## **快速开始**

### **前提条件**

- 您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。如果通过SDK调用，还需要 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

- 您需要登录阿里云百炼控制台界面，在 [**模型广场**](https://bailian.console.aliyun.com/#/model-market) 找到您需要申请的MiniMax大语言模型，单击 **立即申请**，等待申请完成即可进行调用。


### **示例代码**

以下示例展示了调用API对一个用户指令进行响应的代码。

Python

Java

Python

```python
# coding=utf-8
import os
import dashscope

messages = [{'role': 'system', 'content': 'You are a helpful assistant.'},\
            {'role': 'user', 'content': '你是谁'}]
response = dashscope.Generation.call(
    # 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    model='abab6.5s-chat',  # 此处以abab6.5s-chat为例，可按需更换模型名称。模型列表：https://help.aliyun.com/zh/model-studio/getting-started/models
    messages=messages,
)
print(response)
```

Java

```java
import java.util.Arrays;
import java.lang.System;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;

public class Main {
    public static GenerationResult callWithMessage() throws ApiException, NoApiKeyException, InputRequiredException {
        Generation gen = new Generation();
        Message systemMsg = Message.builder()
                .role(Role.SYSTEM.getValue())
                .content("You are a helpful assistant.")
                .build();
        Message userMsg = Message.builder()
                .role(Role.USER.getValue())
                .content("你是谁？")
                .build();
        GenerationParam param = GenerationParam.builder()
                // 若没有配置环境变量，请用阿里云百炼API Key将下行替换为：.apiKey("sk-xxx")
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                // 此处以abab6.5s-chat为例，可按需更换模型名称。模型列表：https://help.aliyun.com/zh/model-studio/getting-started/models
                .model("abab6.5s-chat")
                .messages(Arrays.asList(systemMsg, userMsg))
                .build();
        return gen.call(param);
    }
    public static void main(String[] args) {
        try {
            GenerationResult result = callWithMessage();
            System.out.println(JsonUtils.toJson(result));
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            // 使用日志框架记录异常信息
            System.err.println("An error occurred while calling the generation service: " + e.getMessage());
        }
        System.exit(0);
    }
}
```

调用成功后，将会返回如下示例结果。

JSON

JSON

```json
{
    "status_code": 200,
    "request_id": "f7c8b6dc-4cfa-9f07-a71b-56159d24c13c",
    "code": "",
    "message": "",
    "output": {
        "text": null,
        "finish_reason": null,
        "choices": [\
            {\
                "finish_reason": "stop",\
                "message": {\
                    "role": "assistant",\
                    "content": "您好！我是一个人工智能助手，专门设计来回答问题、提供信息和帮助解决问题。请随时向我咨询任何问题或请求帮助。",\
                    "name": "MM智能助理",\
                    "audio_content": ""\
                },\
                "index": 0\
            }\
        ]
    },
    "usage": {
        "input_tokens": 35,
        "output_tokens": 30,
        "total_tokens": 65
    }
}
```

## **了解更多**

有关MiniMax大语言模型API的详细调用文档可前往 [MiniMax](https://help.aliyun.com/zh/model-studio/minimax-llm-api "") 页面进行了解。