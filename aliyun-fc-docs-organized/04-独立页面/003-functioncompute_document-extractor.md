### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 文档提取器

# 文档提取器

更新时间：2025-12-08 02:38:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

定义

前置条件

使用示例

支持的文档类型

输入和输出

常见用例

## **定义**

文档提取节点支持您在工作流中解析特定格式的文档，并将其中的文本内容提取出来。它能将文件转换为文本，让不支持多模态的大模型拥有一定的文本处理的能力，同时可以降低大模型处理文件的成本。

> 支持的文档类型见下文。

## **前置条件**

- [创建AI Studio服务](https://help.aliyun.com/zh/cap/user-guide/create-an-ai-studio-service/ "")


## **使用示例**

1. 在开始时，声明单文件或多文件类型的变量，例如file。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2524715671/p1033020.png)

2. 添加文档提取器节点，并将文件变量作为输入。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2524715671/p1033021.png)

3. 添加结束文件。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2524715671/p1033022.png)

4. 测试，输入文件地址，并执行。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2524715671/p1033023.png)


## **支持的文档类型**

- **文本文档**：例如Markdown、TXT等类型文件；

- **Office Word文档**：不包括DOC类型的文件；

- **PDF文档**；

- **表格文档**：例如XLS、XLSX、CSV类型的文件；

- **专业格式文档**：例如YAML、JSON文件；


**说明**

如果文档中包含非文本的内容（例如二进制信息、音视频信息），相关的内容不会被处理。

## **输入和输出**

- 文档提取器可以接受文档类型文件作为输入，可以是单文件，也可以是文件列表。

- 当文档提取器接受单文件作为输入时，输出是字符串类型的文本内容；

- 当文档提取器接受文件列表作为输入时，输出是字符串数组类型的文本内容。


## **常见用例**

- 提取文档并让大模型总结关键信息：配合提示词，可以让大模型将用户关注的内容从文件中提取出来，例如合同条款提取、论文核心内容总结等；

- 提取文档：用于分析、建议索引或迁移等；

- 文档存储：将文档录入数据库、知识库等。