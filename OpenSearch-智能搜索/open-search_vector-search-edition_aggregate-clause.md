### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[向量检索传统版（停售）](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-retrieval-general-edition/)[向量检索版文档3.9.0](https://help.aliyun.com/zh/open-search/vector-search-edition/documentation-of-vector-search-edition-v3-9/)[问天引擎Query DSL](https://help.aliyun.com/zh/open-search/vector-search-edition/query-dsl-of-opensearch-vector-search-edition/)[查询语法](https://help.aliyun.com/zh/open-search/vector-search-edition/query-syntax/)aggregate子句

# aggregate子句

更新时间：2024-02-27 22:04:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：sort子句](https://help.aliyun.com/zh/open-search/vector-search-edition/sort-clause)[下一篇：distinct子句](https://help.aliyun.com/zh/open-search/vector-search-edition/distinct-clause)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

子句说明

子句语法

注意事项

## 子句说明

一个关键词查询后可能会找到数以万计的文档，用户不太可能浏览所有的文档来获取自己需要的信息，有些情况下用户感兴趣的可能是一些统计的信息。

## 子句语法

```plain
aggregate=group_key:field, range:number1~number2, agg_fun:func1#func2, max_group:number2, agg_filter:filter_clause, max_group:number
```

- group\_key：必选参数。field为要进行统计的字段名，必须配置属性字段，字段类型必须是整形或者string。

- agg\_fun：必选参数。func可以为count()、sum(id)、max(id)、min(id)四种系统函数，含义分别为：文档个数、对ID字段求和、取ID字段最大值、取ID字段最小值；支持同时进行多个函数的统计，中间用英文井号（#）分隔；sum、max、min的内容支持基本的算术运算；

- range：表示分段统计，可用于分布统计，只支持单个range参数。表示number1~number2及大于number2的区间情况。不支持string类型的字段分布统计。

- agg\_filter：非必须参数，表示仅统计满足特定条件的文档；

- agg\_sampler\_threshold：非必须参数，抽样统计的阈值。表示该值之前的文档会依次统计，该值之后的文档会进行抽样统计；

- agg\_sampler\_step：非必须参数，抽样统计的步长。表示从agg\_sampler\_threshold后的文档将间隔agg\_sampler\_step个文档统计一次。对于sum和count类型的统计会把阈值后的抽样统计结果最后乘以步长进行估算，估算的结果再加上阈值前的统计结果就是最后的统计结果。

- max\_group：最大返回组数，默认为1000。


示例：

- 简单统计示例


```plain
aggregate=group_key:group_id,agg_fun:sum(price)
返回结果示例（只展示统计结果）：
{
　　result: {
　　　　facet: [\
　　　　　　{\
　　　　　　　　key: "group_id",\
　　　　　　　　items: [\
　　　　　　　　　　{\
　　　　　　　　　　　　value: 43,\
　　　　　　　　　　　　sum: 81\
　　　　　　　　　　},\
　　　　　　　　　　{\
　　　　　　　　　　　　value: 63,\
　　　　　　　　　　　　sum: 91\
　　　　　　　　　　}\
　　　　　　　　]\
　　　　　　}\
　　　　]
　　}
},
```

- 抽样统计


```plain
aggregate=group_key:company_id,agg_fun:count(),agg_sampler_threshold:5,agg_sampler_step:2

注：中抽样的阈值为5，步长为2，前5个命中的文档会依次统计，从第6个文档开始每隔1个文档进行抽样统计。对于sum和count类型的统计会把从第6个文档开始的抽样统计结果最后乘以步长进行估算，估算的结果再加上伐值前的统计结果就是最后的统计结果。
```

- 同时统计多项信息


```plain
aggregate=group_key:company_id,agg_fun:sum(id)#max(id)#min(id)
注：同时获取company_id中id之和，最大值及最小值，多个function函数之间用'#'拼接
```

- 多groupkey统计


```plain
aggregate=group_key:id,agg_fun:sum(price)&&aggregate=group_key:company_id,agg_fun:count(),agg_sampler_threshold:5, agg_sampler_step:2
注：可以支持多个统计子句，多个统计子句之间使用'&&'拼接
```

- 精确统计


```plain
config=cluster:general.default_agg&&aggregate=group_key:company_id,agg_fun:count()
注：指定cluster为clusterName连接'.default_agg'，表示开启精确统计，精确统计也是受限于rank_size，在rank_size范围之内是精确的。如果满足条件的文档个数远大于rank_size，大于的部分是不会参与统计的。
```

- 类精确统计


```plain
aggregate=group_key:company_id,agg_fun:distinct_count(brand)
注：如果统计函数为distinct_count，表示开启类精确统计（基于HLL算法），这种统计的精度损失通常在1%以内。
```

## 注意事项

- aggregate为非必选子句；

- 在aggregate中出现的字段必须在定义应用结构的时候配置为属性字段；

- aggregate结果会在搜索节点facet节点中展示出来，具体值字段名为agg\_fun的名字，如sum、count等

- aggregate支持多个key的统计，多个统计中间用英文分号（;）分隔。

- 该统计子句信息展示在facet 中，需设置config子句中的format 为fulljson 格式，才会返回并展示facet 对应内容。

- 受引擎性能影响，aggregate统计子句仅能保证10w的召回量下的文档数统计准确，超过10w的文档数统计不保证准确。