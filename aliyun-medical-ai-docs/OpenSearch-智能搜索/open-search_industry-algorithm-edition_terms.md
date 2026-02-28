### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[产品概述](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-product-overview/)名词解释

# 名词解释

更新时间：2023-02-01 03:56:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用限制](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/limits-1)[下一篇：新功能发布记录](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/release-notes-7)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

实例管理

数据同步

配额管理

搜索

## 实例管理

| 名称 | 说明 |
| --- | --- |

|     |     |
| --- | --- |
| 名称 | 说明 |
| 实例 | 实例是用户的一套数据配置，包括数据源结构、索引结构及其它属性配置。一个实例即一个搜索服务。 |
| 文档 | 文档是可搜索的结构化数据单元。文档包含一个或多个字段，但必须有主键字段，OpenSearch通过主键值来确定唯一的文档。主键重复则文档会被覆盖。 |
| 字段 | 字段是文档的组成单元，包含字段名称和字段内容。 |
| 插件 | 为了在导入过程中进行一些数据处理，系统内置了若干数据处理插件，可以在定义应用结构或者配置数据源时选择。 |
| 源数据 | 原始数据，包含一个或多个源字段。 |
| 源字段 | 组成源数据的最小单元，包含字段名称和字段值，可选数据类型请参见 [应用结构&索引结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/schema-of-tables-for-industry-algorithm-edition)。 |
| 索引 | 索引是用于加速检索速度的数据结构，一个实例可以创建多个索引。 |
| 组合索引 | 可将多个TEXT或SHORT\_TEXT文本类型的字段配置到同一个索引，用来做组合索引。如一个论坛搜索，需要提供基于标题(title)的搜索及基于标题(title)和内容(body)的综合搜索，那么可以将title建立title\_search索引，将title和body建立default组合索引。那么，在title\_search上查询即可实现基于标题的搜索，在default上查询即可实现基于标题和内容的综合搜索。 |
| 索引字段 | 在 [query子句](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/query-clause) 中使用，需要定义索引字段，通过索引字段来做高性能的检索召回。 |
| 属性字段 | 在 [filter](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/filter-clause)、 [sort](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sort-clause)、 [aggregate](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/aggregate-clause)、 [distinct](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/distinct-clause) 子句使用，用来实现过滤、统计等功能。 |
| 默认展示字段 | 用来做结果展示。可以通过API参数fetch\_fields来控制每次结果的返回字段，需注意在程序中配置fetch\_fields该参数后会覆盖默认展示字段配置，以程序中的fetch\_fields设置为主；若程序中不设置fetch\_fields参数则以默认展示字段为主。 |
| 分词 | 对文档进行词组切分，TEXT类型按检索单元切分，SHORT\_TEXT按单字切分。如“浙江大学”，TEXT类型会切分成2个词组：“浙江”、“大学”。SHORT\_TEXT会切分成4个词组：“浙”、“江”、“大”、“学”。 |
| term | 分词后的词组称为term。 |
| 构建索引 | 分词后会进行索引构建，以便根据查询请求，快速定位到文档。搜索引擎会构建出两种类型的链表：倒排和正排链表。 |
| 倒排 | 词组到文档的对应关系组成的链表，query子句采用这种排序方式进行查询。例如：term1->doc1,doc2,doc3；term2->doc1,doc2。 |
| 正排 | 文档到字段对应关系组成的链表，filter子句采用这种排序方式，性能略慢于倒排。例如：doc1->id,type,create\_time。 |
| 召回 | 通过查询的关键词进行分词，将分词后的词组通过查找倒排链表快速定位到文档。 |
| 召回量 | 召回得到的文档数为召回量。 |

## 数据同步

| 名称 | 说明 |
| --- | --- |

|     |     |
| --- | --- |
| 名称 | 说明 |
| 数据源 | 数据来源，目前支持阿里云RDS、MaxCompute、PolarDB的数据同步。 |
| 索引重建 | 重新构建索引。在配置/修改应用结构、数据源后需要索引重建。 |

## 配额管理

| 名称 | 说明 |
| --- | --- |

|     |     |
| --- | --- |
| 名称 | 说明 |
| 文档容量 | 实例中各个表的总文档大小累加值（不考虑字段名，字段内容按照string来计算容量）。 |
| QPS | 每秒查询请求数。 |
| LCU | LCU（逻辑计算单元）是 **衡量搜索计算能力的单位**，一个LCU代表搜索集群中1/100个核的计算能力。 |
| 快速扩缩容 | 根据实际业务需求，快速升降配，小规格可实时生效，涉及规格转换（如：共享型-集群转换为独享型-集群）需审批后生效。 |

## 搜索

| 名称 | 说明 |
| --- | --- |

|     |     |
| --- | --- |
| 名称 | 说明 |
| 排序表达式 | 排序表达式是用于控制搜索文档排序的表达式，支持基本数学运算、数学函数和内置函数。 |
| 基础排序表达式 | 对搜索结果进行第一轮的海选，按照表达式对文档进行算分，并按照算分结果进行排序。 |
| 业务排序表达式 | 对第一轮的排序结果选取前N个按照业务排序表达式进行第二轮更细节的分值计算，按照分值进行最终的排序。 |
| 结果摘要 | 文本内容一般会很长，在搜索结果展示的时候可以只展示部分匹配的内容，方便用户快速了解文档主要内容。 |
| 查询分析 | 目前支持同义词、拼写纠错、停用词、词权重等功能，理解用户的搜索意图。 |