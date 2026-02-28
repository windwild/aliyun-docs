### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[日志数据采集（Log）](https://help.aliyun.com/zh/sls/sls-log-collection/)[云产品日志采集](https://help.aliyun.com/zh/sls/collection-of-alibaba-cloud-service-logs/)[函数计算执行日志](https://help.aliyun.com/zh/sls/function-compute-execution-logs/)[函数计算（2.0）](https://help.aliyun.com/zh/sls/function-compute-2-0/)日志字段详情

# 日志字段详情

更新时间：2024-06-05 02:48:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：开通日志功能](https://help.aliyun.com/zh/sls/enable-the-logging-feature)[下一篇：开通日志功能](https://help.aliyun.com/zh/sls/enable-the-log-function-in-the-function-compute-3-0-console)

该文章对您有帮助吗？

反馈

本文介绍函数计算（2.0）执行日志的字段详情。

| **指标名称** | **描述** | **示例值** | **是否每次调用都会记录** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **指标名称** | **描述** | **示例值** | **是否每次调用都会记录** |
| serviceName | 服务名称。 | my-service | 是 |
| functionName | 函数名称。 | my-function | 是 |
| versionId | 版本名称。 | 12 | 是 |
| qualifier | 服务别名。默认为LATEST。 | prod | 是 |
| requestId | 请求ID。 | db72ce53-ccbe-4216-af55-642622e01494 | 是 |
| operation | 操作名称。 | InvokeFunction | 是 |
| invocationType | 调用类型，包含以下两种。<br>Sync：同步调用<br>Async：异步调用 | Sync | 是 |
| memoryMB | 函数的内存上限。 | 512 | 是 |
| memoryUsageMB | 函数执行消耗的内存。 | 410 | 是 |
| durationMs | 请求执行时间。 | 20.20 | 是 |
| isColdStart | 是否为冷启动。<br>**说明**<br>当请求抵达函数计算时，函数计算系统没有已经启动的函数实例执行请求，需要重新创建实例、下载代码、启动执行环境。<br>请求生命周期内经历了完整的创建实例、下载代码、启动执行环境过程的请求我们称之为冷启动请求。<br>函数计算平台对冷启动做了很多优化，为避免冷启动，平台会提前创建实例，请求抵达函数计算平台后创建实例过程中，可能会等到一个已经创建好的实例，这种请求我们不称之为冷启动请求。 | false | 是 |
| instanceEvent | 实例事件。目前只有ColdStart，在冷启动请求时记录。 | ColdStart | 否 |
| hasFunctionError | 函数执行是否出现函数错误。 | false | 是 |
| errorType | 函数错误类型，包含以下三种：<br>- FunctionOOMError：内存溢出。<br>  <br>- FunctionTimeoutError：执行时间超限。<br>  <br>- FunctionUnhandledError：未捕获的其他异常。 | FunctionUnhandledError | 否。仅在函数执行出现错误即`hasFunctionError:true`时记录。 |
| invokeFunctionLatencyMs | 初始化函数执行时间。 | 99.00 | 否。仅当发生冷启动且配置初始化函数时记录。 |
| traceContext | 链路追踪上下文信息。 | 371d3ff242fcee9:371d3ff242fcee9:0:1 | 否。仅当配置链路追踪时记录。 |
| isSampled | 请求是否被链路追踪采样。 | true | 否。仅当配置链路追踪时记录。 |
| resourceMode | 执行请求的实例类型。取值如下：<br>- OnDemand：表示按量实例。<br>  <br>- Provision：表示预留实例。 | OnDemand | 是 |
| instanceID | 实例ID。 | c-65603d8c-37e1bf7123054a77\*\*\*\* | 是 |
| hostname | 实例Host。 | c-65603d8c-37e1bf7123054a77\*\*\*\* | 是 |
| ipAddress | 实例IP地址。<br>说明：此IP为实例内部IP，用于区分不同实例，不是实例公网IP地址。 | 21.0.XX.XX | 是 |
| activeInstances | 活跃实例数。 | 1 | 是 |
| activeInstancesPerFunction | 当前函数活跃实例数。 | 1 | 是 |
| scheduleLatencyMs | 调度耗时。请求冷启动时，调度延时相对比较长。 | 10.07 | 是 |
| coldStartStartTimestamp | 冷启动开始时间戳。 | 1700806029167 | 否。仅当发生冷启动时有记录。 |
| coldStartLatencyMs | 冷启动耗时。 | 487.65 | 否。仅当发生冷启动时有记录。 |
| prepareCodeStartTimestamp | 下载代码开始时间戳。13位时间戳，精确到毫秒。 | 1700806029167 | 否。仅当发生冷启动时有记录。 |
| prepareCodeLatencyMs | 下载代码耗时。 | 0.18 | 否。仅当发生冷启动时有记录。 |
| runtimeInitializationStartTimestamp | 运行时初始化开始时间戳。 | 1700806029168 | 否。仅当发生冷启动时有记录。 |
| runtimeInitializationMs | 运行时初始化耗时。 | 487.37 | 否。仅当发生冷启动时有记录。 |
| asyncAttemptStartTimestamp | 异步调用函数执行失败默认重试3次<br>此参数为第${retryCount}次重试的开始时间戳。 | 1700806028084 | 否。仅当异步调用时有记录。 |
| asyncAttemptLatencyMs | 异步调用函数执行失败默认重试3次<br>此参数为第${retryCount}次重试的开始时间戳。 | 1688.74 | 否。仅当异步调用时有记录。 |
| asyncMode | 异步调用模式。取值说明如下：<br>- Stateless：无状态异步调用<br>  <br>- Stateful：有状态异步调用 | Stateful | 否。仅当异步调用时有记录。 |
| retryCount | 重试次数。 | 0 | 否。仅当异步调用时有记录。 |