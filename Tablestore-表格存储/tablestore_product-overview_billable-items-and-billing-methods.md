### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[产品简介](https://help.aliyun.com/zh/tablestore/product-overview/)[产品计费](https://help.aliyun.com/zh/tablestore/product-overview/billing/)[计费概述](https://help.aliyun.com/zh/tablestore/product-overview/billing-overview/)CU模式（原按量模式）

# CU模式（原按量模式）

更新时间：2026-01-08 04:32:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：VCU模式（原预留模式）](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-and-billing-methods-of-vcu-model/)[下一篇：多元索引计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-search-indexes-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费价格

基础计费

计费组成

计费项

核心能力计费

计费案例

案例背景

案例分析

常见问题

CU模式（原按量模式）适用于业务峰谷变化较大，不可预测的场景。表格存储按实例计费。CU模式（原按量模式）的计费项包括读吞吐量、写吞吐量、数据存储量、跨地域复制流量和外网下行流量五部分。如果在实际业务中使用了多元索引、二级索引、SQL查询、时序模型、多版本、生命周期管理、通道服务、全局表、数据迁移同步等核心功能，则会产生相应的读写数据、数据存储费用。

## 计费价格

具体计费价格，请参见[表格存储价格详情页](https://www.aliyun.com/price/product#/ots/detail)。

您可以使用 [价格计算器](https://www.aliyun.com/price/product#/ots/calculator) 对产品价格成本进行初步估算。

## 基础计费

### **计费组成**

表格存储提供了容量型实例和高性能实例两种实例规格。不同实例规格的计费组成如下图所示。

![fig_20230313_billingoverview](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0174687671/p581833.png)

### **计费项**

CU模式（原按量模式）下，表格存储实例产生的费用主要由读吞吐量、写吞吐量、数据存储量、跨地域复制流量和外网下行流量五部分构成。

| **计费项** | **付费方式** | **计费标准** |
| --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **计费项** | **付费方式** | **计费标准** |
| [读吞吐量](https://help.aliyun.com/zh/tablestore/product-overview/read-and-write-throughput#concept-e5y-nmj-bfb "") | 预留读吞吐量 | - 按量付费<br>  <br>- 资源包 | 实例所有表的预留读吞吐量之和，按小时计费（账单周期内每小时预留读吞吐量的平均值）。单位为 [CU](https://help.aliyun.com/zh/tablestore/product-overview/read-and-write-throughput#concept-e5y-nmj-bfb "")。<br>**说明**<br>仅高性能 [实例](https://help.aliyun.com/zh/tablestore/product-overview/instance-of-tablestore#concept-hz2-btj-bfb "") 支持预留读吞吐量。 |
| 按量读吞吐量 | - 按量付费<br>  <br>- 资源包 | 每秒实际消耗的读吞吐量。表格存储对账单周期内实例下所有表的按量读吞吐量之和进行计费。单位为 [CU](https://help.aliyun.com/zh/tablestore/product-overview/read-and-write-throughput#concept-e5y-nmj-bfb "")。 |
| [写吞吐量](https://help.aliyun.com/zh/tablestore/product-overview/read-and-write-throughput#concept-e5y-nmj-bfb "") | 预留写吞吐量 | - 按量付费<br>  <br>- 资源包 | 实例所有表的预留写吞吐量之和，按小时计费（账单周期内每小时预留写吞吐量的平均值）。单位为 [CU](https://help.aliyun.com/zh/tablestore/product-overview/read-and-write-throughput#concept-e5y-nmj-bfb "")。<br>**说明**<br>仅高性能 [实例](https://help.aliyun.com/zh/tablestore/product-overview/instance-of-tablestore#concept-hz2-btj-bfb "") 支持预留写吞吐量。 |
| 按量写吞吐量 | - 按量付费<br>  <br>- 资源包 | 每秒实际消耗的写吞吐量。表格存储对账单周期内实例下所有表的按量写吞吐量之和进行计费。单位为 [CU](https://help.aliyun.com/zh/tablestore/product-overview/read-and-write-throughput#concept-e5y-nmj-bfb "")。 |
| [数据存储量](https://help.aliyun.com/zh/tablestore/product-overview/storage-usage#concept-okx-2tj-bfb "")<br>**说明**<br>当数据量较大时，建议您使用预购资源包的方式降低存储成本。 | 高性能存储 | - 按量付费<br>  <br>- 资源包 | 适用于对延迟敏感在线业务，单请求ms级别延迟。<br>根据实际使用量可以动态扩展，按小时计费（账单周期内每小时数据总量的平均值），单位为GB。 |
| 容量型存储 | - 按量付费<br>  <br>- 资源包 | 适用于对读延迟不敏感的，存储空间需求大业务场景。 <br>根据实际使用量可以动态扩展，按小时计费（账单周期内每小时数据总量的平均值），单位为GB。 |
| 跨地域复制流量 | 按量付费 | 使用全局表时，向各副本表异步复制数据时产生跨地域数据传输流量。按实际同步的数据量计费。单位为GB。<br>**重要**<br>各副本的跨地域复制流量费单独计算，费用均计量到到被拉取数据的实例。 |
| 外网下行流量 | 按量付费 | 应用程序访问表格存储所产生的外网下行流量费用，主要构成为应用程序使用HTTP方式访问表格存储返回的响应。<br>计费公式为：外网下行流量费用=外网下行流量（GB）×每GB单价。<br>**说明**<br>- 表格存储仅对外网下行流量收费，对上行流量和通过内网访问的流量均不收费。<br>  <br>- 访问失败时，表格存储会返回操作失败信息，这部分也会产生下行流量。<br>  <br>- 不同地域间的访问也属于外网访问。 |

## **核心能力计费**

使用多元索引、二级索引、SQL查询、时序模型、多版本、生命周期管理、通道服务、全局表、数据迁移同步等核心功能时会产生相应的费用。

**重要**

- 如果通过外网访问表格存储，则会产生外网下行流量费用。

- SQL本身不会有额外的费用，但是使用SQL查询数据过程中涉及到的表扫描、索引查询等操作会产生费用。


各功能的计费原则请参见下表。

| **核心功能** | **计费原则** |
| --- | --- |

|     |     |
| --- | --- |
| **核心功能** | **计费原则** |
| 多元索引 | 不论当前实例规格，多元索引均会产生高性能存储量、预留读吞吐量与按量读吞吐量等。更多信息，请参见 [多元索引计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-search-indexes-1#concept-287174 "")。 |
| SQL查询 | SQL本身当前不会有额外的计算消耗，但会根据使用SQL查询数据的过程中，数据表扫描、索引查询等操作产生读写吞吐量。更多信息，请参见 [SQL查询计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-sql-query#concept-2211626 "")。 |
| 二级索引 | 计费项包括索引表数据存储量和索引表读吞吐量。更多信息，请参见 [二级索引计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-secondary-indexes-1#concept-nnw-b1f-zgb "")。 |
| 时序模型 | 计费项包括数据存储量和按量读写吞吐量。更多信息，请参见 [时序模型计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-the-timeseries-model-1#concept-2213794 "")。 |
| 数据多版本 | 主要产生基于版本号与各个版本数据额外的存储量费用。更多信息，请参见 [数据存储量](https://help.aliyun.com/zh/tablestore/product-overview/storage-usage#concept-okx-2tj-bfb "")。 |
| 生命周期管理 | 配置生命周期管理清理数据，不会有额外的数据清理费用。但开启生命周期管理功能后，会在各个属性列增加时间戳作为的版本号数据，有额外的存储量产生。更多信息，请参见 [数据存储量](https://help.aliyun.com/zh/tablestore/product-overview/storage-usage#concept-okx-2tj-bfb "")。 |
| 通道服务 | 当前通道服务本身没有额外的费用开销。在消费通道服务数据时，根据实际拉取的数据产生读吞吐量。 |
| 全局表 | 使用全局表过程中会产生数据读写费用、数据存储费用以及副本间数据同步的跨地域复制流量费用。更多信息，请参见 [全局表计量计费](https://help.aliyun.com/zh/tablestore/product-overview/global-table-metering-and-billing "")。 |
| 数据同步迁移（通过工具或其他产品） | 在使用迁移工具或其他产品（例如DTS、阿里云物联网平台等）迁移访问表格存储时，会根据具体的读写请求按照读写吞吐量计量计费。 |
| 计算引擎访问（MaxCompute、Spark、Flink等） | 各个计算引擎访问表格存储，会根据具体的读写请求按照读写吞吐量计量计费。 |

## **计费案例**

### **案例背景**

假设某杭州用户开通表格存储服务后，分别创建了高性能实例和容量型实例，且两种实例下创建的表数据每天都有稳定的10000读QPS，每次访问均小于4 KB（即1 CU）。

### **案例分析**

下表将从预留读吞吐量设置、费用组成及说明等方面说明如何计算不同实例下的同一张表一天的费用。

| **实例类型** | **预留读吞吐量设置** | **费用计算公式** | **费用（单位：元）** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **实例类型** | **预留读吞吐量设置** | **费用计算公式** | **费用（单位：元）** | **说明** |
| 高性能实例 | 0 | 按量读单价 \\* 按量读CU | 10000\*86400/10000\*0.01=864 | 当预留读吞吐量为0时，只需根据按量CU消耗的总量计费。<br>一天消耗的按量读CU个数为10000\*86400。 |
| 4000 | 预留读单价 \\* 预留读CU + 按量读单价 \* 按量读CU | 4000\*0.00056\*24+(10000-4000)\*86400/10000\*0.01=572.16 | 当预留读吞吐量大于0且小于表的QPS时，预留吞吐量按照实际设置的值计费，超出预留吞吐量部分按量计费。<br>其中预留读吞吐量费用为`4000*0.00056*24`=53.76元，按量读吞吐量费用为`（10000-4000）*86400/10000*0.01`=518.4元。 |
| 10000 | 预留读单价 \\* 预留读CU | 10000\*0.00056\*24=134.4 | 当预留读吞吐量与表的QPS相同时，没有消耗按量CU，只需根据预留CU的总量进行计费。 |
| 容量型实例 | 不适用 | 按量读单价 \\* 按量读CU | 10000\*86400/10000\*0.004=345.6 | 容量型实例不支持预留读写吞吐量，所有的读写访问均根据按量读写吞吐量进行计费。 |

由此可见，合理使用预留读写吞吐量，能使资源费用最优化。

**说明**

- 以上价格仅供参考，具体价格请以控制台为准。

- 容量型能够提供更低的存储成本和数据访问成本，支持百万TPS的写入能力，但读性能弱于高性能实例。

- 实例类型（高性能与容量型）在实例创建之后不支持修改，请根据您的使用场景创建不同的实例类型。


## 常见问题

#### **我使用的容量型实例，为什么会存在预留读吞吐量费用？**

使用多元索引功能时，表格存储会根据索引数据规模自动设置一个预留读吞吐量。因此容量型实例中如果使用了多元索引，也会产生预留读吞吐量费用。关于多元索引计费的更多信息，请参见 [多元索引计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-search-indexes-1#concept-287174 "")。

多元索引的预留读吞吐量费用包含以下资源消耗：

- 创建索引时，会先从数据表中读取数据，从而消耗一定读吞吐量。

- 创建索引需要消耗写吞吐量，且创建索引时可能还会有分词，对资源的消耗会比较高。这部分费用也会包括在预留读吞吐量中，不会再额外计费。

- 为了保证索引和查询的性能，索引的部分内容会提前加载进内存且内存常驻，并消耗系统的内存资源。这部分费用也会包括在预留读吞吐量中。


#### **VCU模式（原预留模式）与CU模式（原按量模式）有哪些区别？**

VCU模式（原预留模式）和CU模式（原按量模式）的主要区别如下：

- 计算部分

VCU模式（原预留模式）是以包年包月方式购买预留VCU（VCU，4核16 GB）或使用弹性能力根据实际计算消耗折算成VCU进行计费，而CU模式（原按量模式）是根据实际计算消耗折算成CU进行计费。

- 存储部分

VCU模式（原预留模式）支持按照不同存储类型收费，而CU模式（原按量模式）只能与实例类型绑定。

- 索引部分

VCU模式（原预留模式）的存储部分单独收费，计算部分统一在计算资源中消耗；而CU模式（原按量模式）按照高性能存储与预留CU方式计费。


更多信息，请参见 [VCU模式和CU模式的区别](https://help.aliyun.com/zh/tablestore/product-overview/compare-the-on-demand-mode-and-reserved-mode#concept-2065585 "")。

#### **当前使用的数据存储、读写吞吐量较多，如何降低成本？**

表格存储提供了资源包的付费方式，用于降低使用成本。购买资源包即可根据购买资源与时长享受不同的使用折扣。关于资源包的更多信息，请参见 [资源包](https://help.aliyun.com/zh/tablestore/product-overview/resource-plan-overview/#concept-lyb-gtj-bfb "")。

资源包类型包括按量写CU套餐、按量读CU套餐、存储套餐和预留CU套餐四种。不同计费模式支持的资源包类型不同，详细说明请参见下表。

**说明**

未购买资源包的资源默认按量付费。例如您购买了存储套餐资源包和按量写套餐资源包，则存储和按量写吞吐使用资源包抵扣，读吞吐按量付费。

| **类型** | **适用的计费模式** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **类型** | **适用的计费模式** | **描述** |
| 按量写CU套餐 | CU模式（原按量模式） | 有效期内每个月能使用的写CU总数，用于抵扣按量写吞吐量。例如购买了一年的10亿规格按量写CU套餐，表示每个月都有10亿的按量写CU会通过资源包进行抵扣，为期一年。 |
| 按量读CU套餐 | CU模式（原按量模式） | 有效期内每个月能使用的读CU总数，用于抵扣按量读吞吐量和预留读吞吐量。 |
| 存储套餐 | - VCU模式（原预留模式）<br>  <br>- CU模式（原按量模式） | 有效期内每个小时能用来抵扣的存储量。 |
| 预留CU套餐 | CU模式（原按量模式） | 有效期内每个小时能用来抵扣的预留读写CU量（包含多元索引产生的预留读吞吐量）。<br>**说明**<br>多元索引预留读吞吐量支持使用预留CU套餐抵扣。 |

当资源的按量付费成本高于对应时长资源包的成本时，建议购买资源包来降低使用成本。具体计算方式请通过 [表格存储定价详情](https://www.aliyun.com/price/product#/ots/calculator) 和价格计算器进行初步成本估算和对比。

当使用高性能实例或者使用多元索引功能时，您可以通过购买预留CU套餐进行预留读写吞吐量的抵扣。

#### **按量付费实例是否能够控制资源使用上限？**

按量付费实例当前无法控制整体资源的使用上限，需要业务层来自行管控避免异常流量与使用导致的表格存储资源开销。

#### **如何查看实例读写CU的使用量？**

您可以通过以下方式查看表格存储实例读写CU的使用量。

- [通过表格存储控制台查看监控数据](https://help.aliyun.com/zh/tablestore/view-monitoring-data-in-the-tablestore-console#concept-2207400 "")

- [通过云监控控制台与SDK查看监控数据](https://help.aliyun.com/zh/tablestore/view-monitoring-data-by-using-the-cloudmonitor-console-and-cloudmonitor-sdks#concept-2228088 "")

- 通过费用中心导出计量数据。具体操作，请参见 [用量查询](https://help.aliyun.com/zh/tablestore/product-overview/query-resource-usage#task-2235086 "")。


#### **如何查看实例中的表数据大小？**

您可以通过表格存储控制台或者通过费用中心查看实例中的表数据大小。

- 通过表格存储控制台查看

1. 登录[表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择地域。

3. 在 **概览** 页面，单击目标实例名称或在操作列单击 **实例管理**。

4. 在 **实例详情** 页签的 **实例基础信息** 区域，查看表数据大小。
- 通过费用中心导出计量数据。具体操作，请参见 [用量查询](https://help.aliyun.com/zh/tablestore/product-overview/query-resource-usage#task-2235086 "")。