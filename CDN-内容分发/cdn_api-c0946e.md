调用DescribeDomainISPData查询加速域名天粒度的用户运营商分布数据统计，支持获取最近90天的数据。

阿里云CDN产品的统计分析功能已经下线，与统计分析功能相关的OpenAPI接口已不再继续维护。鉴于当前该接口可能存在数据缺失、不准确等问题，建议您不要使用该接口。如果您有数据统计分析相关的需求，可以通过 [运营报表](https://help.aliyun.com/zh/cdn/user-guide/customize-an-operations-report-template-and-create-a-tracking-task) 或者 [投递实时日志到SLS](https://help.aliyun.com/zh/cdn/user-guide/best-practices-for-shipping-and-analyzing-alibaba-cloud-cdn-real-time-logs-in-log-service) 来实现。


**说明**

- 如果您不指定StartTime和EndTime时，该接口返回过去24小时的数据；指定StartTime和EndTime时，返回起止时间的数据。
- 该接口只支持获取一个域名或当前账户下所有域名的数据。
- 单用户调用频率：100次/秒。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Cdn&api=DescribeDomainISPData&type=RPC&version=2018-05-10)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求参数

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |
| Action | String | 是 | DescribeDomainISPData | 系统规定参数。取值： **DescribeDomainISPData**。 |
| DomainName | String | 否 | example.com | 加速域名，仅支持查询单个域名。<br>默认查询所有加速域名。 |
| StartTime | String | 否 | 2019-11-29T05:33:00Z | 获取数据起始时间点。日期格式按照ISO8601表示法，并使用UTC时间。格式为yyyy-MM-ddTHH:mm:ssZ。 |
| EndTime | String | 否 | 2019-11-30T05:40:00Z | 获取数据结束时间点。日期格式按照ISO8601表示法，并使用UTC时间。格式为yyyy-MM-ddTHH:mm:ssZ。<br>结束时间需大于起始时间。 |

## 返回数据

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |
| EndTime | String | 2019-11-30T05:40:00Z | 获取数据结束时间点。 |
| StartTime | String | 2019-11-29T05:33:00Z | 获取数据起始时间点。 |
| RequestId | String | DE81639B-DAC1-4C76-AB72-F34B836837D5 | 请求ID。 |
| DomainName | String | example.com | 加速域名。 |
| DataInterval | String | 86400 | 时间间隔，单位：秒。 |
| Value | Array of ISPProportionData |  | 各运营商访问占比数据列表。 |
| ISPProportionData |  |  |  |
| TotalQuery | String | 1 | 总请求次数。 |
| TotalBytes | String | 7081884 | 总流量。 |
| AvgResponseRate | String | 88.92594866772144 | 平均响应速度，单位：byte/毫秒。 |
| AvgResponseTime | String | 79638.0 | 平均响应时间，单位：毫秒。 |
| ReqErrRate | String | 0.0 | 请求错误率。 |
| AvgObjectSize | String | 7081884.7 | 响应平均大小，单位：byte。 |
| Bps | String | 1311.4601296296296 | 带宽。 |
| Qps | String | 2.3148148148148147E-5 | 每秒查询率。 |
| Proportion | String | 0.004509176173513099 | 占比使用数据。 |
| IspEname | String | alibaba | 运营商英文名称。 |
| ISP | String | 阿里巴巴 | 运营商信息。 |
| BytesProportion | String | 0.012220518530445479 | 总流量占比。 |

## 示例

请求示例

```1c
http://cdn.aliyuncs.com/?Action=DescribeDomainISPData
&DomainName=example.com
&StartTime=2015-12-05T00:00:00Z
&EndTime=2019-11-30T05:40:00Z
&<公共请求参数>
```

正常返回示例

`XML`格式


