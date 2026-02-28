### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)Cherry Studio

# Cherry Studio

更新时间：2026-02-11 01:59:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Chatbox](https://help.aliyun.com/zh/model-studio/chatbox)[下一篇：Claude Code](https://help.aliyun.com/zh/model-studio/claude-code)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

效果展示

如何使用

前提条件

应用场景

常见问题

Q：Qwen3 模型为何报错 The value of the enable\_thinking parameter is restricted to True？

Q：为什么有免费额度但产生了费用？

Cherry Studio 是主流的大模型桌面客户端。它支持大模型 API 与 MCP 服务器集成，也可连接 Embedding API 实现本地知识库问答。

## **效果展示**

以导入 [限流](https://help.aliyun.com/zh/model-studio/rate-limit "") 文档，集成网页抓取 MCP 工具，探索限流报错的解决方案为例：

![cherry-studio-mcp (online-video-cutter](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997274.gif)

> 原始动图较长，此处进行加速处理。

## **如何使用**

### **前提条件**

1. **安装 Cherry Studio**

前往 [下载界面](https://www.cherry-ai.com/download)，根据系统类型下载安装包；

2. **获取 API 密钥**

您需要 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，并开通阿里云百炼的模型服务；

3. **配置模型**

单击右上角的设置按钮，在 **模型服务** 栏中找到 **阿里云百炼**，在 **API 密钥** 输入您的 API Key；在 **API 地址** 输入对应地域的base\_url；单击 **添加**。


   - **北京地域**：`https://dashscope.aliyuncs.com/compatible-mode/v1`

   - **新加坡地域**：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`

   - **弗吉尼亚地域** **：**`https://dashscope-us.aliyuncs.com/compatible-mode/v1`


![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3274214671/p920483.png)

在 **模型 ID** 填入您需要使用的模型，此处以 `qwen-plus-latest`为例。

> 如需选择其它模型，请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")，模型的支持情况以实际效果为准。

> 如果您是 RAM 用户，请参见 [业务空间管理](https://help.aliyun.com/zh/model-studio/use-workspace "")，确保拥有模型的调用权限。

### **应用场景**

本文通过简单对话、MCP与本地知识库问答三个场景，介绍如何将阿里云百炼的模型与 MCP 服务集成到 Cherry Studio。

简单对话

调用 MCP 工具

查询本地知识库

单击对话按钮，在输入框中输入“你是谁”，`qwen-plus-latest` 模型会在思考后进行回答。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997047.png)

`qwen-plus-latest` 为混合思考模型，可通过输入框的![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997049.png)按钮控制是否开启思考模式。

Cherry Studio 是先进的 MCP 客户端，可通过界面化操作为模型提供工具参考信息。

### **1\. 获取 MCP 工具**

以接入 ModelScope 提供的[Fetch 网页抓取](https://www.modelscope.cn/mcp/servers/@modelcontextprotocol/fetch)MCP 服务器为例。通过右侧的**服务配置信息**，获取专属URL。

![c-3-zh](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6168414671/p1029545.jpg)

### **2\. 添加 MCP 服务器**

单击 Cherry Studio 右上角的设置按钮，单击 **MCP**，在新页面中单击 **添加-从 JSON 导入**，粘贴上图**服务配置信息**中的 JSON 配置信息。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6169214671/p997234.png)

上图为添加 MCP 服务器成功状态。

### **3\. 提问**

回到对话框，单击 MCP 服务器的图标![mcp图标](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6168414671/p1029573.jpg)，并选中添加的 **Fetch**，此时 MCP 服务器的图标变绿![mcp图标-变绿](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6168414671/p1029574.jpg)。

向输入框输入问题“https://help.aliyun.com/zh/model-studio/rate-limit 请问我遇到限流报错应该怎么办？”，Cherry Studio 通过Fetch工具获取指定网页的内容，并准确回答问题：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997252.png)

阿里云百炼提供 Embedding 模型与 Rerank 模型 API，可无缝集成至 Cherry Studio 的本地知识库功能。

> 据 [Cherry Studio 官方文档](https://docs.cherry-ai.com/knowledge-base/data) 介绍，在 Cherry Studio 知识库中添加的数据全部存储在本地。

### **1\. 添加 Embedding 与 Rerank 模型（可选） API**

单击右上角的设置按钮，在 **模型服务** 栏中找到 **阿里云百炼**，添加`text-embedding-v4`（嵌入模型），Cherry Studio 会自动识别模型功能并标记在模型名称后。

为提升检索效果，您可额外添加`gte-rerank-v2`（重排模型），以增强召回文本与提问的相关性。该模型 **仅支持** **中国内地版** **（北京）地域**，需使用对应的 API 地址。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997109.png)

### **2\. 创建知识库**

在对话框，单击知识库的图标![20251126160222](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6168414671/p1029740.jpg)，单击 **添加知识库**，在知识库页面单击 **添加** 以创建知识库。

![知识库-zh](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6168414671/p1029739.jpg)

#### 2.1. 配置嵌入模型与重排模型

名称输入“百炼错误信息文档”，嵌入模型下拉框选择`text-embedding-v4`，重排模型下拉框选择`gte-rerank-v2`，其它选项保持默认，单击 **确定**。

> 暂无法配置多模态向量模型`multimodal-embedding-v1`。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997185.png)

#### **2.2. 添加知识**

Cherry Studio 提供了文件、目录、网址等多种添加知识的途径，此处以网址信息为例。选中 **网址** 后单击 **添加网址**，输入`https://help.aliyun.com/zh/model-studio/error-code`。等待界面显示嵌入完成![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997193.png)，即可返回对话界面进行提问。

#### **2.3. 提问**

返回对话界面，单击知识库按钮，选中 **百炼错误信息文档**。

![20251126161356](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6168414671/p1029743.jpg)

以用户在使用阿里云百炼时可能遇到的常见问题为例，输入：“Input data may contain inappropriate content.这种报错该咋解决”，可得到以下回答：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6571715571/p997203.png)

## **常见问题**

### **Q：Qwen3 模型为何报错** The value of the enable\_thinking parameter is restricted to True？

A： **原因**：可能使用了 Qwen3 开源版的 Thinking 模型，该类模型仅支持在思考模式下运行（详情请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models#fa618290fc24d "")），但您在调用时关闭了输入框的思考按钮。

**解决方案**：更新 Cherry Studio 客户端，或在使用 Qwen3 Thinking 模型时打开思考按钮。

### **Q：为什么有免费额度但产生了费用？**

A：可能的原因如下：

- **免费额度地域限制**：免费额度仅适用于 **中国内地版**（北京地域）的模型，如果您使用了 **国际版**（新加坡地域）的模型，则会产生费用。请检查您在 [配置模型](https://help.aliyun.com/zh/model-studio/cherry-studio#005ba3e2a0gaf "") 处使用的 **API 地址** 是否正确，详情请参见 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "")。

- **免费额度按模型独立计算**：各模型的免费额度相互独立，不可跨模型共享。例如，当qwen-max模型的免费额度耗尽后，继续调用该模型会产生费用，即便其他模型（如qwen-max-latest）仍有可用免费额度。

- **免费额度数据更新延迟**：控制台显示的免费额度数据每小时更新。因此，即使控制台显示仍有余量，您的免费额度也可能已经耗尽，导致产生了调用费用。建议您稍后再次查看最新的免费额度情况。


您可以通过 [如何查看产生费用的模型？](https://help.aliyun.com/zh/model-studio/new-free-quota#3bfa8283d0tc2 "") 及 [如何查看模型调用记录？](https://help.aliyun.com/zh/model-studio/new-free-quota#ab6ba5c538rn3 "") 确认费用详情。