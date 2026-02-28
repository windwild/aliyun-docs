调用DescribeActiveVersionOfConfigGroup查询生效的配置组版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Cdn&api=DescribeActiveVersionOfConfigGroup&type=RPC&version=2018-05-10)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求参数

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |
| Action | String | 是 | DescribeActiveVersionOfConfigGroup | 系统规定参数。取值： **DescribeActiveVersionOfConfigGroup**。 |
| ConfigGroupId | String | 是 | testID | 配置组ID。 |
| Env | String | 否 | staging | 环境。取值：<br>- **staging**：模拟环境。<br>   <br>- **production**：生产环境。 |

## 返回数据

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |
| BaseVersionId | String | testBaseVersionId | 基础版本的ID。 |
| ConfigGroupId | String | testID | 配置组的ID。 |
| CreateTime | String | 2019-09-26T12:16:02+08:00 | 创建时间。 |
| Description | String | For query Version | 版本的描述。 |
| Operator | String | testOperator | 操作者。 |
| RequestId | String | 28B66E7B-671A-8297-9687-2Y4477247A74 | 请求ID。 |
| SeqId | Long | 1 | 版本序号ID。 |
| Status | String | deactive | 状态。 |
| UpdateTime | String | 2019-09-28T12:16:02+08:00 | 修改时间。 |
| VersionId | String | testVersionId | 版本ID。 |

## 示例

请求示例

```1c
http(s)://cdn.aliyuncs.com/?Action=DescribeActiveVersionOfConfigGroup
&ConfigGroupId=testID
&Env=staging
&<公共请求参数>
```

正常返回示例

`XML`格式


```apache
<DescribeActiveVersionOfConfigGroupResponse>
  <RequestId>28B66E7B-671A-8297-9687-2Y4477247A74</RequestId>
  <ConfigGroupId>testID</ConfigGroupId>
  <CreateTime>2019-09-26T12:16:02+08:00</CreateTime>
  <UpdateTime>2019-09-28T12:16:02+08:00</UpdateTime>
  <SeqId>1</SeqId>
  <Status>deactive</Status>
  <Description>For query Version</Description>
  <VersionId>testVersionId</VersionId>
  <Operator>testOperator</Operator>
  <BaseVersionId>testBaseVersionId</BaseVersionId>
</DescribeActiveVersionOfConfigGroupResponse>
```

`JSON`格式


```json
{
    "RequestId":"28B66E7B-671A-8297-9687-2Y4477247A74",
     "ConfigGroupId": "testID",
     "CreateTime": "2019-09-26T12:16:02+08:00",
     "UpdateTime": "2019-09-28T12:16:02+08:00",
     "SeqId": 1,
     "Status":"deactive",
     "Description":"For query Version",
     "VersionId":"testVersionId",
     "Operator":"testOperator",
     "BaseVersionId":"testBaseVersionId"
  }
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Cdn)查看更多错误码。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 查询生效的配置组版本

# 查询生效的配置组版本

更新时间：2021-09-14 05:13:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

请求参数

返回数据

示例

错误码