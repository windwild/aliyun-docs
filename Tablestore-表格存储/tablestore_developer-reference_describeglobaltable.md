### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[全局表操作](https://help.aliyun.com/zh/tablestore/developer-reference/global-table-api/)DescribeGlobalTable

# DescribeGlobalTable

更新时间：2026-01-07 05:24:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CreateGlobalTable](https://help.aliyun.com/zh/tablestore/developer-reference/createglobaltable)[下一篇：UpdateGlobalTable](https://help.aliyun.com/zh/tablestore/developer-reference/updateglobaltable)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

调用DescribeGlobalTable接口查询全局表中的物理表描述信息。

## **请求消息结构**

```protobuf
message DescribeGlobalTableRequest {
  optional string globalTableId = 1;
  required string globalTableName = 2;
  optional PhyTable phyTable = 3;
  optional bool returnRpo = 4;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **globalTableId** | string | 否 | 全局表ID。 |
| **globalTableName** | string | 是 | 全局表名称。 |
| **phyTable** | [PhyTable](https://help.aliyun.com/zh/tablestore/developer-reference/phytable "") | 否 | 筛选物理表条件，只需设置物理表的地域ID或实例名称。 |
| **returnRpo** | bool | 否 | 是否同时返回RPO。 |

## **响应消息结构**

```protobuf
message DescribeGlobalTableResponse {
  required string globalTableId = 2;
  required GlobalTableStatus status = 3;
  repeated PhyTable phyTables = 4;
  optional ServeMode serveMode = 5;
}
```

| **名称** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **类型** | **描述** |
| **globalTableId** | string | 全局表ID。 |
| **status** | [GlobalTableStatus](https://help.aliyun.com/zh/tablestore/developer-reference/globaltablestatus "") | 全局表名称。 |
| **phyTables** | [PhyTable](https://help.aliyun.com/zh/tablestore/developer-reference/phytable "") | 物理表详细信息列表。 |
| **serveMode** | [ServeMode](https://help.aliyun.com/zh/tablestore/developer-reference/servemode "") | 服务模式。 |