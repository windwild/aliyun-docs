### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/)[DQL操作](https://help.aliyun.com/zh/tablestore/dql-statements/)JSON函数

# JSON函数

更新时间：2024-07-15 23:00:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Join](https://help.aliyun.com/zh/tablestore/join-function)[下一篇：查询索引描述信息](https://help.aliyun.com/zh/tablestore/query-the-index-information-about-a-table)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

支持的JSON函数

->>

语法

函数说明

参数

示例

JSON\_UNQUOTE

语法

函数说明

参数

示例

JSON\_EXTRACT

语法

函数说明

参数

示例

JSON path说明

路径选择器

示例

如果表中某列数据以JSON格式存储，您可以使用JSON函数查询JSON数据。Tablestore SQL的JSON函数遵循MySQL 5.7的语法。本文介绍Tablestore SQL支持的JSON函数以及JSON函数的用法。

## 支持的JSON函数

目前Tablestore SQL支持的JSON函数请参见下表。

| **JSON函数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **JSON函数** | **说明** |
| [->>](https://help.aliyun.com/zh/tablestore/json-functions#section-dwh-fav-b0m "") | 从JSON文档中解出某一路径对应的文档并取消引用转换为字符串，等效于`JSON_UNQUOTE(JSON_EXTRACT())`。 |
| [JSON\_UNQUOTE](https://help.aliyun.com/zh/tablestore/json-functions#title-nfo-s21-pqe "") | 去除JSON值外的引号，返回结果为字符串。 |
| [JSON\_EXTRACT](https://help.aliyun.com/zh/tablestore/json-functions#zejPf "") | 从JSON文档中解出某一路径对应的子文档。 |

## ->>

`->>`用于从JSON文档中解出某一路径对应的文档并取消引用转换为字符串，等效于`JSON_UNQUOTE(JSON_EXTRACT())`。

### **语法**

```sql
column->>path
```

### **函数说明**

返回值为路径参数匹配的值。

如果任何参数为NULL或所设置的路径在文档中未找到值，则返回NULL。

### **参数**

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| column | String | 列名。 |
| path | String | 用于定位JSON文档中的某个路径。<br>path必须以`$`为开头，`$`表示整个JSON文档。其后可以选择添加路径选择器，选择器可以组合使用。更多信息，请参见 [JSON path说明](https://help.aliyun.com/zh/tablestore/json-functions#section-wos-dbi-4o1 "")。 |

### **示例**

以下示例用于查询json\_table表pkint主键值为1的行对应coljson列值中路径为`$.a`的数据。

```sql
SELECT coljson, coljson->>'$.a' AS subdoc FROM json_table WHERE pkint = 1;
```

返回结果示例如下图所示。

![image..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1720184861/p673405.png)

## JSON\_UNQUOTE

JSON\_UNQUOTE用于去除JSON值外的引号，返回结果为字符串。

### **语法**

```sql
JSON_UNQUOTE(json_val)
```

### **函数说明**

返回值为去除JSON值外面引号的字符串。

如果参数为NULL，则返回NULL。

**重要**

如果值以双引号开头和结尾，但不是有效的JSON字符串文字，则会发生错误。

### **参数**

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| json\_val | JSON\_EXTRACT语句。更多信息，请参见 [JSON\_EXTRACT](https://help.aliyun.com/zh/tablestore/json-functions#zejPf "")。 |

### **示例**

以下示例用于查询json\_table表pkint主键值为1的行对应coljson列值中路径为`$.a`的数据。

```sql
SELECT coljson, JSON_UNQUOTE(JSON_EXTRACT(coljson, '$.a')) AS subdoc FROM json_table WHERE pkint = 1;
```

返回结果示例如下图所示。

![1673770680585-e4dc3466-2434-4ccb-be2f-f5166a7e3e49..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2951474861/p673194.png)

## **JSON\_EXTRACT**

JSON\_EXTRACT用于从JSON文档中解出某一路径对应的子文档。由于表格存储未支持原生的JSON类型，直接使用会抛出非法类型参数的错误，因此JSON\_EXTRACT需要结合JSON\_UNQUOTE进行使用。

### **语法**

```sql
JSON_EXTRACT(json_doc, path[, path] ...)
```

### **函数说明**

返回值由路径参数匹配的所有值组成。 如果这些参数可能返回多个值，则匹配的值将自动包装为一个数组，顺序与生成值的路径相对应， 否则返回值为单个匹配值。

如果任何参数为NULL或所设置的路径在文档中未找到值，则返回NULL。

### **参数**

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| json\_doc | String | JSON格式的文档。<br>**重要**<br>如果json\_doc参数不是有效的JSON文档或任何路径参数不是有效的路径表达式，则会发生错误。 |
| path | String | 用于定位JSON文档中的某一个路径。<br>path必须以`$`为开头，`$`表示整个JSON文档。其后可以选择添加路径选择器，选择器可以组合使用。更多信息，请参见 [JSON path说明](https://help.aliyun.com/zh/tablestore/json-functions#section-wos-dbi-4o1 "")。 |

### **示例**

以下示例用于查询json\_table表pkint主键值为1的行对应coljson列值中路径为`$.a`的数据。其中coljson列的值为`{"a": 1, "b":2, "c":{"d":4}}`。

```sql
SELECT coljson, JSON_UNQUOTE(JSON_EXTRACT(coljson, '$.a')) AS subdoc FROM json_table WHERE pkint = 1;
```

返回结果示例如下图所示。

![1673770680585-e4dc3466-2434-4ccb-be2f-f5166a7e3e49..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2951474861/p673194.png)

您也可以一次查询多个path，多个path的结果以数组格式组织。以下SQL语句示例用于查询json\_table表pkint主键值为1的行对应coljson列值中路径为`$.a`、`$.b`、`$.c.d`的数据。其中coljson列的值为`{"a": 1, "b":2, "c":{"d":4}}`。

```sql
SELECT coljson, JSON_UNQUOTE(JSON_EXTRACT(coljson, '$.a', '$.b', '$.c.d')) AS subdoc FROM json_table WHERE pkint = 1;
```

返回结果示例如下图所示。

![1673771181990-4c5db21a-7ccc-4a7c-ba4a-c87a36e2aa13..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2951474861/p673196.png)

## JSON path说明

path主要用于定位JSON文档中的某一个路径。

path必须以`$`为开头，`$`表示整个JSON文档。其后可以选择添加路径选择器，选择器可以组合使用。

**重要**

如果对应路径在JSON文档中不存在数据，则会返回NULL。

### **路径选择器**

主要的路径选择器如下：

- `$.key`用于JSON Object类型。在半角句号（.）后可以添加对应的键值，用于选中键值对应的对象，例如`$.a`。如果key中包含空格，则需要为key添加双引号，例如`$."a b"`。

- `[N]`：用于JSON Array类型，选择数组对应的下标。下标从0开始，例如`$[0]`、`$[1]`。

- 路径也支持包含星号（\*）和`**`通配符，主要用法如下：

  - `.*`：用于计算JSON Object中所有成员的值。

  - `[*]`：用于计算JSON Array中所有元素的值。

  - `prefix**suffix`：表示全部以prefix开始，以suffix结尾的路径。

### **示例**

JSON Object查询

JSON Array查询

通配符查询

假设要查询的JSON Object对象如下：

```json
{"a": 1, "f": [1, 2, 3], "c": {"d": 4}}
```

不同路径选择器配置时的返回值说明请参见下表。

|     |     |
| --- | --- |
| **路径选择器** | **返回值** |
| $ | `{"a": 1, "c": {"d": 4}, "f": [1, 2, 3]}` |
| $.a | 1 |
| $.c | `{"d": 4}` |
| $.c.d | 4 |
| $.f\[1\] | 2 |

对于key中含有空格的情况，假设要查询的JSON Object对象如下：

```json
{"a fish": "shark", "a bird": "sparrow"}
```

不同路径选择器配置时的返回值说明请参见下表。

|     |     |
| --- | --- |
| **路径选择器** | **返回值** |
| $."a fish" | shark |
| $."a bird" | sparrow |

假设要查询的JSON Array对象如下：

```json
[3, {"a": [5, 6], "b": 10}, [99, 100]]
```

不同路径选择器配置时的返回值说明请参见下表。

**说明**

当返回值为非标量值时，您可以继续进行嵌套查询。例如`$[1]`和`$[2]`返回的为非标量值，可以继续使用`$[1].a`、`$[2][0]`等进行嵌套查询。

|     |     |
| --- | --- |
| **路径选择器** | **返回值** |
| $\[0\] | 3 |
| $\[1\] | `{"a": [5, 6], "b": 10}` |
| $\[1\].a | `[5, 6]` |
| $\[1\].a\[1\] | 6 |
| $\[1\].b | 10 |
| $\[2\] | `[99, 100]` |
| $\[2\]\[0\] | 99 |
| $\[3\] | NULL |

假设要查询的JSON对象如下：

```json
{"a": 1, "b": 2, "c": [3, 4, 5]}
```

不同路径选择器配置时的返回值说明请参见下表。

|     |     |
| --- | --- |
| **路径选择器** | **返回值** |
| $.\* | `[1, 2, [3, 4, 5]]` |
| $.c\[\*\] | `[3, 4, 5]` |

假设要查询的JSON对象如下：

```json
{"a": {"b": 1}, "c": {"b": 2}}
```

设置路径选择器为`$**.b`时，返回值为`[1, 2]`。等效于（$.a.b和$.c.b）。