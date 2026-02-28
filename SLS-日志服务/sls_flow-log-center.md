### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)Flowlog日志中心

# Flowlog日志中心

更新时间：2024-12-23 20:34:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：日志字段详情](https://help.aliyun.com/zh/sls/log-fields-20)[下一篇：设置Flowlog日志中心](https://help.aliyun.com/zh/sls/configure-a-flow-log-center-instance)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

产品试用

功能说明

资产说明

费用说明

使用限制

阿里云日志服务和专有网络联合推出Flowlog日志中心，用于VPC的策略统计、弹性网卡流量统计以及网段间流量统计，帮助您快速、有效地分析VPC流日志。

## **产品试用**

SLS Playground中的Flowlog日志中心Demo，内置了实例、演示数据、可视化图表等资源，提供了完整的演示环境，便于您快速了解及体验功能。

您可以单击 [Flowlog日志中心](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/app/flowlog)，进行试用。

**重要**

SLS Playground中的数据为演示数据，请勿用于生产环境。

## 功能说明

Flowlog日志中心包括监控中心和域间分析，详细说明如下：

- 监控中心

监控中心用于分析与监控VPC流日志。

  - 提供概览、策略统计、ENI流量和ECS间流量仪表盘。更多信息，请参见 [专属仪表盘](https://help.aliyun.com/zh/sls/usage-notes-6#table-xjj-jj1-llf "")。

  - 提供自定义查询页面，便于您查询和分析VPC流日志。具体操作，请参见 [查询与分析快速指引](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis#task-tqc-ddm-gfb "")。
- 域间分析

开启域间分析功能后，系统将自动创建数据加工任务，生成具有网段信息的VPC流日志，用于分析不同网段之间的流量情况。

  - 提供域间流量、ECS到区间流量、威胁情报仪表盘。更多信息，请参见 [专属仪表盘](https://help.aliyun.com/zh/sls/usage-notes-6#table-xjj-jj1-llf "")。

  - 提供自定义查询页面，便于您查询和分析具有网段信息的VPC流日志。具体操作，请参见 [查询与分析快速指引](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis#task-tqc-ddm-gfb "")。

## 资产说明

- Project和Logstore

您需要自定义Project和Logstore，用于存储VPC流日志。当您配置域间网段后，系统将自动生成数据加工任务，并创建一个名为_flowlog-enriched-实例ID_的Logstore，用于存储经过数据加工后的VPC流日志。

- 专属仪表盘


表 1\. 专属仪表盘



|     |     |     |
| --- | --- | --- |
| **仪表盘名称** | **关联的Logstore** | **说明** |
| 概览 | 自定义的Logstore | 展示VPC流日志的整体信息。 |
| 策略统计 | 自定义的Logstore | 展示Accept趋势、Reject趋势、Accept次数统计（由五元组构成）、Reject次数统计（由五元组构成）等信息。五元组是由源网段、源端口、协议类型、目标网段和目标端口组成的集合。<br>  - ACCEPT：安全组和网络ACL允许记录的流量。<br>    <br>  - REJECT：安全组和网络ACL拒绝记录的流量。 |
| ENI流量 | 自定义的Logstore | 展示弹性网卡ENI传入和传出的流量信息。 |
| ECS间流量 | 自定义的Logstore | 展示ECS实例之间的流量情况。 |
| 域间流量 | 名为_flowlog-enriched-实例ID_的Logstore | 展示不同网段之间的流量情况。 |
| ECS到区间流量 | 名为_flowlog-enriched-实例ID_的Logstore | 展示ECS实例到目标网段的流量情况。 |
| 威胁情报 | 名为_flowlog-enriched-实例ID_的Logstore | 展示源IP地址与目标IP地址的威胁情报信息。 |


## 费用说明

目前，流日志仅支持将提取到的网络日志投递到日志服务，流日志的费用=网络日志提取费+日志服务的服务费。

- 网络日志提取费

VPC按照提取的日志收取网络日志提取费。更多信息，请参见 [流日志计费说明](https://help.aliyun.com/zh/vpc/user-guide/billing-of-flow-logs#concept-2234514 "")。

- 日志服务的服务费

  - 当涉及的Logstore的计费模式为按使用功能计费时，日志服务采集到VPC流日志后，根据存储空间、读取流量、请求数量、数据加工、数据投递等进行收费。更多信息，请参见 [按使用功能计费模式计费项](https://help.aliyun.com/zh/sls/billable-items#concept-xzl-hjg-vgb "")。

  - 当涉及的Logstore的计费模式为按写入数据量计费时，日志服务采集到VPC流日志后，日志服务将根据原始写入数据量等进行收费。更多信息，请参见 [按写入数据量计费模式计费项](https://help.aliyun.com/zh/sls/billing-items-in-the-pay-per-data-write-mode#main-2351620 "")。

## 使用限制

日志服务Project与VPC实例需处于同一地域。