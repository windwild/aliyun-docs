### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[开发指南](https://help.aliyun.com/zh/open-search/vector-search-edition/development-guide/)[数据API](https://help.aliyun.com/zh/open-search/vector-search-edition/data-api/)统计数据

# 统计数据

更新时间：2023-09-08 04:41:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：向量引擎统计语法](https://help.aliyun.com/zh/open-search/vector-search-edition/api-vector-engine-statistical-syntax)[下一篇：管控API](https://help.aliyun.com/zh/open-search/vector-search-edition/description-of-the-control-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

URL

请求协议

请求方式

支持格式

签名机制

请求body

返回参数

## URL

`/vector-service/stats`

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

```python
cm9vdDp******mdhbA==
```

使用HTTP请求设置authorization参数是需加上Basic前缀

示例：（加在header中）

```python
authorization: Basic cm9vdDp******mdhbA==
```

## 请求body

|     |     |     |     |
| --- | --- | --- | --- |
| 参数 | 描述 | 类型 | 是否必须 |
| tableName | 表名 | string | 是 |

**示例**：

```json
{
    "tableName": "gist"
}
```

## 返回参数

- response


|     |     |     |
| --- | --- | --- |
| 字段 | 描述 | 类型 |
| result | 结果信息 | StatsInfo |
| totalTime | 引擎耗时，单位ms | float |

- StatsInfo


|     |     |     |
| --- | --- | --- |
| 字段 | 描述 | 类型 |
| partitions | 每个分片的信息 | list\[PartInfo\] |
| totalDocCount | 总的doc数 | int |
| totalSegmentCount | 总的segment数 | int |

- PartInfo


| **字段** | **描述** | **类型** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段** | **描述** | **类型** |
| partId | 分片对应的id | int |
| docCount | 文档数量 | int |
| segmentCount | segment数量 | int |

**示例**：

```json
{
    "result": {
        "partitions": [\
            {\
                "partId": 0,\
                "docCount": 3,\
                "segmentCount": 1\
            }\
        ],
        "totalDocCount": 3,
        "totalSegmentCount": 1
    },
    "totalTime": 2.185
}
```