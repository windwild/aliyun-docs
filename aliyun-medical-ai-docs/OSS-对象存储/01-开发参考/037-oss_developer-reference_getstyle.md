### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[图片样式（Style）](https://help.aliyun.com/zh/oss/developer-reference/image-style/)GetStyle

# 调用GetStyle接口查询某个Bucket下指定的样式信息

更新时间：2025-05-06 05:24:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PutStyle](https://help.aliyun.com/zh/oss/developer-reference/putstyle)[下一篇：ListStyle](https://help.aliyun.com/zh/oss/developer-reference/liststyle)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

请求语法

请求头

响应头

响应元素

示例

SDK

命令行工具ossutil

调用GetStyle接口查询某个Bucket下指定的样式信息。

## **注意事项**

阿里云账号默认拥有查询某个Bucket下指定样式信息的权限。如果您希望通过RAM用户或者STS的方式进行查询，您必须拥有`oss:GetStyle`权限。具体操作，请参见 [为RAM用户授予自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

## 请求语法

**说明**

获取某个Bucket下指定的样式信息时，您需要通过`styleName`参数指定样式名称，例如`GET /?style&styleName=imagestyle HTTP/1.1`。

```plaintext
GET /?style&styleName=styleName HTTP/1.1
Date:  GMT Date
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Authorization: SignatureValue
```

## **请求头**

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## **响应头**

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 响应元素

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| Style | 容器 | 不涉及 | 保存已获取样式内容的容器。<br>父节点：无<br>子节点：Name、Content、CreateTime、LastModifyTime |
| Name | 字符串 | imagestyle | 样式名称。<br>父节点：Style<br>子节点：无 |
| Content | 字符串 | image/resize,p\_50 | 样式内容。<br>父节点：Style<br>子节点：无 |
| Category | 字符串 | image | 样式分类。<br>取值：image、document、video。<br>父节点：Style<br>子节点：无 |
| CreateTime | 字符串 | Wed, 20 May 2020 12:07:15 GMT | 样式创建时间。<br>父节点：Style<br>子节点：无 |
| LastModifyTime | 字符串 | Wed, 21 May 2020 12:07:15 GMT | 样式修改时间。<br>父节点：Style<br>子节点：无 |

## 示例

- 请求示例


```plaintext
GET /?style&styleName=imagestyle HTTP/1.1
Date: Thu, 17 Apr 2025 05:34:24 GMT
Content-Length: 63
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=content-length,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

- 返回示例


```plaintext
HTTP/1.1 200 OK
Server: AliyunOSS
Date: Fri, 04 Mar 2022 05:28:35 GMT
Content-Type: application/xml
Content-Length: 239
Connection: keep-alive
x-oss-request-id: 6221A383CBD8483439E7****
<?xml version="1.0" encoding="UTF-8"?>
<Style>
 <Name>imagestyle</Name>
 <Content>image/resize,p_50</Content>
 <Category>image</Category>
 <CreateTime>Wed, 20 May 2020 12:07:15 GMT</CreateTime>
 <LastModifyTime>Wed, 21 May 2020 12:07:15 GMT</LastModifyTime>
</Style>
```

## SDK

本接口对应的SDK如下：

- [Python](https://help.aliyun.com/zh/oss/developer-reference/python-sdk-image-styles "")


## **命令行工具ossutil**

GetStyle接口所对应的ossutil命令，请参见 [get-style](https://help.aliyun.com/zh/oss/developer-reference/get-style "")。