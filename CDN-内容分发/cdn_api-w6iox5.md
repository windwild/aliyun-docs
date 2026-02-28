调用DescribeDomainSrcTopUrlVisit获取加速域名的回源热门URL。

阿里云CDN产品的统计分析功能已经下线，与统计分析功能相关的OpenAPI接口已不再继续维护。鉴于当前该接口可能存在数据缺失、不准确等问题，建议您不要使用该接口。如果您有数据统计分析相关的需求，可以通过 [运营报表](https://help.aliyun.com/zh/cdn/user-guide/customize-an-operations-report-template-and-create-a-tracking-task) 或者 [投递实时日志到SLS](https://help.aliyun.com/zh/cdn/user-guide/best-practices-for-shipping-and-analyzing-alibaba-cloud-cdn-real-time-logs-in-log-service) 来实现。


**说明**

- 查询的时间粒度为5分钟。
- 单用户调用频率：10次/秒。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Cdn&api=DescribeDomainSrcTopUrlVisit&type=RPC&version=2018-05-10)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求参数

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |
| Action | String | 是 | DescribeDomainSrcTopUrlVisit | 系统规定参数。取值： **DescribeDomainSrcTopUrlVisit**。 |
| DomainName | String | 是 | example.com | 加速域名，多个域名用英文逗号（,）分隔。 |
| StartTime | String | 否 | 2018-10-03T16:00:00Z | 获取数据起始时间点。日期格式按照ISO8601表示法，并使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。<br>**说明**<br>如果不指定StartTime，默认读取前一天的数据。 |
| EndTime | String | 否 | 2018-10-03T20:00:00Z | 获取数据结束时间点。日期格式按照ISO8601表示法，并使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。<br>**说明**<br>结束时间需大于起始时间，并且结束时间和开始时间相差不超过7天。 |
| SortBy | String | 否 | pv | 排序方式，默认值为 **pv**。取值：<br> <br>- **traf**：流量。<br>   <br>- **pv**：访问量。 |

## 返回数据

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |
| StartTime | String | 2018-10-03T16:00:00Z | 查询指定日期。 |
| RequestId | String | 64D28B53-5902-409B-94F6-FD46680144FE | 请求ID。 |
| DomainName | String | example.com | 加速域名信息。 |
| AllUrlList | Array of UrlList |  | 全部热门URL列表。 |
| UrlList |  |  |  |
| Flow | String | 460486880 | 流量。单位：byte。 |
| UrlDetail | String | http://example.com/nn\_live/nn\_x64/a0.m3u8 | 完整的URL地址。 |
| FlowProportion | Float | 0.35 | 流量占比。 |
| VisitData | String | 161673 | 访问次数。 |
| VisitProportion | Float | 0.35 | 访问占比。 |
| Url200List | Array of UrlList |  | 返回为2xx的URL列表。 |
| UrlList |  |  |  |
| Flow | String | 460486880 | 流量。单位：byte。 |
| UrlDetail | String | http://example.com/nn\_live/nn\_x64/a0.m3u8 | 完整的URL地址。 |
| FlowProportion | Float | 0.35 | 流量占比。 |
| VisitData | String | 161673 | 访问次数。 |
| VisitProportion | Float | 0.35 | 访问占比。 |
| Url300List | Array of UrlList |  | 返回为3xx的URL列表。 |
| UrlList |  |  |  |
| Flow | String | 460486880 | 流量。单位：byte。 |
| UrlDetail | String | http://example.com/nn\_live/nn\_x64/a0.m3u8 | 完整的URL地址。 |
| FlowProportion | Float | 0.35 | 流量占比。 |
| VisitData | String | 161673 | 访问次数。 |
| VisitProportion | Float | 0.35 | 访问占比。 |
| Url400List | Array of UrlList |  | 返回为4xx的URL列表。 |
| UrlList |  |  |  |
| Flow | String | 460486880 | 流量。单位：byte。 |
| UrlDetail | String | http://example.com/nn\_live/nn\_x64/a0.m3u8 | 完整的URL地址。 |
| FlowProportion | Float | 0.35 | 流量占比。 |
| VisitData | String | 161673 | 访问次数。 |
| VisitProportion | Float | 0.35 | 访问占比。 |
| Url500List | Array of UrlList |  | 返回为5xx的URL列表。 |
| UrlList |  |  |  |
| Flow | String | 460486880 | 流量，单位：byte。 |
| UrlDetail | String | http://example.com/nn\_live/nn\_x64/a0.m3u8 | 完整的URL地址。 |
| FlowProportion | Float | 0.35 | 流量占比。 |
| VisitData | String | 161673 | 访问次数。 |
| VisitProportion | Float | 0.35 | 访问占比。 |

