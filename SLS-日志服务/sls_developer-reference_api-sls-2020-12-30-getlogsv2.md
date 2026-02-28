### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[开发参考](https://help.aliyun.com/zh/sls/developer-reference/)[API参考](https://help.aliyun.com/zh/sls/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-dir/)[日志库](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-dir-logstore/)GetLogsV2 - 查询Logstore中的日志数据

# GetLogsV2 - 查询Logstore中的日志数据

更新时间：2026-02-09 03:10:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetCursorTime - 通过Cursor查询服务器端时间](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-getcursortime)[下一篇：PullLogs - 拉取日志](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-pulllogs)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

接口说明

鉴权资源

调试

授权信息

请求语法

路径参数

请求参数

返回参数

示例

错误码

变更历史

查询指定Project下某个Logstore中的原始日志数据，返回结果显示某时间区间中的原始日志（返回结果压缩后传输）。

## 接口说明

- 日志服务 SDK 目前仅支持 Go、Java、Python 三种语言，OpenAPI 全部已支持。

- 使用过程中注意指定压缩方法，不同语言实现的压缩算法不同，详情参考入参 Accept-Encoding。

- 更多相关说明请参见 [GetLogs](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-getlogs) 。


### 鉴权资源

下表列出了 API 对应的授权信息。您可以在 RAM 权限策略语句的 Action 元素中添加该信息，用于为 RAM 用户或 RAM 角色授予调用此 API 的权限。

| 动作（Action） | 授权策略中的资源描述方式（Resource） |
| :-- | :-- |

