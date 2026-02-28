### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[数据索引（Data Indexing）](https://help.aliyun.com/zh/oss/developer-reference/data-indexing/)CloseMetaQuery

# CloseMetaQuery

更新时间：2025-05-06 05:22:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DoMetaQuery](https://help.aliyun.com/zh/oss/developer-reference/dometaquery)[下一篇：附录：标量检索的字段和操作符列表](https://help.aliyun.com/zh/oss/developer-reference/appendix-supported-fields-and-operators)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

请求语法

请求头

响应头

示例

SDK

命令行工具ossutil

错误码

调用CloseMetaQuery接口关闭存储空间（Bucket）的元数据管理功能。关闭元数据管理功能后，OSS会自动删除Bucket的元数据索引库，您将无法进行元数据索引。

## 注意事项

- 要关闭Bucket的元数据管理功能，您必须有`oss:CloseMetaQuery`权限。具体操作，请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

- 无论Bucket是否已开启元数据管理功能，调用CloseMetaQuery接口关闭元数据管理功能时均返回200状态码。

- 该接口为异步操作，不是立即生效的。调用CloseMetaQuery接口后，OSS需要一定时间完成元数据索引库的实际删除。


## 请求语法

```plaintext
POST /?metaQuery&comp=delete HTTP/1.1
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

## 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

请求示例

```plaintext
POST /?metaQuery&comp=delete HTTP/1.1
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Thu, 17 Apr 2025 13:08:38 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

```plaintext
HTTP/1.1 200 OK
x-oss-request-id: 5C1B138A109F4E405B2D****
Date: Mon, 26 Jul 2021 13:08:38 GMT
Content-Length: 0
Connection: keep-alive
Server: AliyunOSS
x-oss-server-time: 178
```

## SDK

本接口对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/data-indexing-2 "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/data-indexing-using-oss-sdk-for-python-v2 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/data-indexing-3 "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/data-indexing-using-oss-sdk-for-php-v2 "")


## **命令行工具ossutil**

CloseMetaQuery接口所对应的ossutil命令，请参见 [close-meta-query](https://help.aliyun.com/zh/oss/developer-reference/close-meta-query "")。

## 错误码

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| AccessDenied | 403 | 没有访问该Bucket的权限，请确保已为RAM用户授予访问该Bucket的权限。 |
| NoSuchBucket | 404 | 目标Bucket不存在，请设置正确的Bucket名称。 |