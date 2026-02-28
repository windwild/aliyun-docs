### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)SyncMode

# SyncMode

更新时间：2026-01-07 03:07:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

SyncMode数据类型定义，表示全局表的数据同步模式。

## **数据结构**

- SYNC\_MODE\_ROW；行级同步，以行为单位进行数据同步，每行数据变更会独立复制到其他地域。目前只支持行级同步。

- SYNC\_MODE\_COLUMN：列级同步。


```protobuf
enum SyncMode {
  SYNC_MODE_ROW = 1;
  SYNC_MODE_COLUMN = 2;
}
```