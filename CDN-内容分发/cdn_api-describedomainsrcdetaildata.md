调用DescribeDomainSrcDetailData查询回源详细数据，支持查询7天内的数据。

**说明**

- 单次查询StartTime和EndTime跨度不能超过1天。
- 单用户调用频率：10次/秒。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Cdn&api=DescribeDomainSrcDetailData&type=RPC&version=2018-05-10)

## 请求参数

| 名称 | 类型 | 是否必选 | 示例值 | 描述 |
| --- | --- | --- | --- | --- |
| Action | String | 是 | DescribeDomainSrcDetailData | 系统规定参数，取值： **DescribeDomainSrcDetailData**。 |
| DomainName | String | 是 | example.com | 加速域名，多个用半角逗号（,）分隔。 |
| StartTime | String | 是 | 2018-06-05T20:00:00Z | 获取数据起始时间点。日期格式按照ISO8601表示法，并使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
| EndTime | String | 是 | 2018-06-05T20:10:00Z | 获取数据结束时间点。日期格式按照ISO8601表示法，并使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
| Field | String | 是 | qps,bps,http\_code | 获取的维度，多个用半角逗号（,）分隔。取值：<br>- qps<br>- bps<br>- http\_code |

## 返回数据

| 名称 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- |
| Data | String | { "bps": 306202454542.3067, "domain\_name": "example.com",<br> "qps": 71814.53333333334, "http\_code": { "200": 466521,<br> "304": 35, "400": 16594, "404": 112, <br> "502": 10038, "504": 151 }, "time\_stp": "2018-06-05T20:00:00Z"<br> } | 回源详细数据。 |
| RequestId | String | B49E6DDA-F413-422B-B58E-2FA23F286726 | 请求ID。 |

## 示例

请求示例

```
https://cdn.aliyuncs.com?Action=DescribeDomainSrcDetailData
&DomainName=example.com
&Field=qps,bps,http_code
&StartTime=2018-06-05T20:00:00Z
&EndTime=2018-06-05T20:10:00Z
&<公共请求参数>
```

正常返回示例

`XML`格式


```
<DescribeDomainSrcDetailDataResponse>
<Data>
    <bps>306202454542.3067</bps>
    <domain_name>example.com</domain_name>
    <qps>71814.53333333334</qps>
    <http_code>
        <200>466521</200>
        <304>35</304>
        <400>16594</400>
        <404>112</404>
        <502>10038</502>
        <504>151</504>
    </http_code>
    <time_stp>2018-06-05T20:00:00Z</time_stp>
</Data>
<RequestId>B49E6DDA-F413-422B-B58E-2FA23F286726</RequestId>
</DescribeDomainSrcDetailDataResponse>
```

`JSON`格式


```
{
   "Data":[\
        {\
            "bps": 306202454542.3067,\
            "domain_name": "example.com",\
            "qps": 71814.53333333334,\
            "http_code": {\
                "200": 466521,\
                "304": 35,\
                "400": 16594,\
                "404": 112,\
                "502": 10038,\
                "504": 151\
            },\
            "time_stp": "2018-06-05T20:00:00Z"\
        }\
   ],
   "RequestId":"B49E6DDA-F413-422B-B58E-2FA23F286726"
}
```

## 错误码

| HttpCode | 错误码 | 错误信息 | 描述 |
| --- | --- | --- | --- |
| 400 | InvalidEndTime.Mismatch | Specified end time does not math the specified start time. | 请检查时间设置是否正确，结束时间不能小于或等于开始时间。 |

访问[错误中心](https://error-center.aliyun.com/status/product/Cdn)查看更多错误码。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/)

# 查询回源详细数据

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