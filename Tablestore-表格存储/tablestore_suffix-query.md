### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[多元索引](https://help.aliyun.com/zh/tablestore/search-index-introduction-of-tablestore/)[基础查询](https://help.aliyun.com/zh/tablestore/basic-features/)[模糊查询](https://help.aliyun.com/zh/tablestore/like/)后缀查询

# 后缀查询

更新时间：2025-03-09 23:32:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：前缀查询](https://help.aliyun.com/zh/tablestore/prefix-query-function)[下一篇：基于分词的通配符查询](https://help.aliyun.com/zh/tablestore/fuzzy-query)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能概述

接口

参数

使用方式

计费说明

常见问题

相关文档

后缀查询（SuffixQuery）是通过指定后缀条件查询索引中的数据，例如通过手机尾号后4位查询快递。

## **功能概述**

后缀查询主要用于查找以特定后缀结尾的数据。使用SuffixQuery功能查询数据时，您需要指定后缀值。

当前支持用于SuffixQuery的数据类型只有FuzzyKeyword。FuzzyKeyword是专门为SuffixQuery、PrefixQuery和WildcardQuery等模糊查询功能优化过的数据类型，在小、中、大规模数据上的查询性能均会更好更稳定，且性能基本不会随着数据规模增长而下降。

**说明**

- FuzzyKeyword类型的字段不支持排序和统计聚合。如果FuzzyKeyword类型的字段同时需要进行排序或统计聚合，可以通过虚拟列为Keyword类型实现。

- 如果希望在Keyword类型上实现后缀查询效果，您可以在写入数据时将数据翻转，然后使用前缀查询（PrefixQuery）功能进行数据查询。


## 接口

后缀查询的接口为 [Search](https://help.aliyun.com/zh/tablestore/developer-reference/search "") 或者 [ParallelScan](https://help.aliyun.com/zh/tablestore/developer-reference/parallelscan "")，具体的Query类型为SuffixQuery。

## **参数**

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| query | 设置查询类型为SuffixQuery。 |
| fieldName | 要匹配的字段。 |
| suffix | 后缀值。 |
| getTotalCount | 是否返回匹配的总行数，默认为false，表示不返回。 <br>返回匹配的总行数会影响查询性能。 |
| weight | 查询权重，用于全文检索场景中的score排序。查询时指定列的算分权重，值越大，结果中分数的值会越大。取值范围为正浮点数。<br>使用此参数不会影响返回的结果数，只会影响返回的结果中的分数。 |
| tableName | 数据表名称。 |
| indexName | 多元索引名称。 |
| columnsToGet | 是否返回所有列，包含returnAll和columns设置。 <br>returnAll默认为false，表示不返回所有列，此时可以通过columns指定返回的列；如果未通过columns指定返回的列，则只返回主键列。<br>当设置returnAll为true时，表示返回所有列。 |

## **使用方式**

您可以使用控制台或者SDK进行后缀查询。进行后缀查询之前，您需要完成如下准备工作。

- 已创建RAM用户并为RAM用户授权表格存储操作权限。具体操作，请参见 [使用RAM用户访问密钥访问表格存储](https://help.aliyun.com/zh/tablestore/developer-reference/access-tablestore-by-ram-user "")。

- 已创建数据表。具体操作，请参见 [数据表操作](https://help.aliyun.com/zh/tablestore/table-operations "")。

- 已为数据表创建多元索引。具体操作，请参见 [创建多元索引](https://help.aliyun.com/zh/tablestore/create-search-indexes-by-using-console-cli-or-sdk "")。


**使用控制台**

1. 进入 **索引管理** 页签。

1. 登录[表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择资源组和地域。

3. 在 **概览** 页面，单击实例名称或在 **操作** 列单击 **实例管理**。

4. 在 **实例详情** 页签下的 **数据表列表** 页签，单击数据表名称或在操作列单击 **索引管理**。
2. 在 **索引管理** 页签，单击目标多元索引 **操作** 列的 **搜索**。

1. 系统默认返回所有列，如需显示指定属性列，关闭 **获取所有列** 并输入需要返回的属性列，多个属性列之间用半角逗号（,）隔开。



      **说明**





      系统默认会返回数据表的主键列。

2. 根据需要选择逻辑操作符为 **And**、 **O** r 或者 **Not**。

      当选择逻辑操作符为 **And** 时，返回满足指定条件的数据。当选择逻辑操作符为 **Or** 时，如果配置了单个条件，则返回满足指定条件的数据；如果配置了多个条件，则返回满足任意一个条件的数据。当选择逻辑操作符为 **Not** 时，返回不满足指定条件的数据。

3. 选择FuzzyKeyword类型的索引字段，单击 **添加**。

4. 设置索引字段的查询类型为 **后缀查询（SuffixQuery）** 和输入要查询的值。

5. 系统默认关闭排序功能，如需根据指定字段对返回结果进行排序，打开 **是否排序** 开关后，根据需要添加要进行排序的字段并配置排序方式。

6. 系统默认关闭统计功能，如需对指定字段进行数据统计，打开 **是否统计** 开关后，根据需要添加要进行统计的字段和配置统计信息。
3. 单击 **确定**。

符合查询条件的数据会显示在 **索引管理** 页签中。


**使用SDK**

您可以通过 [Java SDK](https://help.aliyun.com/zh/tablestore/developer-reference/suffix-query-by-using-java-sdk "") 使用后缀查询。

**重要**

- 表格存储Java SDK从5.17.0版本开始支持后缀查询功能。

- 使用SDK进行后缀查询前，您需要初始化Client。具体操作，请参见 [初始化Client](https://help.aliyun.com/zh/tablestore/tablestore-client-initiation-in-java "")。


以下示例用于查询表中Col\_FuzzyKeyword列的值中后缀为"hangzhou"的数据。

```java
/**
 * 查询表中Col_FuzzyKeyword列中后缀为"hangzhou"的数据。
 * @param client
 */
private static void suffixQuery(SyncClient client) {
    SearchQuery searchQuery = new SearchQuery();
    SuffixQuery suffixQuery = new SuffixQuery(); //设置查询类型为SuffixQuery。
    searchQuery.setGetTotalCount(true);
    suffixQuery.setFieldName("Col_FuzzyKeyword");
    suffixQuery.setSuffix("hangzhou");
    searchQuery.setQuery(suffixQuery);
    //searchQuery.setGetTotalCount(true); //设置返回匹配的总行数。

    SearchRequest searchRequest = new SearchRequest("<TABLE_NAME>", "<SEARCH_INDEX_NAME>", searchQuery);
    //通过设置columnsToGet参数可以指定返回的列或返回所有列，如果不设置此参数，则默认只返回主键列。
    SearchRequest.ColumnsToGet columnsToGet = new SearchRequest.ColumnsToGet();
    //columnsToGet.setReturnAll(true); //设置为返回所有列。
    columnsToGet.setColumns(Arrays.asList("Col_FuzzyKeyword")); //设置为返回指定列。
    searchRequest.setColumnsToGet(columnsToGet);

    SearchResponse resp = client.search(searchRequest);
    //System.out.println("TotalCount: " + resp.getTotalCount()); //打印匹配到的总行数，非返回行数。
    System.out.println("Row: " + resp.getRows());
}
```

## **计费说明**

使用 VCU 模式（原预留模式）时，使用多元索引查询数据会消耗 VCU 的计算资源。使用 CU 模式（原按量模式）时，使用多元索引查询数据会消耗读吞吐量。更多信息，请参见 [多元索引计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-search-indexes-1 "")。

## **常见问题**

- [使用多元索引 Search 接口查不到数据](https://help.aliyun.com/zh/tablestore/what-do-i-do-if-no-data-can-be-found-by-calling-the-search-operation "")

- [如何将多元索引 Search 接口查询数据的 limit 提高到 1000](https://help.aliyun.com/zh/tablestore/support/how-do-i-increase-the-value-of-the-limit-parameter-to-1000-when-i-call-the-search-operation-of-the-search-index-feature-to-query-data "")

- [为什么使用多元索引翻页查询时 Token 失效了？](https://help.aliyun.com/zh/tablestore/why-does-a-token-become-invalid-when-pagination-is-used-in-a-search-index-based-query "")


## **相关文档**

- 多元索引查询类型包括 [精确查询](https://help.aliyun.com/zh/tablestore/term-query-function "")、 [多词精确查询](https://help.aliyun.com/zh/tablestore/terms-query-function "")、 [全匹配查询](https://help.aliyun.com/zh/tablestore/match-all-query-function "")、 [匹配查询](https://help.aliyun.com/zh/tablestore/match-query-function "")、 [短语匹配查询](https://help.aliyun.com/zh/tablestore/match-phrase-query-function "")、 [范围查询](https://help.aliyun.com/zh/tablestore/range-query-function "")、 [前缀查询](https://help.aliyun.com/zh/tablestore/prefix-query-function "")、 [后缀查询](https://help.aliyun.com/zh/tablestore/suffix-query "")、 [通配符查询](https://help.aliyun.com/zh/tablestore/wildcard-query-function "")、 [基于分词的通配符查询](https://help.aliyun.com/zh/tablestore/fuzzy-query "")、 [组合查询](https://help.aliyun.com/zh/tablestore/boolean-query-function "")、 [地理位置查询](https://help.aliyun.com/zh/tablestore/geographical-location-query/ "")、 [嵌套类型查询](https://help.aliyun.com/zh/tablestore/nested-query-function "")、 [向量检索、](https://help.aliyun.com/zh/tablestore/vector-query-introduction-and-usage "") 和 [列存在性查询](https://help.aliyun.com/zh/tablestore/exists-query-function "")，您可以选择合适的查询类型进行多维度数据查询。

如果要对结果集进行排序或者翻页，您可以使用排序和翻页功能来实现。具体操作，请参见 [排序和翻页](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function "")。

如果要按照某一列对结果集做折叠，使对应类型的数据在结果展示中只出现一次，您可以使用折叠（去重）功能来实现。具体操作，请参见 [折叠（去重）](https://help.aliyun.com/zh/tablestore/collapse "")。

- 如果要进行数据分析，例如求最值、求和、统计行数等，您可以使用 Search 接口的统计聚合功能或者 SQL 查询来实现。具体操作，请参见 [统计聚合](https://help.aliyun.com/zh/tablestore/aggregation-of-tablestore "") 和 [SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/ "")。

- 如果要快速导出数据，而不关心整个结果集的顺序时，您可以使用 ParallelScan 接口和 ComputeSplits 接口实现多并发导出数据。具体操作，请参见 [并发导出数据](https://help.aliyun.com/zh/tablestore/parallel-scan-2 "")。