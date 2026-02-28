### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[向量检索传统版（停售）](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-retrieval-general-edition/)[实例管理](https://help.aliyun.com/zh/open-search/vector-search-edition/instance-management-2/)[运维中心](https://help.aliyun.com/zh/open-search/vector-search-edition/operation-and-maintenance-center-1/)[运维管理](https://help.aliyun.com/zh/open-search/vector-search-edition/operation-and-maintenance-management-1/)配置更新

# 配置更新

更新时间：2025-05-22 04:24:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：修改索引表](https://help.aliyun.com/zh/open-search/vector-search-edition/modify-an-index-table-1)[下一篇：索引重建](https://help.aliyun.com/zh/open-search/vector-search-edition/perform-reindexing-1)

该文章对您有帮助吗？

反馈

当用户执行了添加数据源、新增索引表/修改索引表、新增/更新高级配置时，需要在运维管理界面进行 **配置更新**，再 **索引重建** 才会生效：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8614770861/p621904.png)

1. 选择需要更新的“索引结构版本”，包括对应的数据源中的索引表的版本，选择需要更新的“高级配置版本”，选择是否需要自动触发索引重建：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8614770861/p621905.png)

**注意**：

   - 一次配置更新，只能选择一个数据源，一个数据源中可选择多个索引表进行配置更新：

     - 如果有多个集群，配置更新默认所有集群生效；

     - 如果选择自动触发索引重建，并且配置的MaxCompute数据源，则需要选择具体的分区进行索引重建：

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8614770861/p621903.png)

     - 如果选择自动触发索引重建，并且配置的是API推送数据源，数据来源可以选择“空数据”和“ [从索引中恢复数据](https://help.aliyun.com/zh/open-search/vector-search-edition/restore-data-from-an-index-version "")”，如需保留当前全量版本的全部数据，请选择从 **索引中恢复数据** 并选择数据恢复版本：

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2781125661/p499428.png)



       **重要**





       - 时间戳配置需满足校验规则：不可以填写推送API数据源之后的时间点
2. 推送配置后，可在运维中心>变更历史中查看数据源变更的生效进度：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8614770861/p621906.png)


全量完成后，推送的配置才会生效，线上即可使用。