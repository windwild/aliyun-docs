### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[SDK参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdk-reference/)[JavaSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-java-sdk/)[子句及参数类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/clause-and-parameter-class-462789/)Distinct类

# Distinct类

更新时间：2023-10-24 03:12:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Config类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/config)[下一篇：Order类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/order)

该文章对您有帮助吗？

反馈

**功能简介**

Distinct 类功能及方法描述

**构造函数（1）**

```java
无参构造函数
Distinct()
```

**构造函数（2）**

```java
创建对象时指定dist_key参数值
Distinct(String key)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| key | String | 为用户用于做distinct抽取的字段，该字段要求为属性字段 |

* * *

**设置dist\_key参数**

**接口定义**

```java
设置dist_key参数
Distinct    setKey(String key)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| key | String | 为用户用于做distinct抽取的字段，该字段要求为属性字段 |

* * *

**获取dist\_key参数值**

**接口定义**

```java
获取dist_key参数值
String    getKey()
```

**返回结果**

- dist\_key参数值


* * *

**设置dist\_count参数**

**接口定义**

```java
设置dist_count参数
Distinct    setDistCount(int distCount)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| distCount | int | 为一次抽取的document数量，默认值为1 |

* * *

**获取dist\_count参数值**

**接口定义**

```java
获取dist_count参数值
int    getDistCount()
```

**返回结果**

- dist\_count参数值


* * *

**设置dist\_times参数**

**接口定义**

```java
设置dist_times参数
Distinct    setDistTimes(int distTimes)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| distTimes | int | 为抽取的次数，默认值为1 |

* * *

**获取dist\_times参数值**

**接口定义**

```java
获取dist_times参数值
int    getDistTimes()
```

**返回结果**

- dist\_times参数值


* * *

**设置reserved参数**

**接口定义**

```java
设置reserved参数
Distinct    setReserved(boolean reserved)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| reserved | boolean | 为是否保留抽取之后剩余的结果，true为保留，false则丢弃，丢弃时totalHits的个数会减去被distinct而丢弃的个数，但这个结果不一定准确，默认为true |

* * *

**设置update\_total\_hit参数**

**接口定义**

```java
设置update_total_hit参数
Distinct    setUpdateTotalHit(boolean updateTotalHit)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| updateTotalHit | boolean | 当reserved为false时，设置update\_total\_hit为true，则最终total\_hit会减去被distinct丢弃的数目（不一定准确），为false则不减； 默认为false |

* * *

**设置dist\_filter参数**

**接口定义**

```java
设置dist_filter参数
Distinct    setDistFilter(String distFilter)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| distFilter | String | 为过滤条件，被过滤的doc不参与distinct，只在后面的排序中，这些被过滤的doc将和被distinct出来的第一组doc一起参与排序。默认是全部参与distinct |

* * *

**获取dist\_filter参数值**

**接口定义**

```java
获取dist_filter参数值
String    getDistFilter()
```

**返回结果**

- dist\_filter参数值


* * *

**设置grade参数**

**接口定义**

```java
设置grade参数
Distinct    setGrade(double grade)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| grade | double | 指定档位划分阈值 |

* * *

**获取grade参数值**

**接口定义**

```java
获取grade参数值
String    getGrade()
```

**返回结果**

- grade参数值