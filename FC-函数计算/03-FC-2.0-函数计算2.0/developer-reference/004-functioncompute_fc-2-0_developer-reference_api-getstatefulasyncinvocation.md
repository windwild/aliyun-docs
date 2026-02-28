### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[函数异步调用](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/asynchronous-invocation-1/)GetStatefulAsyncInvocation

# GetStatefulAsyncInvocation

更新时间：2025-08-20 04:26:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ListFunctionAsyncInvokeConfigs](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-listfunctionasyncinvokeconfigs)[下一篇：ListStatefulAsyncInvocations](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-liststatefulasyncinvocations)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

请求头

请求语法

请求参数

返回数据

示例

错误码

调用GetStatefulAsyncInvocation接口获取符合条件的异步任务记录。

StatefulAsyncInvocation：异步任务。异步任务在普通的异步调用基础上增加了状态管理的功能，更适用于各类任务场景。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=GetStatefulAsyncInvocation&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口无特殊请求头，关于公共请求头信息，请参见 [公共参数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/common-parameters)。

## 请求语法

```plaintext
GET /services/{serviceName[.qualifier]}/functions/{functionName}/stateful-async-invocations/{statefulAsyncInvocationId} HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 异步任务所属的服务的名称。 |
| functionName | String | Path | 是 | function\_name | 异步任务所属的函数的名称。 |
| qualifier | String | Path | 否 | alias | 异步任务所属的服务的别名或版本。 |
| statefulAsyncInvocationId | String | Path | 是 | e026ae92-61e5-472f-b32d-1c9e3c4e\*\*\*\* | 异步任务的ID。<br>**说明**<br>建议您在使用SDK调用时设置与业务相关的ID，方便对相关执行进行后续操作。例如，一个视频处理函数可以使用视频文件名作为调用ID，通过该ID可以查看视频是否处理完成或终止视频的处理。该ID的命名规则只能以英文大小写字母或下划线（\_）开头，由英文大小写字母、数字（0-9）、下划线（\_）及短划线（-）组成，不超过128个字符。如果您未设置异步调用的ID时，系统则会自动生成一个ID。 |

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| startedTime | Long | 2020-08-20T02:28:21Z | 异步任务的开始时间。 |
| endTime | Long | 2020-08-20T02:38:21Z | 异步任务的结束时间。 |
| functionName | String | function\_name | 异步任务所属的函数名称。 |
| qualifier | String | alias | 异步任务所属的服务的别名或版本。 |
| serviceName | String | service\_name | 异步任务所属的服务名称。 |
| invocationId | String | e026ae92-61e5-472f-b32d-1c9e3c4e\*\*\*\* | 异步任务的任务ID。 |
| requestId | String | 403fcbd6-ec41-401f-9fa7-386f3d3d\*\*\*\* | 异步任务的请求ID。 |
| status | String | Succeeded | 异步任务的执行状态。<br>- **Enqueued**：异步消息已入队，等待处理。<br>- **Dequeued**：异步消息已出队，等待触发。<br>- **Running**：调用执行中。<br>- **Succeeded**：调用执行成功。<br>- **Failed**：调用执行失败。<br>- **Stopped**：调用执行终止。<br>- **Stopping**：执行停止中。<br>- **Expired**：您给异步消息配置了存活有效期，该消息因过期已被丢弃（未触发）。<br>- **Invalid**：您的执行因函数被删除等原因处于无效状态（未触发）。<br>- **Retrying**：异步调用因执行错误重试中。 |
| destinationStatus | String | Succeeded | 本次异步任务的目的状态。 |
| invocationErrorMessage | String | UnhandledException | 异步任务调用失败的错误消息。 |
| InvocationPayload | String | hello world | 异步任务调用的输入。 |
| alreadyRetriedTimes | Long | 3 | 本次异步任务失败后的最大重试次数，默认值为3。取值范围\[0,8\]。 |

## 示例

请求示例

```plaintext
GET /2016-08-15/services/{serviceName[.qualifier]}/functions/function_name/stateful-async-invocations/e026ae92-61e5-472f-b32d-1c9e3c4e**** HTTP/1.1
公共请求头
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
Content-Type:application/json

{
  "functionName" : "function_name",
  "qualifier" : "alias",
  "serviceName" : "service_name",
  "invocationId" : "e026ae92-61e5-472f-b32d-1c9e3c4e****",
  "requestId" : "403fcbd6-ec41-401f-9fa7-386f3d3d****",
  "status" : "Succeeded",
  "destinationStatus" : "Succeeded",
  "invocationErrorMessage" : "UnhandledException",
  "InvocationPayload" : "function_name",
  "alreadyRetriedTimes" : 3
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。