### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[开发与执行环境](https://help.aliyun.com/zh/functioncompute/fc/user-guide/development-and-execution-environment/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc/user-guide/code-development/)Java

# Java

更新时间：2025-02-25 05:10:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

Java运行时

相关文档

本文介绍在函数计算中使用Java框架编写函数的运行环境信息。

## 背景信息

Java语言和Python、Node.js这类脚本型语言不同，该语言需要编译后才能在JVM虚拟机中运行。针对Java语言，函数计算当前具有以下限制：

- 不支持代码编译：仅支持上传已经开发完成、编译打包后的ZIP包或JAR包。函数计算不提供Java的编译能力。

- 不支持在线编辑：由于不支持上传代码，所以不支持在线编辑代码，仅支持通过 **上传 JAR 包** 或 **通过 OSS 上传** 两种方法提交代码。


## Java运行时

函数计算目前支持的Java运行环境如下。

| **版本** | **操作系统** | **架构** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **版本** | **操作系统** | **架构** |
| Java 11 | Linux | x86\_64 |
| Java 8 | Linux | x86\_64 |

函数计算为Java运行时提供以下依赖库：

- `com.aliyun:fc-java-core`：定义了请求处理程序中使用的handler接口和context对象等信息。

- `com.aliyun:fc-java-events`：提供了常用的事件源的event类型。

- `FC SDK for Java`：函数计算官方的Java SDK。


## 相关文档

- [请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc/user-guide/handlers-in-a-java-runtime "")

- [上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-3-1 "")

- [编译部署代码包](https://help.aliyun.com/zh/functioncompute/fc/user-guide/compile-and-deploy-code-packages "")

- [日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-1-1 "")

- [错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-2-1 "")

- [函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-4-1 "")