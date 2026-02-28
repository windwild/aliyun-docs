### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[SDK参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdk-reference/)[JavaSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-java-sdk/)[子句及参数类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/clause-and-parameter-class-462789/)Suggest类

# Suggest类

更新时间：2024-01-02 03:02:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SortField类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sortfield)[下一篇：Summary类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/summary-2)

该文章对您有帮助吗？

反馈

**功能简介**

Suggest 类功能方法描述，主要用户下拉提示操作

**下拉提示实现依赖简述**

通过代码实现下拉提示功能，需要依赖多个类组合实现，主要涉及的类有 Suggest 、SearchParams 、SearcherClient（依赖其它2个类） 、Config 等类，具体代码实现参考标准版查询部分中的下拉提示代码Demo.

**构造函数（1）**

```java
有参构造函数，在创建对象时指定下拉提示名称
Suggest(String suggestName)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| suggestName | String | 下拉提示名称 |

**构造函数（2）**

```java
无参构造函数
Suggest()
```

* * *

**设置下拉名称**

**接口定义**

```java
设置下拉名称
Suggest setSuggestName(String suggestName)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| suggestName | String | 下拉提示名称 |

* * *

**获取下拉提示名称**

**接口定义**

```java
获取下拉提示名称
String    getSuggestName()
```

**返回结果**

- String 下拉提示名称


* * *

**设置下拉提示搜索关键词**

**接口定义**

依赖

SearchParams

类对象中的 setQuery( String query ) 方法实现，需参考 SearchParams 类方法描述

* * *

**设置下拉提示结果条数**

**接口定义**

依赖

Config

类对象中的 setHits( int hits ) 方法实现，需参考 Config 类方法描述