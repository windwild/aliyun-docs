### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[应用中心](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/serverless-application-center/)[流水线](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/pipelines/)流水线简介

# 流水线简介

更新时间：2025-09-10 05:27:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：管理环境](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-the-environment-of-an-application)[下一篇：相关概念](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/terms-2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

使用限制

应用场景

DevOps

UIOps

平台集成

费用说明

Serverless应用中心依托Serverless产品，为所有用户和平台提供平滑易用、灵活、易集成的流水线编辑以及执行能力，帮助用户在Serverless场景以及其他场景下，实现应用的持续集成和持续交付（CI/CD）。

## 功能介绍

与开源产品GitHub Actions类似，Serverless应用中心的流水线提供了两层业务模型的抽象，流水线（Pipeline）和任务（Task）。

- 流水线是一个流程描述对象，它描述了流水线的执行上下文和从属于流水线的任务之间的依赖关系。

- 任务是一个具体的执行描述对象，它描述了任务应该如何被执行。


通过流水线与任务模型，用户可以编排一个符合自身预期的CI/CD流程。应用中心根据流水线与任务模型，在特定的事件下自动或手动执行。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9246947571/CAEQYBiBgID4vfOB2xgiIDJjZDhlNWJhNWU0YTQwODE4MTM4NzM5M2NiNWQ3NWE13963382_20230830144006.372.svg)

## 使用限制

- 应用中心流水线严格遵守阿里云RAM授权认证标准，因此，只能为阿里云用户的CI/CD需求提供服务。

- 应用中心的流水线任务，运行在阿里云函数计算产品下，因此，构建能力无法与虚拟机、物理机完全保持一致。


## 应用场景

### DevOps

应用中心流水线产品能力将依托DevOps理念持续发展，坚持帮助用户以低成本、自动化、代码化的方式自定义专属流水线。

### UIOps

应用中心流水线产品能力面向传统运维人员或管理员Ops场景，提供流水线、任务编辑的控制台界面，内置并不断丰富开箱即用的任务模板以及流水线模板，以积木搭建的体验甚至是成品购买的体验，为用户提供流水线编辑与执行的能力。

### 平台集成

应用中心流水线通过开放OpenAPI，开源生态，提供被集成的能力，同时支持为非Serverless、非应用中心的用户提供流水线能力。

## 费用说明

应用中心流水线默认采用多租账号模式，即由阿里云函数计算为您承担流水线执行过程中的费用成本。此流水线模式可以满足绝大部分场景，但是您无法自定义您的流水线环境，也无法通过VPC触发流水线执行。流水线中的任务同样支持运行在用户的账户下，以解决用户自定义构建函数的配置与环境等需求。关于配置用户账号的流水线，即自定义流水线的说明，请参见 [管理流水线](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-pipelines#section-h06-tzn-b0z "")。

运行在用户账户下的流水线任务被触发后，将会产生相关资源使用费用。更多信息，请参见 [计费概述](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/billing-overview#concept-2557114 "")。