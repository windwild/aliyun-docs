### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [用户指南](https://help.aliyun.com/zh/oss/user-guide/) [服务支持](https://help.aliyun.com/zh/oss/user-guide/support/) [错误码](https://help.aliyun.com/zh/oss/user-guide/error-code/) 错误码

# 错误码

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：错误码](https://help.aliyun.com/zh/oss/user-guide/error-code/)[下一篇：获取Request ID](https://help.aliyun.com/zh/oss/user-guide/obtain-request-ids)

该文章对您有帮助吗？

反馈

访问OSS时返回的错误信息，通常包含`EC码`和`HTTP状态码`两种。遵循以下自助排查流程，可快速定位并解决问题。

## **自助排查流程**

**步骤一：定位关键信息**

一次典型的错误响应包含了定位问题的核心信息。建议首先阅读`Message`字段获得错误的直接描述，然后按以下顺序使用关键字段进行排查，如下为错误响应示例：

```xml
HTTP/1.1 400 Bad Request
Server: AliyunOSS
Date: Thu, 11 Aug 2019 01:44:54 GMT
Content-Type: application/xml
Content-Length: 322
Connection: keep-alive
x-oss-request-id: 57ABD896CCB80C366955****
x-oss-server-time: 0
<?xml version="1.0" encoding="UTF-8"?>
<Error>
  <Code>MissingArgument</Code>
  <Message>Missing Some Required Arguments.</Message>
  <RequestId>57ABD896CCB80C366955****</RequestId>
  <HostId>oss-example.oss-cn-hangzhou.aliyuncs.com</HostId>
  <EC>0016-00000502</EC>
  <RecommendDoc>https://api.aliyun.com/troubleshoot?q=0016-00000502</RecommendDoc>
</Error>
```

- `RecommendDoc` ( **首选方案**)：官方为该EC码推荐的解决方案链接。

- `EC` ( **自助排查的核心**)：细粒度的错误码，唯一对应一个错误原因。

- `HTTP状态码` (如 400 Bad Request)：请求结果的通用状态，可用于初步判断问题方向。

- `RequestId` ( **寻求支持的凭证**)：请求的唯一ID，在联系技术支持时必须提供。


**步骤二：获取解决方案**

获取`EC`码后，有两种方式可用于自助排查：

**重要**

`EC`码仅用于问题定位，其值可能会发生变化，您的业务逻辑不应依赖`EC`码。

1. **访问**`RecommendDoc` **链接**

   - 直接访问错误响应中提供的`RecommendDoc`链接。
2. **查阅EC错误码列表**

   - 若响应中没有`RecommendDoc`，可根据`EC`码在错误码列表中查找其含义。

在完成上述自助排查步骤后，如果问题依旧存在，可准备相关信息联系技术支持。

为确保问题能被快速、精确地定位，寻求支持时必须提供本次请求的 `Request ID`。详细的获取方法见 [获取Request ID](https://help.aliyun.com/zh/oss/user-guide/obtain-request-ids#concept-2087584 "")。

## **错误响应字段详解**

### **错误响应头**

|     |     |
| --- | --- |
| **响应头** | **说明** |
| `x-oss-ec` | OSS的一种细粒度错误码。每一个错误原因对应一个唯一的EC（Error Code）。相比于响应体中的Code，EC能更加精确地反映请求出错的原因，同时也方便检索对应的解决方案。<br>**重要** <br>EC仅用于问题定位，有可能发生变化，不保证前向兼容。因此，您的业务逻辑不应该依赖于EC错误码。 |
| `x-oss-request-id` | 请求的唯一ID。您可以凭借此Request ID联系技术支持，排查并解决您遇到的问题。 |

**响应头示例**

```http
HTTP/1.1 403 Forbidden
Server: AliyunOSS
Date: Wed, 09 Nov 2022 08:45:46 GMT
Content-Type: application/xml
Content-Length: 471
Connection: keep-alive
x-oss-request-id: 636B68BA80DA8539399F****
x-oss-server-time: 0
x-oss-ec: 0003-00000001
```

关于 `Content-Length`，`Connection` 等公共响应头的更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

### **错误响应体**

|     |     |
| --- | --- |
| **响应元素** | **说明** |
| `Code` | OSS定义的通用错误码。 |
| `Message` | 详细的错误描述信息。 |
| `RequestId` | 请求的唯一ID。您可以凭借此Request ID联系技术支持，排查并解决您遇到的问题。 |
| `HostId` | 用于标识访问的OSS集群，与用户请求时使用的Host一致。 |
| `EC` | 与响应头中的 `x-oss-ec` 一致的细粒度错误码。 |
| `RecommendDoc` | EC对应的OpenAPI问题诊断链接。强烈建议您优先访问此链接进行自助排查。 |

**响应体示例**

```xml
<?xml version="1.0" ?>
<Error xmlns="http://doc.oss-cn-hangzhou.aliyuncs.com">
  <Code>MalformedXML</Code>
  <Message>The XML you provided was not well-formed or did not validate against our published schema.</Message>
  <RequestId>57ABD896CCB80C366955****</RequestId>
  <HostId>oss-cn-hangzhou.aliyuncs.com</HostId>
  <EC>0031-00000001</EC>
  <RecommendDoc>https://api.aliyun.com/troubleshoot?q=0031-00000001</RecommendDoc>
</Error>
```

## 相关文档

- [获取Request ID](https://help.aliyun.com/zh/oss/user-guide/obtain-request-ids#concept-2087584 "")

- [EC错误码列表](https://help.aliyun.com/zh/oss/user-guide/error-codes/ "")

- [HTTP错误码列表](https://help.aliyun.com/zh/oss/user-guide/http-status-code/ "")