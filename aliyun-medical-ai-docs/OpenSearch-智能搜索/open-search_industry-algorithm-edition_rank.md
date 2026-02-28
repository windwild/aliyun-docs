### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[SDK参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdk-reference/)[JavaSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-java-sdk/)[子句及参数类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/clause-and-parameter-class-462789/)Rank 类

# Rank 类

更新时间：2024-01-02 03:02:49

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Order类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/order)[下一篇：SearchParams类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/searchparams)

该文章对您有帮助吗？

反馈

**功能简介**

Rank 表达式类及rerank\_size参数方法描述

**构造函数**

```java
无参构造函数
Rank()
```

**设置粗排表达式名称**

**接口定义**

```java
设置粗排表达式名称
Rank    setFirstRankName(String firstRankName)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| firstRankName | String | 粗排表达式名称 |

**获取粗排表达式名称**

**接口定义**

```java
获取 粗排表达式名称
String    getFirstRankName()
```

**返回结果**

- String 粗排表达式名称


**设置精排表达式名称**

**接口定义**

```java
设置精排表达式名称
Rank    setSecondRankName(String secondRankName)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| secondRankName | String | 精排表达式名称 |

**设置排序表达式类型**

**接口定义**

```java
设置排序表达式类型
Rank setSecondRankType(RankType secondRankType)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| secondRankType | RankType | 排序表达式类型（枚举）：<br>- EXPRESSION（默认）：策略排序<br>  <br>- CAVA\_SCRIPT：CAVA脚本 |

**获取精排表达式名称**

**接口定义**

```java
获取 精排表达式名称
String    getSecondRankName()
```

**返回结果**

- String 精排表达式名称


**设置参与精排个数**

**接口定义**

```java
设置参与精排个数，该参数对应于config子句中的rerank_size参数
Rank    setReRankSize(int reRankSize)
```

**参数描述**

| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 参数 | 类型 | 必需 | 取值范围 | 默认值 | 描述 |
| rerank\_size | int | 否 | \[0, 2000\] | 200 | 参与精排个数 |

**获取参与精排个数**

**接口定义**

```java
获取 参与精排个数
int    getReRankSize()
```

**返回结果**

- int 参与精排个数