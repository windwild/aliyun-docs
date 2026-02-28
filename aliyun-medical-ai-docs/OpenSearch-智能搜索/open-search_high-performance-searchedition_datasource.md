### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/high-performance-searchedition/control-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/high-performance-searchedition/data-structures/)DataSource

# DataSource

更新时间：2024-02-06 02:22:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：QuotaReviewTask](https://help.aliyun.com/zh/open-search/high-performance-searchedition/quotareviewtask)[下一篇：FirstRank](https://help.aliyun.com/zh/open-search/high-performance-searchedition/firstrank)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

## 描述

数据源信息

## 示例

```json
{
  "tableName": "news",
  "type": "rds",
  "fields": [\
    {\
      "id": "id"\
    },\
    {\
      "caption": "caption"\
    },\
    {\
      "content": "content"\
    },\
    {\
      "categoryId": "category_id"\
    }\
  ],
  "plugins": {
    "caption": {
      "name": "HTMLTagRemover",
      "parameters": {}
    },
    "content": {
      "name": "HTMLTagRemover",
      "parameters": {}
    }
  },
  "keyField": "id",
  "parameters": {
    "filter": "",
    "instanceId": "rm-abc",
    "dbName": "my_db",
    "dbTableName": "my_table",
    "dbUser": "my_user",
    "dbPassword": "my-password",
    "autoSync": true
  }
}
```

## 结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| tableName | String | 表名 |
| type | String | 数据源类型- rds- odps- opensearch-polardb |
| fields\[\] | Object | 表字段映射信息{key:value}，key：数据源表字段，value：应用表字段。 |
| plugins | Object | 字段数据处理插件 |
| plugins.\* | Object | 插件详情，具体说明查看下文 [Plugin](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)\*：字段名 |
| keyField | String | 主键 |
| parameters | Object | 数据源信息不同数据源的配置信息各不相同，具体说明查看相关下文：<br>- [rds](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)<br>- [odps](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)<br>- [opensearch](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)<br>- [polardb](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource) |

**Plugin**

示例

```json
{
  "name": "HTMLTagRemover",
  "parameters": {}
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| name | String | 插件名称- JsonKeyValueExtractor- MultiValueSpliter- KeyValueExtractor- StringCatenateExtractor- HTMLTagRemover |
| parameters | Object | 插件参数不同插件的参数各不相同，具体说明查看相关下文：<br>- [JsonKeyValueExtractor](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)<br>- [MultiValueSpliter](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)<br>- [KeyValueExtractor](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)<br>- [StringCatenateExtractor](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource)<br>- [HTMLTagRemover](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datasource) |

**JsonKeyValueExtractor**

从JSON格式的来源字段中提取指定的键值，提取出来的键值作为目标表字段的内容，只能抽取某个key中的值。示例

```json
{
  "key": "my_field"
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| key | String | 键名 |

**MultiValueSpliter**

将来源字段按照分隔符分割成多个值，分割后的内容作为目标表字段的内容，目标表字段必须是配置为ARRAY类型的字段（若分隔符为不可见字符，需要使用unicode字符来标识，如\\u001D）。示例

```json
{
  "seperator": "|"
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| seperator | String | 分隔符 |

**KeyValueExtractor**

从KV格式的来源字段中提取指定的键值，提取出来的键值作为目标表字段的内容，只能抽取某个key中的值。分隔符可以不填。示例

```json
{
  "key": "my_field",
  "fieldSep": ";",
  "kvSep": ":"
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| key | String | 键 |
| fieldSep | String | 键分隔符 |
| kvSep | String | 键值分隔符 |

**StringCatenateExtractor**

将多个指定字段按照指定的顺序拼接成一个字符串，该插件不支持int字段类型，建议用literal字段类型；字段列表以逗号分隔（字段需来自于目标字段）。示例

```json
{
  "connector": "-",
  "sources": "id,title"
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| connector | String | 连接符 |
| sources | String | 指定的多个字段 |

**HTMLTagRemover**

剔除来源字段中的HTML标签，剔除标签后的内容复制到当前字段，源字段配置为当前字段则做内容替换。注：此插件不需要额外参数。

**rds**

示例

```json
{
  "instanceId": "rds-instance-id",
  "dbName": "my_db",
  "dbTableName": "my_table",
  "dbUser": "my",
  "dbPassword": "my_passwd",
  "filter":"",
  "autoSync": true
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| instanceId | String | 实例ID |
| dbName | String | 数据库名 |
| dbTableName | String | 数据库表名 |
| dbUser | String | 数据库账号 |
| dbPassword | String | 数据库账号密码 |
| filter | String | 过滤条件目前支持的条件有<, >, =, !=, >=, <=，多个条件用’,’分隔 |
| autoSync | Boolean | 是否数据自动同步- true 是- false 否 |

**odps**

示例

```json
{
  "projectName": "my_project",
  "tableName": "my_table",
  "partition": "",
  "done": "no",
  "donePrefix": "",
  "timestamp":""
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| projectName | String | 项目名称 |
| tableName | String | 表名 |
| partition | String | 分区信息参考： [ODPS数据源配置](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/configure-a-maxcompute-data-source) |
| done | String | 是否使用done文件- no- yes |
| donePrefix | String | done文件前缀注：当done=”yes”时必填 |
| timestamp | String | 全量数据的时间戳 |

**opensearch**

示例

```json
{
  "appId": "12345678",
  "tableName": "my_table",
  "appType": "standard",
  "filter": ""
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| appId | String | 应用ID |
| tableName | String | 应用表名 |
| appType | String | 应用类型- standard 标准版- advance 老高级版（新应用不支持此类型）- enhanced 新高级版 |
| filter | String | 过滤条件目前支持的条件有<, >, =, !=, >=, <=，多个条件用’,’分隔 |

**polardb**

示例

```json
{
  "clusterId": "my_cluster_id",
  "dbName": "my_db",
  "dbTableName": "my_table",
  "aliyunUserId":"123455789",
  "dbUser":"my_user",
  "dbPassword":"my_passwd",
  "autoSync":true,
  "filter": "id>100"
}
```

结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| clusterId | String | 集群ID |
| dbName | String | 数据库名 |
| dbTableName | String | 数据表名 |
| aliyunUserId | String | 阿里云用户ID |
| dbUser | String | 数据库账号 |
| dbPassword | String | 数据库账号密码 |
| autoSync | Boolean | 是否数据自动同步- true 是- false 否 |
| filter | String | 过滤条件目前支持的条件有<, >, =, !=, >=, <=，多个条件用’,’分隔 |