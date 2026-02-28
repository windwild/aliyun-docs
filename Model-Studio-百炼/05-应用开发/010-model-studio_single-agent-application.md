### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用开发](https://help.aliyun.com/zh/model-studio/llm-application/)智能体应用

# 智能体应用

更新时间：2026-02-12 02:59:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：新版智能体应用](https://help.aliyun.com/zh/model-studio/new-single-agent-application)[下一篇：工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

基本原理

快速开始

创建一个基础智能体

通过官方模板创建应用

智能体能力

模型

系统提示词（System Prompt）

知识库（RAG）

MCP

插件

复用智能体与工作流

记忆

智能体交互

文本对话

文本生成

语音和视频互动

个性化交互体验

智能体发布与调用

应用发布

通过 API 调用

发布为官方网页版

发布为钉钉机器人

发布为微信公众号

发布为组件

通过魔笔渠道分享应用

发布为百炼应用模板

智能体管理

删除与复制

版本管理

应用于生产环境

启动和备份多轮对话

内容安全与风控

应用合规备案

计费说明

支持的模型

常见问题

大语言模型（Large Language Model, LLM）无法直接访问专有知识库或获取实时动态信息。针对这一瓶颈，阿里云百炼提供了智能体（Agent）应用。智能体支持以零代码方式，将大模型与外部工具进行集成，从而扩展模型的能力边界。

## **基本原理**

智能体（Agent）由提示词（Prompt）驱动，通过协同多种外部能力来完成复杂任务。在接收请求后，大模型进行意图理解和任务规划，自主决策并调用一个或多个外部能力来执行任务，最终整合信息生成响应。

百炼智能体支持核心能力包括：

1. **知识库（RAG）**：通过连接外部知识库，使应用能基于私有数据回答问题，解决大模型无法访问特定信息的问题。

2. **插件**：能调用平台预置的效率工具（如代码执行、图像生成、天气查询等）。

3. **MCP**：允许将第三方服务封装并接入智能体，智能体可调用这些外部服务来完成特定工作。

4. **复用智能体与工作流：** 允许将其他智能体或工作流应用封装为模块化组件，实现复杂功能的复用。

5. **记忆**：使应用能够跨会话存储和回忆关键信息，实现个性化、连贯的对话体验。


## **快速开始**

### 创建一个基础智能体

1. 访问阿里云百炼控制台 [应用管理](https://bailian.console.aliyun.com/?tab=app#/app-center)，单击 **创建应用**，选择 **智能体应用**。

2. 配置 **应用名称**、 **描述信息**、 **应用头像**，点击 **立即创建**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009679.png)

3. 在应用管理界面，在模型选择器的下拉菜单中选择模型，例如`千问-Plus-Latest`.

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2529068571/p1010418.png)

4. 创建完成后，在右侧对话框中输入问题进行测试。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1005360.png)


### **通过官方模板创建应用**

访问阿里云百炼控制台 [应用管理](https://bailian.console.aliyun.com/?tab=app#/app-center)，选择 **智能体应用**。选择一个 **官方模板**，例如 **知识问答**，单击 **立即创建**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009694.png)

## 智能体能力

阿里云百炼智能体应用支持通过选择模型、优化系统提示词、添加 RAG、调用插件和MCP 服务、启用记忆以拓展能力。

### 模型

模型是驱动智能体进行思考、推理和决策的核心。百炼智能体支持选择千问系列、Deepseek 等官方模型，也支持选择自定义部署的模型。

1. **模型选择**

在应用配置界面，在右侧下拉菜单中选择一个模型，例如`千问-Plus-Latest`。单击 **更多模型** 可以选择 [支持的模型](https://help.aliyun.com/zh/model-studio/single-agent-application#93d5702b06zm1 "") 中的其他模型。

![截屏2025-09-23 14](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2529068571/p1010434.png)

2. **参数配置**

单击模型下拉框右侧的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1007468.png)，可以勾选、配置参数。模型参数会随模型选择动态变化，通常支持的参数如下：

1. **最长回复长度**：模型生成的长度限制，不包含提示词。允许的最大长度因模型不同有所改变。

2. **temperature**：控制生成随机性和多样性，数值越高多样性越强，数值越低一致性越强，取值范围为\[0, 2)。\
\
3. **enable\_thinking**：是否开启推理模式。部分不支持推理模式的模型无法配置 enable\_thinking 参数。\
\
\
      > 开启推理模式后，模型在生成回复时进行更多的内部推理和上下文处理，Token 消耗会增加。\
\
### 系统提示词（System Prompt）\
\
系统提示词是为智能体预设的元指令，用于定义其角色、行为准则与能力边界，以确保其在交互中始终保持一致性、可控性和任务合规性。\
\
> DeepSeek R1 系列模型不建议设置系统提示词。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009402.png)\
\
1. **配置提示词**\
\
配置系统提示词为`请你模仿《百年孤独》的风格来回答我的问题`，以下是效果对比：\
\
   - 无系统提示词：\
