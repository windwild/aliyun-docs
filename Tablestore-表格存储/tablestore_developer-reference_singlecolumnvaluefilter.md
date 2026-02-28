### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)SingleColumnValueFilter

# SingleColumnValueFilter

更新时间：2024-08-22 23:06:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SortOrder](https://help.aliyun.com/zh/tablestore/developer-reference/sortorder)[下一篇：SingleWordAnalyzerParameter](https://help.aliyun.com/zh/tablestore/developer-reference/singlewordanalyzerparameter)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

相关操作

单个条件，例如`column_a>5`等，适用于ConditionUpdate（条件更新）和Filter（过滤器）功能。

## 数据结构

```protobuf
message SingleColumnValueFilter {
    required ComparatorType comparator = 1;
    required string column_name = 2;
    required bytes column_value = 3;
    required bool filter_if_missing = 4;
    required bool latest_version_only = 5;
    optional ValueTransferRule value_transfer_rule =6;

}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| comparator | [ComparatorType](https://help.aliyun.com/zh/tablestore/developer-reference/comparatortype#reference455 "") | 是 | 关系运算符。 |
| column\_name | string | 是 | 列名称。 |
| column\_value | bytes | 是 | 列值经过 [Plainbuffer](https://help.aliyun.com/zh/tablestore/developer-reference/plainbuffer#reference3003 "") 编码后的值。 |
| filter\_if\_missing | bool | 是 | 当某行的该列不存在时，设置条件是否过滤。 |
| latest\_version\_only | bool | 是 | 是否只对最新版本有效。取值范围如下：<br>- true（默认）：只检测最新版本的值是否满足条件。<br>  <br>- false：检测所有版本的值是否满足条件。 |
| value\_transfer\_rule | [ValueTransferRule](https://help.aliyun.com/zh/tablestore/developer-reference/valuetransferrule#reference-2089868 "") | 否 | 使用正则表达式匹配到字符串后，将字符串转换为String、Integer或者Double类型。<br>当某些列中存储了自定义格式数据（例如JSON格式字符串）时，如果用户希望通过某个子字段值来过滤查询该列数据，则需要设置此参数。 |

## 相关操作

- 条件更新： [PutRow](https://help.aliyun.com/zh/tablestore/developer-reference/putrow#reference1838 "")、 [UpdateRow](https://help.aliyun.com/zh/tablestore/developer-reference/updaterow#reference2046 "")、 [DeleteRow](https://help.aliyun.com/zh/tablestore/developer-reference/deleterow#reference1493 "")、 [BatchWriteRow](https://help.aliyun.com/zh/tablestore/developer-reference/batchwriterow#reference1996 "")

- 过滤器： [GetRow](https://help.aliyun.com/zh/tablestore/developer-reference/getrow#reference-oty-2q3-bfb "")、 [GetRange](https://help.aliyun.com/zh/tablestore/developer-reference/getrange#reference3923 "")、 [BatchGetRow](https://help.aliyun.com/zh/tablestore/developer-reference/batchgetrow#reference1686 "")