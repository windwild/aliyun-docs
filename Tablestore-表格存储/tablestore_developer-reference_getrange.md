### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[基础数据操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-basic-data-operations/)GetRange

# GetRange

更新时间：2023-10-06 22:28:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DeleteRow](https://help.aliyun.com/zh/tablestore/developer-reference/deleterow)[下一篇：BatchGetRow](https://help.aliyun.com/zh/tablestore/developer-reference/batchgetrow)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

服务能力单元消耗

调用GetRange接口读取指定主键范围内的数据。

## 请求消息结构

```protobuf
message GetRangeRequest {
    required string table_name = 1;
    required Direction direction = 2;
    repeated string columns_to_get = 3;  // 不指定则读出所有列。
    optional TimeRange time_range = 4;
    optional int32 max_versions = 5;
    optional int32 limit = 6;
    required bytes inclusive_start_primary_key = 7; // Plainbuffer编码为二进制。
    required bytes exclusive_end_primary_key = 8; // Plainbuffer编码为二进制。
    optional bytes filter = 10;
    optional string start_column = 11;
    optional string end_column = 12;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| table\_name | string | 是 | 表名。 |
| direction | [Direction](https://help.aliyun.com/zh/tablestore/developer-reference/direction#reference189 "") | 是 | 本次查询的顺序。 <br>- 如果设置此项为FORWARD（正序），则inclusive\_start\_primary必须小于exclusive\_end\_primary，响应中各行按照主键由小到大的顺序进行排列。<br>  <br>- 如果设置此项为BACKWARD（逆序），则inclusive\_start\_primary必须大于exclusive\_end\_primary，响应中各行按照主键由大到小的顺序进行排列。 |
| columns\_to\_get | repeated string | 否 | 需要返回的全部列的列名。columns\_to\_get中的string个数不能超过128个。<br>- 如果未设置此项或者设置此项为空，则返回指定行的所有列。<br>  <br>- 如果设置此项为指定列，当某行中指定的列均不存在时，则不返回该行，即返回值为null；当某行中存在部分指定的列时，则返回该行且只返回存在的列。<br>  <br>  如果指定的列中存在重复的列名，则返回结果中只会包含一次该列。 |
| time\_range | [TimeRange](https://help.aliyun.com/zh/tablestore/developer-reference/timerange#reference456 "") | 否，和max\_versions只能存在一个 | 读取数据的版本时间戳范围。时间戳的单位为毫秒，取值最小值为0，最大值为`INT64.MAX`。<br>- 如果要查询一个时间范围，则指定start\_time和end\_time。time\_range为前闭后开区间，即`[start_time,end_time)`。<br>  <br>  如果指定的time\_range为`[100, 200)`，则返回的列数据的时间戳必须处于`[100, 200)`范围内，<br>  <br>- 如果要查询一个特定时间戳，则指定specific\_time。 |\
| max\_versions | int32 | 否，和time\_range只能存在一个 | 最多返回的版本个数。<br>如果指定max\_versions为2，则每一列最多返回2个版本的数据。 |\
| limit | int32 | 否 | 本次读取最多返回的行数。取值必须大于0。<br>如果查询到的行数超过此值，则通过响应中会包含断点来记录本次读取到的位置，以便下一次读取。<br>无论是否设置此项，表格存储最多返回的行数为5000且总数据大小不超过4 MB。 |\
| inclusive\_start\_primary\_key | bytes | 是 | 本次范围读取的起始主键，由Plainbuffer编码。更多信息，请参见 [Plainbuffer](https://help.aliyun.com/zh/tablestore/developer-reference/plainbuffer#reference3003 "")。<br>如果该行存在，则响应中一定会包含此行。 |\
| exclusive\_end\_primary\_key | bytes | 是 | 本次范围读取的结束主键，由Plainbuffer编码。更多信息，请参见 [Plainbuffer](https://help.aliyun.com/zh/tablestore/developer-reference/plainbuffer#reference3003 "")。<br>无论该行是否存在，则响应中一定不会包含此行。<br>在使用GetRange操作时，inclusive\_start\_primary\_key和exclusive\_end\_primary\_key中Column的type支持使用特有的INF\_MIN和INF\_MAX两个类型。其中类型为INF\_MIN的Column小于其它Column，类型为INF\_MAX的Column大于其它Column。 |\
| filter | bytes | 否 | 过滤条件表达式。 [Filter](https://help.aliyun.com/zh/tablestore/developer-reference/filter-1#reference427 "") 经过protobuf序列化后的二进制数据。 |\
| start\_column | string | 否 | 指定读取时的起始列，主要用于宽行读。返回结果中会包含当前起始列。列的顺序按照列名的字典序排序。<br>如果表中有a、b、c三列，当读取数据时指定start\_column为b，则会从b列开始读数据，返回b、c两列。 |\
| end\_column | string | 否 | 指定读取时的结束列，主要用于宽行读。返回结果中不会包含当前结束列。列的顺序按照列名的字典序排序。<br>如果表中有a、b、c三列，当读取数据时指定end\_column为b，则读到b列会结束，返回a列。 |\
\
## 响应消息结构\
\
```protobuf\
message GetRangeResponse {\
    required ConsumedCapacity consumed = 1;\
    required bytes rows = 2;\
    optional bytes next_start_primary_key = 3;\
}\
```\
\
| **名称** | **类型** | **描述** |\
| --- | --- | --- |\
\
|     |     |     |\
| --- | --- | --- |\
| **名称** | **类型** | **描述** |\
| consumed | [ConsumedCapacity](https://help.aliyun.com/zh/tablestore/developer-reference/consumedcapacity#reference186 "") | 本次操作消耗的服务能力单元。更多信息，请参见 [服务能力单元](https://help.aliyun.com/zh/tablestore/developer-reference/getrange#section-2ij-qj7-ulf "")。 |\
| rows | bytes | 读取到的所有数据，由Plainbuffer编码。更多信息，请参见 [Plainbuffer](https://help.aliyun.com/zh/tablestore/developer-reference/plainbuffer#reference3003 "")。<br>- 如果在请求中设置 **direction** 为 **FORWARD**，则所有行按照主键由小到大进行排序。<br>  <br>- 如果在请求中设置 **direction** 为 **BACKWARD**，则所有行按照主键由大到小进行排序。<br>  <br>其中每行的primary\_key\_columns和attribute\_columns均只包含在columns\_to\_get中指定的列，其顺序不保证与请求中的columns\_to\_get一致；primary\_key\_columns的顺序也不保证与建表时指定的顺序一致。<br>如果在请求中指定的columns\_to\_get不包含任何主键列，当某行的主键在查询范围内，但该行没有属性列在columns\_to\_get中，则该行不会出现在响应消息。 |\
| next\_start\_primary\_key | bytes | 本次操作的断点信息，由Plainbuffer编码。更多信息，请参见 [Plainbuffer](https://help.aliyun.com/zh/tablestore/developer-reference/plainbuffer#reference3003 "") 编码。<br>- 当返回值为空时，表示本次GetRange的响应消息中已包含请求范围内的所有数据。<br>  <br>- 当返回值不为空时，表示本次GetRange的响应消息中只包含了`[inclusive_start_primary_key, next_start_primary_key)`间的数据。<br>  <br>  如果需要继续读取剩下的数据，则需要将next\_start\_primary\_key作为inclusive\_start\_primary\_key，原始请求中的 exclusive\_end\_primary\_key作为exclusive\_end\_primary\_key继续执行GetRange操作。<br>  <br>**说明**<br>表格存储限制GetRange操作响应消息中的数据行数不能超过5000行，数据大小不能超过4 MB。<br>即使在GetRange请求中未设置limit，在响应消息中仍可能出现next\_start\_primary\_key。因此使用GetRange操作时，您需要对响应消息中是否有next\_start\_primary\_key进行处理。 |\
\
## 使用SDK\
\
您可以使用如下语言的SDK范围读取数据。\
\
- [Java SDK：范围读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-java-sdk#section-n82-igs-yy6 "")\
\
- [Go SDK：范围读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-go-sdk#section-4cd-rqb-x81 "")\
\
- [Python SDK：范围读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-python-sdk#section-tjs-722-kdx "")\
\
- [Node.js SDK：范围读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-nodejs-sdk#section-3wf-ez5-eak "")\
\
- [.NET SDK：范围读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-net-sdk#section-at5-3hz-ddh "")\
\
- [PHP SDK：范围读取数据](https://help.aliyun.com/zh/tablestore/developer-reference/read-data-by-using-php-sdk#section-lcc-ax1-lqk "")\
\
\
## 服务能力单元消耗\
\
- GetRange操作消耗读服务能力单元的数值为查询范围内所有行主键数据大小与实际读取的属性列数据大小之和除以4 KB向上取整。关于数据大小的计算请参见 [数据存储量](https://help.aliyun.com/zh/tablestore/product-overview/storage-usage "")。\
\
- 如果请求超时，结果未定义，则服务能力单元有可能被消耗，也可能未被消耗。\
- 如果返回内部错误（HTTP状态码：5XX），则此次操作不消耗服务能力单元，其他错误情况消耗1读服务能力单元。