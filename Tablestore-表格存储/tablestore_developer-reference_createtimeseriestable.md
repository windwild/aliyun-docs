### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[时序表操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-timeseries-table-operations/)CreateTimeseriesTable

# CreateTimeseriesTable

更新时间：2025-04-03 03:09:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：时序表操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-timeseries-table-operations/)[下一篇：ListTimeseriesTable](https://help.aliyun.com/zh/tablestore/developer-reference/listtimeseriestable)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

调用CreateTimeseriesTable接口以创建时序表。在创建时序表时，您可以同时创建一个分析存储，以便低成本地存储时序数据并进行查询与分析。此外，您还可以同时创建Lastpoint索引用于快速获取时间线最新时间点的时序数据。

## 请求消息结构

```protobuf
message CreateTimeseriesTableRequest {
  required TimeseriesTableMeta table_meta = 1;
  repeated TimeseriesAnalyticalStore analytical_stores = 3;
  optional bool enable_analytical_store = 4;
  repeated LastpointIndexMetaForCreate lastpoint_index_metas = 5;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| table\_meta | [TimeseriesTableMeta](https://help.aliyun.com/zh/tablestore/developer-reference/timeseriestablemeta#reference-2125566 "") | 是 | 时序表的配置信息。 |
| analytical\_stores | [TimeseriesAnalyticalStore](https://help.aliyun.com/zh/tablestore/developer-reference/timeseries-analyticalstore "") | 否 | 创建分析存储的配置信息。 |
| enable\_analytical\_store | bool | 否 | 是否创建默认分析存储。默认值为true。 |
| lastpoint\_index\_metas | [LastpointIndexMetaForCreate](https://help.aliyun.com/zh/tablestore/developer-reference/lastpointindexmetaforcreate "") | 否 | Lastpoint索引配置。 |

## 响应消息结构

```protobuf
message CreateTimeseriesTableResponse {
}
```

## 使用SDK

您可以使用如下语言的SDK创建时序表。

- [Java SDK：创建时序表](https://help.aliyun.com/zh/tablestore/developer-reference/create-a-time-series-table-by-using-java-sdk#concept-2126662 "")

- [Go SDK：创建时序表](https://help.aliyun.com/zh/tablestore/developer-reference/create-a-time-series-table-by-using-go-sdk#concept-2126662 "")

- [Python SDK：创建时序表](https://help.aliyun.com/zh/tablestore/developer-reference/create-a-time-series-table-by-python-sdk "")