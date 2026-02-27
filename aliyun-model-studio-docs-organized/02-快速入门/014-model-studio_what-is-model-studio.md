### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[开始使用](https://help.aliyun.com/zh/model-studio/get-started-with-models/)产品简介

# 什么是阿里云百炼

更新时间：2026-02-16 02:33:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[下一篇：首次调用千问API](https://help.aliyun.com/zh/model-studio/first-api-call-to-qwen)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型服务

开箱即用的模型

模型调优、部署和评测

应用构建

产品计费

新用户免费额度

如何支付费用

查看账单与用量

开始使用阿里云百炼

常见问题

Q：我的数据安全吗？阿里云百炼会用我的数据进行训练吗？

Q：中国内地（北京）、美国（弗吉尼亚）和国际（新加坡）地域有什么区别？

Q：如何避免自动扣费？

Q：如何使用Qwen3系列模型或DeepSeek？

阿里云百炼是一站式大模型开发与应用平台，集成了千问及主流第三方模型。它为开发者提供了兼容OpenAI的API及全链路模型服务；同时，也提供可视化应用构建能力，让业务人员能快速创建智能体、知识库问答等AI应用。

借助阿里云百炼，您可以：

|     |     |     |
| --- | --- | --- |
| ![api](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710872271/p824099.png) 调用API<br>只需如下几行代码，即可与大模型进行对话，实现内容创作、摘要生成等。<br>> 阿里云百炼兼容OpenAI接口规范，您只需调整 API Key、base\_url 和模型名称，即可将原有 OpenAI 代码迁移至阿里云百炼。<br>Python<br>Node.js<br>curl<br>```python<br>import os<br>from openai import OpenAI<br># 注意: 不同地域的base_url不通用（下方示例使用北京地域的 base_url）<br># - 华北2（北京）: https://dashscope.aliyuncs.com/compatible-mode/v1<br># - 新加坡: https://dashscope-intl.aliyuncs.com/compatible-mode/v1<br>client = OpenAI(<br>    api_key=os.getenv("DASHSCOPE_API_KEY"),<br>    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",<br>)<br>completion = client.chat.completions.create(<br>    model="qwen3.5-plus",<br>    messages=[{'role': 'user', 'content': '你是谁？'}]<br>)<br>print(completion.choices[0].message.content)<br>```<br>```nodejs<br>import OpenAI from "openai";<br>// 注意: 不同地域的base_url不通用（下方示例使用北京地域的base_url）<br>// - 华北2（北京）: https://dashscope.aliyuncs.com/compatible-mode/v1<br>// - 新加坡: https://dashscope-intl.aliyuncs.com/compatible-mode/v1<br>const openai = new OpenAI(<br>    {<br>        apiKey: process.env.DASHSCOPE_API_KEY,<br>        baseURL: "https://dashscope.aliyuncs.com/compatible-mode/v1",<br>    }<br>);<br>async function main() {<br>    const completion = await openai.chat.completions.create({<br>        model: "qwen3.5-plus",<br>        messages: [{ role: "user", content: "你是谁？"}],<br>    });<br>    console.log(completion.choices[0].message.content)<br>}<br>main()<br>```<br>不同地域的 Base URL 不通用（以下示例是北京地域 Base URL）<br>- 华北2（北京）： `https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions`<br>  <br>- 新加坡： `https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions`<br>  <br>```curl<br>curl -X POST https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions \<br>-H "Authorization: Bearer $DASHSCOPE_API_KEY" \<br>-H "Content-Type: application/json" \<br>-d '{<br>    "model": "qwen3.5-plus",<br>    "messages": [<br>        {<br>            "role": "user",<br>            "content": "你是谁？"<br>        }<br>    ]<br>}'<br>``` |
| ![robot](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710872271/p824100.png)[构建智能客服](https://help.aliyun.com/zh/model-studio/single-agent-application "")<br>可视化的应用构建，让您可以快速构建一个AI助手来应对客户咨询。<br>![客服3](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710872271/p823451.gif) | ![process](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710872271/p824091.png)[编排流程](https://help.aliyun.com/zh/model-studio/workflow-application/ "")<br>可视化的流程编排，让无代码基础的业务人员也能进行流程设计。<br>![流程_4](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710872271/p824085.png) | ![tune_8](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710872271/p824102.png)[微调模型](https://help.aliyun.com/zh/model-studio/model-training-overview "")<br>可视化的微调功能，即使不熟悉微调的工程代码，也能完成模型定制。<br>![loss_3](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710872271/p824086.png) |

## **模型服务**

### 开箱即用的模型

阿里云百炼平台提供开箱即用的模型服务，无需自行部署或运维，即可直接调用自研千问（Qwen）全系列模型，以及[DeepSeek](https://help.aliyun.com/zh/model-studio/minimax-llm-api "")、 [Kimi](https://help.aliyun.com/zh/model-studio/models#2363cbf60fe6m "")、 [GLM](https://help.aliyun.com/zh/model-studio/models#059d6a5d1chfp "")等第三方大模型。详情请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

- **千问（Qwen）系列旗舰模型**：

  - [千问Max](https://help.aliyun.com/zh/model-studio/models#d4ccf72f23jh9 "") ：Qwen3系列效果最好的模型，适合处理复杂、多步骤任务。

  - [千问Plus](https://help.aliyun.com/zh/model-studio/models#5ef284d4ed42p "")：在效果、速度和成本上表现均衡，是多数场景的 **推荐选择**。


    > 最新的Qwen3.5-Plus系列在语言理解、逻辑推理、代码生成、智能体任务、图像理解、视频理解等多种任务中表现突出，推荐选用。

  - [千问Flash](https://help.aliyun.com/zh/model-studio/models#13ff05e329blt "") ：高性价比、低延迟，适合需要快速响应的简单任务。

  - [千问Coder](https://help.aliyun.com/zh/model-studio/models#d698550551bob "")：擅长工具调用和环境交互，专用于代码生成与理解。
- **多模态覆盖**：涵盖 [文本生成](https://help.aliyun.com/zh/model-studio/models#9f8890ce29g5u "")、 [视觉理解](https://help.aliyun.com/zh/model-studio/models#3f1f1c8913fvo "")、 [图像生成](https://help.aliyun.com/zh/model-studio/models#4611ffaa38hnp "")、 [视频生成](https://help.aliyun.com/zh/model-studio/models#43aa6e41fd25m "")、 [语音识别](https://help.aliyun.com/zh/model-studio/models#8017a37ad5a66 "") 与 [合成](https://help.aliyun.com/zh/model-studio/models#b9e5744149hd6 "")、 [嵌入向量](https://help.aliyun.com/zh/model-studio/models#3383780daf8hw "") 等多种能力。

- **细分领域模型**：针对特定行业和任务，提供 [长文本处理](https://help.aliyun.com/zh/model-studio/models#27b2b3a15d5c6 "")、 [翻译](https://help.aliyun.com/zh/model-studio/models#b51e22f4b036h "")、 [数据挖掘](https://help.aliyun.com/zh/model-studio/models#531dbf3f1addx "")、 [法律](https://help.aliyun.com/zh/model-studio/models#f0436273ef1xm "")、 [意图理解](https://help.aliyun.com/zh/model-studio/models#85209145a5r68 "")、 [角色扮演](https://help.aliyun.com/zh/model-studio/models#083f31bde1lv3 "")、 [深入研究](https://help.aliyun.com/zh/model-studio/models#af665c3673n6e "") 等多种领域模型。


### 模型调优、部署和评测

- [模型调优](https://help.aliyun.com/zh/model-studio/model-training-overview "")：支持有监督微调（SFT）、继续预训练（CPT）和直接偏好优化（DPO）调优训练方法，以满足特定业务需求。

- [模型部署](https://help.aliyun.com/zh/model-studio/model-deployment-introduction "")：支持将预置模型或调优后的自定义模型部署为资源专享的推理服务，以满足对高并发、低延迟等不同性能的业务需求。提供按时长、包月、按Token量等多种计费方式。

- [模型评测](https://help.aliyun.com/zh/model-studio/model-evaluation-overview "")：提供包括人工评测、自动评测和基线评测在内的评测体系，支持快速对比不同模型的表现，检验模型调优效果，并预先发现潜在调用风险。


## **应用构建**

- **应用类型：** 提供可视化与高代码两种应用开发模式，以满足不同开发者的需求。通过可视化方式可快速创建 [智能体应用](https://help.aliyun.com/zh/model-studio/single-agent-application "") 与 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "")，而 [高代码应用](https://help.aliyun.com/zh/model-studio/high-code-application "") 则支持将Python项目部署为后端服务，支持自动化运维、可观测、日志服务等能力。

- **功能拓展**：支持通过 [知识库（RAG）](https://help.aliyun.com/zh/model-studio/rag-knowledge-base "") 连接私有数据和专业领域知识，通过 [插件](https://help.aliyun.com/zh/model-studio/plug-in-overview "") 和 [模型上下文协议（MCP）](https://help.aliyun.com/zh/model-studio/mcp-introduction "") 调用外部服务，实现了灵活、个性化的功能拓展。

- **分享与发布**：支持将应用以多种方式分享或发布至不同平台，包括网页应用、钉钉机器人、微信公众号以及音视频互动智能体等，将 AI 能力集成到具体业务中，详见 [应用分享](https://help.aliyun.com/zh/model-studio/share-an-application "")。


## **产品计费**

开通阿里云百炼并不会产生费用，调用、微调、部署模型会产生相应费用，详情请参见 [计费项](https://help.aliyun.com/zh/model-studio/billing-for-model-studio "") 和 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

### **新用户免费额度**

阿里云百炼为新用户提供北京地域专属的新人免费额度，用于体验模型调用。额度用完后将转为按量付费。为避免意外扣费，您可开启 [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 功能，服务将在额度耗尽时自动停止，详见 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。

### **如何支付费用**

调用模型会自动扣费（按小时出账），请确保您的阿里云账户余额充足，可通过 [费用与成本](https://usercenter2.aliyun.com/home) 页面进行充值。

### **查看账单与用量**

- **消费明细：** 访问[账单详情](https://usercenter2.aliyun.com/finance/expense-report/expense-detail)和[成本分析](https://usercenter2.aliyun.com/expense-manage/expense-analyze)页面。

- **调用统计**：模型调用完约 **一小时后**，在[模型监控（北京）](https://bailian.console.aliyun.com/?tab=model#/model-telemetry)、 [模型监控（弗吉尼亚）](https://modelstudio.console.aliyun.com/us-east-1?tab=dashboard#/model-telemetry)、 [模型监控（新加坡）](https://modelstudio.console.aliyun.com/?spm=a2c4g.11186623.0.0.39086143l397a1&tab=model#/model-telemetry)页面设置查询条件，点击目标模型 **操作** 列的 **监控**，即可查看该模型的调用量、Token消耗、成功率等统计结果。详情请参见 [模型监控](https://help.aliyun.com/zh/model-studio/model-telemetry/ "")。


## **开始使用阿里云百炼**

- 在线体验大模型：[模型体验](https://bailian.console.aliyun.com/?tab=model#/efm/model_experience_center/text)

- 发起第一个API请求： [首次调用千问API](https://help.aliyun.com/zh/model-studio/first-api-call-to-qwen "")

- 构建第一个大模型应用： [0代码构建问答应用](https://help.aliyun.com/zh/model-studio/build-knowledge-base-qa-assistant-without-coding/ "")


## 常见问题

### **Q：我的数据安全吗？阿里云百炼会用我的数据进行训练吗？**

A：阿里云严格保护数据隐私，绝不会将您的数据用于模型训练。同时，您在构建应用或训练大模型过程中传输的数据都会经过加密，以确保数据安全。详情请参见 [隐私说明](https://help.aliyun.com/zh/model-studio/privacy-notice "")。

### Q：中国内地（ **北京）、美国（弗吉尼亚）和国际（新加坡）** **地域有什么区别？**

A：阿里云百炼提供中国内地（ [**北京**](https://bailian.console.aliyun.com/?tab=model#/model-market)）、美国 **（** [**弗吉尼亚**](https://modelstudio.console.aliyun.com/us-east-1) **）** 和国际（ [**新加坡**](https://modelstudio.console.aliyun.com/?tab=doc#/doc/?type=model&url=2840914)）地域的模型服务，选择邻近地域调用可降低网络延迟。不同地域的服务接入点（Endpoint/Base URL）不同，且API Key不通用，支持的模型、平台功能及价格也有所不同，详情请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

### **Q：如何避免自动扣费？**

A：阿里云百炼采用按量付费模式，本身 **不提供"自动扣费"开关**。为避免产生费用，您可采取以下措施：

- **删除已创建的 API Key**

进入[**API-KEY（北京）**](https://bailian.console.aliyun.com/?apiKey=1&tab=globalset#/efm/api_key)、 [**API-KEY（弗吉尼亚）**](https://modelstudio.console.aliyun.com/us-east-1?tab=dashboard#/api-key) 或 [**API-KEY（新加坡）**](https://modelstudio.console.aliyun.com/?tab=globalset#/efm/api_key)页面，删除所有 API Key。删除后将无法通过 API 调用百炼模型，从而彻底阻断费用产生。

- **停止所有模型调用行为**


  - 停止应用程序中的模型调用

  - 停止智能体和工作流等应用的调用

  - 排查并停止定时任务或后台进程


> 费用由实际调用触发，确保所有调用行为都已停止。

- **清理计费资源**

  - **知识库**：删除不再使用的知识库。

  - **已部署模型**：访问 [模型部署](https://bailian.console.aliyun.com/?tab=model#/efm/model_deploy) 页面，对于按算力时长计费的部署必须 **下线** 实例；按调用量计费的部署，停止调用或删除 API Key 即可。
- **开启“** [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") **”功能（仅限新用户）**

在支持该功能的模型详情页开启此开关。当免费额度耗尽时，服务会自动停止（返回错误码 AllocationQuota.FreeTierOnly），避免转为付费。


> 注意：该功能仅适用于中国大陆版（北京）模型，且在免费额度有效期内。

- **设置费用监控和预警**

  - 查看[**账单详情**](https://usercenter2.aliyun.com/finance/expense-report/expense-detail)

  - 访问[**模型监控（北京）**](https://bailian.console.aliyun.com/?tab=model#/model-telemetry)、 [**模型监控（弗吉尼亚）**](https://modelstudio.console.aliyun.com/us-east-1?tab=dashboard#/model-telemetry) 或 [**模型监控（新加坡）**](https://modelstudio.console.aliyun.com/?tab=model#/model-telemetry)查看调用统计（调用后约1小时更新）

  - 设置 [**高额消费预警**](https://usercenter2.aliyun.com/home/alarm-threshold)：当指定产品的日账单超过阈值时，系统每日短信提醒一次，便于及时干预

通过以上措施，您可以有效控制阿里云百炼的使用费用。

### **Q：如何使用Qwen3系列模型或DeepSeek？**

A：

1. **在线体验**：请访问[**模型广场（北京）**](https://bailian.console.aliyun.com/?tab=model#/model-market)、 [**模型广场（弗吉尼亚）**](https://modelstudio.console.aliyun.com/us-east-1?tab=doc#/doc/?type=model&url=2840914) 或 [**模型广场（新加坡）**](https://modelstudio.console.aliyun.com/?tab=doc#/doc/?type=model&url=2840914)页面，点击模型进行体验（DeepSeek仅支持北京地域）。

2. **通过API调用模型**：调用流程请参见 [首次调用千问API](https://help.aliyun.com/zh/model-studio/first-api-call-to-qwen "")，支持的模型见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

3. **通过开发工具（如Claude Code）调用模型**：请参考 [接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/ "")。

4. **通过可视化界面构建大模型应用**：请参考 [智能体应用](https://help.aliyun.com/zh/model-studio/single-agent-application "") 或 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "")。