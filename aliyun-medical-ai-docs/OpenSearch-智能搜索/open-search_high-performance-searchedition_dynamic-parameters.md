### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[SQL支持](https://help.aliyun.com/zh/open-search/high-performance-searchedition/sql-features/)[SQL查询语句语法](https://help.aliyun.com/zh/open-search/high-performance-searchedition/sql-query-syntax/)动态参数

# 动态参数

更新时间：2025-09-14 22:44:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：JOIN操作类型](https://help.aliyun.com/zh/open-search/high-performance-searchedition/join-operation-types-1/)[下一篇：Table Value Function](https://help.aliyun.com/zh/open-search/high-performance-searchedition/table-valued-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

## **描述**

动态参数类似的数据库中的PrepareStatement。用户可以在SQL中设置placeholder（?表示），同时传递placeholder对应的值。引擎内部会自动替换。

动态参数主要用于提高Cache命中率，对于查询模式固定的场景性能提升明显。

注意动态参数只能替换值，不支持关键字或字段替换。

## **示例**

示例1

```sql
SELECT i1, cast(? as bigint) FROM t1 WHERE (i2 > 5 AND d3 < 10.1) OR s5 = ?
```

为了替换掉SQL中的动态参数（也就是"?"）,具体如下：

```sql
 dynamic_params:[[10, "str5"]]
```

示例2

```sql
SELECT
    price,
    title,
    compute(
        longitude,
        latitude,
        city_id,
        CAST(? AS double),
        CAST(? AS double),
        CAST(1 AS bigint)
    ) AS distance
FROM
    store,
    unnest(store.sub_table)
WHERE
    MATCHINDEX('shop', ?)
    AND QUERY(name, ?)
```

```sql
dynamic_params:[[119.98844256998,\
                36.776817017143,\
                "excellect",\
                "水果 OR 西瓜"]]
```