### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 快速使用

# 快速使用

更新时间：2026-02-11 02:37:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

BiLLa

快速开始

前提条件

示例代码

了解更多

## BiLLa

**说明**

支持的领域 / 任务：aigc

BiLLa模型在大模型服务平台上的模型名称为"billa-7b-sft-v1"。BiLLa 是开源的推理能力增强的中英双语 LLaMA 模型. 模型的主要特点：

- 较大提升 LLaMA 的中文理解能力, 并尽可能减少对原始 LLaMA 英文能力的损伤;

- 训练过程增加较多的任务型数据, 利用 ChatGPT 生成解析, 强化模型理解任务求解逻辑;

- 全量参数更新, 追求更好的生成效果。


当前在大模型服务平台部署服务时使用的ModelScope社区模型id：AI-ModelScope/BiLLa-7B-SFT，模型版本：v1.0.5。

更多信息可以参考ModelScope上 [BiLLa的开源repo](https://www.modelscope.cn/models/AI-ModelScope/BiLLa-7B-SFT/summary)。

## **快速开始**

### **前提条件**

- 已开通服务并获得API-KEY： [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

- 已安装最新版SDK： [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


### **示例代码**

以下示例展示了调用BiLLa API对一个用户指令进行响应的代码。

**说明**

需要使用您的API-KEY替换示例中的 _your-dashscope-api-key_，代码才能正常运行。

#### 设置API-KEY

```python
export DASHSCOPE_API_KEY=YOUR_DASHSCOPE_API_KEY
```

Python

Java

Python

```python
# For prerequisites running the following sample, visit https://help.aliyun.com/document_detail/611472.html

import dashscope
from http import HTTPStatus

response = dashscope.Generation.call(
    model='billa-7b-sft-v1',
    prompt='翻译成英文：春天来了，花朵都开了。'
)
# The response status_code is HTTPStatus.OK indicate success,
# otherwise indicate request is failed, you can get error code
# and message from code and message.
if response.status_code == HTTPStatus.OK:
    print(response.output)  # The output text
else:
    print(response.code)  # The error code.
    print(response.message)  # The error message.
```

Java

```java
// Copyright (c) Alibaba, Inc. and its affiliates.

import com.alibaba.dashscope.aigc.generation.Generation;
import com.alibaba.dashscope.aigc.generation.GenerationParam;
import com.alibaba.dashscope.aigc.generation.GenerationResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.JsonUtils;

public class Main {
  public static void usage()
      throws NoApiKeyException, ApiException, InputRequiredException {
    Generation gen = new Generation();
    String prompt = "翻译成英文：春天来了，花朵都开了。";
    GenerationParam param = GenerationParam
        .builder()
        .model("billa-7b-sft-v1")
        .prompt(prompt)
        .build();
    GenerationResult result = gen.call(param);
    System.out.println(JsonUtils.toJson(result));
  }

  public static void main(String[] args) {
    try {
      usage();
    } catch (ApiException | NoApiKeyException | InputRequiredException e) {
      System.out.println(e.getMessage());
    }
    System.exit(0);
  }
}
```

调用成功后，将会返回如下示例结果。

JSON

JSON

```json
{"text": "Translation into English: Spring has come, and the flowers have all bloomed."}
```

## **了解更多**

有关BiLLa模型API的详细调用文档可前往 [BiLLa](https://help.aliyun.com/zh/model-studio/videos/billa-api "") 页面进行了解。