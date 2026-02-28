### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)UpdatePhyTable

# UpdatePhyTable

更新时间：2026-01-07 05:21:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：TunnelType](https://help.aliyun.com/zh/tablestore/developer-reference/tunneltype)[下一篇：ValueTransferRule](https://help.aliyun.com/zh/tablestore/developer-reference/valuetransferrule)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

UpdatePhyTable数据类型定义，表示全局表中待更新的物理表信息。

## **数据结构**

```protobuf
message UpdatePhyTable {
  required string regionId = 1;
  required string instanceName = 2;
  required string tableName = 3;
  optional bool writable = 4;
  // set phy table is eligible for primary, only need at PRIMARY_SECONDARY serve mode
  optional bool primaryEligible = 5;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **regionId** | string | 是 | 物理表所在地域ID。 |
| **instanceName** | string | 是 | 物理表所在实例名称。 |
| **tableName** | string | 是 | 物理表名称。 |
| **writable** | bool | 否 | 是否可写。默认值为false。当使用主备模式时，请保持默认配置。当使用多写模式时，请按需配置此项为true。 |
| **primaryEligible** | bool | 否 | 是否设置为具备主资质，用于在主备模式时进行主备切换。<br>在主备模式下，默认不允许开启其他非主表的写操作。当执行主备切换时，将副表标记为具备主资质。 |