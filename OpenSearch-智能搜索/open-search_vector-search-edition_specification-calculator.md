### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[产品概述](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-search-product-overview/)[产品计费](https://help.aliyun.com/zh/open-search/vector-search-edition/billing/)规格计算器

# 规格计算器

更新时间：2025-03-03 01:56:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：向量检索版计费概述](https://help.aliyun.com/zh/open-search/vector-search-edition/billing-overview-of-vector-search-edition)[下一篇：购买OpenSearch向量检索版实例](https://help.aliyun.com/zh/open-search/vector-search-edition/buy-opensearch-vector-retrieve-version-of-the-instance)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

购买服务

基础情况

向量数据情况

查询情况

向量检索版针对用户实例预算问题，提供了资源计算器，新接入的实例可通过计算器对实例资源进行预算参考。切换向量检索版，单击 **创建实例**，在右侧会展示 **规格计算器**。

## **购买服务**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0172961171/p786871.png)

单击 **规格计算器**：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0172961171/p786872.png)

## **基础情况**

1. 实例所在区域：用户需要创建引擎的区域。

2. 是否有容灾需求：用户是否需要容灾需求，可下拉选择：有、无。


## **向量数据情况**

1. 向量数据条数：用户要写入引擎向量数据doc数。

2. 向量维度：用户写入引擎的向量维度。

3. 向量算法：可根据需求进行选择，目前支持三种算法：


1. HNSW：基于图的向量检索算法，召回率极高且性能很好，内存及存储占用与Linear相当，在低维度和高维度向量数据集上均有很好的表现，适用于大多数向量检索场景。

2. QC：基于量化聚类的向量检索算法，召回结果正确率极高，占用资源较少，性能较好，在低维度向量数据集上有更好表现,内存及储存占用一般只有Linear和HNSW的1/4，适用于对召回率没有严苛要求的大数据量检索场景。

3. Linear：线性检索，即暴力检索，召回结果完全正确，占用资源多性能较差，通常适用于小数据集上（1W条数据量以内）的精确检索。


## **查询情况**

1. 平均QPS：用户接入引擎的流量QPS

2. 期望搜索平均响应时间：用户期望召回结果的平均耗时，单位下拉可选，s或ms。


上述填写完毕，点击 **运行计算**：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0172961171/p786873.png)

运算后，平台会推荐出需要购买的查询节点以及数据节点的规格及副本数，如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0172961171/p786874.png)

用户可根据推荐的规格资源进行购买机器。