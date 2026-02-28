### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/)DQL操作

# DQL操作

更新时间：2025-02-17 02:07:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查询表的描述信息](https://help.aliyun.com/zh/tablestore/query-the-information-about-a-table)[下一篇：查询数据](https://help.aliyun.com/zh/tablestore/query-data)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

功能支持列表

表格存储的DQL操作兼容MySQL的查询语法，本文介绍DQL操作支持的功能。

## **背景信息**

表格存储在传统的NoSQL结构化存储之上，提供了云原生的SQL引擎能力，兼容MySQL的查询语法。具体使用方式，请参见 [查询数据](https://help.aliyun.com/zh/tablestore/query-data "")。

## **功能支持列表**

使用SELECT语句时支持结合聚合函数、多元索引查询功能、Join功能进行多维数据查询和分析。具体说明请参见下表。

| **功能** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **功能** | **说明** |
| [聚合函数](https://help.aliyun.com/zh/tablestore/aggregate-functions "") | 对多行数据的指定字段执行计算并返回统计结果，例如计算总数、平均数、最大值、最小值等。 |
| [多元索引全文检索](https://help.aliyun.com/zh/tablestore/full-text-search-by-using-sql-query "") | 使用匹配查询（TEXT\_MATCH）或者短语匹配查询（TEXT\_MATCH\_PHRASE）条件作为SELECT语句中的WHERE子句，可以通过多元索引查询表中匹配指定字符串的数据。 |
| [多元索引数组类型](https://help.aliyun.com/zh/tablestore/multiple-index-array-type "") | 使用ARRAY\_EXTRACT条件作为SELECT语句中的WHERE子句，可以通过多元索引查询数组类型列的数据。 |
| [多元索引嵌套类型](https://help.aliyun.com/zh/tablestore/multiple-index-nested-type "") | 使用嵌套类型的子列直接与运算符组合或者使用`NESTED_QUERY(subcol_column_condition)`函数作为SELECT语句中的WHERE子句，可以通过多元索引查询嵌套类型列的数据。 |
| [多元索引虚拟列](https://help.aliyun.com/zh/tablestore/virtual-columns-of-search-index-in-sql-query "") | 虚拟列可直接作为SELECT语句中的WHERE子句进行数据查询，也可用于统计聚合中进行数据分析，支持按照虚拟列分组、排序和TopN查询。 |
| [多元索引向量检索](https://help.aliyun.com/zh/tablestore/knn-vector-query-of-search-index-in-sql-query "") | 使用VECTOR\_QUERY\_FLOAT32函数作为SELECT语句中的WHERE子句，可以通过多元索引查询向量类型列的数据。同时支持将`SCORE()`函数作为SELECT语句的列表达式来获取查询结果的相关性分数。 |
| [Join](https://help.aliyun.com/zh/tablestore/join-function "") | 使用Join功能将两个表或多个表进行连接，并返回符合连接条件和查询条件的数据。 |
| [JSON函数](https://help.aliyun.com/zh/tablestore/json-functions "") | 使用JSON函数作为SELECT语句中的列表达式，可以使用JSON函数查询JSON数据。 |