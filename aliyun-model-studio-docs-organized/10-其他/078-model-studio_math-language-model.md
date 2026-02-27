### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[文本生成](https://help.aliyun.com/zh/model-studio/core-concepts/)[专项模型](https://help.aliyun.com/zh/model-studio/specialized-models/)数学能力（Qwen-Math）

# 数学能力（Qwen-Math）

更新时间：2026-01-21 07:45:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：深入研究（Qwen-Deep-Research）](https://help.aliyun.com/zh/model-studio/qwen-deep-research)[下一篇：对话分析（Tongyi-Xiaomi-Analysis）](https://help.aliyun.com/zh/model-studio/dialogue-analysis)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型与价格

快速开始

使用建议

常见问题

阿里云百炼提供的 Qwen-Math 系列模型具备强大的数学推理和计算能力，模型提供详细的解题步骤，便于理解和验证。

**说明**

- 推荐使用 **最新的** [Qwen3](https://help.aliyun.com/zh/model-studio/models#2c9c4628c9yyd "") 通用模型替代 Qwen-Math 模型，后者仍基于 Qwen2.5 模型。

- 本文档仅适用于“中国内地（北京）”地域，需使用“中国内地（北京）”地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)。


## 模型与价格

**商业版**

| **模型名称** | **输入价格** | **输出价格** | **上下文长度** | **最大输入** | **最大输出** | **免费额度**<br>[（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| --- | --- | --- | --- | --- | --- | --- |
| **（每百万Token）** | **（Token数）** |
| --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **输入价格** | **输出价格** | **上下文长度** | **最大输入** | **最大输出** | **免费额度**<br>[（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| **（每百万Token）** | **（Token数）** |
| **qwen-math-plus** | 4元 | 12元 | 4,096 | 3,072 | 3,072 | 各100万Token<br>有效期：百炼开通后90天内 |
| **qwen-math-turbo** | 2元 | 6元 |

> `qwen-math-xxx` 与快照版本的以上参数完全相同。（如 `qwen-math-xxx-latest` 和 `qwen-math-xxx-YYYY-MM-DD`）

> 模型能力：`qwen-math-xxx`=`qwen-math-xxx-latest`=`qwen-math-xxx-2024-09-19`

> **各模型的免费额度均不共用。**

**开源版**

| **模型名称** | **输入价格** | **输出价格** | **上下文长度** | **最大输入** | **最大输出** | **免费额度**<br>[（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| --- | --- | --- | --- | --- | --- | --- |
| **（每百万Token）** | **（Token数）** |
| --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **输入价格** | **输出价格** | **上下文长度** | **最大输入** | **最大输出** | **免费额度**<br>[（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| **（每百万Token）** | **（Token数）** |
| qwen2.5-math-72b-instruct | 4元 | 12元 | 4,096 | 3,072 | 3,072 | 各100万Token<br>有效期：百炼开通后90天内 |
| qwen2.5-math-7b-instruct | 1元 | 2元 |
| qwen2.5-math-1.5b-instruct | 限时免费 | 限时免费 |

关于模型的限流条件，请参见 [限流](https://help.aliyun.com/zh/model-studio/rate-limit "")。

## **快速开始**

您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。如果通过OpenAI SDK或DashScope SDK进行调用，还需要 [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

OpenAI兼容

DashScope

Python

curl

```python
from openai import OpenAI
import os

client = OpenAI(
    api_key=os.getenv("DASHSCOPE_API_KEY"), # 请勿在代码中硬编码凭证，应始终使用环境变量或密钥管理服务
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)
completion = client.chat.completions.create(
    model="qwen-math-plus",
    messages=[{'role': 'user', 'content': 'Derive a universal solution for the quadratic equation $ Ax^2+Bx+C=0 $'}])
print(completion.choices[0].message.content)
```

```shell
curl --location "https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions" \
--header "Authorization: Bearer $DASHSCOPE_API_KEY" \
--header "Content-Type: application/json" \
--data '{
    "model": "qwen-math-plus",
    "messages": [\
        {\
            "role": "user",\
            "content": "Derive a universal solution for the quadratic equation $ Ax^2+Bx+C=0 $"\
        }\
    ]
}'
```

Python

Java

curl

```python
from http import HTTPStatus
import dashscope

def call_with_messages():
    messages = [\
        {'role': 'user', 'content': 'Derive a universal solution for the quadratic equation $ Ax^2+Bx+C=0 $'}]
    response = dashscope.Generation.call(
        model='qwen-math-plus',
        messages=messages,
        # 设置result_format为message格式
        result_format='message',
    )
    if response.status_code == HTTPStatus.OK:
        print(response)
    else:
        print('Request id: %s, Status code: %s, error code: %s, error message: %s' % (
            response.request_id, response.status_code,
            response.code, response.message
        ))

if __name__ == '__main__':
    call_with_messages()

```

```java
import java.util.Arrays;
import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.common.Message;
import com.alibaba.dashscope.common.Role;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;

public class Main {
    public static void callWithMessage()
            throws NoApiKeyException, ApiException, InputRequiredException {
        Generation gen = new Generation();
        Message userMsg = Message.builder().role(Role.USER.getValue()).content("Derive a universal solution for the quadratic equation $ Ax^2+Bx+C=0 $").build();
        GenerationParam param =GenerationParam.builder()
                .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                .model("qwen-math-plus")
                .messages(Arrays.asList(userMsg))
                .resultFormat(GenerationParam.ResultFormat.MESSAGE)
                .build();
        GenerationResult result = gen.call(param);
        System.out.println(result);
    }

    public static void main(String[] args){
        try {
            callWithMessage();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

```curl
curl --location "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
--header "Authorization: Bearer $DASHSCOPE_API_KEY" \
--header "Content-Type: application/json" \
--data '{
    "model": "qwen-math-plus",
    "input":{
        "messages":[\
            {\
                "role": "user",\
                "content": "Derive a universal solution for the quadratic equation $ Ax^2+Bx+C=0 $"\
            }\
        ]
    },
    "parameters": {
        "result_format": "message"
    }
}'
```

> 也可以前往[百炼控制台](https://bailian.console.aliyun.com/tab=model#/efm/model_experience_center/text?currentTab=textChat&modelId=qwen-math-plus)体验模型。

## 使用建议

1. **使用英文\+ LaTeX：** Qwen-Math 模型专精于英文数学问题，输入时建议使用 LaTeX 表示数学符号或公式。

2. **规范内容输出：** [前缀续写模式（Partial Mode）](https://help.aliyun.com/zh/model-studio/partial-mode "") 可提供精确控制能力，确保模型输出的内容紧密衔接提供的前缀，提升生成结果的准确性与可控性。

3. 模型默认设置`temperature=0`，无须调节。

4. **便捷提取结果：** Qwen-Math 模型默认将把最终结果输出在`\boxed{}`区块中。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7746368571/p1006794.png)


## 常见问题

|     |
| --- |
| **如何利用通义千问数学模型解答图片中的数学问题？** |
| 通义千问数学模型暂不支持图片识别功能。<br>- 如果图片中是简单的数学问题，可以使用 [通义千问VL](https://help.aliyun.com/zh/model-studio/vision "")、 [QVQ](https://help.aliyun.com/zh/model-studio/visual-reasoning "") 模型进行解答。<br>  <br>- 如果图片中包含复杂的数学问题，可以先使用 [通义千问VL](https://help.aliyun.com/zh/model-studio/vision "")、 [QVQ](https://help.aliyun.com/zh/model-studio/visual-reasoning "") 模型提取图片中的文字，再使用通义千问数学模型解答问题。<br>  <br>关于通义千问数学模型的输入与输出参数，请参考 [通义千问 API 参考](https://help.aliyun.com/zh/model-studio/qwen-api-reference/ "")。 |
| **在哪里可以查到错误码的详细信息？** |
| 如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。 |