|     |     |
| --- | --- |
| 动作（Action） | 授权策略中的资源描述方式（Resource） |
| `log:GetLogStoreLogs` | `acs:log:{#regionId}:{#accountId}:project/{#ProjectName}` |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/Sls/2020-12-30/GetLogsV2)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)\\
调试](https://api.aliyun.com/api/Sls/2020-12-30/GetLogsV2)

## **授权信息**

当前API暂无授权信息透出。

## 请求语法

```plaintext
POST /logstores/{logstore}/logs HTTP/1.1
```

## 路径参数

| **名称** | **类型** | **必填** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **必填** | **描述** | **示例值** |
| logstore | string | 是 | logstore 名称。 | test-logstore |

## 请求参数

| **名称** | **类型** | **必填** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **必填** | **描述** | **示例值** |
| project | string | 是 | project 名称。 | ali-test-project |
| Accept-Encoding | string | 是 | 压缩方式<br>- Java、Python、Go 目前支持 lz4 、gzip 解压缩<br>  <br>- php、Js、C#目前仅支持 gzip 解压缩<br>  <br>**枚举值：**<br>- lz4 : <br>  <br>lz4<br>  <br>- gzip : <br>  <br>gzip | lz4 |
| body | object | 否 | 请求结构体。 |  |
| from | integer | 是 | 查询开始时间点。该时间是指写入日志数据时指定的日志时间。<br>请求参数 from 和 to 定义的时间区间遵循左闭右开原则，即该时间区间包括区间开始时间点，但不包括区间结束时间点。如果 from 和 to 的值相同，则为无效区间，函数直接返回错误。<br>Unix 时间戳格式，表示从 1970-1-1 00:00:00 UTC 计算起的秒数。 | 1627268185 |
| to | integer | 是 | 查询结束时间点。该时间是指写入日志数据时指定的日志时间。<br>请求参数 from 和 to 定义的时间区间遵循左闭右开原则，即该时间区间包括区间开始时间点，但不包括区间结束时间点。如果 from 和 to 的值相同，则为无效区间，函数直接返回错误。<br>Unix 时间戳格式，表示从 1970-1-1 00:00:00 UTC 计算起的秒数。 | 1627268185 |
| line | integer | 否 | 仅当 query 参数为查询语句时，该参数有效，表示请求返回的最大日志条数。最小值为 0，最大值为 100，默认值为 100。 | 100 |
| offset | integer | 否 | 仅当 query 参数为查询语句时，该参数有效，表示查询开始行。默认值为 0。 | 0 |
| reverse | boolean | 否 | 用于指定返回结果是否按日志时间戳降序返回日志，精确到分钟级别。<br>true：按照日志时间戳降序返回日志。<br>false（默认值）：按照日志时间戳升序返回日志。<br>注意<br>当 query 参数为查询语句时，参数 reverse 有效，用于指定返回日志排序方式。<br>当 query 参数为查询和分析语句时，参数 reverse 无效，由 SQL 分析语句中 order by 语法指定排序方式。如果 order by 为 asc（默认），则为升序；如果 order by 为 desc，则为降序。 | false |
| powerSql | boolean | 否 | 是否开启增强 sql，默认关闭。 | false |
| session | string | 否 | 查询参数 | mode=scan |
| topic | string | 否 | 日志主题。默认值为双引号（""）。 | "" |
| query | string | 否 | 查询语句或者分析语句。更多信息，请参见 [查询概述](https://help.aliyun.com/zh/sls/log-search-overview) 和 [分析概述](https://help.aliyun.com/zh/sls/log-analysis-overview)。<br>在 query 参数的分析语句中加上 set session parallel\_sql=true;，表示使用 SQL 独享版。例如\* \| set session parallel\_sql=true; select count(\*) as pv 。<br>说明当 query 参数中有分析语句（SQL 语句）时，该接口的 line 参数和 offset 参数无效，建议设置为 0，需通过 SQL 语句的 LIMIT 语法实现翻页。更多信息，请参见分页显示查询分析结果。 | status: 401 \| SELECT remote\_addr,COUNT(\*) as pv GROUP by remote\_addr ORDER by pv desc limit 5 |
| forward | boolean | 否 | scan 或短语查询表示是否向前或向后翻页 | false |
| highlight | boolean | 否 | 是否高亮 | false |
| isAccurate | boolean | 否 | 是否开启纳秒级有序 | true |

## **返回参数**

| **名称** | **类型** | **描述** | **示例值** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **描述** | **示例值** |
|  | object | 返回数据 |  |
| meta | object | 返回数据 meta 信息 |  |
| progress | string | 查询的结果是否完整。<br>- Complete：查询已经完成，返回结果为完整结果。<br>  <br>- Incomplete：查询已经完成，返回结果为不完整结果，需要重复请求以获得完整结果。 | Complete |
| aggQuery | string | 查询语句中 \| 之后的 SQL 部分 | select \* |
| whereQuery | string | 查询语句中 \| 之前的部分 | \* |
| hasSQL | boolean | 是否 sql 查询 | false |
| processedRows | integer | 本次查询处理的行数。 | 10000 |
| elapsedMillisecond | integer | 本次查询消耗的毫秒时间。 | 5 |
| cpuSec | number | 独享 SQL 的核时 | 0.002 |
| cpuCores | integer | 使用 cpu 核数 | 3 |
| keys | array | 查询结果中所有的 key |  |
|  | string | key | key |
| terms | array<object> | 查询语句中所有的词 |  |
|  | object | 词 | {term=\*, key=} |
| limited | integer | 限制条数，sql 不带 limit 会返回 | 100 |
| mode | integer | 查询模式枚举<br>0: 普通查询（包括 sql）<br>1: 短语查询<br>2: SCAN 扫描<br>3: SCAN SQL | 0 |
| phraseQueryInfo | object | 短语查询 |  |
| scanAll | boolean | 是否已经扫描了全部日志 | true |
| beginOffset | integer | 本次扫描结果对应的索引过滤后的起始 offset | 0 |
| endOffset | integer | 本次扫描结果对应的索引过滤后的结束 offset | 0 |
| endTime | integer | 本次扫描结果对应的索引过滤后的最后时间 | 1 |
| scanBytes | integer | scan 时返回扫描的数据量（字节）。 | 1024 |
| highlights | array | 高亮内容 |  |
|  | array | 高亮内容 |  |
|  | [LogContent](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-struct-logcontent) | 高亮日志内容 |  |
| count | integer | 本次查询请求返回的日志行数。 | 1 |
| processedBytes | integer | 查询处理日志量 | 10000 |
| isAccurate | boolean | 是否开启纳秒级有序 | true |
| columnTypes | array | 列类型 |  |
|  | string | 类型 | long |
| telementryType | string | 可观测数据类型 | None |
| data | array<object> | 返回结果。 |  |
|  | object | 返回的数据。 |  |
|  | string | 返回数据。 | {'remote\_addr': '198.51.XXX.XXX', 'pv': '1', '\_\_source\_\_': '', '\_\_time\_\_': '1649902984'} |

## 示例

正常返回示例

`JSON`格式

```json
{
  "meta": {
    "progress": "Complete",
    "aggQuery": "select *",
    "whereQuery": "*",
    "hasSQL": false,
    "processedRows": 10000,
    "elapsedMillisecond": 5,
    "cpuSec": 0.002,
    "cpuCores": 3,
    "keys": [\
      "key"\
    ],
    "terms": [\
      {\
        "test": "test",\
        "test2": 1\
      }\
    ],
    "limited": 100,
    "mode": 0,
    "phraseQueryInfo": {
      "scanAll": true,
      "beginOffset": 0,
      "endOffset": 0,
      "endTime": 1
    },
    "scanBytes": 1024,
    "highlights": [\
      [\
        {\
          "Key": "key-test",\
          "Value": "value-test"\
        }\
      ]\
    ],
    "count": 1,
    "processedBytes": 10000,
    "isAccurate": true,
    "columnTypes": [\
      "long"\
    ],
    "telementryType": "None"
  },
  "data": [\
    {\
      "key": "{'remote_addr': '198.51.XXX.XXX', 'pv': '1', '__source__': '', '__time__': '1649902984'}"\
    }\
  ]
}
```

## 错误码

访问[错误中心](https://api.aliyun.com/document/Sls/2020-12-30/errorCode)查看更多错误码。

## **变更历史**

更多信息，参考[变更详情](https://api.aliyun.com/document/Sls/2020-12-30/GetLogsV2#workbench-doc-change-demo)。