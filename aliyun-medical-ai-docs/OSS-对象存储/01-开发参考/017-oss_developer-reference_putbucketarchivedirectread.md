### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[归档直读（ArchiveDirectRead）](https://help.aliyun.com/zh/oss/developer-reference/archivedirect-reading/)PutBucketArchiveDirectRead

# PutBucketArchiveDirectRead

更新时间：2025-04-25 03:58:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DeleteAccessPointPublicAccessBlock](https://help.aliyun.com/zh/oss/developer-reference/deleteaccesspointpublicaccessblock)[下一篇：GetBucketArchiveDirectRead](https://help.aliyun.com/zh/oss/developer-reference/getbucketarchivedirectread)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

请求语法

请求头

请求元素

响应头

示例

命令行工具ossutil

调用PutBucketArchiveDirectRead接口为Bucket开启或关闭归档直读。

## **注意事项**

- 要为Bucket开启归档直读，您必须有`oss:PutBucketArchiveDirectRead`权限。具体操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

- 每个地域都有对应的访问域名（Endpoint）。关于地域与访问域名对应关系的更多信息，请参见 [访问域名和数据中心](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")。

- 开启归档直读后，直接读取归档存储类型的文件，会产生归档直读数据取回容量（RetrievalDataArchiveDirect）费用。对于已经解冻的归档存储类型的文件，不会产生归档直读数据取回容量费用。详情请参见 [数据处理费用](https://help.aliyun.com/zh/oss/data-processing-fees "")。


## **请求语法**

```http
PUT /?bucketArchiveDirectRead HTTP/1.1
Date: GMT Date
Content-Length：ContentLength
Content-Type: application/xml
Authorization: SignatureValue
Host: BucketName.oss-cn-hangzhou.aliyuncs.com

<?xml version="1.0" encoding="UTF-8"?>
<ArchiveDirectReadConfiguration>
    <Enabled>true</Enabled>
</ArchiveDirectReadConfiguration>
```

## **请求头**

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## **请求元素**

| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| ArchiveDirectReadConfiguration | 容器 | 是 | 不涉及 | Bucket归档直读配置。 |
| Enabled | 布尔型 | 是 | true | 是否为Bucket开启归档直读。取值如下：<br>- true：开启归档直读。<br>  <br>- false：关闭归档直读。 |

## **响应头**

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## **示例**

- 请求示例















```http
PUT /?bucketArchiveDirectRead HTTP/1.1
Date: Mon, 24 Apr 2023 15:56:37 GMT
Content-Length：60
Content-Type: application/xml
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=content-length,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
Host: oss-example.oss-cn-hangzhou.aliyuncs.com

<?xml version="1.0" encoding="UTF-8"?>
<ArchiveDirectReadConfiguration>
      <Enabled>true</Enabled>
</ArchiveDirectReadConfiguration>
```

- 返回示例















```http
HTTP/1.1 200 OK
x-oss-request-id: 534B371674E88A4D8906****
Date: Mon, 24 Apr 2023 15:56:37 GMT
Content-Length: 60
Connection: keep-alive
Server: AliyunOSS
```


## **命令行工具ossutil**

PutBucketArchiveDirectRead接口所对应的ossutil命令，请参见 [put-bucket-archive-direct-read](https://help.aliyun.com/zh/oss/developer-reference/put-bucket-archive-direct-read "")。