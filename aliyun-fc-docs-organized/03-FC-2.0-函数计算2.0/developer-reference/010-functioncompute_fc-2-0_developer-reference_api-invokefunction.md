### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/) [函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/) [开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/) [API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/) [API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/) [函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/function/) InvokeFunction

# InvokeFunction

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ListFunctions](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-listfunctions)[下一篇：触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/trigger/)

该文章对您有帮助吗？

反馈

调用InvokeFunction接口执行函数。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=InvokeFunction&type=ROA&version=2021-06-22)

## 请求头

该接口无特殊请求头，关于公共请求头信息，请参见 [公共参数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/common-parameters)。

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例** | **描述** |
| X-Fc-Invocation-Type | String | 否 | Sync | 调用方式。取值说明如下：<br>- **Sync**：同步调用。<br>- **Async**：异步调用。 |
| X-Fc-Log-Type | String | 否 | None | 请求返回日志。<br>- **Tail**：返回当前请求产生的最后4 KB日志。<br>- **None**：默认值，不返回请求日志。 |
| X-Fc-Stateful-Async-Invocation-Id | String | 否 | g6u\*\*\*\*\*iyvhd3jk8s6bhj0hh | 异步任务ID。您需要事先开启异步任务。<br>**说明** 建议您在使用SDK调用时设置与业务相关的ID，方便对相关执行进行后续操作。例如，一个视频处理函数可以使用视频文件名作为调用ID，通过该ID可以查看视频是否处理完成或终止视频的处理。该ID的命名规则只能以英文大小写字母或下划线（\_）开头，由英文大小写字母、数字（0-9）、下划线（\_）及短划线（-）组成，不超过128个字符。如果您未设置异步调用的ID，系统则会自动生成一个ID。 |

## 请求语法

```plaintext
POST /services/{serviceName.qualifier}/functions/{functionName} HTTP/1.1
```

## 请求参数

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 服务的名称。 |
| qualifier | String | Path | 否 | LATEST | 服务的版本或别名。 |
| functionName | String | Path | 是 | function\_name | 函数的名称。 |
|  | String | Body | 是 | {"key1": "value1"} | 函数的事件，类型为二进制Byte数组。函数计算将Event传递给用户函数处理。 |

## 返回数据

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| X-Fc-Error-Type | String | UnhandledInvocationError | 调用函数的错误类型。 <br>- **HandledInvocationError**：只有在Node.js中通过`callback`返回的错误是`HandledInvocationError`。更多信息，请参见 [错误处理](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。<br>- **UnhandledInvocationError**：除了`HandledInvocationError`，其余的错误都是`UnhandledInvocationError`。更多信息，请参见 [错误处理](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。 |
| X-Fc-Log-Result | String | demo log result | 返回日志结果。 |
| X-Fc-Code-Checksum | String | 5697641582914695457 | 函数代码包的CRC-64值。 |
| X-Fc-Stateful-Async-Invocation-Id | String | g6u\*\*\*\*\*iyvhd3jk8s6bhj0hh | 异步任务ID。您需要事先开启异步任务。<br>**说明** 建议您在使用SDK调用时设置与业务相关的ID，方便对相关执行进行后续操作。例如，一个视频处理函数可以使用视频文件名作为调用ID，通过该ID可以查看视频是否处理完成或终止视频的处理。该ID的命名规则只能以英文大小写字母或下划线（\_）开头，由英文大小写字母、数字（0-9）、下划线（\_）及短划线（-）组成，不超过128个字符。如果您未设置异步调用的ID时，系统则会自动生成一个ID。 |
| X-Fc-Instance-Id | String | 7c43576b-48b1-4c3a-86e5-dcb01872\*\*\*\* | 函数实例的ID。 |
| X-Fc-Request-Id | String | dab25e58-9356-4e3f-97d6-f044c4\*\*\*\* | 函数调用的请求ID。 |
| X-Fc-Max-Memory-Usage | String | 9.2 | 函数执行消耗的内存，单位MB。 |
| X-Fc-Invocation-Duration | String | 10 | 函数执行消耗的时长，单位毫秒。 |
| X-Fc-Invocation-Service-Version | String | LATEST | 调用函数的版本或者别名。 |
|  | String | hello world | 调取函数返回的结果，函数具体的返回内容由您定义。 |

## 示例

请求示例

```plaintext
POST /services/{serviceName.qualifier}/functions/function_name HTTP/1.1
Host:fc-ram.aliyuncs.com
X-Fc-Invocation-Type:Sync
X-Fc-Log-Type:None
X-Fc-Stateful-Async-Invocation-Id:g6u*****iyvhd3jk8s6bhj0hh
Content-Type:application/json

{"key1": "value1"}
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
Content-Type:application/json

{
  "result" : "hello world"
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。