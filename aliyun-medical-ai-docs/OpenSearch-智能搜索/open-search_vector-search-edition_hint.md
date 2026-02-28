### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[向量检索传统版（停售）](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-retrieval-general-edition/)[向量检索版文档3.9.0](https://help.aliyun.com/zh/open-search/vector-search-edition/documentation-of-vector-search-edition-v3-9/)[SQL](https://help.aliyun.com/zh/open-search/vector-search-edition/sql-statements/)[查询语法](https://help.aliyun.com/zh/open-search/vector-search-edition/query-syntax-3/)[查询语句](https://help.aliyun.com/zh/open-search/vector-search-edition/query-statements-1/)Hint

# Hint

更新时间：2025-03-13 22:23:36

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：动态参数](https://help.aliyun.com/zh/open-search/vector-search-edition/dynamic-parameters-1)[下一篇：Table Value Function](https://help.aliyun.com/zh/open-search/vector-search-edition/table-valued-function)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

支持版本

语法格式

内置Hint

示例

内置ATTR HINT

单机并发（>=Ha3 3.8.0）

冲突解决

## 描述

为了增强SQL的可定制性，TuringSQL现已支持了Hint语义。

​

## 支持版本

>= Ha3 3.7.3

​

## 语法格式

```sql
Select:
  SELECT [/*+ HintName(params)  */]
    { * | projectItem [, projectItem ]* }
  FROM tableExpression [/*+ HintName(params)  */]

HintName: [a-zA-Z][a-zA-Z_]*
Params:
                                 Identifier[, Identifier]
      |
              Identifier=Identifier[, Identifier=Identifier]
Identifier: [a-zA-Z_][a-zA-Z_0-9]*
```

## 内置Hint

目前TuringSQL内置了如下四种Hint：

| Hint名字 | 含义 | 语法 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| Hint名字 | 含义 | 语法 |
| HASH\_JOIN | 1) 本Hint作用于Table上<br>2) 附带本Hint的Table参与Join时优先采用HashJoin，并且本Table优先为内层build表 | HASH\_JOIN(tableName1， tableName2，...) |
| LOOKUP\_JOIN | 1) 本Hint作用于Table上<br>2) 附带本Hint的Table参与Join时优先采用LookupJoin，并且本Table优先为内层build表 | LOOKUP\_JOIN(tableName1， tableName2，...) |
| NORMAL\_AGG | 1) 指示Hint作用的Aggregate优先采用一阶段执行 | NORMAL\_AGG(<br>distributionCheck='false' \| 'true'，<br>propScope='all'<br>)<br>distributionCheck：是否检查当前分布，如果distributionCheck=’true‘， 但是Agg的Group Key不是分列字段，那么当前Hint失效。<br>propScope：是否将当前Hint向下传播到其他的Agg节点。如果propScope='all'，代表将传播到当前及其以下的agg节点。如果不填，那么代表当前Hint只作用在最近的Agg节点。 |
| NO\_INDEX | 1) 指示Hint作用的字段在Filter时优先不开启索引优化 | NO\_INDEX(<br>tableName='t1', <br>fields='a, b, c'<br>)<br>tableName：用来制定表名。<br>fields: 用来制定不使用索引优化的字段列表。 |

## 示例

**HASH\_JOIN**

```sql
SELECT
    /*+ HASH_JOIN(tj_relation)*/
    *
FROM
    (
        SELECT
            /*+ HASH_JOIN(tj_item_raw)*/
            *
        FROM
            (
                SELECT
                    sum(tj_item.id) as sum0
                FROM
                    tj_item
                GROUP BY
                    tj_item.id
            ) B
            JOIN tj_item_raw on B.sum0 = tj_item_raw.id   --> (1)
    ) D
    JOIN tj_relation on D.sum0 = tj_relation.item_id    --> (2)

(1)(2)两个join会被优化为HashJoin
```

**LOOKUP\_JOIN**

```sql
SELECT
    /*+ LOOKUP_JOIN(tj_relation)*/
    *
FROM
    (
        SELECT
            /*+ LOOKUP_JOIN(tj_item_raw)*/
            *
        FROM
            (
                SELECT
                    sum(tj_item.id) as sum0
                FROM
                    tj_item
                GROUP BY
                    tj_item.id
            ) B
            JOIN tj_item_raw on B.sum0 = tj_item_raw.id  ---> (1)
    ) D
    JOIN tj_relation on D.sum0 = tj_relation.item_id   ---> (2)

(1)(2)两个join均为LookupJoin
```

**NORMAL\_AGG**

```sql
SELECT
    /*+ LOOKUP_JOIN(tj_relation), NORMAL_AGG(distributionCheck='false', propScope='all')*/
    tj_relation.price
FROM
    (
        SELECT
            *
        FROM
            (
                SELECT
                    sum(tj_item.id) as sum0
                FROM
                    tj_item
                GROUP BY              ----> (1)
                    tj_item.id
            ) B
            JOIN tj_item_raw ON B.sum0 = tj_item_raw.id
    ) D
    JOIN tj_relation ON D.sum0 = tj_relation.item_id
GROUP BY                             ----> (2)
    tj_relation.price

(1)(2)两个Agg均为NormalAgg（不拆分两个阶段）
```

**NO\_INDEX**

