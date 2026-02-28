### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[阻止公共访问（BlockAccess）](https://help.aliyun.com/zh/oss/developer-reference/bllock-public-access-api/)[Bucket级别阻止公共访问](https://help.aliyun.com/zh/oss/developer-reference/block-public-access-at-the-bucket-level/)DeleteBucketPublicAccessBlock

# DeleteBucketPublicAccessBlock

更新时间：2025-04-25 03:57:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetBucketPublicAccessBlock](https://help.aliyun.com/zh/oss/developer-reference/getbucketpublicaccessblock)[下一篇：PutAccessPointPublicAccessBlock](https://help.aliyun.com/zh/oss/developer-reference/putaccesspointpublicaccessblock)

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

调用DeleteBucketPublicAccessBlock接口删除指定Bucket的阻止公共访问配置信息。

## **注意事项**

阿里云账号默认拥有删除指定Bucket的阻止公共访问配置信息的权限。如果您希望通过RAM用户或者STS的方式删除指定Bucket的阻止公共访问的配置信息，您必须拥有`oss:DeleteBucketPublicAccessBlock`权限。具体操作，请参见 [RAM Policy常见示例](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

## **请求语法**

```http
DELETE /?publicAccessBlock HTTP/1.1
Date: GMT Date
Content-Length：ContentLength
Content-Type: application/xml
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Authorization: SignatureValue
```

## 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅包含公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## **示例**

- 请求示例















```http
DELETE /?publicAccessBlock HTTP/1.1
Date: Mon, 19 Feb 2024 08:40:17 GMT
Content-Length：0
Content-Type: application/xml
Host: examplebucket.oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=content-length,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

- 返回示例















```http
HTTP/1.1 204 OK
x-oss-request-id: 534B371674E88A4D8906****
Date: Mon, 19 Feb 2024 08:40:17 GMT
Server: AliyunOSS
```


## SDK

本接口对应的SDK如下：

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/blocking-public-access-at-the-bucket-level-using-oss-sdk-for-python-v2#a7cc6eae2a0qz "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/blocking-public-access-at-the-bucket-level-using-oss-sdk-for-go-v2 "")


## **命令行工具ossutil**

DeleteBucketPublicAccessBlock接口所对应的ossutil命令，请参见 [delete-bucket-public-access-block](https://help.aliyun.com/zh/oss/developer-reference/delete-bucket-public-access-block "")。