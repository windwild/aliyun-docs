### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于LiveChannel的操作](https://help.aliyun.com/zh/oss/developer-reference/livechannel-operations/)GetLiveChannelInfo

# GetLiveChannelInfo

更新时间：2025-04-24 21:59:52

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

GetLiveChannelInfo接口用于获取指定LiveChannel的配置信息。

## 请求语法

```plaintext
GET /ChannelName?live HTTP/1.1
Date: GMT date
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Authorization: SignatureValue
```

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
| LiveChannelConfiguration | 容器 | 不涉及 | 保存GetLiveChannelInfo返回结果的容器。 <br>子节点：Description、Status、Target<br>父节点：无 |
| Description | 字符串 | test | LiveChannel的描述信息。 <br>子节点：无<br>父节点：LiveChannelConfiguration |
| Status | 枚举字符串 | enabled | LiveChannel的状态信息。 <br>子节点：无<br>父节点：LiveChannelConfiguration<br>有效值：<br>- enabled：启用状态<br>  <br>- disabled：禁用状态 |
| Target | 容器 | 不涉及 | 保存LiveChannel转储配置的容器。 <br>子节点：Type、FragDuration、FragCount、PlaylistName <br>**说明**<br>FragDuration、FragCount、PlaylistName只有当Type取值为HLS时才会返回。<br>父节点：LiveChannelConfiguration |
| Type | 枚举字符串 | HLS | 当Type为HLS时，指定推流时转储文件类型。 <br>子节点：无<br>父节点：Target<br>有效值：HLS |
| FragDuration | 字符串 | 2 | 当Type为HLS时，指定每个ts文件的时长。 <br>单位：秒<br>子节点：无<br>父节点：Target |
| FragCount | 字符串 | 3 | 当Type为HLS时，指定m3u8文件中包含ts文件的个数。 <br>子节点：无<br>父节点：Target |
| PlaylistName | 字符串 | playlist.m3u8 | 当Type为HLS时，指定生成的m3u8文件的名称。 <br>子节点：无<br>父节点：Target |

## 示例

请求示例

```plaintext
GET /test-channel?live HTTP/1.1
Date: Thu, 25 Aug 2016 05:52:40 GMT
Host: test-bucket.oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

```plaintext
HTTP/1.1 200
content-length: 475
server: AliyunOSS
connection: close
x-oss-request-id: 57BE87A8B92475920B00****
date: Thu, 25 Aug 2016 05:52:40 GMT
content-type: application/xml

<?xml version="1.0" encoding="UTF-8"?>
<LiveChannelConfiguration>
  <Description></Description>
  <Status>enabled</Status>
  <Target>
    <Type>HLS</Type>
    <FragDuration>2</FragDuration>
    <FragCount>3</FragCount>
    <PlaylistName>playlist.m3u8</PlaylistName>
  </Target>
</LiveChannelConfiguration>
```

## SDK

[Java](https://help.aliyun.com/zh/oss/developer-reference/common-operations-of-oss-sdk-for-java-on-livechannels#concept-995188 "")