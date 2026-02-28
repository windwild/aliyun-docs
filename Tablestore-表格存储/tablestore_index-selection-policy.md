### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/)[查询优化](https://help.aliyun.com/zh/tablestore/query-optimization/)索引选择策略

# 索引选择策略

更新时间：2025-01-22 00:17:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用数据表映射表

自动选择策略

手动选择策略

使用二级索引映射表

使用多元索引映射表

附录：多元索引中功能与SQL表达式的映射

相关文档

表格存储作为海量结构化大数据存储，支持不同的索引结构，便于不同场景下进行查询分析加速使用。本文介绍在数据表上存在多元索引和二级索引时如何选择SQL查询所使用的索引。

**说明**

关于二级索引和多元索引的更多信息，请分别参见 [二级索引](https://help.aliyun.com/zh/tablestore/overview-of-secondary-index/#concept-ogb-g2b-ffb "") 和 [多元索引简介](https://help.aliyun.com/zh/tablestore/search-index-introduction-of-tablestore/#concept-gmr-nyf-ffb "")。

## **使用数据表映射表**

当数据表上存在二级索引和多元索引时，使用SQL查询会涉及到多个索引的选择，索引选择策略包括自动选择策略和手动选择策略。

**重要**

请确保已在数据表上创建映射关系。具体操作，请参见 [创建表的映射关系](https://help.aliyun.com/zh/tablestore/create-mapping-tables-for-tables-of-sql-query#concept-2098376 "")。

### **自动选择策略**

使用数据表的映射表查询数据时，表格存储会自动选择数据表、二级索引或多元索引进行数据查询。

**重要**

- 如果创建表的映射关系时设置了执行的查询结果要满足强一致性或者不允许通过牺牲聚合操作的精度提升查询性能，则表格存储不会自动选择多元索引进行数据查询。

- 当二级索引和多元索引同时包含SQL查询涉及的所有列时，表格存储会优先选择多元索引进行数据查询。


自动选择策略由上到下依次执行。具体执行流程如下：

1. **自动选择多元索引**：如果WHERE子句中的所有过滤列、聚合计算和排序涉及的列均包含在同一个多元索引中，则表格存储会自动选择该多元索引进行数据查询。

例如`SELECT A,B,C FROM sampletable WHERE A=XXX and D = YY;`语句，如果A、B、C、D列均在sampletable表上的同一个多元索引中，则会自动选择到多元索引进行查询。

此外，当Groupby、聚合函数等组合使用时，如果符合多元索引Search接口的统计聚合能力，则表格存储也会进行识别并下推算子，关于下推算子的更多信息，请参见 [计算下推](https://help.aliyun.com/zh/tablestore/computing-pushdown#concept-2098481 "")。

2. **自动选择二级索引**：如果二级索引能比数据表命中更多的WHERE子句中的主键条件（遵循最左匹配原则），且覆盖了SQL查询涉及的所有列，则表格存储会自动选择该二级索引进行数据查询。

例如数据表主键为a、b，数据表上某个二级索引的主键为c、a、b，当查询条件为`c = 1 and a > 1`时，二级索引命中两个主键列，数据表命中一个主键列，则会自动选择到二级索引进行查询。

3. **自动选择数据表或二级索引**：根据SQL引擎内部的CBO逻辑从数据表或二级索引间进行选择，此时的选择结果与具体SQL的Pattern有关，SQL引擎会尽量选择代价较低的索引来执行查询。


### **手动选择策略**

当要在查询数据时稳定地选择某一个索引时，您可以通过`use index`语法显式指定索引或者直接使用索引的映射表。

此处以数据表名为sampletable，多元索引名为sampletable\_search\_index，二级索引名为sampletable\_secondary\_index为例介绍手动选择策略的操作。

- **显式指定访问数据表**

在SQL语句中显式指定访问数据表。SQL示例如下：















```sql
SELECT * FROM sampletable use index();
```

- **显式指定访问多元索引或二级索引**



**说明**





如果索引中不包含SQL查询相关的列，则SQL引擎会自动反查数据表以获取所需数据。





在SQL语句中显式指定要访问的索引。SQL示例如下：















```sql
SELECT * FROM sampletable use index(sampletable_search_index); --显式访问多元索引
SELECT * FROM sampletable use index(sampletable_secondary_index); --显式访问二级索引
```


## **使用二级索引映射表**

当要通过指定的二级索引查询数据时，您可以直接使用二级索引映射关系进行查询。具体操作如下：

**说明**

使用索引映射表查询数据时，只能查询索引中包含的数据列。

1. 使用CREATE TABLE语句创建二级索引表的映射关系。具体操作，请参见 [创建表的映射关系](https://help.aliyun.com/zh/tablestore/create-mapping-tables-for-tables-of-sql-query#concept-2098376 "")。

2. 使用SELECT语句通过二级索引映射表查询数据。具体操作，请参见 [查询数据](https://help.aliyun.com/zh/tablestore/query-data#concept-2098388 "")。


## **使用多元索引映射表**

当要通过指定的多元索引查询数据时，您可以直接使用多元索引映射关系进行查询。具体操作如下：

**说明**

使用索引映射表查询数据时，只能查询索引中包含的数据列。

1. 使用CREATE TABLE语句创建多元索引的映射关系。具体操作，请参见 [创建多元索引的映射关系](https://help.aliyun.com/zh/tablestore/create-mapping-tables-for-search-indexes-of-sql-query#concept-2196713 "")。

2. 使用SELECT语句通过多元索引映射表查询数据。具体操作，请参见 [查询数据](https://help.aliyun.com/zh/tablestore/query-data#concept-2098388 "")。


## 附录：多元索引中功能与SQL表达式的映射

多元索引能够实现与SQL表达式相同的功能，具体功能映射信息请参见下表。

| **SQL表达式** | **示例** | **多元素引中功能** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **SQL表达式** | **示例** | **多元素引中功能** |
| without predicate | 不涉及 | [全匹配查询（MatchAllQuery）](https://help.aliyun.com/zh/tablestore/match-all-query-function#concept-227002 "") |
| = | - a = 1<br>  <br>- b = "hello world" | [精确查询（TermQuery）](https://help.aliyun.com/zh/tablestore/term-query-function#concept-227006 "") |
| > | a > 1 | [范围查询（RangeQuery）](https://help.aliyun.com/zh/tablestore/range-query-function#concept-227247 "") |
| >= | a >= 2 |
| < | a < 5 |
| <= | a <= 10 |
| is null | a is null | [列存在性查询（ExistsQuery）](https://help.aliyun.com/zh/tablestore/exists-query-function#concept-995063 "") |
| is not null | a is not null |
| and | a = 1 and b = "hello world" | [多条件组合查询（BoolQuery）](https://help.aliyun.com/zh/tablestore/boolean-query-function#concept-227249 "") |
| or | a > 1 or b = 2 |
| not | not a = 1 |
| != | a !=1 |
| like | a like "%s%" | [通配符查询（WildcardQuery）](https://help.aliyun.com/zh/tablestore/wildcard-query-function#concept-227248 "") |
| in | a in (1,2,3) | [多词精确查询（TermsQuery）](https://help.aliyun.com/zh/tablestore/terms-query-function#concept-227243 "") |
| text\_match | text\_match(a, "tablestore cool") | [匹配查询（MatchQuery）](https://help.aliyun.com/zh/tablestore/match-query-function#concept-227004 "") |
| text\_match\_phrase | text\_match\_phrase(a, "tablestore cool") | [短语匹配查询（MatchPhraseQuery）](https://help.aliyun.com/zh/tablestore/match-phrase-query-function#concept-227005 "") |
| array\_extract | array\_extract(col\_long) | [数组和嵌套类型](https://help.aliyun.com/zh/tablestore/array-and-nested-field-types "") |
| nested\_query | nested\_query(\`tags.tagName\` = 'tag1' AND \`tags.score\` = 0.2) | - [数组和嵌套类型](https://help.aliyun.com/zh/tablestore/array-and-nested-field-types "")<br>  <br>- [嵌套类型查询（NestedQuery）](https://help.aliyun.com/zh/tablestore/nested-query-function "") |
| order by | nested\_query col\_long | [排序和翻页](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#concept-226989 "") |
| limit | limit 10 |
| min() | min(col\_long) | [统计聚合](https://help.aliyun.com/zh/tablestore/aggregation-of-tablestore "") |
| max() | max(col\_long) |
| sum() | sum(col\_long) |
| avg() | avg(col\_long) |
| count() | count(col\_long) |
| count(distinct) | count(distinct col\_long) |
| any\_value() | any\_value(col\_long) |
| group by | group by col\_long |

## **相关文档**

使用多元索引加速SQL查询数据时，您可以通过多元索引实现 [全文检索](https://help.aliyun.com/zh/tablestore/full-text-search-by-using-sql-query "")、 [多元索引数组类型](https://help.aliyun.com/zh/tablestore/multiple-index-array-type "")、 [多元索引嵌套类型](https://help.aliyun.com/zh/tablestore/multiple-index-nested-type "")、 [多元索引虚拟列](https://help.aliyun.com/zh/tablestore/virtual-columns-of-search-index-in-sql-query "") 等功能。