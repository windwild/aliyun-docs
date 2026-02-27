### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)Assistant API

# Assistant API

更新时间：2025-10-15 04:15:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

与文本生成 API 的区别

交互方式

模型支持

工具支持

快速开始

Assistant API 旨在帮助开发者快速构建 [大模型应用](https://help.aliyun.com/zh/model-studio/application-introduction#c92394b9b4d8v "")（Assistant），例如个人助理、智能导购、会议助手等。相比 [文本生成API](https://help.aliyun.com/zh/model-studio/text-generation "")，Assistant API 内置了对话管理、知识检索以及多种工具的调用能力，从而降低了此类应用的开发成本。

**说明**

[智能体应用](https://help.aliyun.com/zh/model-studio/single-agent-application "") 和 Assistant 均为大模型应用，但二者的功能相互独立，其管理方法（创建、读取、更新和删除）也有所不同：

- 智能体应用：采用无代码/低代码的设计理念，仅可通过控制台进行管理。

- Assistant：采用纯代码的设计理念，仅可通过 Assistant API 进行管理。


## **与文本生成 API 的区别**

文本生成 API 的基本要素是消息（Messages），您可以使用模型（Models，如 Qwen-Plus、Qwen-Max 等）生成消息。在使用这种轻量级的 API 时，您需要手动管理对话状态、定义工具、检索知识库和执行代码，才能构建一个简单的智能体应用。

在文本生成 API 的基础上，Assistant API 的基本要素演进为：

- 消息对象（Messages）：封装了对话信息的角色和内容，类似于文本生成 API 的消息。

- 智能体对象（Assistants）：封装了一个基础模型，默认指令和工具。

- 线程对象（Threads）：表示当前的对话状态。

- 运行对象（Runs）：驱动智能体在一个对话线程上执行，包括文本响应和工具使用。


接下来，您将进一步了解这些基本元素的交互方式，以构建一个智能体应用。

## **交互方式**

Assistant API 使用线程（Thread）机制来确保消息按顺序执行，从而维护对话的连贯性。具体流程如下：

1. **创建消息实例**：用户使用`Message.create()`方法创建消息实例，将其归属于特定线程，确保消息与上下文正确关联。

2. **启动运行环境**：使用`Run.create()`函数初始化智能体对象的运行环境，提供消息处理所需的配置。

3. **等待结果**：调用`wait()`函数等待智能体对象完成处理并返回结果，确保在获取响应前程序保持同步，避免数据乱序。


以一个简单的绘画智能体应用为例：

|     |     |
| --- | --- |
| - **用户输入**：用户输入两条消息：<br>  <br>  - 输入1：“你是一位画家”<br>    <br>  - 输入2：“帮我画一只猫”<br>- **消息创建**：每个用户输入的消息通过 `Message.create()` 方法创建并发送到线程。<br>  <br>- **线程处理**：线程通过 `Thread.create()` 创建会话，接收消息，并传递给智能体对象。<br>  <br>- **消息传递给智能体**：智能体对象收到上下文信息，分别处理每条消息：<br>  <br>  - 消息1（“你是一位画家”）的角色是用户。<br>    <br>  - 消息2（“帮我画一只猫”）的角色也是用户。<br>- **智能体的响应**：智能体对象处理用户消息后生成相应的回复，输出消息3，角色为智能体，回复内容为“布偶猫\[url\]”。<br>  <br>- **运行和等待**：运行通过 `Run.create()` 创建并开始执行，之后智能体在 `Run.wait()` 阶段等待任务完成。 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6468924271/p836947.png) |

## **模型支持**

**说明**

Assistant API 不支持模型的快照版本（例如qwen-plus-0919）。模型的兼容性以 Assistant API 的实际执行结果为准，更多详情可参考 [模型列表与价格](https://help.aliyun.com/zh/model-studio/models "")。

| **模型系列** | **模型标识符** |
| --- | --- |

|     |     |
| --- | --- |
| **模型系列** | **模型标识符** |
| 通义千问-Turbo | qwen-turbo |
| 通义千问-Plus | qwen-plus |
| 通义千问-Max | qwen-max |
| 通义千问2-开源版-57B | qwen2-57b-a14b-instruct |
| 通义千问2-开源版-72B | qwen2-72b-instruct |

## **工具支持**

**说明**

插件的兼容性请以 Assistant API 的实际执行结果为准，更多详情可参考 [插件列表](https://help.aliyun.com/zh/model-studio/user-guide/plug-ins/ "")。

| **工具（tools）** | **唯一标识符** | **用途** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **工具（tools）** | **唯一标识符** | **用途** |
| 代码解释器插件 | code\_interpreter | 帮助执行 Python 代码，适用于编程问题、数学计算、数据分析等场景 |
| 夸克搜索插件 | quark\_search | 用于实时检索网络信息，增强知识获取能力。 |
| 图片生成插件 | text\_to\_image | 将文字描述转为图像，丰富回复形式。 |
| 函数调用（Function calling） | function | 在本地设备上执行特定功能，无需依赖外部网络服务。 |
| 知识检索增强（RAG） | rag | 检索外部知识，增强大模型回答准确性。 |
| 自定义插件 | ${plugin\_id} | 连接自定义业务接口，扩展 AI 业务能力。 |

## 快速开始

如需调试大语言模型或快速掌握 Assistant API，请参考：

- [模型体验](https://bailian.console.aliyun.com/#/efm/model_experience_center/text)：支持测试各类大模型的推理效果，为选择合适的 Assistant 模型提供参考依据。

- [快速入门](https://help.aliyun.com/zh/model-studio/quick-start-of-assistant-api "")：通过基本用法和示例，引导您快速构建首个 Assistant。

- [API 手册](https://help.aliyun.com/zh/model-studio/assistantapi/ "")：详细解析 Assistant API 各组件的参数，帮助您解决开发中的疑难问题。