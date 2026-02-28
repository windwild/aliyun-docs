本文介绍基于负载均衡7层访问日志提取的指标详情，包括全局指标、app\_lb\_id维度指标、status维度指标和upstream\_status维度指标。

本文涉及的指标遵循 [时序数据格式](https://help.aliyun.com/zh/sls/metric#concept-2539048 "")，支持使用PromQL或SQL进行查询分析。更多信息，请参见 [时序数据查询和分析简介](https://help.aliyun.com/zh/sls/time-metric-data-query-and-analysis-syntax#concept-2539032 "")。

## 全局指标

全局指标信息如下表所示。

| 指标 | 说明 |
| --- | --- |

| 指标 | 说明 |
| --- | --- |
| pv | 总访问次数 |
| body\_bytes\_sent\_avg | 发送给客户端的HTTP Body平均字节数 |
| body\_bytes\_sent\_sum | 发送给客户端的HTTP Body总字节数 |
| request\_length\_avg | 请求报文的平均长度 |
| request\_length\_sum | 请求报文的总长度 |
| request\_time\_avg | 请求时间的平均值 |
| request\_time\_p50 | 请求时间的50分位值 |
| request\_time\_p90 | 请求时间的90分位值 |
| request\_time\_p99 | 请求时间的99分位值 |
| upstream\_response\_time\_avg | 请求连接时长的平均值<br>**说明**<br>upstream\_response\_time表示请求连接时长，该时长包括从负载均衡向后端建立连接开始到接收数据，然后关闭连接为止的时间。 |
| upstream\_response\_time\_p50 | 请求连接时长的50分位值 |
| upstream\_response\_time\_p90 | 请求连接时长的90分位值 |
| upstream\_response\_time\_p99 | 请求连接时长的99分位值 |

## app\_lb\_id维度

app\_lb\_id维度指标的标签为app\_lb\_id，指标详情如下表所示。

| 指标 | 单位 | 说明 | 标签 |
| --- | --- | --- | --- |

| 指标 | 单位 | 说明 | 标签 |
| --- | --- | --- | --- |
| pv:app\_lb\_id | count | ALB实例访问次数 | app\_lb\_id |
| body\_bytes\_sent\_avg:app\_lb\_id | byte | 发送给客户端的HTTP Body平均字节数 | app\_lb\_id |
| body\_bytes\_sent\_sum:app\_lb\_id | byte | 发送给客户端的HTTP Body总字节数 | app\_lb\_id |
| request\_length\_avg:app\_lb\_id | byte | 请求报文的平均长度 | app\_lb\_id |
| request\_length\_sum:app\_lb\_id | byte | 请求报文的总长度 | app\_lb\_id |
| request\_time\_avg:app\_lb\_id | second | 请求时间的平均值 | app\_lb\_id |
| request\_time\_p50:app\_lb\_id | second | 请求时间的50分位值 | app\_lb\_id |
| request\_time\_p90:app\_lb\_id | second | 请求时间的90分位值 | app\_lb\_id |
| request\_time\_p99:app\_lb\_id | second | 请求时间的99分位值 | app\_lb\_id |
| upstream\_response\_time\_avg:app\_lb\_id | second | 请求连接时长的平均值<br>**说明**<br>upstream\_response\_time表示请求连接时长，该时长包括从负载均衡向后端建立连接开始到接收数据，然后关闭连接为止的时间。 | app\_lb\_id |
| upstream\_response\_time\_p50:app\_lb\_id | second | 请求连接时长的50分位值 | app\_lb\_id |
| upstream\_response\_time\_p90:app\_lb\_id | second | 请求连接时长的90分位值 | app\_lb\_id |
| upstream\_response\_time\_p99:app\_lb\_id | second | 请求连接时长的99分位值 | app\_lb\_id |

## status维度

status维度指标的标签为app\_lb\_id+host+status，指标详情如下表所示。

| 指标 | 单位 | 说明 | 标签 |
| --- | --- | --- | --- |

| 指标 | 单位 | 说明 | 标签 |
| --- | --- | --- | --- |
| pv:app\_lb\_id:host:status | count | 每个app\_lb\_id、host、status的访问次数 | app\_lb\_id+host+status |
| body\_bytes\_sent\_avg:app\_lb\_id:host:status | byte | 发送给客户端的HTTP Body平均字节数 | app\_lb\_id+host+status |
| body\_bytes\_sent\_sum:app\_lb\_id:host:status | byte | 发送给客户端的HTTP Body总字节数 | app\_lb\_id+host+status |
| request\_length\_avg:app\_lb\_id:host:status | byte | 请求报文的平均长度 | app\_lb\_id+host+status |
| request\_length\_sum:app\_lb\_id:host:status | byte | 请求报文的总长度 | app\_lb\_id+host+status |
| request\_time\_avg:app\_lb\_id:host:status | second | 请求时间的平均值 | app\_lb\_id+host+status |
| request\_time\_p50:app\_lb\_id:host:status | second | 请求时间的50分位值 | app\_lb\_id+host+status |
| request\_time\_p90:app\_lb\_id:host:status | second | 请求时间的90分位值 | app\_lb\_id+host+status |
| request\_time\_p99:app\_lb\_id:host:status | second | 请求时间的99分位值 | app\_lb\_id+host+status |
| upstream\_response\_time\_avg:app\_lb\_id:host:status | second | 请求连接时长的平均值<br>**说明**<br>upstream\_response\_time表示请求连接时长，该时长包括从负载均衡向后端建立连接开始到接收数据，然后关闭连接为止的时间。 | app\_lb\_id+host+status |
| upstream\_response\_time\_p50:app\_lb\_id:host:status | second | 请求连接时长的50分位值 | app\_lb\_id+host+status |
| upstream\_response\_time\_p90:app\_lb\_id:host:status | second | 请求连接时长的90分位值 | app\_lb\_id+host+status |
| upstream\_response\_time\_p99:app\_lb\_id:host:status | second | 请求连接时长的99分位值 | app\_lb\_id+host+status |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[CloudLens](https://help.aliyun.com/zh/sls/cloudlens-46/)[CloudLens for ALB（原ALB日志中心）](https://help.aliyun.com/zh/sls/usage-notes-15/)指标说明

# 指标说明

更新时间：2023-05-22 01:58:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查看数据报表](https://help.aliyun.com/zh/sls/view-reports)[下一篇：日志字段详情](https://help.aliyun.com/zh/sls/log-fields-10)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

全局指标

app\_lb\_id维度

status维度