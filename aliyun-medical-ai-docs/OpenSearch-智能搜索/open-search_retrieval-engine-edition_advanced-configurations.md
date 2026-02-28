### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-召回引擎版](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/)[召回引擎传统版（停售）](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/recall-engine-legacy-edition/)[实例管理](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/instance-management/)[配置中心](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/recall-engine-tradition-configuration-center/)高级配置

# 高级配置

更新时间：2025-03-07 05:30:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：子文档（sub\_doc）配置](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/sub-document-sub-doc-configuration)[下一篇：查询配置](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/query-configurations)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

添加自定义干预词条

删除词典配置版本

注意事项

本文为您介绍高级配置中的词典配置。

## 简介

高级配置中的词典配置主要为用户提供自定义分词的功能，当系统提供的分词器对query的分词结果无法满足用户的业务需求时，可以通过配置对应分词器的自定义词典来干预分词结果，以达到用户的目的

系统默认为用户提供两个词典配置版本，后缀为\_offline\_adv\_v1的词典配置版本由系统默认创建，其中包含6种类型的分词器词典：

| **词典类型** |
| --- |

|     |
| --- |
| **词典类型** |
| 中文-通用分析器.dict |
| 行业-电商通用分析器.dict |
| 行业-游戏通用分析器.dict |
| 行业-教育题目分析器.dict |
| 行业-内容文娱分析器.dict |
| 行业-英文电商通用.dict |
| 行业－内容IT分析.dict |
| 中文－电商分析.dict |

后缀为\_offline\_adv\_edit的高级配置版本可由用户进行“编辑”，添加新分词词条后，点击“发布”，系统会自动生成一个新的高级配置版本，后缀依次递增，如第二次发布时高级配置版本名称后缀为\_offline\_adv\_v2。各个高级配置版本之间可由备注显示区分用途。

## 添加自定义干预词条

**分词bad case**：用户某条doc内容为“乒乓球拍卖完了”，当用户搜索“球拍”时无法将其召回，原因是因为“乒乓球拍卖完了”分词后的内容为“乒乓/球/拍卖/完了”，由于搜索query分词后的item与doc内容分词后的item无法完全匹配，导致该doc无法通过“球拍”召回。

**解决方法**：通过添加自定义分词词条，“乒乓球拍”=>“乒乓球拍”，解决分词的bad case，步骤如下：

1. 在 **配置中心 \> 高级配置** 页面中，找到后缀为“\_offline\_adv\_edit”的高级配置版本，点击操作中的“编辑”按钮：


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p788922.png)

2. 找到对应索引表中索引引用的分词类型，点击“编辑”：


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p788925.png)

3. 添加自定义词条支持两种方式：

1. 界面文本框输入自定义干预词条：乒乓球拍 ，点击“确定”：![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789017.png)

2. 界面上传新增词典文件，上传文件内容后，可继续在界面框内进行编辑，点击“确定”：

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789022.png)

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789020.png)

      **注意文件限制：文件大小需小于5M，文件格式为.dict或.txt**。

词条支持以下两种格式：

1）干预词条不需要继续切分：一行一个词，utf8编码，不能有空格或者\\t符号，例如：

```json
开放搜索
opensearch
```

2）干预词条需要继续切分：原始词和切分之后的词，utf8编码，之间用\\t分割，切分词之间用空格分隔，例如：

```java
开放搜索	开放 搜索
opensearch	open search
```

4. 发布新编辑的词典配置版本：


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789023.png)

为词典配置新版本添加备注：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1875770861/p622725.png)

发布后，系统自动生成一个新的词典配置版本：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789025.png)

5. 为了使配置在集群中生效，需要推送离线配置并做触发索引重建：


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789027.png)

可在 **运维中心 \> 变更历史** 中，数据源变更中查看全量进度：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789028.png)

索引重建成功后，线上查询即可生效。

## 删除词典配置版本

状态为“未使用”的词典配置版本，可以直接在高级配置 \> 词典配置界面删除：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3848312171/p789080.png)

状态为“使用中”的词典配置版本，只可进行“查看”，若需删除，请在 **运维中心** > **运维管理** > **配置更新** 中选择“ **词典配置版本**”时引用其他词典配置版本，然后推送配置并触发索引重建，索引重建后，当该“ **词典配置版本**”处于“未使用”的状态时即可删除。

## 注意事项

- 每个实例只能存在一个编辑中的词典配置版本；

- 线上使用的版本只可查看，无法删除；

- 高级配置目前支持词典配置和查询配置