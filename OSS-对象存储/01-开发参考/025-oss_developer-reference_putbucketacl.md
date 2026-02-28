### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[权限控制（ACL）](https://help.aliyun.com/zh/oss/developer-reference/acl/)PutBucketAcl

# PutBucketAcl

更新时间：2025-05-06 05:20:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetBucketWorm](https://help.aliyun.com/zh/oss/developer-reference/getbucketworm)[下一篇：GetBucketAcl](https://help.aliyun.com/zh/oss/developer-reference/getbucketacl)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

权限说明

请求语法

请求头

响应头

示例

SDK

命令行工具ossutil

错误码

PutBucketAcl接口用于设置或修改存储空间（Bucket）的访问权限（ACL）。

## 注意事项

使用PutBucketAcl接口时，有如下注意事项：

- 该接口的请求者需要对Bucket有写入ACL的权限。

- PutBucketAcl为覆盖语义，即新传入的ACL将覆盖原有的ACL。

- 如果指定要设置ACL的Bucket不存在，调用该接口时将新建Bucket。


## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

| API | Action | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| API | Action | 说明 |
| PutBucketAcl | oss:PutBucketAcl | 设置或修改Bucket ACL。 |

## 请求语法

```plaintext
PUT /?acl HTTP/1.1
x-oss-acl: Permission
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

当您在OSS ON云盒中调用该接口时，您需要将Host替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

## 请求头

| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| x-oss-acl | 字符串 | 是 | private | 指定Bucket的访问权限ACL。<br>PutBucketAcl接口通过Put请求中的x-oss-acl请求头来设置访问权限，如果没有该请求头，则访问权限设置不生效。<br>取值：public-read-write、public-read、private。<br>- public-read-write（公共读写）：所有用户都有该Bucket内的文件的读写权限。请谨慎使用该访问权限。<br>  <br>- public-read（公共读）：Bucket的拥有者和授权用户有该Bucket内的文件的读写权限，其他用户只有该Bucket内的文件的读权限。请谨慎使用该访问权限。<br>  <br>- private：Bucket的拥有者和授权用户有该Bucket内的文件的读写权限，其他用户没有权限操作该Bucket内的文件。 |

此接口涉及的其他公共请求头，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅涉及公共响应头，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

请求示例

```plaintext
PUT /?acl HTTP/1.1
x-oss-acl: public-read
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Thu, 17 Apr 2025 03:21:12 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

- 正常返回示例















```plaintext
HTTP/1.1 200 OK
x-oss-request-id: 534B371674E88A4D8906****
Date: Fri, 24 Feb 2012 03:21:12 GMT
Content-Length: 0
Connection: keep-alive
Server: AliyunOSS
```

- 设置读写权限无效的返回示例















```plaintext
HTTP/1.1 400 Bad Request
x-oss-request-id: 56594298207FB3044385****
Date: Fri, 24 Feb 2012 03:55:00 GMT
Content-Length: 309
Content-Type: text/xml; charset=UTF-8
Connection: keep-alive
Server: AliyunOSS

<?xml version="1.0" encoding="UTF-8"?>
<Error>
    <Code>InvalidArgument</Code>
    <Message>no such bucket access control exists</Message>
    <RequestId>5***9</RequestId>
    <HostId>***-test.example.com</HostId>
    <ArgumentName>x-oss-acl</ArgumentName>
    <ArgumentValue>error-acl</ArgumentValue>
</Error>
```


## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/manage-the-acl-of-a-bucket#section-za5-bj6-495 "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-acl-using-oss-sdk-for-python-v2 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-manage-bucket-acls "")

- [C++](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-acls-2#section-91l-4ge-djo "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/php-v2-manage-the-acl-of-a-bucket "")

- [C](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-acls-5#section-hqc-qko-onk "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-acls-3#section-rul-ig0-7ge "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/manage-the-acl-of-a-bucket-2#section-u46-dpo-nso "")


## **命令行工具ossutil**

PutBucketAcl接口所对应的ossutil命令，请参见 [put-bucket-acl](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-access-permissions "")。

## 错误码

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| AccessDenied | 403 | - 发起PutBucketAcl请求时，没有传入用户验证信息。<br>  <br>- 没有发起PutBucketAcl请求的权限。 |