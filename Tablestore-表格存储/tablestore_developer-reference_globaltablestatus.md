### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)GlobalTableStatus

# GlobalTableStatus

更新时间：2026-01-07 03:03:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GeoPoint](https://help.aliyun.com/zh/tablestore/developer-reference/geopoint)[下一篇：GroupByDateHistogram](https://help.aliyun.com/zh/tablestore/developer-reference/groupbydatehistogram)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

GlobalTableStatus数据类型定义，表示全局表的状态。

## **数据结构**

- G\_INIT：初始化中。全局表第一次创建后进入初始化状态。

- G\_RE\_CONF：重新配置中。全局表所有的副本在配置中或者部分副本在配置中。配置中可能是建表、同步历史数据或绑定解绑全局表的副本。

- G\_ACTIVE：已激活。


```protobuf
enum GlobalTableStatus {
  G_INIT = 1;
  G_RE_CONF = 2;
  G_ACTIVE = 3;
}
```