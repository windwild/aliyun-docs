### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[预定义列操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-defined-column-operations/)AddDefinedColumn

# AddDefinedColumn

更新时间：2024-03-10 23:16:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：预定义列操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-defined-column-operations/)[下一篇：DeleteDefinedColumn](https://help.aliyun.com/zh/tablestore/developer-reference/deletedefinedcolumn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

请求消息结构

响应消息结构

使用SDK

调用AddDefinedColumn接口为数据表添加预定义列。预定义列可用作索引表的主键列或者属性列。

## **注意事项**

- 只有使用二级索引时才需要为数据表添加预定义列。使用多元索引时，无需为数据表添加预定义列。

- 预定义列最多支持创建32个。


## **请求消息结构**

```protobuf
message AddDefinedColumnRequest {
    required string table_name = 1;
    repeated DefinedColumnSchema columns = 2;
}
```

| **参数** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **描述** |
| **table\_name** | string | 是 | 数据表名称。 |
| **columns** | [DefinedColumnSchema](https://help.aliyun.com/zh/tablestore/developer-reference/defined-columns-schema-of-defined-columns "") | 是 | 预定义列结构。 |

## **响应消息结构**

```protobuf
message AddDefinedColumnResponse {
}
```

## 使用SDK

您可以使用如下语言的SDK为数据表添加预定义列。

- [Java SDK：增加预定义列](https://help.aliyun.com/zh/tablestore/developer-reference/defined-column-operation-in-java#section-an1-brd-vxa "")

- [Go SDK：增加预定义列](https://help.aliyun.com/zh/tablestore/developer-reference/defined-column-operation-in-go#section-x9y-ijw-rib "")