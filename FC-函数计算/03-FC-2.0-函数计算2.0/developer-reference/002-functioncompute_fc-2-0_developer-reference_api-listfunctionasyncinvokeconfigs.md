### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[函数异步调用](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/asynchronous-invocation-1/)ListFunctionAsyncInvokeConfigs

# ListFunctionAsyncInvokeConfigs

更新时间：2025-08-20 04:26:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetFunctionAsyncInvokeConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getfunctionasyncinvokeconfig)[下一篇：GetStatefulAsyncInvocation](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getstatefulasyncinvocation)

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

调用ListFunctionAsyncInvokeConfigs接口查询一个服务下某个函数的所有异步配置。当配置个数超过Limit个数时，将返回NextToken参数。可以使用该参数进行后续的分页查询。


配置中的StatefulAsyncInvocation即为异步任务的配置项。当StatefulAsyncInvocation取值为true时，代表您已开启异步任务，所有的异步调用将变为异步任务模式。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=ListFunctionAsyncInvokeConfigs&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口无特殊请求头，关于公共请求头信息，请参见 [公共参数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/common-parameters)。

## 请求语法

```http
GET /services/{serviceName}/functions/{functionName}/async-invoke-configs HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 异步调用配置所属的服务的名称。 |
| functionName | String | Path | 是 | testHelloWorld | 异步调用配置所属的函数的名称。 |
| limit | Integer | Query | 否 | 20 | 限定此次返回资源的数量。如果不设定，默认返回20，最大不能超过100。返回结果可以小于指定的数量，但不会多于指定的数量。 |
| nextToken | String | Query | 否 | caeba0be03\*\*\*\*f84eb48b699f0a4883 | 用来返回更多结果。第一次查询不需要提供这个参数，后续查询所需使用的Token，从返回结果中获取。 |

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| configs | Array |  | 配置列表。 |
| createdTime | String | 2020-08-20T02:28:21Z | 异步调用配置的创建时间。 |
| destinationConfig | [DestinationConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#DestinationConfig "") |  | 异步调用目标的配置结构体。 |
| functionName | String | testHelloWorld | 异步调用配置所属的函数的名称。 |
| lastModifiedTime | String | 2020-09-10T02:45:02Z | 异步调用配置的最后更改时间。 |
| maxAsyncEventAgeInSeconds | Long | 1 | 消息最大存活时长，取值范围\[1,604800\]，默认为86400，单位为秒。 |
| maxAsyncRetryAttempts | Long | 1 | 异步调用失败后的最大重试次数，默认值为3。取值范围\[0,8\]。 |
| qualifier | String | alias | 异步调用配置所属的服务的别名或版本。 |
| serviceName | String | service\_name | 异步调用配置所属的服务的名称。 |
| statefulInvocation | Boolean | true | 是否开启异步任务。<br>- **true**：表示已开启异步任务。<br>- **false**：表示未开启异步任务。 |
| nextToken | String | caeba0be03\*\*\*\*f84eb48b699f0a4883 | 用来返回更多结果。第一次查询不需要提供这个参数，后续查询所需使用的Token，从返回结果中获取。 |

## 示例

请求示例

```pgsql
GET /2016-08-15/services/service_name.alias/functions/testHellowWorld/async-invoke-configs?NextToken=caeba0be03*******b699f0a4883&Limit=20 HTTP/1.1
公共请求头
```

正常返回示例

`JSON`格式

```ruby
HTTP/1.1 200 OK
Content-Type:application/json

{
  "configs" : [ {\
    "createdTime" : "2020-08-20T02:28:21Z",\
    "destinationConfig" : {\
      "onFailure" : {\
        "destination" : "acs:mns:cn-shanghai:1986***743:/queues/failure/messages"\
      },\
      "onSuccess" : {\
        "destination" : "acs:mns:cn-shanghai:1986***743:/queues/success/messages"\
      }\
    },\
    "functionName" : "testHelloWorld",\
    "lastModifiedTime" : "2020-09-10T02:45:02Z",\
    "maxAsyncEventAgeInSeconds" : 1,\
    "maxAsyncRetryAttempts" : 1,\
    "qualifier" : "alias",\
    "serviceName" : "service_name",\
    "statefulInvocation" : true\
  } ],
  "nextToken" : "caeba0be03****f84eb48b699f0a4883"
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。