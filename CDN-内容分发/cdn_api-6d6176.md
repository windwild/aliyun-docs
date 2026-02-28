调DescribeDomainAverageResponseTime获取加速域名的平均响应时间，支持获取最近90天的数据。

阿里云CDN产品的统计分析功能已经下线，与统计分析功能相关的OpenAPI接口已不再继续维护。鉴于当前该接口可能存在数据缺失、不准确等问题，建议您不要使用该接口。如果您有数据统计分析相关的需求，可以通过 [运营报表](https://help.aliyun.com/zh/cdn/user-guide/customize-an-operations-report-template-and-create-a-tracking-task) 或者 [投递实时日志到SLS](https://help.aliyun.com/zh/cdn/user-guide/best-practices-for-shipping-and-analyzing-alibaba-cloud-cdn-real-time-logs-in-log-service) 来实现。


**说明**

- 如果您不指定StartTime和EndTime，该接口返回过去24小时的数据；指定StartTime和EndTime时，返回起止时间的数据。
- 单用户调用频率：100次/秒。
- 支持批量查询域名，多个域名用半角逗号（,）分隔，一次最多支持500个域名查询。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Cdn&api=DescribeDomainAverageResponseTime&type=RPC&version=2018-05-10)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求参数

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |
| Action | String | 是 | DescribeDomainAverageResponseTime | 系统规定参数。取值： **DescribeDomainAverageResponseTime**。 |
| TimeMerge | String | 否 | 1 | 是否自适应计算Interval值，如果 **timeMerge** = **1**，会根据startTime和endTime计算出合适的inteval值，和Interval参数任选。 |
| DomainType | String | 否 | domaintype | 查询类型。传dynamic时，查询全站加速动态资源的平均响应时间和静态资源的平均响应时间；默认不传，查询静态资源的平均响应时间。 |
| DomainName | String | 否 | example.com | 加速域名，多个域名用英文逗号（,）分隔。<br>默认查询所有加速域名。 |
| StartTime | String | 否 | 2019-11-30T05:33:00Z | 获取数据起始时间点。日期格式按照ISO8601表示法，并使用UTC时间。格式为yyyy-MM-ddTHH:mm:ssZ。 |
| EndTime | String | 否 | 2019-11-30T05:40:00Z | 获取数据的结束时间点。获取日期格式按照ISO8601表示法，并使用UTC时间。格式为yyyy-MM-ddTHH:mm:ssZ。<br>结束时间需大于起始时间。 |
| Interval | String | 否 | 300 | 查询数据的时间粒度，单位：秒。根据您指定 **StartTime** 和 **EndTime** 两者的时间跨度，该参数取值如下：<br> <br>- 3天以内（不包含3天整）支持 **300**、 **3600**、 **86400**，如果不传该参数，默认值为 **300**。<br>   <br>- 3-31天（不包含31天整）支持 **3600** 和 **86400**，如果不传该参数，默认值为 **3600**。<br>   <br>- 31天及以上支持 **86400**，如果不传该参数，默认值为 **86400**。 |
| IspNameEn | String | 否 | unicom | 运营商英文名，通过 [DescribeCdnRegionAndIsp](https://help.aliyun.com/zh/cdn/api-describecdnregionandisp) 接口获得，默认查询所有运营商。 |
| LocationNameEn | String | 否 | beijing | 地域英文名，通过 [DescribeCdnRegionAndIsp](https://help.aliyun.com/zh/cdn/api-describecdnregionandisp) 接口获得，默认查询所有地域。 |

## 返回数据

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |
| EndTime | String | 2019-11-30T05:40:00Z | 结束时间。 |
| StartTime | String | 2019-11-30T05:33:00Z | 开始时间。 |
| RequestId | String | 3C6CCEC4-6B88-4D4A-93E4-D47B3D92CF8F | 请求ID。 |
| DomainName | String | example.com | 加速域名。 |
| DataInterval | String | 300 | 数据时间间隔。 |
| AvgRTPerInterval | Array of DataModule |  | 每个时间点平均响应时间。 |
| DataModule |  |  |  |
| Value | String | 3 | 平均响应时间。 |
| TimeStamp | String | 2015-12-10T20:00:00Z | 时间片起始时刻。 |

## 示例

请求示例

```1c
http://cdn.aliyuncs.com/?Action=DescribeDomainAverageResponseTime
&DomainName=example.com
&StartTime=2019-11-30T05:33:00Z
&EndTime=2019-11-30T05:40:00Z
&<公共请求参数>
```

正常返回示例

`XML`格式


```apache
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeDomainAverageResponseTimeResponse>
	<DomainName>example.com</DomainName>
	<RequestId>3C6CCEC4-6B88-4D4A-93E4-D47B3D92CF8F</RequestId>
	<StartTime>2019-11-30T05:33:00Z</StartTime>
	<EndTime>2019-11-30T05:40:00Z</EndTime>
	<DataInterval>300</DataInterval>
	<AvgRTPerInterval>
		<DataModule>
			<TimeStamp>2019-11-30T05:33:00Z</TimeStamp>
			<Value>3</Value>
		</DataModule>
		<DataModule>
			<TimeStamp>2019-11-30T05:38:00Z</TimeStamp>
			<Value>3</Value>
		</DataModule>
	</AvgRTPerInterval>
</DescribeDomainAverageResponseTimeResponse>
```

`JSON`格式


```ruby
HTTP/1.1 200 OK
Content-Type:application/json

{
  "DomainName" : "example.com",
  "RequestId" : "3C6CCEC4-6B88-4D4A-93E4-D47B3D92CF8F",
  "StartTime" : "2019-11-30T05:40:00Z",
  "EndTime" : "2019-11-30T05:33:00Z",
  "DataInterval" : "300",
  "AvgRTPerInterval" : {
    "DataModule" : [ {\
      "TimeStamp" : "2019-11-30T05:33:00Z",\
      "Value" : "3"\
    }, {\
      "TimeStamp" : "2019-11-30T05:38:00Z",\
      "Value" : "3"\
    } ]
  }
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

[首页](https://help.aliyun.com/) 获取平均响应时间数据

# 获取平均响应时间数据

更新时间：2022-08-17 02:14:10

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