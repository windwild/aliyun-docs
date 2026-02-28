### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[多元索引](https://help.aliyun.com/zh/tablestore/search-index-introduction-of-tablestore/)[基础查询](https://help.aliyun.com/zh/tablestore/basic-features/)查询后过滤

# 查询后过滤

更新时间：2025-11-27 02:48:51

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：折叠（去重）](https://help.aliyun.com/zh/tablestore/collapse)[下一篇：组合查询](https://help.aliyun.com/zh/tablestore/boolean-query-function)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

与其他过滤方式的对比

与 Elasticsearch post\_filter 的区别

与 Tablestore BoolQuery 中 Filter 的区别

使用限制

使用方式

查询后过滤（Filter）是表格存储多元索引（Search Index）新增的一种查询辅助功能，支持对 Query 结果再做一次过滤。该功能的目的主要是人工干预内部的查询优化器，强制某些查询条件在最后阶段执行，使用合理，可以大幅提高查询性能。

**说明**

如需使用查询后过滤功能，请加入钉钉群36165029092（表格存储技术交流群-3）联系表格存储技术支持开通。

## **功能介绍**

查询后过滤（Filter）是一种不同于 Query 的查询语法，执行步骤在 Query 阶段执行后， 在 Aggregate 和 GroupBy 阶段执行之前。

主要作用是通过人为控制查询流程，优化查询优化器，将命中量大的查询条件从 Query 阶段移到 Filter 阶段可以大幅提升查询性能。

- Query 阶段：支持多元索引的所有查询类型（例如范围查询、精确查询、模糊查询、地理位置查询等）和所有数据类型，用于从索引中初步检索符合条件的数据。

- Filter 阶段：在Query 阶段的结果上进行二次筛选，仅支持Keyword、Long 和 Double 类型，查询语法支持精确查询、范围查询、存在性查询等类型


## **与其他过滤方式的对比**

### **与 Elasticsearch post\_filter 的区别**

两者的区别主要是生效位置不同：

1. Tablestore 中 Filter 的执行顺序：Query → Filter → Aggregate/TotalCount

2. Elasticsearch 中 post\_filter 的执行顺序：Query → Aggregate/TotalCount → PostFilter


### **与 Tablestore BoolQuery 中 Filter 的区别**

BoolQuery 中 Filter 类似于 BoolQuery 中 Must，属于 Query 中的一个子功能。

## **使用限制**

- 必须与多元索引查询条件组合使用，支持精确查询（TermQuery）、多词精确查询（TermsQuery）、范围查询（RangeQuery）、列存在性查询（ExistsQuery）及其组合查询（BoolQuery）。

- BoolQuery 查询时，仅支持必须匹配（mustQueries）、必须不匹配（mustNotQueries）、可选匹配（shouldQueries）子句，不支持过滤子句（filterQueries）。

- 仅支持对不可分词字符串（Keyword）、长整型（Long）、双精度浮点型（Double）字段进行过滤，且字段必须启用排序统计（enableSortAndAgg）属性。

- 查询后过滤不支持设置权重。


## **使用方式**

当前支持通过 [Java SDK](https://help.aliyun.com/zh/tablestore/developer-reference/query-filter-in-java "")、 [Go SDK](https://help.aliyun.com/zh/tablestore/developer-reference/query-filter-in-go "") 进行查询后过滤。