\
     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1008856.png)\
\
   - 配置系统提示词\
\
     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1008859.png)\
2. **在系统提示词中使用自定义变量（可选）**\
\
1. 输入`/`，单击 **新增变量**，配置自定义变量。\
\
      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1010013.png)\
\
      配置完成后，可以单击提示词框上方的 **自定义变量** 查看已配置的变量。\
\
2. 再次输入`/`，使用已配置的变量。\
\
### **知识库（RAG）**\
\
知识检索增强 (Retrieval-Augmented Generation, RAG) 能够使智能体查询外部知识库，并将检索到的最相关的信息作为生成答案的直接依据。在处理私有知识或垂直领域问答时，RAG 能显著提升智能体的回答准确率，减少幻觉问题。详情请参考 [知识库](https://help.aliyun.com/zh/model-studio/rag-knowledge-base "")。\
\
> RAG 检索到的文本也会占用大模型的上下文窗口长度（Context Window），因此需要根据实际情况调整检索策略和文本长度，以充分利用上下文窗口并避免超出限制。\
\
### **MCP**\
\
模型上下文协议（Model Context Protocol, MCP）是连接智能体与外部世界能力的关键桥梁，允许智能体调用外部工具。当智能体接收到无法仅凭自身知识完成的任务时（例如查询实时天气），它会调用 MCP 来执行这些任务。\
\
阿里云百炼提供了多种 [官方 MCP 服务](https://help.aliyun.com/zh/model-studio/official-and-third-party-mcp "")，同时也支持创建 [自定义MCP服务](https://help.aliyun.com/zh/model-studio/custom-mcp "")。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1010026.png)\
\
### **插件**\
\
智能体应用通过调用插件，可完成代码执行、网络搜索、基于文本生成图片等具体任务。阿里云百炼提供了多种官方插件，同时也支持添加自定义插件，详情参见 [插件概述](https://help.aliyun.com/zh/model-studio/plug-in-overview#0bbb546d962ms "")。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1008906.png)\
\
### **复用智能体与工作流**\
\
百炼智能体应用支持接入模块化的智能体或工作流组件，实现功能复用。\
\
> 接入前需要将智能体和工作流应用 [发布为组件](https://help.aliyun.com/zh/model-studio/use-agent-or-workflow-as-component "")。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1008909.png)\
\
### **记忆**\
\
智能体应用的记忆功能分为短期记忆和长期记忆。\
\
1. **短期记忆** 是会话中提供给智能体的上下文信息。轮数越多，对话相关性越强，输入长度也会增加。支持记忆的上下文轮数为 0 到 30（0 代表不传递多轮对话记录）。\
\
2. **长期记忆** 可以提取对话的关键信息并保存至对应的记忆体（Memory ID）中，详细的功能介绍请参考 [长期记忆](https://help.aliyun.com/zh/model-studio/long-term-memory "")。\
\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1008898.png)\
\
## **智能体交互**\
\
智能体应用支持多种交互方式，包括文本对话、文本生成、语音和视频互动。\
\
> 视频互动仅限千问 VL 系列模型。\
\
### **文本对话**\
\
文本对话是智能体应用的核心交互方式，能够提供智能和个性化的多轮对话体验。\
\
文本对话支持两种主要输入方式：\
\
1. **文本输入：** 输入文字与智能体进行对话。\
\
2. **文件上传：** 上传文件作为附件给到智能体，支持文档、图片、视频、音频等多种格式。详情请参考 [文件问答](https://help.aliyun.com/zh/model-studio/file-q-a "")。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1008968.png)\
\
\
### **文本生成**\
\
文本生成是面向单轮任务的生成式交互，适合对文章进行信息抽取与文本创作。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1008973.png)\
\
文本生成支持配置两种内置变量：\
\
1. **Prompt**：用户指令，用来指导应用生成回复。\
\
2. **Files & Images**：支持上传文档、图片、视频、音频等多种格式，自动识别类型并分类处理。\
\
3. **自定义变量**：传入变量值将替换提示词中对应的变量位置。\
\
\
### 语音和视频互动\
\
**重要**\
\
**计费模式**\
\
阿里云百炼与视频云分别产生应用调用的账单。\
\
1. 阿里云百炼按照应用API调用计费（如果TTS选择阿里云百炼CosyVoice，则模型调用也会计费），详情请参见 [大模型产品计费说明](https://help.aliyun.com/zh/model-studio/billing-for-model-studio#1d28825731abn "")。\
\
2. 视频云按照AI实时互动计费模式计费，AI实时互动每日为未订阅套餐包的用户赠送20通免费电话额度用于产品体验。详情请参见 [AI实时互动计费说明](https://help.aliyun.com/zh/document_detail/2850678.html "")。\
\
\
**说明**\
\
1. 不推荐使用深度思考模式的模型进行实时音视频对话，会影响对话体验，如DeepSeek-R1、QwQ系列模型\
\
2. DeepSeek V3 模型不支持视频对话功能。\
\
\
智能体应用支持语音和视频互动，可以与智能体进行实时语音和视频通话。\
\
1. **语音互动**：智能体能依托 [语音合成-CosyVoice](https://help.aliyun.com/zh/model-studio/text-to-speech "") 模型将文本回复转换为自然语音输出，从而进行实时的语音通话。\
\
2. **视频互动**：智能体能依托 [图像与视频理解](https://help.aliyun.com/zh/model-studio/vision "") 模型识别画面中的物体、场景、人物动作等，从而进行实时的视频通话。\
\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009000.png)\
\
### 个性化交互体验\
\
通过设置欢迎语、添加预设问题，进一步完善智能体应用体验。\
\
1. **欢迎语**：智能体的开场白，帮助营造友好积极的对话氛围。仅文本对话模式支持。\
\
2. **预设问题**：预设一系列启发性的问题，帮助快速了解智能体的核心能力。仅文本对话模式支持。\
\
3. **测试样例**：预置一组输入数据，配置完成后可快速发起测试。仅文本对话、文本生成模式支持。\
\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009006.png)\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009305.png)\
\
## 智能体发布与调用\
\
百炼智能体支持通过 API 外部调用，同时支持一键发布到三方平台，并通过组件或魔笔分享渠道集成到其他业务流程中。\
\
### 应用发布\
\
**重要**\
\
应用发布是后续所有智能体应用调用、集成的前提条件。\
\
单击智能体应用管理界面右上角的 **发布** 按钮，单击 **确认发布**，即可完成应用发布。\
\
> 若应用非首次发布，弹窗会展示自上次发布以来的变更详情。\
\
**说明**\
\
如果应用为 RAM 账号所创建，发布应用前请确认已拥有服务关联角色权限 `ram:CreateServiceLinkedRole`，详情请参考 [服务关联角色](https://help.aliyun.com/zh/model-studio/bailian-service-linked-role "")。\
\
### **通过 API 调用**\
\
您可以在智能体应用 **发布渠道** 页签，单击 **API调用** 右侧的 **查看API**，查看通过API调用智能体应用的方法。\
\
> 将DASHSCOPE\_API\_KEY替换为实际的百炼 API Key 才可发起调用。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1344728571/p911660.png)\
\
### 发布为官方网页版\
\
单击官方渠道右侧的 **生成分享链接**，可以分享给任意阿里云账号进行登录体验。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009050.png)\
\
### 发布为钉钉机器人\
\
集成智能体应用与钉钉机器人后，可在钉钉内访问和使用该应用。此集成需要在钉钉平台创建机器人，并将其与阿里云百炼应用关联。详细步骤，请参阅 [通过钉钉发布应用](https://help.aliyun.com/zh/model-studio/share-an-application#8778cb4490l2i "")。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3719962371/p877459.png)\
\
### 发布为微信公众号\
\
集成智能体应用与微信公众号后，可通过微信公众号访问和使用智能体应用。此集成需要创建微信公众号，并将其与阿里云百炼应用相关联。详细步骤，请参阅 [通过微信发布应用](https://help.aliyun.com/zh/model-studio/share-an-application#763832277bxo6 "")。\
\
在应用的 **发布渠道** 页签下，将鼠标悬停在 **微信公众号** 右侧的二维码图标上，即可显示公众号的二维码。用户可以通过微信扫一扫功能，扫描此二维码来关注您的公众号，进而访问已集成的阿里云百炼应用。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3719962371/p877474.png)\
\
### **发布为组件**\
\
将智能体应用发布为组件，以便于在其他智能体或工作流应用调用。详细的组件配置方法请参考 [发布为组件](https://help.aliyun.com/zh/model-studio/use-agent-or-workflow-as-component "")。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009362.png)\
\
### 通过魔笔渠道分享 **应用**\
\
将百炼智能体发布为生产级 Web/H5 应用，或嵌入已有的 Web/H5/App/小程序中。魔笔分享渠道功能现已迁移至 [UI设计](https://help.aliyun.com/zh/model-studio/ui-designer "")。\
\
### 发布为 **百炼应用模板**\
\
如有需要，您可以将您的应用上架为官网模板。请填写 [阿里云百炼应用模板上架申请](https://survey.aliyun.com/apps/zhiliao/dsv4Fcx_G)，我们的团队将与您取得联系。应用审核通过后，应用将会被上架至 [应用广场](https://bailian.console.aliyun.com/tab=app/app-market/app-template-experience/assistant/Legal-Document-Review-Analyser?tab=app#/app-market)。\
\
## **智能体管理**\
\
### 删除与复制\
\
可以在 **应用管理** 找到已发布的应用卡片，在**更多** \> **复制应用/删除应用**进行 **删除与复制智能体、修改应用名** 操作。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6338458571/p921163.png)\
\
### **版本管理**\
\
通过版本管理功能，可以编辑历史版本描述信息，或选择和使用发布过的历史版本。\
\
1. 在智能体应用的 **配置** 页签，单击顶部导航栏右侧的 **版本管理**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0031814471/p934802.png)\
\
2. 在历史版本列表中，选中目标版本后：![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1691413471/p934803.png)\
\
\
   - 如果需要修改版本信息，请将鼠标悬浮至![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1691413471/p934804.png)图标位置单击，在 **编辑版本描述** 对话框中按需完成修改后，单击 **确定**。\
\
   - 如果需要使用该历史版本，请单击 **覆盖当前草稿**，在二次确认对话框中单击 **确认**。\
\
\
     > 该历史版本内容将覆盖当前版本草稿内容。\
\
\
## **应用于生产环境**\
\
### **启动和备份多轮对话**\
\
百炼智能体应用默认开启多轮对话功能，通过内置缓存保存对话记录，有效期为 1 小时。对话记录也支持备份至 ADB-PG。在 **应用管理** 找到已发布的应用卡片，单击右下角![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009074.png)，单击 **高级配置**，选择多轮对话。\
\
> ADB-PG 的更多功能与计费信息，请参阅 [云原生数据仓库AnalyticDB PostgreSQL版](https://help.aliyun.com/zh/analyticdb/analyticdb-for-postgresql/product-overview/) 帮助文档。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3700879371/p914324.png)\
\
### 内容安全与风控\
\
发布应用后，可以在内置的安全规则基础上，自定义内容干预规则，确保大模型生成的内容安全可控。在 **应用管理** 找到已发布的应用卡片，单击右下角![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1166068571/p1009074.png)，单击 **高级配置**。\
\
1. **使用快速干预工具**\
\
使用 **快速干预工具**，可以及时拦截和处理对话中存在潜在的违规、敏感或不当内容。该工具基于自定义的规则，检测用户输入或模型生成的文本，一旦触发条件就会执行预先设置的干预操作，以此保证智能体应用在与用户交互时保持合规与安全，满足平台审核要求，提供更健康的对话体验。\
\
\
> 快速干预工具仅通过规则方式快速处理用户输入的违规话术或者大模型生成的风险内容，该工具无法替代内容安全检测类的专业产品。\
\
\
1. **创建输入话术规则**\
\
\
\
\
\
\
      - 在 **干预输入话术** 面板点击 **创建输入话术规则**，并为规则命名。\
\
      - 通过支持正则表达式的检测方式，将需要识别的违规关键词或短语添加到条件里。您可以设置单独的 AND / OR 逻辑条件组合，使规则匹配更灵活多样。\
\
      - 在 **触发条件时的回复** 中输入当用户触发风险内容时，系统需要返回的警示或替代文本。这样一来，违规内容就会被拦截并给予提示性的响应。\
\
\
2. **创建生成结果规则**\
\
\
\
\
\
\
      - 若想对模型在回复时可能出现的风险内容进行控制，则可以在 **干预生成结果** 面板添加相应规则。\
\
      - 规则以正则匹配为基础，结合多条件的 AND / OR 逻辑来判定文本风险。\
\
      - 在 **触发条件时的回复** 中配置好干预后需要返回的安全文本，或者是让系统拒绝输出某些不合规的语言。\
2. **配置内容安全策略**\
\
智能体应用内置了一套内容安全策略，当大模型生成的内容触发此策略时，智能体应用将拦截全部生成内容，并提示内容存在安全问题。\
\
目前，阿里云百炼仅提供“全部拦截”的风险内容拦截方式，您无需手动配置此项。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3700879371/p914342.png)\
\
\
### 应用合规备案\
\
若应用对外提供服务，必须遵守国家网信办《生成式人工智能服务管理暂行办法》等法规，完成必要的 [应用合规备案](https://help.aliyun.com/zh/model-studio/compliance-and-launch-filing-guide-for-ai-apps-powered-by-the-tongyi-model "")。\
\
## 计费说明\
\
智能体功能计费主要体现在以下几个方面：\
\
1. **模型调用**\
\
智能体会产生模型调用费用，具体费用取决于模型类型、输入和输出 Token 数量。\
\
具体的模型类型和对应的计费规则请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。\
\
2. **知识库**\
\
   - 知识库采取按量付费，详情请参见 [知识库计费说明](https://help.aliyun.com/zh/model-studio/billing-for-knowledge-base "")。\
\
   - 从知识库召回的文本切片会增加模型输入 Token 数量，可能导致模型推理（调用）费用的增加。\
3. **MCP**\
\
   - 部分官方 MCP 按模型调用计费，如文生图、文生视频、语音合成等 MCP。\
\
   - 部分 MCP 服务涉及第三方 API 调用，使用后可能会产生费用。这部分费用由第三方收取，阿里云百炼不收取费用。\
4. **长期记忆**\
\
   - 长期记忆的数据存储不收费。\
\
   - 在调用应用进行问答时，记忆体内容会合并到 Prompt 传递给大模型，从而增加 Token 消耗。 **被记忆体内容占用的Token暂不计费。**\
\
## **支持的模型**\
\
**说明**\
\
数据更新可能存在延迟，模型的支持情况以智能体应用内显示为准。\
\
- [千问-Plus](https://help.aliyun.com/zh/model-studio/models#03a05ab98953u "")\
\
- [千问-Max](https://help.aliyun.com/zh/model-studio/models#b00bc62972qtn "")\
\
- [千问3-Coder-Plus](https://help.aliyun.com/zh/model-studio/models#8e453767fbkka "")\
\
- [千问3开源模型](https://help.aliyun.com/zh/model-studio/models#42ee525d93ke0 "")\
\
- [千问VL-Max](https://help.aliyun.com/zh/model-studio/models#88a4ba679cay7 "")\
\
- [千问VL-Plus](https://help.aliyun.com/zh/model-studio/models#4dfc2e52fams1 "")\
\
- [千问-QwQ-Plus](https://help.aliyun.com/zh/model-studio/models#5b345b2e75d35 "")\
\
- [DeepSeek](https://help.aliyun.com/zh/model-studio/models#21ab4c25c7lml "")\
\
- [千问2.5开源模型](https://help.aliyun.com/zh/model-studio/models#e4831f1e9388j "")\
\
- [千问-Turbo](https://help.aliyun.com/zh/model-studio/models#218847c4b35vb "")\
\
- [千问-QwQ](https://help.aliyun.com/zh/model-studio/models#ff99b03558zo4 "")\
\
- [千问2开源模型](https://help.aliyun.com/zh/model-studio/models#5d2908c05460t "")\
\
- [Qwen-Long](https://help.aliyun.com/zh/model-studio/models#27b2b3a15d5c6 "")\
\
\
## **常见问题**\
\
百炼应用如何计费？\
\
只创建应用不会收费。但如果调用应用进行了问答，则会根据调用的模型类型收取模型调用费用。\
\
配置了知识库，但智能体的回答和知识库内容不相关，该如何解决？\
\
1. 首先进行知识库命中测试，查看问题与知识库内容的相似度得分。如果得分较低，请尝试优化检索配置，确保模型优先从知识库中获取答案。\
\
2. 在提示词技能设置中添加限制，要求模型仅基于知识库内容回答，避免使用大模型自有知识生成回复。\
\
3. 如果问题仍然存在，可能是模型本身的特性导致，建议尝试更换其他模型以获得更稳定的输出。\
\
\
自定义插件是否有超时限制？\
\
是，超时限制时间为 5 秒。\
\
是否支持通过 API 创建智能体应用？\
\
支持使用 Assistant API 创建大模型应用，其功能和智能体应用类似。但 Assistant API 创建的应用 **不支持控制台管理**，详细信息请参阅 [Assistant API 文档](https://help.aliyun.com/zh/model-studio/assistant-api/ "")。