### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[权限控制（ACL）](https://help.aliyun.com/zh/oss/developer-reference/acl/)GetBucketAcl

# GetBucketAcl

更新时间：2025-05-06 05:20:28

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

请求语法

请求头

响应元素

示例

SDK

命令行工具ossutil

错误码

GetBucketAcl接口用于获取某个存储空间（Bucket）的访问权限（ACL）。

## **注意事项**

获取某个存储空间（Bucket）的访问权限（ACL），您必须拥有`oss:GetBucketAcl`权限。具体操作，请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

## 请求语法

```plaintext
GET /?acl HTTP/1.1
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

当您在OSS ON云盒中调用该接口时，您需要将Host替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

### 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应元素

| **名称** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **类型** | **描述** |
| AccessControlList | 容器 | 存储ACL信息的容器类。<br>父节点：AccessControlPolicy |
| AccessControlPolicy | 容器 | 保存GetBucketACL结果的容器<br>父节点：None |
| DisplayName | 字符串 | Bucket拥有者的名称（目前和用户ID一致）。<br>父节点：AccessControlPolicy.Owner |
| Grant | 枚举字符串 | Bucket的ACL权限。<br>有效值：private、public-read、public-read-write<br>父节点：AccessControlPolicy.AccessControlList |
| ID | 字符串 | Bucket拥有者的用户ID。<br>父节点：AccessControlPolicy.Owner |
| Owner | 容器 | 保存Bucket拥有者信息的容器。<br>父节点：AccessControlPolicy |

## 示例

请求示例

```plaintext
GET /?acl HTTP/1.1
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Thu, 17 Apr 2025 04:11:23 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e

```

返回示例

```plaintext
HTTP/1.1 200 OK
x-oss-request-id: 534B371674E88A4D8906****
Date: Fri, 24 Feb 2012 04:11:23 GMT
Content-Length: 253
Content-Type: application/xml
Connection: keep-alive
Server: AliyunOSS

<?xml version="1.0" ?>
<AccessControlPolicy>
    <Owner>
        <ID>0022012****</ID>
        <DisplayName>user_example</DisplayName>
    </Owner>
    <AccessControlList>
        <Grant>public-read</Grant>
    </AccessControlList>
</AccessControlPolicy>
```

## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/manage-the-acl-of-a-bucket#section-9vy-z0n-kix "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/create-bucket-using-oss-sdk-for-python-v2 "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/php-v2-create-bucket "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-create-bucket "")

- [C](https://help.aliyun.com/zh/oss/developer-reference/create-a-bucket-1#concept-32135-zh "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/create-buckets-using-oss-sdk-for-csharp-v1#concept-32089-zh "")

- [Android](https://help.aliyun.com/zh/oss/developer-reference/create-buckets-using-oss-sdk-for-csharp-v1#concept-32089-zh "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/create-a-bucket-4#concept-32071-zh "")

- [Ruby](https://help.aliyun.com/zh/oss/developer-reference/create-a-bucket-2#concept-32116-zh "")


## **命令行工具ossutil**

GetBucketAcl接口所对应的ossutil命令，请参见 [get-bucket-acl](https://help.aliyun.com/zh/oss/developer-reference/get-bucket-acl "")。

## 错误码

| **错误码** | **HTTP 状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP 状态码** | **描述** |
| NoSuchBucket | 404 | 目标Bucket不存在。 |
| AccessDenied | 403 | 没有操作权限。只有Bucket的拥有者才能获取Bucket的访问权限。 |