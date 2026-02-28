### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)SQL分析语法与功能

# SQL分析语法与功能

更新时间：2026-01-04 03:57:24

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

基础语法

SQL函数与SQL子句

示例1\. 查询昨天的日志

示例2\. 查看日志来源IP的分布情况

示例3\. 统计Nginx流入流出的流量

示例4\. 查看Nginx访问前十的地址

示例5\. 查看请求方法分类pv趋势

示例6\. 查看今日PV和昨日对比

示例7\. 预测Nginx访问日志的PV

示例8\. 统计HTTP\_USER\_AGENT并根据PV进行排序展示

示例9\. 分析Nginx日志错误请求占比

日志服务Project支持使用SQL语句对查询结果进行分析。本文介绍SQL分析语句基础语法。

## 基础语法

**说明**

[通过AI智能生成查询与分析语句（Copilot）](https://help.aliyun.com/zh/sls/copilot-automatic-generation-of-ai-assisted-sql-statements "")：日志服务提供AI智能辅助SQL语句的使用，支持自然语言生成SQL、解释复杂SQL、优化SQL语句。

查询语句和分析语句以`|`分割。其格式为：

```plaintext
查询语句|分析语句
```

查询语句可单独使用，分析语句必须与查询语句一起使用。即分析功能是基于查询结果或全量数据进行的。

**重要**

- 查询语句中建议不超过30个条件。

- 分析语句中不写FROM子句和WHERE子句时，默认分析当前LogStore中的数据。分析语句不支持使用offset，不区分大小写，末尾无需加分号。


| **语句类型** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **语句类型** | **说明** |
| 查询语句 | 查询条件，可以为关键词、数值、数值范围、空格、星号（\*）等。 <br>如果为空格或星号（\*），表示无过滤条件。 |
| 分析语句 | 对查询结果或全量数据进行计算和统计。日志服务支持的分析函数和语法，请参见：<br>- [SQL函数](https://help.aliyun.com/zh/sls/sql-function/ "")<br>  <br>- [SQL子句](https://help.aliyun.com/zh/sls/sql-syntax/ "")<br>  <br>- [嵌套子查询](https://help.aliyun.com/zh/sls/nested-subquery "")<br>  <br>- [Logstore和MySQL联合查询分析](https://help.aliyun.com/zh/sls/join-queries-on-a-logstore-and-a-mysql-database "") |

SQL分析语句示例：

```sql
* | SELECT status, count(*) AS PV GROUP BY status
```

## SQL函数与SQL子句

[SQL函数](https://help.aliyun.com/zh/sls/sql-function/ "") 通常用于对数据进行计算、转换和格式化。例如，计算总和、平均值、字符串操作、日期处理等。SQL函数通常嵌入在SQL子句中使用。

[SQL子句](https://help.aliyun.com/zh/sls/sql-syntax/ "") 用于构建完整的SQL查询或数据操作语句，决定数据的来源、条件、分组、排序等。

### **示例1\.** 查询昨天的日志

通过 [current\_date函数](https://help.aliyun.com/zh/sls/date-and-time-functions-1#title-haf-yb6-4po "") 返回当前日期。再使用 [date\_add函数](https://help.aliyun.com/zh/sls/date-and-time-functions-1#title-fmc-baq-7l8 "") 在当前日期中减去指定的时间间隔。通过表格进行展示，可以较为直观的看到这些数据。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
SELECT
    *
FROM  log
WHERE
    __time__ < to_unixtime(current_date)
    AND __time__ > to_unixtime(date_add('day', -1, current_date))
```

- 结果展示![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7734825371/p895315.png)


### **示例2\. 查看日志来源IP的分布情况**

通过 [ip\_to\_province函数](https://help.aliyun.com/zh/sls/ip-functions#title-vfw-dpo-y8k "") 得出ip对应的省地址，用`group by`对地址聚合，用 [count函数](https://help.aliyun.com/zh/sls/aggregate-function#title-9tl-8ms-d3x "") 计算出每个地址出现的次数。通过饼图进行展示。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
select
    count(1) as c,
    ip_to_province(remote_addr) as address
group by
    address
limit
    100
```

- 结果展示![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7734825371/p895306.png)


### **示例3\. 统计Nginx流入流出的流量**

通过 [date\_trunc函数](https://help.aliyun.com/zh/sls/date-and-time-functions-1#title-tz0-yz4-43k "") 将`__time__`对齐到小时（`__time__`为系统字段，日志采集的时间，默认为秒时间戳），用 [date\_format函数](https://help.aliyun.com/zh/sls/date-and-time-functions-1#title-y3f-fqi-d36 "") 将对齐的结果进行格式化，用`group by`将对齐的时间聚合，用 [sum函数](https://help.aliyun.com/zh/sls/aggregate-function#title-88h-pgn-zjm "") 计算出每小时流量合计，通过线图进行展示，X轴设置为`time`，左Y轴选择`net_out`和`net_in`。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
select
    sum(body_bytes_sent) as net_out,
    sum(request_length) as net_in,
    date_format(date_trunc('hour', __time__), '%m-%d %H:%i') as time
group by
    date_format(date_trunc('hour', __time__), '%m-%d %H:%i')
order by
    time
limit
    10000
```

- 结果展示

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7734825371/p895288.png)


### 示例4\. 查看Nginx访问前十的地址

通过 [split\_part函数](https://help.aliyun.com/zh/sls/string-functions-1#title-755-t6x-3iz "") 将`request_uri`按`?`分割成`array`，取分割后的第一个字符串，得出请求的路径。按这个路径`group by`进行聚合，用 [count函数](https://help.aliyun.com/zh/sls/aggregate-function#title-9tl-8ms-d3x "") 计算每个路径访问的次数，用`order by`对次数进行排序，desc表示顺序是从大到小，通过柱状图进行展示。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
select
    count(1) as pv,
    split_part(request_uri, '?', 1) as path
group by
    path
order by
    pv desc
limit
    10
```

- 结果展示

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7734825371/p895286.png)


### 示例5\. 查看请求方法分类pv趋势

使用 [date\_trunc函数](https://help.aliyun.com/zh/sls/date-and-time-functions-1#title-tz0-yz4-43k "") 将时间按照分钟对齐，然后与`request_method`一起分组聚合计算pv。然后按照时间继续排序， 使用流图展示，x轴为时间，y轴为pv，聚合列为`request_method`。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
select
    date_format(date_trunc('minute', __time__), '%m-%d %H:%i') as t,
    request_method,
    count(*) as pv
group by
    t,
    request_method
order by
    t asc
limit
    10000
```

- 结果展示

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7734825371/p895284.png)


### 示例6\. 查看今日PV和昨日对比

先通过count函数计算总的pv，再用compare函数得出今日的 pv 与昨日的同比。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=%2Flognext%2Fproject%2Fnginx-demo-log%2Flogsearch%2Fnginx-access-log%3Fencode%3Dbase64%26queryString%3DKiB8IHNlbGVjdCBkaWZmIFsxXSBhcyB0b2RheSwgcm91bmQoKGRpZmYgWzNdIC0xLjApICogMTAwLCAyKSBhcyBncm93dGggRlJPTSAoIFNFTEVDVCBjb21wYXJlKHB2LCA4NjQwMCkgYXMgZGlmZiBGUk9NICggU0VMRUNUIENPVU5UKDEpIGFzIHB2IEZST00gbG9nICkgKQ%3D%3D%26queryTimeType%3D6%26isShare%3Dtrue&maxWidth=true)）

- 查询与分析语句















```sql
* |
select
    diff [1] as today,
    round((diff [3] -1.0) * 100, 2) as growth
FROM
    (
      SELECT
        compare(pv, 86400) as diff
      FROM
        (
          SELECT
            COUNT(1) as pv
          FROM
            log
        )
    )
```

- 结果展示![image](<Base64-Image-Removed>)


### 示例7\. 预测Nginx访问日志的PV

`time - time % 60`（将time时间戳减去time时间戳对60的余数），得到按分钟对齐的时间`stamp`，用`group by`对`stamp`聚合，用 [count函数](https://help.aliyun.com/zh/sls/aggregate-function#title-9tl-8ms-d3x "") 计算每分钟的次数，将得到的结果作为一个子查询，用 [ts\_predicate\_simple函数](https://help.aliyun.com/zh/sls/prediction-and-anomaly-detection-functions#title-ezb-vsd-s63 "") 预测未来6个点的情况，查询结果按时序图进行展示。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
select
    ts_predicate_simple(stamp, value, 6)
from
    (
      select
        __time__ - __time__ % 60 as stamp,
        COUNT(1) as value
      from
        log
      GROUP BY
        stamp
      order by
        stamp
    )
LIMIT
    1000
```

- 结果展示

![image](<Base64-Image-Removed>)


### **示例8\. 统计** HTTP\_USER\_AGENT并根据PV **进行排序展示**

通过`http_user_agent`分组聚合，然后查询出各个代理的请求、以及返回客户端流量的和，由于单位是`byte`，使用 [round函数](https://help.aliyun.com/zh/sls/mathematical-calculation-functions#title-qza-f6e-ws1 "") 运算转为`MB`并保留两位小数。再使用`case when`为`status`分层，分为`2xx`、`3xx`、`4xx`、`5xx`以及各层所占的比例。 使用表格展示，可以较为直观的看到这些数据及含义。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
select
    http_user_agent as "用户代理",
    count(*) as pv,
    round(sum(request_length) / 1024.0 / 1024, 2) as "请求报文流量(MB)",
    round(sum(body_bytes_sent) / 1024.0 / 1024, 2) as "返回客户端流量(MB)",
    round(
      sum(
        case
          when status >= 200
          and status < 300 then 1
          else 0
        end
      ) * 100.0 / count(1),
      6
    ) as "2xx比例(%)",
    round(
      sum(
        case
          when status >= 300
          and status < 400 then 1
          else 0
        end
      ) * 100.0 / count(1),
      6
    ) as "3xx比例(%)",
    round(
      sum(
        case
          when status >= 400
          and status < 500 then 1
          else 0
        end
      ) * 100.0 / count(1),
      6
    ) as "4xx比例(%)",
    round(
      sum(
        case
          when status >= 500
          and status < 600 then 1
          else 0
        end
      ) * 100.0 / count(1),
      6
    ) as "5xx比例(%)"
group by
    "用户代理"
order by
    pv desc
limit
    100
```

- 结果展示![image](<Base64-Image-Removed>)


### 示例9\. 分析Nginx日志错误请求占比

先在SQL内部获取到请求status超过400的错误请求数量，以及总的请求数量，然后再外部计算比值， 展示时使用统计图。（ [试用 Demo](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKiB8DQpTRUxFQ1QNCiAgKg0KRlJPTSAgbG9nDQpXSEVSRQ0KICBfX3RpbWVfXyA8IHRvX3VuaXh0aW1lKGN1cnJlbnRfZGF0ZSkNCiAgQU5EIF9fdGltZV9fID4gdG9fdW5peHRpbWUoZGF0ZV9hZGQoJ2RheScsIC0xLCBjdXJyZW50X2RhdGUpKQ%3D%3D)）

- 查询与分析语句















```sql
* |
select
    round((errorCount * 100.0 / totalCount), 2) as errorRatio
from
    (
      select
        sum(
          case
            when status >= 400 then 1
            else 0
          end
        ) as errorCount,
        count(1) as totalCount
      from
        log
    )
```

- 结果展示![image](<Base64-Image-Removed>)