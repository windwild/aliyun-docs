### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Object操作](https://help.aliyun.com/zh/oss/developer-reference/object-operations/)[标签（Tagging）](https://help.aliyun.com/zh/oss/developer-reference/tagging-1/)DeleteObjectTagging

# DeleteObjectTagging

更新时间：2025-04-25 06:30:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

版本控制

权限说明

请求语法

请求头

响应头

示例

SDK

命令行工具ossutil

调用DeleteObjectTagging接口删除指定对象（Object）的标签（Tagging）信息。

## 版本控制

调用DeleteObjectTagging接口时，默认只能删除Object当前版本的标签信息。您可以通过指定versionId参数来删除指定Object版本的标签信息。如果Object的对应版本为删除标记（Delete Marker），则OSS将返回404 Not Found。

## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

| API | Action | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| API | Action | 说明 |
| DeleteObjectTagging | oss:DeleteObjectTagging | 删除指定Object的标签信息。 |
| oss:DeleteObjectVersionTagging | 删除指定版本Object的标签信息。 |

## 请求语法

```plaintext
DELETE /objectname?tagging
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue
```

当您在OSS ON云盒中调用该接口时，您需要将Host替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

## 请求头

此接口仅涉及公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

- 未开启版本控制

在未开启版本控制的情况下，通过DELETE请求删除了存储空间bucketname中对象objectname已有的标签信息，OSS解析此请求后删除此对象中的所有标签。



请求示例

















```plaintext
DELETE /objectname?tagging
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: Tue, 09 Apr 2019 03:00:33 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```







返回示例

















```plaintext
204 (No Content)
content‐length: 0
server: AliyunOSS
x‐oss‐request‐id: 5CAC0AD16D0232E2051B****
date: Tue, 09 Apr 2019 03:00:33 GMT
```

- 已启用版本控制

在启用版本控制的情况下，通过DELETE请求删除存储空间bucketname中对象objectname已有的标签信息，删除时指定了对象版本号（即请求示例中的versionId），OSS解析此请求后删除此版本对象中的所有标签。



请求示例

















```plaintext
DELETE /objectname?tagging&versionId=CAEQExiBgID.jImWlxciIDQ2ZjgwODIyNDk5MTRhNzBiYmQwYTZkMTYzZjM0****
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: Wed, 24 Jun 2020 09:01:09 GMT
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```







返回示例

















```plaintext
204 (No Content)
content-length: 0
server: AliyunOSS
x-oss-request-id: 5EF3165525D95C3338E8****
date: Wed, 24 Jun 2020 09:01:09 GMT
x-oss-version-id: CAEQExiBgID.jImWlxciIDQ2ZjgwODIyNDk5MTRhNzBiYmQwYTZkMTYzZjM0****
```


## SDK

DeleteObjectTagging接口对应的各语言SDK示例如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/delete-the-tags-of-an-object-1#concept-727776 "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/delete-object-tags-using-oss-sdk-for-python-v2 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-delete-object-tags "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/delete-object-tags-using-oss-sdk-for-php-v2 "")

- [Android](https://help.aliyun.com/zh/oss/developer-reference/object-tagging-4 "")

- [C++](https://help.aliyun.com/zh/oss/developer-reference/delete-object-tags-2#concept-727374 "")

- [.NET](https://help.aliyun.com/zh/oss/developer-reference/delete-object-tags#concept-2512416 "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/delete-the-tags-of-an-object-2#concept-2404257 "")

- [iOS](https://help.aliyun.com/zh/oss/developer-reference/object-tagging-1 "")


## **命令行工具ossutil**

DeleteObjectTagging接口所对应的ossutil命令，请参见 [delete-object-tagging](https://help.aliyun.com/zh/oss/developer-reference/delete-object-tagging "")。