### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)QueryProcessor

# QueryProcessor

更新时间：2023-12-22 06:19:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SecondRank](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/secondrank)[下一篇：Summary](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/summary)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

## 描述

opensearch 应用版本的查询意图理解规则

## 示例

```json
{
    "name": "qp_lsh_test_1",
    "domain": "GENERAL",
    "processors": [{\
        "name": "stop_word",\
        "use_system_dictionary": true,\
        "intervention_dictionary": ""\
    }],
    "indexes": [\
        "default"\
    ],
    "active": true
}
```

## 结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| name | String | 规则名称（数字、小写英文字母或下划线组成，小写字母开头，长度不超过16位） |
| domain | String | 行业类型\- GENERAL 通用- ECOMMERCE 电商- IT\_CONTENT IT内容 |
| processors\[\] | Object | 包含功能具体说明查看下文：Processor |
| indexes | Array | 应用的索引范围 |
| active | Boolean | 是否默认规则 |

**Processor**

示例：

```javascript
{
        "name": "stop_word",
        "use_system_dictionary": true,
        "intervention_dictionary": ""
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| name | String | 功能名称\- stop\_word 停用词- spell\_check 拼写检查- term\_weighting 词权重- synonym 同义词- category\_prediction 类目预测- ner 实体识别 |
| use\_system\_dictionary | Boolean | 是否使用系统内置词典 |
| intervention\_dictionary | String | 干预词典名称 |

**类目预测**

示例：

```json
{
        "name": "stop_word",
        "categoryPrediction": 12345,
        "projectId": 12346
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| name | String | 功能名称\- category\_prediction 类目预测 |
| categoryPrediction | Integer | 类目预测模型ID |
| projectId | Integer | 算法工程ID |

**实体识别**

示例：

```json
{
    "name": "stop_word",
    "use_system_dictionary": true,
    "intervention_dictionary": "",
    "priorities": [{\
        "priority": "HIGH",\
        "tag": "test",\
        "order": 1\
    }]
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| name | String | 功能名称\- ner 实体识别 |
| use\_system\_dictionary | Boolean | 是否使用系统内置词典 |
| intervention\_dictionary | String | 干预词典名称 |
| priorities\[\] | Object | 实体类型重要性设置 |
| priorities\[\].priority | String | 重要性\- HIGH- MIDDLE- LOW |
| priorities\[\].tag | String | 实体类型的内部英文表示 |
| priorities\[\].order | Integer | 在同一个priority下的排序顺序优先顺序按照数字从小到大，默认为0 |