### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[版本控制（Versioning）](https://help.aliyun.com/zh/oss/developer-reference/versioning-1/)GetBucketVersioning

# GetBucketVersioning

更新时间：2025-02-12 22:19:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求语法

请求头

响应头

响应元素

示例

SDK

命令行工具ossutil

错误码

GetBucketVersioning接口用于获取指定Bucket的版本控制状态。

## 请求语法

```plaintext
GET /?versioning HTTP/1.1
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

当您在OSS ON云盒中调用该接口时，您需要将Host替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

## 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 响应元素

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| VersioningConfiguration | 容器 | 不涉及 | 保存版本控制状态的容器。<br>子节点：Status<br>父节点：无 |
| Status | 字符串 | Enabled | 版本控制状态<br>父节点：VersioningConfiguration<br>有效值： <br>- Enabled：开启版本控制状态<br>  <br>- Suspended：暂停版本控制状态<br>  <br>**说明**<br>如果Bucket从未开启版本控制，则响应元素中不包含Status元素。 |

## 示例

请求示例

```plaintext
GET /?versioning HTTP/1.1
Host: bucket-versioning.oss-cn-hangzhou.aliyuncs.com
Date: Tue, 09 Apr 2019 02:28:18 GMT
Authorization: OSS qn6q**************:77Dv****************
```

返回示例

- 已开启版本控制的返回示例















```plaintext
HTTP/1.1 200 OK
x-oss-request-id: 5CAC0342B7AEADE01700****
Date: Tue, 09 Apr 2019 02:28:18 GMT
Content-Length: 121
Content-Type: application/xml
Connection: keep-alive
Server: AliyunOSS
<?xml version="1.0" encoding="UTF-8"?>
<VersioningConfiguration>
      <Status>Enabled</Status>
</VersioningConfiguration>
```

- 未曾开启版本控制的返回示例

如果该Bucket未曾开启版本控制状态，则XML中不会返回版本控制Status信息。















```plaintext
HTTP/1.1 200 OK
x-oss-request-id: 5CAC015CB7AEADE01700****
Date: Tue, 09 Apr 2019 02:20:12 GMT
Content-Length: 74
Content-Type: application/xml
Connection: keep-alive
Server: AliyunOSS
<VersioningConfiguration xmlns="http://doc.oss-cn-hangzhou.aliyuncs.com"/>
```


## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/versioning-8#concept-265070 "")

- [Python](https://help.aliyun.com/zh/oss/developer-reference/manage-versioning-2#concept-265070 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-manage-versioning-3 "")

- [C++](https://help.aliyun.com/zh/oss/developer-reference/manage-versioning#concept-2331567 "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/versioning-4#concept-2486979 "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/versioning-9#concept-2435967 "")


## **命令行工具ossutil**

GetBucketVersioning接口所对应的ossutil命令，请参见 [get-bucket-versioning](https://help.aliyun.com/zh/oss/developer-reference/get-bucket-versioning "")。

## 错误码

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| AccessDenied | 403 | 无权限查看Bucket的版本控制状态。<br>只有Bucket拥有者及授予了GetBucketVersioning权限的RAM用户才能查看Bucket的版本控制状态。 |
| NoSuchBucket | 404 | 访问的Bucket不存在。 |