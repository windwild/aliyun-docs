### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储 Tablestore](https://help.aliyun.com/zh/tablestore/) [开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/) [API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/) [API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/) [数据流Stream操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-data-stream-operations/) DescribeStream

# DescribeStream

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ListStream](https://help.aliyun.com/zh/tablestore/developer-reference/liststream)[下一篇：GetShardIterator](https://help.aliyun.com/zh/tablestore/developer-reference/getsharditerator)

该文章对您有帮助吗？

反馈

调用DescribeStream接口获取当前Stream的Shard信息。

## 注意事项

读取当前Shard的数据时需要确保父Shard的数据已经全部读取完毕。

## 请求消息结构

```protobuf
message DescribeStreamRequest {
    required string stream_id = 1;
    optional string inclusive_start_shard_id = 2;
    optional int32 shard_limit = 3;
    optional bool support_timeseries_data_table = 4;
}
```

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| stream\_id | string | 是 | 当前Stream的ID。 |
| inclusive\_start\_shard\_id | string | 否 | 查询起始Shard的ID。 |
| shard\_limit | int32 | 否 | 单次查询返回Shard数目的上限。 |
| support\_timeseries\_data\_table | bool | 否 | 当前操作的流所属的表是否为时序表。 |

## 响应消息结构

```protobuf
message DescribeStreamResponse {
    required string stream_id = 1;
    required int32 expiration_time = 2;
    required string table_name = 3;
    required int64 creation_time = 4;
    required StreamStatus stream_status = 5;
    repeated StreamShard shards = 6;
    optional string next_shard_id = 7;
    optional bool is_timeseries_data_table = 8;
}
```

|     |     |     |
| --- | --- | --- |
| **名称** | **类型** | **描述** |
| stream\_id | string | 当前Stream的ID。 |
| expiration\_time | int32 | Stream的过期时间。 |
| table\_name | string | 当前Stream所属的table名称。 |
| creation\_time | int64 | 当前Stream创建的时间。 |
| stream\_status | StreamStatus | 当前Stream的状态，包括enabling和active。 |
| shards | StreamShard | Streamshard的信息，包括Shard的ID，父Shard的ID和父Shard的邻居Shard信息。适用于父Shard发生merge。 |
| next\_shard\_id | string | 分页查询下一个Shard的起始ID。 |
| is\_timeseries\_data\_table | bool | 流相关联的表格是否为时间序列数据表。 |

## 使用SDK

[Java SDK：查询表Stream描述信息](https://help.aliyun.com/zh/tablestore/developer-reference/incremental-data-operations-by-using-java-sdk#section-buh-fai-jfc "")