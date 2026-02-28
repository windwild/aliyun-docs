### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[日志管理（Logging）](https://help.aliyun.com/zh/oss/developer-reference/logging-3/)DeleteBucketLogging

# DeleteBucketLogging

更新时间：2025-09-23 06:42:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

权限说明

请求语法

请求头

响应头

示例

SDK

命令行工具ossutil

错误码

DeleteBucketLogging用于关闭存储空间（Bucket）的访问日志记录功能。只有Bucket的拥有者才有权限关闭Bucket访问日志记录功能。

## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

| **API** | **Action** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **API** | **Action** | **说明** |
| DeleteBucketLogging | oss:DeleteBucketLogging | 关闭Bucket日志转存功能。 |

## 请求语法

```plaintext
DELETE /?logging HTTP/1.1
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

当您在OSS ON云盒中调用该接口时，您需要将Host替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

## 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

**Bucket示例**

请求示例

```plaintext
DELETE /?logging HTTP/1.1
Host: Host
Date: Thu, 17 Apr 2025 05:35:24 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

**说明**

如果目标Bucket没有开启访问日志记录功能，则返回204状态码。

```plaintext
HTTP/1.1 204 No Content
x-oss-request-id: 534B371674E88A4D8906****
Date: Fri, 24 Feb 2012 05:35:24 GMT
Connection: keep-alive
Content-Length: 0
Server: AliyunOSS
x-oss-server-time: 198
```

**向量Bucket示例**

> 向量 Bucket 的Host中的地域参数使用阿里云标准地域 ID（如 cn-hangzhou），而非用于通用 Bucket 的旧版 OSS 地域（如 oss-cn-hangzhou）

请求示例

```plaintext
DELETE /?logging HTTP/1.1
Host: exampebucket-123***456.cn-hangzhou.oss-vectors.aliyuncs.com
Date: Thu, 17 Apr 2025 05:35:24 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

**说明**

如果目标Bucket没有开启访问日志记录功能，则返回204状态码。

```plaintext
HTTP/1.1 204 No Content
x-oss-request-id: 534B371674E88A4D8906****
Date: Fri, 24 Feb 2012 05:35:24 GMT
Connection: keep-alive
Content-Length: 0
Server: AliyunOSS
x-oss-server-time: 198
```

## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/logging-1#concept-32019-zh "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/bucket-logging-using-oss-sdk-for-python-v2 "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/php-logging-2 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-logging-5 "")

- [C](https://help.aliyun.com/zh/oss/developer-reference/logging-12#concept-89684-zh "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/logging-2#concept-48308-zh "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/logging-8#concept-32080-zh "")

- [Ruby](https://help.aliyun.com/zh/oss/developer-reference/logging-6#concept-32125-zh "")


## **命令行工具ossutil**

DeleteBucketLogging接口所对应的ossutil命令，请参见 [delete-bucket-logging](https://help.aliyun.com/zh/oss/developer-reference/delete-bucket-logging "")。

## 错误码

| **错误码** | **HTTP 状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP 状态码** | **描述** |
| NoSuchBucket | 404 | 目标Bucket不存在。 |
| AccessDenied | 403 | 没有关闭Bucket访问日志记录功能的权限。只有Bucket的拥有者才可以关闭Bucket访问日志记录功能。 |