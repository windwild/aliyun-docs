### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 快速开始

# 快速开始

更新时间：2025-01-23 22:57:43

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速开始

前提条件

示例代码

了解更多

本文主要介绍如何使用API调用阿里云百炼的流程编排应用，也就是从应用中心中创建的流程编排应用。

## **快速开始**

### **前提条件**

- 已开通百炼服务： [产品开通](https://help.aliyun.com/zh/model-studio/activate-alibaba-cloud-model-studio "")。


- 已创建API-KEY: [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

- 已安装最新版SDK： [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

- 已创建RAG检索增强应用： [0代码构建私有知识问答应用](https://help.aliyun.com/zh/model-studio/build-knowledge-base-qa-assistant-without-coding/ "")，并参考 [流程编排（旧）](https://help.aliyun.com/zh/model-studio/manage-processes-old/ "") 配置流程编排应用。


### **示例代码**

以下示例展示了调用流程编排应用来调用自定义插件进行实时天气查询问答。

**说明**

需要使用您的API-KEY替换示例中的YOUR\_API\_KEY，并将APP-ID替换示例中的YOUR\_APP\_ID，代码才能正常运行。

python sdk version: dashscope>=1.10.0

java sdk version: >=2.5.0

设置API-KEY

```shell
export DASHSCOPE_API_KEY=YOUR_API_KEY
```

#### **流程编排应用示例**

Python

Java

Python

```python
from http import HTTPStatus
from dashscope import Application

def flow_call():
    response = Application.call(app_id='YOUR_APP_ID',
                                prompt='杭州的天气怎么样',
                                )

    if response.status_code != HTTPStatus.OK:
        print('request_id=%s, code=%s, message=%s\n' % (response.request_id, response.status_code, response.message))
    else:
        print('request_id=%s\n output=%s\n usage=%s\n' % (response.request_id, response.output, response.usage))

if __name__ == '__main__':
    flow_call()
```

Java

```java
import com.alibaba.dashscope.app.*;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.InputRequiredException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import java.util.List;

public class Main{
    public static void flowCall()
            throws ApiException, NoApiKeyException, InputRequiredException {
        ApplicationParam param = ApplicationParam.builder()
                .appId("YOUR_APP_ID")
                .prompt("杭州的天气怎么样")
                .build();

        Application application = new Application();
        ApplicationResult result = application.call(param);

        System.out.printf("requestId: %s, text: %s, finishReason: %s\n",
                result.getRequestId(), result.getOutput().getText(), result.getOutput().getFinishReason());
    }

    public static void main(String[] args) {
        try {
            flowCall();
        } catch (ApiException | NoApiKeyException | InputRequiredException e) {
            System.out.printf("Exception: %s", e.getMessage());
        }
        System.exit(0);
    }
}
```

#### 流程编排应用 **示例结果**

```json
request_id=0656f381-561f-9c9c-b5f8-549a2e7a18eb
 output={"text": " 杭州的天气为小到中雨，气温在15~27℃之间。", "finish_reason": "stop", "session_id": "3741d1ab9be******720dd172330b", "thoughts": [{"thought": " 首先调用查询天气插件，输入参数为杭州，以获取杭州的天气信息。\n", "action_type": "api", "response": null, "action_name": "查询天气插件", "action": "plg_aa02454d04884113aa0a697d4c4fa813", "action_input_stream": " {\"city\": \"杭州\"}", "action_input": null, "observation": "{\"data\":\"小到中雨，气温15~27℃\",\"errorInfo\":\"\",\"status\":\"success\"}"}, {"thought": " 调用查询天气插件后，根据返回的成功状态和天气数据，直接告知用户杭州的天气情况。\n", "action_type": "response", "response": " 杭州的天气为小到中雨，气温在15~27℃之间。", "action_name": null, "action": null, "action_input_stream": null, "action_input": null, "observation": null}], "doc_references": null}
 usage={"models": [{"model_id": "pre-plugin-888", "input_tokens": 459, "output_tokens": 68}, {"model_id": "pre-plugin-888", "input_tokens": 583, "output_tokens": 51}]}
```

## 了解更多

有关流程编排应用API的详细调用文档可前往 [API详情](https://help.aliyun.com/zh/model-studio/process-orchestration-api "") 页面进行了解。