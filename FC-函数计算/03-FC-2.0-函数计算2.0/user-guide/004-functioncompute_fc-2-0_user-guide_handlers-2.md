### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/programming-languages/)[Python](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/python-1/)请求处理程序（Handler）

# 请求处理程序（Handler）

更新时间：2025-08-04 01:22:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：环境说明](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/overview)[下一篇：事件请求处理程序（Event Handler）](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/event-handlers)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

什么是请求处理程序

配置说明

更多信息

本文介绍在函数计算中使用Python运行时开发请求处理程序的相关概念和方法。

## 什么是请求处理程序

FC函数的请求处理程序，是函数代码中处理请求的方法。当您的FC函数被调用时，函数计算会运行您提供的Handler方法处理请求。您可以通过 [函数计算控制台](https://fcnext.console.aliyun.com/) 的 **请求处理程序（函数入口）** 配置Handler。

对Python语言的FC函数而言，您的请求处理程序格式为`文件名.方法名`。例如，您的文件名为`main.py`，方法名为`handler`，则请求处理程序为`main.handler`。

关于FC函数的具体定义和相关操作，请参见 [管理函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions#multiTask3514 "")。

## 配置说明

请求处理程序的具体配置均需符合函数计算平台的配置规范。配置规范因请求处理程序类型而异。

请求处理程序分为事件请求处理程序（Event Handler）和HTTP请求处理程序（HTTP Handler）。其中事件请求由各种事件源触发生成，HTTP请求则由HTTP触发器触发生成。两种请求处理程序的详细解释，请参见 [请求处理程序类型](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/overview-30#concept-2260120 "")。

请求处理程序的具体配置示例，请分别参见 [事件请求处理程序（Event Handler）](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/event-handlers#multiTask701 "") 和 [HTTP请求处理程序（HTTP Handler）](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/http-handlers-1#multiTask9351 "")。

## 更多信息

如何将您的代码包部署至函数计算平台，请参见 [部署代码包](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/deploy-a-code-package-1#task-2203155 "")。