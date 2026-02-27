### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)Cursor

# Cursor

更新时间：2026-02-19 23:02:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Cline](https://help.aliyun.com/zh/model-studio/cline)[下一篇：Dify](https://help.aliyun.com/zh/model-studio/dify)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型配置

支持的模型

模型选型建议

详细步骤

步骤一：安装 Cursor

步骤二：开通阿里云百炼

步骤三：配置模型

常见问题

Q：为什么无法添加自定义模型，报错“The model xxx does not work with your current plan or api key”？

Q：配置完成后找不到添加的模型怎么办？

Q：为什么调用模型报错“We're having trouble connecting to the model provider. ”或“Unauthorized User API key”？

Q：模型响应速度较慢怎么办？

阿里云百炼支持通过 Cursor 使用千问系列模型。您可在 Cursor 中配置 OpenAI 兼容的 Base URL 和 API Key，将模型切换为百炼提供的模型进行代码编写与对话。

**重要**

**本文档仅适用于按量付费模式**。如果您已订阅阿里云百炼 Coding Plan 并希望在 Cursor 中使用，请参考 [Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan "") 进行配置。

## 模型配置

### **支持的模型**

|     |     |
| --- | --- |
| **文本生成-千问** | [千问Max](https://help.aliyun.com/zh/model-studio/models#qwen-max-cn-bj "")、 [千问Plus](https://help.aliyun.com/zh/model-studio/models#03a05ab98953u "")、 [千问Flash](https://help.aliyun.com/zh/model-studio/models#9b418d9a481yp "")、 [千问Turbo](https://help.aliyun.com/zh/model-studio/models#218847c4b35vb "")、 [千问Coder](https://help.aliyun.com/zh/model-studio/models#5d7f137a6467d "")、 [QwQ](https://help.aliyun.com/zh/model-studio/models#5b345b2e75d35 "") |
| **文本生成-千问-开源版** | [Qwen3.5](https://help.aliyun.com/zh/model-studio/models#7a4e23add2464 "")、 [Qwen3](https://help.aliyun.com/zh/model-studio/models#2c9c4628c9yyd "")、 [QwQ-开源版](https://help.aliyun.com/zh/model-studio/models#690e39465dvqv "")、 [QwQ-Preview](https://help.aliyun.com/zh/model-studio/models#18e88cc886ll3 "")、 [Qwen2.5](https://help.aliyun.com/zh/model-studio/models#15f2bdc5dd3zd "")、 [Qwen2](https://help.aliyun.com/zh/model-studio/models#4969f9cd9170b "")、 [Qwen1.5](https://help.aliyun.com/zh/model-studio/models#759b2e1092vt2 "")、 [Qwen-Coder](https://help.aliyun.com/zh/model-studio/models#8fa09f2273rf2 "") |
| **文本生成第三方模型** | [MiniMax-M2.1](https://help.aliyun.com/zh/model-studio/models#6194236b53fx0 "") |

### 模型选型建议

- **深度研发与架构设计**：推荐使用`qwen3.5-plus` 、`qwen3-max`、`qwen3-coder-plus`、`qwen3-coder-next`。适用于复杂算法实现、系统架构设计及核心逻辑推理。

- **辅助编码与轻量任务**：推荐使用 `qwen3-coder-next`、`qwen-flash`。适用于代码补全、解释及日常脚本编写。


## 详细步骤

### 步骤一：安装 Cursor

通过 [Cursor 官网](https://cursor.com/features) 下载并安装 Cursor。

**说明**

由于 Cursor 的产品限制，仅订阅 **Cursor Pro** 及以上套餐的用户支持自定义配置模型，否则会报错“The model xxx does not work with your current plan or api key”。

### 步骤二：开通阿里云百炼

1. **注册账号**：若无阿里云账号，需首先[注册](https://account.alibabacloud.com/register/intl_register.htm)。


> 如遇问题，请参见 [注册阿里云账号](https://help.aliyun.com/zh/account/step-1-register-an-alibaba-cloud-account "")。

2. **开通阿里云百炼：** 使用 **阿里云主账号** 前往[阿里云百炼大模型服务平台](https://bailian.console.aliyun.com/?tab=model#/model-market)，阅读并同意协议后，将自动开通阿里云百炼，如果未弹出服务协议，则表示您已经开通。


> 如果开通服务时提示"您尚未进行实名认证"，请先进行 [实名认证](https://help.aliyun.com/zh/account/verify-your-identity-individual-account "")。


> 首次开通百炼后，您可领取新人免费额度（有效期：百炼开通后90天内），用于模型推理服务。免费额度领取方法和详情，请查看 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 页面。

**说明**

超出额度或期限将产生费用，开启 [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 功能可避免此情况下产生费用，具体费用请以控制台的实际报价和最终账单为准。

### 步骤三：配置模型

1. 在 Cursor 中，点击![2026-02-03_16-52-37](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0376170771/p1052115.jpg)图标，单击 **Cursor Settings**，选择 **Models** 页面。

2. 开启 **OpenAI API Key**，填入 [阿里云百炼API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")

3. 开启 **Override OpenAI Base URL**，根据地域填入服务地址：

   - **华北2（北京）**：`https://dashscope.aliyuncs.com/compatible-mode/v1`

   - **新加坡**：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`

   - **美国（弗吉尼亚）**：`https://dashscope-us.aliyuncs.com/compatible-mode/v1`
4. 在 **Add or search model** 中，输入要使用的模型名称，点击 **Add Custom Model**，建议选择代码能力较强的模型，各模式支持的模型请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。


配置完成后，在聊天面板中选择已配置的模型即可开始使用。

![2026-02-03_17-20-29](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9210680771/p1052132.jpg)

## 常见问题

### Q：为什么无法添加自定义模型，报错“The model xxx does not work with your current plan or api key”？

A：请检查您的 Cursor 订阅套餐是否为 Cursor Pro 及以上版本。只有 Pro 及以上套餐支持添加自定义模型功能。

### Q：配置完成后找不到添加的模型怎么办？

A：请在聊天面板点击并关闭 **Auto** 模式，在模型下拉栏选择所需模型。

### **Q：为什么调用模型报错“We're having trouble connecting to the model provider. ”或“** Unauthorized User API key **”？**

A：可能有以下原因：

- 您调用的模型不存在，各部署模型模式支持的模型请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

- 在配置了阿里云百炼的请求地址和API Key后，调用其他模型提供商的模型将导致报错。如需使用其他模型，请依据情况重新配置或关闭 **OpenAI API Key** 和 **Override OpenAI Base URL**。

- 报错可能源于 Cursor 软件与部分模型不兼容，而非配置或模型提供商的问题。


### Q：模型响应速度较慢怎么办？

A：响应速度受多种因素影响，建议：

- **选择合适的模型**：对于简单任务，使用 `qwen3-coder-next` 、`qwen-flash` 可获得更快的响应速度。

- **检查网络连接**：确保网络连接稳定，必要时可切换网络环境。

- **减少上下文长度**：过长的对话历史会增加处理时间，为提升响应效率，可以开启新的对话。