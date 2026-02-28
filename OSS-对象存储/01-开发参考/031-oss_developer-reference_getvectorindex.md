### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [开发参考](https://help.aliyun.com/zh/oss/developer-reference/) [API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/) [关于向量Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/apis-for-operations-on-vector-buckets/) [索引 Index](https://help.aliyun.com/zh/oss/developer-reference/vector-index-api/) GetVectorIndex

# GetVectorIndex

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PutVectorIndex](https://help.aliyun.com/zh/oss/developer-reference/putvectorindex)[下一篇：ListVectorIndexes](https://help.aliyun.com/zh/oss/developer-reference/listvectorindexes)

该文章对您有帮助吗？

反馈

调用GetVectorIndex接口获取向量索引的详细信息。

## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

|     |     |     |
| --- | --- | --- |
| **API** | **Action** | **说明** |
| GetVectorIndex | `oss:GetVectorIndex` | 获取向量索引信息。 |

## 请求语法

```plaintext
POST /?getVectorIndex HTTP/1.1
Host: examplebucket-123***456.cn-hangzhou.oss-vectors.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
{
   "indexName": "string"
}
```

## **请求头**

此接口仅涉及公共请求头。更多信息，请参见 [公共HTTP头定义](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 请求参数

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **数据类型** | **是否必选** | **示例值** | **描述** |
| **indexName** | 字符串 | 是 | vectorindex1 | 索引名称。 |

## **响应头**

此接口仅涉及公共响应头。更多信息，请参见 [公共HTTP头定义](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 响应元素

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **数据类型** | **示例值** | **描述** |
| **index** | 容器 | - | 保存向量索引信息的容器。 |
| **indexName** | 字符串 | vectorindex1 | 索引名称。<br>父节点：index |
| **createTime** | 字符串 | 2025-04-17T10:56:21.000Z | 索引的创建时间，格式为GMT时间。<br>父节点：index |
| **dataType** | 字符串 | float32 | 向量数据类型。<br>父节点：index |
| **dimension** | 整型 | 1024 | 向量维度。<br>父节点：index |
| **distanceMetric** | 字符串 | euclidean | 距离度量函数。<br>父节点：index |
| **metadata** | 容器 | - | 元数据配置。<br>父节点：index |
| **nonFilterableMetadataKeys** | 字符串数组 | \["category", "timestamp"\] | 非过滤元数据字段列表。<br>父节点：metadata |
| **status** | 字符串 | enable | 索引当前的状态。取值：<br>- creating（创建中）<br>  <br>- enable（可用）<br>  <br>- deleting（删除中） |

## 示例

请求示例

```plaintext
POST /?getVectorIndex HTTP/1.1
Host: examplebucket-123***456.cn-hangzhou.oss-vectors.aliyuncs.com
Date: Thu, 17 Apr 2025 01:33:47 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218

{
   "indexName": "vectorindex1"
}
```

返回示例

```plaintext
HTTP/1.1 200 OK
x-oss-request-id: 534B371674E88A4D8906****
Date: Thu, 17 Apr 2025 01:33:47 GMT
Connection: keep-alive
Server: AliyunOSS
Content-type: application/json

{
   "index": {
      "createTime": "2025-04-17T10:56:21.000Z",
      "dataType": "float32",
      "dimension": 1024,
      "distanceMetric": "euclidean",
      "metadata": {
         "nonFilterableMetadataKeys": ["category", "timestamp"]
      },
      "status": "enable"
   }
}
```

## **SDK**

GetVectorIndex接口所对应的各语言SDK如下：

- [获取向量 Index 信息（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/get-vector-index-python-sdk-2-0 "")

- [获取向量Index信息（Go SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/get-vector-index-go-sdk-2-0 "")


## **命令行工具ossutil**

GetVectorIndex接口所对应的ossutil命令，请参见 [get-vector-index](https://help.aliyun.com/zh/oss/developer-reference/get-vector-index "")。

## 错误码

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| VectorIndexParameterInvalid | 400 | 请求中提供的向量索引参数不合法。 |
| MalformedJson | 400 | 请求体中的 JSON 格式不符合规范。 |
| AccessDenied | 403 | 返回该错误的可能原因如下：<br>- 发起请求时没有传入用户验证信息。<br>  <br>- 没有操作权限。 |
| NoSuchVectorIndex | 404 | 目标向量索引不存在。 |