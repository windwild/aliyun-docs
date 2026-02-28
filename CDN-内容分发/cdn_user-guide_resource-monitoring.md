### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[监控查询](https://help.aliyun.com/zh/cdn/user-guide/monitoring-and-usage-analytics/)资源监控

# 资源监控

更新时间：2025-11-21 02:08:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：回源常见问题](https://help.aliyun.com/zh/cdn/user-guide/back-to-source-faq)[下一篇：实时监控](https://help.aliyun.com/zh/cdn/user-guide/real-time-monitoring)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

支持查询的时间粒度

监控项和监控指标

注意事项

用量查询、资源监控、实时监控在数据统计维度上的区别

资源监控和实时监控的区别

操作步骤

资源监控基于客户端IP地址的归属区域或运营商，统计流量带宽、访问请求数、缓存命中率以及HTTP状态码等数据。通过对CDN资源的监控，您可以全面了解带宽使用情况以及缓存命中率等关键指标，从而进行优化和调整。

## 功能介绍

资源监控和实时监控相比，资源监控的单次查询最大时间和可查询历史数据时间范围更大，详情请参见下方报表。

### 支持查询的时间粒度

通过控制台查询数据和调用相关API接口查询时，单次查询的最大时间跨度和可查询历史数据时间范围存在区别。不同时间粒度对应的单次查询的最大时间跨度、可查询的历史数据时间范围和数据延迟关系如下：

- 通过控制台查询：




| **时间粒度** | **单次查询的最大时间跨度** | **可查询历史数据时间范围** | **数据延迟** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **时间粒度** | **单次查询的最大时间跨度** | **可查询历史数据时间范围** | **数据延迟** |
| 5分钟 | 3天 | 90天 | 15分钟 |
| 1小时 | 31天 | 90天 | 4小时 |
| 1天 | 90天 | 90天 | 次日凌晨4点 |

- 调用相关API接口查询：




| **时间粒度** | **单次查询的最大时间跨度** | **可查询历史数据时间范围** | **数据延迟** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **时间粒度** | **单次查询的最大时间跨度** | **可查询历史数据时间范围** | **数据延迟** |
| 5分钟 | 3天 | 93天 | 15分钟 |
| 1小时 | 31天 | 186天 | 4小时 |
| 1天 | 366天 | 366天 | 次日凌晨4点 |


### 监控项和监控指标

资源监控功能包含了下表中的六个监控项，您可以选择需要监控的域名、区域、运营商等，在线查看各监控项和监控指标的具体情况，也可以将查询结果下载到本地查看及分析。

**说明**

- 资源监控以客户端IP地址所在地区或者运营商归属来统计数据，计量计费以统计各个计费大区的CDN节点上产生的流量、带宽数据和请求数来统计数据。由于统计方式不同，两者结果会有一定的差异。资源监控的曲线图主要用于带宽趋势的展示，如果您需要查询计费账单对应的计量数据，可通过 [用量概述](https://help.aliyun.com/zh/cdn/user-guide/resource-usage-overview#task-187634 "") 查看。

- 数据计算和统计源于API，如需查看更详细的信息，请参见下表中对应的API文档。


| **监控项** | **监控指标** | **相关API** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **监控项** | **监控指标** | **相关API** |
| **访问流量/带宽** | 展示加速域名的带宽和流量。支持按区域、运营商和协议（HTTP、HTTPS、QUIC、IPv4和IPv6）查询。 | - [查询带宽-按协议](https://help.aliyun.com/zh/cdn/api-describedomainbpsdatabylayer#doc-api-Cdn-DescribeDomainBpsDataByLayer "")<br>  <br>- [查询用量-按天](https://help.aliyun.com/zh/cdn/api-describedomainsusagebyday#doc-api-Cdn-DescribeDomainsUsageByDay "") |
| **回源流量/带宽** | 展示加速域名的回源带宽和回源流量。<br>**说明**<br>- 回源宽带：指当用户请求的资源在CDN节点未命中时，CDN节点向源站请求资源所消耗的网络带宽。<br>  <br>- 回源流量：指当CDN节点无法从本地缓存中获取用户请求的内容时，需要向源服务器请求数据的流量。 | - [查询回源带宽](https://help.aliyun.com/zh/cdn/api-describedomainsrcbpsdata-2#doc-api-Cdn-DescribeDomainSrcBpsData "")<br>  <br>- [查询回源流量](https://help.aliyun.com/zh/cdn/api-describedomainsrctrafficdata#doc-api-Cdn-DescribeDomainSrcTrafficData "") |
| **访问请求数** | 展示加速域名的请求次数和QPS。支持按区域、运营商和协议（HTTP、HTTPS、QUIC、IPv4和IPv6）查询。<br>**说明**<br>- 加速域名的请求次数指最小时间粒度内的请求数总和（例如最小时间粒度为5分钟，那么展示的加速域名请求次数指5分钟内的请求数总和）。<br>  <br>- QPS指的是每秒的请求次数。 | [查询QPS-按协议](https://help.aliyun.com/zh/cdn/api-describedomainqpsdatabylayer#doc-api-Cdn-DescribeDomainQpsDataByLayer "") |
| **命中率** | 展示加速域名的字节命中率和请求命中率。<br>**说明**<br>- 字节命中率：单位时间内CDN节点响应用户的总字节数中，CDN节点直接响应（非回源）的字节数占比。计算公式为：（CDN节点响应用户的总字节数 \- 源站响应CDN节点的总字节数）÷ CDN节点响应用户的总字节数。<br>  <br>- 命中率：单位时间内所有请求（包含HTTP协议和HTTPS协议）的字节命中率。<br>  <br>- HTTPS命中率：单位时间内HTTPS请求的字节命中率。 | - [查询字节命中率](https://help.aliyun.com/zh/cdn/api-describedomainhitratedata#doc-api-Cdn-DescribeDomainHitRateData "")<br>  <br>- [查询请求命中率](https://help.aliyun.com/zh/cdn/api-describedomainreqhitratedata#doc-api-Cdn-DescribeDomainReqHitRateData "") |
| **HTTPCODE** | 展示加速域名的HTTP状态码信息，支持按照2xx、3xx、4xx和5xx维度查询。参考 [HTTP状态码](https://help.aliyun.com/zh/cdn/developer-reference/http-status-code-description "") 查看状态码详细说明和解决措施。<br>- **2xx成功**- **边缘响应**：表示客户端访问阿里云CDN节点时，请求已被服务器成功处理，并返回了相应的资源或确认信息。<br>  <br>- **4xx客户端错误** **-** **边缘响应**：表示客户端访问阿里云CDN节点时，由于客户端发送的请求有问题（例如，权限不足），阿里云CDN节点无法处理，请修改客户端请求内容后重新发送。<br>  <br>- **5xx服务器错误**- **边缘响应**：表示客户端访问阿里云CDN节点时，阿里云CDN节点的服务器出现了内部错误（例如，阿里云CDN节点负载过高），请检查源站配置（例如，源站的网络设置）。 | [查询HTTP状态码-按协议](https://help.aliyun.com/zh/cdn/api-describedomainhttpcodedatabylayer#doc-api-Cdn-DescribeDomainHttpCodeDataByLayer "") |
| **回源HTTPCODE** | 展示加速域名的回源HTTP状态码信息，支持按照2xx、3xx、4xx和5xx维度查询。参考 [HTTP状态码](https://help.aliyun.com/zh/cdn/developer-reference/http-status-code-description "") 查看状态码详细说明和解决措施。<br>- **4xx客户端错误** **-** **回源响应**：表示阿里云CDN节点访问源站时，由于阿里云CDN节点发送的请求有问题（例如，请求的资源不存在），源站服务器无法处理，请修改客户端请求内容或调整CDN域名配置后重新发送。<br>  <br>- **5xx服务器错误**- **回源响应**：表示阿里云CDN节点访问源站时，源站服务器出现了内部错误（例如：源站服务器负载过高），请检查源站配置（例如，源站的服务器负载）。 | [查询回源HTTP状态码](https://help.aliyun.com/zh/cdn/api-describedomainsrchttpcodedata#doc-api-Cdn-DescribeDomainSrcHttpCodeData "") |

## 注意事项

通过CDN/DCDN控制台（或者OpenAPI）的监控查询、用量查询（实际计费流量）功能查到的加速域名使用的流量数据与通过日志统计的流量数据有差异。通常来说，通过监控查询、用量查询功能查到的加速域名使用的流量数据是通过日志统计的流量数据的1.1倍，详细请参见 [为什么监控查询流量、用量查询流量与日志统计流量有差异](https://help.aliyun.com/zh/cdn/product-overview/traffic-amount-in-the-monitoring-and-usage-analytics-or-in-the-usage-statistics-feature-different-from-the-logged-traffic-amount#trouble-2320953 "")。

## 用量查询、资源监控、实时监控在数据统计维度上的区别

- 用量查询：按CDN节点维度来统计用量数据，每个CDN节点都唯一归属于某个计费大区，因此用量查询只能按计费大区来查询用量数据，例如，中国内地、亚太1区、北美区等。具体内容请参见[用量查询](https://help.aliyun.com/zh/cdn/user-guide/query-resource-usage-1)。

- 资源监控和实时监控：按客户端IP维度来统计监控数据，每个客户端IP都唯一归属于某个区域或者某个运营商，因此资源监控和实时监控只能按区域或者运营商（可以使用区域+运营商的组合）来查询监控数据。具体内容请参见 [资源监控](https://help.aliyun.com/zh/cdn/user-guide/resource-monitoring#task-261642 "") 和 [实时监控](https://help.aliyun.com/zh/cdn/user-guide/real-time-monitoring#task-2036744 "")。


## 资源监控和实时监控的区别

- 最低数据延迟：实时监控可以查询到延迟更低的数据。在实时监控下，当数据查询粒度为1分钟时，数据延迟约为5分钟；而资源监控只能在数据查询粒度为5分钟的情况下，将数据延迟控制在约15分钟左右。

- 最小数据粒度：实时监控可以查询到更小颗粒度的数据。实时监控可以查询的最小数据颗粒度为1分钟，而资源监控支持查询的最小数据颗粒度为5分钟。

- 可查询协议层：资源监控可以按更多的细分协议层来查询数据。资源监控支持按HTTP、HTTPS、QUIC、IPv4、IPv6这五种协议层来查询数据，而实时监控不支持。


## 操作步骤

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，选择**监控查询** \> **资源监控**。

3. 在 **资源监控** 页面，选择您要查看的监控项和查询条件，单击 **查询**。



系统会根据您选择的监控项和查询条件，显示查询结果。您可以在线分析查询结果，也可以将查询结果下载到本地进行分析。![资源监控](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4534096561/p93734.png)