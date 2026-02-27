### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/function/)UpdateFunction

# UpdateFunction

更新时间：2025-08-20 04:19:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DeleteFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-deletefunction)[下一篇：GetFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getfunction)

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

调用UpdateFunction接口更新函数信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=UpdateFunction&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口使用公共请求头和特殊请求头。本文已列出特殊请求头，公共请求头，请参见 [公共参数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/common-parameters)。

| **名称** | **类型** | **是否必选** | **示例** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例** | **描述** |
| If-Match | String | 否 | e19d5cd5af0378da05f63f891c7467af | 用于确保实际更改的资源和期望更改的资源是一致的，该值来自 [CreateFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-createfunction)、 [GetFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getfunction) 和 [UpdateFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-updatefunction) 的响应。 |
| X-Fc-Code-Checksum | String | 否 | 543402527838814\*\*\*\* | 函数代码包的CRC-64值。 |

## 请求语法

```plaintext
PUT /services/{serviceName}/functions/{functionName} HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 服务的名称。 |
| functionName | String | Path | 是 | function\_name | 函数的名称。 |
|  | Object | Body | 否 |  | 函数的定义。 |
| code | [Code](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#Code "") | Body | 否 |  | 指定Code ZIP包。 |
| customContainerConfig | [CustomContainerConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#CustomContainerConfig "") | Body | 否 |  | Custom Container运行时的相关配置。配置后函数可以使用自定义容器镜像执行函数。 |
| layers | Array of String | Body | 否 | 02f81d283888f5ec63442a88fe82b260#Layer-name#1 | 层资源的名称。 |
| description | String | Body | 否 | test\_description | 函数的描述信息。 |
| environmentVariables | Map | Body | 否 |  | 为函数设置的环境变量，可以在函数中获取环境变量的值。更多信息，请参见 [环境变量](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/fc-environment-variables)。 |
| handler | String | Body | 否 | index.handler | 函数执行的入口，具体格式和语言相关。更多信息，请参见 [函数入口](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。 |
| memorySize | Integer | Body | 否 | 512 | 函数的内存规格，单位为MB，内存大小为64 MB的倍数。不同的函数实例类型，内存规格存在差异，更多信息，请参见 [实例规格](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/instance-types-and-instance-modes)。 |
| runtime | String | Body | 否 | python3 | 函数运行的语言环境，支持**nodejs14**、**nodejs12**、**nodejs10**、**nodejs8**、**nodejs6**、**nodejs4.4**、**python3.9**、**python3**、**python2.7**、**java11**、**java8**、**go1**、**php7.2**、**dotnetcore2.1**、**custom**和**custom-container**。更多信息，请参见 [支持的函数运行环境列表](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions)。 |
| timeout | String | Body | 否 | 60 | 函数运行的超时时间，单位为秒，默认60秒。最小1秒，最长86400秒。函数超过这个时间后会被终止执行。 |
| initializationTimeout | Integer | Body | 否 | 60 | 初始化函数运行的超时时间，单位为秒，默认3秒。最小1秒，最长5分钟。初始化函数超过这个时间后会被终止执行。 |
| initializer | String | Body | 否 | index.handler | 初始化函数执行的入口，具体格式与语言相关，更多信息，请参见 [Initializer函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。 |
| caPort | Integer | Body | 否 | 9000 | Custom Runtime或Custom Container运行时HTTP Server的监听端口。 |

Code支持两种方式提供函数代码包，在一次请求中必须且只能使用其中一种：

- 指定存储代码包的ossBucketName和ossObjectName。
- 指定zipFile为ZIP包的Base64编码内容。

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| ETag | String | e19d5cd5af0378da05f63f891c74\*\*\*\* | 确保实际修改的函数和期望更改的函数是一致的。该值来自 [CreateFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-createfunction)、 [GetFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getfunction) 和 [UpdateFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-updatefunction) 的响应。 |
| codeChecksum | String | 2825179536350\*\*\*\* | 函数代码包的CRC-64值。 |
| codeSize | Long | 421 | 系统返回的函数的代码包大小，单位为Byte。 |
| createdTime | String | 2020-04-01T08:14:58Z | 函数的创建时间。 |
| customContainerConfig | [CustomContainerConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#CustomContainerConfig "") |  | Custom Container运行时的相关配置。配置后函数可以使用自定义容器镜像执行函数。 |
| layers | Array of String | 02f81d283888f5ec63442a88fe82\*\*\*\*#Layer-name#1 | 层资源的名称。 |
| description | String | test\_description | 函数的描述。 |
| environmentVariables | Map |  | 为函数设置的环境变量，可以在函数中获取环境变量的值。更多信息，请参见 [环境变量](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/fc-environment-variables)。 |
| functionId | String | e68905d5-f81c-4238-a5e4-\*\*\* | 系统为每个函数生成的ID，全网唯一。 |
| functionName | String | function\_name | 函数的名称。 |
| handler | String | index.handler | 函数执行的入口，具体格式和语言相关，更多信息，请参见 [函数入口](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。 |
| lastModifiedTime | Long | 2016-08-15T17:00:00.000+0000 | 函数上一次被更新的时间。 |
| memorySize | Integer | 512 | 函数的内存规格，单位为MB，内存大小为64 MB的倍数。不同的函数实例类型，内存规格存在差异，更多信息，请参见 [实例规格](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/instance-types-and-instance-modes)。 |
| runtime | String | python3 | 函数运行的语言环境，支持**nodejs14**、**nodejs12**、**nodejs10**、**nodejs8**、**nodejs6**、**nodejs4.4**、**python3.9**、**python3**、**python2.7**、**java11**、**java8**、**go1**、**php7.2**、**dotnetcore2.1**、**custom**和**custom-container**。更多信息，请参见 [支持的函数运行环境列表](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions)。 |
| timeout | Integer | 10 | 函数运行的超时时间，单位为秒，默认60秒。最小1秒，最长86400秒。函数超过这个时间后会被终止执行。 |
| initializationTimeout | Integer | 60 | 初始化函数运行的超时时间，单位为秒，默认3秒。最小1秒，最长5分钟。初始化函数超过这个时间后会被终止执行。 |
| initializer | String | index.handler | 初始化函数执行的入口，具体格式与语言相关，更多信息，请参见 [Initializer函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/basics)。 |
| caPort | Integer | 9000 | Custom Runtime或Custom Container运行时HTTP Server的监听端口。 |

## 示例

请求示例

```plaintext
PUT /services/service_name/functions/function_name HTTP/1.1
Host:fc-ram.aliyuncs.com
If-Match:e19d5cd5af0378da05f63f891c7467af
X-Fc-Code-Checksum:543402527838814****
Content-Type:application/json

