### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)RowsSerializeType

# RowsSerializeType

更新时间：2024-07-23 01:21:00

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RowInBulkImportResponse](https://help.aliyun.com/zh/tablestore/developer-reference/rowinbulkimportresponse)[下一篇：ScanQuery](https://help.aliyun.com/zh/tablestore/developer-reference/scanquery)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

枚举取值列表

时序数据的行序列化类型。

## 枚举取值列表

- RST\_FLAT\_BUFFER表示使用flatbuffer的序列化方式。

- RST\_PLAIN\_BUFFER表示使用plainbuffer的序列化方式。


```protobuf
enum RowsSerializeType {
  RST_FLAT_BUFFER = 0;
  RST_PLAIN_BUFFER = 1;
}
```