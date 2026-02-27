### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[模型服务 FunModel](https://help.aliyun.com/zh/functioncompute/fc/funmodel/)什么是FunModel

# 什么是FunModel

更新时间：2025-12-08 01:40:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：基于AgentRun构建舆情分析专家](https://help.aliyun.com/zh/functioncompute/fc/construction-of-public-opinion-analysis-assistant-based-on-agenrun)[下一篇：授权RAM用户使用FunModel](https://help.aliyun.com/zh/functioncompute/fc/authorize-ram-users-to-use-funmodel)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

核心能力与实现原理

异构算力虚拟化

负载感知调度与弹性伸缩

集成开发工具链：加速模型迭代与部署

技术优势

快速开始

FunModel 是一个面向 AI 模型开发、部署与运维的全生命周期管理平台。您只需提供模型文件（例如来自 ModelScope、Hugging Face 等社区的模型仓库），即可利用 FunModel 的自动化工具快速完成模型服务的封装与部署，并获得可直接调用的推理 API。平台在设计上旨在提升资源使用效率并简化开发部署流程。

## **核心能力与实现原理**

1. ### **异构算力虚拟化**


FunModel 采用异构算力虚拟化技术，对数据中心内的 CPU、GPU 等计算资源进行统一管理和调度。其核心机制包括：


   - GPU 切分技术：将单张物理 GPU 显卡虚拟化为多个独立的计算单元，支持多个不同大小的模型或实例共享同一张卡，同时保证资源隔离。

   - 资源池化管理：统一纳管数据中心内的 CPU、GPU 等异构算力，形成统一的资源池，根据实际负载动态调度和分配资源。


此架构旨在提高 GPU 等计算资源的整体利用率，从而帮助用户优化算力成本。

2. ### 负载感知调度与弹性伸缩


为应对 AI 推理服务中常见的流量波动，FunModel 设计了一套调度与实例恢复机制，以确保服务的响应速度和稳定性。

   - 三级响应机制：


     - 活跃实例优先：请求优先路由至已激活的实例，实现最低延迟。

     - 浅休眠（原闲置）实例唤醒：当活跃实例不足时，通过快照技术唤醒处于“冻结”状态的浅休眠（原闲置）实例。

     - 冷启动兜底：在无任何可用实例时，执行冷启动创建全新实例。
   - 快照与状态恢复：FunModel使用快照技术将实例的完整状态（包括 GPU 显存）冻结并存储。当需要唤醒时，系统可通过加载快照在秒级别恢复实例状态，极大缩短了实例从创建到就绪的等待时间。

   - 秒级弹性扩容：结合资源池与快照恢复技术，FunModel能够在数秒内完成新实例的调度和启动，以应对突发的流量高峰。

   - 弹性计费：为平衡成本与响应速度，处于“冻结”状态的浅休眠（原闲置）实例，其计算资源将按较低的标准进行计费，详情可参见： [计费概述](https://help.aliyun.com/zh/functioncompute/fc/product-overview/billing-overview-of-fc "")。
3. ### 集成开发工具链：加速模型迭代与部署


FunModel 提供了一系列自动化工具，旨在将开发者的工作重心聚焦于模型开发本身，而非繁琐的部署和运维任务。

   - DevPod 一体化开发环境：提供预置了常用 AI 框架和库的云端开发环境。开发者可通过网页版 `VSCode`、`JupyterLab` 或 `SSH 终端` 直接进行编码与调试，无需在本地配置复杂的开发环境。

   - 一键构建与部署：当开发者在 DevPod 中完成模型开发和本地测试后，可通过平台提供的工具一键触发镜像的构建、推送至镜像仓库，并自动部署到目标环境。整个从代码完成到服务上线的过程清晰、高效，显著缩短了迭代周期。

   - 内置加速框架：平台集成了 vLLM和SGLang等业界主流的推理加速框架。开发者可以在部署时选择启用，通常无需修改代码即可利用这些框架来提升模型的推理性能。

## **技术优势**

| **特性** | **FunModel 实现机制** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **特性** | **FunModel 实现机制** | **说明** |
| 资源利用率 | 采用 GPU 虚拟化与资源池化技术。 | 该设计允许多个任务共享底层硬件资源，旨在提高计算资源的整体使用效率。 |
| 实例就绪时间 | 基于快照技术的状态恢复机制。 | 实例启动时，可通过快照在毫秒级别恢复运行状态，从而将实例从创建到就绪的时间控制在秒级。 |
| 弹性扩容响应 | 结合预热资源池与快速实例恢复能力。 | 当负载增加时，系统可以从预热资源池中快速调度并启动新实例，实现秒级的水平扩展响应。 |
| 自动化部署耗时 | 提供可一键触发的构建与部署流程。 | 一次标准的部署流程（从代码提交到服务上线）通常可在10分钟内完成。 |

## **快速开始**

1. 部署您的第一个模型服务— [快速入门](https://help.aliyun.com/zh/functioncompute/fc/quick-start "")

2. 高级部署方案— [自定义模型部署](https://help.aliyun.com/zh/functioncompute/fc/custom-model-deployment "")

3. 云端AI开发环境— [DevPod开发环境](https://help.aliyun.com/zh/functioncompute/fc/devpod-development-environment "")

4. [DeepSeek-OCR快速开始指南](https://help.aliyun.com/zh/functioncompute/fc/deepseek-ocr-quick-deployment-guide "")