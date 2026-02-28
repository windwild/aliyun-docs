### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-召回引擎版](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/)[引擎技术文档](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/documentation-of-retrieval-engine-edition-v3-9-0/)[索引](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/indexes/)向量索引

# 向量索引

更新时间：2025-03-07 04:36:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：摘要索引](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/summary-indexes)[下一篇：量化聚类（Quantized Clustering）配置](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/quantitative-clustering-configuration)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

向量索引介绍

向量索引配置

不带类目的向量配置

带有类目的向量配置

字段含义

## 向量索引介绍

向量召回是指将商品或者内容等以向量的形式表达，并建立向量索引库，索引库上支持输入一个或多个用户或商品向量来根据向量距离召回topK的商品或内容。

## 向量索引配置

### 不带类目的向量配置

```json
{
  "table_name": "test_vector",
  "summarys": {
    "summary_fields": [\
      "id",\
      "vector_field"\
    ]
  },
  "indexs": [\
    {\
      "index_name": "pk",\
      "index_type": "PRIMARYKEY64",\
      "index_fields": "id",\
      "has_primary_key_attribute": true,\
      "is_primary_key_sorted": false\
    },\
    {\
      "index_name": "embedding",\
      "index_type": "CUSTOMIZED",\
      "index_fields": [\
        {\
          "boost": 1,\
          "field_name": "id"\
        },\
        {\
          "boost": 1,\
          "field_name": "vector_field"\
        }\
      ],\
      "indexer": "aitheta2_indexer",\
      "parameters": {\
        "enable_rt_build": "false",\
        "min_scan_doc_cnt": "20000",\
        "vector_index_type": "Qc",\
        "major_order": "col",\
        "builder_name": "QcBuilder",\
        "distance_type": "SquaredEuclidean",\
        "embedding_delimiter": ",",\
        "enable_recall_report": "false",\
        "is_embedding_saved": "false",\
        "linear_build_threshold": "5000",\
        "dimension": "128",\
        "search_index_params": "{\"proxima.qc.searcher.scan_ratio\":0.01}",\
        "searcher_name": "QcSearcher",\
        "build_index_params": "{\"proxima.qc.builder.quantizer_class\":\"Int8QuantizerConverter\",\"proxima.qc.builder.quantize_by_centroid\":true,\"proxima.qc.builder.optimizer_class\":\"BruteForceBuilder\",\"proxima.qc.builder.thread_count\":10,\"proxima.qc.builder.optimizer_params\":{\"proxima.linear.builder.column_major_order\":true},\"proxima.qc.builder.store_original_features\":false,\"proxima.qc.builder.train_sample_count\":3000000,\"proxima.qc.builder.train_sample_ratio\":0.5}"\
      }\
    }\
  ],
  "attributes": [\
    "id",\
    "vector_field"\
  ],
  "fields": [\
    {\
      "field_name": "id",\
      "field_type": "INTEGER"\
    },\
    {\
      "user_defined_param": {\
        "multi_value_sep": ","\
      },\
      "field_name": "vector_field",\
      "field_type": "FLOAT",\
      "multi_value": true\
    }\
  ]
}
```

### 带有类目的向量配置

```json
{
  "table_name": "test_vector",
  "summarys": {
    "summary_fields": [\
      "id",\
      "vector_field",\
      "category_id"\
    ]
  },
  "indexs": [\
    {\
      "index_name": "pk",\
      "index_type": "PRIMARYKEY64",\
      "index_fields": "id",\
      "has_primary_key_attribute": true,\
      "is_primary_key_sorted": false\
    },\
    {\
      "index_name": "embedding",\
      "index_type": "CUSTOMIZED",\
      "index_fields": [\
        {\
          "boost": 1,\
          "field_name": "id"\
        },\
        {\
          "field_name": "category_id",\
          "boost": 1\
        },\
        {\
          "boost": 1,\
          "field_name": "vector_field"\
        }\
      ],\
      "indexer": "aitheta2_indexer",\
      "parameters": {\
        "enable_rt_build": "false",\
        "min_scan_doc_cnt": "20000",\
        "vector_index_type": "Qc",\
        "major_order": "col",\
        "builder_name": "QcBuilder",\
        "distance_type": "SquaredEuclidean",\
        "embedding_delimiter": ",",\
        "enable_recall_report": "false",\
        "is_embedding_saved": "false",\
        "linear_build_threshold": "5000",\
        "dimension": "128",\
        "search_index_params": "{\"proxima.qc.searcher.scan_ratio\":0.01}",\
        "searcher_name": "QcSearcher",\
        "build_index_params": "{\"proxima.qc.builder.quantizer_class\":\"Int8QuantizerConverter\",\"proxima.qc.builder.quantize_by_centroid\":true,\"proxima.qc.builder.optimizer_class\":\"BruteForceBuilder\",\"proxima.qc.builder.thread_count\":10,\"proxima.qc.builder.optimizer_params\":{\"proxima.linear.builder.column_major_order\":true},\"proxima.qc.builder.store_original_features\":false,\"proxima.qc.builder.train_sample_count\":3000000,\"proxima.qc.builder.train_sample_ratio\":0.5}"\
      }\
    }\
  ],
  "attributes": [\
    "id",\
    "vector_field",\
    "category_id"\
  ],
  "fields": [\
    {\
      "field_name": "id",\
      "field_type": "INTEGER"\
    },\
    {\
      "user_defined_param": {\
        "multi_value_sep": ","\
      },\
      "field_name": "vector_field",\
      "field_type": "FLOAT",\
      "multi_value": true\
    },\
    {\
      "field_name": "category_id",\
      "field_type": "INTEGER"\
    }\
  ]
}
```

