### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/function/)GetFunction

# GetFunction

更新时间：2025-08-20 04:19:51

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：UpdateFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-updatefunction)[下一篇：GetFunctionCode](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getfunctioncode)

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

调用GetFunction接口获取函数信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=GetFunction&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口无特殊请求头，关于公共请求头信息，请参见 [公共参数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/common-parameters)。

## 请求语法

```plaintext
GET /services/{serviceName.qualifier}/functions/{functionName} HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 服务的名称。 |
| qualifier | String | Path | 否 | test | 服务的版本或别名。 |
| functionName | String | Path | 是 | function\_name | 函数的名称。 |

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| ETag | String | e19d5cd5af0378da05f63f891c74\*\*\*\* | 确保实际修改的函数和期望更改的函数是一致的。 |
| codeChecksum | String | 2825179536350\*\*\*\* | 函数代码包的CRC-64值。 |
| codeSize | Long | 421 | 系统返回的函数代码包的大小，单位Byte。 |
| createdTime | String | 2020-04-01T08:15:27Z | 函数的创建时间。 |
| description | String | test\_description | 函数的描述。 |
| environmentVariables | Map |  | 为函数设置的环境变量，可以在函数中获取环境变量的值。更多信息，请参见 [环境变量](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/fc-environment-variables)。 |
| functionId | String | aa715851-1c20-4b89-a8fb-\*\*\* | 系统为每个函数生成的ID，全局唯一。 |
| functionName | String | function\_name | 函数的名称。 |
| handler | String | index.handler | 函数执行的入口，更多信息，请参见 [函数入口](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。 |
| lastModifiedTime | Long | 2020-04-01T08:15:27Z | 函数上一次被更新的时间。 |
| memorySize | Integer | 256 | 函数的内存规格，单位为MB，内存大小为64 MB的倍数。不同的函数实例类型，内存规格存在差异，更多信息，请参见 [实例规格](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/instance-types-and-instance-modes)。 |
| runtime | String | python3 | 函数运行的语言环境。关于函数计算支持的运行环境，请参见 [支持的函数运行环境列表](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions)。 |
| timeout | Integer | 60 | 函数运行的超时时间，单位为秒，默认60秒。最小1秒，最长86400秒。如果函数运行超过设置的时间，函数运行将被终止。 |
| initializationTimeout | Integer | 60 | 初始化函数运行的超时时间，单位为秒，默认3秒。最小1秒，最长5分钟。初始化函数超过这个时间后会被终止执行。 |
| initializer | String | index.handler | 初始化函数执行的入口，具体格式与语言相关，更多信息，请参见 [Initializer函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。 |
| caPort | Integer | 9000 | Custom Runtime或Custom Container运行时HTTP Server的监听端口。 |
| customContainerConfig | [CustomContainerConfigInfo](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#CustomContainerConfigInfo "") |  | custom-container运行时的相关配置，配置后函数可以使用自定义容器镜像执行函数。 |
| layers | Array of String | 02f81d283888f5ec63442a88fe82b260#Layer-name#1 | 层资源的名称。 |

## 示例

请求示例

```plaintext
GET /services/{serviceName.qualifier}/functions/function_name HTTP/1.1
Host:fc-ram.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
Content-Type:application/json

{
  "codeChecksum" : "2825179536350****",
  "codeSize" : 421,
  "createdTime" : "2020-04-01T08:15:27Z",
  "description" : "test_description",
  "functionId" : "aa715851-1c20-4b89-a8fb-***",
  "functionName" : "function_name",
  "handler" : "index.handler",
  "memorySize" : 256,
  "runtime" : "python3",
  "timeout" : 60,
  "initializationTimeout" : 60,
  "initializer" : "index.handler",
  "caPort" : 9000,
  "customContainerConfig" : {
    "args" : "[\"-arg1\", \"value1\"]",
    "command" : "[\"/code/myserver\"]",
    "image" : "registry-vpc.cn-hangzhou.aliyuncs.com/fc-demo/helloworld:v1beta1",
    "accelerationType" : "Default",
    "accelerationInfo" : {
      "status" : "Preparing"
    },
    "instanceID" : "cri-xxxxxx"
  },
  "layers" : [ "02f81d283888f5ec63442a88fe82b260#Layer-name#1" ]
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。