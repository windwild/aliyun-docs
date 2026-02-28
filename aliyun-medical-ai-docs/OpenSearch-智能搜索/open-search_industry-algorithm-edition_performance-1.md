### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/) [OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/) [实践教程](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/best-practices-2/) 性能篇

# 性能篇

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：定制排序模型](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/custom-rank-model)[下一篇：数据推送](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-push)

该文章对您有帮助吗？

反馈

- 使用API/SDK推送数据有次数及大小限制，推荐将文档批量打包发送。使用RDS自动同步数据有TPS及大小限制。具体限制以及更多相关详情请参见 [数据推送](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-push "")。

- 搜索查询的效果主要跟query关键词中命中的文档数有关，命中的文档数越多，系统要进行的计算就越多，那么耗时就会越高。因此，优化的一个重要手段就是尽量降低query召回的文档数。详情请参见 [搜索](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/document-search "")。

- 您可以通过 [多表join引发的数据同步延迟](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-synchronization-latency-caused-by-multi-table-joins "") 了解多表情况下的一些注意事项。