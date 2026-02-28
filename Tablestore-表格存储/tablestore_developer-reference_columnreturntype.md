### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)ColumnReturnType

# ColumnReturnType

更新时间：2024-04-08 22:02:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ComparatorType](https://help.aliyun.com/zh/tablestore/developer-reference/comparatortype)[下一篇：ColumnsToGet](https://help.aliyun.com/zh/tablestore/developer-reference/columnstoget)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

枚举取值列表

表示列返回类型。

## **枚举取值列表**

- RETURN\_ALL表示返回数据表中的所有列。

- RETURN\_SPECIFIED表示返回指定列，此时需要设置要返回的列。可以是数据表或多元索引中的任意列。

- RETURN\_NONE表示只返回主键。

- RETURN\_ALL\_FROM\_INDEX表示返回多元索引中的所有列。


```protobuf
enum ColumnReturnType {
    RETURN_ALL = 1;
    RETURN_SPECIFIED = 2;
    RETURN_NONE = 3;
    RETURN_ALL_FROM_INDEX = 4;
}
```