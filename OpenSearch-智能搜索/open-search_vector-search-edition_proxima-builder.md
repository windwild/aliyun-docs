### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[向量检索传统版（停售）](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-retrieval-general-edition/)[向量检索版文档3.9.0](https://help.aliyun.com/zh/open-search/vector-search-edition/documentation-of-vector-search-edition-v3-9/)[索引](https://help.aliyun.com/zh/open-search/vector-search-edition/indexes/)[向量索引](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-indexes-2/)Proxima Builder

# Proxima Builder

更新时间：2023-08-30 04:44:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：向量索引](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-indexes-2/)[下一篇：Proxima Searcher](https://help.aliyun.com/zh/open-search/vector-search-edition/proxima-searcher)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

LinearBuilder

QcBuilder

HnswSearcher

## **LinearBuilder**

| 参数名 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| 参数名 | 类型 | 默认值 | 说明 |
| proxima.linear.builder.column\_major\_order | string | false | 构建的时候特征用行排（false）/列排（true） |

## **QcBuilder**

| 参数名 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| 参数名 | 类型 | 默认值 | 说明 |
| proxima.qc.builder.train\_sample\_count | uint32 | 0 | 指定训练数据量，如果为0则使用全部数据 |
| proxima.qc.builder.thread\_count | uint32 | 0 | 构建时开启线程数量，设置为0时为cpu核数 |
| proxima.qc.builder.centroid\_count | string | 可选 | 聚类中心点参数，支持层次聚类。层之间用“\*”分隔。<br>一层聚类示例：1000<br>两层示例：100\*100<br>如果使用两层中心点，一般第一次中心点数量比第二层多，效果更好。经验值是第一层是第二层10倍。<br>未配置时，系统会自动推导出合适的中心点个数，建议由系统自动推导。 |
| proxima.qc.builder.cluster\_class | string | OptKmeansCluster | 指定聚类方法，更多参见 [聚类文档](https://help.aliyun.com/zh/open-search/vector-search-edition/proxima-cluster-parameters "")。 |
| proxima.qc.builder.cluster\_auto\_tuning | bool | false | 指定是否开启中心点数目自适应 |
| proxima.qc.builder.cluster\_params\_in\_level\_ | IndexParams | - | 指定聚类方法需要的参数，详见 [聚类文档](https://help.aliyun.com/zh/open-search/vector-search-edition/proxima-cluster-parameters "")。<br>每层需要分别制定，从1开始。<br>比如第一层的key是proxima.qc.builder.cluster\_params\_in\_level\_1 |
| proxima.qc.builder.optimizer\_class | string | HcBuilder | 针对中心点部分的优化器，用于提升分类时的精度，后续在线候选中心点部分的查询均基于此方法进行，比如此处配置了HcBuilder，在线部分候选中心点查询时会用HcSearcher来进行查询，目前该参数可选择HcBuilder、HnswBuilder、SsgBuilder和LinearBuilder等方法 |
| proxima.qc.builder.optimizer\_params | IndexParams | - | optimize方法对应的构建和检索参数，比如optimizer配置了Hnswbuilder，那么该处参数可配置为：<br>proxima.hnsw.builder.max\_neighbor\_count: 100 proxima.hnsw.searcher.max\_scan\_ratio: 0.1 |
| proxima.qc.builder.converter\_class | string | - | 如果Measure是InnerProduct，会自动进行Mips转换操作，使用L2检索 |
| proxima.qc.builder.converter\_params | IndexParams | - | proxima.qc.builder.converter\_class 初始化参数 |
| proxima.qc.builder.quantizer\_class | string | - | 配置量化器，默认不使用量化器。可选有 Int8QuantizerConverter, HalfFloatConverter, DoubleBitConverter。一般配置量化器可提升性能，减少索引大小，召回视情况有所损失 |
| proxima.qc.builder.quantizer\_params | IndexParams | - | 配置上面量化器相关参数 |
| proxima.qc.builder.optimizer\_quantizer\_class | string | - | 配置对中心点进行量化的 converter 名称 |
| proxima.qc.builder.optimizer\_quantizer\_params | IndexParams | - | 对中心点进行量化的 converter 参数 |
| proxima.qc.builder.quantize\_by\_centroid | bool | False | 使用proxima.qc.builder.quantizer\_class时，是否按中心点进行量化。目前仅支持 proxima.qc.builder.quantizer\_class 为 Int8QuantizerConverter 的情况 |
| proxima.qc.builder.store\_original\_features | bool | False | 是否保留原始特征。使用proxima.qc.builder.quantizer\_class 时，IndexProvider 获取的特征是量化后的，需要开始此选项，才能获取原始特征 |

## HnswSearcher

| **参数名** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数名** | **类型** | **默认值** | **说明** |
| proxima.hnsw.builder.max\_neighbor\_count | uint32 | 100 | 指定图中节点最大邻居数。该值越大，代表图的连通性越好，相应的构图成本和索引size也会增加。 |
| proxima.hnsw.builder.efconstruction | uint32 | 500 | 指控制图构建过程中近邻扫描区域大小，该值越大，离线构图质量越好，索引构建越慢。建议初始从400配置 |
| proxima.hnsw.builder.thread\_count | uint32 | 0 | 构建时开启线程数量，设置为0时为cpu核数 |