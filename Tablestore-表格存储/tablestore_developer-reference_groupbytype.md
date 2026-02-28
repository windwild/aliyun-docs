### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)GroupByType

# GroupByType

更新时间：2024-04-08 05:40:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GroupBysResult](https://help.aliyun.com/zh/tablestore/developer-reference/groupbysresult)[下一篇：GroupKeySort](https://help.aliyun.com/zh/tablestore/developer-reference/groupkeysort)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

枚举取值列表

表示分组类型。

## **枚举取值列表**

- GROUP\_BY\_FIELD表示字段值分组。

- GROUP\_BY\_RANGE表示范围分组。

- GROUP\_BY\_FILTER表示过滤条件分组。

- GROUP\_BY\_GEO\_DISTANCE表示地理位置分组。

- GROUP\_BY\_HISTOGRAM表示直方图统计。

- GROUP\_BY\_DATE\_HISTOGRAM表示日期直方图统计。


```protobuf
enum GroupByType {
    GROUP_BY_FIELD = 1;
    GROUP_BY_RANGE = 2;
    GROUP_BY_FILTER = 3;
    GROUP_BY_GEO_DISTANCE = 4;
    GROUP_BY_HISTOGRAM = 5;
    GROUP_BY_DATE_HISTOGRAM = 6;
}
```