### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[局部事务操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-local-transaction-operations/)AbortTransaction

# AbortTransaction

更新时间：2024-05-14 21:34:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CommitTransaction](https://help.aliyun.com/zh/tablestore/developer-reference/committransaction)[下一篇：时序表操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-timeseries-table-operations/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

请求消息结构

响应消息结构

使用SDK

调用AbortTransaction接口丢弃局部事务。创建一个分区键值内的局部事务并对局部事务中的数据进行写操作后，如果无需保存数据更新，则需要丢弃局部事务或者等待局部事务超时。

## **注意事项**

- 每个局部事务从创建开始生命周期最长为60秒。

如果超过60秒未提交局部事务或丢弃局部事务，则表格存储服务端会认为此局部事务超时，并将局部事务丢弃。

- 如果未对局部事务范围内的数据进行写操作，则提交局部事务或丢弃局部事务的操作是等同的。


## **请求消息结构**

```protobuf
message AbortTransactionRequest {
    required string transaction_id = 1;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **transaction\_id** | string | 是 | 局部事务ID。 |

## **响应消息结构**

```protobuf
message AbortTransactionResponse {
}
```

## **使用SDK**

您可以使用如下语言的SDK使用局部事务。

- [Java SDK：局部事务](https://help.aliyun.com/zh/tablestore/developer-reference/configure-local-transaction-by-java-sdk#concept-2356866 "")

- [Go SDK：局部事务](https://help.aliyun.com/zh/tablestore/developer-reference/configure-local-transaction-by-go-sdk#concept-2498322 "")

- [Python SDK：局部事务](https://help.aliyun.com/zh/tablestore/developer-reference/configure-local-transaction-by-python-sdk#concept-2356921 "")

- [Node.js SDK：局部事务](https://help.aliyun.com/zh/tablestore/developer-reference/configure-local-transaction-by-nodejs-sdk#concept-2494488 "")

- [PHP SDK：局部事务](https://help.aliyun.com/zh/tablestore/developer-reference/configure-local-transaction-by-php-sdk#concept-422975 "")