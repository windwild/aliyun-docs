### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储 Tablestore](https://help.aliyun.com/zh/tablestore/) [开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/) [API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/) [DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/) NestedQuery

# NestedQuery

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：NestedFilter](https://help.aliyun.com/zh/tablestore/developer-reference/nestedfilter)[下一篇：PercentilesAggregation](https://help.aliyun.com/zh/tablestore/developer-reference/percentilesaggregation)

该文章对您有帮助吗？

反馈

NestedQuery数据类型定义，表示嵌套类型查询配置。NestedQuery用于查询嵌套类型字段中子行的数据。嵌套类型不能直接查询，需要通过NestedQuery包装，NestedQuery中需要指定嵌套类型字段的路径和一个子查询，其中子查询可以是任意Query类型。

## **数据结构**

```protobuf
message NestedQuery {
    optional string path = 1;
    optional Query query = 2;
    optional ScoreMode score_mode = 3;
    optional float weight = 4;
    optional InnerHits inner_hits = 5;
}
```

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **path** | string | 是 | 路径名，嵌套类型字段的树状路径。例如news.title表示嵌套类型的news字段中的title子列。 |
| **query** | [Query](https://help.aliyun.com/zh/tablestore/developer-reference/query "") | 是 | 嵌套类型字段的子列上的查询，子列上的查询可以是任意Query类型。 |
| **score\_mode** | [SortMode](https://help.aliyun.com/zh/tablestore/developer-reference/sortmode "") | 否 | 当字段存在多个值时基于哪个值计算分数。 |
| **weight** | float | 否 | 查询条件的权重配置。 |
| **inner\_hits** | [InnerHits](https://help.aliyun.com/zh/tablestore/developer-reference/innerhits "") | 否 | 嵌套类型字段的子列的配置参数。 |