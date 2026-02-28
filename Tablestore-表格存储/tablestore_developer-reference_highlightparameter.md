### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)HighlightParameter

# HighlightParameter

更新时间：2025-01-02 03:26:36

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：HighlightFragmentOrder](https://help.aliyun.com/zh/tablestore/developer-reference/highlightfragmentorder)[下一篇：HighlightResult](https://help.aliyun.com/zh/tablestore/developer-reference/highlightresult)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

HighlightParameter数据类型定义，表示高亮参数。

## **数据结构**

```protobuf
message HighlightParameter {
    optional string  field_name = 1;
    optional int32   number_of_fragments = 2;
    optional int32   fragment_size = 3;
    optional string  pre_tag = 4;
    optional string  post_tag = 5;
    optional HighlightFragmentOrder fragments_order = 6 [default=TEXT_SEQUENCE];
}
```

| **名称** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **说明** |
| **field\_name** | string | 是 | 字段名称。请确保在创建多元索引时已为该字段开启查询摘要与高亮。 |
| **number\_of\_fragments** | int32 | 否 | 返回高亮分片的最大数量，推荐设置为1。 |
| **fragment\_size** | int32 | 否 | 每个分片的长度。默认值100。 |
| **pre\_tag** | string | 否 | 查询词高亮的前置Tag，例如`<em>`、`<b>`。默认值为`<em>`，您可以按需自定义前置Tag。preTag支持的字符集包括`< > " ' /`、`a-z`、`A-Z`、`0-9`。 |
| **post\_tag** | string | 否 | 查询词高亮的后置Tag，例如`</em>`、`</b>`。默认值为`</em>`，您可以按需自定义后置Tag。postTag支持的字符集包括`< > " ' /`、`a-z`、`A-Z`、`0-9`。 |
| **fragments\_order** | [HighlightFragmentOrder](https://help.aliyun.com/zh/tablestore/developer-reference/highlightfragmentorder "") | 否 | 当高亮字段返回多个分片时，分片的排序规则。 |