### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[自定义域名](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/customdomain/)ListCustomDomains

# ListCustomDomains

更新时间：2025-08-20 04:24:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetCustomDomain](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-getcustomdomain)[下一篇：PutProvisionConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-putprovisionconfig)

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

调用ListCustomDomains接口获取自定义域名列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=ListCustomDomains&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```plaintext
GET /custom-domains HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| limit | Integer | Query | 否 | 20 | 限定此次返回资源的数量。如果不设定，默认返回20，最大不能超过100。返回结果可以小于指定的数量，但不能大于指定的数量。 |
| nextToken | String | Query | 否 | 20 | 当指定Limit时，如果还有多余的返回值则会返回NextToken。 |
| prefix | String | Query | 否 | prefix\_text | 限定返回的资源名称必须以Prefix作为前缀。 |
| startKey | String | Query | 否 | next\_service | 设定结果从startKey之后（包括startKey）按字母排序的第一个开始返回。 |

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| nextToken | String | example.com | 当指定Limit时，如果还有多余的返回值则会返回NextToken。 |
| customDomains | Array |  | 自定义域名。 |
| accountId | String | 19861144305\*\*\*\* | 账号ID。 |
| apiVersion | String | 2016-08-15 | API的版本。 |
| certConfig | [CertConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#CertConfig "") |  | HTTPS证书的配置信息。 |
| createdTime | String | 2020-07-27T08:02:19Z | 域名的创建时间。 |
| domainName | String | example.com | 域名。 |
| lastModifiedTime | String | 2020-07-27T08:02:19Z | 域名上一次被更新的时间。 |
| protocol | String | HTTP | 域名支持的协议类型。<br>- HTTP：仅支持HTTP协议。<br>- HTTP,HTTPS：支持HTTP及HTTPS协议。 |
| routeConfig | [RouteConfig](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#RouteConfig "") |  | 路由表：定义域名访问时的PATH到Function的映射。 |

## 示例

请求示例

```plaintext
GET /custom-domains?limit=20&nextToken=20&prefix=prefix_text&startKey=next_service HTTP/1.1
Host:fc-ram.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
Content-Type:application/json

{
  "nextToken" : "example.com",
  "customDomains" : [ {\
    "accountId" : "19861144305****",\
    "apiVersion" : "2016-08-15",\
    "certConfig" : {\
      "certificate" : "-----BEGIN CERTIFICATE----- xxxxx -----END CERTIFICATE-----",\
      "privateKey" : "-----BEGIN RSA PRIVATE KEY----- xxxxx -----END RSA PRIVATE KEY-----"\
    },\
    "createdTime" : "2020-07-27T08:02:19Z",\
    "domainName" : "example.com",\
    "lastModifiedTime" : "2020-07-27T08:02:19Z",\
    "protocol" : "HTTP",\
    "routeConfig" : {\
      "routes" : [ {\
        "functionName" : "f1",\
        "methods" : [ "GET" ],\
        "path" : "/login",\
        "qualifier" : "prod",\
        "serviceName" : "s1"\
      } ]\
    }\
  } ]
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。