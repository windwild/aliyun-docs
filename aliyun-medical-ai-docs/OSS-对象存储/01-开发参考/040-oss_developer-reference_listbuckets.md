### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Service操作](https://help.aliyun.com/zh/oss/developer-reference/service-operations/)ListBuckets（GetService）

# ListBuckets（GetService）

更新时间：2025-05-06 05:24:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

请求语法

请求头

请求参数

响应头

响应元素

示例

SDK

命令行工具ossutil

错误码

调用ListBuckets（GetService）接口列举请求者拥有的所有存储空间（Bucket）。您还可以通过设置prefix、marker或者max-keys参数列举满足指定条件的存储空间。

## 注意事项

如果您需要列举OSS Bucket，您必须拥有`oss:ListBuckets`权限。

如果您需要列举云盒Bucket，您需要拥有`oss-cloudbox:ListBuckets`权限。

具体操作，请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

## 请求语法

```plaintext
GET / HTTP/1.1
Host: oss.example.com
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
| x-oss-resource-group-id | 字符串 | 否 | rg-aek27tc\*\*\*\*\*\*\*\* | 指定资源组ID。<br>- 如果在请求中携带该请求头并指定资源组ID，则OSS会返回属于该资源组的所有Bucket。<br>  <br>  当指定的资源组ID为rg-default-id时，OSS会返回属于默认资源组的所有Bucket。<br>  <br>- 如果在请求中携带了该请求头但未指定资源组ID，则OSS会返回属于默认资源组的所有Bucket。<br>  <br>- 如果在请求中未携带该请求头，则OSS会返回请求者拥有的所有Bucket。<br>  <br>您可以通过资源管理的控制台或ListResourceGroups接口获取资源组ID。具体操作，请分别参见 [查看资源组基本信息](https://help.aliyun.com/zh/resource-management/resource-group/user-guide/view-basic-information-of-a-resource-group#task-2398293 "") 和 [ListResourceGroups](https://help.aliyun.com/zh/resource-management/api-listresourcegroups#doc-api-ResourceManager-ListResourceGroups "")。 |

此接口涉及的其他公共请求头，例如Host、Date等的更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 请求参数

| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| prefix | 字符串 | 否 | my | 限定返回的Bucket名称必须以prefix作为前缀。如果不设定，则不过滤前缀信息。 <br>默认值：无 |
| marker | 字符串 | 否 | mybucket10 | 设定结果从marker之后按字母排序的第一个开始返回。如果不设定，则从头开始返回数据。 <br>默认值：无 |
| max-keys | Integer | 否 | 10 | 限定此次返回Bucket的最大个数。<br>取值范围：1~1000<br>默认值：100 |

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 响应元素

**说明**

调用ListBuckets（GetService）接口时，如果所有Bucket已返回，则返回的XML中不包含Prefix、Marker、MaxKeys、IsTruncated和NextMarker响应元素。

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| ListAllMyBucketsResult | 容器 | 不涉及 | 保存ListBuckets（GetService）请求结果的容器。 <br>子节点：Owner、Buckets<br>父节点：None |
| Prefix | 字符串 | my | 本次查询结果的前缀。 <br>父节点：ListAllMyBucketsResult |
| Marker | 字符串 | mybucket | 表示本次ListBuckets（GetService）的起点。<br>父节点：ListAllMyBucketsResult |
| MaxKeys | 字符串 | 10 | 响应请求内返回结果的最大个数。 <br>父节点：ListAllMyBucketsResult |
| IsTruncated | 枚举字符串 | true | 是否所有的结果都已经返回。 取值范围如下：<br>- true：表示本次没有返回全部结果。<br>  <br>- false：表示本次已经返回了全部结果。<br>  <br>父节点：ListAllMyBucketsResult |
| NextMarker | 字符串 | mybucket10 | 用于继续查询时给marker赋值。表示下一次ListBuckets（GetService）可以以此为marker，将未返回的结果返回。 <br>父节点：ListAllMyBucketsResult |
| Owner | 容器 | 不涉及 | 用于存放Bucket拥有者信息的容器。 <br>父节点：ListAllMyBucketsResult |
| ID | 字符串 | ut\_test\_put\_bucket | Bucket拥有者的用户ID。 <br>父节点：ListAllMyBucketsResult.Owner |
| DisplayName | 字符串 | ut\_test\_put\_bucket | Bucket拥有者的名称 （目前和ID一致）。 <br>父节点：ListAllMyBucketsResult.Owner |
| Buckets | 容器 | 不涉及 | 保存多个Bucket信息的容器。 <br>子节点：Bucket<br>父节点：ListAllMyBucketsResult |
| Bucket | 容器 | 不涉及 | 保存Bucket信息的容器。 <br>子节点：Name, CreationDate, Location<br>父节点：ListAllMyBucketsResult.Buckets |
| Name | 字符串 | mybucket01 | Bucket名称。 <br>父节点：ListAllMyBucketsResult.Buckets.Bucket |
| CreationDate | 时间 | 2014-05-15T11:18:32.000Z | Bucket创建时间。格式为`yyyy-mm-ddThh:mm:ss.timezone`。<br>父节点：ListAllMyBucketsResult.Buckets.Bucket |
| Location | 字符串 | oss-cn-hangzhou | OSS专用Region ID。 <br>父节点：ListAllMyBucketsResult.Buckets.Bucket |
| ExtranetEndpoint | 字符串 | oss-cn-hangzhou.aliyuncs.com | 外网访问域名。 <br>父节点：ListAllMyBucketsResult.Buckets.Bucket |
| IntranetEndpoint | 字符串 | oss-cn-hangzhou-internal.aliyuncs.com | 内网访问域名。 <br>父节点：ListAllMyBucketsResult.Buckets.Bucket |
| Region | 字符串 | cn-hangzhou | 阿里云通用Region ID。<br>父节点：ListAllMyBucketsResult.Buckets.Bucket |
| StorageClass | 字符串 | Standard | Bucket存储类型，支持Standard、IA、Archive、ColdArchive和DeepColdArchive多种存储类型。<br>父节点：ListAllMyBucketsResult.Buckets.Bucket |
| ResourceGroupId | 字符串 | rg-aek27tc\*\*\*\*\*\*\*\* | Bucket所属资源组ID。如果Bucket属于默认资源组，则返回值为rg-default-id。<br>父节点：ListAllMyBucketsResult.Buckets.Bucket |

## 示例

- 获取请求者拥有的所有Bucket



请求示例

















```plaintext
GET / HTTP/1.1
Date: Thu, 15 May 2014 11:18:32 GMT
Host: oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=host,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```







返回示例

















```plaintext
HTTP/1.1 200 OK
Date: Thu, 15 May 2014 11:18:32 GMT
Content-Type: application/xml
Content-Length: 556
Connection: keep-alive
Server: AliyunOSS
x-oss-request-id: 5374A2880232A65C2300****
<?xml version="1.0" encoding="UTF-8"?>
<ListAllMyBucketsResult>
    <Owner>
      <ID>512**</ID>
      <DisplayName>51264</DisplayName>
    </Owner>
    <Buckets>
      <Bucket>
        <CreationDate>2014-02-17T18:12:43.000Z</CreationDate>
        <ExtranetEndpoint>oss-cn-shanghai.aliyuncs.com</ExtranetEndpoint>
        <IntranetEndpoint>oss-cn-shanghai-internal.aliyuncs.com</IntranetEndpoint>
        <Location>oss-cn-shanghai</Location>
        <Name>app-base-oss</Name>
        <Region>cn-shanghai</Region>
        <StorageClass>Standard</StorageClass>
      </Bucket>
      <Bucket>
        <CreationDate>2014-02-25T11:21:04.000Z</CreationDate>
        <ExtranetEndpoint>oss-cn-hangzhou.aliyuncs.com</ExtranetEndpoint>
        <IntranetEndpoint>oss-cn-hangzhou-internal.aliyuncs.com</IntranetEndpoint>
        <Location>oss-cn-hangzhou</Location>
        <Name>mybucket</Name>
        <Region>cn-hangzhou</Region>
        <StorageClass>IA</StorageClass>
      </Bucket>
    </Buckets>
