### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)PrimaryKeySchema

# PrimaryKeySchema

更新时间：2024-12-04 22:36:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PrimaryKeyOption](https://help.aliyun.com/zh/tablestore/developer-reference/primarykeyoption)[下一篇：PrimaryKeyType](https://help.aliyun.com/zh/tablestore/developer-reference/primarykeytype)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

主键列的配置信息。

## 数据结构

```protobuf
message PrimaryKeySchema {
    required string name = 1;
    required PrimaryKeyType type = 2;
    optional PrimaryKeyOption option = 3;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **name** | string | 是 | 主键列名称。 |
| **type** | [PrimaryKeyType](https://help.aliyun.com/zh/tablestore/developer-reference/primarykeytype#reference164 "") | 是 | 主键列的类型。 |
| **option** | [PrimaryKeyOption](https://help.aliyun.com/zh/tablestore/developer-reference/primarykeyoption#reference109 "") | 否 | 主键列的可选配置。 |