{
  "code" : {
    "ossBucketName" : "demo-bucket",
    "ossObjectName" : "demo-key",
    "zipFile" : "cHJpbnQoImhlbGxvIHdvcmxkIikK"
  },
  "customContainerConfig" : {
    "args" : "[\"-arg1\", \"value1\"]",
    "command" : "[\"/code/myserver\"]",
    "image" : "registry-vpc.cn-hangzhou.aliyuncs.com/fc-demo/helloworld:v1beta1",
    "accelerationType" : "Default",
    "instanceID" : "cri-xxxxxxxx"
  },
  "layers" : [ "02f81d283888f5ec63442a88fe82b260#Layer-name#1" ],
  "description" : "test_description",
  "handler" : "index.handler",
  "memorySize" : 512,
  "runtime" : "python3",
  "timeout" : "60",
  "initializationTimeout" : 60,
  "initializer" : "index.handler",
  "caPort" : 9000
}
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
Content-Type:application/json

{
  "codeChecksum" : "2825179536350****",
  "codeSize" : 421,
  "createdTime" : "2020-04-01T08:14:58Z",
  "customContainerConfig" : {
    "args" : "[\"-arg1\", \"value1\"]",
    "command" : "[\"/code/myserver\"]",
    "image" : "registry-vpc.cn-hangzhou.aliyuncs.com/fc-demo/helloworld:v1beta1",
    "accelerationType" : "Default",
    "instanceID" : "cri-xxxxxxxx"
  },
  "layers" : [ "02f81d283888f5ec63442a88fe82****#Layer-name#1" ],
  "description" : "test_description",
  "functionId" : "e68905d5-f81c-4238-a5e4-***",
  "functionName" : "function_name",
  "handler" : "index.handler",
  "memorySize" : 512,
  "runtime" : "python3",
  "timeout" : 10,
  "initializationTimeout" : 60,
  "initializer" : "index.handler",
  "caPort" : 9000
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。