</ListAllMyBucketsResult>
```

- 根据指定前缀、最大返回个数等获取Bucket



请求示例

















```plaintext
GET /?prefix=my&max-keys=10 HTTP/1.1
Date: Thu, 15 May 2014 11:18:32 GMT
Host: oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=host,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```







返回示例

















```plaintext
HTTP/1.1 200 OK
Date: Thu, 15 May 2014 11:18:32 GMT
Content-Type: application/xml
Content-Length: 545
Connection: keep-alive
Server: AliyunOSS
x-oss-request-id: 5374A2880232A65C2300****
<?xml version="1.0" encoding="UTF-8"?>
<ListAllMyBucketsResult>
    <Prefix>my</Prefix>
    <Marker>mybucket</Marker>
    <MaxKeys>10</MaxKeys>
    <IsTruncated>true</IsTruncated>
    <NextMarker>mybucket10</NextMarker>
    <Owner>
      <ID>ut_test_put_bucket</ID>
      <DisplayName>ut_test_put_bucket</DisplayName>
    </Owner>
    <Buckets>
      <Bucket>
        <CreationDate>2014-05-14T11:18:32.000Z</CreationDate>
        <ExtranetEndpoint>oss-cn-hangzhou.aliyuncs.com</ExtranetEndpoint>
        <IntranetEndpoint>oss-cn-hangzhou-internal.aliyuncs.com</IntranetEndpoint>
        <Location>oss-cn-hangzhou</Location>
        <Name>mybucket01</Name>
        <Region>cn-hangzhou</Region>
        <StorageClass>Standard</StorageClass>
      </Bucket>
    </Buckets>
