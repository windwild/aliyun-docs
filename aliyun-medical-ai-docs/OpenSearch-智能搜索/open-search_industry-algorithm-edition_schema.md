### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)Schema

# Schema

更新时间：2026-01-16 03:18:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：App](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/app)[下一篇：Quota](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/quota)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

内置分析器

## 描述

opensearch 应用的 schema

## 示例

```json
{
    "tables": {
        "main": {
            "primaryTable": true,
            "name": "main",
            "fields": {
                "id": {
                    "name": "id",
                    "type": "LITERAL",
                    "primaryKey": true
                },
                "title": {
                    "name": "title",
                    "type": "TEXT",
                    "primaryKey": false
                },
                "buy": {
                    "name": "buy",
                    "type": "INT",
                    "primaryKey": false
                },
                "cate_id": {
                    "name": "cate_id",
                    "type": "INT",
                    "primaryKey": false
                },
                "cate_name": {
                    "name": "cate_name",
                    "type": "LITERAL",
                    "primaryKey": false
                }
            }
        }
    },
    "indexes": {
        "searchFields": {
            "id": {
                "fields": [\
                    "id"\
                ]
            },
            "default": {
                "fields": [\
                    "title"\
                ],
                "analyzer": "chn_standard"
            },
            "cate_name": {
                "fields": [\
                    "cate_name"\
                ]
            }
        },
        "filterFields": [\
            "id",\
            "buy",\
            "cate_id",\
            "cate_name"\
        ]
    }
}
```

## 结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| tables | Object | 表结构 |
| tables.\* | Object | 表结构详情，具体说明查看下文Table\*：表名 |
| indexes | Object | 索引结构，具体说明查看下文Index |

**Table**

示例

```json
{
    "primaryTable": true,
    "name": "main",
    "fields": {
        "id": {
            "name": "id",
            "type": "LITERAL",
            "primaryKey": true
        },
        "title": {
            "name": "title",
            "type": "TEXT",
            "primaryKey": false
        },
        "buy": {
            "name": "buy",
            "type": "INT",
            "primaryKey": false
        },
        "cate_id": {
            "name": "cate_id",
            "type": "INT",
            "primaryKey": false
        },
        "cate_name": {
            "name": "cate_name",
            "type": "LITERAL",
            "primaryKey": false
        }
    }
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| fields | Object | 字段结构 |
| fields.\* | Object | 字段详情，具体说明查看下文Field\*：字段名 |
| primaryTable | Boolean | 是否是主表 |
| name | String | 表名 |

**Field**

示例：

```json
{
  "name": "json_nested",
  "type": "NESTED",
  "primaryKey": false,
  "innerSchema": {
    "job": {
      "name": "job",
      "type": "TEXT",
      "primaryKey": false
    },
    "ssn": {
      "name": "ssn",
      "type": "LITERAL",
      "primaryKey": false
    }
  }
}
```

结构

| **字段** | **类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段** | **类型** | **描述** |
| type | String | 字段类型，详细字段信息请参见 [应用结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/application-schema/ "")。 |
| name | String | 字段名 |
| primaryKey | Boolean | 是否是主键 |
| joinWith | Array | 外表链接的数据表集合 |
| innerSchema | Object | 当字段类型为`OBJECT`或者`NESTED`时指定其数据结构，支持嵌套。 |

**Index**

示例

```json
{
    "searchFields": {
      "default": {
        "fields": [\
          "title"\
        ],
        "analyzer": "chn_standard"
      },
      "id": {
        "fields": [\
          "id"\
        ]
      }
    },
    "filterFields": [\
      "id"\
    ]
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| filterFields | Array | 属性字段集合 |
| searchFields | Object | 索引字段 |
| searchFields.\* | Object | 索引字段详情，具体说明查看下文SearchField\*：索引名称 |

**SearchField**

示例

```json
{
  "fields": ["title"],
  "analyzer": "chn_standard"
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| fields | Array | 索引字段集合 |
| analyzer | String | 可填写 [自定义分析器](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/custom-text-analyzers) 和 [内置分析器](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/text-analyzers) 名称 |

## 内置分析器

| 分析器 | 描述 |
| --- | --- |

|     |     |
| --- | --- |
| 分析器 | 描述 |
| chn\_standard | 中文-通用分析 |
| simple | 简单分析 |
| chn\_single | 中文-单字分析 |
| eng\_standard | 英文-去词根分析 |
| eng\_nostem | 英文-不去词根分析 |
| fuzzy | 模糊分析 |
| keyword | 关键字 |
| chn\_ecommerce | 中文-电商分析 |
| chn\_film | 中文－视频分析 |
| chn\_scene\_name | 中文－人名分析 |
| chn\_scene\_org | 中文－机构名分析 |
| first\_letter | 拼音－简拼分析 |
| full\_pinyin | 拼音全拼分析 |
| numeric | 数值分析 |
| geo | 地理位置分析 |
| chn\_it\_content | IT-内容分析 |