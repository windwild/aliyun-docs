### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[模型部署](https://help.aliyun.com/zh/model-studio/model-deployment-1/)模型部署简介

# 模型部署简介

更新时间：2026-02-24 20:47:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：视频生成模型调优](https://help.aliyun.com/zh/model-studio/wan-video-generation-finetune-guide)[下一篇：模型导入](https://help.aliyun.com/zh/model-studio/model-import)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费方式

计费详情

部署方法

部署配置

部署后调用

部署服务扩缩容

部署服务下线

常见问题

可以上传和部署自己的模型吗？

部署时提示权限不足怎么办？

该如何切换到其他的计费方式？

无论是平台的预置模型还是您 [调优](https://help.aliyun.com/zh/model-studio/model-training-overview "") 后的模型，您可通过部署获得独立的、资源专享的推理服务，以满足您对高并发、低延迟等不同性能的业务需求。

**重要**

本文档仅适用于“中国内地（北京）”地域。

## 计费方式

> 部署前可以在[模型部署控制台（北京）](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/model_deploy/create)查看不同模型的预估每小时费用。

**说明**

计费方式在服务创建后无法更改。如需切换，必须下线已经部署的模型后再重新部署。

|  | **预置吞吐**<br>**（** **高吞吐；高性能）** | **模型单元**<br>**（自定义性能指标；资源隔离）** | **Token 用量**<br>**（** [**调优**](https://help.aliyun.com/zh/model-studio/model-training-overview "") **后按量计费/效果验证）** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
|  | **预置吞吐**<br>**（** **高吞吐；高性能）** | **模型单元**<br>**（自定义性能指标；资源隔离）** | **Token 用量**<br>**（** [**调优**](https://help.aliyun.com/zh/model-studio/model-training-overview "") **后按量计费/效果验证）** |
| **计费图示** | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6346770771/p1052924.png) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6346770771/p1052921.png) | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6346770771/p1052922.png) |
| **支持模型** | 部分预置模型 | 部分预置模型与所有调优后模型 | 部分经过 LoRA 调优后的模型 |
| **使用场景** | 1. 银行App的智能客服（流量稳定，需保障并发体验）。<br>   <br>2. 社交平台的实时内容审核（需稳定处理可预估的流水线任务）。<br>   <br>3. 公有云翻译API（为标准套餐用户提供基线服务保障）。 | 1. 电商专属微调大模型（部署私有模型，大促时手动扩容）。<br>   <br>2. 医药公司的分子筛选模型（需独占资源跑长时任务）。<br>   <br>3. 自动驾驶仿真（需要进行长时间持续计算）。 | 1. 调优后模型效果验证 |
| **计费方式** | 按使用时长和预置吞吐<br>随用随付、包天 | 按使用时长和模型单元数量<br>随用随付、包月 | 按模型 Token 使用量<br>随用随付 |
| **扩缩容方式** | 自助增减吞吐量 | 自助增减模型单元数量 | 在控制台提交申请，等待人工审核。 |
|  |
| **优势** | 1. 为 **高负载生产环境** 提供稳定的吞吐容量、更低延迟和更强的资源确定性。<br>   <br>2. 支持设置自动续费。 | 1. 延迟/吞吐等 **性能指标可自定义**。<br>   <br>2. 支持设置自动续费。 | 1. **不使用不计费**。 |
| **产品约束** | 1. 预付费按天计费。无法提前退费<br>   <br>2. 如果单位时间内使用超出购买的吞吐量，将自动切换成百炼提供的 [模型调用](https://help.aliyun.com/zh/model-studio/model-pricing "") 服务。 | 1. 预付费购买后，若在首月内提前退订，日单价将按 **1.2** 倍计费 | 1. 只支持部分高效微调（LoRA）后的模型。<br>   <br>2. 一个月内不使用将自动释放。 |

如需查看单次调用的 Token 使用量及调用次数历史统计，请前往：[模型监控（北京）](https://bailian.console.aliyun.com/?tab=model#/model-telemetry)。

## **计费详情**

按使用时长计费（预置吞吐）

按使用时长计费（模型单元）

按模型 Token 使用量

图片、视频生成模型（预置）-按实例时长计费

`费用 = 使用时长 × (输入 TPM 单价 × 输入 TPM + 输出 TPM 单价 × 输出 TPM)`

- 预付费订单支付后实时生效，有效期 N 天至第 N 天 23:59 结束。若在 22:00 后下单，到期日将自动顺延1天。

- 预付费订单到期后，将延后2小时停止服务，停止后资源保留14小时后释放。

- 预付费订单无法提前终止服务。

- 后付费时，如果账户欠费，部署的资源将保留并继续计费 24 小时，之后自动释放资源。


当模型输入超过最长输入 Token 或 超出购买的 TPM 量，相关调用将 **自动** 切换为按量付费的模型调用，推理性能可能下降， [限流](https://help.aliyun.com/zh/model-studio/rate-limit "") 占用业务空间的公共流量， [费用](https://help.aliyun.com/zh/model-studio/model-pricing "") 按模型调用（按量付费）标准计收。

- 此时，调用 API 返回 Header 将包含：`x-dashscope-ptu-overflow:true`。

- TPM 统计请前往：[模型监控（北京）](https://bailian.console.aliyun.com/?tab=model#/model-telemetry)。


|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **模型类型** | **最长上下文**<br>**（输入 Token + 输出 Token）** | **最长输入 Token** | **后付费-按小时** | **预付费-按天** |
| **输入（Per 10k TPM）** | **输出（Per 1k TPM）** | **输入（Per 10k TPM）** | **输出（Per 1k TPM）** |
| 千问3-max-2025-09-23 | Instruct | 128,000 | 128,000 | ¥7.68 | ¥3.08 | ¥92.16 | ¥36.96 |
| 千问-plus-2025-12-01 | Instruct | ¥1.92 | ¥0.48 | ¥23.04 | ¥5.76 |
| Thinking | ¥1.92 | ¥23.04 |
| 千问-flash-2025-07-28 | Instruct/Thinking | ¥0.36 | ¥0.36 | ¥4.32 | ¥4.32 |
| 千问3-vl-plus-2025-09-23 | Instruct/Thinking | ¥2.40 | ¥2.40 | ¥28.80 | ¥28.80 |
| DeepSeek-v3.2 | Instruct/Thinking | 64,000 | ¥7.20 | ¥1.08 | ¥86.40 | ¥12.96 |

模型类型：

- Instruct - 模型部署后以 **非思考模式** 进行推理。

- Thinking - 模型部署后以思考模式进行推理。


`费用 = 使用时长（小时）× 模型单元数量 × 模型单元单价`

- 预付费购买的首月，如在首月内提前退订，日单价将按 **1.2** 倍计费


千问

千问VL

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型名称** | **模型类型** | **支持限流** | **模型单元规格** | **最长上下文** | **后付费-按小时**<br>（不满 1 分钟按 1 分钟计费） | **预付费-按天**<br>（不满 1 天按 1 天计费） |
| 千问3-14B | Instruct/Thinking | 不支持 | I 型模型单元（MU1） | 固定为： `131,072`<br>详情请参考： [qwen-3](https://help.aliyun.com/zh/model-studio/models#2c9c4628c9yyd "") | ¥96/小时 | ¥46,000/月 |
| 千问3-8B | Instruct/Thinking | 不支持 |
| 千问2.5-开源版-14B | Instruct | 不支持 | 固定为： `131,072`<br>详情请参考： [qwen-2.5](https://help.aliyun.com/zh/model-studio/models#15f2bdc5dd3zd "") |
| 千问2.5-开源版-7B | Instruct | 不支持 |
| 千问2-开源版-7B | Instruct | 不支持 | 固定为： `131,072` |
| 千问-Turbo-0624（2024） | Instruct | 不支持 | 固定为： `8,000` |
|  |
| 千问-Plus-2025-12-01 | Instruct/Thinking | 支持 | I 型模型单元（MU1） | 可设置：`1~1,000,000`<br>详情请参考： [qwen-plus](https://help.aliyun.com/zh/model-studio/models#03a05ab98953u "") | ¥192/小时 | ¥92,000/月 |
| 千问-Plus-2025-07-28 | Instruct/Thinking | 支持 |
| 千问-Flash-2025-07-28 | Instruct/Thinking | 支持 | 可设置：`1~1,000,000`<br>详情请参考： [qwen-flash](https://help.aliyun.com/zh/model-studio/models#9b418d9a481yp "") |
| 千问-Plus-0723（2024） | Instruct | 不支持 | 固定为： `32,000` |
| 千问2.5-开源版-72B | Instruct | 不支持 | 固定为： `131,072`<br>详情请参考： [qwen-2.5](https://help.aliyun.com/zh/model-studio/models#15f2bdc5dd3zd "") |
| 千问2.5-开源版-32B | Instruct | 不支持 |
| 千问2-开源版-72B | Instruct | 不支持 | 固定为： `131,072` |
| 千问3-32B | Instruct | 不支持 | 固定为： `131,072`<br>详情请参考： [qwen-3](https://help.aliyun.com/zh/model-studio/models#2c9c4628c9yyd "") |
|  |
| 千问3-Max-2025-09-23 | Instruct | 支持 | II 型 / III 型模型单元<br>（MU2/MU3） | 可设置：`1-262,144`<br>详情请参考： [qwen-max](https://help.aliyun.com/zh/model-studio/models#qwen-max-cn-bj "") | I 型模型单元：¥448/小时<br>III 型模型单元：¥1048/小时 | I 型模型单元：¥216,000/月<br>III 型模型单元：¥504,000/月 |

模型类型：

- Instruct - 模型部署后以 **非思考模式** 进行推理。

- Thinking - 模型部署后以思考模式进行推理。


|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **模型服务** | **模型类型** | **支持限流** | **模型单元规格** | **最长上下文** | **单价**<br>（不满 1 分钟按 1 分钟计费） | **包月单价**<br>（不满 1 天按 1 天计费）<br>（如在首月内提前退订，日单价将按 **1.2** 倍计费） |
| 千问VL-Max-2025-08-13 | Instruct | 支持 | VI 型模型单元（MU6） | 固定为： `131,072` | ¥72/小时 | ¥34,800/月 |
|  |
| 千问VL-Plus | Instruct | 不支持 | I 型模型单元（MU1） | 固定为： `131,072` | ¥40/小时 | ¥20,000/月 |
|  |  |  |  |  |  |  |
| 千问3-VL-8B-Instruct | Instruct | 不支持 | I 型模型单元（MU1） | 固定为： `131,072` | ¥96/小时 | ¥46,000/月 |
| 千问3-VL-8B-Thinking | Thinking | 不支持 |
| 千问3-VL-4B-Instruct | Instruct | 不支持 |
| 千问2.5-VL-7B | Instruct | 不支持 |
|  |  |  |  |  |  |
| 千问VL-Max-0201（2024） | Instruct | 不支持 | 固定为： `8,000` | ¥160/小时 | ¥80,000/月 |
|  |  |  |  |  |  |  |
| 千问3-VL-Flash-2025-10-15 | Instruct/Thinking | 支持 | I 型模型单元（MU1） | 固定为： `262,144` | ¥192/小时 | ¥92,000/月 |
| 千问3-VL-Plus-2025-09-23 | Instruct/Thinking | 不支持 |
| 千问3-VL-235B-A22B-Instruct | Instruct | 不支持 | 固定为： `131,072` |
| 千问3-VL-32B-Instruct | Instruct | 不支持 |
| 千问2.5-VL-32B | Instruct | 不支持 |
| 千问2.5-VL-72B | Instruct | 不支持 |

模型类型：

- Instruct - 模型部署后以 **非思考模式** 进行推理。

- Thinking - 模型部署后以思考模式进行推理。

- Instruct/Thinking - 可在模型部署时 **选择是否开启思考模式**。


`费用 = 模型输入 Token 数 × 模型输入单价 + 模型输出 Token 数 × 模型输出单价（最小计费单位：1 token）`

- 仅当对下列基础模型完成 SFT 高效训练并得到自定义模型后，才支持按模型 Token 使用量计费。


|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **基础模型** | **模型类型** | **最长上下文** | **输入单价** | **输出单价** |
| 千问3-32B | Instruct | 固定为： `131,072`<br>详情请参考： [qwen-3](https://help.aliyun.com/zh/model-studio/models#2c9c4628c9yyd "") | ¥0.002/千Token | 非思考模式：¥0.008/千Token<br>思考模式：¥0.02/千Token |
| 千问3-14B | Instruct | ¥0.001/千Token | 非思考模式：¥0.004/千Token<br>思考模式：¥0.01/千Token |
| 千问3-8B | Instruct | ¥0.0005/千Token | 非思考模式：¥0.002/千Token<br>思考模式：¥0.005/千Token |
| 千问 2.5-72B | Instruct | 固定为： `131,072`<br>详情请参考： [qwen-2.5](https://help.aliyun.com/zh/model-studio/models#15f2bdc5dd3zd "") | ¥0.004/千Token | ¥0.012/千Token |
| 千问 2.5-32B | Instruct | ¥0.002/千Token | ¥0.006/千Token |
| 千问 2.5-14B | Instruct | ¥0.001/千Token | ¥0.003/千Token |
| 千问 2.5-7B | Instruct | ¥0.0005/千Token | ¥0.001/千Token |
| 千问2.5-VL-72B | Instruct | 固定为： `131,072` | ¥0.016/千Token | ¥0.048/千Token |
| 千问2.5-VL-32B | Instruct | ¥0.008/千Token | ¥0.024/千Token |
| 千问2.5-VL-7B | Instruct | ¥0.002/千Token | ¥0.005/千Token |
| 千问 2-开源版-7B | Instruct | 固定为： `131,072` | ¥0.001/千Token | ¥0.002/千Token |

`费用 = 资源占用时长（小时）× 实例数量 × 实例单价（不满 1 小时按 1 小时计费）`

图片生成

视频生成

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型服务** | **模型类型** | **独占实例资源规格** | **后付费单价** | **预付费单价**<br>**（预付费）** |
| 万相-文本生成图像-0521 | 预置模型 | 轻量版 | ¥20/实例/小时 | ¥10,000/月 |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型服务** | **模型类型** | **独占实例资源规格** | **后付费单价** | **预付费单价**<br>**（预付费）** |
| 悦动人像EMO-detect | 预置模型 | 轻量版 | ¥20/实例/小时 | ¥10,000/月 |
| 悦动人像EMO |
| 舞动人像AnimateAnyone-detect |
| 舞动人像AnimateAnyone |

如果需要部署更多模型，请参考此[解决方案](https://www.aliyun.com/solution/tech-solution/deepseek-r1-for-platforms)并结合具体业务需求选择最适合的部署方案。

## 部署方法

您可以在控制台上部署模型，请参考以下操作步骤：

> 如果提示权限不足，请参考： [部署时提示权限不足怎么办？](https://help.aliyun.com/zh/model-studio/model-deployment-introduction#5c1c099745drz "")

|     |     |
| --- | --- |
| 1. 前往[模型部署控制台（北京）](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/model_deploy/create)。 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9498900771/p1051037.png) |
| 2. 选择模型、计费方式，其他设置保持默认，最后设置模型名称并开始部署。<br>   <br>   <br>   > 需先完成 [模型调优](https://help.aliyun.com/zh/model-studio/model-training-on-console#a6da1accf0dun "")，方可部署大部分模型。 |
| 3. 部署状态为 **运行中** 时，代表该模型已部署成功。<br>   <br>**重要**<br>模型部署成功后将产生费用。 |

### **部署配置**

模型单元

|     |     |
| --- | --- |
| **配置内容** | **配置详情** |
| 配置模型推理模式 | 部分模型在以 **模型单元** 方式部署时，可配置推理模式、最长上下文等。<br>- Instruct - 模型部署后以 **非思考模式** 进行推理。<br>  <br>- Thinking - 模型部署后以思考模式进行推理。 |
| 最长上下文 | 部分模型的 **模型单元** 部署模式支持该设置。最长上下文长度基于模型类型。 |
| 服务限流 | 部分模型的 **模型单元** 部署模式支持该设置，可限制模型调用的 RPM、TPM。 |

## **部署后调用**

模型部署成功后，支持通过 [OpenAI 兼容](https://help.aliyun.com/zh/model-studio/qwen-api-reference/#d397bcc41eu3q "")、 [Dashscope](https://help.aliyun.com/zh/model-studio/qwen-api-reference/#69cac67a477k2 "") 及 [Assistant SDK](https://help.aliyun.com/zh/model-studio/assistant#87b4aacb4bsww "") 进行调用。

在调用已部署成功的模型时，`model`的取值应为模型部署成功后的模型`code`。请前往[模型部署控制台（北京）](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/model_deploy/create)界面获取 **模型code**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0929900771/p1051901.png)

示例代码以调用微调后的 qwen3-8b 模型为例：

**说明**

模型特性（是否支持非流式输出、结构化输出等）与 [微调前的模型](https://help.aliyun.com/zh/model-studio/models "") 保持一致。

经过调优的深度思考模型在调用时是否开启深度思考，建议与调优数据格式一致：

- 调优数据含深度思考，调用时建议开启`enable_thinking`参数。

- 调优数据不含深度思考，调用时不建议开启`enable_thinking`参数。


DashScope

OpenAI兼容接口

```python
import os
import dashscope

messages = [\
    {"role": "system", "content": "You are a helpful assistant."},\
    {"role": "user", "content": "你是谁？"},\
]
response = dashscope.Generation.call(
    # 若没有配置环境变量，请用百炼API Key将下一行替换为：api_key="sk-xxx",
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    model="qwen3-14b-xxx-xxx",  # 请替换为模型部署成功后的code
    messages=messages,
    result_format="message",
    enable_thinking=False,
)
print(response)
```

```python
import os
from openai import OpenAI

client = OpenAI(
    # 若没有配置环境变量，请用百炼API Key将下一行替换为：api_key="sk-xxx",
    api_key=os.getenv('DASHSCOPE_API_KEY'),
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)

completion = client.chat.completions.create(
    model="qwen3-14b-xxx-xxx",  # 请替换为模型部署成功后的code
    messages=[\
        {"role": "system", "content": "You are a helpful assistant."},\
        {"role": "user", "content": "你是谁？"},\
    ],
    extra_body={"enable_thinking": False},
)
print(completion)
```

## 部署服务扩缩容

- 预置吞吐（按时长）：点击 **扩缩容** 按钮，自助、手动调节实例数量。

- 模型单元（按时长）：点击 **扩缩容** 按钮，自助、手动调节实例数量。

- 按 Token 调用量：点击 **扩容** 按钮，填写并提交扩容申请表单，等待人工审核。


## **部署服务下线**

前往[模型部署控制台（北京）](https://bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/model_deploy/create)，找到要下线的部署服务，点击 **下线** 并确认。下线后将不再产生计费。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0929900771/p1051902.png)

## **常见问题**

### **可以上传和部署自己的模型吗？**

支持在 [我的模型控制台（北京）](https://pre-bailian.console.aliyun.com/cn-beijing/?tab=model#/efm/model_center) 导入部分开源模型，详细支持列表请参考： [模型导入](https://help.aliyun.com/zh/model-studio/model-import "")。

此外，阿里云人工智能平台 PAI 提供了部署自有模型的功能，您可以参考 [PAI-LLM大语言模型部署](https://help.aliyun.com/zh/pai/user-guide/deploy-an-llm/ "") 了解部署方法。

### **部署时提示权限不足怎么办？**

1. 如果显示 **“缺少该模块的权限”**，请确保您的账号在该业务空间的权限管理页面中拥有 **模型部署-操作** 权限。

![PixPin_2025-11-27_15-09-44](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1126324671/p1030122.png)

如果无法正常操作，请联系您的组织或 IT 管理员添加相关权限或代为检查权限问题。

2. 如果部署时报错“ **xx业务空间没有部署xx模型的权限**”，请前往百炼的 [业务空间管理](https://bailian.console.aliyun.com/?tab=globalset#/efm/business_management) 页面，为对应业务空间添加对应模型的部署权限。


> API 调用报错：`Workspace xxx does not have deployment privilege for model xxxx`。


![PixPin_2025-11-27_15-03-57](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1816324671/p1030115.png)

![PixPin_2025-11-27_15-06-41](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1816324671/p1030118.png)

如果提示权限不足，请联系您的组织或 IT 管理员添加相关权限或代为操作。


### **该如何切换到其他的计费方式？**

只能释放原有资源，再通过需要的计费方式创建新资源。

建议按照以下步骤进行切换：

1. 使用需要的计费方式部署新的资源。

2. 切换 API 并测试服务可用性。

3. 下线释放原有资源。