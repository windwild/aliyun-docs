### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[开始使用](https://help.aliyun.com/zh/model-studio/get-started-with-models/)限流

# 限流

更新时间：2026-02-24 10:02:49

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

限流规则

限流FAQ

为什么触发限流？

如何查看模型调用量？

遇到限流后多久恢复？

如何避免限流？

文本生成-千问

千问语言模型

千问VL（视觉理解/图生文）

千问Omni

千问Omni-Realtime

千问OCR（文字提取）

千问Audio（音频理解）

千问数学模型

千问Coder

千问翻译模型

千问数据挖掘模型

千问深入研究模型

通义晓蜜对话分析模型

文本生成-千问-开源版

千问语言模型开源版

Qwen-VL

Qwen-Omni

Qwen3-Omni-Captioner

Qwen-Audio

Qwen-Math

Qwen-Coder

文本生成-第三方模型

DeepSeek

DeepSeek-硅基流动

Kimi

Kimi-月之暗面

GLM

MiniMax

MiniMax-稀宇科技

Llama

百川

图像生成

千问（Qwen-Image）

文生图-Z-Image

万相

图像编辑与生成

人物写真生成-FaceChain

创意文字生成-WordArt锦书

AI试衣-OutfitAnyone

图像生成-第三方模型

StableDiffusion文生图模型

FLUX文生图模型

语音合成（文本转语音）

千问语音合成

千问实时语音合成

千问声音复刻

千问声音设计

CosyVoice语音合成

Sambert语音合成

语音识别（语音转文本）与翻译（语音转成指定语种的文本）

千问3-LiveTranslate-Flash

千问3-LiveTranslate-Flash-Realtime

千问录音文件识别

千问实时语音识别

Gummy语音识别/翻译

Fun-ASR录音文件识别

Fun-ASR实时语音识别

Paraformer语音识别

SenseVoice语音识别

视频生成

万相系列

舞动人像AnimateAnyone

悦动人像EMO

灵动人像LivePortrait

声动人像VideoRetalk

表情包Emoji

视频风格重绘

向量模型

文本向量

多模态向量

文本分类、抽取、排序

OpenNLU

文本排序模型

行业

通义法睿（法律模型）

意图理解

角色扮演

界面交互

已下线模型

为了保证用户调用模型的公平性，阿里云百炼设置了基础限流。限流基于模型维度且与用户的阿里云主账号相关联，按照该账号下所有API-KEY调用该模型的总和计算限流。若超出限制，API请求将会失败，需等到解除限流条件时再次调用。

## **限流规则**

- **主账号维度**：按 **主账号** 下，所有RAM子账号、所有业务空间、所有API-KEY的调用总和计算。

- **不同模型独立限流**：具体参见下方表格。


## **限流FAQ**

### **为什么触发限流？**

根据错误信息判断：

- Requests rate limit exceeded或You exceeded your current requests list：表示 **调用频率** 触发限流。

- Allocated quota exceeded或You exceeded your current quota：表示 **Token消耗** 触发限流。

- Request rate increased too quickly：表示在未达到RPM或TPM限流条件时，因 **调用频率在短时间内激增**，触发了系统稳定性保护机制。

- 其他报错请参考 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 确认原因。


**注意**：除了RPM（Requests Per Minute，每分钟请求数）和TPM，限流策略可能按秒级 **RPS**（RPM/60）与 **TPS**（TPM/60）限制，即使总调用量未达到每分钟上限，短时间内的请求爆发也可能触发限流。

### **如何查看模型调用量？**

模型调用完 **一小时后**，在模型监控（ [北京](https://bailian.console.aliyun.com/?tab=model#/model-telemetry) 或 [新加坡](https://modelstudio.console.aliyun.com/?tab=model#/model-telemetry)）页面设置查询条件（例如，选择时间范围、业务空间等），再在 **模型列表** 区域找到目标模型并单击 **操作** 列的 **监控**，即可查看该模型的调用统计结果。具体请参见 [模型监控](https://help.aliyun.com/zh/model-studio/model-telemetry/ "") 文档。

> 数据按小时更新，高峰期可能有小时级延迟，请您耐心等待。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6923304571/p992753.png)

### **遇到限流后多久恢复？**

**通常在一分钟内恢复**。若出现其他报错，请根据 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行解决。

### **如何避免限流？**

