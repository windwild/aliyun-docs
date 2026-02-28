### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/) [用户指南（应用）](https://help.aliyun.com/zh/model-studio/application-user-guide/) [应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/) [官方应用-通义深度搜索](https://help.aliyun.com/zh/model-studio/tongyi-deepsearch/) [API参考](https://help.aliyun.com/zh/model-studio/deepsearch-api-reference/) API概览

# API概览

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：API参考](https://help.aliyun.com/zh/model-studio/deepsearch-api-reference/)[下一篇：服务接入节点](https://help.aliyun.com/zh/model-studio/deepsearch-service-access-point)

该文章对您有帮助吗？

反馈

本产品（通义深度搜索）对外服务接口目录。所有接口使用 DashScope HTTP 协议对外提供服务。

## **API鉴权**

调用接口需要先 [获取 API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，邀测期间，仅百炼 **默认业务空间** 所属的API Key有调用权限。

## **API目录**

|     |     |
| --- | --- |
| **API名称** | **API概述** |
| [生成对话](https://help.aliyun.com/zh/model-studio/deepsearch-chat-generate "") | 基于智能体应用管理提供的 agent\_id 与 agent\_version 信息，提供场景化对话、研究、写作相关能力。 |
| [上传文件](https://help.aliyun.com/zh/model-studio/deepsearch-file-upload "") | 基于动态文件操作接口能力获取处理好的文件信息，支持智能体应用的 API 调用通过 parameters.agent\_options.sessions\_files 参数完成“动态文档解析”工具的文件数据注入。 |
| [对话文件管理](https://help.aliyun.com/zh/model-studio/deepsearch-session-file-management "") | 深度搜索应用支持按 session\_id 维护对话文件目录树：可基于临时文件ID和文件/目录元信息更新目录树，也可删除文件并获取目录树信息，该能力仅适用于法律阅卷场景。 |
| [生成报告导出](https://help.aliyun.com/zh/model-studio/deepsearch-report-export "") | 深度搜索应用生成的结果报告文件（md、html、pdf）获取。 |
| [对接自有知识库](https://help.aliyun.com/zh/model-studio/docking-self-built-database "") | 支持接入自有知识库，用户可以参考该接口规范进行知识库对接，该能力仅适用于通用场景。 |