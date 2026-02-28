### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[服务](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/service/)ListServices

# ListServices

更新时间：2025-08-20 04:18:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetService](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getservice)[下一篇：CreateFunction](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-createfunction)

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

调用ListServices接口获取服务列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=ListServices&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```plaintext
GET /services HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| limit | Integer | Query | 否 | 20 | 限定此次返回资源的数量。如果不设定，默认返回20，最大不能超过100。返回结果可以小于指定的数量，但不会多于指定的数量。 |
| nextToken | String | Query | 否 | nextService | 用来返回更多结果。第一次查询不需要提供这个参数，后续查询的Token从返回结果中获取。 |
| prefix | String | Query | 否 | prefix\_text | 限定返回的资源名称，名称必须以Prefix作为前缀，例如Prefix是a，则返回的资源名均是以a开始的。 |
| startKey | String | Query | 否 | nextService | 设定结果从startKey之后（包括startKey）按字母排序的第一个开始返回。 |

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| nextToken | String | \_FUN\_NAS-classify | 用来返回更多结果。<br>**说明**<br>如果这个值没有返回，则说明没有更多结果。 |
| services | Array |  | 服务列表。 |
| createdTime | String | 2020-04-03T05:57:28Z | 服务的创建时间。 |
| description | String | test\_description | 服务的描述。 |
| internetAccess | Boolean | true | 是否允许函数访问公网：<br>- **true**：允许函数访问公网。<br>- **false**：不允许函数访问公网。 |
| lastModifiedTime | String | 2020-04-03T05:57:28Z | 服务上一次被更新的时间。 |
| logConfig | [LogConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#LogConfig "") |  | 日志配置，函数产生的日志会写入这里配置的Logstore。 |
| nasConfig | [NASConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#NASConfig "") |  | NAS配置，配置后函数可以访问指定NAS资源。 |
| role | String | acs:ram::198613743\*\*\*\*:role/fc-public-test | 授予函数计算所需权限的RAM角色，使用场景包含：<br>- 把函数产生的日志发送到您的Logstore中。<br>- 为函数在执行中访问其他云资源生成Token。 |
| serviceId | String | c910061f-\*\*\*\*-44e6-b659-\*\*\*c | 系统为每个服务生成的ID，全网唯一。 |
| serviceName | String | service\_name | 服务的名称。 |
| vpcConfig | [VPCConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#VPCConfig "") |  | VPC配置，配置后函数可以访问指定VPC资源。 |
| tracingConfig | [TracingConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#TracingConfig "") |  | 链路追踪配置。当函数计算与链路追踪集成后，您可以记录请求在函数计算的耗时时间、查看函数的冷启动时间、记录函数内部时间的消耗等，更多信息，请参见 [链路追踪](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/overview-32)。 |

## 示例

请求示例

```plaintext
GET /2016-08-15/services HTTP/1.1
公共请求头
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
Content-Type:application/json

{
  "nextToken" : "_FUN_NAS-classify",
  "services" : [ {\
    "createdTime" : "2020-04-03T05:57:28Z",\
    "description" : "test_description",\
    "internetAccess" : true,\
    "lastModifiedTime" : "2020-04-03T05:57:28Z",\
    "logConfig" : {\
      "logstore" : "test-prj",\
      "project" : "test-logstore",\
      "enableRequestMetrics" : true,\
      "logBeginRule" : "DefaultRegex"\
    },\
    "nasConfig" : {\
      "groupId" : "100",\
      "mountPoints" : [ {\
        "mountDir" : "/home/test",\
        "serverAddr" : "***-uni85.cn-hangzhou.nas.aliyuncs.com:/"\
      } ],\
      "userId" : "100"\
    },\
    "role" : "acs:ram::198613743****:role/fc-public-test",\
    "serviceId" : "c910061f-****-44e6-b659-***c",\
    "serviceName" : "service_name",\
    "vpcConfig" : {\
      "securityGroupId" : "sg-bp18hj1wtxgy3b0***",\
      "vSwitchIds" : [ "vsw-bp1ozpcrdc6r****" ],\
      "vpcId" : "vpc-***"\
    },\
    "tracingConfig" : {\
      "type" : "Jaeger"\
    }\
  } ]
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。