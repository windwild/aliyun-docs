### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/) [查询与分析](https://help.aliyun.com/zh/sls/index-and-query/) [查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/) [SQL分析语法与功能](https://help.aliyun.com/zh/sls/sql-syntax-and-functions/) [SQL子句](https://help.aliyun.com/zh/sls/sql-syntax/) UNNEST子句

# UNNEST子句

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：UNION子句](https://help.aliyun.com/zh/sls/union-clause)[下一篇：VALUES子句](https://help.aliyun.com/zh/sls/values-clause)

该文章对您有帮助吗？

反馈

在复杂的业务场景下，日志字段的值可能为数组（array）、对象（map）等类型。对这种特殊类型的日志字段进行查询和分析时，您可以先使用UNNEST子句将字段值展开。

## 语法

- 将array类型的数据展开为多行单列形式，列名为_column\_name_。


```plaintext
UNNEST(x) AS table_alias(column_name)
```

- 将map类型的数据展开为多行多列形式，列名为_key\_name_和_value\_name_。


```plaintext
UNNEST(y) AS table(key_name,value_name)
```


**重要**

UNNEST子句处理的是array或者map类型的数据。如果您输入的数据为字符串类型，则需要先转化为JSON类型，然后再转化为array类型或map类型，转化方法为`try_cast(json_parse(array_column) as array(bigint))`。更多信息，请参见 [类型转换函数](https://help.aliyun.com/zh/sls/data-type-conversion-functions#concept-v55-4lq-zdb "")。

## 参数说明

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 数据类型为array类型。 |
| _column\_name_ | 将array类型的数据展开后，指定一个列名。该列用于存放array中的元素。 |
| _y_ | 数据类型为map类型。 |
| _key\_name_ | 将map类型的数据展开后，指定一个列名。该列用于存放map中的键。 |
| _value\_name_ | 将map类型的数据展开后，指定一个列名。该列用于存放map中的键值。 |

## 示例

### 示例1

将number字段的值（array类型）展开为多行单列形式。

- 字段样例


```plaintext
number:[49, 50, 45, 47, 50]
```

- 查询和分析语句


```plaintext
* |
SELECT
    a
FROM  log,
    UNNEST(cast(json_parse(number) AS array(bigint))) AS t(a)
```

- 查询和分析结果![unnest](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2216692361/p335777.png)


### 示例2

将number字段的值（array类型）展开为多行单列形式，并进行求和计算。

- 字段样例

此处仅提供一条日志样例，求和计算是针对所有日志，即对所有日志中的number字段的值进行求和。


```plaintext
number:[49, 50, 45, 47, 50]
```

- 查询和分析语句


```plaintext
* |
SELECT
    sum(a) AS sum
FROM  log,
    UNNEST(cast(json_parse(number) as array(bigint))) AS t(a)
```

- 查询和分析结果![unnest](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2216692361/p335783.png)


### 示例3

将number字段的值（array类型）展开为多行单列形式，并对各个值进行分组统计。

- 字段样例


```plaintext
number:[49, 50, 45, 47, 50]
```

- 查询和分析语句


```plaintext
* |
SELECT
    a, count(*) AS count
FROM  log,
    UNNEST(cast(json_parse(number) as array(bigint))) AS t(a) GROUP BY a
```

- 查询和分析结果![unnest](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3170792361/p335842.png)


### 示例4

将number字段的值（map类型）展开为多行多列形式。

- 字段样例


```plaintext
result:{
    anomaly_type:"OverThreshold"
    dim_name:"request_time"
    is_anomaly:true
    score:1
    value:"3.000000"}
```

- 查询和分析语句


```plaintext
* |
select
    key,
    value
FROM  log,
    UNNEST(
      try_cast(json_parse(result) as map(varchar, varchar))
    ) AS t(key, value)
```

- 查询和分析结果![unnest](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3170792361/p335844.png)


### 示例5

将number字段的值（map类型）展开为多行多列形式，并对各个键进行分组统计。

- 字段样例


```plaintext
result:{
    anomaly_type:"OverThreshold"
    dim_name:"request_time"
    is_anomaly:true
    score:1
    value:"3.000000"}
```

- 查询和分析语句


```plaintext
* |
select
    key,
    count(*) AS count
FROM  log,
    UNNEST(
      try_cast(json_parse(result) as map(varchar, varchar))
    ) AS t(key, value)
GROUP BY
    key
```

- 查询和分析结果![unnest](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3170792361/p335847.png)


### 示例6

使用histogram函数获取各个请求方法对应的请求数量，返回结果为map类型。然后通过unnest子句将histogram函数的返回结果展开为多行多列形式，并通过柱状图展示。

- 查询和分析语句


```plaintext
* |
SELECT
    key,
    value
FROM(
      SELECT
        histogram(request_method) AS result
      FROM      log
    ),
    UNNEST(result) AS t(key, value)
```

- 查询和分析结果![unnest](<Base64-Image-Removed>)