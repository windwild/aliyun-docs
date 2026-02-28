### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[开始使用](https://help.aliyun.com/zh/sls/start-using-sls/)[产品计费](https://help.aliyun.com/zh/sls/billing/)[计费方式](https://help.aliyun.com/zh/sls/billing-methods/)[资源包](https://help.aliyun.com/zh/sls/resource-plan/)资源包介绍

# 资源包介绍

更新时间：2025-08-21 22:34:49

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：按写入数据量计费](https://help.aliyun.com/zh/sls/billing-per-amount-of-data-written)[下一篇：选购资源包](https://help.aliyun.com/zh/sls/purchase-a-resource-plan)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

资源包

新版资源包-预付计划2.0（推荐）

旧版资源包-存储包

旧版资源包-索引流量包

旧版资源包-读写流量包

新旧版资源包对比

常见问题

购买资源包

使用资源包

查看资源包明细

预先购买资源包，在费用结算时，优先从资源包抵扣用量。本文介绍资源包的基本信息。

## 资源包

日志服务提供如下资源包。

**重要**

当您拥有新版资源包和旧版资源包（读写流量包、索引流量包和存储包）时，优先抵扣旧版资源包。

| **资源包** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **资源包** | **说明** |
| 新版资源包-预付计划2.0（推荐） | 支持抵扣日志服务中所有计费项。<br>**说明**<br>在有效期内，每月拥有相同的资源额度。每月月底清零，次月恢复。 |
| 旧版资源包-存储包 | 仅用于抵扣 **存储空间-日志存储** 计费项所产生的费用。 |
| 旧版资源包-索引流量包 | 仅用于抵扣 **索引流量-日志索引** 计费项所产生的费用。 |
| 旧版资源包-读写流量包 | 仅用于抵扣 **读写流量** 计费项所产生的费用。 |

## 新版资源包-预付计划2.0（推荐）

资源包支持抵扣日志服务中所有计费项。规格越大、包年期时长越长，价格优惠力度越大。系统每天会统计您使用的日志服务用量，在资源包额度范围内直接抵扣。在有效期内，每月有相同的资源额度。当月额度用完后，自动转为按量付费方式。

**重要**

- 新版资源包的优先级高于节省计划，如果同时拥有两者，则优先抵扣新版资源包。

- 同时支持按使用功能计费模式和按写入数据量计费模式。

- 日志服务新版资源包的包年计划（1年期及以上版本），根据规格大小给予不同的折扣优惠，具体折扣以购买页面为准。按量付费方式的定价无变化，只有购买新版资源包（1年期及以上版本），才享受预付计划2.0的优惠策略。

- 阿里云在您购买新版资源包时一次性收取费用。例如您要购买1年期、100 CU的新版资源包，则阿里云将在您购买当天一次性收取1年的费用。


新版资源包的规格单位为资源额度CU（Cost Unit）。

- 资源包支持 **按使用功能计费模式** 和 **按写入数据量计费模式**。

- 每个计费项抵扣消耗资源包额度（CU）的比例，与该计费项的按量付费的单价完全一致。例如公共云日志服务的读写流量的按量付费价格为0.18元/GB，则每GB读写流量，抵扣0.18个CU，详细信息如下表所示：


按使用功能计费

按写入数据量计费

|     |     |     |
| --- | --- | --- |
| **计费项** | **公共云版本** | **金融云版本** |
| 读写流量（每GB） | 0.18 CU | 0.342 CU |
| 索引流量-日志索引（每GB） | 0.35 CU | 0.665 CU |
| 索引流量-日志索引-查询型（每GB） | 0.1 CU | 0.19 CU |
| 存储空间-日志热存储（每GB/天） | 0.0115 CU | 0.02185 CU |
| 存储空间-日志低频存储（每GB/天） | 0.005 CU | 0.0095 CU |
| 存储空间-日志归档存储（每GB/天） | 0.0017CU | 0.00323 CU |
| 索引流量-时序索引（每GB） | 0.2 CU | 0.38 CU |
| 存储空间-时序存储（每GB/天） | 0.0035 CU | 0.00665 CU |
| 数据加工（每GB） | 0.15 CU | 0.285 CU |
| 投递数据到OSS基础版（JSON或CSV格式）（每GB） | 0.05 CU | 0.095 CU |
| 投递数据到OSS高级版（Parquet或ORC格式）（每GB） | 0.2 CU | 0.38 CU |
| 投递数据到MaxCompute（每GB） | 0.2 CU | 0.38 CU |
| 投递数据到AnalyticDB MySQL版（每GB） | 0.2 CU | 0.38 CU |
| 投递数据到云原生多模数据库 Lindorm（每GB） | 0.200 元/GB | 0.380 元/GB |
| 电话告警通知（每次） | 0.15 CU | 0.285 CU |
| 短信告警通知（每次） | 0.05 CU | 0.095 CU |
| SQL独享版（每核×小时） | 0.35 CU | 0.665 CU |
| 扫描流量 | 0.05 CU | 0.095 CU |
| 活跃 Shard 租用（每天） | 0.04 CU | 0.076 CU |
| 读写次数（每百万次） | 0.12 CU | 0.228 CU |
| 外网读取流量（每GB） | 0.8 CU | 1.52 CU |

|     |     |     |
| --- | --- | --- |
| **计费项** | **公共云版本** | **金融云版本** |
| 原始写入数据量（每GB） | 0.4 CU | 0.76 CU |
| 存储空间-日志热存储（每GB/天） | 0.0115 CU | 0.02185 CU |
| 存储空间-日志低频存储（每GB/天） | 0.005 CU | 0.0095 CU |
| 存储空间-日志归档存储（每GB/天） | 0.0017 CU | 0.00323 CU |
| 外网读取流量（每GB） | 0.8 CU | 1.52 CU |

## 旧版资源包-存储包

存储包仅用于抵扣 **存储空间-日志存储** 计费项所产生的费用。系统每天会统计您使用的日志存储量，如果没有存储包的容量大小则不会产生费用，超出部分使用按量付费方式。

存储包支持叠加购买，存在多个存储包时，按照购买时间进行抵扣。

## 旧版资源包-索引流量包

索引流量包仅用于抵扣 **索引流量-日志索引** 计费项所产生的费用。系统每天会统计您使用的日志索引流量，如果没有超出索引流量包的容量大小则不会产生费用，超出部分使用按量付费方式。

索引流量包支持叠加购买，存在多个索引流量包时，按照购买时间进行抵扣。

## 旧版资源包-读写流量包

读写流量包仅用于抵扣 **读写流量** 计费项所产生的费用。系统每天会统计您使用的读写流量，如果没有超出读写流量包的容量大小，则不会产生费用，超出部分使用按量付费方式。

读写流量包支持叠加购买，存在多个读写流量包时，按照购买时间进行抵扣。

## 新旧版资源包对比

- 新版资源包

支持抵扣日志服务中所有计费项。包括存储、索引流量、读写流量、请求、加工、投递、告警通知（短信、电话）等。具有易管理、易使用、全覆盖等优势。






按使用功能计费



按写入数据量计费

















![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8800385571/CAEQOxiBgMCJy42D8hgiIDY2MjQ4NWJjNDQzNDRkZWRhYjljZDRhZGM2Y2M4ODNm3926471_20230822152343.335.svg)![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8800385571/CAEQOxiBgIDhuoiD8hgiIDA1NDhmMWRlNWRlNzRkY2E4YTE0N2U1YTZmMDlhMzcy3926471_20230822152343.335.svg)
- 旧版资源包



包括存储包、索引流量包和读写流量包。单计费项资源包模式存在难管理、覆盖不全、购买复杂等问题。





**重要**





日志存储空间包、日志索引流量包和读写流量包仅支持日志数据（Logstore），不支持时序数据（MetricStore）。






![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8800385571/CAEQOxiBgIDi9veA8hgiIDUwNmUyMThlYTJhODQ4MzRiYTc5ODU3ZDhiN2YzZGFm4261167_20240315114358.644.svg)

## 常见问题

### 购买资源包

- [如何选择资源包规格？](https://help.aliyun.com/zh/sls/how-do-i-select-a-quota-for-a-resource-plan#concept-2066150 "")

- [为什么购买资源包后，当月的日志服务消费额暴涨？](https://help.aliyun.com/zh/sls/why-do-fees-significantly-increase-in-the-month-when-i-purchase-a-resource-plan#concept-2286934 "")

- [购买资源包后，多久生效？](https://help.aliyun.com/zh/sls/when-does-a-resource-plan-take-effect-after-i-purchase-it#concept-2286945 "")

- [为什么购买了资源包仍会欠费？](https://help.aliyun.com/zh/sls/why-do-i-have-overdue-payments-even-if-i-purchase-a-resource-plan#concept-2035815 "")

- [资源包额度不够用怎么办？](https://help.aliyun.com/zh/sls/what-do-i-do-if-the-quota-of-a-resource-plan-is-insufficient#concept-2286991 "")

- [资源包购买页没有所需的资源包规格怎么办？](https://help.aliyun.com/zh/sls/what-do-i-do-if-i-cannot-find-a-resource-plan-that-i-require#concept-2286981 "")


### 使用资源包

- [新旧版资源包的抵扣顺序是怎样的？](https://help.aliyun.com/zh/sls/what-is-the-offset-order-of-the-new-and-old-resource-plans#concept-2286923 "")

- [为什么资源包的余量显示为-或者余量保持不变？](https://help.aliyun.com/zh/sls/why-is-the-remaining-quota-of-a-resource-plan-displayed-as-or-remains-unchanged#concept-2286949 "")

- [已经产生的欠费是否可以购买资源包进行抵扣？](https://help.aliyun.com/zh/sls/can-i-purchase-a-resource-plan-to-offset-overdue-payments#concept-2287075 "")

- [超出资源包使用额度后，如何计费？](https://help.aliyun.com/zh/sls/how-am-i-charged-if-the-quota-of-a-resource-plan-is-exceeded#concept-2287081 "")

- [为什么1年期的资源包，1个月就被用完了？](https://help.aliyun.com/zh/sls/why-the-quota-of-a-one-year-resource-plan-is-used-up-in-one-month#concept-2287101 "")


### 查看资源包明细

[如何查看资源包使用明细？](https://help.aliyun.com/zh/sls/how-do-i-view-the-usage-details-of-my-resource-plans#concept-2286948 "")