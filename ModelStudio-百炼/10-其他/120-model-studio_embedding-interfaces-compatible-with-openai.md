### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[工具包/框架](https://help.aliyun.com/zh/model-studio/toolkits-and-frameworks/)OpenAI兼容-Embedding

# OpenAI Embedding接口兼容

更新时间：2025-12-12 04:23:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenAI兼容-Batch Chat](https://help.aliyun.com/zh/model-studio/openai-compatible-batch-chat)[下一篇：Anthropic API兼容](https://help.aliyun.com/zh/model-studio/anthropic-api-messages)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

支持的模型

模型调用

调用示例

异常响应示例

API参考

错误码

阿里云百炼的Embedding模型兼容OpenAI接口规范。将原有 OpenAI 应用迁移至阿里云百炼只需调整三个参数：

- base\_url：替换为`https://dashscope.aliyuncs.com/compatible-mode/v1`

- api\_key：替换为 [阿里云百炼 API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")

- model：替换为以下模型列表中的模型名称


## **支持的模型**

| **模型名称** | **向量维度** | **最大行数** | **单行最大** [Token](https://help.aliyun.com/zh/model-studio/billing-for-model-studio#f300d75bd5rb2 "") **数** | **单价（每千输入Token）** | **支持语种** | **免费额度** [（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **向量维度** | **最大行数** | **单行最大** [Token](https://help.aliyun.com/zh/model-studio/billing-for-model-studio#f300d75bd5rb2 "") **数** | **单价（每千输入Token）** | **支持语种** | **免费额度** [（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| text-embedding-v4<br>> 属于 [Qwen3-Embedding](https://qwenlm.github.io/zh/blog/qwen3-embedding/) 系列 | 2,048、1,536、1,024（默认）、768、512、256、128、64 | 10 | 8,192 | 0.0005元<br>[Batch调用](https://help.aliyun.com/zh/model-studio/batch-interfaces-compatible-with-openai/ "")：0.00025元 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语、日语、韩语、德语、俄罗斯语等100+主流语种及多种编程语言 | 各100万Token<br>有效期：百炼开通后90天内 |
| text-embedding-v3 | 1,024（默认）、768、512、256、128或64 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语、日语、韩语、德语、俄罗斯语等50+主流语种 |
| text-embedding-v2 | 1,536 | 25 | 2,048 | 0.0007元<br>[Batch调用](https://help.aliyun.com/zh/model-studio/batch-interfaces-compatible-with-openai/ "")：0.00035元 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语、日语、韩语、德语、俄罗斯语 | 各50万Token<br>有效期：百炼开通后90天内 |
| text-embedding-v1 | 中文、英语、西班牙语、法语、葡萄牙语、印尼语 |

## 模型调用

### **调用示例**

本章节提供Python（OpenAI SDK）和cURL（HTTP接口）的字符串输入调用示例，更多编程语言或输入方式示例请参考： [文本与多模态向量化](https://help.aliyun.com/zh/model-studio/embedding#793f71eacdohs "")。

使用OpenAI SDK调用

使用HTTP接口调用

使用OpenAI SDK调用服务，您还需安装 [OpenAI SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.getenv("DASHSCOPE_API_KEY"),  # 如果您没有配置环境变量，请在此处用您的API Key进行替换
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1"  # 百炼服务的base_url
)

completion = client.embeddings.create(
    model="text-embedding-v4",
    input='衣服的质量杠杠的，很漂亮，不枉我等了这么久啊，喜欢，以后还来这里买',
    dimensions=1024, # 指定向量维度（仅 text-embedding-v3及 text-embedding-v4支持该参数）
    encoding_format="float"
)

print(completion.model_dump_json())
```

### **提交接口调用**

```http
POST https://dashscope.aliyuncs.com/compatible-mode/v1/embeddings
```

### **命令行调用**

```curl
curl --location 'https://dashscope.aliyuncs.com/compatible-mode/v1/embeddings' \
--header "Authorization: Bearer $DASHSCOPE_API_KEY" \
--header 'Content-Type: application/json' \
--data '{
    "model": "text-embedding-v4",
    "input": "衣服的质量杠杠的，很漂亮，不枉我等了这么久啊，喜欢，以后还来这里买",
    "encoding_format": "float"
}'
```

运行代码可以获得以下结果：

**运行结果**

```json
{
  "data": [\
    {\
      "embedding": [\
        0.0023064255,\
        -0.009327292,\
        ....\
        -0.0028842222\
      ],\
      "index": 0,\
      "object": "embedding"\
    }\
  ],
  "model":"text-embedding-v4",
  "object":"list",
  "usage":{"prompt_tokens":23,"total_tokens":23},
  "id":"f62c2ae7-0906-9758-ab34-47c5764f07e2"
}
```

### **异常响应示例**

在访问请求出错的情况下，输出的结果中会通过`code`和`message`指明出错原因。

```json
{
    "error": {
        "message": "Incorrect API key provided. ",
        "type": "invalid_request_error",
        "param": null,
        "code": "invalid_api_key"
    }
}
```

## API参考

[通用文本向量接口API详情](https://help.aliyun.com/zh/model-studio/text-embedding-synchronous-api "")

## 错误码

如果模型调用失败并返回报错信息，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。