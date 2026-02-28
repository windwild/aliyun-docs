### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[SDK参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdk-reference/)[JavaSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-java-sdk/)[子句及参数类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/clause-and-parameter-class-462789/)SearchParamsBuilder类

# SearchParamsBuilder类

更新时间：2023-10-24 03:12:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SearchParams类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/searchparams)[下一篇：SearchResult类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/searchresult)

该文章对您有帮助吗？

反馈

**功能简介**

SearchParams的工具类，提供了更为便捷的操作

**构造函数（1）**

```java
该类是直接通过调用该类中静态方法传参并返回生成对象
SearchParamsBuilder    SearchParamsBuilder.create(SearchParams otherSearchParams)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| otherSearchParams | SearchParams | 根据SearchParams参数对象创建SearchParamsBuilder实例对象. |

**构造函数（2）**

```java
该类是直接通过调用该类中静态方法传参并返回生成对象
SearchParamsBuilder    SearchParamsBuilder.create(Config config)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| config | Config | 根据config参数对象创建SearchParamsBuilder对象. |

* * *

**增加过滤规则（1）**

**接口定义**

```java
增加过滤规则（1）
SearchParamsBuilder        addFilter(String filter)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| filter | String | 过滤规则，例如fieldName >= 1. |

* * *

**增加过滤规则（2）**

**接口定义**

```java
增加过滤规则（2）
SearchParamsBuilder        addFilter(String filter,String operator)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| filter | String | 过滤规则，例如fieldName >= 1. |
| operator | String | 操作符，可以为 AND OR。默认为 AND. |

* * *

**添加自定义参数（键值对）**

**接口定义**

```java
添加自定义参数（键值对）
SearchParamsBuilder        addCustomParam(String key,String value)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| key | String | 参数键名 |
| value | String | 参数键值 |

* * *

**禁用某个功能**

**接口定义**

```java
禁用某个功能
SearchParamsBuilder        addDisableFunction(String function,String value)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| function | String | 功能名称 |
| value | String | 参数值 |

* * *

**添加打散条件**

**接口定义**

```java
添加打散条件
SearchParamsBuilder        addDistinct(String key,int distCount,int distTimes,boolean reserved,String distFilter,boolean updateTotalHit,double grade)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| key | String | 为用户用于做distinct抽取的字段，该字段要求为属性字段 |
| distCount | int | 为一次抽取的document数量，默认值为1 |
| distTimes | int | 为抽取的次数，默认值为1 |
| reserved | boolean | 为是否保留抽取之后剩余的结果，true为保留，false则丢弃，丢弃时totalHits的个数会减去被distinct而丢弃的个数，但这个结果不一定准确，默认为true |
| distFilter | String | 为过滤条件，被过滤的doc不参与distinct，只在后面的排序中，这些被过滤的doc将和被distinct出来的第一组doc一起参与排序。默认是全部参与distinct |
| updateTotalHit | boolean | 当reserved为false时，设置update\_total\_hit为true，则最终total\_hit会减去被distinct丢弃的数目（不一定准确），为false则不减； 默认为false |
| grade | double | 指定档位划分阈值 |

* * *

**添加一条动态摘要(summary)信息**

**接口定义**

```java
添加一条动态摘要(summary)信息
SearchParamsBuilder    addSummary(String fieldName, Integer len, String element, String ellipsis, Integer snippet)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| fieldName | String | 指定的生效的字段，此字段必需为可分词的text类型的字段. |
| len | Integer | 指定结果集返回的词字段的字节长度，一个汉字为2个字节. |
| element | String | 指定命中的query的标红标签，可以为em等. |
| ellipsis | String | 指定用什么符号来标注未展示完的数据，例如“…”. |
| snippet | Integer | 指定query命中几段summary内容. |

添加一条动态摘要(summary)信息，增加了此内容后，fieldName字段可能会被截断、飘红等。