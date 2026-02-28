### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[函数运维](https://help.aliyun.com/zh/functioncompute/fc/user-guide/function-o-m/)[监控报警](https://help.aliyun.com/zh/functioncompute/fc/user-guide/monitoring-and-alerting/)[日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging-1/)打印函数日志

# 打印函数日志

更新时间：2024-01-10 03:38:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：请求级别指标日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/request-level-metric-logs)[下一篇：实例命令行操作](https://help.aliyun.com/zh/functioncompute/fc/user-guide/instance-command-line-operations)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

日志格式

不同运行时记录日志

如您需要调试和验证您的代码是否正常工作，可以使用编程语言的标准日志记录功能输出日志。函数计算运行时会将函数输出到STDOUT和STDERR的日志上传至您配置的logstore中，日志主题为functionName，您可以通过`__topic__: "FCLogs:functionName"`搜索当前函数的日志。

## **日志格式**

建议您打印的日志中包含请求ID，方便日后诊断问题。推荐日志格式为`$utcdatetime(yyyy-MM-ddTHH:mm:ss.fff) $requestId [$Level] $message`，例如`2023-10-23 15:43:19 1-65362416-68afb557d64a2e283eccebce [info] hello world`。函数计算支持的运行时中使用`context.getLogger()`记录的日志都使用以上格式。

## **不同运行时记录日志**

关于不同编程语言日志打印相关内容，请参见以下文档：

- [Node.js运行环境记录日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging "")

- [Python运行环境记录日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging-2 "")

- [PHP运行环境记录日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging-3 "")

- [Java运行环境记录日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-1-1 "")

- [C#运行环境记录日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-1-2 "")

- [Golang运行环境记录日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-2-1 "")

- [Custom Runtime日志格式](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-and-log-format-1#section-s6s-3fu-cwl "")