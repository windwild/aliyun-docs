### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[快速入门](https://help.aliyun.com/zh/open-search/vector-search-edition/getting-started/)[向量索引](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-index/)CagraHnsw配置

# CagraHnsw配置

更新时间：2025-10-28 22:27:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CAGRA配置](https://help.aliyun.com/zh/open-search/vector-search-edition/gpu-algorithm-cagra-configuration)[下一篇：DiskANN配置](https://help.aliyun.com/zh/open-search/vector-search-edition/diskann)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

build参数

search参数

## build参数

| **参数值** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数值** | **类型** | **默认值** | **说明** |
| proxima.cagra\_hnsw.index.graph\_degree | int | 64 | 图索引中每个节点（向量）的邻居数量。该参数影响索引质量和查询性能。增加该值通常会提高召回率，但会增加索引构建时间和内存占用，并可能降低查询QPS。<br>取值约束：必须是 32 的倍数。 |
| proxima.cagra\_hnsw.index.intermediate\_graph\_degree | int | 128 | 最终产出图索引前需要对点的邻居进行裁剪，此参数用于控制裁剪前点的邻居数量，proxima.cagra\_hnsw.index.graph\_degree为裁剪后的邻居数量。<br>取值约束：必须是 32 的倍数，且必须大于或等于 `proxima.cagra_hnsw.index.graph_degree`。 |

## search参数

| **参数名** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数名** | **类型** | **默认值** | **说明** |
| proxima.hnsw.searcher.ef | uint32 | 500 | 用于控制在线检索时考察的子图范围大小。该值越大，召回越高，性能越差，建议取值\[100,1000\]。 |
| proxima.hnsw.searcher.max\_scan\_ratio | float | 无 | 用于控制在线检索时扫描点的比例，该值越大召回越高，性能越差。 |
| proxima.hnsw.searcher.brute\_force\_threshold | uint32 | 无 | 用于控制在线检索时最少扫描的点的个数，如果该数值大于单分片的文档个数，查询退化为暴力检索。 |