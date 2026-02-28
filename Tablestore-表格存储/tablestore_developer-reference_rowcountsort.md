### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储 Tablestore](https://help.aliyun.com/zh/tablestore/) [开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/) [API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/) [DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/) RowCountSort

# RowCountSort

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ReturnType](https://help.aliyun.com/zh/tablestore/developer-reference/returntype)[下一篇：RowExistenceExpectation](https://help.aliyun.com/zh/tablestore/developer-reference/rowexistenceexpectation)

该文章对您有帮助吗？

反馈

表示按照分组中总行数排序的排序规则。

## **数据结构**

```protobuf
message RowCountSort {
    optional SortOrder order = 1;
}
```

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **order** | [SortOrder](https://help.aliyun.com/zh/tablestore/developer-reference/sortorder "") | 是 | 分组中总行数的排序顺序。 |