### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[函数异步调用](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/asynchronous-invocation-1/)PutFunctionAsyncInvokeConfig

# PutFunctionAsyncInvokeConfig

更新时间：2025-08-20 04:25:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetResourceTags](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getresourcetags)[下一篇：DeleteFunctionAsyncInvokeConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-deletefunctionasyncinvokeconfig)

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

调用PutFunctionAsyncInvokeConfig接口创建或更新函数的异步调用配置。


函数会根据异步调用配置是否存在，在调用PutFunctionAsyncInvokeConfig接口时创建或更新相关配置信息。

- 如果函数的异步调用配置不存在，调用PutFunctionAsyncInvokeConfig接口则会创建相应配置。
- 如果函数的异步调用配置已存在，调用PutFunctionAsyncInvokeConfig接口则会更新本次调用时新传递的内容，未指定的内容将保持不变。

配置中的StatefulAsyncInvocation即为异步任务的配置项。异步任务在普通的异步调用基础上增加了状态管理的功能，更适用于各类任务场景。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=PutFunctionAsyncInvokeConfig&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口无特殊请求头，关于公共请求头信息，请参见 [公共参数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/common-parameters)。

## 请求语法

```http
PUT /services/{serviceName[.qualifier]}/functions/{functionName}/async-invoke-config HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 异步调用配置所属的服务的名称。 |
| functionName | String | Path | 是 | testHelloWorld | 异步调用配置所属的函数的名称。 |
| qualifier | String | Path | 否 | alias | 异步调用配置所属的服务的别名或版本。 |
|  | Object | Body | 否 |  | 异步调用配置。 |
| destinationConfig | [DestinationConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#DestinationConfig "") | Body | 否 |  | 异步调用目标的配置结构体。 |
| maxAsyncEventAgeInSeconds | Long | Body | 否 | 300 | 消息最大存活时长，取值范围\[1,604800\]，默认为86400，单位为秒。 |
| maxAsyncRetryAttempts | Long | Body | 否 | 3 | 异步调用失败后的最大重试次数，默认值为3。取值范围\[0,8\]。 |
| statefulInvocation | Boolean | Body | 否 | true | 是否开启异步任务。<br>- **true**：表示已开启异步任务。<br>- **false**：表示未开启异步任务。 |

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| createdTime | String | 2020-08-20T02:28:21Z | 服务的创建时间。 |
| destinationConfig | [DestinationConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#DestinationConfig "") |  | 异步调用目标的配置结构体。 |
| functionName | String | testHelloWorld | 异步调用配置所属的函数的名称。 |
| lastModifiedTime | String | 2020-09-10T02:45:02Z | 异步调用配置的最后更改时间。 |
| maxAsyncEventAgeInSeconds | Long | 1 | 消息最大存活时长，取值范围\[1,2592000\]。单位：秒。 |
| maxAsyncRetryAttempts | Long | 1 | 异步调用失败后的最大重试次数，默认值为3。取值范围\[0,8\]。 |
| qualifier | String | alias | 异步调用配置所属的服务的别名或版本。 |
| serviceName | String | service\_name | 异步调用配置所属的服务的名称。 |
| statefulInvocation | Boolean | true | 是否开启异步任务。<br>- **true**：表示已开启异步任务。<br>- **false**：表示未开启异步任务。 |

## 示例

请求示例

```swift
PUT /2016-08-15/services/service_name.alias/functions/testHelloWorld/async-invoke-config HTTP/1.1
公共请求头

{
  "destinationConfig" : {
    "onFailure" : {
      "destination" : "acs:mns:cn-shanghai:1986***743:/queues/failure/messages"
    },
    "onSuccess" : {
      "destination" : "acs:mns:cn-shanghai:1986***743:/queues/success/messages"
    }
  },
  "maxAsyncEventAgeInSeconds" : 300,
  "maxAsyncRetryAttempts" : 3,
  "statefulInvocation" : true
}
```

正常返回示例

`JSON`格式

```ruby
HTTP/1.1 200 OK
Content-Type:application/json

{
  "createdTime" : "2020-08-20T02:28:21Z",
  "destinationConfig" : {
    "onFailure" : {
      "destination" : "acs:mns:cn-shanghai:1986***743:/queues/failure/messages"
    },
    "onSuccess" : {
      "destination" : "acs:mns:cn-shanghai:1986***743:/queues/success/messages"
    }
  },
  "functionName" : "testHelloWorld",
  "lastModifiedTime" : "2020-09-10T02:45:02Z",
  "maxAsyncEventAgeInSeconds" : 1,
  "maxAsyncRetryAttempts" : 1,
  "qualifier" : "alias",
  "serviceName" : "service_name",
  "statefulInvocation" : true
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。