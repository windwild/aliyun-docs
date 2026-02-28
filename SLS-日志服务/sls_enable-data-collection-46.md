### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[CloudLens](https://help.aliyun.com/zh/sls/cloudlens-46/)[CloudLens for PolarDB](https://help.aliyun.com/zh/sls/cloudlens-for-polardb-usage-notes/)开启数据采集功能

# 开启数据采集功能

更新时间：2026-01-04 03:55:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：授权RAM用户操作CloudLens for PolarDB](https://help.aliyun.com/zh/sls/grant-the-operation-permissions-on-cloudlens-for-polardb-to-a-ram-user)[下一篇：设置告警](https://help.aliyun.com/zh/sls/configure-alert-monitoring-rules)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

首次配置

开启数据采集功能

相关操作

后续步骤

CloudLens for PolarDB支持一键开启数据采集功能，用于采集PolarDB MySQL集群的审计日志、慢查询日志、错误日志和性能指标。本文介绍开启数据采集功能的操作步骤及相关操作。

## 前提条件

已创建PolarDB MySQL集群。具体操作，请参见 [自定义购买](https://help.aliyun.com/zh/polardb/polardb-for-mysql/user-guide/purchase-a-pay-as-you-go-cluster#task-1580301 "") 或 [购买包年包月集群](https://help.aliyun.com/zh/polardb/polardb-for-mysql/user-guide/purchase-a-subscription-cluster#task-1580301 "")。

## 首次配置

**重要**

本操作只需执行一次。

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。
2. 在 **日志应用** 区域的 **云产品Lens** 页签中，单击 **CloudLens for PolarDB**。

3. 根据页面提示，开启CloudLens for PolarDB。



在开启过程中，系统会自动授权CloudLens for PolarDB使用服务关联角色AliyunServiceRolePolicyForSLSAudit采集PolarDB MySQL集群的日志和性能指标。更多信息，请参见 [管理服务关联角色AliyunServiceRoleForSLSAudit](https://help.aliyun.com/zh/sls/manage-the-aliyunserviceroleforslsaudit-service-linked-role#concept-2089820 "")。


## 开启数据采集功能

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。
2. 在 **日志应用** 区域的 **云产品Lens** 页签中，单击 **CloudLens for PolarDB**。

3. 在 **接入管理** 页面的 **PolarDB集群接入** 页签中，单击目标PolarDB MySQL集群对应的 **开启**。



日志服务支持采集PolarDB MySQL集群的审计日志、慢查询日志、错误日志和性能指标。您可以根据业务需求，开启对应数据的采集功能。





**重要**





开启PolarDB MySQL集群的审计日志采集功能后，会自动开启PolarDB MySQL集群的SQL洞察功能。SQL洞察功能按照审计日志存储的容量收取费用。更多信息，请参见 [计费项概览](https://help.aliyun.com/zh/polardb/polardb-for-mysql/enterprise-billing-item-overview#concept-zbj-4pg-tdb "")。

4. 在采集确认对话框中，单击 **确认**。



性能指标是中心化存储，当前阿里云账号下的所有PolarDB MySQL集群的性能指标都会被采集到一个Metricstore中。您需要在首次开启性能指标的采集功能时，需选择一个目标地域。更多信息，请参见 [资产说明](https://help.aliyun.com/zh/sls/cloudlens-for-polardb-usage-notes/#section-svl-y37-5bb "")。


## 相关操作

开启CloudLens for PolarDB后，您还可以在 **接入管理** 页签中，执行如下操作。

| **操作** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **操作** | **说明** |
| 管理PolarDB MySQL集群 | 开启CloudLens for PolarDB后，CloudLens for PolarDB将展示当前阿里云账号下所有的PolarDB MySQL集群。<br>单击目标PolarDB MySQL集群，系统将跳转至云数据库PolarDB控制台。您可以查看PolarDB MySQL集群详情以及执行登录数据库、迁入数据等操作。更多信息，请参见 [5.6/5.7/8.0版功能对比](https://help.aliyun.com/zh/polardb/polardb-for-mysql/version-comparison#task-2550662 "")。 |
| 关闭采集功能 | 单击目标PolarDB MySQL集群对应的 **关闭**，关闭采集功能。<br>**重要**<br>关闭审计日志时，不会自动关闭SQL洞察功能。如果您不再采集目标集群的审计日志，则可以在PolarDB控制台上关闭SQL洞察功能。具体操作，请参见 [关闭SQL洞察和审计](https://help.aliyun.com/zh/polardb/polardb-for-mysql/user-guide/sql-explorer-and-audit#section-myx-gws-2gb "")。 |
| 查询和分析 | - 单击目标PolarDB MySQL集群对应的 **日志查询**，选择对应的日志，系统将跳转至对应的LogStore中。您可以在LogStore中查看对应的原始日志，并执行查询分析操作。具体操作，请参见 [查询与分析快速指引](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis#task-tqc-ddm-gfb "")。<br>  <br>- 单击目标PolarDB MySQL集群对应的 **日志查询**，选择 **性能指标**，系统将跳转至对应的Metricstore中。您可以在Metricstore中查看对应的指标数据，并执行查询分析操作。具体操作，请参见 [查询和分析时序数据](https://help.aliyun.com/zh/sls/query-and-analyze-metric-data#task-2539642 "")。 |
| 修改存储时长 | 您可以在 **存储目标库** 页签中，找到目标存储库，单击![修改保存时间](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5662084361/p341815.png)图标，修改目标存储库中数据的保存时间。 |

## 后续步骤

[查看性能监控大盘](https://help.aliyun.com/zh/sls/view-performance-monitoring-dashboards#task-2168127 "")