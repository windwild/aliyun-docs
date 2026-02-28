### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[向量检索传统版（停售）](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-retrieval-general-edition/)[向量检索版文档3.9.0](https://help.aliyun.com/zh/open-search/vector-search-edition/documentation-of-vector-search-edition-v3-9/)[SQL](https://help.aliyun.com/zh/open-search/vector-search-edition/sql-statements/)[查询语法](https://help.aliyun.com/zh/open-search/vector-search-edition/query-syntax-3/)[查询语句](https://help.aliyun.com/zh/open-search/vector-search-edition/query-statements-1/)WHERE

# WHERE

更新时间：2024-02-27 22:22:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SELECT](https://help.aliyun.com/zh/open-search/vector-search-edition/select)[下一篇：ORDER BY](https://help.aliyun.com/zh/open-search/vector-search-edition/order-by-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

支持版本

语法格式

示例

Hint

## 描述

WHERE用于有条件地从表中选取数据。

​

## 支持版本

>= Ha3 3.7.0

​

## 语法格式

```sql
select:
  SELECT [ DISTINCT ]
    { * | projectItem [, projectItem ]* }
  FROM tableExpression
    [ WHERE booleanExpression ]
```

其中booleanExpression可以为以下几种：

| 序号 | 表达式类型 | 实例 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 序号 | 表达式类型 | 实例 |
| 0 | AND, OR | 1. WHERE a > 1 AND a < 100<br>   <br>2. WHERE a > 5 OR c > 100 |
| 1 | >, >=, <, <=, <> |  |
| 2 | IN | WHERE id IN (1, 2, 3, 4, 5) |
| 3 | UDF（ [更多](https://help.aliyun.com/zh/open-search/vector-search-edition/overview-6 "")） | 1. WHERE MATCHINDEX(brand, "Huawei")<br>   <br>2. WHERE QUERY(brand, "Huawei OR OPPO")<br>   <br>3. WHERE UDF(brand, "test") > 10 |

## 示例

```sql
SELECT * FROM table WHERE f1 > 10 AND f2 < 5

SELECT * FROM table WHERE id IN (5, 6, 7, 8, 9)
```

## Hint

turing sql支持where使用ha3的倒排优化加速查找，如MATCHINDEX，QUERY为兼容ha3查询的语法实现，以及等值条件，如 `SELECT * FROM table WHERE f1 = 10`，当f1是建立倒排索引的等值条件场景下，能够自动优化为倒排查找。scan op会自动提取能够优化的query 条件。