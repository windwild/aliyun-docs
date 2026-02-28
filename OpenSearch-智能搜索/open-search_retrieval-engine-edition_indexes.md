### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-召回引擎版](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/)[引擎技术文档](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/documentation-of-retrieval-engine-edition-v3-9-0/)索引

# 索引

更新时间：2024-12-05 05:11:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：小语种分析器](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/text-analyzers-for-languages-except-for-chinese-and-english)[下一篇：倒排索引介绍](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/introduction-to-inverted-indexes)

该文章对您有帮助吗？

反馈

每个Document都是由多个field组成，每个field中包含一系列的词语，构建索引的目的是为了加快检索的速度，根据映射关系方向的不同，索引可以分为：

- 倒排索引（index）倒排索引存储了从单词到DocID的映射关系，形如：词-->（Doc1,Doc2,...,DocN）倒排索引主要用在检索中，它能快速的定位用户查询到关键字对应的Document。

- 正排索引（attribute）正排索引存储从DocID到field的映射关系，形如：DocID-->（term1,term2,...termn）正排索引分单值和多值两种，单值attribute由于长度是固定的（不包括string类型），因此查找效率高，而且可以支持更新。多值attribute表示某个field中有多个数据（数量不固定），由于长度不确定，因此查找效率相较与单值更慢，而且不能支持更新。正排索引主要是在查询到了某个Document后，根据docid值能快速获取到其attribute用来统计、排序、过滤中。目前引擎支持的正排字段基本类型包括：INT8（8位有符号数字类型）, UINT8（8位无符号数字类型）, INT16（16位有符号数字类型）, UINT16（16位无符号数字类型）, INTEGER（32位有符号数字类型）, UINT32（32位无符号数字类型）, INT64（64位有符号数字类型）, UINT64（64位无符号数字类型）, FLOAT（32位浮点数）, DOUBLE（64位浮点数）, STRING（字符串类型）多值的attribute只是一个field中可能出现数量不确定的单值attribute，引擎对上述的单值类型attribute都支持对应的多值attribute（例如multi\_int8，multi\_string）。

- 摘要（summary）summary的存储形式与attribute类似，但是summary是将一个Document对应的多个field存储在一起，并且建立映射，所以能很快从docid定位到对应的summary内容。summary主要是用于结果的展示，一般而言summary的内容都比较大，对于每次查询而言不适合取过多的summary，只有最终需要展示结果的Document会取到对应的summary。由于summary过大，引擎在存储summary时提供压缩的机制，在schema中配置summary压缩，那么引擎在存储时会用zlib压缩后再存储，读取时引擎会先解压，再返回给用户。