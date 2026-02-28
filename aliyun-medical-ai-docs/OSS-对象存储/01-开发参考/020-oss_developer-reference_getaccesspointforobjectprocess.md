### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/) [开发参考](https://help.aliyun.com/zh/oss/developer-reference/) [API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/) [关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/) [对象FC接入点（Object FC AccessPoint）](https://help.aliyun.com/zh/oss/developer-reference/object-fc-access-point/) GetAccessPointForObjectProcess

# GetAccessPointForObjectProcess

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CreateAccessPointForObjectProcess](https://help.aliyun.com/zh/oss/developer-reference/createaccesspointforobjectprocess)[下一篇：DeleteAccessPointForObjectProcess](https://help.aliyun.com/zh/oss/developer-reference/deleteaccesspointforobjectprocess)

该文章对您有帮助吗？

反馈

调用GetAccessPointForObjectProcess接口获取对象FC接入点基础信息。

## 注意事项

阿里云账号默认拥有获取对象FC接入点基础信息的权限。如果您希望通过RAM用户或者STS的方式获取对象FC接入点基础信息，您必须拥有`oss:GetAccessPointForObjectProcess`权限。

## **请求语法**

```xml
GET /?accessPointForObjectProcess HTTP/1.1
Date: GMT Date
Content-Length：ContentLength
Content-Type: application/xml
Host: BucketName.oss-cn-qingdao.aliyuncs.com
x-oss-access-point-for-object-process-name: fc-ap-01
Authorization: SignatureValue
```

## **请求头**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| x-oss-access-point-for-object-process-name | 字符串 | 是 | fc-ap-01 | 填写对象FC接入点名称。 |

此接口涉及的公共请求头，例如Date、Host等。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")

## 响应头

此接口仅包含公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## **响应元素**

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| GetAccessPointForObjectProcessResult | 容器 | 不涉及 | 保存对象FC接入点信息的容器。<br>父节点：无<br>子节点：AccessPointNameForObjectProcess，AccessPointForObjectProcessAlias、AccessPointName、AccountId、AccessPointForObjectProcessArn、CreationDate、Status和Endpoints |
| AccessPointNameForObjectProcess | 字符串 | fc-ap-01 | 对象FC接入点名称。<br>父节点：GetAccessPointForObjectProcessResult<br>子节点：无 |
| AccessPointForObjectProcessAlias | 字符串 | fc-ap-01-3b00521f653d2b3223680ec39dbbe2\*\*\*\*-opapalias | 对象FC接入点别名。<br>父节点：GetAccessPointForObjectProcessResult<br>子节点：无 |
| AccessPointName | 字符串 | ap-01 | 接入点名称。<br>父节点：GetAccessPointForObjectProcessResult<br>子节点：无 |
| AccountId | 字符串 | 111933544165\*\*\*\* | 配置对象FC接入点的阿里云账号UID。<br>父节点：GetAccessPointForObjectProcessResult<br>子节点：无 |
| AccessPointForObjectProcessArn | 字符串 | acs:oss:cn-qingdao:119335441657143:accesspointforobjectprocess/fc-ap-01 | 对象FC接入点ARN。<br>父节点：GetAccessPointForObjectProcessResult<br>子节点：无 |
| CreationDate | 字符串 | 1626769503 | 对象FC接入点创建时间，格式为时间戳。<br>父节点：GetAccessPointForObjectProcessResult<br>子节点：无 |
| Status |  | enable | 对象FC接入点所处状态。返回值如下：<br>- enable：对象FC接入点已创建完成。<br>  <br>- disable：对象FC接入点已禁用。<br>  <br>- creating：对象FC接入点正在创建中。<br>  <br>- deleting：对象FC接入点已删除。<br>  <br>父节点：GetAccessPointForObjectProcessResult<br>子节点：无 |
| Endpoints | 容器 | 不涉及 | 保存对象FC接入点访问域名信息的容器。<br>父节点：GetAccessPointForObjectProcessResult<br>子节点：PublicEndpoint和InternalEndpoint |
| PublicEndpoint | 字符串 | fc-ap-01-111933544165\*\*\*\*.oss-cn-qingdao.oss-object-process.aliyuncs.com | 对象FC接入点的外网Endpoint。<br>父节点：Endpoints<br>子节点：无 |
| InternalEndpoint | 字符串 | fc-ap-01-111933544165\*\*\*\*.oss-cn-qingdao-internal.oss-object-process.aliyuncs.com | 对象FC接入点的内网Endpoint。<br>父节点：Endpoints<br>子节点：无 |
| PublicAccessBlockConfiguration | 容器 | 不涉及 | 保存阻止公共访问信息的容器。<br>父节点：GetAccessPointResult<br>子节点：BlockPublicAccess |
| BlockPublicAccess | 布尔值 | true | 指定对象FC接入点是否开启阻止公共访问。<br>- true：开启阻止公共访问。<br>  <br>- false：关闭阻止公共访问。<br>  <br>父节点：PublicAccessBlockConfiguration<br>子节点：无 |

## **示例**

- 请求示例


```xml
GET /?accessPointForObjectProcess HTTP/1.1
Date: Mon, 30 Oct 2023 03:15:40 GMT
Content-Length：870
Content-Type: application/xml
Host: oss-example.oss-cn-qingdao.aliyuncs.com
x-oss-access-point-for-object-process-name: fc-ap-01
Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=content-length,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
```

- 返回示例


```xml
HTTP/1.1 200
<?xml version="1.0" encoding="UTF-8"?>
<GetAccessPointForObjectProcessResult>
    <AccessPointNameForObjectProcess>fc-ap-01</AccessPointNameForObjectProcess>
    <AccessPointForObjectProcessAlias>fc-ap-01-3b00521f653d2b3223680ec39dbbe2****-opapalias</AccessPointForObjectProcessAlias>
    <AccessPointName>ap-01</AccessPointName>
    <AccountId>111933544165****</AccountId>
    <AccessPointForObjectProcessArn>acs:oss:cn-qingdao:11933544165****:accesspointforobjectprocess/fc-ap-01</AccessPointForObjectProcessArn>
    <CreationDate>1626769503</CreationDate>
    <Status>enable</Status>
    <Endpoints>
      <PublicEndpoint>fc-ap-01-111933544165****.oss-cn-qingdao.oss-object-process.aliyuncs.com</PublicEndpoint>
      <InternalEndpoint>fc-ap-01-111933544165****.oss-cn-qingdao-internal.oss-object-process.aliyuncs.com</InternalEndpoint>
    </Endpoints>
    <PublicAccessBlockConfiguration>
      <BlockPublicAccess>true</BlockPublicAccess>
    </PublicAccessBlockConfiguration>
</GetAccessPointForObjectProcessResult>
```