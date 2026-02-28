### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[开发指南](https://help.aliyun.com/zh/open-search/vector-search-edition/development-guide/)[数据API](https://help.aliyun.com/zh/open-search/vector-search-edition/data-api/)[检索数据](https://help.aliyun.com/zh/open-search/vector-search-edition/query-data/)文本与向量混合查询

# 文本与向量混合查询

更新时间：2025-03-24 05:31:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：filter表达式](https://help.aliyun.com/zh/open-search/vector-search-edition/filter-expression)[下一篇：向量引擎统计语法](https://help.aliyun.com/zh/open-search/vector-search-edition/api-vector-engine-statistical-syntax)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

查询语法

URL

请求协议

请求方式

支持格式

签名机制

查询参数

注意事项

查询示例

返回结果

## 查询语法

### **URL**

- curl -X POST /search 或者 curl -X POST /vector-service/search


- 以上 URL 省略了请求Header参数及编码等因素。

- 以上 URL 中省略了访问应用的 host 地址。

- 以上URL 中拼接的所有查询参数，请查看下方“查询参数”的参数定义、使用方式及样例。


### **请求协议**

HTTP

### **请求方式**

POST

### **支持格式**

JSON

### **签名机制**

可用以下方法计算签名（authorization）

|     |     |     |
| --- | --- | --- |
| 参数 | 类型 | 描述 |
| accessUserName | string | 用户名，可在实例详情页>网络信息查看 |
| accessPassWord | string | 密码，可在实例详情页>网络信息修改 |

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

```python
cm9vdDp******mdhbA==
```

使用HTTP请求设置authorization参数时需加上Basic前缀

示例：（加在header中）

```python
authorization: Basic cm9vdDp******mdhbA==
```

### **查询参数**

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数名称** | **类型** | **是否必须** | **默认值** | **描述** |
| tableName | string | 是 | 无 | 查询的表名 |
| knn | Object | 否 | 无 | knn查询参数 |
| knn.vector | list\[float\] | 是 | 无 | 查询的稠密向量数据 |
| knn.topk | int | 否 | 无 | 返回个数 |
| knn.filter | String | 否 | "" | 过滤条件表达式。 |
| knn.weight | Float | 否 | 1.0 | knn查询结果的权重，以score \* weight的结果作为该路的排序分。 |
| text | Object | 否 | 无 | text查询参数 |
| text.queryString | String | 是 | 无 | [Ha3 query语法](https://help.aliyun.com/zh/open-search/vector-search-edition/query-clause "")，支持多个文本索引的AND、OR嵌套 |
| text.queryParams | Map<String, String> | 否 | {} | query查询参数：<br>- default\_op: 指定在该次查询中使用的默认query 分词后的连接操作符，`AND`或`OR`。默认为AND。<br>  <br>- no\_token\_indexes: 支持查询中指定的index不分词（除分词以外的其他流程如归一化、去停用词会正常执行），多个index之间用`;`分割。<br>  <br>- remove\_stopwords: `true`或`false` 表示是否需要删除stop words，stop words在分词器中配置。默认值为`true`。 |
| text.filter | String | 否 | "" | 过滤条件表达式。 |
| text.weight | Float | 否 | 1.0 | text查询结果的权重，以score \* weight的结果作为该路的排序分。 |
| text.terminateAfter | Integer | 否 | 0 | 每个分片查找满足条件的文档的最大数量。到达这个数量后，查询将提前结束，不再继续查询索引。默认为0，不设置限制。 |
| size | Integer | 否 | 100 | 返回结果的个数。 |
| from | Integer | 否 | 0 | 从结果集的第from返回doc。 |
| outputFields | List\[String\] | 否 | \[\] | 指定需要在结果中返回的字段。 |
| order | String | 否 | DESC | 结果排序方向：<br>- DESC: 降序排序<br>  <br>- ASC: 升序排序 |
| rank | Object | 否 | {} | 指定两路结果融合的方式，目前支持两种策略：<br>- 默认策略：两路结果中相同pk的doc的分数按权重相加。按加权后的分数排序。<br>  <br>- rrf: 使用rrf融合两路结果。 |

### **注意事项**

- knn仅支持单个向量查询，参数与query API相同。

- 距离分转换

为了将knn与text分数做融合，将对knn的距离分做转换。















```json
# 欧式距离
score = 1.0 / (1.0 + l2_distance^2)

# 内积距离
score = (1.0 + ip_distance) / 2.0
```

- knn查询中的order参数不起作用，统一使用外层的order参数。

- 默认排序

  - 配置方式：不配置rank，或者rank配置为空{}















    ```json
    {
      "rank": {}
    }
    ```

  - 两路结果中相同pk的doc的分数按权重相加。按加权后的分数排序。















    ```json
    score(i) = knn_score(i) * knn_weight + text_score(i) * text_weight
    ```
- RRF

  - 配置方式：















    ```json
    {
      "rank": {
        "rrf": {
          "rankConstant": 60
        }
      }
    }

    # rankConstant为可选参数，默认为60
    ```

  - 公式















    ```json
    score = 0.0
    if d in result(q):
        score += 1.0 / (rankConstant + rank(result(q), d))
    return score

    # rankConstant是排序常数，决定了单路结果集中的文档对最终结果的影响程度。大的值表示低排名的文档具有更大的影响力。可以设置为大于等于1的整数。默认为60.
    # rank(result(q), d) 是该文档在某一路查询结果中的位置，从1开始。
    ```

## 查询示例

```json
{
    "tableName": "test",
    "text": {
        "queryString": "title:'阿里巴巴'",
        "queryParams": {
            "default_op": "OR"
        },
        "filter": "count > 0",
        "terminateAfter": 100000
    },
    "knn": {
        "vector": [0.1, 0.2, 0.3, 0.4, 0.5],
        "namespace": "1",
        "topK": 100
    },
    "order": "DESC",
    "size": 10,
    "rank": {
        "rrf": {
            "rankConstant": 1
        }
    },
    "outputFields": ["title"]
}
```

## 返回结果

```json
{
  "totalTime": 8.522,
  "coveredPercent": 1.0,
  "totalCount": 5,
  "result": [\
    {\
      "__source__": 2,\
      "score": 0.833333,\
      "namespace": 1,\
      "id": 2,\
      "fields": {\
        "title": "a b c"\
      }\
    },\
    {\
      "__source__": 3,\
      "score": 0.666666,\
      "namespace": 1,\
      "id": 1,\
      "fields": {\
        "title": "a b"\
      }\
    },\
    {\
      "__source__": 3,\
      "score": 0.333333,\
      "namespace": 2,\
      "id": 5,\
      "fields": {\
        "title": "c"\
      }\
    },\
    {\
      "__source__": 2,\
      "score": 0.25,\
      "namespace": 2,\
      "id": 4,\
      "fields": {\
        "title": "b c"\
      }\
    },\
    {\
      "__source__": 2,\
      "score": 0.2,\
      "namespace": 1,\
      "id": 0,\
      "fields": {\
        "title": "a"\
      }\
    }\
  ]
}
```

**result参数**：

| **字段名称** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段名称** | **类型** | **说明** |
| id | schema里配置的类型 | 主键值。 |
| namespace | schema里配置的类型 | knn查询的向量索引的namespace，如果配置了才有该字段。 |
| vector | List\[Float\] | knn查询的向量索引的向量值，需要在knn中设置"includeVector": true。 |
| score | Float | 最终排序分。 |
| fields | Map<String, FieldType> | 返回的字段内容，kvmap结构。 |
| totalTime | Integer | 引擎耗时，单位ms。 |
| totalCount | Integer | 返回结果的数量。 |
| \_\_source\_\_ | Integer | 从哪个query召回的数据。<br>1：表示knn查询召回。<br>2：表示text查询召回。<br>3：表示knn和text同时召回。 |
| coveredPercent | Float | 正常返回结果的分片数比例，例如：1.0 表示所有的分片都正常返回数据。 |