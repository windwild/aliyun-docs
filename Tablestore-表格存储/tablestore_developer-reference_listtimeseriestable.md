### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[时序表操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-timeseries-table-operations/)ListTimeseriesTable

# ListTimeseriesTable

更新时间：2025-04-03 03:09:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CreateTimeseriesTable](https://help.aliyun.com/zh/tablestore/developer-reference/createtimeseriestable)[下一篇：DescribeTimeseriesTable](https://help.aliyun.com/zh/tablestore/developer-reference/describetimeseriestable)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

调用ListTimeseriesTable接口以获取当前实例下时序表的名称及其配置信息。

## 请求消息结构

```protobuf
message ListTimeseriesTableRequest {
}
```

## 响应消息结构

```protobuf
message ListTimeseriesTableResponse {
  repeated TimeseriesTableMeta table_metas = 1;
}
```

| **名称** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **类型** | **描述** |
| table\_metas | [TimeseriesTableMeta](https://help.aliyun.com/zh/tablestore/developer-reference/timeseriestablemeta#reference-2125566 "") | 所有时序表的配置信息。 |

## 使用SDK

您可以使用如下语言的SDK列出时序表。

- [Java SDK：列出时序表](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-names-of-time-series-tables-by-using-java-sdk#concept-2126666 "")

- [Go SDK：列出时序表](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-names-of-time-series-tables-by-using-go-sdk#concept-2126666 "")

- [Python SDK：列出时序表](https://help.aliyun.com/zh/tablestore/developer-reference/query-the-names-of-time-series-tables-by-python-sdk "")