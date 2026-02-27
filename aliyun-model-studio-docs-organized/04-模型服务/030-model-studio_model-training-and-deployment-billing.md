### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[产品计费](https://help.aliyun.com/zh/model-studio/test-1/)模型训练与部署计费

# 模型训练与部署计费

更新时间：2026-02-24 20:54:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：模型调用计费](https://help.aliyun.com/zh/model-studio/model-pricing)[下一篇：节省计划与资源包](https://help.aliyun.com/zh/model-studio/savings-plan-and-resource-package)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型训练计费

文本生成模型-千问

视频生成模型-万相

模型部署计费

文本生成模型-千问

图像和视频生成模型（预置模型）

常见问题

本文介绍阿里云百炼平台的模型训练、模型部署的计费规则及价格。

## **模型训练计费**

### **文本生成模型-千问**

**说明**

模型训练流程请参见 [模型调优](https://help.aliyun.com/zh/model-studio/model-training-overview "")。训练完成后的新模型需先完成 **模型部署**，才能评测和调用。

|     |     |
| --- | --- |
| **计费方式** | 按训练Token计费 |
| **计费公式** | 模型训练费用 = （训练数据 Token 总数 + 混合训练数据 Token 总数）× 循环次数 × 训练单价（最小计费单位：1 token）<br>> 您可以查看 [模型训练控制台](https://bailian.console.aliyun.com/#/efm/model_manager/create) 底部的预估训练费用，并单击 **计算详情**，查看训练 Token 总数、循环次数和训练单价 **。** |

千问

千问VL

|     |     |     |
| --- | --- | --- |
| **模型服务** | **模型规格** | **价格** |
| 千问2.5-72B | qwen2.5-72b-instruct | 0.15元/千Token |
| 千问2-开源版-72B | qwen2-72b-instruct |
| 千问1.5-开源版-72B | qwen1.5-72b-chat |
| 千问-Plus-0723 | qwen-plus-0723 |
| Qwen-Plus-character-2025-11-06 | qwen-plus-character-2025-11-06 |
|  |
| 千问3-32B | qwen3-32b | 0.04 元/千Token |
|  |
| 千问3-30B-A3B-Instruct-2507 | qwen3-30b-a3b-instruct-2507 | 0.03元/千Token |
| 千问3-14B | qwen3-14b |
| 千问3-VL-32B-Base | qwen3-vl-32b-base |
| 千问2.5-32B | qwen2.5-32b-instruct |
| 千问2.5-14B | qwen2.5-14b-instruct |
| 千问1.5-开源版-14B | qwen1.5-14b-chat |
| 千问-Plus | qwen-plus |
| 千问Turbo | qwen-turbo |
| 千问-Turbo-0624 | qwen-turbo-0624 |
|  |
| 千问3-VL-8B-Base | qwen3-vl-8b-base | 0.012元/千Token |
|  |
| 千问3-8B | qwen3-8b | 0.006元/千Token |
| 千问3-4B-Instruct-2507 | qwen3-4b-instruct-2507 |
| 千问3-4B-Base-2507 | qwen3-4b-base-2507 |
| 千问3-VL-4B-Instruct | qwen3-vl-4b-instruct |
| 千问2.5-7B | qwen2.5-7b-instruct |
| 千问2-开源版-7B | qwen2-7b-instruct |
| 千问1.5-开源版-7B | qwen1.5-7b-chat |
|  |
| 千问3-1.7B | qwen3-1.7b | 0.0045元/千Token |
|  |
| 千问3-0.6B | qwen3-0.6b | 0.003元/千Token |

|     |     |     |
| --- | --- | --- |
| **模型服务** | **模型规格** | **价格** |
| 千问VL-Max-0201 | qwen-vl-max-0201 | 0.15元/千Token |
| 千问VL-Plus | qwen-vl-plus | 0.03元/千Token |
|  |  |  |
| 千问3-VL-8B-Instruct | qwen3-vl-8b-instruct | 0.012元/千Token |
| 千问3-VL-8B-Thinking | qwen3-vl-8b-thinking |
|  |  |  |
| 千问2.5-VL-72B | qwen2.5-vl-72b-instruct | 0.05 元/千Token |
| 千问2.5-VL-32B | qwen2.5-vl-32b-instruct | 0.02 元/千Token |
| 千问2.5-VL-7B | qwen2.5-vl-7b-instruct | 0.01 元/千Token |

### **视频生成模型-万相**

**说明**

模型训练流程请参见 [模型调优](https://help.aliyun.com/zh/model-studio/wan-video-generation-finetune-guide "")。训练完成后的新模型需先完成 **模型部署**，才能调用。

|     |     |
| --- | --- |
| **计费方式** | 按训练Token计费 |
| **计费公式** | 模型训练费用 = 训练Tokens总量 x 训练单价（计费单位：每千Token） |

**训练Tokens总量的计算公式**

训练Tokens总量=(i=1∑N​视频i​的计费时长)×1024max\_pixels​×n\_epochs

其中：

- N：训练集中的视频总数。

- max\_pixels：训练时指定的超参数，表示视频的最大像素数（创建微调任务时配置）。

- n\_epochs：训练时指定的超参数，表示循环次数（创建微调任务时配置）。

- 单个视频计费时长计算规则：先将原始视频时长（秒）四舍五入取整，再根据模型限制取最终值。

  - wan2.5模型：`计费时长=min(10, 四舍五入后的时长)`，即单条视频最多按 10 秒计算。

  - wan2.2模型：`计费时长=min(5, 四舍五入后的时长)`，即单条视频最多按 5 秒计算。

| **模型服务** | **模型名称** | **训练价格（每千Token）** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型服务** | **模型名称** | **训练价格（每千Token）** |
| 万相-图生视频-基于首帧 | wan2.2-i2v-flash | 0.06元 |
| wan2.5-i2v-preview | 0.32元 |
| 图生视频-基于首尾帧 | wan2.2-kf2v-flash | 0.06元 |

**计费示例**

假设训练集包含 2 条视频，时长分别为 3.4 秒 和 6.5 秒，max\_pixels = 262144，n\_epochs = 400，训练单价 = 0.06元/千Token：

- 时长计算：

  - 视频 1：3.4 → 四舍五入 → 3 秒 → 计费时长 = min(5, 3) = 3

  - 视频 2：6.5 → 四舍五入 → 7 秒 → 计费时长 = min(5, 7) = 5

  - 总计费时长 = 3 + 5 = 8 秒
- 训练 Tokens 总量 = 8 ×（2262144/1024）× 400 = 819200 = 819.2 千 Token

- 模型训练费用 = 819.2 × 0.06 = 49.152 元


## **模型部署计费**

### **文本生成模型-千问**

#### 方式一： **按预置吞吐的使用时长计费**

**适用场景**：追求稳定吞吐保障和高并发低延迟，且流量可预估的场景。

| **计费方式** | **计费公式** |
| --- | --- |

|     |     |
| --- | --- |
| **计费方式** | **计费公式** |
| 按使用时长和预置吞吐 | 费用 = 使用时长 × (输入 TPM 单价 × 输入 TPM + 输出 TPM 单价 × 输出 TPM) |

| **模型名称** | **模型类型** | **最长上下文**<br>**（输入 Token + 输出 Token）** | **最长输入 Token** | **后付费-按小时** | **预付费-按天** |
| --- | --- | --- | --- | --- | --- |
| **输入（Per 10k TPM）** | **输出（Per 1k TPM）** | **输入（Per 10k TPM）** | **输出（Per 1k TPM）** |
| --- | --- | --- | --- |

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

#### 方式二： **按模型单元的使用时长计费**

**适用场景**：对并发要求较高、需要独占算力资源的场景。

**说明**

**模型单元** 是百炼平台提供的 **算力部署最小单位**，按照使用时长收取资源费用。

| **计费方式** | **计费公式** |
| --- | --- |

|     |     |
| --- | --- |
| **计费方式** | **计费公式** |
| 按资源占用时长（后付费） | 费用 = 使用时长（小时）× 模型单元数量 × 模型单元单价（不满1分钟按1分钟计费）<br>> 部署前可以在 [模型部署控制台](https://bailian.console.aliyun.com/#/efm/model_deploy/create) 查看不同模型的预估每小时费用。 |
| 资源包月（预付费） | 费用 = 购买时长（月）× 模型单元数量 × 模型单元包月单价（不满1天按1天计费）<br>> 如果在开始使用的一个月内提前退订，日单价将为 **1.2** 倍，退订细节请参考 [非全额退款](https://help.aliyun.com/zh/user-center/cancel-subscription/#6829b8dd122qe "")。 |

**选择“模型单元”有什么优势？**

基于时间的计费方式都支持手动扩缩容，灵活调整并发量。

- 按模型单元的资源占用时长计费的计费粒度更小（分钟），使用灵活。

- 模型单元资源包月计费的计费周期长（月），但更加便宜（6.7折）。


> 退订细节请参考 [非全额退款](https://help.aliyun.com/zh/user-center/cancel-subscription/#6829b8dd122qe "")。


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


#### 方式三：按模型 Token 调用量计费

**适用场景**：调用量波动大、希望低成本启动的场景。

按模型调用量计费方式价格很低。如果需要进一步增加并发量，需要部署后在模型部署控制台手动申请，平台会进行人工审批。

| **计费方式** | **计费公式** |
| --- | --- |

|     |     |
| --- | --- |
| **计费方式** | **计费公式** |
| 按模型调用量 | 费用 = 模型输入 Token 数 × 模型输入单价 + 模型输出 Token 数 × 模型输出单价（最小计费单位：1 token） |

**控制台示例**：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5539394371/p881644.png)

**重要**

一个模型是可以在百炼的 [模型调优](https://help.aliyun.com/zh/model-studio/model-training-on-console#aa8da600c3x52 "") 中进行重复训练的。

只有在 **基于以下基础模型进行“SFT高效训练”** 后获得的模型，才支持按调用量计费。

| **基础模型** | **模型类型** | **最长上下文** | **输入单价** | **输出单价** |
| --- | --- | --- | --- | --- |

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

#### **方式四：按实例的使用时长计费（已停止购买）**

**说明**

自 2025年 10月 24 日起，按实例计费方式不再支持新购。

|     |     |
| --- | --- |
| **计费方式** | **计费公式** |
| 按实例资源占用时长计费 | 费用 = 资源占用时长（小时）× 实例数量 × 实例单价（不满1小时按1小时计费）<br>> 部署前可以在 [模型部署控制台](https://bailian.console.aliyun.com/#/efm/model_deploy/create) 查看不同模型的预估每小时费用。 |
| 资源包月计费/预付费 | 费用 = 购买时长（月）× 实例数量 × 模型对应的实例单价<br>购买资源：请前往 [模型部署控制台](https://bailian.console.aliyun.com/#/efm/model_deploy)（点击右上角的 **资源池管理**）购买。（资源购买完成后便开始计费）<br>退订资源：请前往主账号的 [退订管理](https://usercenter2.aliyun.com/refund/refund) 退订。退订后，将根据未用时长退回未使用金额。（不满1天按1天计费） |

千问

千问VL

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型服务** | **模型类型** | **独占实例资源规格** | **实例单价（按小时）** | **实例单价（按月，预付费）** |
| 千问-Turbo-0624 | 微调模型 | 基础版v2-Qwen2 | 40元/小时 | 20,000元/月 |
| 千问2.5-开源版-14B | 基础版v2-Qwen2 |
| 千问2.5-开源版-7B | 基础版v2-Qwen2 |
| 千问2-开源版-7B | 基础版v2-Qwen2 |
| 千问1.5-开源版-14B | 基础版 |
| 千问1.5-开源版-7B | 基础版 |
| 千问3-14B | NA | 不支持按月预付费 |
| 千问3-8B | NA |
| 千问-Plus-0723 | 标准版v2-Qwen2 | 160元/小时 | 80,000元/月 |
| 千问2.5-开源版-72B | 标准版v2-Qwen2 |
| 千问2.5-开源版-32B | 标准版v2-Qwen2 |
| 千问2-开源版-72B | 标准版v2-Qwen2 |
| 千问1.5-开源版-72B | 标准版 |
| 千问3-32B | NA | 不支持按月预付费 |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型服务** | **模型类型** | **独占实例资源规格** | **实例单价（按小时）** | **实例单价（按月，预付费）** |
| 千问VL-Plus | 微调模型 | 基础版 | 40元/小时 | 20,000元/月 |
| 千问VL-Max-0201 | 标准版 | 160元/小时 | 80,000元/月 |
| 千问2.5-VL-7B | NA | 40元/小时 | 不支持按月预付费 |
| 千问2.5-VL-32B | NA | 160元/小时 |
| 千问2.5-VL-72B | NA | 160元/小时 |

### **图像和视频生成模型（预置模型）**

| **计费方式** | **计费公式** |
| --- | --- |

|     |     |
| --- | --- |
| **计费方式** | **计费公式** |
| 按实例资源占用时长计费 | 费用 = 资源占用时长（小时）× 实例数量 × 实例单价（不满1小时按1小时计费）<br>> 部署前可以在 [模型部署控制台](https://bailian.console.aliyun.com/#/efm/model_deploy/create) 查看不同模型的预估每小时费用。 |
| 实例包月计费/预付费 | 费用 = 购买时长（月）× 实例数量 × 模型对应的实例单价<br>购买资源：请前往 [模型部署控制台](https://bailian.console.aliyun.com/#/efm/model_deploy)（点击右上角的 **资源池管理**）购买。（资源购买完成后便开始计费）<br>退订资源：请前往主账号的 [退订管理](https://usercenter2.aliyun.com/refund/refund) 退订。退订后，将根据未用时长退回未使用金额。（不满1天按1天计费） |

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

## **常见问题**

#### **Q：** 模型部署什么时候开始计费？

A：当模型完成部署，即状态为 **运行中** 时，开始收取模型部署的费用。模型状态为 **部署中**、 **欠费**、 **部署失败** 时，均不会计费。

如果是包月预付费，模型状态为 **运行中** 后，开始消耗包月时间。

#### **Q：** 取消模型训练会收费么？

A： **会收费**。如果您主动取消训练，之前已产生的费用仍会被计算。其他原因导致的训练中断，阿里云百炼不会向您收取训练费用。

#### **Q：怎么查看已部署模型的调用统计？**

A：请访问[模型监控（北京）](https://bailian.console.aliyun.com/?tab=model#/model-telemetry)、 [模型监控（弗吉尼亚）](https://modelstudio.console.aliyun.com/us-east-1?tab=dashboard#/model-telemetry)、 [模型监控（新加坡）](https://modelstudio.console.aliyun.com/?spm=a2c4g.11186623.0.0.39086143l397a1&tab=model#/model-telemetry)页面。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8302853471/p936026.png)