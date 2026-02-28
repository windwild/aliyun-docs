### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 模型体验介绍

# 模型体验介绍

更新时间：2024-09-18 23:41:28

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型体验

模型调试

对输入模式进行调试

对模型配置进行调试

历史对话一键继承

本篇内容介绍模型体验和模型调试。

## **模型体验**

支持选择多个模型同时体验，快速对比不同模型的效果，最多同时选择3个模型，支持差异化模型配置及重复模型选择。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7827176271/p850876.png)

**说明**

- 为了保障模型的正常使用和输出质量，模型体验中心不同模型的文本输入长度限制不同，例如Qwen-Long模型输入Token限制为2k个。如果您需要输入更长的文本，建议使用API调用方式，具体操作请参见 [API详情](https://help.aliyun.com/document_detail/2788814.html "")。

- 关于模型输入输出限制Token的具体规则，以及各大模型收费标准，请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

- 关于Token的计算方法，请参见 [Token是怎么计算的](https://help.aliyun.com/zh/model-studio/billing-for-model-studio#79de3fd8a6cr4 "")。


**示例内容**：

提问：阿里云百炼大模型是什么

下方图片展示了不同大模型生成的答案。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7827176271/p850859.png)

## **模型调试**

支持对文本模型的模型配置和输入模式进行调试，并透明地查看模型输出结果。

### **对输入模式进行调试**

对输入模式进行调试，以便于开发者调试模型的效果。

输入模式包括Prompt模式及Message模式。其中，Prompt模式更侧重于单次的文本生成，而Message模式则适用于需要跟踪对话历史的多轮对话场景。

- Prompt模式：在Prompt模式下，您直接向模型提供一段文本作为输入，这段文本即为Prompt，模型根据Prompt生成响应。Prompt可以包含指令、问题、上下文等信息，指导模型生成特定格式或内容的回复。

- Message模式：Message模式更适用于对话场景。它通过一系列的Message（消息）来构建对话历史，每个Message包括角色（如system、user、assistant）和内容。模型基于整个对话历史生成回复，能够保持对话的连贯性和上下文的一致性。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7827176271/p850870.png)

### **对模型配置进行调试**

对模型配置进行调试，以便于开发者对模型配置差异化效果进行对比。支持top-p、system、自定义随路参数及自定义停止符等多种自定义模型配置。

> 不同模型的参数不同，请以界面实际显示为准。

- system：系统人设，例如“你是一个AI助手”。

- top\_p：控制核采样方法的概率阈值，取值越大，生成的随机性越高。

- temperature：控制生成随机性和多样性，范围（0，2）。建议该参数和top\_p只设置1个。

- stop：用于控制生成时遇到某些内容则停止。您可以传入多个字符串。

- enable\_search：是否参考搜索的结果，默认为false。


**示例内容**：

使大模型检测Prompt中是否存在错别字，并进行纠正。详细内容参数值参考下方图片。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7827176271/p850932.png)

## **历史对话一键继承**

新增对比模型时，一键继承已有模型历史对话，保持History消息不变的情况下，查看后续对话效果对比。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7827176271/p850975.png)