### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[开发指南](https://help.aliyun.com/zh/open-search/vector-search-edition/development-guide/)[数据API](https://help.aliyun.com/zh/open-search/vector-search-edition/data-api/)[检索数据](https://help.aliyun.com/zh/open-search/vector-search-edition/query-data/)稀疏向量查询

# 稀疏向量查询

更新时间：2025-03-24 05:32:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

URL

请求协议

请求方式

支持格式

签名机制

请求body语法

查询权重

混合查询

返回参数

## URL

`/vector-service/query`

- 以上 URL 省略了请求Header参数及编码等因素。

- 以上 URL 中省略了访问应用的 host 地址。

- 以上URL 中拼接的所有查询参数，请查看下方“查询参数”的参数定义、使用方式及样例。


## 请求协议

HTTP

## 请求方式

POST

## 支持格式

JSON

## 签名机制

**可用以下方法计算签名（** authorization **）**

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **描述** |
| accessUserName | string | 用户名，可在 **实例详情页>网络信息** 查看 |
| accessPassWord | string | 密码，可在 **实例详情页>网络信息** 修改 |

```java
import com.aliyun.darabonba.encode.Encoder;
import com.aliyun.darabonbastring.Client;

public class GenerateAuthorization {

    public static void main(String[] args) throws Exception {
        String accessUserName = "username";
        String accessPassWord = "password";
        String realmStr = "" + accessUserName + ":" + accessPassWord + "";
        String authorization = Encoder.base64EncodeToString(Client.toBytes(realmStr, "UTF-8"));
        System.out.println(authorization);
    }
}
```

authorization正确返回格式：

```plaintext
cm9vdDp******mdhbA==
```

使用HTTP请求设置authorization参数时需加上Basic前缀

示例：（加在header中）

```java
authorization: Basic cm9vdDp******mdhbA==
```

## 请求body语法

- SearchRequest


|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数名称** | **描述** | **默认值** | **类型** | **是否必须** |
| tableName | 查询的表名 | 无 | string | 是 |
| indexName | 稠密向量索引名称 | 无 | string | 是 |
| vector | 查询的稠密向量数据 | 无 | list\[float\] | 是 |
| sparseData | 查询的稀疏向量数据 | 无 | SparseData | 是 |
| vectorCount | vector字段中包含的向量个数 | 1 | int | 否 |
| namespace | 查询向量的空间 | "" | string | 否 |
| topK | 返回个数 | 100 | int | 否 |
| includeVector | 是否返回文档中的向量信息 | false | bool | 否 |
| outputFields | 需要返回值的字段列表 | \[\] | list\[string\] | 否 |
| order | 排序顺序, ASC：升序 DESC: 降序 | ASC | string | 否 |
| searchParams | 查询参数<br>- [HnswSearcher](https://help.aliyun.com/zh/open-search/vector-search-edition/hnsw-hierarchical-navigable-small-world-configuration#t1Kji "") | "" | string | 否 |
| filter | 过滤表达式 | "" | string | 否 |
| scoreThreshold | 分数过滤， 使用欧式距离时，只返回小于scoreThreshold的结果。使用内积时，只返回大于scoreThreshold的结果 | 默认不过滤 | float | 否 |
| sort | 排序表达式 | "" | string | 否 |

- SparseData


| **参数名称** | **描述** | **默认值** | **类型** | **是否必须** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数名称** | **描述** | **默认值** | **类型** | **是否必须** |
| count | 每个稀疏向量中包含的元素个数 | 只有一个稀疏向量时默认为indices长度 | list\[int\] | 否 |
| indices | 元素下标（需要从小到大排序） | 无 | list\[int\] | 是 |
| values | 元素值（与下标一一对应） | 无 | list\[float\] | 是 |

向量检索版将稀疏向量下标和值用独立的两个多值字段表示，两个字段个数需要相等，位置一一对应。

例如：(0, 0.5), (100, 0.9), (40, 0.3), (50, 0.7), (20, 0.6)，表示成：

```json
{
  "indices": [0, 100, 40, 50, 20],
  "values": [0.5, 0.9, 0.3, 0.7, 0.6]
}
```

在数据写入和查询时要求下标值按从小到大排序，值做相应的调整，最终表示为：

```json
{
  "indices": [0, 20, 40, 50, 100],
  "values": [0.5, 0.6, 0.3, 0.7, 0.9]
}
```

## 查询权重

混合查询时，相同文档的最终分数是将稠密向量的距离和稀疏向量的距离加和，如果需要给稀疏向量和稠密向量不同的权重，可以做如下处理：

```python
{
    "vector": [v * weight for v in dense_vector],
    "sparseData": {
        "indices": sparse_data["indices"],
        "values": [v * (1 - weight) for v in sparse_data["values"]]
    }
}
```

## 混合查询

```json
{
    "tableName": "in0",
    "indexName": "vector",
    "vector": [\
        0.1,\
        0.2,\
        0.3,\
        0.4,\
        0.5\
    ],
    "sparseData": {
        "indices": [\
            0,\
            2\
        ],
        "values": [\
            1.2,\
            2.4\
        ]
    },
    "topK": 2,
    "order": "DESC"
}
```

## 返回参数

| **字段名称** | **描述** | **类型** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段名称** | **描述** | **类型** |
| result | 结果列表 | list\[Item\] |
| totalCount | result中的个数 | int |
| totalTime | 引擎处理耗时，单位ms | float |
| errorCode | 错误码，有错误时才有该字段 | int |
| errorMsg | 错误信息，有错误时才有该字段 | string |

**item定义**：

| **字段名称** | **描述** | **类型** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段名称** | **描述** | **类型** |
| score | 距离分 | float |
| fields | 字段名称和对应的值 | map<string, FieldType> |
| vector | 向量值 | list\[float\] |
| id | 主键值，类型为所定义的字段类型 | FieldType |
| namespace | 向量的名称空间，如果设置了namespace会返回该字段 | string |

**示例**：

```json
{
    "totalCount": 50,
    "result": [\
        {\
            "id": 99,\
            "score": 0.18588095903396607,\
            "__source__": 1,\
            "fields": {\
                "content": "众好六类网线RJ45 6类千兆8芯双绞跳线 宽带监控家用网线成品线"\
            }\
        }\
    ],
    "totalTime": 4.057
}
```