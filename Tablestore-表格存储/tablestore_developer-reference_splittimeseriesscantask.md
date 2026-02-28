### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[时序数据操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-timeseries-data-operations/)SplitTimeseriesScanTask

# SplitTimeseriesScanTask

更新时间：2024-05-13 01:09:49

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DeleteTimeseriesMeta](https://help.aliyun.com/zh/tablestore/developer-reference/deletetimeseriesmeta)[下一篇：ScanTimeseriesData](https://help.aliyun.com/zh/tablestore/developer-reference/scantimeseriesdata)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

调用SplitTimeseriesScanTask接口切分全量导出任务。

## **请求消息结构**

```protobuf
message SplitTimeseriesScanTaskRequest {
  required string table_name = 1;
  optional string measurement_name = 2;
  required int32 split_count_hint = 3;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **table\_name** | string | 是 | 时序表名。 |
| **measurement\_name** | string | 否 | 度量名称。 |
| **split\_count\_hint** | int32 | 是 | 期望切分的任务数，取值大于0。<br>服务端会根据该值切分任务个数，但实际切分的任务个数由服务端决定。 |

## **响应消息结构**

```protobuf
message SplitTimeseriesScanTaskResponse {
  repeated bytes split_infos = 1;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **split\_infos** | bytes | 是 | 服务端编码的任务切分信息，用于传递给 [ScanTimeseriesData](https://help.aliyun.com/zh/tablestore/developer-reference/scantimeseriesdata "") 接口进行时序数据扫描。 |