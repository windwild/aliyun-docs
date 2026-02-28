### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[开始使用](https://help.aliyun.com/zh/sls/start-using-sls/)[产品计费](https://help.aliyun.com/zh/sls/billing/)停止计费

# 停止计费

更新时间：2025-12-23 21:30:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：费用优化](https://help.aliyun.com/zh/sls/cost-optimization)[下一篇：如何查看日志服务的存储容量和消费记录](https://help.aliyun.com/zh/sls/how-to-view-the-storage-capacity-and-consumption-records-of-log-service)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

停止计费说明

删除Project或LogStore

云产品日志

日志审计服务日志

Cloud Lens服务日志

其他日志

相关文档

日志服务开通后无法关闭，如果不再需要使用日志服务，您可删除所有Project，日志服务将自动停止计费。

## 停止计费说明

- 创建LogStore时，日志服务默认预留两个Shard。因此只要LogStore存在，无论是否使用都会产生活跃Shard租用费用。日志服务根据您的活跃Shard租用量收取费用。关于Shard租用费用详细说明，请参见 [为什么会产生活跃Shard租用费用](https://help.aliyun.com/zh/sls/why-am-i-charged-for-active-shards "")。如果您不再需要使用LogStore存储日志，请及时删除，避免产生额外费用。具体操作，请参见 [停止计费/删除LogStore](https://help.aliyun.com/zh/sls/manage-a-logstore#sectiondiv-0x2-666-fo5 "")。

- 目前日志服务仅支持 [修改数据保存时间](https://help.aliyun.com/zh/sls/how-do-i-delete-logs "") 来删除日志，无法手动删除指定内容的日志，当日志保存时间达到您所设置的保存时间后，日志将被删除。如需降低存储费用，您可设置较短的存储周期。如果不再需要已有日志，您可直接 [删除Project或LogStore](https://help.aliyun.com/zh/sls/stop-billing#8b220faa93r2o "")。

- 删除Project的当天仍会产生存储等费用，次日不再产生任何费用。即您在删除Project的第三天不会再收到日志服务的账单。


## 删除Project或LogStore

**警告**

通过任意方式删除Project或LogStore后，所有日志数据及配置信息都会被释放，不可恢复，请慎重确认，避免数据丢失。

### **云产品日志**

在弹性计算、存储服务、安全、数据库等多种阿里云云产品开通日志分析服务，会在日志服务控制台自动创建对应的Project和LogStore。更多信息，请参见 [云产品日志概述](https://help.aliyun.com/zh/sls/alibaba-cloud-service-logs "")。

如果不需要云产品日志，您可按照以下步骤关闭。

1. 在对应云产品控制台关闭日志分析服务。

2. 在日志服务控制台删除Project或LogStore。

   - 如需保留Project仅删除LogStore，请参见 [停止计费/删除LogStore](https://help.aliyun.com/zh/sls/manage-a-logstore#section-ezq-vjx-ndb "")。

   - 如需删除整个Project，请参见 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#entry-m7e-hhf-r4z "")。

### **日志审计服务日志**

- 如果您不再需要采集云产品日志，但想要暂时保留已采集的日志（日志将在超出存储天数后被删除），请参见 [停止采集日志](https://help.aliyun.com/zh/sls/enable-log-collection-1#p-si8-s2a-b7n "")。

- 如果您需要清理并删除日志审计服务相关的所有日志服务资源（如Project、LogStore、仪表盘、告警等），请参见 [删除审计资源](https://help.aliyun.com/zh/sls/enable-log-collection-1#p-yen-feo-nfz "")。


### **Cloud Lens服务日志**

#### 注意事项

**警告**

CloudLens功能要求云账号下必须存在至少一个Project。

在用户开通和使用CloudLens功能时，日志服务会检测账号下是否存在Project，具体逻辑如下。

##### **检测逻辑**

1. 用户第一次开通CloudLens功能，日志服务会自动检测您当前的阿里云账号下是否存在任意Project，如果没有Project，则会在华南2（河源）地域创建一个名称为`aliyun-product-data-阿里云账号ID-cn-heyuan`的Project。

2. 用户开通CloudLens功能后进入CloudLens，日志服务只会自动检测您当前的阿里云账号下是否存在任意Project，不会在华南2（河源）地域创建Project，用户可以手动创建任意Project，创建Project的步骤请参见 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#entry-m7e-hhf-r4z "")。


##### **删除Project**

- 如果您要删除`aliyun-product-data-阿里云账号ID-cn-heyuan`这个Project，可以打开[云命令行](https://shell.aliyun.com/)，执行以下命令进行删除，请根据实际情况替换 **阿里云账号ID**。















```shell
aliyunlog log delete_project --project_name=aliyun-product-data-阿里云账号ID-cn-heyuan --region-endpoint=cn-heyuan.log.aliyuncs.com
```

- 删除其他Project和Logstore的步骤，请参见 [管理LogStore](https://help.aliyun.com/zh/sls/manage-a-logstore#section-ezq-vjx-ndb "") 和 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#entry-m7e-hhf-r4z "")。


### **其他日志**

- 如需保留Project仅删除LogStore，请参见 [停止计费/删除LogStore](https://help.aliyun.com/zh/sls/manage-a-logstore#section-ezq-vjx-ndb "")。

- 如需删除整个Project，请参见 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#entry-m7e-hhf-r4z "")。


## 相关文档

- 查看Project、LogStore的存储容量，请参见 [如何查看日志服务的存储容量和消费记录](https://help.aliyun.com/zh/sls/how-to-view-the-storage-capacity-and-consumption-records-of-log-service "")。

- 节省计划仅支持抵扣按写入数据量计费模式原始写入数据量计费项费用，不支持抵扣按使用功能计费模式下的计费项抵扣。更多信息，请参见 [节省计划概述](https://help.aliyun.com/zh/sls/overview-of-savings-plan "")。

- 新版资源包可用于抵扣日志服务所有的计费项，在有效期内，每月有相同的资源额度。当月额度用完后，自动转为按量付费方式。更多信息，请参见 [资源包介绍](https://help.aliyun.com/zh/sls/overview-11 "")。

- 日志服务支持使用API方式删除Project或LogStore。具体操作，请参见 [删除指定Project](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-deleteproject "") 和 [删除LogStore](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-deletelogstore "")。