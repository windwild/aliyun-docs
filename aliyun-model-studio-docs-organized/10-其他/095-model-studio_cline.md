### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[接入客户端/开发工具](https://help.aliyun.com/zh/model-studio/use-chat-client-or-development-tool/)Cline

# Cline

更新时间：2026-02-19 22:21:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Claude Code](https://help.aliyun.com/zh/model-studio/claude-code)[下一篇：Cursor](https://help.aliyun.com/zh/model-studio/cursor)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

使用步骤

1\. 安装 Cline

2\. 配置模型与 API Key

3\. 使用 Cline

常见问题

Q：为什么报 401 Incorrect API key provided 错误？

Q：为什么 Token 消耗快？

Q：如何节省 Token？

Q：使用 QwQ 模型报错400 <400> InternalError.Algo.InvalidParameter: An error during model pre-process？

Cline 是一款用于智能编程的 VSCode 插件，您可以集成阿里云百炼提供的千问或 DeepSeek 模型，完成复杂的编程任务。

**重要**

本文档仅适用于按量付费模式。如果您已订阅阿里云百炼 Coding Plan 并希望在 Cline 中使用，请参考 [Coding Plan](https://help.aliyun.com/zh/model-studio/coding-plan "") 进行配置。

## **前提条件**

- 您需要 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，并确保已开通阿里云百炼的模型服务；

- 在 [模型列表](https://help.aliyun.com/zh/model-studio/models "") 选择您需要使用的千问或DeepSeek 模型。


> 由于 Cline 的功能可能发生变化，模型的支持情况以实际效果为准。

- 您需要下载并安装 [VSCode](https://code.visualstudio.com/) IDE。


## **使用步骤**

### **1\. 安装 Cline**

打开 VSCode，在扩展商店搜索`Cline`并安装。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2061045471/p947567.png)

### **2\. 配置模型与 API Key**

安装完成后，您需要打开左侧边栏的![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2061045471/p947571.png)进入 Cline 的界面，单击 **Bring my own API key**，在弹出的界面中，请选择 **API Provider** ：

- **推荐**：选择 **OpenAI Compatible**，可以灵活使用包括最新模型在内的更广泛模型。

- **备选**：选择 **Alibaba Qwen**，配置步骤更简单，但可能不支持部分最新模型。


> 如果您之前使用过 Cline，请单击右上角的设置按钮后进行配置。

OpenAI Compatible

Alibaba Qwen

推荐使用此方式，支持更广泛的模型。详细配置如下：

|     |     |
| --- | --- |
| |     |     |
| --- | --- |
| **配置项** | **说明** |
| **API Provider** | 选择 **OpenAI Compatible**。 |
| **Base URL** | 根据您要调用模型的地域，填入对应的URL：<br>- **北京地域**：`https://dashscope.aliyuncs.com/compatible-mode/v1`<br>  <br>- **新加坡地域**：`https://dashscope-intl.aliyuncs.com/compatible-mode/v1`<br>  <br>- **弗吉尼亚地域**：`https://dashscope-us.aliyuncs.com/compatible-mode/v1` |
| **API Key** | 根据使用模型的地域，填入对应的 API Key。 |
| **Model ID** | 填入您需要使用的模型名。建议您选择代码能力较强的模型，如：<br>- `qwen3.5-plus`<br>  <br>- `qwen3-coder-next`<br>  <br>- `qwen3-coder-plus`<br>  <br>- `qwen3-max`<br>  <br>各模式支持的模型请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。 |
| 其它 | 其它选项保持默认即可。更多功能请您根据需要进行探索。<br>**说明**<br>如果您使用 Qwen3（思考模式）或 QwQ 模型，请单击`MODEL CONFIGURATION`，并勾选 **Enable R1 messages format**。 |

单击 **Continue** 完成配置。

> 如果您之前使用过 Cline，请单击右上角的 **Done**。 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7476423571/p988858.png) |

|     |     |
| --- | --- |
| |     |     |
| --- | --- |
| **配置项** | **说明** |
| **API Provider** | 选择 **Alibaba Qwen**。 |
| **Alibaba API LIne** | - 若使用**北京地域**模型，选择 **China API**。<br>  <br>- 若使用**新加坡地域**模型，选择 **Internationl API**。 |
| **Qwen API Key** | 根据使用模型的地域，填入对应的 API Key。 |
| **Model ID** | 在下拉栏中选择您需要使用的模型。建议您选择编程能力较强的模型，如：<br>- `qwen-coder-plus`<br>  <br>- `qwen2.5-coder-32b-instruct`<br>  <br>> 部分最新模型（如 qwen3-coder 系列）在**北京地域**下可能无法选择。如需使用这些模型，建议将 API Provider 更换为 OpenAI Compatible。 |
| 其他 | 其它选项保持默认即可。更多功能请您根据需要进行探索。<br>**说明**<br>模型的上下文参数与价格请参考 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。 |

单击 **Continue** 完成配置。

> 如果您之前使用过 Cline，请单击右上角的 **Done**。 | ![20251201174113](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1446854671/p1031124.jpg) |

### **3\. 使用 Cline**

您可以通过输入框上方的 **Auto-approve** 来对 Cline 的读、写、执行命令等权限进行配置。

**重要**

打开这些权限可能导致 Token 消耗量的增加，建议您在充分了解 Cline 的功能特性后打开这些权限。

Cline 分为 **Plan** 和 **Act** 两种工作模式。

- **Plan** 模式下，Cline 将主要负责收集信息、拆解问题并设计完成任务的详细计划，但不会对文件直接进行修改。

- **Act** 模式下，Cline 将专注于制定方案并逐步完成具体操作，可以运行命令与修改文件。


您可以在对话框的下侧进行模式的切换。

Plan

Act

以生成 Python 快速排序算法为例，在 Plan 模式下向 Cline 提问：“写一个 Python 的快速排序算法？直接把代码给我。”

![20251127145130](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5051324671/p1030114.jpg)

在 Plan 模式下 Cline 不会直接进行代码文件的创建与修改。在 Act 模式下，Cline 会直接新建文件并将代码写入。

您可以新开一个会话，切换到 Act 模式。以生成 Python 快速排序算法为例，向 Cline 提问：“写一个 Python 的快速排序算法？”

![20251127151539](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5051324671/p1030127.jpg)

Cline 不仅生成了代码，还会将代码写进文件，并询问是否需要运行文件来测试效果，在您确认后 Cline 才会运行命令。

## **常见问题**

### **Q：为什么报** 401 Incorrect API key provided 错误？

A：可能有以下原因：

- API Key 和 **Base URL** 的地域不匹配，请检查二者是否对应。

- 低版本 Cline 不支持选择 **Alibaba Qwen** 作为 **API Provider**。请升级 Cline，或将 **API Provider** 更换为 **OpenAI Compatible**。


### **Q：为什么 Token 消耗快？**

A：Cline 会读取您本地的项目文件，并且多次调用API，这可能造成大量的 Token 消耗。如果您只需要简单的问答场景，请取消勾选输入框上方的 **Auto-approve** 并使用 Plan 模式。

### **Q：如何节省 Token？**

A：

1. **减少无关文件**：为避免扫描不相关文件而造成 Token 消耗，建议在具体的项目目录中启动 Cline，同时仅保留必要的项目文件。

2. **总结对话**：Cline 会将历史对话内容作为上下文，可以点击 **Compact Task** 按钮或输入命令`/compact`总结对话内容。

![20251127153230](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5051324671/p1030138.jpg)

3. **精确指令**：模糊的请求会触发非必要的文件扫描，消耗更多的 Token。请在使用 Cline 时提出更明确、具体的问题或指令。

4. **分解任务**：在处理复杂任务时，可以将其分解为若干简单任务。


### **Q：使用 QwQ 模型报错** 400 <400> InternalError.Algo.InvalidParameter: An error during model pre-process **？**

A：请在设置界面单击`MODEL CONFIGURATION`，并勾选 **Enable R1 messages format。**