## 示例

请求示例

```1c
http://cdn.aliyuncs.com?Action=DescribeDomainSrcTopUrlVisit
&DomainName=example.com
&StartTime=2018-10-03T16:00:00Z
&EndTime=2018-10-03T20:00:00Z
&<公共请求参数>
```

正常返回示例

`XML`格式


```xml
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeDomainSrcTopUrlVisitResponse>
<AllUrlList>
    <UrlList>
        <VisitData>161673</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/a0.m3u8</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
    <UrlList>
        <VisitData>37</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/ZXg9MQ,,/HNJSMPP360.ts</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
</AllUrlList>
<Url300List>
    <UrlList>
        <VisitData>161673</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SE5KU0GNfbGl2ZQ,,/HNJSMPP360.m3u8</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
    <UrlList>
        <VisitData>3</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SE5KU01QUDZXg9MQ,,/HNJSMPP360.ts</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
</Url300List>
<Url400List>
    <UrlList>
        <VisitData>1884</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SE5KU01QUhb,,/HNJSMPP360.m3u8</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
    <UrlList>
        <VisitData>1</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SEEwODgm,/HNJSMPP360.ts</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
</Url400List>
<RequestId>64D28B53-5902-409B-94F6-FD46680144FE</RequestId>
<DomainName>example.com</DomainName>
<Url200List>
    <UrlList>
        <VisitData>161673</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SE5KU0bGxfcG,,/HNJSMPP360.m3u8</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
    <UrlList>
        <VisitData>3</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SE5KDMlPTIwMTQ,,/HNJSMPP360.ts</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
</Url200List>
<StartTime>2018-10-03T16:00:00Z</StartTime>
<Url500List>
    <UrlList>
        <VisitData>161673</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SE5KU0GNfbGl2ZQ,,/HNJSMPP360.m3u8</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
    <UrlList>
        <VisitData>3</VisitData>
        <UrlDetail>http://example.com/nn_live/nn_x64/aWQ9SE5KU01QUDZXg9MQ,,/HNJSMPP360.ts</UrlDetail>
        <VisitProportion>0.35</VisitProportion>
        <Flow>460486880</Flow>
        <FlowProportion>0.35</FlowProportion>
    </UrlList>
</Url500List>
</DescribeDomainSrcTopUrlVisitResponse>
```

`JSON`格式


```prolog
HTTP/1.1 200 OK
Content-Type:application/json

{
  "AllUrlList" : {
    "UrlList" : [ {\
      "VisitData" : "161673",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/a0.m3u8",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    }, {\
      "VisitData" : "37",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/ZXg9MQ,,/HNJSMPP360.ts",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    } ]
  },
  "Url300List" : {
    "UrlList" : [ {\
      "VisitData" : "161673",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SE5KU0GNfbGl2ZQ,,/HNJSMPP360.m3u8",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    }, {\
      "VisitData" : "3",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SE5KU01QUDZXg9MQ,,/HNJSMPP360.ts",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    } ]
  },
  "Url400List" : {
    "UrlList" : [ {\
      "VisitData" : "1884",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SE5KU01QUhb,,/HNJSMPP360.m3u8",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    }, {\
      "VisitData" : "1",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SEEwODgm,/HNJSMPP360.ts",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    } ]
  },
  "RequestId" : "64D28B53-5902-409B-94F6-FD46680144FE",
  "DomainName" : "example.com",
  "Url200List" : {
    "UrlList" : [ {\
      "VisitData" : "161673",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SE5KU0bGxfcG,,/HNJSMPP360.m3u8",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    }, {\
      "VisitData" : "3",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SE5KDMlPTIwMTQ,,/HNJSMPP360.ts",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    } ]
  },
  "StartTime" : "2018-10-03T16:00:00Z",
  "Url500List" : {
    "UrlList" : [ {\
      "VisitData" : "161673",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SE5KU0GNfbGl2ZQ,,/HNJSMPP360.m3u8",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
    }, {\
      "VisitData" : "3",\
      "UrlDetail" : "http://example.com/nn_live/nn_x64/aWQ9SE5KU01QUDZXg9MQ,,/HNJSMPP360.ts",\
      "VisitProportion" : 0.35,\
      "Flow" : "460486880",\
      "FlowProportion" : 0.35\
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
| 400 | InvalidTime.ValueNotSupported | StartTime or EndTime is miss match. | 开始时间和结束时间不匹配、时间跨度超限或时间参数错误。 |

访问 [错误中心](https://error-center.aliyun.com/status/product/Cdn) 查看更多错误码。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 获取回源热门URL

# 获取回源热门URL

更新时间：2022-08-17 02:12:22

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