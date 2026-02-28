### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[CloudLens](https://help.aliyun.com/zh/sls/cloudlens-46/)[CloudLens for OSS](https://help.aliyun.com/zh/sls/cloudlens-for-oss/)日志字段详情

# 日志字段详情

更新时间：2025-12-23 03:25:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置异常检测功能](https://help.aliyun.com/zh/sls/configure-the-anomaly-detection-feature)[下一篇：CloudLens for PolarDB](https://help.aliyun.com/zh/sls/cloudlens-for-polardb-usage-notes/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

OSS日志类型

访问明细日志

计量日志

批量删除日志

时序监控指标

附录：访问类型

本文介绍OSS日志字段详情。

## OSS日志类型

| **日志类型** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **日志类型** | **说明** |
| 访问明细日志 | - 需要手动开通，开通步骤请参见 [开启日志采集功能](https://help.aliyun.com/zh/sls/enable-the-log-collection-feature-46 "")。<br>  <br>- 实时采集相关OSS Bucket的所有访问日志、批量删除日志时的删除信息。<br>  <br>  <br>  <br>  **说明**<br>  <br>  <br>  <br>  <br>  <br>  - 当您调用DeleteObjects接口时，访问日志中会有一条请求记录。<br>    <br>  - `oss-log-store`可能同时包含 **访问明细日志** 与 **每小时计量日志**（不同于下面的计量日志），`_topic_:oss_access_log`代表 **访问明细日志**，`_topic_:oss_metering_log`代表 **每小时计量日志**。 |
| 计量日志 | - 默认免费开通。<br>  <br>- 记录特定OSS Bucket每小时累计的计量数据。日志采集时间比实际产生时间延迟几小时，用于辅助分析。 |
| 时序监控数据 | - 默认免费开通。<br>  <br>- 记录10秒粒度的请求、延迟、流量等指标及5分钟粒度的请求、流量等指标。 |

## 访问明细日志

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为oss\_access\_log。 |
| time | OSS请求结束时间，例如27/Feb/2018:13:58:45。<br>如果需要时间戳，可以使用\_\_time\_\_字段。 |
| access\_id | 请求者的AccessKey ID。 |
| owner\_id | OSS Bucket拥有者的阿里云账号ID。 |
| user\_agent | HTTP的User-Agent头，例如curl/7.15.5。 |
| logging\_flag | 是否开启定期导出日志到OSS Bucket的功能。其中，true表示开启。 |
| bucket | OSS Bucket名称。 |
| content\_length\_in | 请求头中Content-Length的值，单位：字节。 |
| content\_length\_out | 响应头中Content-Length的值，单位：字节。 |
| object | 请求的OSS Object，格式为URL编码。<br>查询时可以使用`select url_decode(object)`解码。 |
| object\_size | OSS Object的大小，单位：字节。 |
| operation | 访问类型。更多信息，请参见 [附录：访问类型](https://help.aliyun.com/zh/sls/log-fields-17#section-z8x-xpl-qbi "")。 |
| bucket\_location | OSS Bucket所在的数据中心，一般格式为`oss-<region ID>`。 |
| request\_uri | HTTP请求的URI，包括query-string，格式为URL编码。<br>查询时可以使用`select url_decode(request_uri)`解码。 |
| error\_code | OSS返回的错误码。更多信息，请参见 [OSS错误码](https://help.aliyun.com/zh/oss/user-guide/overview-14#concept-dt2-hq3-wdb "")。 |
| request\_length | HTTP请求的大小，包括header，单位：字节。 |
| client\_ip | 发起请求的IP地址，即客户端IP地址、其网络防火墙或Proxy IP地址。 |
| response\_body\_length | HTTP响应中的Body大小，不包括header。 |
| http\_method | HTTP请求方法。 |
| referer | 请求的HTTP Referer。 |
| requester\_id | 请求者的ID，如果是匿名访问，则显示为短划线（-）。 |
| request\_id | 请求ID。 |
| response\_time | HTTP响应时间，单位：毫秒。 |
| server\_cost\_time | OSS服务器处理本次请求所花的时间，单位：毫秒。 |
| http\_type | HTTP请求类型，包括HTTP和HTTPS。 |
| sign\_type | 签名类型。<br>- NotSign：未签名。<br>  <br>- NormalSign：一般方式签名。<br>  <br>- UriSign：通过URL签名。<br>  <br>- AdminSign：管理员账号。<br>  <br>- NORMAL\_SIGN4： [V4签名。](https://help.aliyun.com/zh/oss/developer-reference/guidelines-for-upgrading-v1-signatures-to-v4-signatures "")。<br>  <br>- URI\_SIGN4： [在URL中包含V4签名](https://help.aliyun.com/zh/oss/developer-reference/add-signatures-to-urls "")。 |
| http\_status | HTTP请求返回的状态。 |
| sync\_request | 同步请求类型。<br>- 短划线（-）：一般请求。<br>  <br>- cdn：CDN回源。<br>  <br>- lifecycle：设置生命周期规则。 |
| bucket\_storage\_type | OSS Object存储类型。<br>- standard：标准存储类型。<br>  <br>- archive：归档存储类型。<br>  <br>- IA：低频访问存储类型。 |
| host | 请求访问域名，例如：bucket123.oss-cn-beijing.aliyuncs.com。 |
| vpc\_addr | OSS所在VPC的Havip地址。<br>该地址为整数类型（例如343819108）。您可以使用`int_to_ip(cast(vpc_addr as bigint))`将其转换为IP地址形式，转换后需要将IP地址倒序。例如，转换结果为`9.58.XXX.XXX`，倒序后的结果为`XXX.XXX.58.9`。 |
| vpc\_id | OSS所在VPC的ID。 |
| delta\_data\_size | OSS Object大小的变化量，如果没有变化则为0；如果不是上传请求，则为短划线（-） 。 |
| ec | 详细错误码。根据错误码自助排查的步骤，请参见 [使用EC错误码自助排查](https://help.aliyun.com/zh/oss/support/self-troubleshooting-by-using-error-codes "")。 |
| acc\_access\_region | 如果是传输加速请求，该字段为请求接入点所在地域名，否则为短划线（-）。 |
| restore\_priority | 解冻优先级。 |
| extend\_information | 扩展字段，默认为短划线（-）。<br>如果是通过RAM角色发起的请求，则日志会记录相关的RAM角色信息，拼接规则为`requesterParentId,roleName,roleSessionName,roleOwnerId`，以半角逗号（,）分隔，可能会继续拼接新字段。 |
| user\_defined\_log\_fields | 扩展字段，默认为短划线（-）。 <br>如果您为该Bucket配置了自定义header和param，则日志会记录与配置中相匹配的header和param的信息，为一个JSON字段进行base64编码后的值。 |
| archive\_direct\_read\_size | 请求产生的归档直读计量大小。如果是非归档直读，则为短划线（-），单位：字节。 |

## 计量日志

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为oss\_metering\_log。 |
| owner\_id | OSS Bucket拥有者的阿里云账号ID。 |
| bucket | OSS Bucket名称。 |
| cdn\_in | CDN流入量，单位：字节。 |
| cdn\_out | CDN流出量，单位：字节。 |
| metering\_datasize | 非标准存储的计量数据大小。 |
| get\_request | GET请求次数。 |
| intranet\_in | 内网流入量，单位：字节。 |
| intranet\_out | 内网流出量，单位：字节。 |
| network\_in | 外网流入量，单位：字节。 |
| network\_out | 外网流出量，单位：字节。 |
| put\_request | PUT请求次数。 |
| storage | OSS Bucket存储量，单位：字节。 |
| storage\_type | OSS Bucket存储类型 。<br>- standard：标准存储类型。<br>  <br>- archive：归档存储类型。<br>  <br>- IA：低频访问存储类型。 |
| process\_img\_size | 处理的图像大小，单位：字节。 |
| sync\_in | 同步流入量，单位：字节。 |
| sync\_out | 同步流出量，单位：字节。 |
| start\_time | 计量开始时间戳，单位：秒。 |
| end\_time | 计量截止时间戳，单位：秒。 |
| region | OSS Bucket所在地域。 |
| process\_img | 处理图像。 |
| bucket\_location | OSS Bucket所在的数据中心，一般格式为oss-<region ID>。 |
| standard\_total | 标准存储-总物理容量，单位：字节。 |
| standard\_lrs | 标准存储-本地冗余-物理容量，单位：字节。 |
| standard\_zrs | 标准存储-同城冗余-物理容量，单位：字节。 |
| ia\_total | 低频存储-总物理容量，单位：字节。 |
| ia\_lrs | 低频存储-本地冗余-物理容量，单位：字节。 |
| ia\_zrs | 低频存储-同城冗余-物理容量，单位：字节。 |
| ia\_total\_charged\_datasize | 低频存储-总计费容量，单位：字节。 |
| ia\_lrs\_charged\_datasize | 低频存储-本地冗余-计费容量，单位：字节。 |
| ia\_zrs\_charged\_datasize | 低频存储-同城冗余-计费容量，单位：字节。 |
| archive\_total | 归档存储-总物理容量，单位：字节。 |
| archive\_lrs | 归档存储-本地冗余-物理容量，单位：字节。 |
| archive\_zrs | 归档存储-同城冗余-物理容量，单位：字节。 |
| archive\_total\_charged\_datasize | 归档存储-总计费容量，单位：字节。 |
| archive\_lrs\_charged\_datasize | 归档存储-本地冗余-计费容量，单位：字节。 |
| archive\_zrs\_charged\_datasize | 归档存储-同城冗余-计费容量，单位：字节。 |
| coldarchive\_total | 冷归档存储-总物理容量，单位：字节。 |
| coldarchive\_lrs | 冷归档存储-本地冗余-物理初始容量，单位：字节。 |
| coldarchive\_total\_charged\_datasize | 冷归档存储-总计费容量，单位：字节。 |
| coldarchive\_lrs\_charged\_datasize | 冷归档存储-本地冗余-计费容量，单位：字节。 |
| deepcoldarchive\_total | 深度冷归档-总物理容量，单位：字节。 |
| deepcoldarchive\_lrs | 深度冷归档-本地冗余-物理容量，单位：字节。 |
| deepcoldarchive\_total\_charged\_datasize | 深度冷归档-总计费容量，单位：字节。 |
| deepcoldarchive\_lrs\_charged\_datasize | 深度冷归档-本地冗余-计费容量，单位：字节。 |
| reserved\_capacity | 预留空间-总已使用容量，单位：字节。 |
| reserved\_capacity\_lrs | 预留空间-本地冗余-已使用容量，单位：字节。 |
| reserved\_capacity\_zrs | 预留空间-同城冗余-已使用容量，单位：字节。 |
| total\_storage | 总物理容量，单位：字节。 |
| total\_storage\_charged\_datasize | 总计费容量（不包括标准存储），单位：字节。 |

## 批量删除日志

当您调用DeleteObjects接口时，访问日志中会有一条请求记录。但因为删除的文件信息存放在请求的HTTP Body中，访问日志中的object字段值为短划线（-）。查看具体的删除文件的列表，需要查看批量删除日志。批量删除日志的字段及说明如下，可以通过request\_id字段关联。

| **字段名称** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段名称** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为oss\_batch\_delete\_log。 |
| bucket | OSS Bucket名称。 |
| bucket\_location | OSS Bucket所在的数据中心，格式为oss-<region ID>。 |
| client\_ip | 发起请求的IP地址，例如客户端IP地址、其网络防火墙或Proxy的IP地址。 |
| delta\_data\_size | OSS Object大小的变化量，如果没有变化则为0；如果不是上传请求，则为短划线（-）。 |
| error\_code | OSS返回的错误码。更多信息，请参见 [OSS错误码](https://help.aliyun.com/zh/oss/user-guide/overview-14#undefined "")。 |
| host | 请求访问域名，例如bucket123.oss-cn-beijing.aliyuncs.com。 |
| http\_method | HTTP请求方法，例如POST。 |
| http\_status | HTTP请求返回的状态。 |
| logging\_flag | 是否开启定期导出日志到OSS Bucket的功能，true表示开启。 |
| object | 请求的OSS Object，格式为URL编码，查询时可以使用`select url_decode(object)`解码。 |
| object\_size | OSS Object的大小，对应请求对象的大小，单位：字节。 |
| operation | 访问类型。更多信息，请参见 [日志字段详情](https://help.aliyun.com/zh/sls/log-fields-13#section-qll-cvs-zdb "") 。 |
| owner\_id | OSS Bucket拥有者的阿里云账号ID。 |
| response\_body\_length | HTTP响应Body的大小，不包括header。 |
| request\_length | HTTP请求的大小，包括header，单位：字节。 |
| referer | 请求的HTTP Referer。 |
| request\_id | 请求ID。 |
| requester\_id | 请求者的ID，如果匿名访问则为短划线（-）。 |
| request\_uri | 请求的URI，包括query-string，格式为URL编码，查询时可以使用`select url_decode(request_uri)`解码。 |
| sync\_request | 同步请求类型。<br>- 短划线（-）：一般请求。<br>  <br>- cdn：CDN回源。<br>  <br>- lifecycle：设置生命周期规则。 |
| server\_cost\_time | OSS服务器处理本次请求的时间，单位：毫秒。 |
| user\_agent | HTTP的User-Agent头，例如curl/7.15.5。 |

## 时序监控指标

本文涉及的指标遵循 [时序数据格式](https://help.aliyun.com/zh/sls/metric#concept-2539048 "")，支持使用PromQL或SQL进行查询分析。更多信息，请参见 [时序数据查询与分析简介](https://help.aliyun.com/zh/sls/time-metric-data-query-and-analysis-syntax#concept-2539032 "")。

| **指标** | **单位** | **说明** | **标签** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **指标** | **单位** | **说明** | **标签** |
| private\_net\_in\_traffic\_10s | byte | 每10秒内的内网流入流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| private\_net\_out\_traffic\_10s | byte | 每10秒内的内网流出流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| public\_net\_in\_traffic\_10s | byte | 每10秒内的公网流入流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| public\_net\_out\_traffic\_10s | byte | 每10秒内的公网流出流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| cdn\_in\_10s | byte | 每10秒内的CDN流入流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| cdn\_out\_10s | byte | 每10秒内的CDN流出流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| sync\_in\_10s | byte | 每10秒内的同步请求流入流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| sync\_out\_10s | byte | 每10秒内的同步请求流出流量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| request\_cnt\_total\_10s | Count | 每10秒内的请求总数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| write\_qps\_10s | Count | 每10s内的计费PUT、POST、HEAD请求次数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| read\_qps\_10s | Count | 每10秒内的计费GET请求次数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_4xx\_10s | Count | 每10秒内的4xx请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_403\_10s | Count | 每10秒内的403请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_404\_10s | Count | 每10秒内的404请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_408\_10s | Count | 每10秒内的408请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_499\_10s | Count | 每10秒内的499请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_5xx\_10s | Count | 每10秒内的5xx请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_503\_10s | Count | 每10秒内的503请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| success\_2xx\_10s | Count | 每10秒内的2xx请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| success\_203\_10s | Count | 每10秒内203请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| success\_3xx\_10s | Count | 每10秒内的3xx请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| client\_latency\_10s | millsecond | 每10秒内的客户端延迟。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| server\_latency\_10s | millsecond | 每10秒内的服务端延迟。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| request\_cnt\_level4\_10s | Count | 每10秒内的请求个数，对应的请求文件大于1 MB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| client\_latency\_level4\_10s | millsecond | 每10秒内的客户端延迟，对应的请求文件大于1 MB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| server\_latency\_level4\_10s | millsecond | 每10秒内的服务端延迟，对应的请求文件大于1 MB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| request\_cnt\_level2\_10s | Count | 每10秒内的请求个数，对应的请求文件在100 KB~200 KB之间。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| client\_latency\_level2\_10s | millsecond | 每10秒内的客户端延迟，对应的请求文件在100 KB~200 KB之间。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| server\_latency\_level2\_10s | millsecond | 每10秒内的服务端延迟，对应的请求文件在100 KB~200 KB之间。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| request\_cnt\_level1\_10s | Count | 每10秒内的请求个数，对应的请求文件小于100 KB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| client\_latency\_level1\_10s | millsecond | 每10秒内的客户端延迟，对应的请求文件小于100 KB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| server\_latency\_level1\_10s | millsecond | 每10秒内的服务端的延迟，对应的请求文件小于100 KB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| request\_cnt\_level3\_10s | Count | 每10秒内的请求个数，对应的请求文件在200 KB~1 MB之间。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| client\_latency\_level3\_10s | millsecond | 每10秒内的客户端延迟，对应的请求文件在200 KB~1 MB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| server\_latency\_level3\_10s | millsecond | 每10秒内的服务端延迟，对应的请求文件在200 KB~1 MB。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| error\_timeout\_10s | Count | 每10秒内超时的请求个数。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| delta\_add\_10s | byte | 每10秒内的存储增量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| delta\_del\_10s | byte | 每10秒内的存储减量。 | owner\_id、region、bucket、storage\_type、operation、sync\_type |
| top\_object\_pv\_5m | Count | 每5分钟内Top文件访问次数。 | owner\_id、region、bucket、storage\_type、object |
| top\_object\_bandwidth\_out\_5m | byte | 每5分钟内Top文件流出流量。 | owner\_id、region、bucket、storage\_type、object |
| top\_object\_bandwidth\_in\_5m | byte | 每5分钟内Top文件流入流量。 | owner\_id、region、bucket、storage\_type、object |
| top\_ip\_method\_pv\_5m | Count | 每5分钟内Top IP地址访问次数。 | owner\_id、region、bucket、storage\_type、operation、client\_ip |
| top\_ip\_method\_bandwidth\_out\_5m | byte | 每5分钟内Top IP地址流出流量。 | owner\_id、region、bucket、storage\_type、operation、client\_ip |
| top\_ip\_method\_bandwidth\_in\_5m | byte | 每5分钟内Top IP地址流入流量。 | owner\_id、region、bucket、storage\_type、operation、client\_ip |
| top\_ip\_storage\_pv\_5m | Count | 每5分钟内Top IP地址访问次数。 | owner\_id、region、bucket、storage\_type、client\_ip |
| top\_ip\_storage\_bandwidth\_out\_5m | byte | 每5分钟内Top IP地址流出流量。 | owner\_id、region、bucket、storage\_type、client\_ip |
| top\_ip\_storage\_bandwidth\_in\_5m | byte | 每5分钟内Top IP地址流入流量。 | owner\_id、region、bucket、storage\_type、client\_ip |
| top\_refer\_pv\_5m | Count | 每5分钟内Top Refer访问次数。 | owner\_id、region、bucket、storage\_type、refer |

其中，标签字段说明如下表所示。

| **标签字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **标签字段** | **说明** |
| owner\_id | OSS Bucket拥有者的阿里云账号ID。 |
| region | OSS Bucket所在地域。 |
| bucket | OSS Bucket名称。 |
| object | OSS对象名称。 |
| storage\_type | OSS Bucket存储类型。 |
| operation | 访问类型。更多信息，请参见 [附录：访问类型](https://help.aliyun.com/zh/sls/log-fields-17#section-z8x-xpl-qbi "")。 |
| sync\_type | 同步类型。 |
| client\_ip | 访问来源IP地址。 |
| refer | 请求的HTTP Refer。 |

## 附录：访问类型

访问类型如下表所示。更多信息，请参见 [API概览](https://help.aliyun.com/zh/oss/developer-reference/list-of-operations-by-function#reference-wrz-l2q-tdb "")。

| **操作** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **操作** | **说明** |
| AbortMultiPartUpload | 断点上传-中止。 |
| AppendObject | 追加上传文件。 |
| CompleteUploadPart | 完成断点上传。 |
| CopyObject | 复制文件。 |
| DeleteBucket | 删除Bucket。 |
| DeleteLiveChannel | 删除LiveChannel。 |
| DeleteObject | 删除文件。 |
| DeleteObjects | 删除多个文件。 |
| ExpireObject | 删除过期Object。 |
| GetBucket | 列举文件。 |
| GetBucketAcl | 获取Bucket权限。 |
| GetBucketCors | 查看Bucket的CORS规则。 |
| GetBucketEventNotification | 获取Bucket通知配置。 |
| GetBucketInfo | 查看Bucket信息。 |
| GetBucketLifecycle | 查看Bucket的Lifecycle配置。 |
| GetBucketLocation | 查看Bucket地域。 |
| GetBucketLog | 查看Bucket访问日志配置。 |
| GetBucketReferer | 查看Bucket防盗链设置。 |
| GetBucketReplication | 查看跨地域复制。 |
| GetBucketReplicationProgress | 查看跨地域复制进度。 |
| GetBucketStat | 获取bucket的相关信息。 |
| GetBucketWebSite | 查看Bucket的静态网站托管状态。 |
| get\_image\_exif | 获取图片的exif信息。 |
| get\_image\_info | 获取图片的长宽等信息。 |
| get\_image\_infoexif | 获取图片的长宽以及exif信息。 |
| GetLiveChannelStat | 获取LiveChannel状态信息。 |
| GetObject | 读取文件。 |
| GetObjectAcl | 获取文件访问权限。 |
| GetObjectInfo | 获取文件信息。 |
| GetObjectMeta | 查看文件信息。 |
| GetObjectSymlink | 获取symlink文件的详细信息。 |
| GetPartData | 获取断点文件块数据。 |
| GetPartInfo | 获取断点文件块信息。 |
| GetProcessConfiguration | 获取Bucket图片处理配置。 |
| GetService | 列举Bucket。 |
| get\_style | 获取Bucket样式。 |
| HeadBucket | 查看Bucket信息。 |
| HeadObject | 查看文件信息。 |
| InitiateMultipartUpload | 初始化断点上传文件。 |
| ListMultiPartUploads | 列举断点事件。 |
| ListParts | 列举断点块状态。 |
| list\_style | 列举Bucket的样式。 |
| PostObject | 表单上传文件。 |
| PostProcessTask | 提交相关的数据处理，例如截图等。 |
| PostVodPlaylist | 创建LiveChannel点播列表。 |
| ProcessImage | 图片处理。 |
| PutBucket | 创建Bucket。 |
| PutBucketCors | 设置Bucket的CORS规则。 |
| PutBucketLifecycle | 设置Bucket的Lifecycle配置。 |
| PutBucketLog | 设置Bucket访问日志。 |
| PutBucketWebSite | 设置Bucket静态网站托管模式。 |
| PutLiveChannel | 创建LiveChannel。 |
| PutLiveChannelStatus | 设置LiveChannel状态。 |
| PutObject | 上传文件。 |
| PutObjectAcl | 修改文件访问权限。 |
| PutObjectSymlink | 创建symlink文件。 |
| put\_style | 创建Bucket样式。 |
| RedirectBucket | bucket endpoint重定向。 |
| RestoreObject | 解冻文件。 |
| UploadPart | 断点上传文件。 |
| UploadPartCopy | 复制文件块。 |