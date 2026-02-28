### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)KnnVectorQuery

# KnnVectorQuery

更新时间：2024-06-14 03:23:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：JsonType](https://help.aliyun.com/zh/tablestore/developer-reference/jsontype)[下一篇：LastpointIndexMetaForCreate](https://help.aliyun.com/zh/tablestore/developer-reference/lastpointindexmetaforcreate)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

KnnVectorQuery使用数值向量进行近似最近邻查询，可以在大规模数据集中找到最相似的数据项。

## **数据结构**

```protobuf
message KnnVectorQuery {
    optional string field_name = 1;
    optional int32 top_k = 2;
    repeated float float32_query_vector = 4;
    optional Query filter = 5;
    optional float weight = 6;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **field\_name** | string | 是 | 向量字段名称。 |
| top\_k | int32 | 是 | 查询最邻近的topK个值。关于最大值的说明请参见 [多元索引限制](https://help.aliyun.com/zh/tablestore/product-overview/limits-on-search-index "")。 |
| float32\_query\_vector | float | 是 | 要查询相似度的向量。 |
| filter | [Query](https://help.aliyun.com/zh/tablestore/developer-reference/query "") | 否 | 查询过滤器，支持组合使用任意的非向量检索的查询条件。 |
| weight | float | 否 | 查询条件的权重配置。 |