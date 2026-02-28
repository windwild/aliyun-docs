### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)SuffixQuery

# SuffixQuery

更新时间：2025-03-17 22:09:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SubAggSort](https://help.aliyun.com/zh/tablestore/developer-reference/subaggsort)[下一篇：SumAggregation](https://help.aliyun.com/zh/tablestore/developer-reference/sumaggregation)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

SuffixQuery数据类型定义，表示后缀查询配置。SuffixQuery通过指定后缀条件查询索引中的数据，例如通过手机尾号后4位查询快递。

## **数据结构**

```protobuf
message SuffixQuery {
    optional string field_name = 1;
    optional string suffix = 2;
    optional float weight = 3;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **field\_name** | string | 是 | 列名。 |
| **suffix** | string | 是 | 后缀值。 |
| **weight** | float | 否 | 查询条件的权重配置。 |