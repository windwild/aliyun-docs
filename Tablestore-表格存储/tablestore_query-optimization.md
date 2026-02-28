### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/)查询优化

# 查询优化

更新时间：2025-01-16 21:57:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：列出映射表名称列表](https://help.aliyun.com/zh/tablestore/list-table-names-of-sql-query)[下一篇：索引选择策略](https://help.aliyun.com/zh/tablestore/index-selection-policy)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

索引选择策略

计算下推

SQL查询时支持通过索引选择和计算下推两种方法提高数据查询效率。本文介绍两种查询优化的使用。

## **索引选择策略**

表格存储作为海量结构化大数据存储，支持不同的索引结构，便于在不同场景下进行查询分析加速使用。使用SQL查询数据时，通过为数据表创建二级索引或多元索引可以实现数据查询加速。更多信息，请参见 [索引选择策略](https://help.aliyun.com/zh/tablestore/index-selection-policy#53c65cc2ed96j "")。

- 使用数据表映射表查询数据时，索引选择策略支持自动选择和手动选择。

  - **自动选择策略**：由表格存储自动选择数据表、二级索引表或者多元索引进行数据查询。

  - **手动选择策略**：显式指定使用数据表、二级索引或者多元索引进行数据查询。
- 使用二级索引映射表或者多元索引映射表查询数据时，只支持查询指定索引包含的数据列。


## **计算下推**

多元索引提供了条件过滤、聚合、排序等功能。在创建多元索引后，使用SQL查询时，系统能够充分利用多元索引的计算能力，将部分SQL计算任务下推到多元索引执行，避免全表扫描，从而提高计算效率。更多信息，请参见 [计算下推](https://help.aliyun.com/zh/tablestore/computing-pushdown#concept-2098481 "")。