1. **选用高限流模型**

   - 优先使用 [qwen-plus](https://help.aliyun.com/zh/model-studio/models#6c45e49509gtr "") 等限流宽松的模型。

   - 稳定版或最新版比带日期的快照版本限流更宽松。
2. **优化调用策略**

   - **调整调用频率**：触发Requests rate limit exceeded或You exceeded your current requests list时，降低调用频率。

   - **减少Token消耗：** 触发Allocated quota exceeded或You exceeded your current quota时，缩短输入或输出长度。

   - **平滑请求速率**：当调用频率骤增并触发系统稳定性保护（收到 Request rate increased too quickly 报错）时，建议优化客户端调用逻辑，采用平滑请求策略（如匀速调度、指数退避或请求队列缓冲），将请求均匀分散在时间窗口内，避免瞬时高峰。
3. **添加备选模型**

建议您在遇到限流报错后切换到备用模型继续生成，提升并发并降低失败概率。以下代码展示了调用 `qwen-plus-2025-07-28` 触发限流，改用 `qwen-plus-2025-07-14` 重发请求的示例。



**示例代码**




















```python
import os
import asyncio
from openai import AsyncOpenAI, APIStatusError

# 配置
API_KEY = os.getenv("DASHSCOPE_API_KEY")
# 主用模型
MODEL = "qwen-plus-2025-07-28"
# 备选模型
BACKUP_MODEL = "qwen-plus-2025-07-14"
# 测试问题
QUESTION = "你是谁？"
# 并发设置
NUM_REQUESTS = 10

client = AsyncOpenAI(
       api_key=API_KEY,
       base_url="https://dashscope.aliyuncs.com/compatible-mode/v1"
)

async def send_request(model):
       """发送单个请求"""
       try:
           await client.chat.completions.create(
               model=model,
               messages=[{"role": "user", "content": QUESTION}]
           )
           return True
       except APIStatusError as e:
           if e.status_code == 429:
               print(f"[限流触发] 模型 {model}")
               return False
           raise
       except Exception as e:
           print(f"[请求失败] 模型 {model}，错误：{e}")
           return False

async def task(i):
       # 尝试主模型
       if await send_request(MODEL):
           return True
       # 限流时尝试备用模型
       return await send_request(BACKUP_MODEL)

async def main():
       results = await asyncio.gather(*(task(i) for i in range(NUM_REQUESTS)))
       print(f"成功请求: {sum(results)}, 失败请求: {len(results) - sum(results)}")

if __name__ == "__main__":
       asyncio.run(main())
```

4. **任务拆分**：处理长对话或大型文档会快速消耗大量Token。可以将大批量任务拆分为小批次，在不同时间段提交。

5. **批量推理**：如果无需实时返回结果，可使用 [批量推理](https://help.aliyun.com/zh/model-studio/batch-inference "")（Batch API），不受实时限流约束，但需考虑排队和处理时间。


## **文本生成-千问**

### **千问语言模型**

中国内地

全球

国际

美国

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-max | 30,000 | 5,000,000 |
| qwen3-max-2026-01-23 | 600 | 1,000,000 |
| qwen3-max-2025-09-23 | 60 | 100,000 |
| qwen3-max-preview | 600 | 1,000,000 |
| qwen-max<br>> 用 [Batch API](https://help.aliyun.com/zh/model-studio/openai-compatible-batch-file-input/ "") 调用服务时，不受限流限制。 | 1,200 |
| qwen-max-latest |
| qwen-max-2025-01-25<br>（qwen-max-0125） | 60 | 100,000 |
| qwen-max-2024-09-19<br>（qwen-max-0919） |

| qwen-max-2024-04-28<br>（qwen-max-0428） |
| qwen3.5-plus | 30,000 | 5,000,000 |
| qwen3.5-plus-2026-02-15 | 600 | 1,000,000 |
| qwen-plus<br>> 用 [Batch API](https://help.aliyun.com/zh/model-studio/openai-compatible-batch-file-input/ "") 调用服务时，不受限流限制。 | 30,000 | 5,000,000 |
| qwen-plus-latest | 15,000 | 1,200,000 |
| qwen-plus-2025-12-01 | 120 | 1,000,000 |
| qwen-plus-2025-09-11 | 60 |
| qwen-plus-2025-07-28<br>（qwen-plus-0728） |
| qwen-plus-2025-07-14<br>（qwen-plus-0714） | 100,000 |
| qwen-plus-2025-04-28<br>（qwen-plus-0428） | 1,000,000 |
| qwen-plus-2025-01-25<br>（qwen-plus-0125） | 150,000 |
| qwen-plus-2025-01-12<br>（qwen-plus-0112） |
| qwen-plus-2024-12-20<br>（qwen-plus-1220） |
| qwen3.5-flash | 30,000 | 10,000,000 |
| qwen3.5-flash-2026-02-23 | 600 | 1,000,000 |
| qwen-flash | 30,000 | 10,000,000 |
| qwen-flash-2025-07-28 | 60 | 1,000,000 |
| qwen-turbo<br>> 用 [Batch API](https://help.aliyun.com/zh/model-studio/openai-compatible-batch-file-input/ "") 调用服务时，不受限流限制。 | 1,200 | 5,000,000 |
| qwen-turbo-latest |
| qwen-turbo-2025-07-15<br>(qwen-turbo-0715) | 60 | 100,000 |
| qwen-turbo-2025-04-28<br>(qwen-turbo-0428) | 1,000,000 |
| qwen-turbo-2025-02-11<br>(qwen-turbo-0211) | 5,000,000 |
| qwen-turbo-2024-11-01<br>(qwen-turbo-1101) |
| qwq-plus | 600 | 1,000,000 |
| qwq-plus-latest |
| qwq-plus-2025-03-05 | 60 | 100,000 |
| qwen-long | 1,200 | 3,000,000 |
| qwen-long-latest | 60,000 |
| qwen-long-2025-01-25<br>(qwen-long-0125) | 3 | 7,500 |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-max | 600 | 1,000,000 |
| qwen3-max-2025-09-23 | 60 | 100,000 |
| qwen3-max-preview | 600 | 1,000,000 |
| qwen-plus | 15,000 | 5,000,000 |
| qwen-plus-2025-12-01 | 60 | 1,000,000 |
| qwen-plus-2025-09-11 |
| qwen-plus-2025-07-28 |
| qwen-flash | 15,000 | 10,000,000 |
| qwen-flash-2025-07-28 | 60 | 1,000,000 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-max | 600 | 1,000,000 |
| qwen3-max-2026-01-23 |
| qwen3-max-2025-09-23 | 60 | 100,000 |
| qwen3-max-preview | 600 | 1,000,000 |
| qwen-max | 120 | 100,000 |
| qwen-max-latest | 600 | 1,000,000 |
| qwen-max-2025-01-25<br>(qwen-max-0125) | 60 | 100,000 |
| qwen3.5-plus | 15,000 | 5,000,000 |
| qwen3.5-plus-2026-02-15 | 60 | 1,000,000 |
| qwen-plus-latest | 600 | 1,000,000 |
| qwen-plus-2025-12-01 | 120 |
| qwen-plus-2025-09-11 | 120 |
| qwen-plus-2025-07-28 | 60 | 100,000 |
| qwen-plus-2025-07-14<br>(qwen-plus-0714) |
| qwen-plus-2025-04-28<br>(qwen-plus-0428) | 1,000,000 |
| qwen-plus-2025-01-25<br>(qwen-plus-0125) | 100,000 |
| qwen3.5-flash | 15,000 | 5,000,000 |
| qwen3.5-flash-2026-02-23 | 600 | 1,000,000 |
| qwen-flash | 600 | 5,000,000 |
| qwen-flash-2025-07-28 | 600 | 5,000,000 |
| qwq-plus | 60 | 100,000 |
| qwen-turbo | 240 | 100,000 |
| qwen-turbo-latest | 600 | 5,000,000 |
| qwen-turbo-2025-04-28<br>(qwen-turbo-0428) | 60 | 1,000,000 |
| qwen-turbo-2024-11-01<br>(qwen-turbo-1101) | 5,000,000 |

在 [美国部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源仅限于美国境内。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-plus-us | 600 | 1,000,000 |
| qwen-plus-2025-12-01-us | 60 |
| qwen-flash-us | 600 | 5,000,000 |
| qwen-flash-2025-07-28-us |

### **千问VL（视觉理解/图生文）**

中国内地

全球

国际

美国

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-vl-plus | 3,000 | 5,000,000 |
| qwen3-vl-plus-2025-12-19 | 60 | 100,000 |
| qwen3-vl-plus-2025-09-23 |
| qwen3-vl-flash | 3,000 | 5,000,000 |
| qwen3-vl-flash-2026-01-22 | 60 | 100,000 |
| qwen3-vl-flash-2025-10-15 |
| qwen-vl-max | 1,200 | 1,000,000 |
| qwen-vl-max-latest |
| qwen-vl-max-2025-08-13<br>（qwen-vl-max-0813） | 60 | 100,000 |
| qwen-vl-max-2025-04-08<br>（qwen-vl-max-0408） |
| qwen-vl-max-2025-04-02<br>（qwen-vl-max-0402） |
| qwen-vl-max-2025-01-25<br>（qwen-vl-max-0125） |
| qwen-vl-max-2024-12-30<br>（qwen-vl-max-1230） |
| qwen-vl-max-2024-11-19<br>（qwen-vl-max-1119） |
| qwen-vl-plus | 1,200 | 1,000,000 |
| qwen-vl-plus-latest |
| qwen-vl-plus-2025-08-15<br>（qwen-vl-plus-0815） | 60 | 100,000 |
| qwen-vl-plus-2025-07-10<br>（qwen-vl-plus-0710） |
| qwen-vl-plus-2025-05-07<br>（qwen-vl-plus-0507） |
| qwen-vl-plus-2025-01-25<br>（qwen-vl-plus-0125） |
| qwen-vl-plus-2025-01-02<br>（qwen-vl-plus-0102） |
| qvq-max |
| qvq-max-latest |
| qvq-max-2025-05-15<br>（qvq-max-0515） |
| qvq-max-2025-03-25<br>（qvq-max-0325） |
| qvq-plus |
| qvq-plus-latest |
| qvq-plus-2025-05-15<br>（qvq-plus-0515） |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-vl-plus | 1,200 | 1,000,000 |
| qwen3-vl-plus-2025-09-23 | 60 | 100,000 |
| qwen3-vl-flash | 1,200 | 1,000,000 |
| qwen3-vl-flash-2025-10-15 | 60 | 100,000 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-vl-plus | 1,200 | 1,000,000 |
| qwen3-vl-plus-2025-12-19 | 60 | 100,000 |
| qwen3-vl-plus-2025-09-23 | 120 | 1,000,000 |
| qwen3-vl-flash | 1,200 | 1,000,000 |
| qwen3-vl-flash-2026-01-22 | 60 | 100,000 |
| qwen3-vl-flash-2025-10-15 | 120 | 1,000,000 |
| qwen-vl-max | 1,200 | 1,000,000 |
| qwen-vl-max-latest |
| qwen-vl-max-2025-08-13<br>(qwen-vl-max-0813) | 60 | 100,000 |
| qwen-vl-max-2025-04-08<br>(qwen-vl-max-0408) | 1,200 | 1,000,000 |
| qwen-vl-plus |
| qwen-vl-plus-latest |
| qwen-vl-plus-2025-08-15<br>(qwen-vl-plus-0815) | 120 | 1,000,000 |
| qwen-vl-plus-2025-05-07<br>(qwen-vl-plus-0507) |
| qwen-vl-plus-2025-01-25<br>(qwen-vl-plus-0125) | 1,200 |
| qvq-max | 60 | 100,000 |
| qvq-max-latest |
| qvq-max-2025-03-25<br>(qvq-max-0325) |

在 [美国部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源仅限于美国境内。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-vl-flash-us | 1,200 | 1,000,000 |
| qwen3-vl-flash-2025-10-15-us | 120 | 1,000,000 |

### **千问Omni**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-omni-flash | 60 | 100,000 |
| qwen3-omni-flash-2025-12-01 |
| qwen3-omni-flash-2025-09-15 |
| qwen-omni-turbo |
| qwen-omni-turbo-latest |
| qwen-omni-turbo-2025-03-26<br>（qwen-omni-turbo-0326） |
| qwen-omni-turbo-2025-01-19<br>（qwen-omni-turbo-0119） |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-omni-flash | 60 | 100,000 |
| qwen3-omni-flash-2025-12-01 |
| qwen3-omni-flash-2025-09-15 |
| qwen-omni-turbo |
| qwen-omni-turbo-latest |
| qwen-omni-turbo-2025-03-26 |

### **千问Omni-Realtime**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-omni-flash-realtime | 60 | 100,000 |
| qwen3-omni-flash-realtime-2025-12-01 |
| qwen3-omni-flash-realtime-2025-09-15 |
| qwen-omni-turbo-realtime-latest |
| qwen-omni-turbo-realtime-2025-05-08 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-omni-flash-realtime | 60 | 100,000 |
| qwen3-omni-flash-realtime-2025-12-01 |
| qwen3-omni-flash-realtime-2025-09-15 |
| qwen-omni-turbo-realtime | 10,000 |
| qwen-omni-turbo-realtime-latest |
| qwen-omni-turbo-realtime **-** 2025-05-08 |

### **千问OCR（文字提取）**

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-vl-ocr | 600 | 6,000,000 |
| qwen-vl-ocr-latest | 1,200 |
| qwen-vl-ocr-2025-11-20 |
| qwen-vl-ocr-2025-08-28 | 600 |
| qwen-vl-ocr-2025-04-13 |
| qwen-vl-ocr-2024-10-28 |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-vl-ocr | 600 | 6,000,000 |
| qwen-vl-ocr-2025-11-20 | 1,200 |

在 [美国部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源仅限于美国境内。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-vl-ocr | 600 | 6,000,000 |
| qwen-vl-ocr-2025-11-20 | 1,200 |

### **千问Audio（音频理解）**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-audio-turbo | 120 | 100,000 |
| qwen-audio-turbo-latest | 60 |

### **千问数学模型**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-math-plus | 1,200 | 1,000,000 |
| qwen-math-plus-latest |
| qwen-math-plus-2024-09-19<br>（qwen-math-plus-0919） | 60 | 100,000 |
| qwen-math-plus-2024-08-16<br>（qwen-math-plus-0816） | 10 | 20,000 |
| qwen-math-turbo | 1200 | 1,000,000 |
| qwen-math-turbo-latest |
| qwen-math-turbo-2024-09-19<br>（qwen-math-turbo-0919） | 60 | 100,000 |

### **千问Coder**

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-coder-plus | 5,000 | 5,000,000 |
| qwen3-coder-plus-2025-09-23 | 60 | 1,000,000 |
| qwen3-coder-plus-2025-07-22 |
| qwen3-coder-flash | 5,000 | 5,000,000 |
| qwen3-coder-flash-2025-07-28 | 60 | 1,000,000 |
| qwen-coder-plus | 1,200 |
| qwen-coder-plus-latest |
| qwen-coder-plus-2024-11-06<br>（qwen-coder-plus-1106） | 120 | 200,000 |
| qwen-coder-turbo | 1,200 | 1,000,000 |
| qwen-coder-turbo-latest |
| qwen-coder-turbo-2024-09-19<br>（qwen-coder-turbo-0919） | 60 | 100,000 |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-coder-plus | 2,400 | 2,000,000 |
| qwen3-coder-plus-2025-09-23 | 60 | 1,000,000 |
| qwen3-coder-plus-2025-07-22 |
| qwen3-coder-flash | 1,200 |
| qwen3-coder-flash-2025-07-28 | 60 |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-coder-plus | 2,400 | 2,000,000 |
| qwen3-coder-plus-2025-09-23 | 600 | 1,000,000 |
| qwen3-coder-plus-2025-07-22 | 60 | 1,000,000 |
| qwen3-coder-flash | 600 | 5,000,000 |
| qwen3-coder-flash-2025-07-28 | 600 | 5,000,000 |

### **千问翻译模型**

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-mt-plus | 60 | 25,000 |
| qwen-mt-flash | 35,000 |
| qwen-mt-lite | 100,000 |
| qwen-mt-turbo | 35,000 |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-mt-plus | 60 | 25,000 |
| qwen-mt-flash | 35,000 |
| qwen-mt-lite | 100,000 |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-mt-plus | 60 | 100,000 |
| qwen-mt-flash |
| qwen-mt-lite |
| qwen-mt-turbo |

### **千问数据挖掘模型**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-doc-turbo | 600 | 3,000,000 |

### **千问深入研究模型**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-deep-research | 120 | 1,200,000 |

### **通义晓蜜对话分析模型**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| tongyi-xiaomi-analysis-flash | 600 | 1,000,000 |
| tongyi-xiaomi-analysis-pro |

## **文本生成-千问-开源版**

### **千问语言模型开源版**

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3.5-397b-a17b | 600 | 1,000,000 |
| qwen3.5-122b-a10b |
| qwen3.5-27b |
| qwen3.5-35b-a3b |
| qwen3-next-80b-a3b-thinking |
| qwen3-next-80b-a3b-instruct |
| qwen3-235b-a22b-thinking-2507 |
| qwen3-235b-a22b-instruct-2507 |
| qwen3-30b-a3b-thinking-2507 |
| qwen3-30b-a3b-instruct-2507 |
| qwen3-235b-a22b |
| qwen3-30b-a3b |
| qwen3-32b | 2400 |
| qwen3-14b | 600 |
| qwen3-8b |
| qwen3-4b |
| qwen3-1.7b |
| qwen3-0.6b |
| qwq-32b |
| qwq-32b-preview | 1,200 |
| qwen2.5-72b-instruct |
| qwen2.5-32b-instruct |
| qwen2.5-14b-instruct |
| qwen2.5-14b-instruct-1m | 5,000,000 |
| qwen2.5-7b-instruct | 1,000,000 |
| qwen2.5-7b-instruct-1m | 5,000,000 |
| qwen2.5-3b-instruct | 2,000,000 |
| qwen2.5-1.5b-instruct |
| qwen2.5-0.5b-instruct |
| qwen2-72b-instruct | 60 | 150,000 |
| qwen2-57b-a14b-instruct |
| qwen2-7b-instruct |
| qwen2-1.5b-instruct | 2,000,000 |
| qwen2-0.5b-instruct |
| qwen1.5-110b-chat | 10 | 20,000 |
| qwen1.5-72b-chat | 120 | 200,000 |
| qwen1.5-32b-chat | 10 | 20,000 |
| qwen1.5-14b-chat | 120 | 200,000 |
| qwen1.5-7b-chat |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-next-80b-a3b-thinking | 600 | 1,000,000 |
| qwen3-next-80b-a3b-instruct |
| qwen3-235b-a22b-thinking-2507 |
| qwen3-235b-a22b-instruct-2507 |
| qwen3-30b-a3b-thinking-2507 |
| qwen3-30b-a3b-instruct-2507 |
| qwen3-235b-a22b |
| qwen3-32b |
| qwen3-30b-a3b |
| qwen3-14b |
| qwen3-8b |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3.5-397b-a17b | 600 | 1,000,000 |
| qwen3.5-122b-a10b | 5,000,000 |
| qwen3.5-27b |
| qwen3.5-35b-a3b |
| qwen3-next-80b-a3b-thinking | 1,000,000 |
| qwen3-next-80b-a3b-instruct |
| qwen3-235b-a22b-thinking-2507 |
| qwen3-235b-a22b-instruct-2507 |
| qwen3-30b-a3b-thinking-2507 | 5,000,000 |
| qwen3-30b-a3b-instruct-2507 |
| qwen3-235b-a22b | 1,000,000 |
| qwen3-32b |
| qwen3-30b-a3b |
| qwen3-14b |
| qwen3-8b |
| qwen3-4b |
| qwen3-1.7b |
| qwen3-0.6b |
| qwen2.5-14b-instruct-1m | 1,200 | 5,000,000 |
| qwen2.5-7b-instruct-1m |
| qwen2.5-72b-instruct | 60 | 150,000 |
| qwen2.5-32b-instruct |
| qwen2.5-14b-instruct |
| qwen2.5-7b-instruct |

### **Qwen-VL**

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-vl-32b-thinking | 600 | 1,000,000 |
| qwen3-vl-32b-instruct |
| qwen3-vl-30b-a3b-thinking |
| qwen3-vl-30b-a3b-instruct |
| qwen3-vl-8b-thinking |
| qwen3-vl-8b-instruct |
| qwen3-vl-235b-a22b-thinking | 60 | 100,000 |
| qwen3-vl-235b-a22b-instruct |
| qwen2.5-vl-72b-instruct |
| qwen2.5-vl-32b-instruct |
| qwen2.5-vl-7b-instruct | 1,200 | 1,000,000 |
| qwen2.5-vl-3b-instruct |
| qwen2-vl-72b-instruct |
| qwen2-vl-7b-instruct |
| qwen2-vl-2b-instruct |
| qwen-vl-v1 | 60 | 10,000 |
| qwen-vl-chat-v1 |
| qvq-72b-preview | 60 | 100,000 |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-vl-235b-a22b-thinking | 60 | 100,000 |
| qwen3-vl-235b-a22b-instruct |
| qwen3-vl-32b-thinking | 600 | 1,000,000 |
| qwen3-vl-32b-instruct |
| qwen3-vl-30b-a3b-thinking |
| qwen3-vl-30b-a3b-instruct |
| qwen3-vl-8b-thinking |
| qwen3-vl-8b-instruct |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-vl-32b-thinking | 60 | 100,000 |
| qwen3-vl-32b-instruct |
| qwen3-vl-30b-a3b-thinking |
| qwen3-vl-30b-a3b-instruct |
| qwen3-vl-8b-thinking |
| qwen3-vl-8b-instruct |
| qwen3-vl-235b-a22b-thinking |
| qwen3-vl-235b-a22b-instruct |
| qwen2.5-vl-72b-instruct |
| qwen2.5-vl-32b-instruct |
| qwen2.5-vl-7b-instruct | 1,200 | 1,000,000 |
| qwen2.5-vl-3b-instruct |

### **Qwen-Omni**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen2.5-omni-7b | 60 | 100,000 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen2.5-omni-7b | 60 | 100,000 |

### **Qwen3-Omni-Captioner**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-omni-30b-a3b-captioner | 60 | 100,000 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-omni-30b-a3b-captioner | 60 | 100,000 |

### Qwen-Audio

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-audio-chat | 120 | 100,000 |

### **Qwen-Math**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen2.5-math-72b-instruct | 1,200 | 1,000,000 |
| qwen2.5-math-7b-instruct |
| qwen2.5-math-1.5b-instruct |

### **Qwen-Coder**

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-coder-next | 600 | 1,000,000 |
| qwen3-coder-480b-a35b-instruct |
| qwen3-coder-30b-a3b-instruct |
| qwen2.5-coder-32b-instruct | 1,200 |
| qwen2.5-coder-14b-instruct |
| qwen2.5-coder-7b-instruct |
| qwen2.5-coder-3b-instruct | 2,000,000 |
| qwen2.5-coder-1.5b-instruct |
| qwen2.5-coder-0.5b-instruct |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-coder-480b-a35b-instruct | 600 | 1,000,000 |
| qwen3-coder-30b-a3b-instruct | 600 | 1,000,000 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-coder-next | 600 | 1,000,000 |
| qwen3-coder-480b-a35b-instruct |
| qwen3-coder-30b-a3b-instruct |

## **文本生成-第三方模型**

### **DeepSeek**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| deepseek-v3.2 | 15,000 | 1,200,000 |
| deepseek-v3.2-exp | 15,000 | 1,200,000 |
| deepseek-v3.1 |
| deepseek-r1-0528 | 60 | 100,000 |
| deepseek-r1 | 15,000 | 1,200,000 |
| deepseek-v3 |
| deepseek-r1-distill-qwen-7b |
| deepseek-r1-distill-qwen-14b |
| deepseek-r1-distill-qwen-32b |
| deepseek-r1-distill-qwen-1.5b | 60 | 100,000 |
| deepseek-r1-distill-llama-8b |
| deepseek-r1-distill-llama-70b |

### **DeepSeek-硅基流动**

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| siliconflow/deepseek-v3.2 | 500 | 500,000 |
| siliconflow/deepseek-v3.1-terminus |
| siliconflow/deepseek-r1-0528 |
| siliconflow/deepseek-v3-0324 |

### **Kimi**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| kimi-k2.5 | 60 | 100,000 |
| kimi-k2-thinking | 60 | 100,000 |
| Moonshot-Kimi-K2-Instruct | 60 | 100,000 |

### **Kimi-月之暗面**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| kimi-k2.5 | 500 | 3,000,000 |

### **GLM**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| glm-5 | 60 | 1,000,000 |
| glm-4.7 |
| glm-4.6 |
| glm-4.5 |
| glm-4.5-air |

### **MiniMax**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| MiniMax-M2.5 | 60 | 1,000,000 |
| MiniMax-M2.1 | 60 | 100,000 |
| abab6.5s-chat |
| abab6.5t-chat |
| abab6.5g-chat |

### **MiniMax-稀宇科技**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| MiniMax/MiniMax-M2.5 | 500 | 2,000,000 |
| MiniMax/MiniMax-M2.1 |

### **Llama**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| llama-4-maverick-17b-128e-instruct | 10 | 20,000 |
| llama-4-scout-17b-16e-instruct |

### **百川**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| baichuan2-turbo-192k | 60 | 100,000 |
| baichuan2-turbo |

## **图像生成**

### **千问（Qwen-Image）**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型名称** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **任务下发接口调用限制** | **同时处理中任务数量（并发数）** |
| 文生图 | qwen-image-max | 2 次/分钟 | 同步接口无限制 |
| qwen-image-max-2025-12-30 | 2 次/分钟 | 同步接口无限制 |
| qwen-image-plus | 2 次/秒 | 同步接口无限制 / 异步接口 2 |
| qwen-image-plus-2026-01-09 | 2 次/秒 | 同步接口无限制 |
| qwen-image | 2 次/秒 | 同步接口无限制 / 异步接口 2 |
| 图像编辑 | qwen-image-edit-max | 2 次/分钟 | 同步接口无限制 |
| qwen-image-edit-max-2026-01-16 | 2 次/分钟 | 同步接口无限制 |
| qwen-image-edit-plus | 2 次/秒 | 同步接口无限制 |
| qwen-image-edit-plus-2025-12-15 | 2 次/秒 | 同步接口无限制 |
| qwen-image-edit-plus-2025-10-30 | 2 次/秒 | 同步接口无限制 |
| qwen-image-edit | 2 次/秒 | 同步接口无限制 |
| 图像翻译 | qwen-mt-image | 1 次/秒 | 2 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **任务下发接口调用限制** | **同时处理中任务数量（并发数）** |
| 文生图 | qwen-image-max | 2 次/分钟 | 同步接口无限制 |
| qwen-image-max-2025-12-30 | 2 次/分钟 | 同步接口无限制 |
| qwen-image-plus | 2 次/秒 | 同步接口无限制 / 异步接口 2 |
| qwen-image-plus-2026-01-09 | 2 次/秒 | 同步接口无限制 |
| qwen-image | 2 次/秒 | 同步接口无限制 / 异步接口 2 |
| 图像编辑 | qwen-image-edit-max | 2 次/分钟 | 同步接口无限制 |
| qwen-image-edit-max-2026-01-16 | 2 次/分钟 | 同步接口无限制 |
| qwen-image-edit-plus | 2 次/秒 | 同步接口无限制 |
| qwen-image-edit-plus-2025-12-15 | 2 次/秒 | 同步接口无限制 |
| qwen-image-edit-plus-2025-10-30 | 2 次/秒 | 同步接口无限制 |
| qwen-image-edit | 2 次/秒 | 同步接口无限制 |

### **文生图-Z-Image**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| z-image-turbo | 2 | 同步接口无限制 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| z-image-turbo | 2 | 同步接口无限制 |

### **万相**

中国内地

全球

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| 文生图 | wan2.6-t2i | 1 | 5 |
| wan2.5-t2i-preview | 5 |
| wan2.2-t2i-plus | 2 | 2 |
| wan2.2-t2i-flash |
| wanx2.1-t2i-plus |
| wanx2.1-t2i-turbo |
| wanx2.0-t2i-turbo |
| 图像生成 | wan2.6-image | 5 | 5 |
| 通用图像编辑 | wan2.5-i2i-preview | 5 | 5 |
| wanx2.1-imageedit | 2 | 2 |
| 文生图 | wanx-v1 | 2 | 1 |
| 图像局部重绘 | wanx-x-painting |
| 涂鸦作画 | wanx-sketch-to-image-lite |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| 文生图 | wan2.6-t2i | 5 | 5 |
| 图像生成 | wan2.6-image | 5 | 5 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| 文生图 | wan2.6-t2i | 5 | 5 |
| wan2.5-t2i-preview |
| wan2.2-t2i-flash | 2 | 2 |
| wan2.2-t2i-plus |
| wan2.1-t2i-turbo |
| wan2.1-t2i-plus |
| 图像生成 | wan2.6-image | 5 | 5 |
| 通用图像编辑 | wan2.5-i2i-preview | 5 | 5 |

### **图像编辑与生成**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| --- | --- |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| shoemodel-v1 | 2 | 1 |
| wanx-virtualmodel |
| wanx-style-repaint-v1 |
| wanx-poster-generation-v1 |
| virtualmodel-v2 |
| wanx-background-generation-v2 |
| image-instance-segmentation |
| image-erase-completion |
| image-out-painting | 2 | 5 |

### **人物写真生成-FaceChain**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| --- | --- |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| facechain-facedetect | 5 | 同步接口无限制 |
| facechain-finetune | 2 | 1 |
| facechain-generation |

### **创意文字生成-WordArt锦书**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| --- | --- |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| wordart-texture | 2 | 1 |
| wordart-semantic |

### **AI试衣-OutfitAnyone**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| --- | --- |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| aitryon | 10 | 5 |
| aitryon-plus | 10 | 5 |
| aitryon-parsing-v1 | 10 | 同步接口无限制 |
| aitryon-refiner | 10 | 5 |

## **图像生成-第三方模型**

### **StableDiffusion文生图模型**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| --- | --- |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| stable-diffusion-3.5-large | 2 | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |
| stable-diffusion-3.5-large-turbo |
| stable-diffusion-xl |
| stable-diffusion-v1.5 |

### **FLUX文生图模型**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| --- | --- |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **作业提交接口RPS限制** | **同时处理中任务数量** |
| flux-merged | 2 | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |
| flux-dev |
| flux-schnell |

## **语音合成（文本转语音）**

### **千问语音合成**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

千问3-TTS-Instruct-Flash

千问3-TTS-VD

千问3-TTS-VC

千问3-TTS-Flash

千问-TTS

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-instruct-flash | 180 |
| qwen3-tts-instruct-flash-2026-01-26 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vd-2026-01-26 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vc-2026-01-22 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-flash | 180 |
| qwen3-tts-flash-2025-11-27 | 180 |
| qwen3-tts-flash-2025-09-18 | 10 |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-tts | 10 | 100,000 |
| qwen-tts-latest |
| qwen-tts-2025-05-22 |
| qwen-tts-2025-04-10 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

千问3-TTS-Instruct-Flash

千问3-TTS-VD

千问3-TTS-VC

千问3-TTS-Flash

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-instruct-flash | 180 |
| qwen3-tts-instruct-flash-2026-01-26 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vd-2026-01-26 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vc-2026-01-22 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-flash | 180 |
| qwen3-tts-flash-2025-11-27 | 180 |
| qwen3-tts-flash-2025-09-18 | 10 |

### **千问实时语音合成**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

千问3-TTS-Instruct-Flash-Realtime

千问3-TTS-VD-Realtime

千问3-TTS-VC-Realtime

千问3-TTS-Flash-Realtime

千问-TTS-Realtime

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-instruct-flash-realtime | 180 |
| qwen3-tts-instruct-flash-realtime-2026-01-22 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vd-realtime-2026-01-15 | 180 |
| qwen3-tts-vd-realtime-2025-12-16 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vc-realtime-2026-01-15 | 180 |
| qwen3-tts-vc-realtime-2025-11-27 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-flash-realtime | 180 |
| qwen3-tts-flash-realtime-2025-11-27 | 180 |
| qwen3-tts-flash-realtime-2025-09-18 | 10 |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-tts-realtime | 10 | 100,000 |
| qwen-tts-realtime-latest |
| qwen-tts-realtime-2025-07-15 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

千问3-TTS-Instruct-Flash-Realtime

千问3-TTS-VD-Realtime

千问3-TTS-VC-Realtime

千问3-TTS-Flash-Realtime

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-instruct-flash-realtime | 180 |
| qwen3-tts-instruct-flash-realtime-2026-01-22 | 180 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vd-realtime-2026-01-15 | 180 |
| qwen3-tts-vd-realtime-2025-12-16 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-vc-realtime-2026-01-15 | 180 |
| qwen3-tts-vc-realtime-2025-11-27 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-tts-flash-realtime | 180 |
| qwen3-tts-flash-realtime-2025-11-27 | 180 |
| qwen3-tts-flash-realtime-2025-09-18 | 10 |

### **千问声音复刻**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen-voice-enrollment | 180 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen-voice-enrollment | 180 |

### **千问声音设计**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen-voice-design | 180 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen-voice-design | 180 |

### **CosyVoice语音合成**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

语音合成

声音复刻

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| cosyvoice-v3-plus | 3 |
| cosyvoice-v3-flash |
| cosyvoice-v2 |
| cosyvoice-v1 |

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| cosyvoice-v3-plus | 10<br>无论声音复刻功能是单独调用某一模型版本，还是同时调用多个模型版本，其总并发请求数均限制为 10 RPS。这意味着：<br>- 如果您仅调用 v2，则其最大并发请求为 10 RPS。<br>  <br>- 如果您同时调用 v2 和 v3，两者的请求总和不能超过 10 RPS（例如，v2 使用 7 RPS，则 v3 最多只能使用 3 RPS）。 |
| cosyvoice-v3-flash |
| cosyvoice-v2 |
| cosyvoice-v1 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

语音合成

声音复刻

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| cosyvoice-v3-plus | 3 |
| cosyvoice-v3-flash |

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| cosyvoice-v3-plus | 10<br>无论声音复刻功能是单独调用某一模型版本，还是同时调用多个模型版本，其总并发请求数均限制为 10 RPS。这意味着：<br>- 如果您仅调用 v2，则其最大并发请求为 10 RPS。<br>  <br>- 如果您同时调用 v2 和 v3，两者的请求总和不能超过 10 RPS（例如，v2 使用 7 RPS，则 v3 最多只能使用 3 RPS）。 |
| cosyvoice-v3-flash |

### **Sambert语音合成**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型服务** | **提交作业接口RPS限制** |
| --- | --- |

|     |     |
| --- | --- |
| **模型服务** | **提交作业接口RPS限制** |
| Sambert系列模型 | 20 |

## **语音识别（语音转文本）与翻译（语音转成指定语种的文本）**

### **千问3-LiveTranslate-Flash**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-livetranslate-flash | 100 | 100,000 |
| qwen3-livetranslate-flash-2025-12-01 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-livetranslate-flash | 100 | 100,000 |
| qwen3-livetranslate-flash-2025-12-01 |

### **千问3-LiveTranslate-Flash-Realtime**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-livetranslate-flash-realtime | 10 | 100,000 |
| qwen3-livetranslate-flash-realtime-2025-09-22 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-livetranslate-flash-realtime | 10 | 100,000 |
| qwen3-livetranslate-flash-realtime-2025-09-22 |

### **千问录音文件识别**

中国内地

国际

美国

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

千问3-ASR-Flash-Filetrans

千问3-ASR-Flash

千问ASR

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-asr-flash-filetrans | 100 |
| qwen3-asr-flash-filetrans-2025-11-17 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-asr-flash | 100 |
| qwen3-asr-flash-2025-09-08 |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-audio-asr | 60 | 100,000 |
| qwen-audio-asr-latest |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

千问3-ASR-Flash-Filetrans

千问3-ASR-Flash

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-asr-flash-filetrans | 100 |
| qwen3-asr-flash-filetrans-2025-11-17 |

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-asr-flash | 100 |
| qwen3-asr-flash-2025-09-08 |

在 [美国部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源仅限于美国境内。

|     |     |
| --- | --- |
| **模型名称** | **每分钟调用次数（RPM）** |
| qwen3-asr-flash-us | 100 |
| qwen3-asr-flash-2025-09-08-us |

### **千问实时语音识别**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |
| --- | --- |
| **模型名称** | **每秒钟调用次数（RPS）** |
| qwen3-asr-flash-realtime | 20 |
| qwen3-asr-flash-realtime-2026-02-10 |
| qwen3-asr-flash-realtime-2025-10-27 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |
| --- | --- |
| **模型名称** | **每秒钟调用次数（RPS）** |
| qwen3-asr-flash-realtime | 20 |
| qwen3-asr-flash-realtime-2026-02-10 |
| qwen3-asr-flash-realtime-2025-10-27 |

### **Gummy语音识别/翻译**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **提交作业接口RPS限制** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| gummy-realtime-v1 | 10 |
| gummy-chat-v1 |

### **Fun-ASR录音文件识别**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **提交作业接口RPS限制** | **任务查询接口RPS限制** |
| fun-asr | 10 | 20 |
| fun-asr-2025-11-07 |
| fun-asr-2025-08-25 |
| fun-asr-mtl |
| fun-asr-mtl-2025-08-25 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **提交作业接口RPS限制** | **任务查询接口RPS限制** |
| fun-asr | 10 | 20 |
| fun-asr-2025-11-07 |
| fun-asr-2025-08-25 |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **提交作业接口RPM限制** | **任务查询接口RPS限制** |
| fun-asr-mtl | 100 | 20 |
| fun-asr-mtl-2025-08-25 |

### **Fun-ASR实时语音识别**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| fun-asr-realtime | 20 |
| fun-asr-realtime-2025-11-07 |
| fun-asr-realtime-2025-09-15 |
| fun-asr-flash-8k-realtime |
| fun-asr-flash-8k-realtime-2026-01-28 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| fun-asr-realtime | 20 |
| fun-asr-realtime-2025-11-07 |

### **Paraformer语音识别**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **提交作业接口RPS限制** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **提交作业接口RPS限制** |
| paraformer-realtime-v2 | 20 |
| paraformer-realtime-v1 |
| paraformer-realtime-8k-v2 |
| paraformer-realtime-8k-v1 |

| **模型名称** | **提交作业接口RPS限制** | **任务查询接口RPS限制** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **提交作业接口RPS限制** | **任务查询接口RPS限制** |
| paraformer-v2 | 20 | 20 |
| paraformer-v1 | 10 |
| paraformer-8k-v2 | 20 |
| paraformer-8k-v1 | 10 |
| paraformer-mtl-v1 | 10 |

### **SenseVoice语音识别**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **提交作业接口RPS限制** | **任务查询接口RPS限制** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **提交作业接口RPS限制** | **任务查询接口RPS限制** |
| sensevoice-v1 | 10 | 20 |

## **视频生成**

### **万相系列**

中国内地

全球

国际

美国

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| 文生视频 | wan2.6-t2v | 5 | 5 |
| wan2.5-t2v-preview | 5 | 5 |
| wan2.2-t2v-plus | 2 | 2 |
| wanx2.1-t2v-turbo |
| wanx2.1-t2v-plus |
| 图生视频-基于首帧 | wan2.6-i2v-flash | 5 | 5 |
| wan2.6-i2v |
| wan2.5-i2v-preview |
| wan2.2-i2v-flash | 2 | 2 |
| wan2.2-i2v-plus |
| wanx2.1-i2v-turbo |
| wanx2.1-i2v-plus |
| 图生视频-基于首尾帧 | wan2.2-kf2v-flash |
| wanx2.1-kf2v-plus |
| 通用视频编辑 | wanx2.1-vace-plus |
| 参考生视频 | wan2.6-r2v-flash | 5 | 5 |
| wan2.6-r2v | 5 | 5 |
| 数字人s2v | wan2.2-s2v-detect | 5 | 同步接口无限制 |
| wan2.2-s2v | 1 |
| 图生动作 | wan2.2-animate-move | 5 | 1 |
| 视频换人 | wan2.2-animate-mix | 5 | 1 |

在 [全球部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源在全球范围内动态调度。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| 文生视频 | wan2.6-t2v | 5 | 5 |
| 图生视频-基于首帧 | wan2.6-i2v |
| 参考生视频 | wan2.6-r2v |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| 文生视频 | wan2.6-t2v | 5 | 5 |
| wan2.5-t2v-preview |
| wan2.2-t2v-plus | 2 | 2 |
| wan2.1-t2v-turbo |
| wan2.1-t2v-plus |
| 图生视频-基于首帧 | wan2.6-i2v-flash | 5 | 5 |
| wan2.6-i2v |
| wan2.5-i2v-preview |
| wan2.2-i2v-plus | 2 | 2 |
| wan2.1-i2v-turbo |
| wan2.1-i2v-plus |
| 图生视频-基于首尾帧 | wan2.1-kf2v-plus | 1 |
| 通用视频编辑 | wan2.1-vace-plus | 2 |
| 参考生视频 | wan2.6-r2v-flash | 5 | 5 |
| wan2.6-r2v | 5 | 5 |
| 图生动作 | wan2.2-animate-move | 5 | 1 |
| 视频换人 | wan2.2-animate-mix | 5 | 1 |

在 [美国部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **美国（弗吉尼亚）地域**，模型推理计算资源仅限于美国境内。

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量（并发数）** |
| 文生视频 | wan2.6-t2v-us | 5 | 5 |
| 图生视频-基于首帧 | wan2.6-i2v-us |

### **舞动人像AnimateAnyone**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| animate-anyone-detect-gen2 | 5 | 同步接口无限制 |
| animate-anyone-template-gen2 | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |
| animate-anyone-gen2 |
| animate-anyone-detect | 1算力单元支持2并发 |
| animate-anyone | 1算力单元支持1并发 |

### **悦动人像EMO**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| emo-detect-v1 | 5 | 同步接口无限制 |
| emo-v1 | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |

### **灵动人像LivePortrait**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| liveportrait-detect | 5 | 同步接口无限制 |
| liveportrait | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |

### **声动人像VideoRetalk**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| videoretalk | 1 | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |

### **表情包Emoji**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| emoji-detect-v1 | 1 | 同步接口无限制 |
| emoji-v1 | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |

### **视频风格重绘**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **任务下发接口RPS限制** | **同时处理中任务数量** |
| video-style-transform | 2 | 1<br>在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |

## **向量模型**

### **文本向量**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟调用次数（RPS）** | **每分钟消耗Token数（TPM）/作业数**<br>> **仅输入Token** |
| text-embedding-v1 | 30 | 1,200,000 |
| text-embedding-v2 |
| text-embedding-v3 |
| text-embedding-v4 |
| text-embedding-async-v1 | 1 | 当前用户在系统通用文本向量异步作业排队中和运行中的作业数量不超过50个。<br>另外，为了避免大量突发的作业占据太多资源，限制并发的作业数为3个，即任意时间，单个用户最多只有3个通用文本向量的异步作业在并发运行，其他的作业只能在队列中等待。 |
| text-embedding-async-v2 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）/作业数**<br>> **含输入与输出Token** |
| text-embedding-v3 | 6,000 | 24,000,000 |

### **多模态向量**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **仅输入Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **仅输入Token** |
| qwen3-vl-embedding | 1,200 | 600,000 |
| qwen2.5-vl-embedding |
| tongyi-embedding-vision-plus | 600 | 200,000 |
| tongyi-embedding-vision-flash | 600 |
| multimodal-embedding-v1 | 120 |

## **文本分类、抽取、排序**

### **OpenNLU**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| opennlu-v1 | 60 | 10,000 |

### **文本排序模型**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-rerank | 5,400 | 5,000,000,000 |
| gte-rerank-v2 | 5,040 | 4,980,000,000 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen3-rerank | 5,400 | 5,000,000,000 |
| gte-rerank-v2 | 5,040 | 4,980,000,000 |

## **行业**

### **通义法睿（法律模型）**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| farui-plus | 120 | 500,000 |

### **意图理解**

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| tongyi-intent-detect-v3 | 1,200 | 1,000,000 |

### **角色扮演**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-plus-character | 120 | 500,000 |
| qwen-flash-character |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| qwen-plus-character-ja | 120 | 500,000 |

### 界面交互

**说明**

仅支持[中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "")。接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| --- | --- |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **限流条件（超出任一数值时触发限流）**<br>> **以下为每分钟限流条件，服务可能按 RPS（RPM/60）与 TPS（TPM/60）限制** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| gui-plus | 80 | 540,000 |

## **已下线模型**

> 详细信息，请参见 [模型下线机制说明](https://help.aliyun.com/zh/model-studio/model-depreciation "")。

2026年1月30日下线

2025年7月30日下线

2025年7月2日下线

2025年5月8日下线

|     |     |     |     |
| --- | --- | --- | --- |
| **类别** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| 千问Max | qwen-max-2024-04-03 | 0 | 0 |
| 千问Plus | qwen-plus-2024-11-27 |
| qwen-plus-2024-11-25 |
| qwen-plus-2024-09-19 |
| qwen-plus-2024-08-06 |
| qwen-plus-2024-07-23 |
| 千问Turbo | qwen-turbo-2024-09-19 |
| qwen-turbo-2024-06-24 |
| 千问VL | qwen-vl-max-2024-10-30 |
| qwen-vl-max-2024-08-09 |
| qwen-vl-plus-2024-08-09 |
| 千问Audio | qwen-audio-turbo-2024-12-04 |
| qwen-audio-turbo-2024-08-07 |
| qwen-audio-asr-2024-12-04 |

|     |     |     |     |
| --- | --- | --- | --- |
| **类别** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| 千问VL | qwen-vl-plus-2023-12-01 | 0 | 0 |
| 零一万物 | yi-large |
| yi-medium |
| yi-large-rag |
| yi-large-turbo |
| Dolly | dolly-12b-v2 |

|     |     |     |     |
| --- | --- | --- | --- |
| **类别** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| Llama-仅文本输入 | llama3.3-70b-instruct | 0 | 0 |
| llama3.2-3b-instruct |
| llama3.2-1b-instruct |
| llama3.1-405b-instruct |
| llama3.1-70b-instruct |
| llama3.1-8b-instruct |
| llama3-70b-instruct |
| llama3-8b-instruct |
| llama2-13b-chat-v2 |
| llama2-7b-chat-v2 |
| Llama-文本和图像输入 | llama3.2-90b-vision-instruct |
| llama3.2-11b-vision |
| 百川-开源版 | baichuan2-13b-chat-v1 |
| baichuan2-7b-chat-v1 |
| baichuan-7b-v1 |
| ChatGLM | chatglm3-6b |
| chatglm-6b-v2 |
| 姜子牙 | ziya-llama-13b-v1 |
| BELLE | belle-llama-13b-2m-v1 |
| 元语 | chatyuan-large-v2 |
| BiLLa | billa-7b-sft-v1 |

|     |     |     |     |
| --- | --- | --- | --- |
| **类别** | **模型名称** | **限流条件（超出任一数值时触发限流）** |
| **每秒钟任务下发接口RPS限制** | **同时处理中任务数量** |
| 动漫人物生成 | wanx-style-cosplay-v1 | 0 | 0 |
| 图配文 | wanx-ast |
| 创意文字生成-WordArt锦书 | wordart-surnames |
| AnyText图文融合 | wanx-anytext-v1 |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **类别** | **模型名称** | **限流条件（超出任一数值时触发限流）** | **替代模型** |
| **每分钟调用次数（RPM）** | **每分钟消耗Token数（TPM）**<br>> **含输入与输出Token** |
| 文本生成-千问 | qwen-max-2024-01-07<br>（qwen-max-0107） | 0 | 0 | qwen-max |
| qwen-plus-2024-06-24<br>（qwen-plus-0624） | qwen-plus |
| qwen-plus-2024-02-06<br>（qwen-plus-0206） |
| qwen-turbo-2024-02-06<br>（qwen-turbo-0206） | qwen-turbo |
| qwen-vl-max-2024-02-01<br>（qwen-vl-max-0201） | qwen-vl-max |
| 文本生成-千问-开源版 | qwen-72b-chat | qwen2.5-72b-instruct |
| qwen-14b-chat | qwen2.5-14b-instruct |
| qwen-7b-chat | qwen2.5-7b-instruct |
| qwen-1.8b-chat | qwen2.5-1.5b-instruct |
| qwen-1.8b-longcontext-chat | qwen2.5-1.5b-instruct |
| qwen2-math-72b-instruct | qwen2.5-math-72b-instruct |
| qwen2-math-7b-instruct | qwen2.5-math-7b-instruct |
| qwen2-math-1.5b-instruct | qwen2.5-math-1.5b-instruct |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **类别** | **模型名称** | **限流条件（超出任一数值时触发限流）** | **替代模型** |
| **任务下发接口RPS限制** | **同时处理中任务数量** |
| 幻影人像Motionshop视频生成模型 | motionshop-video-detect | 0 | 0 | 使用animate-anyone-gen2的“按视频背景生成”功能，可达到近似效果 |
| motionshop-gen3d |
| motionshop-synthesis |