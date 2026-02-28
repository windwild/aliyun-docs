### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储 Tablestore](https://help.aliyun.com/zh/tablestore/) [开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/) [API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/) [DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/) SearchHit

# SearchHit

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SearchFilter](https://help.aliyun.com/zh/tablestore/developer-reference/searchfilter)[下一篇：SearchInnerHit](https://help.aliyun.com/zh/tablestore/developer-reference/searchinnerhit)

该文章对您有帮助吗？

反馈

SearchHit数据类型定义，表示返回的命中结果。当使用查询摘要与高亮或向量检索功能进行查询时才有返回值。

## **数据结构**

```protobuf
message SearchHit {
    optional double score = 3;
    optional HighlightResult highlight_result = 4;
    repeated SearchInnerHit search_inner_hits = 5;
    optional int32 nested_doc_offset = 6;
}
```

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **score** | double | 否 | 相关性分数。 |
| **highlight\_result** | [HighlightResult](https://help.aliyun.com/zh/tablestore/developer-reference/highlightresult "") | 否 | 非嵌套类型字段的高亮分片结果。 |
| **search\_inner\_hits** | [SearchInnerHit](https://help.aliyun.com/zh/tablestore/developer-reference/searchinnerhit "") | 否 | 嵌套类型字段的命中数据行结果。 |
| **nested\_doc\_offset** | int32 | 否 | 当嵌套类型字段包含多个子行时，子行返回的起始位置。 |