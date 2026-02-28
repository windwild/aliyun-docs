### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[产品概述](https://help.aliyun.com/zh/functioncompute/fc/product-overview/)[产品动态](https://help.aliyun.com/zh/functioncompute/fc/product-overview/release-notes-1/)2026年功能发布记录

# 2026年功能发布记录

更新时间：2026-02-12 00:48:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读

2026年01月

本文介绍函数计算FC的产品功能和对应的文档动态。

## **2026年01月**

| **产品** | **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **产品** | **功能名称** | **变更类型** | **功能描述** | **相关文档** |
| AgentRun | 知识库集成 | 新增 | 知识库功能支持将外部专业文档或私有数据关联至 AI Agent。Agent 在执行任务时可检索相关上下文，以提升回答的准确性与时效性。 | [知识库集成指南](https://help.aliyun.com/zh/functioncompute/fc/knowledge-base-integration-guide "") |
| API聚合打包 | 新增 | 支持将不同类型的工具（如 MCP Server、RESTful API）统一封装为 MCP 服务，提供统一的访问入口。该功能支持存量 API 的接入，并可减少 Agent 访问多个工具时的网络与资源开销。 | [API打包](https://help.aliyun.com/zh/functioncompute/fc/api-packaging "") |
| 持久化记忆存储 | 新增 | 为 Agent 提供持久化记忆能力，支持跨会话保存与检索用户交互历史、偏好信息等上下文数据。基于向量检索技术，Agent 可根据历史记忆提供响应，并支持通过 MCP 工具或 LangChain 等开源框架进行集成。 | [记忆存储](https://help.aliyun.com/zh/functioncompute/fc/memory-storage "") |
| Flow创建Agent | 新增 | 基于流程画布（Flow）模式的可视化编排功能。支持开始节点、LLM 节点、MCP 服务节点、代码执行节点等多种类型，系统可将画布配置转换为可执行的工作流。支持对话模式和工作流模式两种执行方式。 | [低代码创建Agent快速入门](https://help.aliyun.com/zh/functioncompute/fc/quick-start-to-low-code-agent-creation "") |
| PrivateLink内网访问 | 新增 | 支持通过 PrivateLink 建立 VPC 私有连接。用户可通过自定义内网域名安全、稳定地访问 AgentRun 资源，无需暴露于公网，提升访问安全性和稳定性。 | [通过PrivateLink内网访问AgentRun资源](https://help.aliyun.com/zh/functioncompute/fc/access-agenrun-resources-through-privatelink-intranet "") |
| 函数计算 | CORS配置支持 | 优化 | 支持通过 API 方式配置 CORS 请求处理策略。用户可在 HTTP 触发器或自定义域名上直接配置策略，无需在函数代码中编写跨域逻辑。 | [HTTP触发器概述](https://help.aliyun.com/zh/functioncompute/fc/user-guide/http-triggers-overview "")<br>[配置自定义域名](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-custom-domain-names "") |