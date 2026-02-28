### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) MCP服务简介

# MCP服务简介

更新时间：2025-08-29 06:14:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

为什么推荐在函数计算开发和托管MCP服务？

计费说明

创建MCP服务

使用MCP服务

模型上下文协议（Model Context Protocol, MCP）是一个开放协议，为大模型和外部工具之间的信息传递提供通道。作为云上托管MCP服务的最佳运行时，函数计算 FC为支持为MCP服务提供弹性调用能力。您可以通过函数计算Function AI内置的MCP服务模板快速体验部署MCP服务。

## **为什么推荐在函数计算开发和托管MCP服务？**

函数计算作为Serverless计算服务，具有弹性伸缩、细粒度资源规格等优势，可按请求分配资源和计费。在轻量化业务场景下，帮助业务自如应对不确定性流量带来的挑战。

MCP服务托管作为云上公共服务，在AI场景下势必会面临流量不确定性问题，函数计算通过技术创新，确保长连接保持与按请求计费兼容，平衡无状态弹性与亲和性调度，在满足 [MCP SSE亲和性调度](https://help.aliyun.com/zh/functioncompute/fc/user-guide/mcp-sse-affinity "") 的基础上，结合无状态计算弹性能力，让业务在面对不确定流量的时候，快速实现MCP服务的弹性扩容。

## **计费说明**

- MCP服务托管到函数计算后，根据使用的弹性资源按量计费。无请求时不计费，请求期间按照请求次数和资源使用量进行 [计费](https://help.aliyun.com/zh/functioncompute/fc/product-overview/billing-overview-of-fc "")。

- 如果您在函数计算创建的MCP服务需要接入阿里云百炼，则会产生百炼侧的 [调用费用或部署费用](https://help.aliyun.com/zh/model-studio/mcp-introduction#fb482455a3u8c "")。


## **创建MCP服务**

函数计算提供支持SSE协议且具备并发能力的MCP运行时，存量STDIO模式的MCP服务无需任何改动即可转换为符合SSE协议的远端服务。

您可以通过Function AI创建 [开发MCP服务](https://help.aliyun.com/zh/functioncompute/mcp-server "")，创建的函数将自带MCP SSE亲和调度能力。

## **使用MCP服务**

在函数计算中创建MCP服务后，您可以通过在 [阿里云百炼控制台](https://bailian.console.aliyun.com/) 部署 [自定义 MCP 服务](https://help.aliyun.com/zh/model-studio/custom-mcp "") 将您的MCP服务注册到百炼，然后 [在智能体或工作流中配置 MCP 服务](https://help.aliyun.com/zh/model-studio/official-and-third-party-mcp#8319d03864jym "")。

阿里云百炼智能体和工作流应用已支持MCP服务：

- 智能体应用

可以接入多个MCP服务，每个MCP服务中包含一组工具。在一轮对话中，智能体会调用一个或多个工具。

- 工作流应用

可以接入MCP服务提供的单个工具，作为一个 MCP 节点。