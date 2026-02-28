### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-召回引擎版](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/)[开发指南](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/developer-guide/)[Java SDK](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/retrieval-engine-edition-sdk-for-java/)[SDK客户端](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/recall-engine-sdk-clients/)Client类

# Client类

更新时间：2024-02-28 05:06:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Config类](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/config-class)[下一篇：PushDocumentsRequestModel类](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/pushdocumentsrequestmodel-class)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能简介

类安全性描述

构造函数

参数描述

push方式推送数据

接口定义

参数描述

异常描述

search方式查询数据

接口定义

参数描述

异常描述

## 功能简介

Client 类功能及方法描述，该客户端主要用于推送/搜索数据操作。

## 类安全性描述

Client 类非线程安全

## 构造函数

Client(Config config)

### 参数描述

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| config | [Config](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/config-class "") | Config类对象 |

## push方式推送数据

### 接口定义

```json
PushDocumentsResponseModel pushDocuments(String dataSourceName, String keyField, PushDocumentsRequestModel request)
```

### 参数描述

|     |     |     |
| --- | --- | --- |
| **参数名称** | **类型** | **描述** |
| dataSourceName | String | 索引标配名 |
| keyField | String | 索引表主键 |
| request | PushDocumentsRequestModel | 推送文档结构 |

### 异常描述

- Exception


## search方式查询数据

### 接口定义

```json
SearchResponseModel Search(SearchRequestModel request)
```

### 参数描述

|     |     |     |
| --- | --- | --- |
| **参数名称** | **类型** | **描述** |
| request | [SearchRequestModel](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/searchrequestmodel-class "") | SearchRequestModel类型 |

### 异常描述

- Exception