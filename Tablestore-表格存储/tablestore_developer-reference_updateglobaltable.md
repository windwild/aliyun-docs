### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[全局表操作](https://help.aliyun.com/zh/tablestore/developer-reference/global-table-api/)UpdateGlobalTable

# UpdateGlobalTable

更新时间：2026-01-07 05:56:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DescribeGlobalTable](https://help.aliyun.com/zh/tablestore/developer-reference/describeglobaltable)[下一篇：BindGlobalTable](https://help.aliyun.com/zh/tablestore/developer-reference/bindglobaltable)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

调用UpdateGlobalTable接口更新全局表中物理表的配置。

## **请求消息结构**

```protobuf
message UpdateGlobalTableRequest {
  required string globalTableId = 1;
  required string globalTableName = 2;
  optional UpdatePhyTable phyTable = 3;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **globalTableId** | string | 是 | 全局表ID。 |
| **globalTableName** | string | 是 | 全局表名称。 |
| **phyTable** | [UpdatePhyTable](https://help.aliyun.com/zh/tablestore/developer-reference/updatephytable "") | 是 | 待更新的物理表信息。 |

## **响应消息结构**

```protobuf
message UpdateGlobalTableResponse {
}
```

可通过判断HTTP请求的status取值是否为200来确定是否执行成功。

- 如果status取值为200，则表示执行成功。

- 如果status取值为400或者500，则表示执行失败。

如果请求执行失败，则会返回Error信息。更多信息，请参见 [Error](https://help.aliyun.com/zh/tablestore/developer-reference/error "")。