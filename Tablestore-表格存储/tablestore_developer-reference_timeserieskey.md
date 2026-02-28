### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)TimeseriesKey

# TimeseriesKey

更新时间：2025-04-10 04:04:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：TimeseriesFieldsToGet](https://help.aliyun.com/zh/tablestore/developer-reference/timeseriesfieldstoget)[下一篇：TimeseriesLastpointIndex](https://help.aliyun.com/zh/tablestore/developer-reference/timeserieslastpointindex)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

数据结构

表示时间线标识。

## **注意事项**

[PutTimeseriesData](https://help.aliyun.com/zh/tablestore/developer-reference/puttimeseriesdata "")、 [GetTimeseriesData](https://help.aliyun.com/zh/tablestore/developer-reference/gettimeseriesdata "")、 [UpdateTimeseriesMeta](https://help.aliyun.com/zh/tablestore/developer-reference/updatetimeseriesmeta "")、 [QueryTimeseriesMeta](https://help.aliyun.com/zh/tablestore/developer-reference/querytimeseriesmeta "")、 [DeleteTimeseriesMeta](https://help.aliyun.com/zh/tablestore/developer-reference/deletetimeseriesmeta "") 和 [ScanTimeseriesData](https://help.aliyun.com/zh/tablestore/developer-reference/scantimeseriesdata "") 操作中提供的supported\_table\_version参数取值会导致TimeseriesKey定义有所变化。

## 数据结构

```protobuf
message TimeseriesKey {
  optional string measurement = 1;
  optional string source = 2;
  optional string tags = 3;
  repeated TimeseriesTag tag_list = 4;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **measurement** | string | 否 | 度量名称。 |
| **source** | string | 否 | 数据源标识。 |
| **tags** | string | 否 | 标签信息。当supported\_table\_version为0时，需要配置此参数。 |
| **tag\_list** | [TimeseriesTag](https://help.aliyun.com/zh/tablestore/developer-reference/timeseriestag "") | 否 | 标签信息。当supported\_table\_version为1时，需要配置此参数。 |