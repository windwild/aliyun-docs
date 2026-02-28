### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)ScanQuery

# ScanQuery

更新时间：2024-04-09 03:17:25

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RowsSerializeType](https://help.aliyun.com/zh/tablestore/developer-reference/rowsserializetype)[下一篇：SearchFilter](https://help.aliyun.com/zh/tablestore/developer-reference/searchfilter)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

相关操作

在ParallelScan操作中表示扫描查询配置。

## **数据结构**

```protobuf
message ScanQuery {
    optional Query query = 1;
    optional int32 limit = 2;
    optional int32 alive_time = 3;  //unit is second
    optional bytes token = 4;
    optional int32 current_parallel_id = 5;
    optional int32 max_parallel = 6;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **query** | [Query](https://help.aliyun.com/zh/tablestore/developer-reference/query "") | 是 | 查询条件。支持精确查询、模糊查询、范围查询、地理位置查询、嵌套查询等。 |
| **limit** | int32 | 否 | 扫描数据时一次能返回的数据行数。 |
| **alive\_time** | int32 | 否 | ParallelScan的当前任务有效时间，也是token的有效时间。默认值为60，建议使用默认值，单位为秒。<br>如果在有效时间内没有发起下一次请求，则不能继续读取数据。持续发起请求会刷新token有效时间。 |
| **token** | bytes | 否 | 用于翻页功能。<br>ParallelScan请求结果中有下一次进行翻页的token，使用该token可以接着上一次的结果继续读取数据。 |
| **current\_parallel\_id** | int32 | 是 | 当前并发ID。取值范围为\[0, max\_parallel)。 |\
| **max\_parallel** | int32 | 是 | 最大并发数。请求支持的最大并发数由用户数据量决定。数据量越大，支持的并发数越多。 |\
\
## **相关操作**\
\
[ParallelScan](https://help.aliyun.com/zh/tablestore/developer-reference/parallelscan "")