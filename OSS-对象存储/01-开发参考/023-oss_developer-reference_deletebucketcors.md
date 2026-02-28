### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[跨域资源共享（CORS）](https://help.aliyun.com/zh/oss/developer-reference/cors-2/)DeleteBucketCors

# 调用DeleteBucketCors接口关闭指定Bucket的跨域资源共享功能

更新时间：2025-05-06 05:26:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求语法

请求头

响应头

示例

SDK

命令行工具ossutil

错误码

DeleteBucketCors用于关闭指定存储空间（Bucket）对应的跨域资源共享CORS（Cross-Origin Resource Sharing）功能并清空所有规则。

## 请求语法

```plaintext
DELETE /?cors HTTP/1.1
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

## 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

请求示例

```plaintext
DELETE /?cors HTTP/1.1
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Thu, 17 Apr 2025 05:45:34 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

```plaintext
HTTP/1.1 204 No Content
x-oss-request-id: 5051845BC4689A033D00****
Date: Fri, 24 Feb 2012 05:45:34 GMT
Connection: keep-alive
Content-Length: 0
Server: AliyunOSS
```

## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/cors-1#concept-32018-zh "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/cross-domain-resource-sharing-using-oss-sdk-for-python-v2 "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/cross-domain-resource-sharing-for-php-sdk-v2 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/cross-domain-resource-sharing-for-go-sdk-v2 "")

- [C++](https://help.aliyun.com/zh/oss/developer-reference/cors-10#concept-89705-zh "")

- [C](https://help.aliyun.com/zh/oss/developer-reference/cors-3#concept-89705-zh "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/cors-9#concept-32095-zh "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/cors-8#section-r9f-ft5-q04 "")

- [Ruby](https://help.aliyun.com/zh/oss/developer-reference/cors-6#concept-32128-zh "")


## **命令行工具ossutil**

DeleteBucketCors接口所对应的ossutil命令，请参见 [delete-bucket-cors](https://help.aliyun.com/zh/oss/developer-reference/delete-a-cross-domain-resource-sharing-rule "")。

## 错误码

| **错误码** | **HTTP 状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP 状态码** | **描述** |
| NoSuchBucket | 404 | 目标Bucket不存在。 |
| AccessDenied | 403 | 没有删除权限。只有Bucket的拥有者才有权限删除Bucket对应的CORS规则。 |