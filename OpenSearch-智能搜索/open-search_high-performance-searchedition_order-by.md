### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[SQL支持](https://help.aliyun.com/zh/open-search/high-performance-searchedition/sql-features/)[SQL查询语句语法](https://help.aliyun.com/zh/open-search/high-performance-searchedition/sql-query-syntax/)ORDER BY

# ORDER BY

更新时间：2025-04-09 04:39:49

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Grouping Sets](https://help.aliyun.com/zh/open-search/high-performance-searchedition/grouping-sets)[下一篇：UNION](https://help.aliyun.com/zh/open-search/high-performance-searchedition/union2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

语法格式

示例

用于对一个或者多个字段进行排序。默认为升序（ASC）。由于排序性能较差，要求排序时必须加上LIMIT子句。

## **语法格式**

```sql
select:
  SELECT [ DISTINCT ]
    { projectItem [, projectItem ]* }
  FROM tableExpression
    ORDER BY { orderByItem [ASC|DESC] [,OrderByItem ASC|DESC]* }
    LIMIT N
    OFFSET M
```

## **示例**

1. 简单排序：


```sql
SELECT nid, brand, price, size FROM phone ORDER BY price LIMIT 1000
```

2. 带升降排序标志的排序：


```sql
SELECT nid, brand, price, size FROM phone ORDER BY price ASC LIMIT 1000
```

3. 多字段排序：


```sql
SELECT nid, brand, price, size FROM phone ORDER BY size DESC, price DESC LIMIT 1000
```

4. 返回价格排序后第11到第20名的结果：


```sql
SELECT nid, brand, price, size FROM phone ORDER BY price DESC LIMIT 10 OFFSET 10
```

5. 不排序，随机返回10个商品：


```sql
SELECT nid, brand, price, size FROM phone LIMIT 10
```