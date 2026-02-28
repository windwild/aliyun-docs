调用DescribeTopDomainsByFlow获取用户按流量排名的域名，支持获取最近30天的数据。

阿里云CDN产品的统计分析功能已经下线，与统计分析功能相关的OpenAPI接口已不再继续维护。鉴于当前该接口可能存在数据缺失、不准确等问题，建议您不要使用该接口。如果您有数据统计分析相关的需求，可以通过 [运营报表](https://help.aliyun.com/zh/cdn/user-guide/customize-an-operations-report-template-and-create-a-tracking-task) 或者 [投递实时日志到SLS](https://help.aliyun.com/zh/cdn/user-guide/best-practices-for-shipping-and-analyzing-alibaba-cloud-cdn-real-time-logs-in-log-service) 来实现。


**说明**

- 如果您不指定 **StartTime** 和 **EndTime**，该接口返回当月数据；指定 **StartTime** 和 **EndTime**，返回起止时间的数据。

- 单用户调用频率：100次/秒。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Cdn&api=DescribeTopDomainsByFlow&type=RPC&version=2018-05-10)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求参数

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |
| Action | String | 是 | DescribeTopDomainsByFlow | 系统规定参数。取值： **DescribeTopDomainsByFlow**。 |
| StartTime | String | 否 | 2019-12-22T08:00:00Z | 获取数据的起始时间点。日期格式按照ISO8601表示法，并使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。<br>**说明**<br>StartTime必须设置为北京时间0点对应的UTC时间，例如：北京时间06月01日0点，需要设置为UTC时间“2021-05-31T16:00:00Z”。 |
| EndTime | String | 否 | 2019-12-23T08:00:00Z | 获取数据的结束时间点。日期格式按照ISO8601表示法，并使用UTC时间。格式为yyyy-MM-ddTHH:mm:ssZ。<br>**说明**<br>结束时间需大于起始时间。 |
| Limit | Long | 否 | 20 | 域名获取数量限制，默认为 **20**，取值 **1** ~ **100**。 |

## 返回数据

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |
| DomainOnlineCount | Long | 68 | 账号下状态为 **正在运行** 的域名总数。 |
| EndTime | String | 2019-12-23T08:00:00Z | 结束时间。 |
| StartTime | String | 2019-12-22T08:00:00Z | 开始时间。 |
| RequestId | String | 4E09C5D7-E1CF-4CAA-A45E-8727F4C8FD70 | 请求ID。 |
| DomainCount | Long | 68 | 账号下的域名总数。 |
| TopDomains | Array of TopDomain |  | 排名域名列表。 |
| TopDomain |  |  |  |
| MaxBps | Float | 22139626 | 带宽峰值。 |
| Rank | Long | 1 | 排名。 |
| TotalAccess | Long | 107784230 | 访问次数。 |
| TrafficPercent | String | 30.64191989360235 | 流量占比。 |
| DomainName | String | example.com | 加速域名。 |
| TotalTraffic | String | 2043859876683.9001 | 总流量。 |
| MaxBpsTime | String | 1457111400 | 带宽峰值时刻。 |

## 示例

请求示例

```1c
http(s)://cdn.aliyuncs.com/?Action=DescribeTopDomainsByFlow
&StartTime=2019-12-22T08:00:00Z
&EndTime=2019-12-23T08:00:00Z
&Limit=5
&<公共请求参数>
```

正常返回示例

`XML`格式


```apache
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeTopDomainsByFlowResponse>
<DomainCount>4</DomainCount>
<DomainOnlineCount>4</DomainOnlineCount>
<RequestId>6796A2B4-15A7-4142-85C0-5A93406034B5</RequestId>
<TopDomains>
    <TopDomain>
        <MaxBps>26.752000000000002</MaxBps>
        <Rank>3</Rank>
        <TrafficPercent>0.000910078753253719</TrafficPercent>
        <TotalTraffic>2003</TotalTraffic>
        <TotalAccess>2</TotalAccess>
        <DomainName>example.com</DomainName>
        <MaxBpsTime>2019-12-22T20:50:00Z</MaxBpsTime>
    </TopDomain>
</TopDomains>
<EndTime>2019-12-23T08:00:00Z</EndTime>
<StartTime>2019-12-22T08:00:00Z</StartTime>
</DescribeTopDomainsByFlowResponse>
```

`JSON`格式


```ada
HTTP/1.1 200 OK
Content-Type:application/json

{
  "DomainCount" : 4,
  "DomainOnlineCount" : 4,
  "RequestId" : "6796A2B4-15A7-4142-85C0-5A93406034B5",
  "TopDomains" : {
    "TopDomain" : [ {\
      "MaxBps" : "26.752000000000002",\
      "Rank" : 3,\
      "TrafficPercent" : "0.000910078753253719",\
      "TotalTraffic" : 2003,\
      "TotalAccess" : 2,\
      "DomainName" : "example.com",\
      "MaxBpsTime" : "2019-12-22T20:50:00Z"\
    } ]
  },
  "EndTime" : "2019-12-23T08:00:00Z",
  "StartTime" : "2019-12-22T08:00:00Z"
}
```

## 错误码

| HttpCode | 错误码 | 错误信息 | 描述 |
| --- | --- | --- | --- |

| HttpCode | 错误码 | 错误信息 | 描述 |
| --- | --- | --- | --- |
| 400 | InvalidStartTime.Malformed | Specified StartTime is malformed. | 起始时间格式错误。日期格式请参考所调用API的帮助文档说明。 |
| 400 | InvalidEndTime.Malformed | Specified EndTime is malformed. | 结束时间格式错误。日期格式请参考所调用API的帮助文档说明。 |
| 400 | InvalidStartTime.ValueNotSupported | The specified value of parameter StartTime is not supported. | 开始时间设置错误，请检查更新后重试。 |

访问 [错误中心](https://error-center.aliyun.com/status/product/Cdn) 查看更多错误码。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 获取按流量排名的加速域名

# 获取按流量排名的加速域名

更新时间：2022-08-17 02:12:34

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