```xml
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeDomainISPDataResponse>
	<Value>
		<ISPProportionData>
			<ByteHitRate>100.0</ByteHitRate>
			<TotalQuery>1</TotalQuery>
			<Bps>1311.4601296296296</Bps>
			<Proportion>0.004509176173513099</Proportion>
			<AvgResponseRate>88.92594866772144</AvgResponseRate>
			<IspEname>alibaba</IspEname>
			<AvgObjectSize>7081884.7</AvgObjectSize>
			<ISP>阿里巴巴</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>2.3148148148148147E-5</Qps>
			<AvgResponseTime>79638.0</AvgResponseTime>
			<ReqHitRate>100.0</ReqHitRate>
			<TotalBytes>7081884</TotalBytes>
			<BytesProportion>0.012220518530445479</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>100.0</ByteHitRate>
			<TotalQuery>3</TotalQuery>
			<Bps>444.455</Bps>
			<Proportion>0.013527528520539298</Proportion>
			<AvgResponseRate>154.3345765545624</AvgResponseRate>
			<IspEname>overseas</IspEname>
			<AvgObjectSize>800019.0</AvgObjectSize>
			<ISP>海外ISP</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>6.944444444444444E-5</Qps>
			<AvgResponseTime>5183.666666666667</AvgResponseTime>
			<ReqHitRate>100.0</ReqHitRate>
			<TotalBytes>2400057</TotalBytes>
			<BytesProportion>0.004141544558417533</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>100.0</ByteHitRate>
			<TotalQuery>82</TotalQuery>
			<Bps>45838.64816666667</Bps>
			<Proportion>0.3697524462280741</Proportion>
			<AvgResponseRate>1025.5028528460102</AvgResponseRate>
			<IspEname>drpeng</IspEname>
			<AvgObjectSize>3018642.684146342</AvgObjectSize>
			<ISP>鹏博士</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>0.0018981481481481482</Qps>
			<AvgResponseTime>2943.5731707317073</AvgResponseTime>
			<ReqHitRate>100.0</ReqHitRate>
			<TotalBytes>247528700</TotalBytes>
			<BytesProportion>0.42713616424581613</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>99.99999999999999</ByteHitRate>
			<TotalQuery>114</TotalQuery>
			<Bps>65933.51396296297</Bps>
			<Proportion>0.5140460837804933</Proportion>
			<AvgResponseRate>484.6396117340071</AvgResponseRate>
			<IspEname>cernet</IspEname>
			<AvgObjectSize>3123166.4508771934</AvgObjectSize>
			<ISP>教育网</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>0.002638888888888889</Qps>
			<AvgResponseTime>6444.30701754386</AvgResponseTime>
			<ReqHitRate>100.0</ReqHitRate>
			<TotalBytes>356040975</TotalBytes>
			<BytesProportion>0.6143852267848392</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>100.0</ByteHitRate>
			<TotalQuery>207</TotalQuery>
			<Bps>81128.73735185186</Bps>
			<Proportion>0.9333994679172115</Proportion>
			<AvgResponseRate>752.2096624205244</AvgResponseRate>
			<IspEname>tietong</IspEname>
			<AvgObjectSize>2116401.843961353</AvgObjectSize>
			<ISP>铁通</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>0.004791666666666666</Qps>
			<AvgResponseTime>2813.5797101449275</AvgResponseTime>
			<ReqHitRate>100.0</ReqHitRate>
			<TotalBytes>438095181</TotalBytes>
			<BytesProportion>0.7559781771177001</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>100.00000000000001</ByteHitRate>
			<TotalQuery>256</TotalQuery>
			<Bps>129137.37100000001</Bps>
			<Proportion>1.1543491004193533</Proportion>
			<AvgResponseRate>321.5924922592767</AvgResponseRate>
			<IspEname>other</IspEname>
			<AvgObjectSize>2723991.4195312504</AvgObjectSize>
			<ISP>其他</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>0.005925925925925926</Qps>
			<AvgResponseTime>8470.3203125</AvgResponseTime>
			<ReqHitRate>100.0</ReqHitRate>
			<TotalBytes>697341803</TotalBytes>
			<BytesProportion>1.2033348171432345</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>99.14745652563326</ByteHitRate>
			<TotalQuery>2866</TotalQuery>
			<Bps>879955.1972037038</Bps>
			<Proportion>12.923298913288543</Proportion>
			<AvgResponseRate>1004.5513789924338</AvgResponseRate>
			<IspEname>mobile</IspEname>
			<AvgObjectSize>1657975.598360084</AvgObjectSize>
			<ISP>移动</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>0.06634259259259259</Qps>
			<AvgResponseTime>1650.463712491277</AvgResponseTime>
			<ReqHitRate>97.3831123517097</ReqHitRate>
			<TotalBytes>4751758064</TotalBytes>
			<BytesProportion>8.19964599032574</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>99.99981717005271</ByteHitRate>
			<TotalQuery>6534</TotalQuery>
			<Bps>3194660.60262963</Bps>
			<Proportion>29.46295711773459</Proportion>
			<AvgResponseRate>1171.525957981939</AvgResponseRate>
			<IspEname>unicom</IspEname>
			<AvgObjectSize>2640215.374074074</AvgObjectSize>
			<ISP>联通</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>0.15125</Qps>
			<AvgResponseTime>2253.6550352004897</AvgResponseTime>
			<ReqHitRate>99.96939087848179</ReqHitRate>
			<TotalBytes>17251167254</TotalBytes>
			<BytesProportion>29.768658772680293</BytesProportion>
		</ISPProportionData>
		<ISPProportionData>
			<ByteHitRate>99.99968869093071</ByteHitRate>
			<TotalQuery>12114</TotalQuery>
			<Bps>6333214.260796296</Bps>
			<Proportion>54.62416016593768</Proportion>
			<AvgResponseRate>984.184264638081</AvgResponseRate>
			<IspEname>telecom</IspEname>
			<AvgObjectSize>2823126.71357933</AvgObjectSize>
			<ISP>电信</ISP>
			<ReqErrRate>0.0</ReqErrRate>
			<Qps>0.28041666666666665</Qps>
			<AvgResponseTime>2868.494056463596</AvgResponseTime>
			<ReqHitRate>99.97523526498266</ReqHitRate>
			<TotalBytes>34199357008</TotalBytes>
			<BytesProportion>59.01449878861353</BytesProportion>
		</ISPProportionData>
	</Value>
	<DataInterval>86400</DataInterval>
	<RequestId>DE81639B-DAC1-4C76-AB72-F34B836837D5</RequestId>
	<DomainName>example.com</DomainName>
	<EndTime>2019-11-29T05:33:00Z</EndTime>
	<StartTime>2019-11-29T05:33:00Z</StartTime>
</DescribeDomainISPDataResponse>
```