**重要**

- 引入分类的目的是为了支持按照分类进行向量检索，比如一个图片有不同的类别，如果不指定分类构建向量索引，只是对检索出来的向量进行过滤很可能会出现无结果的情况。

- 在配置的向量索引时，若为管理员模式，build\_index\_params和search\_index\_params的参数内容要去除转义。


### 字段含义

- field\_name：构建向量索引的字段，必须为RAW类型，最少包括2个字段，一个是主键（或者是主键的hash值），字段值必须是整数，另一个是包含向量的字段。如果需要对向量按照分类构建索引，可以新增一个分类字段，字段类型为RAW类型，字段值为整数。这些字段在索引中的顺序必须和在fields配置的顺序相同，而且必须是按照主键、类目（如果有）、向量这个顺序。

- index\_name：向量索引的名称。

- index\_type：索引类型，必须为CUSTOMIZED。

- indexer：构建向量索引的插件，目前仅支持aitheta2\_indexer。

- parameters：向量索引的构建参数和查询参数。

  - dimension：维度

  - embedding\_delimiter: 向量分隔符，默认是","

  - distance\_type：距离类型，目前仅支持如下两种

    - InnerProduct （内积）

    - SquaredEuclidean（平方欧式距离），经过归一化的数据请配置SquaredEuclidean。
  - major\_order: 数据存储方式，目前支持如下两种

    - col （按列存, 对dimension有要求，必须是2的幂次方, 性能更优）

    - row（按行存，默认使用）
  - builder\_name: 索引构建类型，建议配置下面两种（更多参数请联系我们）

    - QcBuilder

    - LinearBuilder（线性构建，数据文档数量少于1w时，推荐使用）
  - searcher\_name: 索引检索类型，和builder\_name对应，如果有GPU需求请联系我们。

    - QcSearcher（CPU检索，对应QcBuilder）

    - LinearSearcher (CPU暴力检索，对应LinearBuilder)
  - build\_index\_params：索引构建参数，和builder\_name参数对应，具体见 [量化聚类（Quantized Clustering）配置](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/quantitative-clustering-configuration "") 配置。

  - search\_index\_params：索引检索参数，和searcher\_name参数对应，具体见 [search\_index\_params](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/hnsw-hierarchical-navigable-small-world-configuration "") 配置。

  - linear\_build\_threshold：线性构建的阈值，若文档数量低于该阈值，则会使用LinearBuilder构建, LinearSearcher检索。默认是10000，用线性构建的好处是可以节省内存,召回结果无损, 但是若数据规模较大时，性能极差。

  - min\_scan\_doc\_cnt: 召回候选集的个数最小值，默认10000，和proxima.qc.searcher.scan\_ratio的概念类似。两者都配置的情况下，取两者的最大值

    - scan\_ratio&min\_scan\_doc\_cnt不是越大越好。太大的话，会极大影响性能&延迟

    - 一般而言, 若召回topk个向量，min\_scan\_doc\_cnt的建议大小为max(10000, 100\*topk)，scan\_ratio为max(10000, 100\*topk)/total\_doc\_cnt, 具体的还得结合数据规模、召回率以及性能等参数。

    - 之所以存在两个类似参数，主要是由于实时以及多类目场景下的需求。一般用户只需要配置scan\_ratio即可
  - enable\_recall\_report: 是否开启召回率指标汇报，默认关闭

  - is\_embedding\_saved： 是否保存原始向量,默认关闭。如果开启INT8/FP16量化且开启实时检索，务必开启该选项，否则会导致批次增量构建失败

  - enable\_rt\_build：是否支持实时索引，默认开启

  - ignore\_invalid\_doc：是否忽略有问题的向量数据，默认开启

  - rt\_index\_params：实时索引参数，当enable\_rt\_build为true时，可配置，如：















    ```json
    {
      "proxima.oswg.streamer.segment_size": 2048
    }
    ```