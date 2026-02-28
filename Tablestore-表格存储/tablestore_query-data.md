### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/)[DQL操作](https://help.aliyun.com/zh/tablestore/dql-statements/)查询数据

# 查询数据

更新时间：2025-05-20 22:58:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DQL操作](https://help.aliyun.com/zh/tablestore/dql-statements/)[下一篇：聚合函数](https://help.aliyun.com/zh/tablestore/aggregate-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

注意事项

语法

参数

列表达式（select\_expr）

目标表信息（table\_references）

WHERE子句（where\_condition）

GROUP BY分组查询（groupby\_condition）

HAVING子句（having\_condition）

ORDER BY排序（order\_condition）

常见问题

本文为您介绍如何执行SELECT语句查询表中的数据。

## 前提条件

已创建映射关系。

- 如果通过表查询数据，请 [创建表的映射关系](https://help.aliyun.com/zh/tablestore/create-mapping-tables-for-tables-of-sql-query "")。

- 如果通过多元索引查询数据，请 [创建多元索引的映射关系](https://help.aliyun.com/zh/tablestore/create-mapping-tables-for-search-indexes-of-sql-query "")。


## 注意事项

- 如果在未创建数据表的映射关系的情况下，直接使用SQL语句（例如DESCRIBE、SELECT等）查询数据，系统后台将自动创建该数据表的映射关系。自动创建的映射表仅包含数据表的主键列和预定义列，并且不支持更新属性列。

- 当数据表上存在二级索引或多元索引时，执行SQL查询将涉及 [索引选择策略](https://help.aliyun.com/zh/tablestore/index-selection-policy "")，包括自动选择策略和手动选择策略。

- SELECT语句中子句的执行优先级为WHERE子句 \> GROUP BY分组查询 \> HAVING子句 \> ORDER BY排序 \> LIMIT和OFFSET。


## 语法

```sql
SELECT
    [ALL | DISTINCT | DISTINCTROW]
    select_expr [, select_expr] ...
    [FROM table_references | join_expr]
    [WHERE where_condition]
    [GROUP BY groupby_condition]
    [HAVING having_condition]
    [ORDER BY order_condition]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}]
```

## 参数

| **参数** | **是否必选** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **是否必选** | **说明** |
| ALL \| DISTINCT \| DISTINCTROW | 否 | 是否去掉重复的字段，取值范围如下：<br>- ALL（默认）：返回字段中所有重复的值。<br>  <br>- DISTINCT：去掉重复的字段，返回去重字段后的值。<br>  <br>- DISTINCTROW：去掉重复的行，返回去重行后的值。 |
| select\_expr | 是 | 列名或者列表达式，格式为`column_name[, column_name][, column_exp],...`。更多信息，请参见 [列表达式（select\_expr）](https://help.aliyun.com/zh/tablestore/query-data#section-evw-o12-23c "")。 |
| table\_references | 是 | 目标表信息，可以是表名或者SELECT语句，格式为`table_name | select_statement`。更多信息，请参见 [目标表信息（table\_references）](https://help.aliyun.com/zh/tablestore/query-data#section-xm2-i94-062 "")。 |
| join\_expr | 否 | JOIN表达式，用于使用Join功能，格式为`table_references join_type table_references [ ON join_condition | USING ( join_column [, ...] ) ]`。当要使用Join功能时才需要配置此参数。<br>Join功能允许将两表或多表进行连接，并返回符合连接条件和查询条件的数据。更多信息，请参见 [Join](https://help.aliyun.com/zh/tablestore/join-function#main-2348495 "")。 |
| where\_condition | 否 | WHERE子句，可配合不同条件实现相应功能。<br>- 配合关系运算符查询符合指定条件的数据，格式为`column_name operator value [AND | OR] [column_name operator value]`。更多信息，请参见 [WHERE子句（where\_condition）](https://help.aliyun.com/zh/tablestore/query-data#section-95g-dvh-yof "")。<br>  <br>- 配合匹配查询或者短语匹配查询条件实现全文检索。更多信息，请参见 [全文检索](https://help.aliyun.com/zh/tablestore/full-text-search-by-using-sql-query#concept-2190182 "")。<br>  <br>- 配合`ARRAY_EXTRACT(col_name)`函数实现多元索引数组类型的数据查询。更多信息，请参见 [多元索引数组类型](https://help.aliyun.com/zh/tablestore/multiple-index-array-type#main-2353288 "")。<br>  <br>  其中`col_name`为数组列名。<br>  <br>- 配合运算符或使用`NESTED_QUERY(subcol_column_condition)`函数实现多元索引嵌套类型的数据查询。更多信息，请参见 [多元索引嵌套类型](https://help.aliyun.com/zh/tablestore/multiple-index-nested-type#main-2354295 "")。<br>  <br>  其中`subcol_column_condition`为同一嵌套层级下的子列查询条件。<br>  <br>- 配合虚拟列查询满足条件的数据。更多信息，请参见 [多元索引虚拟列](https://help.aliyun.com/zh/tablestore/virtual-columns-of-search-index-in-sql-query "")。 |
| groupby\_condition | 否 | GROUP BY分组查询，可配合聚合函数使用，格式为`column_name`。更多信息，请参见 [GROUP BY分组查询（groupby\_condition）](https://help.aliyun.com/zh/tablestore/query-data#section-glb-mcz-9wc "")。 |
| having\_condition | 否 | HAVING子句，可配合聚合函数使用，格式为` aggregate_function(column_name) operator value`。更多信息，请参见 [HAVING子句（having\_condition）](https://help.aliyun.com/zh/tablestore/query-data#section-cv9-xx7-tch "")。 |
| order\_condition | 否 | ORDER BY排序，格式为`column_name [ASC | DESC][,column_name [ASC | DESC],...]`。更多信息，请参见 [ORDER BY排序（order\_condition）](https://help.aliyun.com/zh/tablestore/query-data#section-bk9-pnd-xpc "")。 |
| row\_count | 否 | 本次查询需要返回的最大行数。 |
| offset | 否 | 本次查询的数据偏移量，默认偏移量为0。 |

## 列表达式（select\_expr）

通过列表达式指定需要查询的列。使用规则如下：

- 使用星号（\*）查询所有列，支持配合WHERE子句指定查询条件。















```sql
SELECT * FROM orders;
```





使用WHERE子句作为查询条件的示例如下：

















```sql
SELECT * FROM orders WHERE orderprice >= 100;
```

- 使用列名指定查询的列。















```sql
SELECT username FROM orders;
```

- 使用JSON函数查询JSON对象















```sql
SELECT coljson, coljson->>'$.a' AS subdoc FROM json_table WHERE pkint = 1;
```



关于JSON函数的更多信息，请参见 [JSON函数](https://help.aliyun.com/zh/tablestore/json-functions#concept-2313379 "")。


## 目标表信息（table\_references）

通过目标表信息指定需要查询的表。

```sql
SELECT orderprice FROM orders;
```

## WHERE子句（where\_condition）

通过WHERE子句查询满足指定条件的数据。使用规则如下：

- 配合算术运算符、关系运算符等构造的简单表达式使用。















```sql
SELECT * FROM orders WHERE username = 'lily';
SELECT * FROM orders WHERE orderprice >= 100;
```

- 配合逻辑运算符构造的组合表达式使用。















```sql
SELECT * FROM orders WHERE username = 'lily' AND orderprice >= 100;
```


关于操作符的更多信息，请参见 [SQL操作符](https://help.aliyun.com/zh/tablestore/sql-operators#concept-2098382 "")。

## GROUP BY分组查询（groupby\_condition）

通过GROUP BY子句对SELECT语句的结果集按照指定条件进行分组。使用规则如下：

- 按照字段分组















```sql
SELECT username FROM orders GROUP BY username;
```

- 在分组的列上支持使用聚合函数















```sql
SELECT username,COUNT(*) FROM orders GROUP BY username;
```

- SELECT的所有列中没有使用聚合函数的列，必须出现在GROUP BY中。















```sql
SELECT username,orderprice FROM orders GROUP BY username,orderprice;
```


关于聚合函数的更多信息，请参见 [聚合函数](https://help.aliyun.com/zh/tablestore/aggregate-functions#concept-2098409 "")。

## HAVING子句（having\_condition）

通过HAVING子句对WHERE子句和GROUP BY分组查询后的分组结果集进行过滤，查询满足条件的分组结果。

通常HAVING子句与聚合函数配合使用，实现过滤。

```sql
SELECT username,SUM(orderprice) FROM orders GROUP BY username HAVING SUM(orderprice) < 500;
```

## ORDER BY排序（order\_condition）

通过ORDER BY子句按照指定字段和排序方式对查询结果集进行排序。使用规则如下：

- 支持使用ASC或者DESC关键字设置排序方式。 默认按照升序（ASC）排列。















```sql
SELECT * FROM orders ORDER BY orderprice DESC LIMIT 10;
```

- 支持设置多个字段进行排序。















```sql
SELECT * FROM orders ORDER BY username ASC,orderprice DESC LIMIT 10;
```

- 通常与LIMIT配合使用限定返回的行数。















```sql
SELECT * FROM orders ORDER BY orderprice LIMIT 10;
```


## **常见问题**

- [SQL查询常见错误排查](https://help.aliyun.com/zh/tablestore/troubleshoot-common-errors-of-sql-query "")

- [使用SQL查询存在数据延迟问题](https://help.aliyun.com/zh/tablestore/what-do-i-do-if-delay-in-querying-data-by-sql "")

- [使用SQL查询数据时报错The sql scanned rows of main table exceeds the quota, main table rows quota is 100000](https://help.aliyun.com/zh/tablestore/the-sql-scanner-rows-of-main-table-exceeded-the-quota "")