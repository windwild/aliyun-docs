### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于LiveChannel的操作](https://help.aliyun.com/zh/oss/developer-reference/livechannel-operations/)ListLiveChannel

# ListLiveChannel

更新时间：2025-04-25 04:33:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PutLiveChannel](https://help.aliyun.com/zh/oss/developer-reference/putlivechannel)[下一篇：DeleteLiveChannel](https://help.aliyun.com/zh/oss/developer-reference/deletelivechannel)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求语法

请求元素

响应元素

示例

SDK

ListLiveChannel接口用于列举指定的LiveChannel。

## 请求语法

```plaintext
GET /?live HTTP/1.1
Date: GMT date
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Authorization: SignatureValue
```

## 请求元素

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| marker | 字符串 | 否 | 设定结果从marker之后按字母排序的第一个开始返回。 |
| max-keys | 字符串 | 否 | 限定此次返回LiveChannel的最大数。<br>取值：大于0小于等于1000<br>默认值：100 |
| prefix | 字符串 | 否 | 限定返回的LiveChannel必须以prefix作为前缀。使用prefix查询时，返回的key中仍会包含prefix。 |

此接口还需要包含Host、Date等公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应元素

| **名称** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **类型** | **描述** |
| ListLiveChannelResult | 容器 | 保存ListLiveChannel请求结果的容器。 <br>子节点：Prefix、Marker、MaxKeys、IsTruncated、NextMarker、LiveChannel<br>父节点：无 |
| Prefix | 字符串 | 本次查询结果的开始前缀。 <br>子节点：无<br>父节点：ListLiveChannelResult |
| Marker | 字符串 | 本次ListLiveChannel的起点。 <br>子节点：无<br>父节点：ListLiveChannelResult |
| MaxKeys | 字符串 | 响应请求内返回结果的最大数目。 <br>子节点：无<br>父节点：ListLiveChannelResult |
| IsTruncated | 字符串 | 是否已返回所有的结果。 <br>- true：表示本次请求已返回全部结果。<br>  <br>- false：表示本次请求未返回全部结果。<br>  <br>子节点：无<br>父节点：ListLiveChannelResult |
| NextMarker | 字符串 | 如果本次没有返回全部结果，响应请求中将包含NextMarker元素，用于标明接下来请求的Marker值。 <br>子节点：无<br>父节点：ListLiveChannelResult |
| LiveChannel | 容器 | 保存返回每个LiveChannel信息的容器。 <br>子节点：Name、Description、Status、LastModified、PublishUrls、PlayUrls<br>父节点：ListLiveChannelResult |
| Name | 字符串 | LiveChannel的名称。 <br>子节点：无<br>父节点：LiveChannel |
| Description | 字符串 | LiveChannel的描述信息。 <br>子节点：无<br>父节点：LiveChannel |
| Status | 枚举字符串 | LiveChannel的状态。 <br>子节点：无<br>父节点：LiveChannel<br>有效值：<br>- disabled：表示禁用LiveChannel。<br>  <br>- enabled：表示启用LiveChannel。 |
| LastModified | 字符串 | LiveChannel配置的最后修改时间。 <br>格式：ISO8601<br>子节点：无<br>父节点：LiveChannel |
| PublishUrls | 容器 | 保存LiveChannel对应的推流地址的容器。 <br>子节点：Url<br>父节点：LiveChannel |
| Url | 字符串 | LiveChannel对应的推流地址。 <br>子节点：无<br>父节点：PublishUrls |
| PlayUrls | 容器 | 保存LiveChannel对应的播放地址的容器。 <br>子节点：Url<br>父节点：LiveChannel |
| Url | 字符串 | LiveChannel对应的播放地址。 <br>子节点：无<br>父节点：PlayUrls |

此接口还包含ETag、x-oss-request-id等公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

请求示例

```plaintext
GET /?live&max-keys=1 HTTP/1.1
Date: Thu, 25 Aug 2016 07:50:09 GMT
Host: test-bucket.oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

```plaintext
HTTP/1.1 200
content-length: 656
server: AliyunOSS
connection: close
x-oss-request-id: 57BEA331B92475920B00****
date: Thu, 25 Aug 2016 07:50:09 GMT
content-type: application/xml

<?xml version="1.0" encoding="UTF-8"?>
<ListLiveChannelResult>
  <Prefix></Prefix>
  <Marker></Marker>
  <MaxKeys>1</MaxKeys>
  <IsTruncated>true</IsTruncated>
  <NextMarker>channel-0</NextMarker>
  <LiveChannel>
    <Name>channel-0</Name>
    <Description></Description>
    <Status>disabled</Status>
    <LastModified>2016-07-30T01:54:21.000Z</LastModified>
    <PublishUrls>
      <Url>rtmp://test-bucket.oss-cn-hangzhou.aliyuncs.com/live/channel-0</Url>
    </PublishUrls>
    <PlayUrls>
      <Url>http://test-bucket.oss-cn-hangzhou.aliyuncs.com/channel-0/playlist.m3u8</Url>
    </PlayUrls>
  </LiveChannel>
</ListLiveChannelResult>
```

## SDK

- [Java](https://help.aliyun.com/zh/oss/developer-reference/common-operations-of-oss-sdk-for-java-on-livechannels#concept-995188 "")

- [Python](https://help.aliyun.com/zh/oss/developer-reference/common-operations-of-oss-sdk-for-python-on-livechannels#concept-2366400 "")

- [Go](https://help.aliyun.com/zh/oss/developer-reference/common-operations-on-livechannels-1#concept-2164037 "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/common-operations-on-livechannels#concept-2161611 "")