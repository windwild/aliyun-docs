### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[成本管家](https://help.aliyun.com/zh/sls/cost-manager/)SLS账单分析案例

# SLS账单分析案例

更新时间：2025-04-17 06:22:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：账单自定义告警案例](https://help.aliyun.com/zh/sls/billing-custom-alarm-case)[下一篇：OSS账单分析案例](https://help.aliyun.com/zh/sls/oss-bill-analysis-case)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

SLS 账单数据概念​

SLS 自助分析报表使用

SLS 账单用量分析

示例1：查看昨日金额

示例2：查询 SLS 云产品各计费项用量趋势

示例3：查询 SLS 各 Project 各 Logstore 用量明细

配置 SLS 存储用量告警​

本文向您介绍SLS自主分析报表的使用、常见SLS账单分析案例以及配置SLS存储用量告警的操作步骤。

## **SLS 账单数据概念** [**​**](https://sls.aliyun.com/doc/billandsecurity/billSls.html\#sls-%E8%B4%A6%E5%8D%95%E6%95%B0%E6%8D%AE%E6%A6%82%E5%BF%B5)

分析 SLS 账单数据前，需了解以下基础概念。计费数据包含云产品的资源用量。例如，日志服务资源用量包括各实例在不同计费项的使用量。您可以通过以下查询分析语句查看日志服务账单信息：

```sql
* |
select
  BillingDate,
  BillingItem,
  BillingType,
  CostUnit,
  Currency,
  DeductedByCashCoupons,
  DeductedByCoupons,
  DeductedByPrepaidCard,
  DeductedByResourcePackage,
  InstanceConfig,
  InstanceID,
  InstanceSpec,
  InvoiceDiscount,
  Item,
  ListPrice,
  ListPriceUnit,
  NickName,
  OutstandingAmount,
  OwnerID,
  PaymentAmount,
  PretaxAmount,
  PretaxGrossAmount,
  ProductCode,
  ProductDetail,
  ProductName,
  ProductType,
  Region,
  ResourceGroup,
  ServicePeriod,
  SubscriptionType,
  Tag,
  Usage,
  UsageUnit,
  Zone
from
  instance_bill
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p940897.png)

其中实例和计费项说明如下：

| **名称** | **字段** | **描述** | **示例** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **字段** | **描述** | **示例** |
| 实例 | InstanceID | 云服务的最小粒度资源，日志服务最小粒度是Logstore。InstanceID格式为：`OwnerId;Project;Logstore;Region`。 | 12345;test-project;test-logstore;cn-guangzhou |
| 计费项 | BillingItem | 是日志服务的 [计费项](https://help.aliyun.com/zh/sls/billable-items#section-js9-o1w-m7r "")，例如存储空间、索引流量等。 | 索引流量 |

## **SLS 自助分析报表使用**

打开成本管家，单击 **SLS账单自助分析** 报表，查看费用和用量趋势。页面上方提供了全局过滤方式，选择对应的 **Project**、 **Logstore**、 **Region**、 **OwnerId** 条件，分析单一实例用量。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p939645.png)

用量分析中提供 **Top Project 用量明细** 和 **Top Logstore 用量明细**，展示了 Project 和Logstore粒度费用及用量，方便您时刻关注用量最多的资源。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p939654.png)

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p939655.png)

## **SLS 账单用量分析**

### **示例1：查看昨日金额**

您可以通过以下步骤查看昨日金额：

1. 打开 **SLS 账单自助分析** 报表，找到 **昨日金额** 图表。

2. 鼠标悬浮在图表右上角![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p940019.png)，单击 **预览查询语句**，查看查询语句。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p939665.png)

查询分析语句：















```sql
(*) |
select
     t,
     cost as "昨日费用",
     (cost - lag(cost, 1, 0) over()) / lag(cost, 1, 0) over() * 100 as "同比前一天费用"
FROM
     (
       select
         sum(PretaxAmount) as cost,
         date_format(__time__, '%Y-%m-%d') as t
       FROM
         instance_bill
       where
         (
           productcode = 'sls'
           or productcode = 'slsingest'
         )
         and split_part(InstanceID, ';', 3) like '%%'
         and split_part(InstanceID, ';', 2) like '%%'
         and split_part(InstanceID, ';', 4) like '%%'
         and OwnerId like '%%'
       group by
         t
       order by
         t asc
     )
limit
     1000
```

3. 如果需要自定义修改，单击 **查询分析**，跳转到成本管家对应的 project 中。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p943416.png)


### **示例2：查询 SLS 云产品各计费项用量趋势**

您可以使用以下查询分析语句统计SLS云产品各计费项用量趋势。

```sql
 * |
select
  date_trunc('day', __time__) as t,
  BillingItem,
  round(sum(Usage), 2) as "用量"
from instance_bill
where ProductCode='sls'
group by BillingItem, t
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p943314.png)

### **示例3：查询 SLS 各 Project 各 Logstore 用量明细**

您可以使用以下查询分析语句查询SLS各Project各Logstore用量明细。其中，请将`${project_name}`替换为实际的Project名称。

```sql
 * | select
  split_part(instanceId, ';', 2) as project,
  split_part(instanceId, ';', 3) as logstore,
  split_part(instanceId, ';', 4) as region,
  BillingItem as "计费项",
  round(sum(Usage), 2) as "用量"
FROM  instance_bill
where
  ProductCode = 'sls'
  and split_part(instanceId, ';', 2) like '${project_name}'
group by
  BillingItem,
  project,
  logstore,
  region
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p943305.png)

## **配置 SLS 存储用量告警** [**​**](https://sls.aliyun.com/doc/billandsecurity/billSls.html\#%E9%85%8D%E7%BD%AE-sls-%E5%AD%98%E5%82%A8%E7%94%A8%E9%87%8F%E5%91%8A%E8%AD%A6)

为了控制整体成本，您可以配置告警关注整体的用量。以下以配置SLS存储用量告警为示例。

1. 在左侧导航栏单击 **告警**，在 **告警中心** 页面单击 **新建告警**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p940070.png)

2. 在新建告警页面，参考下图配置 **检查频率**、 **查询统计** 和 **触发条件**。其余参数，请参考 [配置说明](https://help.aliyun.com/zh/sls/create-an-alert-monitoring-rule-for-logs#0010bad40eyi2 "") 进行设置。


配置如下查询存储空间用量的查询分析语句。由于账单数据同步时间为 T+1，在语句查询区间您可以选择时间为 **昨天**。由于 SLS 账单数据为按日出账，因此您需要在告警检查频率处配置为固定间隔 1 天。 设置触发条件为 **有数据匹配**， 并将匹配条件设置为存储空间用量大于您的告警阈值即可，图中以告警阈值 400 为例。

















```sql
* |
select
      round(sum(Usage), 2) as "存储空间用量"
from instance_bill
where ProductCode='sls'
and BillingItem like '%存储空间%'
```




![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p940086.png)

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635884471/p940079.png)

3. 配置完告警后，您可以在告警大盘 [查看告警触发记录](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#section-ixp-knm-fg9 "")。