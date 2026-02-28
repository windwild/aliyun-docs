### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)SortMode

# SortMode

更新时间：2024-04-08 23:01:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Sorter](https://help.aliyun.com/zh/tablestore/developer-reference/sorter)[下一篇：SortOrder](https://help.aliyun.com/zh/tablestore/developer-reference/sortorder)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

枚举取值列表

当字段中存在多个值时的排序方式，支持按照最大值、最小值或者平均值参与排序。

## **注意事项**

多个值中参与排序的默认值与数据的排列顺序（升序或者降序）有关。

- 当按照升序排列数据时，默认值为SORT\_MODE\_MIN。

- 当按照降序排列数据时，默认值为SORT\_MODE\_MAX。


## **枚举取值列表**

- SORT\_MODE\_MIN表示使用多个值中的最小值参与排序。

- SORT\_MODE\_MAX表示使用多个值中的最大值参与排序。

- SORT\_MODE\_AVG表示使用多个值的平均值参与排序。


```protobuf
enum SortMode {
    SORT_MODE_MIN = 0;
    SORT_MODE_MAX = 1;
    SORT_MODE_AVG = 2;
}
```