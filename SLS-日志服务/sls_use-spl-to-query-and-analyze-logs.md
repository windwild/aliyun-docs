### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[扫描模式查询与分析（Scan）](https://help.aliyun.com/zh/sls/query-and-analyze-logs-in-scan-mode/)使用SPL查询和分析日志

# 使用SPL查询和分析日志

更新时间：2026-01-04 22:37:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：扫描（Scan）日志](https://help.aliyun.com/zh/sls/scan-logs)[下一篇：基于扫描索引加速扫描（Scan）](https://help.aliyun.com/zh/sls/accelerated-scan-based-on-scan-index)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

基本语法

日志样例

示例

按照不同条件进行过滤​

计算出新的字段

保留、移除、重命名字段​

展开非结构化数据

多级管道级联

索引模式SPL与扫描模式SPL的对比

操作方式

控制台

API

当您需要对日志数据进行结构化信息提取、字段操作和数据过滤时，可以通过使用 [SPL语言](https://help.aliyun.com/zh/sls/spl-overview/ "")（SLS Processing Language）来解决这些问题。另外，日志服务还提供多级管道级联功能，以便输出经过SPL处理的结果数据。

## **背景信息**

当SPL查询涉及到的字段都有字段索引（并开启统计）的时候，SPL会按照索引模式执行查询分析。如果SPL涉及的字段没有索引，会按照扫描（Scan）模式查询和分析。更多信息，请参见 [扫描（Scan）查询语法](https://help.aliyun.com/zh/sls/scan-query-syntax "")。

## 基本语法

扫描查询模式支持SPL（SLS Processing Language），更多信息请参见 [SPL语法](https://help.aliyun.com/zh/sls/spl-overview/ "")。对于读取出的原始数据，可以通过SPL语句做结构化信息提取、字段操作、数据过滤等操作，并支持多级管道级联，第一级管道是索引过滤条件，后面的多级管道是SPL指令，最终输出经过SPL处理后的结果数据。

```sql
索引查询语句 | <spl-cmd> ... | <spl-cmd> ...
```

## **日志样例**

- 原始字段： **标识 \[R\]**，适用于扫描搜索。

- 索引字段： **标识 \[I\]**，适用于索引搜索。


```plaintext
[I] __topic__: nginx-access-log
[I] Status: 200
[I] Host: api.abc.com
[R] Method: PUT
[R] ClientIp: 192.168.1.1
[R] Payload: {"Item": "1122", "UserId": "112233", "Operation": "AddCart"}
[R] BeginTime: 1705029260
[R] EndTime: 1705028561
[R] RT: 87
[R] Uri: /request/path-3/file-1
[R] UserAgent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_5; ar) AppleWebKit/533.19.4 (KHTML, like Gecko) Version/5.0.3 Safari/533.19.4
```

## **示例**

**说明**

1. SPL语句中的常量字符串使用单引号（'）包裹，比如 `* | where ClientIp = '192.168.1.1'`

2. 如果字段名称中有特殊符号，对字段名称使用双引号（"）包裹，比如 `* | project-away "user-agent"`


### **按照不同条件进行过滤** [**​**](https://sls.aliyun.com/doc/searchdemo/query/search_with_spl.html\#%E6%8C%89%E7%85%A7%E4%B8%8D%E5%90%8C%E6%9D%A1%E4%BB%B6%E8%BF%9B%E8%A1%8C%E8%BF%87%E6%BB%A4)

- 等值比较。















```sql
Status: 200 | where ClientIp = '192.168.1.1'
```

- 大小写不敏感搜索。















```sql
__topic__: nginx-access-log | where lower(Method) != 'put'
```

- 模糊匹配。















```sql
Status: 200 | where UserAgent like '%Macintosh%'
```

- 数值比较。

注意字段类型默认是varchar，进行数值比较时要先将类型转换成bigint。















```sql
Status: 200 |  where cast(RT as bigint) > 50
```

- 正则匹配。















```sql
# 找出包含"path-数字"的Uri
Status: 200 | where regexp_like(Uri, 'path-\d+')
```


### **计算出新的字段**

[​](https://sls.aliyun.com/doc/searchdemo/query/search_with_spl.html#%E6%8C%89%E7%85%A7%E4%B8%8D%E5%90%8C%E6%9D%A1%E4%BB%B6%E8%BF%9B%E8%A1%8C%E8%BF%87%E6%BB%A4) 通过 [extend指令](https://help.aliyun.com/zh/sls/spl-instructions-and-functions/#9e8791d074r7g "")，可以从已有的字段信息中，计算出新的字段。

- 从正则提取字段。















```sql
# 提取出Uri字段里的文件名编号
* not Status: 200 | extend fileNumber=regexp_extract(Uri, 'file-(\d+)', 1)
```

- 从JSON提取字段。















```sql
Status:200 | extend Item = json_extract_scalar(Payload, '$.Item')
```

- 按照分隔符提取。















```sql
Status:200 | extend urlParam=split_part(Uri, '/', 3)
```

- 根据多个字段值计算出新的字段。















```sql
#根据BeginTime和EndTime计算出时间差
Status:200 | extend timeRange = cast(BeginTime as bigint) - cast(EndTime as bigint)
```


### **保留、移除、重命名字段** [**​**](https://sls.aliyun.com/doc/searchdemo/query/search_with_spl.html\#%E6%8C%89%E7%85%A7%E4%B8%8D%E5%90%8C%E6%9D%A1%E4%BB%B6%E8%BF%9B%E8%A1%8C%E8%BF%87%E6%BB%A4)

- 仅保留某些字段（移除所有其他字段）。















```sql
Status:200 | project Status, Uri
```

- 移除某些字段（其它字段保留）。















```sql
Status:200 | project-away UserAgent
```

- 重命名字段。















```sql
Status:200 | project-rename Latency=RT
```


### **展开非结构化数据**

- 展开JSON中的所有字段。















```sql
#过滤Payload非空的，并且将所有的json字段展开
__topic__: nginx-access-log | where Payload is not null | parse-json Payload
```

- 将JSON字段展开，丢弃原有的JSON字段。















```sql
status:200
| parse-json body
| project-away body
```

- 正则提取出多个字段。















```sql
Status:200 | parse-regexp Uri, 'path-(\d+)/file-(\d+)' as pathIndex, fileIndex
```


### **多级管道级联**

以上示例中所有操作，都可以在同一个查询语句中，通过多级管道级联，执行顺序是从前往后依次执行。

```sql
Status:200
| where Payload is not null
| parse-json Payload
| project-away Payload
| where Host='api.qzzw.com' and cast(RT as bigint) > 80
| extend timeRange=cast(BeginTime as bigint) - cast(EndTime as bigint)
| where timeRange > 500
| project UserId, Uri
```

## 索引模式SPL与扫描模式SPL的对比

当SPL查询涉及到的字段都有字段索引（并开启统计）的时候，SPL会自动按照索引模式执行，否则按照扫描模式执行。

| **对比项** | **索引模式SPL** | **扫描模式SPL** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **对比项** | **索引模式SPL** | **扫描模式SPL** |
| 是否需要配置索引 | 需要SPL中涉及到的字段，开启字段索引并开启统计。 | 不需要。<br>**重要**<br>第一级竖线（\|）前的索引查询语句仍依赖于索引。 |
| 性能 | 强 | 一般 |
| 是否支持随机翻页 | 支持。 | 不支持。 |
| 日志直方图 | 基于查询语句的查询结果进行展示。 | 基于查询语句的查询结果、扫描进度进行展示。 |
| 运算符与函数 | 参考 [SPL指令与函数](https://help.aliyun.com/zh/sls/spl-instructions-and-functions/ "") 与 [SPL支持的SQL函数列表](https://help.aliyun.com/zh/sls/list-of-sql-functions "")。 | 参考 [SPL指令与函数](https://help.aliyun.com/zh/sls/spl-instructions-and-functions/ "") 与 [SPL支持的SQL函数列表](https://help.aliyun.com/zh/sls/list-of-sql-functions "")。 |
| 字段类型 | SPL语句中出现的字段均按照text类型处理。详情请参考 [数据类型转换](https://help.aliyun.com/zh/sls/spl-general-reference#8cdbc5f6bd7jt "")。 | SPL语句中出现的字段均按照text类型处理。详情请参考 [数据类型转换](https://help.aliyun.com/zh/sls/spl-general-reference#8cdbc5f6bd7jt "")。 |
| 结果集大小 | 通过控制台或SDK指定，最大100条。 | 满足下述任一条件，本次扫描结束并返回扫描结果。<br>- 达到您所指定的结果条数。<br>  <br>  您可以控制台或SDK指定返回的结果条数。<br>  <br>- 扫描超过了单次系统设定的最大条数（基于查询语句的结果集，默认10万条。）<br>  <br>- 扫描执行时间超过45秒。 |
| 费用 | 索引流量和索引存储费用。更多信息，请参见 [按使用功能计费模式计费项](https://help.aliyun.com/zh/sls/billable-items#concept-xzl-hjg-vgb "")。<br>SPL执行本身不产生额外费用。 | 扫描部分按照流量收费，即基于索引查询后扫描命中的数据量收费。 |

## **操作方式**

**重要**

在查询日志前，请确保您已采集到日志并创建索引。索引是一种存储结构，用于对日志数据中的一列或多列进行排序。更多信息，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#task-jqz-v55-cfb "")。

### **控制台**

登录[日志服务控制台](https://sls.console.aliyun.com/)，在目标LogStore的查询和分析页面执行查询操作。具体操作，请参见 [查询与分析快速指引](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis#task-tqc-ddm-gfb "")。

#### **示例**

原始日志为1000万条。查询语句：`Status:200 | where Category like '%xx%'`，满足`Status:200`且` where Category like '%xx%'`的日志1000条。查询结果界面中的直方图（histogram）展示了这1000条符合整个SPL语句条件的日志随时间变化的分布情况。

### **API**

通过 [GetLogs（返回结果不压缩后传输）](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-getlogs "")、 [GetLogsV2（返回结果压缩后传输）](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-getlogsv2 "") 接口执行查询操作。