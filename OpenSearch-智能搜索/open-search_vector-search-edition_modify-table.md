### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[操作指南](https://help.aliyun.com/zh/open-search/vector-search-edition/llm-operation-guide/)[表管理](https://help.aliyun.com/zh/open-search/vector-search-edition/table-management/)修改表

# 修改表

更新时间：2025-03-03 20:39:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenLake-DLF向量数据同步至阿里云OpenSearch](https://help.aliyun.com/zh/open-search/vector-search-edition/data-lake-construction-dlf)[下一篇：删除表](https://help.aliyun.com/zh/open-search/vector-search-edition/delete-table)

该文章对您有帮助吗？

反馈

本文介绍通过编辑表操作修改数据分片、数据源、字段配置及索引结构。

此处以 **修改数据分** 片为例，演示如何修改表，以及如何让修改的内容在线生效：

1. 在表管理页找到需要修改的表，单击 **编辑**：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2898900961/p696527.png)

2. 表基础信息编辑，修改数据分片数：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2898900961/p696528.png)

**注意**：

   - 分片数设置时，请填写不超过256的正整数， 用于提升全量构建速度、单次查询性能。（部分存量实例，仍需各索引表分片数保持一致；或至少一个索引表分片数为1，其余索引表分片数一致）

   - 数据节点使用达到上限时，无法进行扩容分片操作，需要进行扩容数据节点，扩容完成后保证 **表的分片个数<=数据节点个数** 时才能进行扩分片操作。扩容操作可参考 [扩缩容](https://help.aliyun.com/zh/open-search/vector-search-edition/change-the-configurations-of-an-instance "")。
3. 校验数据源信息后，单击 **下一步**：

![数据同步.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0938489271/p862620.png)



**说明**





API数据源直接单击 **下一步**，MaxCompute数据源、对象存储OSS数据源与数据湖构建（DLF）数据源默认不变更全量数据来源信息，如有需要选择变更后填写配置信息通过 **数据来源校验** 后单击 **下一步**。

4. 字段配置，如有需求可在此处调整字段类型、高级配置等信息，调整后单击 **下一步**：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7453718171/p809947.png)

5. 索引结构配置，可在此处开启文档过期清理配置与调整向量索引配置，调整后单击 **下一步**：

![索引结构cn.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0938489271/p862616.png)

6. 确认编辑，根据全量数据来源填写后单击确认：


   - MaxCompute数据源：索引重建方式可选择 **全量数据重新导入。**

   - 对象存储OSS数据源：索引重建方式可选择 **全量数据重新导入。**

   - API推送数据源：索引重建方式可选择 **空数据。**

   - 数据湖构建（DLF）数据源：索引重建方式可选择 **全量数据重新导入。**



     **重要**





     - MaxCompute的数据源修改表后，索引重建会重新拉取配置的分区数据 \+ 时间戳配置的增量API数据。

     - **空数据** 的索引重建方式会将之前推送的数据清空，从指定的时间戳开始追实时数据，请谨慎操作。

     - **时间戳**：表示索引重建的新全量版本回溯多久的API增量数据，系统最大支持追溯3天的API增量数据。


![5-cn-表编辑.png](<Base64-Image-Removed>)

7. 可以在变更历史>数据源变更页查看变更进度：

![image.png](<Base64-Image-Removed>)



**说明**





修改表并索引重建后会生成两个FSM，推送配置和手动触发全量，这两个流程全部结束后，本次变更才会生效。