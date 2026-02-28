### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)GroupByDateHistogramItem

# GroupByDateHistogramItem

更新时间：2024-04-08 22:09:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GroupByDateHistogram](https://help.aliyun.com/zh/tablestore/developer-reference/groupbydatehistogram)[下一篇：GeoPolygonQuery](https://help.aliyun.com/zh/tablestore/developer-reference/geopolygonquery)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

在日期直方图统计的返回结果中表示单个范围的分组信息。

## **数据结构**

```protobuf
message GroupByDateHistogramItem {
    optional int64 timestamp = 1;
    optional int64 row_count = 2;
    optional AggregationsResult sub_aggs_result = 3;
    optional GroupBysResult sub_group_bys_result = 4;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **timestamp** | int64 | 是 | 单个分组的时间戳。 |
| **row\_count** | int64 | 是 | 单个分组对应的总行数。 |
| **sub\_aggs\_result** | [AggregationsResult](https://help.aliyun.com/zh/tablestore/developer-reference/aggregationsresult "") | 否 | 子统计聚合SubAggregation的返回信息。 |
| **sub\_group\_bys\_result** | [GroupBysResult](https://help.aliyun.com/zh/tablestore/developer-reference/groupbysresult "") | 否 | 子统计聚合SubGroupBy的返回信息。 |