### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-召回引擎版](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/)[引擎技术文档](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/documentation-of-retrieval-engine-edition-v3-9-0/)[SQL](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/sql-statement/)[查询语法](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/query-syntax/)[SQL语法](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/sql-syntax/)查询语句

# SELECT

更新时间：2025-03-07 04:34:12

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SQL语法](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/sql-syntax/)[下一篇：Summary查询](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/summary-queries)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

SELECT

描述

支持版本

语法格式

示例

case when

描述

支持版本

语法格式​

示例

注意

## SELECT

### 描述

SELECT 语句用于从表中选取数据。

SELECT语句是查询语法的核心，所有高级查询语法都是围绕SELECT语句展开的。本节将简单介绍HA3支持的SELECT语句语法，高级用法请参考其他的小节。

### 支持版本

>= Ha3 3.7.0

### 语法格式

```sql
SELECT:
  SELECT [ DISTINCT ]
   { * | projectItem [, projectItem ]* }
  FROM tableExpression
   [ WHERE booleanExpression ]
   [ GROUP BY { groupItem [, groupItem ]* } ]
    [ ORDER BY { orderByItem [, OrderByItem ]* }]
   [ HAVING booleanExpression ]
    [ LIMIT number]
    [ OFFSET number]

projectItem:
  expression [ [ AS ] columnAlias ]
  | tableAlias . *
```

### 示例

```sql
SELECT * FROM table;

SELECT f1, f2 AS ff FROM table;

SELECT DISTINCT f FROM table;

SELECT * FROM (
      SELECT f1, count(*) AS num
      FROM t1
      GROUP BY f1
  ) tt
  WHERE tt.num > 100;
```

## case when

### 描述

功能类似于if...else if...else语句。如果某个when条件为TRUE，则取对应的then表达式的值；如果所有when条件都为FALSE，则取else表达式的值。

​

### 支持版本

>= Ha3 3.7.5

​

### 语法格式​

```sql
CASE
WHEN condition_1 THEN expression_1
WHEN condition_2 THEN expression_2
……
ELSE expression_n
END
```

### 示例

1. case when 作为输出表达式


```sql
SELECT
    CASE
        WHEN warehouse_id=48 THEN warehouse_id
        WHEN warehouse_id=24 THEN id
        ELSE wave_status
    END AS aa
FROM    s_wmp_package_wave
WHERE   wave_status = 0
LIMIT   10;
```

2. case when 作为条件表达式


```sql
SELECT * FROM
(
  SELECT
  CASE
    WHEN warehouse_id=48 THEN warehouse_id
    WHEN warehouse_id=24 THEN id
    ELSE wave_status
  END AS aa
  FROM    s_wmp_package_wave
  WHERE   wave_status = 0
) t
WHERE t.aa > 10
LIMIT   10;
```

```sql
SELECT *
FROM s_wmp_package_wave
WHERE CASE
        WHEN warehouse_id=48 THEN warehouse_id
  WHEN warehouse_id=24 THEN id
        ELSE buyer_id
END > 10
AND wave_status = 0
LIMIT   10;
```

### 注意

1. 所有THEN、ELSE表达式的值的类型必须一致。

2. 目前只支持CASE WHEN作为一个独立的表达式使用，而不能嵌套于其它表达式或UDF中。如下面表达式暂时不支持：


```sql
SELECT *
FROM s_wmp_package_wave
WHERE CASE
        WHEN warehouse_id=48 THEN warehouse_id
  WHEN warehouse_id=24 THEN id
        ELSE buyer_id
END + wave_status> 10
LIMIT   10;
```

3. CASE WHEN不能用于多值字段。

4. 一定要有ELSE分支。