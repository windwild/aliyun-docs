### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[多元索引](https://help.aliyun.com/zh/tablestore/search-index-introduction-of-tablestore/)[索引管理](https://help.aliyun.com/zh/tablestore/search-index-management/)动态修改schema

# 动态修改schema

更新时间：2025-07-03 23:55:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：生命周期管理](https://help.aliyun.com/zh/tablestore/ttl-of-search-indexes)[下一篇：数据类型](https://help.aliyun.com/zh/tablestore/data-type-mappings-of-search-index/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能概述

使用流程

操作步骤

安全性

计费说明

相关文档

如果由于业务变更、性能优化等情况需要在多元索引中新增、更新或者删除索引列以及修改多元索引的路由键和预排序方式，您可以通过动态修改多元索引的schema实现。动态修改schema操作包括为源索引创建灰度索引并修改多元索引schema、等待表数据全部同步到灰度索引、设置权重进行A/B测试、交换源索引和灰度索引的schema和删除灰度索引五个步骤。

## 功能概述

表格存储数据表是schema free的，而多元索引是强schema的。创建多元索引时，您需要指定添加到多元索引中的列，这样使用多元索引查询数据时才能查询到这些列。但是出于业务变更、性能优化等目的，修改多元索引schema成为一个非常常见的需求。例如以下场景：

- 新增索引列：随着业务发展，需要查询更多的列，则可以添加更多的索引列。

- 更新索引列：可以修改列类型、虚拟列、是否数组、分词类型、日期格式等。

- 删除索引列：随着业务发展，有些列不再需要查询，可以考虑删掉。

- 修改路由键：查询时合理指定路由键，减少查询时的读放大并提升性能。

- 修改预排序：查询时如果数据排序顺序与预排序相同，则可以加速数据查询。


## **使用流程**

**重要**

动态修改schema过程中产生的 \_reindex后缀的索引是流程所需的临时索引，在流程执行过程中指向的索引以及流量权重会发生变化，流程结束后临时索引会被删除，行为多变且可能和业务预期不一致，在任何时候请勿直接使用\_reindex后缀的临时索引查询数据。如果当前的动态修改schema功能无法满足您的需求，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)联系我们。

动态修改schema的具体流程如下图所示。整个过程对业务层透明，您无需变更业务代码，即可实现轻量级动态修改schema。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7431061571/CAEQORiBgID1.arh5hgiIDZmYjZlZTcwNjViZDRkNjA4OTE0YjU4N2RkMWZhMDRk4151440_20240105131642.203.svg)

修改多元索引schema的主要步骤说明请参见下表。

| **步骤** | **操作** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **步骤** | **操作** | **说明** |
| 1 | 创建灰度索引 | 为源索引创建一个灰度索引，并根据需要新增、修改和删除多元索引的schema。 |
| 2 | 查看索引同步进度 | 灰度索引会自动同步数据表的数据，等待数据表的存量和增量数据同步到灰度索引，直到同步进度与源索引的进度相同。 |
| 3 | 设置权重进行A/B测试 | A/B测试功能支持将查询流量按照一定比例分摊到源索引和灰度索引来验证修改schema的效果。<br>通过A/B测试逐步引流查询流量到灰度索引，直到100%查询流量均切到灰度索引。 |
| 4 | 交换索引Schema | 查询流量全部切换到灰度索引后，交换源索引和灰度索引的schema。<br>交换索引后，源索引名会关联到新schema，而灰度索引名会关联到老schema，并且100%查询流量会查询源索引名关联的新schema。 |
| 5 | 删除灰度索引 | 交换索引并验证索引无误后，建议静置一段时间（例如一天）再删除灰度索引。 |

## 操作步骤

1. 进入 **索引管理** 页签。

1. 登录[表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择地域和资源组。

3. 在 **概览** 页面，单击实例名称或在 **操作** 列单击 **实例管理**。

4. 在 **实例详情** 页签的 **数据表列表** 区域，单击数据表名称或在 **操作** 列单击 **索引管理**。
2. 基于源索引创建灰度索引。

1. 在 **索引管理** 页签，单击多元索引 **操作** 列的 **修改schema**。

2. 在 **重建索引** 对话框，根据需要添加、修改或者删除索引字段。



      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4826825371/p893711.png)

