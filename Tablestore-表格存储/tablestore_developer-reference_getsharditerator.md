### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[数据流Stream操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-data-stream-operations/)GetShardIterator

# GetShardIterator

更新时间：2024-07-22 22:52:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DescribeStream](https://help.aliyun.com/zh/tablestore/developer-reference/describestream)[下一篇：GetStreamRecord](https://help.aliyun.com/zh/tablestore/developer-reference/getstreamrecord)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

调用GetShardIterator接口获取读取当前Shard记录的起始iterator。

## 请求消息结构

```protobuf
message GetShardIteratorRequest {
    required string stream_id = 1;
    required string shard_id = 2;
    optional int64 timestamp = 3;
    optional string token = 4;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| stream\_id | string | 是 | 当前Stream的ID。 |
| shard\_id | string | 是 | 当前Shard的ID。 |
| timestamp | int64 | 否 | 根据时间获取ShardIterator，时间单位us。 |
| token | string | 否 | 用于分页获取。 |

## 响应消息结构

```protobuf
message GetShardIteratorResponse {
    required string shard_iterator = 1;
    optional string next_token = 2;
}
```

| **名称** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **类型** | **描述** |
| shard\_iterator | string | 读取当前Shard记录的起始iterator。 |
| next\_token | string | 获取分片迭代器响应中指示下一个迭代器的标识符。 |

## 使用SDK

[Java SDK：获取Shard的读取迭代值](https://help.aliyun.com/zh/tablestore/developer-reference/incremental-data-operations-by-using-java-sdk#section-ckk-xoi-t4s "")