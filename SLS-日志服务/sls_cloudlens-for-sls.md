### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[CloudLens](https://help.aliyun.com/zh/sls/cloudlens-46/)CloudLens for SLS

# CloudLens for SLS

更新时间：2026-01-04 22:23:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：日志索引表](https://help.aliyun.com/zh/sls/log-types-of-cloudlens-applications)[下一篇：授权RAM用户操作CloudLens for SLS](https://help.aliyun.com/zh/sls/authorize-ram-users-to-operate-cloudlens-for-sls)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

产品试用

功能说明

适用场景

资产详情

费用说明

使用限制

注意事项

检测逻辑

删除Project

日志服务推出CloudLens for SLS应用，帮助您监控和管理日志服务Project、LogStore等资产，以提升您对日志服务资产的管理效率、快速了解其消耗情况。

## **产品试用**

SLS Playground中的CloudLens for SLS Demo，内置了演示数据、可视化图表等资源，提供完整的演示环境，便于您快速了解及体验功能。

您可以单击 [CloudLens for SLS](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/app/lens/sls?resource=/common-data-access)，进行试用。

**重要**

SLS Playground中的数据为演示数据，请勿用于生产环境。

## 功能说明

CloudLens for SLS支持如下功能。

- 支持集中管理当前阿里云账号下符合条件的Project和LogStore。条件说明，请参见 [使用限制](https://help.aliyun.com/zh/sls/cloudlens-for-sls/#title-v83-6w5-053 "")。![CloudLens for SLS](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3176568071/p430422.png)

- 支持一键开启实例日志（重要日志、详细日志、任务运行日志）和全局日志（审计日志、计费日志、错误日志、监控指标）的采集功能，集中管理日志的采集状态。



**说明**





实例日志（重要日志、详细日志、任务运行日志）和全局日志（审计日志、错误日志、监控指标）仅支持查看开通日志采集后数据。






  - 重要日志：包括LogStore粒度的消费组消费延时日志、Logtail相关的错误、心跳和统计日志，存储在指定Project下名为internal-diagnostic\_log的LogStore中。

  - 详细日志：包括Project内所有资产的创建、修改、更新、删除操作日志和数据读写日志，存储在指定Project下名为internal-operation\_log的LogStore中。

  - 任务运行日志：记录数据导入（新版）、定时SQL、投递（新版）等任务的出错与延迟信息，存储在指定Project下名为internal-diagnostic\_log的LogStore中。

  - 审计日志：记录当前阿里云账号内所有Project内资源的创建、修改、更新、删除等操作日志，存储在指定Project下名为internal-audit\_log的LogStore中。

  - 计费日志：通过成本管家记录日志服务计费资源数据，存储在表格存储（OTS）中，每日自动全量更新。数据详情，请参见 [账单数据说明](https://help.aliyun.com/zh/sls/use-the-new-version-of-cost-manager#Z8YH7 "")。



    **说明**





    - 初次开通时，数据导入大概需要1~2小时，具体导入时间受账单数据量影响。

    - 仅公共云用户支持开通计费日志。

    - 开通后，不支持关闭。


  - 错误日志：记录当前阿里云账号内所有Project内资源的创建、修改、更新、删除以及数据读写的错误日志，存储在指定Project下名为internal-error\_log的LogStore中。

  - 监控指标：记录Project粒度、LogStore粒度的流量、请求、延迟等指标数据，存储在指定Project下名为internal-monitor-metric的MetricStore中。


更多信息，请参见 [服务日志](https://help.aliyun.com/zh/sls/overview-24/#concept-e2t-hzp-m2b "")。

![CloudLens for SLS](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7958159561/p430421.png)

- CloudLens for SLS预设了基线告警、同环比告警等相关的告警监控规则，用于监控Project、Logtail、消费组等资源的使用，并支持短信、钉钉、邮件、语音、自定义Webhook等通知方式。更多信息，请参见 [设置告警](https://help.aliyun.com/zh/sls/configure-alerts-1#task-2239925 "")。![告警](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3176568071/p481008.png)

- 提供丰富的可视化报表，包括全局概览、访问监控、采集监控、操作监控、作业监控、额度监控、SQL质量监控和计费资源监控这七大类报表。更多信息，请参见 [查看数据报表](https://help.aliyun.com/zh/sls/view-data-reports-2#task-2206358 "")。![CloudLens for SLS](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5230909071/p430610.png)

- 支持查看当前阿里云下符合条件的Project和LogStore的Quota信息。条件说明，请参见 [使用限制](https://help.aliyun.com/zh/sls/cloudlens-for-sls/#title-v83-6w5-053 "")。

![CloudLens for SLS](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2176568071/p474650.png)


## 适用场景

- 开发运维

开发人员可通过CloudLens for SLS监控和管理日志服务Project、LogStore等资产，提升对日志服务资产的管理效率；通过对CloudLens for SLS所采集的Project实例详细日志、重要日志和任务监控日志进行查询与分析，提高了问题定位的效率。

- IT运维

IT运维人员可通过CloudLens for SLS的告警功能及时感知和响应Project服务状态、流量、Quota以及Logtail多维度指标的异常。

- 安全审计

CloudLens for SLS的审计日志可以记录用户对Project内资源的创建、更新和删除操作，便于安全审计人员对特定时间内的操作进行安全分析与审计。


## 资产详情

- Project、LogStore、MetricStore

  - 开启重要日志、任务运行日志采集时，您可以自定义选择一个Project。开启后，日志服务将在该Project下生成一个名为internal-diagnostic\_log的LogStore。

  - 开启详细日志采集时，您可以自定义选择一个Project。开启后，日志服务将在该Project下生成一个名为internal-operation\_log的LogStore。

  - 开启审计日志采集时，您可以自定义选择一个Project。开启后，日志服务将在该Project下生成一个名为internal-audit\_log的LogStore。

  - 开启错误日志采集时，您可以自定义选择一个Project。开启后，日志服务将在该Project下生成一个名为internal-error\_log的LogStore。

  - 开启监控指标采集时，您可以自定义选择一个Project。开启后，日志服务将在该Project下生成一个名为internal-monitor-metric的MetricStore。
- 仪表盘




| **仪表盘** | **说明** |
| --- | --- |



|     |     |     |
| --- | --- | --- |
| **仪表盘** | **说明** |
| 全局概览 | 全局概览 | 展示日志服务Project相关信息，包括读写请求次数、读写请求成功率、4xx请求次数、5xx请求次数、写入流量（原始大小）、写入流量（压缩后）、写入流量压缩比、读取流量等图表。 |
| 访问监控 | 访问流量监控 | 展示日志服务的访问情况，包括今日请求总数、客户端个数、今日用户数、SourceIP读取网络流量Top 10、SourceIP写入流量Top 10、请求数、写入流量、Shard写入流量变化趋势、Shard消费流量趋势、每分钟读写网络流量变化、访问来源分布等图表。 |
| 访问异常监控 | 展示日志服务的异常访问情况，包括今日请求总数、失败请求占比、限流错误、请求异常状态分布、超过写入限制LogStore、请求异常数、请求处理耗时趋势等图表。 |
| 消费组监控 | 展示消费组相关信息，包括消费组个数、消费LogStore个数、消费Shard个数、消费组延迟数、消费组数据占比、消费组列表、消费组延时Top 10、消费落后时长等图表。 |
| 采集监控 | Logtail整体状态 | 展示Logtail相关信息，包括活跃Logtail数、原始数据流量、运行状态分布、内存占用分布、Logtail整体状态、CPU趋势、内存趋势、数据发送流量等图表。 |
| Logtail文件采集监控 | 展示待采集文件的相关信息，包括采集文件数、采集机器数、采集文件分布、采集日志量、平均采集延迟、解析失败率、发送次数趋势等图表。 |
| Logtail异常监控 | 展示Logtail的异常情况，包括活跃Logtail数、Logtail重启列表、重启客户端数、全量错误信息等图表。 |
| 操作监控 | 操作监控 | 展示日志服务操作记录，包括日志库操作总数、日志库操作失败占比、操作客户端个数等图表。 |
| 作业监控 | 数据处理监控 | 展示数据导入任务（新版）、投递任务（新版）或定时SQL任务运行情况，包括读成功条数、读失败条数、写成功条数、写失败条数、读公网流量、写公网流量、处理速率、进度落后、运行异常、运行状态等图表。 |
| 额度监控 | 额度监控 | 展示资产额度超限情况，包括资源配额80%水位预警概览、额度超限分布、LogStore水位占比分布、机器组水位占比分布、Logtail采集配置水位占比分布、Project写入流量水位占比分布、Project基础资源配额详情、Project数据读写资源配额详情、Project资源超限详情等图表。 |
| SQL质量监控 | SQL质量监控 | 展示SQL质量情况，包括SQL 健康分、SQL服务指标、SQL运行明细指标、SQL Pattern等图表。 |
| 计费资源监控 | 计费资源监控 | 展示日志服务计费资源信息，包括存储空间-日志热存储、索引流量-日志索引、读写流量、计费项用量趋势、Top Project用量明细、Top LogStore用量明细等。 |


## 费用说明

CloudLens for SLS应用服务免费，提供的各类日志费用具体说明如下：

- 重要日志、任务运行日志和审计日志的接入、存储与查询分析免费。当您进行数据加工、数据投递等操作时，按量计费。

- 详细日志的计费方式与普通LogStore一致。

- 计费日志不会产生额外费用，其涉及的Project、表格存储实例均为免费实例。


更多信息，请参见 [按使用功能计费模式计费项](https://help.aliyun.com/zh/sls/billable-items#concept-xzl-hjg-vgb "")。

## 使用限制

目前，CloudLens for SLS只监控和管理如下区域的资产。

| **云类型** | **地域** |
| --- | --- |

|     |     |
| --- | --- |
| **云类型** | **地域** |
| 公共云 | 华东1（杭州）、华北1（青岛）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华北6（乌兰察布）、华东2（上海）、西南1（成都）、华南1（深圳）、华南2（河源）、华南3（广州）、中国（香港）、印度尼西亚（雅加达）、马来西亚（吉隆坡）、菲律宾（马尼拉）、新加坡、韩国（首尔）、泰国（曼谷）、日本（东京）、英国（伦敦）、德国（法兰克福）、阿联酋（迪拜）、美国（硅谷）、美国（弗吉尼亚） |
| 金融云 | 华东1（杭州金融云）、华东2（上海金融云）、华北2（北京金融云）、华南1（深圳金融云） |

## 注意事项

**警告**

CloudLens功能要求云账号下必须存在至少一个Project。

在用户开通和使用CloudLens功能时，日志服务会检测账号下是否存在Project，具体逻辑如下。

### **检测逻辑**

1. 用户第一次开通CloudLens功能，日志服务会自动检测您当前的阿里云账号下是否存在任意Project，如果没有Project，则会在华南2（河源）地域创建一个名称为`aliyun-product-data-阿里云账号ID-cn-heyuan`的Project。

2. 用户开通CloudLens功能后进入CloudLens，日志服务只会自动检测您当前的阿里云账号下是否存在任意Project，不会在华南2（河源）地域创建Project，用户可以手动创建任意Project，创建Project的步骤请参见 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#entry-m7e-hhf-r4z "")。


### **删除Project**

- 如果您要删除`aliyun-product-data-阿里云账号ID-cn-heyuan`这个Project，可以打开[云命令行](https://shell.aliyun.com/)，执行以下命令进行删除，请根据实际情况替换 **阿里云账号ID**。















```shell
aliyunlog log delete_project --project_name=aliyun-product-data-阿里云账号ID-cn-heyuan --region-endpoint=cn-heyuan.log.aliyuncs.com
```

- 删除其他Project和LogStore的步骤，请参见 [管理LogStore](https://help.aliyun.com/zh/sls/manage-a-logstore#section-ezq-vjx-ndb "") 和 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#entry-m7e-hhf-r4z "")。