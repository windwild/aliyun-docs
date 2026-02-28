### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)SyncPhase

# SyncPhase

更新时间：2024-04-08 06:04:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SyncMode](https://help.aliyun.com/zh/tablestore/developer-reference/syncmode)[下一篇：SyncStage](https://help.aliyun.com/zh/tablestore/developer-reference/syncstage)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

枚举取值列表

表示多元索引的同步阶段。

## **枚举取值列表**

- FULL表示全量同步阶段。

- INCR表示增量同步阶段。


```protobuf
enum SyncPhase {
    FULL = 1;
    INCR = 2;
}
```