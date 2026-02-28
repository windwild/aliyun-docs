### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于向量Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/apis-for-operations-on-vector-buckets/)[索引 Index](https://help.aliyun.com/zh/oss/developer-reference/vector-index-api/)PutVectorIndex

# PutVectorIndex

更新时间：2026-02-09 22:03:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

权限说明

请求语法

请求头

请求参数

响应头

示例

SDK

命令行工具ossutil

错误码

调用PutVectorIndex接口在向量存储空间中创建向量索引。

## 注意事项

- 单个向量 Bucket 中最多可创建 100 张向量索引，若需调大该配额，可以联系[技术支持](https://selfservice.console.aliyun.com/ticket/createIndex)申请调整。

- 向量索引 PutVectorIndex 请求每秒最大支持 5 个。


## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

| **API** | **Action** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **API** | **Action** | **说明** |
| PutVectorIndex | `oss:PutVectorIndex` | 创建向量索引。 |

## 请求语法

```plaintext
POST /?putVectorIndex HTTP/1.1
Host: examplebucket-123***456.cn-hangzhou.oss-vectors.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
Content-type: application/json

{
   "dataType": "string",
   "dimension": int,
   "distanceMetric": "string",
   "indexName": "string",
   "metadata": {
      "nonFilterableMetadataKeys": [string, string]
   }
}
```

## 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共HTTP头定义](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 请求参数

| **名称** | **数据类型** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **数据类型** | **是否必选** | **示例值** | **描述** |
| **dataType** | 字符串 | 是 | float32 | 向量数据类型，当前用户不可选。默认值：float32。 |
| **dimension** | 数值 | 是 | 512 | 向量维度，支持1~4096维。默认为512。 |
| **distanceMetric** | 字符串 | 是 | euclidean | 距离度量函数，可选值如下：<br>- euclidean：欧氏距离（默认值）<br>  <br>- cosine：余弦距离 |
| **indexName** | 字符串 | 是 | vectorindex1 | 索引名称，用户可自定义，默认为空。<br>- 在 Vector Bucket 内全局唯一，长度 1 ～63 字符<br>  <br>- 只允许字母和数字，首字母必须字母开头 |
| **metadata** | 对象 | 否 | - | 元数据配置的容器，仅支持填写非过滤元数据。 |
| **nonFilterableMetadataKeys** | 字符串数组 | 否 | \["field1", "field2"\] | 非过滤元数据配置。有如下输入限制：<br>- 元数据个数为 1~10 个<br>  <br>- 每个元数据主键名称的长度 1~63 字节，支持大小写字母、数字和下划线(\_)，且起始字符只能是大小写字母和下划线(\_)<br>  <br>父节点：metadata |

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共HTTP头定义](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

请求示例

```plaintext
POST /?putVectorIndex HTTP/1.1
Host: examplebucket-123***456.cn-hangzhou.oss-vectors.aliyuncs.com
Date: Thu, 17 Apr 2025 01:33:47 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218
Content-type: application/json

{
   "dataType": "float32",
   "dimension": 1024,
   "distanceMetric": "euclidean",
   "indexName": "vectorindex1",
   "metadata": {
      "nonFilterableMetadataKeys": ["category", "timestamp"]
   }
}
```

返回示例

```plaintext
HTTP/1.1 200 OK
x-oss-request-id: 534B371674E88A4D8906****
Date: Thu, 17 Apr 2025 01:33:47 GMT
Connection: keep-alive
Server: AliyunOSS
```

## **SDK**

PutVectorIndex接口所对应的各语言SDK如下：

- [创建向量 Index（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/put-vector-index-python-sdk-2-0 "")

- [创建向量Index（Go SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/put-vector-index-go-sdk-v2 "")


## **命令行工具ossutil**

PutVectorIndex接口所对应的ossutil命令，请参见 [put-vector-index](https://help.aliyun.com/zh/oss/developer-reference/put-vector-index "")。

## 错误码

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| VectorIndexParameterInvalid | 400 | 请求中提供的向量索引参数不合法。 |
| MalformedJson | 400 | 请求体中的 JSON 格式不符合规范。 |
| VectorBucketIndexExceedLimit | 400 | 创建的索引数量已达到上限。单个向量 Bucket 最多允许创建 100 个向量索引。 |
| AccessDenied | 403 | 返回该错误的可能原因如下：<br>- 发起请求时没有传入用户验证信息。<br>  <br>- 没有操作权限。 |
| VectorBucketIndexAlreadyExist | 409 | 指定的索引名称已存在，无法重复创建。 |