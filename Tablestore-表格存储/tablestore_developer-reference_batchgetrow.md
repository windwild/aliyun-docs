### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[基础数据操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-basic-data-operations/)BatchGetRow

# BatchGetRow

更新时间：2024-07-29 03:05:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

服务能力单元消耗

调用BatchGetRow接口批量读取一个表或多个表中的若干行数据。

BatchGetRow操作可视为多个GetRow操作的集合，各个操作独立执行，独立返回结果，独立计算服务能力单元。

与执行大量的GetRow操作相比，使用BatchGetRow操作可以有效减少请求的响应时间，提高数据的读取速率。

## 请求消息结构

```purebasic
message BatchGetRowRequest {
    repeated TableInBatchGetRowRequest tables = 1;
}
```

| **参数** | **类型** | **是否必填** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必填** | **描述** |
| tables | repeated [TableInBatchGetRowRequest](https://help.aliyun.com/zh/tablestore/developer-reference/tableinbatchgetrowrequest#reference1854 "") | 是 | 指定需要读取的行信息。<br>如果tables中出现了下述情况，则操作整体失败，返回错误。<br>- tables中任一表不存在。<br>  <br>- tables中任一表名不符合命名规则和数据类型。更多信息，请参见 [命名规则和数据类型](https://help.aliyun.com/zh/tablestore/naming-conventions-and-data-types#concept-iy4-qxq-pgb "")。<br>  <br>- tables中任一行未指定主键、主键名称不符合规范或者主键类型不正确。<br>  <br>- tables中任一表的columns\_to\_get内的列名不符合命令规则和数据类型。更多信息，请参见 [命名规则和数据类型](https://help.aliyun.com/zh/tablestore/naming-conventions-and-data-types#concept-iy4-qxq-pgb "")。<br>  <br>- tables中包含同名的表。<br>  <br>- 所有tables中RowInBatchGetRowRequest的总个数超过100个。<br>  <br>- tables中任一表中不包含任何RowInBatchGetRowRequest。<br>  <br>- tables中任一表的columns\_to\_get超过128列。 |

## 响应消息结构

**说明**

BatchGetRow操作可能会在行级别部分失败，此时返回的HTTP状态码仍为200。应用程序必须对RowInBatchGetRowResponse中的error进行检查确认每一行的执行结果，并进行相应的处理。

```purebasic
message BatchGetRowResponse {
    repeated TableInBatchGetRowResponse tables = 1;
}
```

| **参数** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **描述** |
| tables | repeated [TableInBatchGetRowResponse](https://help.aliyun.com/zh/tablestore/developer-reference/tableinbatchgetrowresponse#reference332 "") | 对应每个table下读取到的数据。<br>响应消息中TableInBatchGetRowResponse对象的顺序与BatchGetRowRequest中的TableInBatchGetRowRequest对象的顺序相同；每个TableInBatchGetRowResponse下的RowInBatchGetRowResponse对象的顺序与TableInBatchGetRowRequest下的RowInBatchGetRowRequest相同。<br>如果某行不存在或者某行在指定的columns\_to\_get中没有数据，仍然会在TableInBatchGetRowResponse中有一条对应的RowInBatchGetRowResponse，但其row下的primary\_key\_columns和attribute\_columns将为空。<br>如果某行读取失败，则该行所对应的RowInBatchGetRowResponse中is\_ok将为false，此时row将为空。 |

## 使用SDK

您可以使用如下语言的SDK批量读取数据。

- [Java SDK：批量读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-java-sdk#section-fdb-ph2-2fb "")

- [Go SDK：批量读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-go-sdk#section-h4a-woi-kmu "")

- [Python SDK：批量读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-python-sdk#section-fd0-sh9-pat "")

- [Node.js SDK：批量读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-nodejs-sdk#section-lds-2s6-fz9 "")

- [.NET SDK：批量读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-net-sdk#section-cw4-4n7-tii "")

- [PHP SDK：批量读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-php-sdk#section-ynn-4ko-2zn "")


## 服务能力单元消耗

- 如果本次操作整体失败，则不消耗任何服务能力单元。

- 如果请求超时，结果未定义，则服务能力单元有可能被消耗，也可能未被消耗。

- 其他情况将每个RowInBatchGetRowRequest视为一个GetRow操作独立计算读服务能力单元。更多信息，请参见 [GetRow服务能力单元消耗](https://help.aliyun.com/zh/tablestore/developer-reference/getrow#section-gxh-25t-1z "")。