### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[二级索引操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-secondary-index-operations/)DropIndex

# DropIndex

更新时间：2024-07-29 03:40:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

调用DropIndex接口在指定的数据表上删除索引表。

## 请求消息结构

```plaintext
message DropIndexRequest {
    required string main_table_name = 1;
    required string index_name = 2;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| main\_table\_name | string | 是 | 要删除的索引表所在的数据表。 |
| index\_name | string | 是 | 要删除的索引表名称。 |

## 响应消息结构

```plaintext
message DropIndexResponse {
}
```

## 使用SDK

您可以使用如下语言的SDK删除索引表。

- [Java SDK：删除索引表](https://help.aliyun.com/zh/tablestore/developer-reference/global-secondary-index-3#section-qnv-qhb-gpm "")

- [Go SDK：删除索引表](https://help.aliyun.com/zh/tablestore/developer-reference/create-secondary-index-by-using-go-sdk#section-3ot-4se-zjx "")

- [Python SDK：删除索引表](https://help.aliyun.com/zh/tablestore/developer-reference/create-secondary-index-by-using-python-sdk#section-z9o-wuj-yku "")

- [Node.js SDK：删除索引表](https://help.aliyun.com/zh/tablestore/developer-reference/create-secondary-index-by-using-nodejs-sdk#section-n7o-etj-crr "")

- [.NET SDK：删除索引表](https://help.aliyun.com/zh/tablestore/developer-reference/create-secondary-index-by-using-net-sdk#section-bf6-rkw-72k "")

- [PHP SDK：删除索引表](https://help.aliyun.com/zh/tablestore/developer-reference/create-secondary-index-by-using-php-sdk#section-ogx-5ag-zri "")