3. 如果需要修改多元索引的路由键或者预排序方式，请打开 **高级选项** 开关，然后根据下表说明进行配置。




      | **参数** | **说明** |
      | --- | --- |



      |     |     |
      | --- | --- |
      | **参数** | **说明** |
      | 路由键 | 自定义路由字段，可以选择部分主键列作为路由字段。<br>在进行索引数据写入时，会根据路由字段的值计算索引数据的分布位置，路由字段的值相同的记录会被索引到相同的数据分区中。更多信息，请参见 [多元索引路由字段的使用](https://help.aliyun.com/zh/tablestore/how-do-i-use-routing-fields "")。 |
      | 预排序 | 多元索引默认按照设置的索引预排序方式进行排序。使用多元索引查询数据时，预排序决定了数据的默认返回顺序。更多信息，请参见 [索引预排序](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#section-lly-qlx-dgb "")。<br>      - 如果要按照主键排序，直接选择此参数为 **默认排序** 即可。<br>        <br>      - 如果要按照字段值或者主键组合排序，请选择此参数为 **自定义排序**，并进行配置。具体操作如下：<br>        <br>        <br>        1. 选择排序类型为 **主键预排序** 或者 **字段预排序**，并单击 **添加**。<br>           <br>        2. 根据实际选择字段名或排序方式。<br>           <br>           排序方式支持选择升序和降序。<br>           <br>           <br>           <br>           **重要**<br>           <br>           <br>           <br>           <br>           <br>           只有选择排序类型为 **字段预排序** 时，才需要选择字段名。<br>           <br>使用自定义排序时支持同时配置主键预排序和字段预排序，请根据需要配置。 |

4. 单击 **确认重建**。

5. 在 **索引对比** 对话框，查看源索引和灰度索引的路由键、预排序和schema对比信息，确认无误后，单击 **确定**。
3. 查看索引同步信息。

1. 单击源索引前的![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3339344071/p754783.png)图标或者源索引名称。

      系统会显示源索引的灰度索引。

2. 单击灰度索引 **操作** 列的 **灰度/上线**。



      **重要**





      灰度索引会经历“存量同步”和“增量同步”两个阶段。



      - 数据同步完成前，将鼠标光标移动至 **操作** 列的 **灰度/上线** 按钮上，系统会提示 **切换有风险**，禁止用户切换。

      - 当灰度索引同步进度追上源索引的同步进度后，将鼠标光标移动至 **操作** 列的 **灰度/上线** 上，系统会提示 **可安全切换**，此时请继续执行后续操作。


3. 在 **灰度/上线** 对话框，查看索引同步信息。

      ![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5750301371/p754782.png)
4. 索引同步完成后，通过设置权重进行A/B测试。



A/B测试功能支持将查询流量按照一定比例分摊到源索引和灰度索引来验证修改schema的效果。仅当查询流量全部都切到灰度索引时，才能继续执行后续步骤。



1. 在 **灰度/上线** 对话框的 **操作** 区域，拖动滑块调整源索引和灰度索引的权重后，单击 **设置权重**。



      ![fig_setindex](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7336228261/p301971.png)

2. 在 **设置权重** 对话框，查看权重数据和schema对比信息。

3. 确认无误后，单击 **设置权重**。

4. 在系统提示框中单击 **确定**。
5. 查询流量全部切换到灰度索引后，交换源索引和灰度索引的schema。



交换索引后，源索引名会关联到新schema，而灰度索引名会关联到老schema，并且100%查询流量会查询源索引名关联的新schema。



![image.png](<Base64-Image-Removed>)



1. 在 **灰度/上线** 对话框的 **操作** 区域，单击 **交换索引**。

2. 在 **交换索引** 对话框，查看源索引和灰度索引的路由键、预排序和schema对比信息，确认无误后，单击 **确认交换**。
6. 交换索引并验证索引无误后，建议静置一段时间（例如一天）再删除源索引。

![image.png](<Base64-Image-Removed>)

1. 在 **灰度/上线** 对话框，单击 **删除灰度索引**。

2. 在 **确认灰度完成，删除旧索引?** 对话框，确认要删除的灰度索引信息正确后，在文本框中输入`我已确认新索引数据已经同步完成并且灰度一定时间`内容。

3. 单击 **确定**。

## 安全性

为了保证操作的安全性，表格存储提供了“回滚机制”和“切换提醒”，最大限度地降低修改索引过程中可能的风险。

- 回滚机制



动态修改Schema的关键步骤均支持回滚。



  - 创建灰度索引后，如果发现灰度索引的Schema不符合预期，您可以删除后重新创建。

  - 在A/B测试阶段，通过设置查询权重，将查询流量逐步引流到灰度索引。在此过程中，如果发现问题，可以随时重新设置查询权重，将查询流量重新引流到源索引。

  - 交换源索引和灰度索引的Schema后，如果发现问题，您可以随时 **撤销交换**，切回源索引的Schema。 **交换索引** 和 **撤销交换** 互为逆向操作。


- 切换提醒

如果在灰度索引的同步进度落后于源索引时将流量切到灰度索引，则可能会出现查询数据回退。此时表格存储会通过源索引和灰度索引的同步状态和最后同步时间，判断“是否可以安全切换”。



当出现如下情况时，表格存储会判断为 **可安全切换**。



  - 当源索引处于全量阶段，灰度索引为全量或者增量阶段，即灰度索引已追上源索引。

  - 源索引和灰度索引均处于增量阶段，且“源索引最后同步时间 \- 60 s <= 灰度索引最后同步时间”，即灰度索引落后源索引的时间不超过1分钟。


## **计费说明**

灰度索引构建和数据写入不会产生费用。源索引和灰度索引均会产生与存储规模有关的存储和预留读CU费用。更多信息，请参见[多元索引计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-search-indexes-1 "")。

## **相关文档**

- 如果要在不改变表结构情况下实现新字段新数据类型的查询功能，您可以通过修改多元索引Schema或者新建多元索引时结合虚拟列功能来实现。更多信息，请参见 [虚拟列](https://help.aliyun.com/zh/tablestore/virtual-columns "")。

- 您可以根据查询场景使用 [全匹配查询](https://help.aliyun.com/zh/tablestore/match-all-query-function "")、 [匹配查询](https://help.aliyun.com/zh/tablestore/match-query-function "")、 [短语匹配查询](https://help.aliyun.com/zh/tablestore/match-phrase-query-function "")、 [精确查询](https://help.aliyun.com/zh/tablestore/term-query-function "")、 [多词精确查询](https://help.aliyun.com/zh/tablestore/terms-query-function "")、 [通配符查询](https://help.aliyun.com/zh/tablestore/wildcard-query-function "")、 [前缀查询](https://help.aliyun.com/zh/tablestore/prefix-query-function "")、 [后缀查询](https://help.aliyun.com/zh/tablestore/suffix-query "")、 [基于分词的通配符查询](https://help.aliyun.com/zh/tablestore/fuzzy-query "")、 [范围查询](https://help.aliyun.com/zh/tablestore/range-query-function "")、 [组合查询](https://help.aliyun.com/zh/tablestore/boolean-query-function "")、 [嵌套类型查询](https://help.aliyun.com/zh/tablestore/nested-query-function "")、 [地理距离查询](https://help.aliyun.com/zh/tablestore/geo-distance-query "")、 [地理长方形范围查询](https://help.aliyun.com/zh/tablestore/geo-bounding-box-query "")、 [地理多边形范围查询](https://help.aliyun.com/zh/tablestore/geo-polygon-query "")、 [列存在性查询](https://help.aliyun.com/zh/tablestore/exists-query-function "")、 [折叠（去重）](https://help.aliyun.com/zh/tablestore/collapse "")、 [虚拟列](https://help.aliyun.com/zh/tablestore/virtual-columns "") 等功能查询所需数据。

- 如果需要使用SQL快速查询多元索引中不同类型的数据，您可以使用SQL查询功能通过多元索引实现。更多信息，请参见 [SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/ "")、 [创建多元索引的映射关系](https://help.aliyun.com/zh/tablestore/create-mapping-tables-for-search-indexes-of-sql-query "")、 [查询数据](https://help.aliyun.com/zh/tablestore/query-data "")、 [全文检索](https://help.aliyun.com/zh/tablestore/full-text-search-by-using-sql-query "")、 [多元索引数组类型](https://help.aliyun.com/zh/tablestore/multiple-index-array-type "")、 [多元索引嵌套类型](https://help.aliyun.com/zh/tablestore/multiple-index-nested-type "") 和 [多元索引虚拟列](https://help.aliyun.com/zh/tablestore/virtual-columns-of-search-index-in-sql-query "")。

- 如果要实现求最小值、求最大值、求和、求平均值、统计行数、去重统计行数、百分位统计、按字段值分组、按范围分组、按地理位置分组、按过滤条件分组、直方图统计、日期直方图统计、获取统计聚合分组内的行、嵌套查询等数据分析需求，您可以使用多元索引统计聚合功能实现。更多信息，请参见 [统计聚合](https://help.aliyun.com/zh/tablestore/aggregation-of-tablestore "")。