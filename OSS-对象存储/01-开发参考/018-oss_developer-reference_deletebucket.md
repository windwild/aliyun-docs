### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[基础操作](https://help.aliyun.com/zh/oss/developer-reference/basic-operations/)DeleteBucket

# DeleteBucket

更新时间：2025-05-06 05:19:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PutBucket](https://help.aliyun.com/zh/oss/developer-reference/putbucket)[下一篇：GetBucket (ListObjects)](https://help.aliyun.com/zh/oss/developer-reference/listobjects)

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

调用DeleteBucket删除某个存储空间（Bucket）。

**重要**

- 只有Bucket的拥有者才有权限删除该Bucket。

- 为了防止误删除的发生，OSS不允许删除一个非空的Bucket。


## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

| **API** | **Action** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **API** | **Action** | **说明** |
| DeleteBucket | `oss:DeleteBucket` | 删除Bucket。 |

## 请求语法

```plaintext
DELETE / HTTP/1.1
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

- 正常删除的请求示例















```plaintext
DELETE / HTTP/1.1
Host: test.oss-cn-hangzhou.aliyuncs.com
Accept-Encoding: identity
User-Agent: aliyun-sdk-python/2.6.0(Windows/7/AMD64;3.7.0)
Accept: */*
Connection: keep-alive
date: Tue, 15 Jan 2019 08:19:04 GMT
authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
Content-Length: 0
```





返回示例

















```plaintext
HTTP/1.1 204 No Content
Server: AliyunOSS
Date: Tue, 15 Jan 2019 08:19:04 GMT
Content-Length: 0
Connection: keep-alive
x-oss-request-id: 5C3D9778CC1C2AEDF85B****
x-oss-server-time: 190
```

- 删除的Bucket不存在的请求示例















```plaintext
DELETE / HTTP/1.1
Host: test.oss-cn-hangzhou.aliyuncs.com
Accept-Encoding: identity
User-Agent: aliyun-sdk-python/2.6.0(Windows/7/AMD64;3.7.0)
Accept: */*
Connection: keep-alive
date: Tue, 15 Jan 2019 07:53:24 GMT
authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=content-length,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
Content-Length: 0
```





返回示例

















```xml
HTTP/1.1 404 Not Found
Server: AliyunOSS
Date: Tue, 15 Jan 2019 07:53:25 GMT
Content-Type: application/xml
Content-Length: 288
Connection: keep-alive
x-oss-request-id: 5C3D9175B6FC201293AD****

<?xml version="1.0" encoding="UTF-8"?>
<Error>
    <Code>NoSuchBucket</Code>
    <Message>The specified bucket does not exist.</Message>
    <RequestId>5C3D9175B6FC201293AD****</RequestId>
    <HostId>test.oss-cn-hangzhou.aliyuncs.com</HostId>
    <BucketName>test</BucketName>
    <EC>0015-00000101</EC>
</Error>
```

- 删除的Bucket非空的请求示例















```plaintext
DELETE / HTTP/1.1
Host: test.oss-cn-hangzhou.aliyuncs.com
Accept-Encoding: identity
User-Agent: aliyun-sdk-python/2.6.0(Windows/7/AMD64;3.7.0)
Accept: */*
Connection: keep-alive
date: Thu, 17 Apr 2025 07:35:06 GMT
authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=content-length,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
Content-Length: 0
```





返回示例

















```plaintext
HTTP/1.1 409 Conflict
Server: AliyunOSS
Date: Tue, 15 Jan 2019 07:35:06 GMT
Content-Type: application/xml
Content-Length: 296
Connection: keep-alive
x-oss-request-id: 5C3D8D2A0ACA54D87B43****
x-oss-server-time: 16

<?xml version="1.0" encoding="UTF-8"?>
<Error>
    <Code>BucketNotEmpty</Code>
    <Message>The bucket has objects. Please delete them first.</Message>
    <RequestId>5C3D8D2A0ACA54D87B43****</RequestId>
    <HostId>test.oss-cn-hangzhou.aliyuncs.com</HostId>
    <BucketName>test</BucketName>
    <EC>0015-00000301</EC>
</Error>
```


## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/delete-a-bucket#concept-2348447 "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/delete-buckets-using-oss-sdk-for-python-v2 "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/php-v2-delete-a-bucket "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/delete-bucket-using-oss-sdk-for-go-v2 "")

- [C](https://help.aliyun.com/zh/oss/developer-reference/delete-buckets-5#concept-2365068 "")

- [C++](https://help.aliyun.com/zh/oss/developer-reference/delete-a-bucket-3#concept-2351985 "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/delete-buckets-2#concept-2372560 "")

- [Android](https://help.aliyun.com/zh/oss/developer-reference/delete-buckets-1#concept-2382431 "")

- [iOS](https://help.aliyun.com/zh/oss/developer-reference/delete-a-bucket-2#concept-2056672 "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/delete-a-bucket-5#concept-2380819 "")

- [Ruby](https://help.aliyun.com/zh/oss/developer-reference/delete-a-bucket-4#concept-2382500 "")


## **命令行工具ossutil**

DeleteBucket接口所对应的ossutil命令，请参见 [delete-bucket](https://help.aliyun.com/zh/oss/developer-reference/delete-bucket "")。

## 错误码

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| AccessDenied | 403 Forbidden | 没有删除该Bucket的权限。只有Bucket的拥有者才能删除该Bucket。 |