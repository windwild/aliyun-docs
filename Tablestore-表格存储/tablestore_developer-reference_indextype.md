### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)IndexType

# IndexType

更新时间：2024-08-22 23:06:58

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：IndexSyncPhase](https://help.aliyun.com/zh/tablestore/developer-reference/index-sync-phase)[下一篇：IndexUpdateMode](https://help.aliyun.com/zh/tablestore/developer-reference/index-update-mode)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

枚举取值列表

表示索引类型。

## 枚举取值列表

- IT\_GLOBAL\_INDEX表示全局二级索引。使用全局二级索引时，表格存储以异步方式将数据表中被索引的列和主键列的数据自动同步到索引表中，正常情况下同步延迟达到毫秒级别。

- IT\_LOCAL\_INDEX表示本地二级索引。使用本地二级索引时，表格存储以同步方式将数据表中被索引的列和主键列的数据自动同步到索引表中，当数据写入数据表后，即可从索引表中查询到数据。


```protobuf
enum IndexType {
    IT_GLOBAL_INDEX = 0;
    IT_LOCAL_INDEX = 1;
}
```