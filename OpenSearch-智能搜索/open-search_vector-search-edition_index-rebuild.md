### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[操作指南](https://help.aliyun.com/zh/open-search/vector-search-edition/llm-operation-guide/)[表管理](https://help.aliyun.com/zh/open-search/vector-search-edition/table-management/)表的索引重建

# 表的索引重建

更新时间：2024-11-08 01:56:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：数据更新资源](https://help.aliyun.com/zh/open-search/vector-search-edition/data-update-resources)[下一篇：表数据加载策略](https://help.aliyun.com/zh/open-search/vector-search-edition/index-table-load-policy)

该文章对您有帮助吗？

反馈

索引重建是将客户全量数据来源中的数据构建成索引的过程，产出的索引成为全量索引，索引的版本称为全量版本。本文介绍OpenSearch-向量检索版中表的索引重建操作方式。

用户可在表管理，表列表中操作一栏中触发索引重建：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8098900961/p696538.png)

索引重建目前根据用户的数据源分为四种：

- MaxCompute数据源索引重建：

方式为 **全量数据重新导入**，需填写数据分区及时间戳。

![1-cn-max索引重建.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6698401371/p862604.png)


- API推送数据源索引重建， **从空数据创建**：

![api数据原索引重建.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6698401371/p863844.png)






**重要**





API推送数据源重建会将之前推送的数据清空，从指定的时间戳开始追实时数据，请谨慎操作。



索引重建时间戳对应的追增量数据（最大支持追3天的增量数据），历史数据将会被清空。


- 对象存储OSS数据源索引重建：

方式为 **全量数据重新导入**，需填写数据分区及时间戳（追API增量的时间，最大不超过3天）。

![oss.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6698401371/p863854.png)


- 数据湖构建DLF数据源索引重建：

![dlf.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6698401371/p863208.png)


触发索引重建后，可在 **变更历史** 中数据源变更，查看构建进度：

![image.png](<Base64-Image-Removed>)