### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储 Tablestore](https://help.aliyun.com/zh/tablestore/) [开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/) [API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/) [DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/) GroupByFilter

# GroupByFilter

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GroupByHistogramItem](https://help.aliyun.com/zh/tablestore/developer-reference/groupbyhistogramitem)[下一篇：GroupByFilterResultItem](https://help.aliyun.com/zh/tablestore/developer-reference/groupbyfilterresultitem)

该文章对您有帮助吗？

反馈

在多元索引统计聚合中表示过滤条件分组，用于按照过滤条件对查询结果进行分组，获取每个过滤条件匹配到的数量，返回结果的顺序和添加过滤条件的顺序一致。

## **请求数据结构**

```protobuf
message GroupByFilter {
    repeated Query filters = 1;
    optional Aggregations sub_aggs = 2;
    optional GroupBys sub_group_bys = 3;
}
```

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **filters** | [Query](https://help.aliyun.com/zh/tablestore/developer-reference/query "") | 是 | 过滤条件，返回结果的顺序和添加过滤条件的顺序一致。 |
| **sub\_aggs** | [Aggregations](https://help.aliyun.com/zh/tablestore/developer-reference/aggregations "") | 否 | 子统计聚合Aggregation，子统计聚合会根据分组内容再进行一次统计聚合分析。 |
| **sub\_group\_bys** | [GroupBys](https://help.aliyun.com/zh/tablestore/developer-reference/groupbys "") | 否 | 子统计聚合GroupBy，子统计聚合会根据分组内容再进行一次统计聚合分析。 |

## **响应数据结构**

```protobuf
message GroupByFilterResult {
    repeated GroupByFilterResultItem group_by_filter_result_items = 1;
}
```

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **group\_by\_filter\_result\_items** | repeated [GroupByFilterResultItem](https://help.aliyun.com/zh/tablestore/developer-reference/groupbyfilterresultitem "") | 是 | 返回的分组信息。 |