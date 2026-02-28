### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[数据复制（Replication）](https://help.aliyun.com/zh/oss/developer-reference/replication/)GetBucketReplication

# GetBucketReplication

更新时间：2025-02-13 22:02:58

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求语法

响应元素

示例

SDK

命令行工具ossutil

错误码

调用GetBucketReplication接口获取某个存储空间（Bucket）已设置的数据复制规则。

## 请求语法

```javascript
GET /?replication HTTP/1.1
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

## 响应元素

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| 名称 | 类型 | 示例值 | 描述 |
| ReplicationConfiguration | 容器 | 不涉及 | Bucket复制规则的容器。<br>父节点：无<br>子节点：Rule |
| Rule | 容器 | 不涉及 | 保存复制规则的容器。<br>父节点：ReplicationConfiguration<br>子节点：Destination、HistoricalObjectReplication、Status和ID |
| ID | 字符串 | test\_replication\_1 | 复制规则对应的ID。<br>父节点：Rule<br>子节点：无 |
| PrefixSet | 容器 | 不涉及 | 保存前缀（Prefix）的容器。每条复制规则中，最多可指定10个Prefix。<br>父节点：Rule<br>子节点：Prefix |
| Prefix | 字符串 | source1 | 被复制到目标Bucket中Object的前缀（Prefix）。<br>父节点：PrefixSet<br>子节点：无 |
| Action | 字符串 | PUT | 表示被同步到目标Bucket的操作。<br>Action允许以下操作类型，您可以指定一项或多项。<br>- ALL（默认值）：表示PUT、DELETE、ABORT操作均会被同步到目标Bucket。<br>  <br>- PUT：表示被同步到目标Bucket的写入操作，包括PutObject、PostObject、AppendObject、CopyObject、PutObjectACL、InitiateMultipartUpload、UploadPart、UploadPartCopy、CompleteMultipartUpload。<br>  <br>父节点：Rule<br>子节点：无 |
| Status | 字符串 | doing | 表示复制状态。<br>取值：<br>- starting：设置数据复制规则后，OSS会为Bucket准备复制任务，此时的复制状态为starting。<br>  <br>- doing：当数据复制规则生效后，即数据处于同步状态时，此时的复制状态为doing。<br>  <br>- closing：删除数据复制规则后，OSS会自动完成清理工作，此时的复制状态为closing。<br>  <br>父节点：Rule<br>子节点：无 |
| Destination | 容器 | 不涉及 | 保存目标Bucket信息的容器。<br>父节点：Rule<br>子节点：Bucket和Location |
| Bucket | 字符串 | destbucket | 数据要复制到的目标Bucket。<br>父节点：Destination<br>子节点：无 |
| Location | 字符串 | oss-cn-beijing | 目标Bucket所处的Location。<br>父节点：Destination<br>子节点：无 |
| TransferType | 字符串 | oss\_acc | 数据复制时使用的数据传输类型。仅当传输类型为oss\_acc时，返回示例中才会包含此元素。<br>取值：<br>- internal（默认值）：OSS默认传输链路。<br>  <br>- oss\_acc：传输加速链路。只有创建跨区域复制规则时才能使用传输加速链路。 |
| HistoricalObjectReplication | 字符串 | disabled | 是否复制历史数据。即开启数据复制前，是否将源Bucket中的已有的数据复制到目标Bucket。<br>取值：<br>- enabled（默认）：表示复制历史数据。<br>  <br>- disabled：表示不复制历史数据，即仅复制数据复制规则生效后新写入的数据。<br>  <br>父节点：Rule<br>子节点：无 |
| SyncRole | 字符串 | aliyunramrole | 跨区域复制时使用的角色。仅当使用SSE-KMS加密目标对象时，返回示例中才会包含此元素。 |
| RTC | 容器 | 不涉及 | 保存RTC状态规则的容器。<br>父节点：Rule<br>子节点：Status |
| Status | 字符串 | enbaled | RTC服务的状态。仅当RTC状态为enabling或enabled时，返回示例中才会包含此元素。<br>取值：<br>- enabling：RTC服务开启中。<br>  <br>- enabled：RTC服务已开启。<br>  <br>- disabled（默认值）：RTC服务已关闭。<br>  <br>父节点：RTC<br>子节点：无 |

## 示例

- 请求示例


```javascript
GET /?replication HTTP/1.1
Host: oss-example.oss-cn-hangzhou.aliyuncs.com
Date: Thu, 24 Sep 2015 15:39:15 GMT
Authorization: OSS qn6q**************:77Dv****************
```

- 返回示例


```javascript
HTTP/1.1 200 OK
x-oss-request-id: 534B371674E88A4D8906****
Date: Thu, 24 Sep 2015 15:39:15 GMT
Content-Length: 186
Content-Type: application/xml
Connection: close
Server: AliyunOSS
<?xml version="1.0" ?>
<ReplicationConfiguration>
  <Rule>
    <ID>test_replication_1</ID>
    <PrefixSet>
      <Prefix>source1</Prefix>
      <Prefix>video</Prefix>
    </PrefixSet>
    <Action>PUT</Action>
    <Destination>
      <Bucket>destbucket</Bucket>
      <Location>oss-cn-beijing</Location>
      <TransferType>oss_acc</TransferType>
    </Destination>
    <Status>doing</Status>
    <HistoricalObjectReplication>enabled</HistoricalObjectReplication>
    <SyncRole>aliyunramrole</SyncRole>
    <RTC>
      <Status>enabled</Status>
    </RTC>
  </Rule>
</ReplicationConfiguration>
```

## SDK

此接口所对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/data-replication-1 "")

- [Python](https://help.aliyun.com/zh/oss/developer-reference/data-replication-3 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-data-replication "")


## **命令行工具ossutil**

GetBucketReplication接口所对应的ossutil命令，请参见 [get-bucket-replication](https://help.aliyun.com/zh/oss/developer-reference/get-bucket-replication "")。

## 错误码

| 错误码 | 状态码 | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 错误码 | 状态码 | 说明 |
| NoSuchBucket | 404 NotFound | 请求的Bucket不存在。 |
| NoSuchReplicationConfiguration | 404 NotFound | 请求的Bucket没有配置数据复制规则。 |