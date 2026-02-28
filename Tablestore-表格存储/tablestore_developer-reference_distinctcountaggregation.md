### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)DistinctCountAggregation

# DistinctCountAggregation

更新时间：2024-04-08 03:18:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Direction](https://help.aliyun.com/zh/tablestore/developer-reference/direction)[下一篇：Error](https://help.aliyun.com/zh/tablestore/developer-reference/error)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求数据结构

响应数据结构

在多元索引统计聚合中表示去重统计行数，用于返回指定字段不同值的数量，类似于SQL中的`count（distinct）`。

## **请求数据结构**

```protobuf
message DistinctCountAggregation {
    optional string field_name = 1;
    optional bytes missing = 2;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **field\_name** | string | 是 | 用于统计聚合的字段。 |
| **missing** | bytes | 否 | 当某行数据中的字段为空时字段值的默认值，由Plainbuffer编码，详见 [Plainbuffer](https://help.aliyun.com/zh/tablestore/developer-reference/plainbuffer#reference3003 "") 编码。<br>- 如果未设置missing值，则在统计聚合时会忽略该行。<br>  <br>- 如果设置了missing值，则使用missing值作为字段值的默认值参与统计聚合。 |

## **响应数据结构**

```protobuf
message DistinctCountAggregationResult {
    optional int64 value = 1;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **value** | int64 | 是 | 返回值。 |