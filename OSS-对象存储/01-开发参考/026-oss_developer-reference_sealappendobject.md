### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Object操作](https://help.aliyun.com/zh/oss/developer-reference/object-operations/)[基础操作](https://help.aliyun.com/zh/oss/developer-reference/basic-operations-1/)SealAppendObject

# SealAppendObject

更新时间：2025-12-01 00:50:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

权限说明

和其他操作的关系

请求语法

请求参数

请求头

响应头

示例

请求示例

响应示例

错误码

如果您希望停止向一个Appendable Object继续追加内容，可以调用SealAppendObject接口。执行该操作后，Object将变为非追加状态。这允许您通过生命周期（Lifecycle）规则将该Object的存储类型转换为冷归档（Cold Archive）或深度冷归档（Deep Cold Archive）存储，从而进一步节省存储成本。未执行此操作前，Appendable Object仅支持转换为低频访问（Infrequent Access）或归档（Archive）存储。

**重要**

如需调用SealAppendObject接口，请 [提交工单](https://smartservice.console.aliyun.com/service/list) 申请。

## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

| **API** | **Action** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **API** | **Action** | **说明** |
| SealAppendObject | `oss:SealAppendObject` | 停止对某个Appendable Object继续追加内容，并将其转为非追加状态。 |

## **和其他操作的关系**

| **操作** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **操作** | **说明** |
| [HeadObject](https://help.aliyun.com/zh/oss/developer-reference/headobject#reference-bgh-cbw-wdb "") | 对于已执行过SealAppendObject操作的Object，HeadObject会返回x-oss-sealed-time，否则不会返回。 |
| [GetObject](https://help.aliyun.com/zh/oss/developer-reference/getobject "") | 对于已执行过SealAppendObject操作的Object，GetObject会返回x-oss-sealed-time，否则不会返回。 |
| [生命周期](https://help.aliyun.com/zh/oss/user-guide/overview-54/ "") | 生命周期服务在执行存储类型转换操作时，默认不支持将追加上传生成的Appendable类型的Object转换为冷归档存储或者深度冷归档存储类型。但对于已停止写入的Appendable Object，则允许将其转为冷归档存储类型或深度冷归档存储类型。 |

## **请求语法**

```http
POST /ObjectName?seal&position=Position HTTP/1.1
Host: BucketName.oss.aliyuncs.com
Content-Length: 0
Date: GMT Date
Authorization: SignatureValue
```

## **请求参数**

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| seal | 字符串 | 是 | 用于发起SealAppendObject操作。 |
| position | 字符串 | 是 | 指定执行SealAppendObject操作时Object的预期长度。OSS会检查此长度与Object的实际长度是否一致。如果不一致，请求将失败并返回PositionNotEqualToLength错误。 |

## 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## **响应头**

| **响应消息头** | **类型** | **示例** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **响应消息头** | **类型** | **示例** | **描述** |
| **x-oss-sealed-time** | 字符串 | Wed, 07 May 2025 23:00:00 GMT | Object首次执行SealAppendObject操作的时间（GMT格式）。即使该操作被重复执行，此时间戳也不会改变。 |

## **示例**

### **请求示例**

```http
POST /test.jpg?seal&position=344606 HTTP/1.1
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Wed, 07 May 2025 23:00:00 GMT
Content-Length: 0
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250507/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3****
```

### **响应示例**

```http
HTTP/1.1 200 OK
x-oss-request-id: 559CC9BDC755F95A6448****
x-oss-object-type: Appendable
x-oss-storage-class: Standard
x-oss-sealed-time: Wed, 07 May 2025 23:00:00 GMT
Date: Wed, 07 May 2025 23:00:00 GMT
Last-Modified: Mon, 07 Apr 2025 07:32:52 GMT
ETag: "fba9dede5f27731c9771645a3986****"
Content-Length: 344606
Content-Type: image/jpg
Connection: keep-alive
Server: AliyunOSS
```

## **错误码**

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| AppendSealedObjectNotAllowed | 409 | 对一个非Appendable Object进行SealAppendObject操作。 |
| PositionNotEqualToLength | 409 | 请求参数中的position和文件实际长度不同。 |