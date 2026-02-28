### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[时序数据操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-timeseries-data-operations/)DeleteTimeseriesMeta

# DeleteTimeseriesMeta

更新时间：2025-05-25 23:05:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：QueryTimeseriesMeta](https://help.aliyun.com/zh/tablestore/developer-reference/querytimeseriesmeta)[下一篇：SplitTimeseriesScanTask](https://help.aliyun.com/zh/tablestore/developer-reference/splittimeseriesscantask)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

调用DeleteTimeseriesMeta接口删除时间线元数据。

## 请求消息结构

```protobuf
message DeleteTimeseriesMetaRequest {
  required string table_name = 1;
  repeated TimeseriesKey timeseries_key = 2;
  optional int64 supported_table_version = 3;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| table\_name | string | 是 | 时序表名称。 |
| timeseries\_key | [TimeseriesKey](https://help.aliyun.com/zh/tablestore/developer-reference/timeserieskey#reference-2126563 "") | 是 | 要删除的时间线标识。 |
| supported\_table\_version | int64 | 否 | SDK中支持的时序表模型版本号。取值范围如下：<br>- 0（默认）：不支持包含 [**自定义时间线标识或作为主键的数据字段**](https://help.aliyun.com/zh/tablestore/customize-timeseries-identity-and-primary-key-fields-of-timeseries-model "") 的时序表。<br>  <br>- 1：支持包含 **自定义时间线标识或作为主键的数据字段** 的时序表。<br>  <br>**说明**<br>- 不同版本号会导致 [TimeseriesKey](https://help.aliyun.com/zh/tablestore/developer-reference/timeserieskey "") 数据结构的差异。<br>  <br>- 如果SDK中的版本号低于待操作的时序表模型版本号，将会导致错误。<br>  <br>- 如果您需自行开发Tablestore SDK，建议将其取值设定为固定值`1`。 |

## 响应消息结构

```protobuf
message DeleteTimeseriesMetaResponse {
  repeated FailedRowInfo failed_rows = 1;
}
```

| **名称** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **类型** | **描述** |
| failed\_rows | [FailedRowInfo](https://help.aliyun.com/zh/tablestore/developer-reference/failedrowinfo#reference-2126559 "") | 删除失败的行的信息。 |

## 使用SDK

您可以使用如下语言的SDK删除时间线元数据。

- [Java SDK：删除时间线元数据](https://help.aliyun.com/zh/tablestore/developer-reference/delete-time-series-metadata-by-using-java-sdk#concept-2171358 "")

- [Go SDK：删除时间线元数据](https://help.aliyun.com/zh/tablestore/developer-reference/delete-time-series-metadata-by-using-go-sdk "")

- [Python SDK：删除时间线元数据](https://help.aliyun.com/zh/tablestore/developer-reference/delete-time-series-metadata-by-python-sdk "")