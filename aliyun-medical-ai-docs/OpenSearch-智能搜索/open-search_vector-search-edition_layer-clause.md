### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[向量检索传统版（停售）](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-retrieval-general-edition/)[向量检索版文档3.9.0](https://help.aliyun.com/zh/open-search/vector-search-edition/documentation-of-vector-search-edition-v3-9/)[问天引擎Query DSL](https://help.aliyun.com/zh/open-search/vector-search-edition/query-dsl-of-opensearch-vector-search-edition/)[查询语法](https://help.aliyun.com/zh/open-search/vector-search-edition/query-syntax/)layer子句

# layer子句

更新时间：2025-03-13 21:58:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：virtual attribute子句](https://help.aliyun.com/zh/open-search/vector-search-edition/virtual-attribute-clause)[下一篇：analyzer子句](https://help.aliyun.com/zh/open-search/vector-search-edition/analyzer-clause)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

子句说明

子句语法

注意事项

## 子句说明

分层查询是一种查询语法的扩充，主要功能是增强查询语法对于召回过程的控制能力，让应用可以根据自己的使用场景来加速文档召回过程，提高系统整体性能，扩充的功能主要有以下几点：

- 允许用户通过某些方式选择召回的区间

- 对于不同区间可以选择召回的先后顺序

- 对于不同区间可以指定不同的query来影响召回集


## 子句语法

**名词介绍**

|     |     |
| --- | --- |
| name | description |
| seek | 查询过程中，查询到一个doc的操作 |
| docid | HA3内部对文档的编号，查询时会按docid从小到大查询。 |
| \[查询\]区间/range | 查询时一个docid的范围，这里的range是指会被查询的docid的范围。 |
| \[查询\]层/layer | 层是由一个或者多个range组成的，层主要作用是决定查询区间的优先级（把不同range放到不同层）。\[查询\]层/layer\[查询\]区间/rangedocidseekname |

**查询语法**

**选择召回区间**

对于召回区间的控制主要通过layer语法来实现，具体语法格式如下 ：

```plain
layer_clause := single_layer{;single_layer}
single_layer := range:attr1{attr1_value1,attr1_value2}*attr2{attr2_value1,[attr2_value2,attr2_value3]},quota:1000
```

一个layer子句可以由多个single\_layer组成，一个single\_layer主要有两个元素：

- quota：用于设置当前层建议召回的doc个数，这里有几个点需要注意：

- quota与rank\_size的关系：各层quota总和不会大于rank\_size，例如rank\_size=10，quota:5;quota:7，这样最终第二层的quota会被截断到5。

- 当前层quota有剩余的情况下，会自动把quota累加到下一层。

- 由于层内的每个区间之间的doc不一定满足前面的doc比后面doc要好，所以quota有两种作用机制，一种是每查找到一个doc，就检查一次quota是否有剩余，另一种是在当前层内无视quota限制（依旧被rank\_size限制），查找完当前层，最后看是否有剩余，若有剩余则累加到下一层

- 当用户显示指定layer子句的时候，每层quota默认值是0，此外quota还支持UNLIMITED的写法

- range ：用于确定当前层的doc范围，如果不写，范围区间为所有doc，及\[0,docCount)。range语法基本工作原理是通过用户给定的attribute，逐级计算最终需要seek的doc范围。需要注意的点：\
\
- 语法中用到的必须是attribute，不能是需要计算的表达式\
\
- 语法中用到的attribute必须与离线排序方式相符，否则会自动转换为查询全部区间。\
\
- 语法中用到的attribute必须要是连续出现的，不可以中间插入扩展关键字（%sorted,%docid等）\
\
- 除了attribute外我们还支持几种扩展语句：%sorted（这一层查询排过序的全量和增量），%unsorted（这一层查询未排序的数据，实时数据等），%other（除去前面层以外的范围），%docid（直接指定docid区间查询），%segmentid（直接指定segmentid区间查询），%percent（指定这个范围百分比范围的区间查询）\
\
- 如果用户在分层子句中没有指定%sorted,%unsorted关键字，引擎会自动为用户添加，默认模式是每层都是sorted，最后如果结果数不够会为用户多查一层实时数据\
\
\
**选择不同区间的不同query**\
\
对于不同查询层，可以使用不同的查询词，或者选择不同的倒排链。不同query通过分号隔开，当layer的数目大于query数目时，会自动用最后一条query填充剩余层。 基本语法如下：\
\
```plain\
query=phrase:mp3;other_index:mp4;phrase:mp3#truncate_index\
layer_clause := single_layer{;single_layer}\
single_layer := range:attr1{attr1_value1,attr1_value2}*attr2{attr2_value1,[attr2_value2,attr2_value3]},quota:1000\
```\
\
**使用示例：**\
\
本节将介绍分层查询与一些引擎提供的其他功能结合使用的场景下，如何搭配使用分层查询。\
\
​\
\
**构建索引时文档排序，查询指定召回区间**\
\
在使用离线的排序功能时，文档是全局有序的，例如，按照站点排序后，同一个站点的文档在索引中是连续的一段，当在某个站点内部查询时，可以利用这个信息来加快seek的速度，假定站点对应的attribute是site\_id，查询的站点ID为1和7，查询词为iphone：\
\
```plain\
layer=range:site_id{1,7},quota:5000\
```\
\
或者如果站点1和7中查询结果不够的情况下，用户还想查询站点5和10的结果作为补充，可以这样：\
\
```plain\
layer=range:site_id{1,7},quota:5000;range:site_id{5,10},quota:0\
```\
\
由于是希望第一层结果不够的情况下才查询第二层，所以第二层的quota设置为0（或者不写）。当然，用户还可以进行多样性召回：\
\
```plain\
layer=range:site_id{1,7},quota:4000;range:site_id{5,10},quota:1000\
```\
\
对于离线排序是多维的情况，也可以支持多维区间的定位，还是以站内查询为例，离线排序是先按站点排序，站点相同的，按照网页的静态分排序，这种时候，查询希望召回静态分大于100的网页，查询语法如下：\
\
```plain\
layer=range:site_id{1,7}*static_score{[100,]},quota:4000\
```\
\
**多query查询**\
\
在某些情况下，用户的查询即担心召回数目是否足够，又希望召回数不能太多，以免影响查询性能，比较常见的一类场景是，有多个查询词，以A，B为例：\
\
|     |     |     |\
| --- | --- | --- |\
| query方式 | 召回数 | 性能 |\
| A AND B | 最少 | 最好 |\
| A OR B | 最多 | 最差 |\
| A RANK B/B RANK A | 适中 | 中等 |\
\
上述的几种query方式，对于A和B的召回数和性能都不一样，大部分查询希望的是有较好的召回，而且召回数不需要太多，这种情况下，固定用某种查询方式，很难保证结果数和性能都适中。使用多query的方式就可以通过一次查询来解决这个问题：\
\
```plain\
cluster=general&&query=A OR B;A RANK B;A AND B&&layer=quota:1000;quota:1000;quota:1000\
```\
\
这种查询方式可以兼顾召回文档数目和性能，对于查询词的关联程度也有比较大的提升（对于大召回可以命中一些A AND B的结果，对于小召回可以通过A OR B来尽可能多召回）。\
\
**需要考虑时效性的查询**\
\
有时候用户会希望查询结果的时效性比较好，在这种情况下用户会希望先查询实时的无序索引，之后再查询全量和增量的有序索引，用户也可以在有序索引中指定先查询后面的一部分数据，再查前面的一部分数据，可以用%percent关键字实现\
\
例如用户想要先查询时效性最好的实时索引，结果不够的话查询有序索引中后50%的doc，最后查询前50%的doc，查询词为iphone：\
\
```plain\
&&layer=range:%unsorted,quota:5000;range:%sorted*service_id{1,3}*%percent{[50,100)},quota:0;range:%sorted*service_id{1,3}*%percent{[0,50)},quota:0\
注：percent关键字中可以指定不同多个区间，区间是左闭右开的\
```\
\
## 注意事项\
\
- layer子句是可选子句