`JSON`格式


```ada
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Value" : {
    "ISPProportionData" : [ {\
      "ByteHitRate" : "100.0",\
      "TotalQuery" : "1",\
      "Bps" : "1311.4601296296296",\
      "Proportion" : "0.004509176173513099",\
      "AvgResponseRate" : "88.92594866772144",\
      "IspEname" : "alibaba",\
      "AvgObjectSize" : "7081884.7",\
      "ISP" : "阿里巴巴",\
      "ReqErrRate" : "0.0",\
      "Qps" : "2.3148148148148147E-5",\
      "AvgResponseTime" : "79638.0",\
      "ReqHitRate" : "100.0",\
      "TotalBytes" : "7081884",\
      "BytesProportion" : "0.012220518530445479"\
    }, {\
      "ByteHitRate" : "100.0",\
      "TotalQuery" : "3",\
      "Bps" : "444.455",\
      "Proportion" : "0.013527528520539298",\
      "AvgResponseRate" : "154.3345765545624",\
      "IspEname" : "overseas",\
      "AvgObjectSize" : "800019.0",\
      "ISP" : "海外ISP",\
      "ReqErrRate" : "0.0",\
      "Qps" : "6.944444444444444E-5",\
      "AvgResponseTime" : "5183.666666666667",\
      "ReqHitRate" : "100.0",\
      "TotalBytes" : "2400057",\
      "BytesProportion" : "0.004141544558417533"\
    }, {\
      "ByteHitRate" : "100.0",\
      "TotalQuery" : "82",\
      "Bps" : "45838.64816666667",\
      "Proportion" : "0.3697524462280741",\
      "AvgResponseRate" : "1025.5028528460102",\
      "IspEname" : "drpeng",\
      "AvgObjectSize" : "3018642.684146342",\
      "ISP" : "鹏博士",\
      "ReqErrRate" : "0.0",\
      "Qps" : "0.0018981481481481482",\
      "AvgResponseTime" : "2943.5731707317073",\
      "ReqHitRate" : "100.0",\
      "TotalBytes" : "247528700",\
      "BytesProportion" : "0.42713616424581613"\
    }, {\
      "ByteHitRate" : "99.99999999999999",\
      "TotalQuery" : "114",\
      "Bps" : "65933.51396296297",\
      "Proportion" : "0.5140460837804933",\
      "AvgResponseRate" : "484.6396117340071",\
      "IspEname" : "cernet",\
      "AvgObjectSize" : "3123166.4508771934",\
      "ISP" : "教育网",\
      "ReqErrRate" : "0.0",\
      "Qps" : "0.002638888888888889",\
      "AvgResponseTime" : "6444.30701754386",\
      "ReqHitRate" : "100.0",\
      "TotalBytes" : "356040975",\
      "BytesProportion" : "0.6143852267848392"\
    }, {\
      "ByteHitRate" : "100.0",\
      "TotalQuery" : "207",\
      "Bps" : "81128.73735185186",\
      "Proportion" : "0.9333994679172115",\
      "AvgResponseRate" : "752.2096624205244",\
      "IspEname" : "tietong",\
      "AvgObjectSize" : "2116401.843961353",\
      "ISP" : "铁通",\
      "ReqErrRate" : "0.0",\
      "Qps" : "0.004791666666666666",\
      "AvgResponseTime" : "2813.5797101449275",\
      "ReqHitRate" : "100.0",\
      "TotalBytes" : "438095181",\
      "BytesProportion" : "0.7559781771177001"\
    }, {\
      "ByteHitRate" : "100.00000000000001",\
      "TotalQuery" : "256",\
      "Bps" : "129137.37100000001",\
      "Proportion" : "1.1543491004193533",\
      "AvgResponseRate" : "321.5924922592767",\
      "IspEname" : "other",\
      "AvgObjectSize" : "2723991.4195312504",\
      "ISP" : "其他",\
      "ReqErrRate" : "0.0",\
      "Qps" : "0.005925925925925926",\
      "AvgResponseTime" : "8470.3203125",\
      "ReqHitRate" : "100.0",\
      "TotalBytes" : "697341803",\
      "BytesProportion" : "1.2033348171432345"\
    }, {\
      "ByteHitRate" : "99.14745652563326",\
      "TotalQuery" : "2866",\
      "Bps" : "879955.1972037038",\
      "Proportion" : "12.923298913288543",\
      "AvgResponseRate" : "1004.5513789924338",\
      "IspEname" : "mobile",\
      "AvgObjectSize" : "1657975.598360084",\
      "ISP" : "移动",\
      "ReqErrRate" : "0.0",\
      "Qps" : "0.06634259259259259",\
      "AvgResponseTime" : "1650.463712491277",\
      "ReqHitRate" : "97.3831123517097",\
      "TotalBytes" : "4751758064",\
      "BytesProportion" : "8.19964599032574"\
    }, {\
      "ByteHitRate" : "99.99981717005271",\
      "TotalQuery" : "6534",\
      "Bps" : "3194660.60262963",\
      "Proportion" : "29.46295711773459",\
      "AvgResponseRate" : "1171.525957981939",\
      "IspEname" : "unicom",\
      "AvgObjectSize" : "2640215.374074074",\
      "ISP" : "联通",\
      "ReqErrRate" : "0.0",\
      "Qps" : "0.15125",\
      "AvgResponseTime" : "2253.6550352004897",\
      "ReqHitRate" : "99.96939087848179",\
      "TotalBytes" : "17251167254",\
      "BytesProportion" : "29.768658772680293"\
    }, {\
      "ByteHitRate" : "99.99968869093071",\
      "TotalQuery" : "12114",\
      "Bps" : "6333214.260796296",\
      "Proportion" : "54.62416016593768",\
      "AvgResponseRate" : "984.184264638081",\
      "IspEname" : "telecom",\
      "AvgObjectSize" : "2823126.71357933",\
      "ISP" : "电信",\
      "ReqErrRate" : "0.0",\
      "Qps" : "0.28041666666666665",\
      "AvgResponseTime" : "2868.494056463596",\
      "ReqHitRate" : "99.97523526498266",\
      "TotalBytes" : "34199357008",\
      "BytesProportion" : "59.01449878861353"\
    } ]
  },
  "DataInterval" : "86400",
  "RequestId" : "DE81639B-DAC1-4C76-AB72-F34B836837D5",
  "DomainName" : "example.com",
  "EndTime" : "2019-11-30T05:40:00Z",
  "StartTime" : "2019-11-29T05:33:00Z"
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
| 404 | InvalidDomain.NotFound | The domain provided does not exist in our records. | 域名不存在或不属于当前用户。请检查您填写的域名书写是否正确，或者域名是否在当前账号中，查看域名是否过期。 |

访问 [错误中心](https://error-center.aliyun.com/status/product/Cdn) 查看更多错误码。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 查询用户运营商分布数据

# 查询用户运营商分布数据

更新时间：2022-08-17 02:13:25

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