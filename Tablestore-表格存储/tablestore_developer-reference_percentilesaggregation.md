### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)PercentilesAggregation

# PercentilesAggregation

更新时间：2024-03-21 05:34:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：NestedQuery](https://help.aliyun.com/zh/tablestore/developer-reference/nestedquery)[下一篇：PercentilesAggregationItem](https://help.aliyun.com/zh/tablestore/developer-reference/percentilesaggregationitem)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求数据结构

响应数据消息

在多元索引统计聚合中表示百分位统计，百分位统计常用来统计一组数据的百分位分布情况，例如在日常系统运维中统计每次请求访问的耗时情况时，需要关注系统请求耗时的P25、P50、P90、P99值等分布情况。

## **请求数据结构**

```protobuf
message PercentilesAggregation {
    optional string field_name = 1;
    repeated double percentiles = 2;
    optional bytes missing = 3;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **field\_name** | string | 是 | 用于统计聚合的字段。 |
| **percentiles** | double | 是 | 百分位分布例如50、90、99，可根据需要设置一个或者多个百分位。多个百分位之间用半角逗号（,）分隔，例如`25.0,50.0,99.0`。<br>单个百分位的取值范围为1~100的数字。 |
| **missing** | bytes | 否 | 当某行数据中的字段为空时字段值的默认值，由Plainbuffer编码，详见 [Plainbuffer](https://help.aliyun.com/zh/tablestore/developer-reference/plainbuffer#reference3003 "") 编码。<br>- 如果未设置missing值，则在统计聚合时会忽略该行。<br>  <br>- 如果设置了missing值，则使用missing值作为字段值的默认值参与统计聚合。 |

## **响应数据消息**

```protobuf
message PercentilesAggregationResult {
    repeated PercentilesAggregationItem percentiles_aggregation_items = 1;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **percentiles\_aggregation\_items** | repeated [PercentilesAggregationItem](https://help.aliyun.com/zh/tablestore/developer-reference/percentilesaggregationitem "") | 是 | 百分位统计中百分位分布信息。 |