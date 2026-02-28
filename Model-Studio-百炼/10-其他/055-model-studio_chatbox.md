### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)Chatbox

# Chatbox

更新时间：2026-02-12 02:59:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：文本与多模态向量化](https://help.aliyun.com/zh/model-studio/embedding)[下一篇：Cherry Studio](https://help.aliyun.com/zh/model-studio/cherry-studio)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

1\. 打开 Chatbox

2\. 配置模型与 API Key

2.1. 选择自定义提供方

2.2. 配置模型与 API 密钥

2.3. 对话设置

3\. 对话

常见问题

Q：如何计费？

Q：Chatbox 报错：“连接 Custom Provider 失败”怎么办？

Q：传入的图片和文档有什么限制？

Chatbox 是一款 AI 客户端应用和智能助手，您无需配置计算环境即可通过 Chatbox 与大模型进行对话。

## **前提条件**

- 您需要 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，并确保已开通阿里云百炼的模型服务；

- 在 [模型列表](https://help.aliyun.com/zh/model-studio/models "") 选择您需要使用的文本生成模型。如果您是 RAM 用户，请参见 [业务空间管理](https://help.aliyun.com/zh/model-studio/use-workspace "")，确保您有相应模型的调用权限。


> 由于 Chatbox 的功能可能发生变化，模型的支持情况以实际效果为准。


## **1\. 打开 Chatbox**

前往[Chatbox](https://chatboxai.app/zh)，根据您的设备下载并安装合适的版本，或直接 **启动网页版**。

## **2\. 配置模型与 API Key**

### **2.1. 选择** **自定义提供方**

单击 Chatbox 页面左下方的 **设置**，单击 **模型提供方**，单击底部的 **添加**。

在弹窗中进行编辑。 **名称** 输入“DashScope”， **API 模式** 选择 **OpenAI API 兼容**，单击 **添加**。

![20251125105130](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029225.jpg)

### **2.2. 配置模型与 API 密钥**

|     |     |
| --- | --- |
| |     |     |
| --- | --- |
| **配置项** | **说明** |
| **API 密钥** | 填入您在阿里云百炼申请的 API Key。 |
| **API 主机** | 根据您要调用模型的地域，填入对应的URL：<br>- **北京地域**：`https://dashscope.aliyuncs.com/compatible-mode/v1`<br>  <br>- **新加坡地域**：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`<br>  <br>- **弗吉尼亚地域**：`https://dashscope-us.aliyuncs.com/compatible-mode/v1`<br>  <br>> API 路径无需填写。 |
| **模型** | 在模型处单击 **新建**，在 **模型ID** 填入您需要使用的千问或 DeepSeek 模型，此处以`qwen3-235b-a22b`为例，勾选 **推理** 与 **工具使用** 按钮。<br>> 若使用其他模型，请根据其具体能力判断是否勾选。支持推理的模型请参见 [深度思考](https://help.aliyun.com/zh/model-studio/deep-thinking "") 与 [视觉推理](https://help.aliyun.com/zh/model-studio/visual-reasoning "")，支持工具使用的模型请参见 [Function Calling](https://help.aliyun.com/zh/model-studio/qwen-function-calling "")。 | | ![20251125133759](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029292.jpg) |

### **2.3. 对话设置**

完成模型与 API 密钥配置后，单击设置页面左侧的 **对话设置**。在弹窗设置 **上下文的消息数量上限** 与 **温度** 参数：

- **上下文的消息数量上限**

每次提问后，大模型参考的历史对话轮数。对于日常聊天对话场景，建议设为5-10。过多的上下文消息数量可能导致报错：`Range of input length should be [1, xxx]`。

- **温度**

用于控制大模型生成文本的多样性。


  - **温度** 越高，生成的文本更多样，适合内容创作、头脑风暴等场景；

  - **温度** 越低，生成的文本更确定。适合代码撰写、数学推理等场景。


> 请设置为小于2的数，否则会报错`'temperature' must be Float`。

- **Top P**

与温度参数作用类似，用于控制生成文本的多样性。


> 请设置为不大于1的数，否则会报错"xx is greater than the maximum of 1 - 'top\_p'"。


## **3\. 对话**

在对话框输入问题，即可开始对话。

> 当前无法传入视频或音频文件进行对话。

普通对话

传入图片

传入文档

在输入框输入“你是谁？”进行测试：

![20251125163922](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029426.jpg)

Chatbox 能够将 Qwen3 模型的思考过程与回复内容进行展示。

#### **1\. 选择模型**

图片问答需要使用具有视觉能力的模型，您可以在配置时选择 [Qwen-VL](https://help.aliyun.com/zh/model-studio/vision#064dc773ccxdn "")、 [QVQ](https://help.aliyun.com/zh/model-studio/visual-reasoning#5be853b164zv4 "") 或 [Qwen-Omni](https://help.aliyun.com/zh/model-studio/qwen-omni#4d82d2217ay95 "") 模型。

参见 [2.2. 配置模型与 API 密钥](https://help.aliyun.com/zh/model-studio/chatbox#ff6dff39e5ww4 "")，在 **模型** 处添加您需要使用的视觉模型，并勾选 **视觉** 能力。

![20251125170032-zh](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029431.jpg)

#### **2\. 对话**

在发送按钮旁选择视觉模型![20251125170154](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029433.jpg)，在输入框中输入问题，并单击![20251125170311](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029434.jpg)，选择 **添加图片** 传入图片。

![诗-zh](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029436.jpg)

Chatbox 支持传入pdf、docx、txt等类型的文件，使模型基于文档进行回答。

> Chatbox 暂时无法解析文档中的图片信息。

#### **1\. 选择模型**

拥有较长上下文处理能力的模型适合用于文档问答场景，建议您选择[Qwen-Flash](https://help.aliyun.com/zh/model-studio/models#13ff05e329blt "")、 [Qwen-Long](https://help.aliyun.com/zh/model-studio/long-context-qwen-long#eb5a1ae09ec37 "") 或`qwen2.5-14b-instruct-1m`、`qwen2.5-7b-instruct-1m`，这些模型具有百万级别 Token 的处理能力与较低的价格。

参见 [2.2. 配置模型与 API 密钥](https://help.aliyun.com/zh/model-studio/chatbox#ff6dff39e5ww4 "")，在 **模型** 处添加您需要使用的模型。此处以 `qwen-flash` 为例。

![flash-zh](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029439.jpg)

#### **2\. 对话**

在发送按钮旁选择添加的模型![flash](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029440.jpg)，在输入框中输入问题，并单击![20251125170311](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029434.jpg)，点击 **选择文件**。

> 基于文档的连续提问可能造成大量的 Token 消耗，为了节省成本，您可以：降低 **上下文的消息数量上限**，减少输入的 Token 数；或优先选择 `qwen-flash` 模型，该模型支持 [上下文缓存](https://help.aliyun.com/zh/model-studio/context-cache "")，可以在多轮对话中降低输入 Token 的费用。

![openzh](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2953214671/p1029441.jpg)

## **常见问题**

### **Q：如何计费？**

A：阿里云百炼对模型输入与输出的 Token 进行计费，模型 Token 的费用请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

> 多轮对话会带入历史对话记录，从而消耗较多 Token。您可以新开对话或降低 **上下文的消息数量上限**，减少不必要的 Token 消耗。日常聊天建议设置 **上下文的消息数量上限** 为5-10。

### **Q：Chatbox 报错：“** 连接 Custom Provider 失败”怎么办？

A：请您根据报错信息进行排查：

- Range of input length should be \[1, xxx\]

可能是您输入的内容过长，或多轮对话累积的上下文超过模型最大上下文长度。请您根据您的使用情况进行排查：

  - **首次对话即报错**

    有可能是您输入的文本过长，或传入的文件包含较多 Token，您可以使用 qwen-flash、qwen-long等上下文长度达到 1,000,000的模型来处理您的请求。

  - **多轮对话后报错**

    有可能是多轮对话累积的 Token 超过了模型的最大上下文长度，您可以参考以下方法：

    1. 新开对话

       大模型回复时将不再参考历史对话。

    2. 减少 **上下文的消息数量上限**

       使大模型回复时仅参考一定范围内的对话记录，避免输入所有历史对话。

    3. 更换模型

       更换为qwen-flash、qwen-long等上下文长度达到 1,000,000的模型以处理更长的上下文，从而进行更多轮的对话。
- Access denied, please make sure your account is in good standing.

您可以查看 [阿里云账户](https://usercenter2.aliyun.com/home?spm=a2c4g.11186623.nav-v2-dropdown-my-aliyun.9.f6683048dWvpGu) 是否欠费。如果欠费，即使模型有免费额度也无法调用。

- 'temperature' must be Float

模型的 `temperature`参数需要小于2，您可以将 **温度(Temperature)** 参数设为小于2的数。


> 如果您的问题不在上述范围，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行排查。

### **Q：传入的图片和文档有什么限制？**

A：

- **图片**：传入图片的限制请参见 [图像与视频理解](https://help.aliyun.com/zh/model-studio/vision#430cb5ea4cety "")；

- **文档**：Chatbox 会对传入的文档进行解析，解析生成的文本与上下文的 Token 长度不高于模型最大上下文长度即可。