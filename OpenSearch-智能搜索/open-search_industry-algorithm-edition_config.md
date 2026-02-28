### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[SDK参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdk-reference/)[JavaSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-java-sdk/)[子句及参数类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/clause-and-parameter-class-462789/)Config类

# Config类

更新时间：2024-01-02 03:02:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Command类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/command)[下一篇：Distinct类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/distinct)

该文章对您有帮助吗？

反馈

**功能简介**

config 可以指定查询结果的起始位置、返回结果的数量、展现结果的格式、参与精排表达式文档个数等。（注：Config子句中的 rerank\_size 参数，放在Rank类方法中进行设置）

**构造函数（1）**

```java
有参构造函数，在创建对象时指定应用名称列表
Config(List<String> appNames)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| appNames | List<String> | 应用名称列表 |

**构造函数（2）**

```java
无参构造函数
Config()
```

* * *

**设置返回结果的偏移量（start）**

**接口定义**

```java
设置返回结果的偏移量(start)
Config    setStart(int start)
```

**参数描述**

| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| start | int | 否 | \[0, 5000\] | 0 | 从搜索结果中第start个文档开始返回 |

* * *

**获取返回结果的偏移量（start）**

**接口定义**

```java
获取返回结果的偏移量(start)
int    getStart()
```

**返回结果**

- start参数值


* * *

**设置当前返回结果集的文档个数（hit）**

**接口定义**

```java
设置当前返回结果集的文档个数(hit)
Config    setHits(int hits)
```

**参数描述**

| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| hits | int | 否 | \[0, 500\] | 10 | 返回文档的最大数量 |

* * *

**获取当前设定的结果集的文档条数（hit）**

**接口定义**

```java
获取当前设定的结果集的文档条数(hit)
int    getHits()
```

**返回结果**

- int 获取设置的返回结果条数


* * *

**设置返回的数据格式类型（format）**

**接口定义**

```java
设置返回的数据格式类型(format)
Config    setSearchFormat(SearchFormat.FULLJSON)
```

**参数描述**

| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| format | string | 否 | xml、JSON、fulljson三种格式可选 | JSON | 返回的文档格式，fulljson：比JSON类型多输出一些节点，如variableValue等。 |

* * *

**获取返回的数据格式类型（format）**

**接口定义**

```java
获取返回的数据格式类型(format)
SearchFormat    getSearchFormat()
```

**返回结果**

- SearchFormat 类型枚举值


* * *

**设置搜索返回的索引字段列表（fetch\_fields）**

**接口定义**

```java
设置搜索返回的索引字段列表(fetch_fields)
Config    setFetchFields(List<String> fetchFields)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| fetchFields | List<String> | 需展示字段名称 |

* * *

**获取搜索结果包含的字段列表（fetch\_fields）**

**接口定义**

```java
获取搜索结果包含的字段列表(fetch_fields)
List<String>    getFetchFields()
```

**返回结果**

- List<String> 获取需展示字段名称


* * *

**设定当前的kvpairs**

**接口定义**

```java
设定当前的kvpairs
config    setKvpairs(String kvpairs)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| kvpairs | String | kvpairs内容 |

* * *

**获取当前的kvpairs**

**接口定义**

```java
获取当前的kvpairs
String    getKvpairs()
```

**返回结果**

- kvpairs内容


* * *

**设定当前的路由值**

**接口定义**

```java
设定当前的路由值
Config    setRouteValue(String routeValue)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| routeValue | String | 路由参数值 |