### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[MCP](https://help.aliyun.com/zh/model-studio/model-context-protocol/)MCP 简介

# 模型上下文协议（MCP）

更新时间：2026-02-11 02:03:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

MCP 服务接入示例

如何使用 MCP

计费说明

云部署 MCP 服务

自定义部署 MCP 服务

模型上下文协议（Model Context Protocol, MCP）旨在搭建大模型和外部工具之间的信息传递通道。通过 MCP 协议，开发者不用为每个外部工具编写复杂的接口，阿里云百炼应用也能够接入海量第三方工具。

## MCP 服务接入示例

| **路径规划智能体** | **网页爬取工作流** |
| --- | --- |

|     |     |
| --- | --- |
| **路径规划智能体** | **网页爬取工作流** |
| - 大模型应用：智能体应用<br>  <br>- 外部工具：Amap Maps MCP 服务提供地理信息获取能力 | - 大模型应用：工作流应用<br>  <br>- 外部工具：Firecrawl MCP 服务提供网页爬取能力 |
| ![2025-04-08_14-07-26 (1)](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2024314471/p938865.gif) | ![2025-04-08_14-36-09 (2)](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2024314471/p939258.gif) |

## **如何使用 MCP**

现在，阿里云百炼智能体和工作流应用已支持接入两种 MCP 服务。使用 MCP 服务的详细方法，请参考 [官方 MCP 服务](https://help.aliyun.com/zh/model-studio/official-and-third-party-mcp "") 和 [自定义MCP服务](https://help.aliyun.com/zh/model-studio/custom-mcp "")。

- 官方 MCP 服务：阿里云百炼官方部署了多种 MCP 服务，方便您快速接入阿里云百炼应用。

- 自定义 MCP 服务：阿里云百炼还支持部署自定义 MCP 服务。您可以在 MCP 市场或互联网上搜寻 MCP 服务，以自定义 MCP 服务的形式部署在阿里云百炼上。


![bailian_map](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2024314471/p939005.svg)

## **计费说明**

### **云部署 MCP 服务**

- **部署费用**：限时免部署费用。

- **调用费用**：部分 MCP 服务涉及第三方 API 调用，使用后可能会产生费用。这部分费用由第三方收取，阿里云百炼不收取费用。


### 自定义部署 MCP 服务

根据服务的响应速度，百炼提供以下两种计费模式：

- **基础模式：**

  - **无部署费用。无调用时不计费，有调用时按调用时长计费。**

    - **调用费率**：0.000156 元/秒
  - **适用场景**：偶尔调用，对启动速度要求不高（首次调用会有一定启动延迟）
- **极速模式**：

  - **有部署费用。无调用时按部署时长计费，有调用时另按调用时长计费。**

    - **调用费率：** 0.000156 元/秒

    - **部署费率：** 0.000036 元/秒
  - **适用场景**：可减少频繁启动服务带来的延迟，适合需要长时间保持在线，且调用较频繁的场景。