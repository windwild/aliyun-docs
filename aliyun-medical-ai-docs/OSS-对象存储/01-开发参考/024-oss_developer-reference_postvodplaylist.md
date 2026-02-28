### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [开发参考](https://help.aliyun.com/zh/oss/developer-reference/) [API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/) [关于LiveChannel的操作](https://help.aliyun.com/zh/oss/developer-reference/livechannel-operations/) PostVodPlaylist

# PostVodPlaylist

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetLiveChannelHistory](https://help.aliyun.com/zh/oss/developer-reference/getlivechannelhistory)[下一篇：GetVodPlaylist](https://help.aliyun.com/zh/oss/developer-reference/getvodplaylist)

该文章对您有帮助吗？

反馈

PostVodPlaylist接口用于为指定的LiveChannel生成一个点播用的播放列表。OSS会查询指定时间范围内由该LiveChannel推流生成的ts文件，并将其拼装为一个m3u8播放列表。

## 请求语法

```plaintext
POST /ChannelName/PlaylistName?vod&endTime=EndTime&startTime=StartTime HTTP/1.1
Date: GMT date
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Authorization: SignatureValue
```

## 请求参数

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| ChannelName | 字符串 | 是 | test-channel | 指定LiveChannel名称，该LiveChannel必须存在。 |
| PlaylistName | 字符串 | 是 | vod.m3u8 | 指定生成的点播播放列表的名称，必须以“.m3u8”结尾。 |
| StartTime | 整数 | 是 | 1472020031 | 指定查询ts文件的起始时间，格式为Unix时间戳，单位为秒。<br>**重要** <br>仅当ts文件的开始时间（即 [GetVodPlaylist](https://help.aliyun.com/zh/oss/developer-reference/getvodplaylist#concept-rqq-gw2-cgb "") 返回的ts文件时间戳）在StartTime与EndTime指定的时间范围内，生成的.m3u8播放列表才会包含ts文件。 |
| EndTime | 整数 | 是 | 1472020226 | 指定查询ts文件的终止时间，格式为Unix时间戳，单位为秒。<br>**说明** <br>EndTime必须大于StartTime，且时间跨度不能大于1天。 |

此接口还需要包含Host、Date等公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

请求示例

```plaintext
POST /test-channel/vod.m3u8?vod&endTime=1543895706266&startTime=1543895706263 HTTP/1.1
Date: Thu, 25 Aug 2016 07:13:26 GMT
Host: examplebucket.oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

返回示例

```plaintext
HTTP/1.1 200
content-length: 0
server: AliyunOSS
connection: close
etag: "9C6104DD9CF1A0C4D0CFD21F4390****"
x-oss-request-id: 57BE9A96B92475920B002359
date: Thu, 25 Aug 2016 07:13:26 GMT
```

## SDK

- [Java](https://help.aliyun.com/zh/oss/developer-reference/common-operations-of-oss-sdk-for-java-on-livechannels#concept-995188 "")

- [Python](https://help.aliyun.com/zh/oss/use-cases/call-selectobject-to-query-csv-and-json-objects-in-a-bucket-by-using-oss-sdk-for-python#concept-1113040 "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/common-operations-on-livechannels#concept-2161611 "")

- [Go](https://help.aliyun.com/zh/oss/developer-reference/common-operations-on-livechannels-1#concept-2164037 "")