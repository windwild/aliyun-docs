### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[多元索引操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-search-index-operations/)DescribeSearchIndex

# DescribeSearchIndex

更新时间：2024-04-09 04:22:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ListSearchIndex](https://help.aliyun.com/zh/tablestore/developer-reference/listsearchindex)[下一篇：DeleteSearchIndex](https://help.aliyun.com/zh/tablestore/developer-reference/deletesearchindex)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

调用DescribeSearchIndex接口查询多元索引描述信息，包括多元索引的字段信息和索引配置等。

## **请求消息结构**

```protobuf
message DescribeSearchIndexRequest {
    optional string table_name = 1;
    optional string index_name = 2;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **table\_name** | string | 否 | 数据表名称。 |
| **index\_name** | string | 否 | 多元索引名称。 |

## **响应消息结构**

```protobuf
message DescribeSearchIndexResponse {
    optional IndexSchema schema = 1;
    optional SyncStat sync_stat = 2;
    optional MeteringInfo metering_info = 3;
    optional string brother_index_name = 4;
    repeated QueryFlowWeight query_flow_weight = 5;
    optional int64 create_time = 6;
    optional int32 time_to_live = 7;  // unit is seconds
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **schema** | [IndexSchema](https://help.aliyun.com/zh/tablestore/developer-reference/indexschema "") | 是 | 索引Schema信息。 |
| **sync\_stat** | [SyncStat](https://help.aliyun.com/zh/tablestore/developer-reference/syncstat "") | 否 | 同步状态，包括同步阶段以及当前同步阶段的时间。 |
| **metering\_info** | [MeteringInfo](https://help.aliyun.com/zh/tablestore/developer-reference/meteringinfo "") | 是 | 计量信息，包括存储量大小、行数、预留读吞吐量和时间。 |
| **brother\_index\_name** | string | 否 | 灰度索引的名称。当使用动态修改schema功能更新多元索引结构时才会返回此参数。 |
| **query\_flow\_weight** | repeated [QueryFlowWeight](https://help.aliyun.com/zh/tablestore/developer-reference/queryflowweight "") | 否 | 查询权重配置。当使用动态修改schema功能更新多元索引结构时才会返回此参数。 |
| **create\_time** | int64 | 是 | 多元索引的创建时间。格式为64位的毫秒单位时间戳。 |
| **time\_to\_live** | int32 | 是 | 多元索引生命周期，即数据的保存时间。单位为秒。<br>当数据的保存时间超过设置的数据生命周期时，系统会自动清理超过数据生命周期的数据。 |

## **使用SDK**

您可以使用如下语言的SDK查询多元索引描述信息。

- [Java SDK：查询多元索引描述信息](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-description-of-a-search-index-3#concept-thd-r2s-dgb "")

- [Go SDK：查询多元索引描述信息](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-description-of-a-search-index-by-using-go-sdk#concept-ajd-c45-hgb "")

- [Python SDK：查询多元索引描述信息](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-description-of-a-search-index-by-using-python-sdk#concept-k4f-d1k-pgb "")

- [Node.js SDK查询多元索引描述信息](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-description-of-a-search-index-by-using-nodejs-sdk#concept-k5h-rvk-2gb "")

- [.NET SDK：查询多元索引描述信息](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-description-of-a-search-index-by-using-net-sdk#concept-qhr-1qc-fgb "")

- [PHP SDK：查询多元索引描述信息](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-description-of-a-search-index-by-using-php-sdk#concept-473397 "")