</ListAllMyBucketsResult>
```

- 获取指定资源组中的所有Bucket



请求示例

















```plaintext
GET / HTTP/1.1
Date: Thu, 15 May 2014 11:18:32 GMT
Host: oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=host,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
x-oss-resource-group-id: rg-aek27tc********
```







返回示例

















```plaintext
HTTP/1.1 200 OK
Date: Thu, 15 May 2014 11:18:32 GMT
Content-Type: application/xml
Content-Length: 556
Connection: keep-alive
Server: AliyunOSS
x-oss-request-id: 5374A2880232A65C2300****
<?xml version="1.0" encoding="UTF-8"?>
<ListAllMyBucketsResult>
    <Owner>
      <ID>512**</ID>
      <DisplayName>51264</DisplayName>
    </Owner>
    <Buckets>
      <Bucket>
        <CreationDate>2014-02-07T18:12:43.000Z</CreationDate>
        <ExtranetEndpoint>oss-cn-shanghai.aliyuncs.com</ExtranetEndpoint>
        <IntranetEndpoint>oss-cn-shanghai-internal.aliyuncs.com</IntranetEndpoint>
        <Location>oss-cn-shanghai</Location>
        <Name>test-bucket-1</Name>
        <Region>cn-shanghai</Region>
        <StorageClass>Standard</StorageClass>
        <ResourceGroupId>rg-aek27tc********</ResourceGroupId>
      </Bucket>
      <Bucket>
        <CreationDate>2014-02-05T11:21:04.000Z</CreationDate>
        <ExtranetEndpoint>oss-cn-hangzhou.aliyuncs.com</ExtranetEndpoint>
        <IntranetEndpoint>oss-cn-hangzhou-internal.aliyuncs.com</IntranetEndpoint>
        <Location>oss-cn-hangzhou</Location>
        <Name>test-bucket-2</Name>
        <Region>cn-hangzhou</Region>
        <StorageClass>IA</StorageClass>
        <ResourceGroupId>rg-aek27tc********</ResourceGroupId>
      </Bucket>
    </Buckets>
</ListAllMyBucketsResult>
```

- 获取默认资源组中的所有Bucket



请求示例

















```plaintext
GET / HTTP/1.1
Date: Thu, 15 May 2014 11:18:32 GMT
Host: oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=host,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
x-oss-resource-group-id：rg-default-id
```







返回示例

















```plaintext
HTTP/1.1 200 OK
Date: Thu, 15 May 2014 11:18:32 GMT
Content-Type: application/xml
Content-Length: 556
Connection: keep-alive
Server: AliyunOSS
x-oss-request-id: 5374A2880232A65C2300****
<?xml version="1.0" encoding="UTF-8"?>
<ListAllMyBucketsResult>
    <Owner>
      <ID>512**</ID>
      <DisplayName>51264</DisplayName>
    </Owner>
    <Buckets>
      <Bucket>
        <CreationDate>2014-02-07T18:12:43.000Z</CreationDate>
        <ExtranetEndpoint>oss-cn-shanghai.aliyuncs.com</ExtranetEndpoint>
        <IntranetEndpoint>oss-cn-shanghai-internal.aliyuncs.com</IntranetEndpoint>
        <Location>oss-cn-shanghai</Location>
        <Name>test-bucket-3</Name>
        <Region>cn-shanghai</Region>
        <StorageClass>Standard</StorageClass>
        <ResourceGroupId>rg-default-id</ResourceGroupId>
      </Bucket>
      <Bucket>
        <CreationDate>2014-02-05T11:21:04.000Z</CreationDate>
        <ExtranetEndpoint>oss-cn-hangzhou.aliyuncs.com</ExtranetEndpoint>
        <IntranetEndpoint>oss-cn-hangzhou-internal.aliyuncs.com</IntranetEndpoint>
        <Location>oss-cn-hangzhou</Location>
        <Name>test-bucket-4</Name>
        <Region>cn-hangzhou</Region>
        <StorageClass>IA</StorageClass>
        <ResourceGroupId>rg-default-id</ResourceGroupId>
      </Bucket>
    </Buckets>
</ListAllMyBucketsResult>
```


## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/list-buckets#concept-2348405 "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-using-oss-sdk-for-python-v2 "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/php-v2-list-buckets "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-list-buckets "")

- [C](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-9#concept-2365059 "")

- [C++](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-3#concept-2351976 "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-using-oss-sdk-for-csharp-v1#concept-2372520 "")

- [iOS](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-10#concept-2056668 "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-8#concept-2380378 "")

- [Ruby](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-7#concept-2382491 "")


## **命令行工具ossutil**

ListBuckets接口所对应的ossutil命令，请参见 [list-buckets（get-service）](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-get-service "")。

## 错误码

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| AccessDenied | 403 | 请求中没有用户验证信息（即匿名访问）。 |