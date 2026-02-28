### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[CloudLens](https://help.aliyun.com/zh/sls/cloudlens-46/)[CloudLens for SLS](https://help.aliyun.com/zh/sls/cloudlens-for-sls/)[最佳实践](https://help.aliyun.com/zh/sls/best-practices-9/)使用CloudLens for SLS监控Project资源配额

# 使用CloudLens for SLS监控Project资源配额

更新时间：2023-09-10 23:37:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用CloudLens for SLS分析资源用量](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-analyze-resource-usage)[下一篇：任务监控大盘异常处理](https://help.aliyun.com/zh/sls/handle-errors-for-a-job-monitoring-dashboard)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景介绍

前提条件

查看额度监控仪表盘

资源配额预警概览

Project重点资源配额实时水位详情

Project资源配额超限详情

资源监控

额度监控

高级监控

资源配额调整申请

本文主要介绍如何使用CloudLens for SLS中全局错误日志、监控指标做Project资源配额的水位监控、超限监控及提交资源配额提升申请。

## **背景介绍**

Alibaba Cloud Lens基于日志服务SLS构建云产品可观测能力。支持一键开启实例日志（重要日志、详细日志、作业运行日志）和全局日志（审计日志、计费日志、错误日志、监控指标）的采集功能。

| **日志分类** | **子分类** | **监控场景说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **日志分类** | **子分类** | **监控场景说明** |
| 实例日志 | 详细日志 | 访问流量监控<br>访问异常监控 |
| 重要日志 | 消费组监控<br>Logtail采集监控 |
| 作业运行日志 | 数据加工（新版）监控<br>定时SQL任务监控 |
| 全局日志 | 审计日志 | 资源操作监控 |
| 错误日志 | 额度超限监控<br>访问异常监控<br>操作异常监控 |
| 监控指标 | 访问流量监控<br>访问异常监控<br>资源配额水位监控 |
| 计费日志 | 资源用量跟踪 |

各类型日志说明，请参见 [日志索引表](https://help.aliyun.com/zh/sls/log-types-of-cloudlens-applications "")。

## **前提条件**

- 已创建RAM用户，并对RAM用户授权。具体操作，请参见 [创建RAM用户](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "") 和 [授予RAM用户操作CloudLens for SLS的权限](https://help.aliyun.com/zh/sls/authorize-ram-users-to-operate-cloudlens-for-sls "")。

- 已开启全局日志：错误日志、指标监控采集功能。具体操作，请参见 [开启日志采集功能](https://help.aliyun.com/zh/sls/enable-the-log-collection-feature-1 "")。


**重要**

- 为了构建实时资源配额水位监控，全局日志需开启：错误日志、指标监控；并且这两种全局日志需存储于同一Project内。

- 为了避免监控日志存放在业务Project导致监控占用Project的配额，可选择系统推荐的固定地域目标Project，如杭州地域：`log-service-{用户ID}-cn-hangzhou`。


## **查看额度监控仪表盘**

通过CloudLens for SLS额度监控大盘，您可以查看资源配额预警情况、Project重点资源配额实时水位详情及Project资源配额超限详情。

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。
2. 在**日志应用** \> **云产品Lens**区域，单击 **CloudLens for SLS**。

3. 选择左侧菜单栏**报表中心** \> **额度监控**，可查看配额信息。


### 资源配额预警概览

报表提供资源配额预警概览（水位超过80%）以及额度超限分布。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6552078861/p690994.png)

### Project重点资源配额实时水位详情

报表包含Project部分基础资源配额以及数据读写资源配额的实时水位详情。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5552078861/p690999.png)![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5552078861/p691000.png)![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5552078861/p691001.png)

### Project资源配额超限详情

报表提供Project资源配额超限详情。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5552078861/p691002.png)

## **资源监控**

CloudLens for SLS支持提供基础资源、数据读写等额度监控和Logstore监控、机器组监控、Project写入监控等高级监控。

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。
2. 在 **日志应用** 区域，单击 **CloudLens for SLS**。

3. 在 **CloudLens for SLS** 配置界面，单击左侧菜单栏中的 **异常检测**，可配置资源告警监控。


### 额度监控

额度监控项分类说明如下：

| **分类** | **监控项** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **分类** | **监控项** | **说明** |
| 实时水位监控 | [基础资源配额水位监控](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#GPoPz "") | - 监控Project内Logstore数量、机器组数量、Logtail采集配置水位是否超阈值预期百分比。<br>  <br>- 依赖时序库：internal-monitor-metric |
| [数据读写配额水位监控](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#zaPPb "") | - 监控Project写入流量、Project写入次数超配额次数。<br>  <br>- 依赖时序库：internal-monitor-metric |
| 额度超限监控 | [资源配额超限次数监控](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#P3sfZ "") | - 监控基础配额、数据读写超配额次数。<br>  <br>- 依赖日志库：internal-error\_log |

#### **基础资源配额水位监控**

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。






| **参数项** | **赋值** |
| --- | --- |



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | 基础资源配额水位监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：指标库<br>     <br>   - 授权方式：默认<br>     <br>   - 指标库：internal-monitor-metric<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * | select Project, region, logstore_ratio, machine_group_ratio, logtail_config_ratio from <br>     (SELECT A.id as Project , A.region as region, <br>     round(COALESCE(SUM(B.count_logstore), 0)/cast(json_extract(A.quota, '$.logstore') as double) * 100, 3)  as logstore_ratio,  cast(json_extract(A.quota, '$.logstore') as double) as quota_logstore, <br>     round(COALESCE(SUM(C.count_machine_group), 0)/cast(json_extract(A.quota, '$.machine_group') as double) * 100, 3)  as machine_group_ratio, cast(json_extract(A.quota, '$.machine_group') as double) as quota_machine_group, <br>     round(COALESCE(SUM(D.count_logtail_config), 0)/cast(json_extract(A.quota, '$.config') as double) * 100, 3)  as logtail_config_ratio, cast(json_extract(A.quota, '$.config') as double) as quota_logtail_config<br>     FROM  "resource.sls.cmdb.project" as A<br>     LEFT JOIN (<br>       SELECT project, COUNT(*) AS count_logstore<br>       FROM "resource.sls.cmdb.logstore" as B<br>       GROUP BY project<br>     ) AS B ON A.id = B.project <br>     LEFT JOIN (<br>       SELECT project, COUNT(*) AS count_machine_group<br>       FROM "resource.sls.cmdb.machine_group" as C<br>       GROUP BY project<br>     ) AS C ON A.id = C.project<br>     LEFT JOIN (<br>       SELECT project, COUNT(*) AS count_logtail_config<br>       FROM "resource.sls.cmdb.logtail_config" as D<br>       GROUP BY project<br>     ) AS D ON A.id = D.project <br>     group by  A.id, A.quota, A.region) <br>     where quota_logstore is not null and quota_machine_group is not null and quota_logtail_config is not null  and (logstore_ratio > 80 or machine_group_ratio > 80 or logtail_config_ratio > 80) limit 10000<br>     ``` |
| **分组评估** | 标签自动 |
| **触发条件** | **说明**<br>     - 当有Project的Logstore数、机器组数、Logtail采集配置其中一个水位超过额度的90%时告警级别为严重。<br>       <br>     - 当有Project的Logstore数、机器组数、Logtail采集配置其中一个水位超过额度的80%时告警级别为中。<br>       <br>   - 当有数据匹配`logstore_ratio > 90 || machine_group_ratio > 90 || logtail_config_ratio > 90`时，严重度：严重。<br>     <br>   - 当有数据匹配`logstore_ratio > 80 || machine_group_ratio > 80 || logtail_config_ratio > 80`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |



![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


#### **数据读写配额水位监控**

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。






| **参数项** | **赋值** |
| --- | --- |



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | 数据读写配额水位监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：指标库<br>     <br>   - 授权方式：默认<br>     <br>   - 指标库：internal-monitor-metric<br>     <br>   - 查询区间：5分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     (*)| select Project, region, inflow_ratio, write_cnt_ratio from (SELECT cmdb.id as Project, cmdb.region as region, round(COALESCE(M.name1,0)/round(cast(json_extract(cmdb.quota, '$.inflow_per_min') as double)/1000000000, 3) * 100, 3) as inflow_ratio, round(COALESCE(M.name2,0)/cast(json_extract(cmdb.quota, '$.write_cnt_per_min') as double) * 100, 3) as write_cnt_ratio<br>      from "resource.sls.cmdb.project" as cmdb  <br>     LEFT JOIN (<br>          select project,  round(MAX(name1)/1000000000, 3) as name1, MAX(name2) as name2 from (SELECT __time_nano__ as time, element_at( split_to_map(__labels__, '|', '#$#') , 'project') as project,   sum(CASE WHEN __name__ = 'logstore_origin_inflow_bytes' THEN __value__ ELSE NULL END) AS name1,<br>       sum(CASE WHEN __name__ = 'logstore_write_count' THEN __value__ ELSE NULL END) AS name2<br>       FROM "internal-monitor-metric.prom" where __name__ in ('logstore_origin_inflow_bytes','logstore_write_count' ) and regexp_like(element_at( split_to_map(__labels__, '|', '#$#') , 'project') , '.*')  group by project,time )group by project) AS M ON cmdb.id = M.project) where inflow_ratio > 80 or write_cnt_ratio > 80  limit 10000<br>     ``` |
| **分组评估** | 标签自动 |
| **触发条件** | **说明**<br>     - 当有Project的Project写入流量、写入次数其中一个水位超过额度的90%时告警级别为严重。<br>       <br>     - 当有Project的Project写入流量、写入次数其中一个水位超过额度的80%时告警级别为中。<br>       <br>   - 当有数据匹配`where inflow_ratio > 90 || write_cnt_ratio > 90`时，严重度：严重。<br>     <br>   - 当有数据匹配`where inflow_ratio > 80 || write_cnt_ratio > 80`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |



![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


#### **资源配额超限次数监控**

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。






| **参数项** | **赋值** |
| --- | --- |



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | 资源配额超限次数监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：日志库<br>     <br>   - 授权方式：默认<br>     <br>   - 日志库：internal-error\_log<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     ((* and (ErrorCode: ExceedQuota or ErrorCode: QuotaExceed or ErrorCode: ProjectQuotaExceed or ErrorCode:WriteQuotaExceed or ErrorCode: ShardWriteQuotaExceed or ErrorCode: ShardReadQuotaExceed)))| SELECT Project,<br>     CASE <br>     WHEN ErrorMsg like '%Project write quota exceed: inflow%' then 'Project写入流量超限'<br>     WHEN ErrorMsg like '%Project write quota exceed: qps%' then 'Project写入次数超限'<br>     WHEN ErrorMsg like '%dashboard quota exceed%' then '报表额度超限'<br>     WHEN ErrorMsg like '%config count%' then 'Logtail采集配置超限'<br>     WHEN ErrorMsg like '%machine group count%' then '机器组超限'<br>     WHEN ErrorMsg like '%Alert count %' then '告警超限'<br>     WHEN ErrorMsg like '%logstore count %' then 'LogStore数超限'<br>     WHEN ErrorMsg like '%shard count%' then 'Shard数超限'<br>     WHEN ErrorMsg like '%shard write bytes%' then 'Shard写入超限'<br>     WHEN ErrorMsg like '%shard write quota%' then 'Shard写入超限'<br>     WHEN ErrorMsg like '%user can only run%' then 'SQL分析操作并发数超限'<br>         ELSE ErrorMsg<br>       END AS ErrorMsg, <br>     COUNT(1) AS count GROUP BY Project, ErrorMsg Limit 1000<br>     ``` |
| **分组评估** | 不分组 |
| **触发条件** | **说明**<br>     - 当有任意额度超限10次错误告警级别为严重。<br>       <br>     - 当有任意额度发生超限1次错误时告警级别为中。<br>       <br>   - 当有数据匹配`count > 10`时，严重度：严重。<br>     <br>   - 当有数据匹配`count > 1`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |



![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


### **高级监控**

高级监控项分类说明如下：

| **分类** | **场景** | **监控项** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **分类** | **场景** | **监控项** | **说明** |
| 基础资源配额 | [Logstore监控](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#d233adc01cbyo "") | 实时水位监控 | - 监控Project下Logstore数水位是否超阈值预期百分比。<br>  <br>- 依赖时序库：internal-monitor-metric |
| 额度超限监控 | - 监控Project下LogStore数超配额次数<br>  <br>- 依赖日志库：internal-error\_log |
| [机器组监控](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#ed3f65401ckuh "") | 实时水位监控 | - 监控Project下机器组数水位是否超阈值预期百分比。<br>  <br>- 依赖时序库：internal-monitor-metric |
| 额度超限监控 | - 监控Project下机器组数超配额次数。<br>  <br>- 依赖日志库：internal-error\_log |
| [Logtail采集配置](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#705968411clb9 "") | 实时水位监控 | - 监控Project下Logtail采集配置数水位是否超阈值预期百分比。<br>  <br>- 依赖时序库：internal-monitor-metric |
| 额度超限监控 | - 监控Project下Logtail采集配置数超配额次数。<br>  <br>- 依赖日志库：internal-error\_log |
| 数据读写资源配额 | [Project写入流量监控](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#749404b11cghw "") | 实时水位监控 | - 监控Project写入流量水位是否超阈值预期百分比。<br>  <br>- 依赖时序库：internal-monitor-metric |
| 额度超限监控 | - 监控Project写入流量超配额次数。<br>  <br>- 依赖日志库：internal-error\_log |
| [Project写入次数监控](https://help.aliyun.com/zh/sls/use-cloudlens-for-sls-to-monitor-project-resource-quotas#5e6cd3511ct7l "") | 实时水位监控 | - 监控Project写入次数水位是否超阈值预期百分比。<br>  <br>- 依赖时序库：internal-monitor-metric |
| 额度超限监控 | - 监控Project写入次数超配额次数。<br>  <br>- 依赖日志库：internal-error\_log |

#### Logstore监控

实时水位监控

额度超限监控

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Logstore数水位监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：指标库<br>     <br>   - 授权方式：默认<br>     <br>   - 指标库：internal-monitor-metric<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * |  select Project, region, round(count_logstore/quota_logstore * 100, 3)  as logstore_ratio from <br>     (SELECT A.id as Project , A.region as region, COALESCE(SUM(B.count_logstore), 0)  AS count_logstore , cast(json_extract(A.quota, '$.logstore') as double)  as quota_logstore<br>     FROM  "resource.sls.cmdb.project" as A<br>     LEFT JOIN (<br>       SELECT project, COUNT(*) AS count_logstore<br>       FROM "resource.sls.cmdb.logstore" as B<br>       GROUP BY project<br>     ) AS B ON A.id = B.project <br>     group by A.id, A.quota, A.region) where  quota_logstore is not null   order by logstore_ratio desc limit 1000<br>     ``` |
| **分组评估** | 标签自动 |
| **触发条件** | **说明**<br>     - 当有Project的LogStore数超过额度的90%时告警级别为严重。<br>       <br>     - 当有Project的LogStore数超过额度的80%时告警级别为中。<br>       <br>   - 当有数据匹配`logstore_ratio > 90`时，严重度：严重。<br>     <br>   - 当有数据匹配`logstore_ratio > 80`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Logstore数额度超限 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：日志库<br>     <br>   - 授权方式：默认<br>     <br>   - 日志库：internal-error\_log<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * and (ErrorCode: ExceedQuota or ErrorCode: QuotaExceed or ErrorCode: ProjectQuotaExceed or ErrorCode:WriteQuotaExceed)| SELECT Project, <br>     COUNT(1) AS count where ErrorMsg like '%logstore count %' GROUP BY Project ORDER BY count DESC LIMIT 1000<br>     ``` |
| **分组评估** | 不分组 |
| **触发条件** | **说明**<br>     - 当有Project的Logstore发生超限10次错误告警级别为严重。<br>       <br>     - 当有Project的Logstore发生超限1次错误时告警级别为中。<br>       <br>   - 当有数据匹配`count > 10`时，严重度：严重。<br>     <br>   - 当有数据匹配`count > 1`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


#### 机器组监控

实时水位监控

额度超限监控

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | 机器组水位监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：指标库<br>     <br>   - 授权方式：默认<br>     <br>   - 指标库：internal-monitor-metric<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * |  select Project, region, round(count_machine_group/quota_machine_group * 100, 3)  as machine_group_ratio from <br>     (SELECT A.id as Project , A.region as region, COALESCE(SUM(B.count_machine_group), 0)  AS count_machine_group , cast(json_extract(A.quota, '$.machine_group') as double)  as quota_machine_group<br>     FROM  "resource.sls.cmdb.project" as A<br>     LEFT JOIN (<br>       SELECT project, COUNT(*) AS count_machine_group<br>       FROM "resource.sls.cmdb.machine_group" as B<br>       GROUP BY project<br>     ) AS B ON A.id = B.project <br>     group by A.id, A.quota, A.region) where  quota_machine_group is not null   order by machine_group_ratio desc limit 1000<br>     ``` |
| **分组评估** | 标签自动 |
| **触发条件** | **说明**<br>     - 当有Project的机器组超过额度的90%时告警级别为严重。<br>       <br>     - 当有Project的机器组超过额度的80%时告警级别为中。<br>       <br>   - 当有数据匹配`machine_group_ratio > 90`时，严重度：严重。<br>     <br>   - 当有数据匹配`machine_group_ratio > 80`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Logstore数额度超限 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：日志库<br>     <br>   - 授权方式：默认<br>     <br>   - 日志库：internal-error\_log<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * and (ErrorCode: ExceedQuota or ErrorCode: QuotaExceed or ErrorCode: ProjectQuotaExceed or ErrorCode:WriteQuotaExceed)| SELECT Project, <br>     COUNT(1) AS count where ErrorMsg like '%machine group count%' GROUP BY Project ORDER BY count DESC LIMIT 1000<br>     ``` |
| **分组评估** | 不分组 |
| **触发条件** | **说明**<br>     - 当有Project的机器组发生超限10次错误告警级别为严重。<br>       <br>     - 当有Project的机器组发生超限1次错误时告警级别为中。<br>       <br>   - 当有数据匹配`count > 10`时，严重度：严重。<br>     <br>   - 当有数据匹配`count > 1`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


#### Logtail采集配置

实时水位监控

额度超限监控

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Logtail采集配置水位监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：指标库<br>     <br>   - 授权方式：默认<br>     <br>   - 指标库：internal-monitor-metric<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * |  select Project, region, round(count_logtail_config/quota_logtail_config * 100, 3)  as logtail_config_ratio from <br>     (SELECT A.id as Project , A.region as region, COALESCE(SUM(B.count_logtail_config), 0)  AS count_logtail_config , cast(json_extract(A.quota, '$.config') as double)  as quota_logtail_config<br>     FROM  "resource.sls.cmdb.project" as A<br>     LEFT JOIN (<br>       SELECT project, COUNT(*) AS count_logtail_config<br>       FROM "resource.sls.cmdb.logtail_config" as B<br>       GROUP BY project<br>     ) AS B ON A.id = B.project <br>     group by A.id, A.quota, A.region) where  quota_logtail_config is not null   order by logtail_config_ratio desc limit 1000<br>     ``` |
| **分组评估** | 标签自动 |
| **触发条件** | **说明**<br>     - 当有Project的Logtail采集配置数超过额度的90%时告警级别为严重。<br>       <br>     - 当有Project的Logtail采集配置数超过额度的80%时告警级别为中。<br>       <br>   - 当有数据匹配`logtail_config_ratio > 90`时，严重度：严重。<br>     <br>   - 当有数据匹配`logtail_config_ratio > 80`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Logtail采集配置额度超限 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：日志库<br>     <br>   - 授权方式：默认<br>     <br>   - 日志库：internal-error\_log<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * and (ErrorCode: ExceedQuota or ErrorCode: QuotaExceed or ErrorCode: ProjectQuotaExceed or ErrorCode:WriteQuotaExceed)| SELECT Project, <br>     COUNT(1) AS count where ErrorMsg like '%config count%' GROUP BY Project ORDER BY count DESC LIMIT 1000<br>     ``` |
| **分组评估** | 不分组 |
| **触发条件** | **说明**<br>     - 当有Project的Logtail采集配置发生超限10次错误告警级别为严重。<br>       <br>     - 当有Project的Logtail采集配置发生超限1次错误时告警级别为中。<br>       <br>   - 当有数据匹配`count > 10`时，严重度：严重。<br>     <br>   - 当有数据匹配`count > 1`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


#### Project写入流量监控

实时水位监控

额度超限监控

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Project写入流量水位监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：指标库<br>     <br>   - 授权方式：默认<br>     <br>   - 指标库：internal-monitor-metric<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     (*)| SELECT Project, region , round(count_inflow/cast(quota_inflow as double) * 100, 3) as inflow_ratio<br>     FROM<br>     (SELECT cmdb.id as Project, cmdb.region as region, COALESCE(M.name1,0) as count_inflow, round(cast(json_extract(cmdb.quota, '$.inflow_per_min') as double)/1000000000, 3) as quota_inflow  from "resource.sls.cmdb.project" as cmdb  <br>     LEFT JOIN (<br>         select project,  round(MAX(name1)/1000000000, 3) as name1 from (SELECT __time_nano__ as time, element_at( split_to_map(__labels__, '|', '#$#') , 'project') as project,   sum(CASE WHEN __name__ = 'logstore_origin_inflow_bytes' THEN __value__ ELSE NULL END) AS name1<br>         FROM "internal-monitor-metric.prom" where __name__ ='logstore_origin_inflow_bytes' and regexp_like(element_at( split_to_map(__labels__, '|', '#$#') , 'project') , '.*') group by project,time )group by project) AS M ON cmdb.id = M.project )order by inflow_ratio desc  limit 1000<br>     ``` |
| **分组评估** | 标签自动 |
| **触发条件** | **说明**<br>     - 当有Project写入流量超过额度的90%时告警级别为严重。<br>       <br>     - 当有Project写入流量超过额度的80%时告警级别为中。<br>       <br>   - 当有数据匹配`inflow_ratio > 90`时，严重度：严重。<br>     <br>   - 当有数据匹配`inflow_ratio > 80`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Project写入流量额度超限 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：日志库<br>     <br>   - 授权方式：默认<br>     <br>   - 日志库：internal-error\_log<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * and (ErrorCode: ExceedQuota or ErrorCode: QuotaExceed or ErrorCode: ProjectQuotaExceed or ErrorCode:WriteQuotaExceed)| SELECT Project, <br>     COUNT(1) AS count where ErrorMsg like '%Project write quota exceed: inflow%' GROUP BY Project ORDER BY count DESC LIMIT 1000<br>     ``` |
| **分组评估** | 不分组 |
| **触发条件** | **说明**<br>     - 当有Project写入流量发生超限10次错误告警级别为严重。<br>       <br>     - 当有Project写入流量发生超限1次错误时告警级别为中。<br>       <br>   - 当有数据匹配`count > 10`时，严重度：严重。<br>     <br>   - 当有数据匹配`count > 1`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


#### Project写入次数监控

实时水位监控

额度超限监控

1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Project写入次数水位监控 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：指标库<br>     <br>   - 授权方式：默认<br>     <br>   - 指标库：internal-monitor-metric<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     (*)| SELECT Project, region,  round(count_write_cnt/cast(quota_write_cnt as double) * 100, 3) as write_cnt_ratio<br>     FROM<br>     (SELECT cmdb.id as Project, cmdb.region as region, COALESCE(M.name1,0) as count_write_cnt,<br>     cast(json_extract(cmdb.quota, '$.write_cnt_per_min') as bigint) as quota_write_cnt from "resource.sls.cmdb.project" as cmdb  <br>     LEFT JOIN (<br>         select project,  MAX(name1) as name1 from (SELECT __time_nano__ as time, element_at( split_to_map(__labels__, '|', '#$#') , 'project') as project, <br>       sum(CASE WHEN __name__ = 'logstore_write_count' THEN __value__ ELSE NULL END) AS name1<br>       FROM "internal-monitor-metric.prom" where __name__  = 'logstore_write_count' and regexp_like(element_at( split_to_map(__labels__, '|', '#$#') , 'project') , '.*')  group by project,time )group by project) AS M ON cmdb.id = M.project ) order by write_cnt_ratio desc  limit 1000<br>     ``` |
| **分组评估** | 标签自动 |
| **触发条件** | **说明**<br>     - 当有Project写入次数超过额度的90%时告警级别为严重。<br>       <br>     - 当有Project写入次数超过额度的80%时告警级别为中。<br>       <br>   - 当有数据匹配`inflow_ratio > 90`时，严重度：严重。<br>     <br>   - 当有数据匹配`inflow_ratio > 80`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


1. 单击 **新建告警**，配置告警规则。

2. 选择创建告警需要挂载的Project为存储全局错误日志和监控指标所在Project。

3. 根据业务场景配置告警触发条件、以及告警策略。



根据下表完成配置，其余参数保持默认即可，具体信息，可参见 [创建日志告警监控规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-nhx-uf4-hz6 "")。



|     |     |
| --- | --- |
| **参数项** | **赋值** |
| **规则名称** | Project写入次数额度超限 |
| **检查频率** | 固定间隔，15分钟 |
| **查询统计** | - 类型：日志库<br>     <br>   - 授权方式：默认<br>     <br>   - 日志库：internal-error\_log<br>     <br>   - 查询区间：15分钟（相对）<br>     <br>   - 查询语句：<br>     <br>     <br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     查询SQL默认返回100条数据，若在SQL结尾添加limit 1000，代表可返回1000条查询结果。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```sql<br>     * and (ErrorCode: ExceedQuota or ErrorCode: QuotaExceed or ErrorCode: ProjectQuotaExceed or ErrorCode:WriteQuotaExceed)| SELECT Project, <br>     COUNT(1) AS count where ErrorMsg like '%Project write quota exceed: qps%' GROUP BY Project ORDER BY count DESC LIMIT 1000<br>     ``` |
| **分组评估** | 不分组 |
| **触发条件** | **说明**<br>     - 当有Project写入次数发生超限10次错误告警级别为严重。<br>       <br>     - 当有Project写入次数发生超限1次错误时告警级别为中。<br>       <br>   - 当有数据匹配`count > 10`时，严重度：严重。<br>     <br>   - 当有数据匹配`count > 1`时，严重度：中。 |
| **输出目标** | SLS通知 |
| **告警策略** | 普通模式 |
| **行动策略** | 按需选择或单击 **新增** 创建行动策略，具体操作，请参见 [创建行动策略](https://help.aliyun.com/zh/sls/create-an-action-policy/ "")。 |

![image.png](<Base64-Image-Removed>)
4. 参数配置完成后，单击 **确定**。


## **资源配额调整申请**

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。
2. 在Project列表区域，单击目标Project。
3. 单击![image.png](<Base64-Image-Removed>)图标。

4. 单击 **资源配额** 对应的 **管理**。

5. 在 **资源配额** 面板中，调整目标资源的配额，然后单击 **保存**。![image.png](<Base64-Image-Removed>)