```sql
SELECT
    /*+ LOOKUP_JOIN(tj_relation), NO_INDEX(tableName='tj_relation', fields='pk') */
    *
FROM
    (
        SELECT
            /*+ NO_INDEX(tableName='tj_item', fields='shop_id, reserve_price') */
            *
        FROM
            (
                SELECT
                    SUM(tj_item.id) as sum0
                FROM
                    tj_item
                    /*+ NO_INDEX(tableName='tj_item', fields='shop_id') */
                WHERE
                        tj_item.id = 100
                    AND
                        tj_item.shop_id = 500   ---> (2)
                GROUP BY
                    tj_item.id
            ) B
            JOIN tj_item_raw on B.sum0 = tj_item_raw.id
    ) D
    JOIN tj_relation /*+ NO_INDEX(tableName='tj_relation', fields='item_id') */  on D.sum0 = tj_relation.item_id
WHERE
    tj_relation.item_id = 900 AND tj_relation.pk = 100   ---> (1)

(1)中的pk和item_id不是用索引
(2)中shop_id不是用索引
```

## 内置ATTR HINT

attr hint是为加速查询处理提供给op的一些辅助信息，主要用于查询的截断，批量的大小等设置，在多列的场景下比较有用。目前支持3种attribute hint。

**SCAN\_ATTR**

为scan op传递信息，目前支持三个参数：

- localLimit：scan输出多少条停止。

- batchSize：scan每批次输出条数，一般与localLimit一起使用。默认是输出全部结果，batchSize由表大小自动计算。

- nestTableJoinType：nest table的join type，可选模式为 {'inner', 'left'} 两种，默认为left join模式。


```sql
SELECT /*+ SCAN_ATTR(localLimit='3',batchSize='2',nestTableJoinType='inner')*/
    company_id, company_name
FROM
          company
```

SCAN\_ATTR也可写在表名之后（推荐方式）。

```sql
SELECT
    company_id, company_name
FROM
    company /*+ SCAN_ATTR(localLimit='3',batchSize='2',nestTableJoinType='inner')*/
```

此外，scan attr还支持按partition查询的功能，注意此功能是调试功能，不要依赖于此功能来做分列查询。

- hashValues: 根据hash values列表计算查询的partition。

- partitionIds: 只查partitionIds列表中的partition，-1为访问全部partition。


指定hash值查，查询a1, a2，会根据表配置的hash func计算出查询的partition id。

```sql
SELECT /*+ SCAN_ATTR(hashValues='a1,a2')*/ company_id, company_name
FROM company
```

指定列查，只查询第1，2两列。

```sql
SELECT /*+ SCAN_ATTR(partitionIds='1,2')*/ company_id, company_name
FROM company
```

**AGG\_ATTR**

为agg op传递信息，目前支持groupKeyLimit与stopExceedLimit两参数，分别是agg key的个数限制与达到限制后是否查询报错。默认key limit是20万，超过key limit查询自动报错。AGG\_ATTR只允许出现在select之后。

AGG\_ATTR也支持propScope参数用于表示传播范围，默认只作用于当前节点。

```sql
SELECT /*+ AGG_ATTR(groupKeyLimit='3',stopExceedLimit='false')*/
    company_id, company_name
FROM
    company
group by
    company_id, company_name
```

**JOIN\_ATTR**

以下只支持 lookup join，用于lookup join的截断。

lookupTurncateThreshold是当lookup inner join成功的key数量达到这个值后join就结束。使用的场景如下：lookup join的input有序，只需要返加top k个有inner join结果的查询。

lookupBatchSize 每批参与lookup join的行数，默认为500。

JOIN\_ATTR也支持propScope参数用于表示传播范围，默认只作用于当前节点。

```sql
SELECT /*+ JOIN_ATTR(lookupTurncateThreshold='30', lookupBatchSize='50')*/
    id, daogou.company_id, company_name
FROM daogou
      JOIN company
      ON daogou.id = company.company_id
```

join\_attr与scan\_attr是可以一起使用的。

```sql
SELECT /*+ JOIN_ATTR(lookupTurncateThreshold='3', lookupBatchSize='2')*/
    id, daogou.company_id, company_name
FROM
    daogou /*+ SCAN_ATTR(localLimit='5',batchSize='1')*/
    JOIN
        company
    ON
        daogou.id = company.company_id
```

**left outer join默认值**

当左表无法join到右表数据时，右表字段会填默认值，join attr 支持修改默认值，每种类型支持一个默认值。

```sql
SELECT /*+ JOIN_ATTR(defaultValue='INTEGER:10,VARCHAR:aa')*/
    id, daogou.company_id, company_name
FROM daogou
      JOIN company
      ON daogou.id = company.company_id
```

## 单机并发（>=Ha3 3.8.0）

目前支持在searcher上开启多路并行优化。LOCAL\_PARALLEL Hint作用在Table上，会自动向上推导可以并发的算子，支持不同的Table开启不同的并发数。

LOCAL\_PARALLEL Hint支持的属性：

- tableName: 指定需要并发的表名，格式为catalogName.dbName.tableName，catalgName和dbName不指定时会使用默认值。

- parallelNum: 并发数。


```sql
SELECT i1
FROM t1 /*+ LOCAL_PARALLEL(tableName='t1', parallelNum='2') */

SELECT i1, COUNT(*)
FROM t1 /*+ LOCAL_PARALLEL(tableName='t1', parallelNum='2') */
GROUP BY i1

SELECT t1.id, t2.id
FROM tj_item /*+ LOCAL_PARALLEL(tableName='tj_item', parallelNum='2') */ AS t1
JOIN tj_shop AS t2
ON t1.id = t2.id
```

说明：开启单机并发后不一定会有明显性能提升，需要配合trace和plan确定瓶颈在哪个算子。

注意：与老的方式不兼容，不能同时开启。

## 冲突解决

- 如果当前节点存在多个同类Hint，则传播路径最短的Hint生效；如果存在多个传播路径一样的Hint，则Hint失效。

- 如果当前节点存在多个不同类但冲突的Hint，则Hint失效。

- 如果Hint会使优化器产出错误计划，则Hint失效。

- 建议有问题时查看生成的计划，确定Hint是否生效。