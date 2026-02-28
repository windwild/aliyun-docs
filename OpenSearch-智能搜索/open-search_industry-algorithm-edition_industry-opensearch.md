### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[SDK参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdk-reference/)[JavaSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-java-sdk/)[SDK客户端](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-sdk-client/)OpenSearch类

# OpenSearch类

更新时间：2025-02-18 01:55:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DocumentClient类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-documentclient)[下一篇：OpenSearchClient类](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-opensearchclient)

该文章对您有帮助吗？

反馈

**功能简介**

OpenSearch 类功能及方法描述，主要用于构建OpenSearchClient对象

**类安全性描述**

OpenSearch 类线程安全

**构造函数（1）**

```java
有参构造函数，创建对象时指定参数
OpenSearch(String accesskey, String secret, String host)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| accesskey | String | 用户的accesskey，从网站中可以获得此信息。 |
| secret | String | 用户的 secret，从网站中可以获得此信息。 |
| host | String | 指定请求的host地址 |

**构造函数（2）**

```java
无参构造函数
OpenSearch()
```

* * *

**设置 AccessKey 参数**

**接口描述**

```java
设置 AccessKey 参数
OpenSearch    setAccessKey(String accesskey)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| accesskey | String | 用户的accesskey，从网站中可以获得此信息。 |

* * *

**获取 AccessKey 参数**

**接口定义**

```java
获取 AccessKey 参数
String    getAccessKey()
```

**返回结果**

- String AccessKey 参数值


* * *

**设置 Secret 参数**

**接口描述**

```java
设置 Secret 值
OpenSearch    setSecret(String secret)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| secret | String | 用户的 secret，从网站中可以获得此信息。 |

* * *

**获取 Secret 参数**

**接口定义**

```java
获取 Secret 参数
String    getSecret()
```

**返回结果**

- String Secret 参数值


* * *

**设置 Host 参数**

**接口描述**

```java
设置 Host 值
OpenSearch    setHost(String host)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| host | String | 指定请求的host地址 |

* * *

**获取 Host 参数**

**接口定义**

```java
获取 Host 参数
String    getHost()
```

**返回结果**

- String Host 参数值


* * *

**设置选项参数**

**接口描述**

```java
设置选项参数
OpenSearch    setOptions(Map<String,String> options)
```

**参数描述**

| 参数名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数名称 | 类型 | 描述 |
| options | Map<String,String> | Map类型选项参数值 |

* * *

**获取选项参数**

**接口定义**

```java
获取 选项参数
Map<String,String>    getOptions()
```

**返回结果**

- Map<String,String> 选项参数值