### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)ExistsQuery

# ExistsQuery

更新时间：2024-04-08 06:10:43

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Error](https://help.aliyun.com/zh/tablestore/developer-reference/error)[下一篇：FailedRowInfo](https://help.aliyun.com/zh/tablestore/developer-reference/failedrowinfo)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

表示列存在性查询配置。ExistsQuery也叫NULL查询或者空值查询，一般用于判断稀疏数据中某一行的某一列是否存在。例如查询所有数据中address列不为空的行。

## **数据结构**

```protobuf
message ExistsQuery {
    optional string field_name = 1;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **field\_name** | string | 是 | 列名。 |