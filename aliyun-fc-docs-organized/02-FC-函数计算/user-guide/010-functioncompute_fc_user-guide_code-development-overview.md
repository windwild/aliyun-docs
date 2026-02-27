### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[开发与执行环境](https://help.aliyun.com/zh/functioncompute/fc/user-guide/development-and-execution-environment/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc/user-guide/code-development/)代码开发概述

# 代码开发概述

更新时间：2025-06-20 02:48:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：LLM推理模型服务指标监控集成方案](https://help.aliyun.com/zh/functioncompute/fc/user-guide/integrating-prometheus-metric-monitoring-for-llm-inference-service-in-function-compute)[下一篇：基础信息](https://help.aliyun.com/zh/functioncompute/fc/user-guide/basics)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

函数计算运行时

自定义运行时

自定义镜像

本文列举函数计算支持的多语言运行时信息。

## 背景信息

运行时提供针对不同语言在执行环境中运行的环境。运行时作为函数计算和您的函数之间的接力员，传递函数调用的事件（event）、上下文信息（context）和响应。您可以使用函数计算提供的运行时或构建您自己的运行时，还可以自行构建容器镜像。

## 函数计算运行时

Node.js

Python

PHP

Java

C#

Go

- [环境说明](https://help.aliyun.com/zh/functioncompute/fc-3-0/user-guide/runtime-overview-1 "")

- [请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc/user-guide/request-handlers "")

- [上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-1-1 "")

- [部署代码包](https://help.aliyun.com/zh/functioncompute/fc/user-guide/deploy-a-code-package "")

- [日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging "")

- [错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-nodejs "")

- [函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances "")


- [环境说明](https://help.aliyun.com/zh/functioncompute/fc-3-0/user-guide/runtime-overview-2 "")

- [请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc/user-guide/event-handlers-1-1 "")

- [上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-1 "")

- [部署代码包](https://help.aliyun.com/zh/functioncompute/fc/user-guide/deploy-a-code-package-1 "")

- [日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging-2 "")

- [错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-1-1 "")

- [函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-1 "")


- [环境说明](https://help.aliyun.com/zh/functioncompute/fc-3-0/user-guide/overview-php "")

- [请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc/user-guide/handlers-in-a-php-runtime "")

- [上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-2-1 "")

- [部署代码包](https://help.aliyun.com/zh/functioncompute/fc/user-guide/deploy-a-code-package-in-a-php-runtime "")

- [日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging-3 "")

- [错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-3-1 "")

- [函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-2 "")


- [环境说明](https://help.aliyun.com/zh/functioncompute/runtime-overview-3 "")

- [请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc/user-guide/handlers-in-a-java-runtime "")

- [上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-3-1 "")

- [编译部署代码包](https://help.aliyun.com/zh/functioncompute/fc/user-guide/compile-and-deploy-code-packages "")

- [日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-1-1 "")

- [错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-2-1 "")

- [函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-4-1 "")


- [环境说明](https://help.aliyun.com/zh/functioncompute/overview-31 "")

- [请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc/user-guide/handlers-in-a-c-runtime "")

- [上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-4 "")

- [编译部署代码包](https://help.aliyun.com/zh/functioncompute/fc/user-guide/compile-and-deploy-code-packages-1-2 "")

- [日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-1-2 "")

- [错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-in-c "")

- [函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-5 "")


- [环境说明](https://help.aliyun.com/zh/functioncompute/fc-3-0/user-guide/overview-of-runtimes-1 "")

- [请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc/user-guide/handlers-in-a-go-runtime "")

- [上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-5 "")

- [编译部署代码包](https://help.aliyun.com/zh/functioncompute/fc/user-guide/compile-and-deploy-code-packages-in-a-go-runtime "")

- [日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-2-1 "")

- [错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-4-1 "")

- [函数实例生命周期回调](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-7 "")


## 自定义运行时

以下为多语言使用示例。更多信息，请参见 [环境说明](https://help.aliyun.com/zh/functioncompute/fc-3-0/user-guide/overview-10-2 "")。

- [Node.js示例](https://gitee.com/devsapp/start-fc/tree/V3/custom/nodejs)

- [Python示例](https://gitee.com/devsapp/start-fc/tree/V3/custom/python)

- [Java示例](https://gitee.com/devsapp/start-fc/tree/V3/custom/java)

- [Go示例](https://gitee.com/devsapp/start-fc/tree/V3/custom/golang)


## 自定义镜像

以下为多语言使用示例。更多信息，请参见 [自定义镜像简介](https://help.aliyun.com/zh/functioncompute/fc-3-0/user-guide/overview-of-customcontainer "")。

- [Node.js示例](https://gitee.com/devsapp/start-fc/tree/V3/custom-container/nodejs)

- [Python示例](https://gitee.com/devsapp/start-fc/tree/V3/custom-container/python)

- [Java示例](https://gitee.com/devsapp/start-fc/tree/V3/custom-container/java)

- [Go示例](https://gitee.com/devsapp/start-fc/tree/V3/custom-container/golang)