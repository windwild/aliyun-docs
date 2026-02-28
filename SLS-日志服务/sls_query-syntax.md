### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)查询语法与功能

# 查询语法与功能

更新时间：2026-01-05 03:29:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：核密度估计函数](https://help.aliyun.com/zh/sls/kernal-density-estimation-functions)[下一篇：短语查询](https://help.aliyun.com/zh/sls/phrase-search)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

基础语法

查询语句编写思路

步骤一：确定查询方式

步骤二：确定字段类型

步骤三：确定匹配模式

查询语句示例

常见问题

无法找到想要的日志

JSON日志问题

查询错误排查

相关文档

日志服务支持使用查询语句对日志进行筛选。筛选结果可独立使用，也可以用于分析语句，进行更复杂的分析处理。

## 前提条件

对日志进行查询，必须先 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#64e73166e2xm0 "")。

## 基础语法

**说明**

[通过AI智能生成查询与分析语句（Copilot）](https://help.aliyun.com/zh/sls/copilot-automatic-generation-of-ai-assisted-sql-statements "")：日志服务提供AI智能辅助查询分析语句的使用，支持自然语言生成查询分析语句、解释复杂查询分析语句、优化查询分析语句等能力。

查询语句与分析语句以`|`分割，格式为`查询语句|分析语句`，示例如下：

```sql
* | SELECT status, count(*) AS PV GROUP BY status
```

| **语句类型** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **语句类型** | **说明** |
| 查询语句 | 查询条件，可以为关键词、数值、数值范围、空格、星号（\*）等。 <br>如果为空格或星号（\*），表示无过滤条件。<br>**重要**<br>查询语句中建议不超过30个条件。 |
| 分析语句 | **重要**<br>必须与查询语句一起使用，分析语句中无需填写FROM子句和WHERE子句，默认分析当前LogStore中的数据。分析语句不支持offset，不区分大小写，末尾无需加分号。<br>对查询结果或全量数据进行计算和统计。日志服务支持的分析函数和语法：<br>- [SQL函数](https://help.aliyun.com/zh/sls/sql-function/ "")<br>  <br>- [SQL子句](https://help.aliyun.com/zh/sls/sql-syntax/ "")<br>  <br>- [机器学习函数](https://help.aliyun.com/zh/sls/machine-learning-functions/ "") |

## **查询语句编写思路**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8471067671/CAEQURiBgMDfveu3mRkiIGMyYmNlNTYwODdlZTQwZGNhYTEzNjYxMDk5ZmQ0YTAz4179186_20240118143909.150.svg)

查询语句的编写流程可分为以下三步：

### **步骤一：确定查询方式**

**重要**

不同的索引配置，会产生不同的查询和分析结果，如果同时创建了全文索引和字段索引，以字段索引的配置为准。

根据 **索引类型** 的不同，日志服务LogStore查询可分为全文查询和字段查询。全文查询和字段查询区别如下：

- 如果只创建 **全文索引**，则只能使用全文查询。

- 如果已创建 **字段索引**，则按以下规则查询：

  - **double**、 **long** 类型：只能根据字段查询语法进行查询。

  - **text** 类型：若知晓关键词属于某个已创建索引的text类型字段，建议使用字段查询语法。如果不确定关键词的具体字段，请使用全文查询语法。

    - 如果没有创建全文索引，全文查询语法仅在字段索引是text类型的字段中查询。

    - 如果已创建全文索引，全文查询语法会从所有text类型索引中查询。

全文查询

字段查询

不针对具体的字段进行查询，支持通配符（`*`、`?`）和逻辑运算符（如and、or等）。

##### **查询语法**

```sql
 keywords1  [ and | or | not ] keywords2  ...
```

#### **示例**

- 示例1

查询关键词为`GET`相关的日志。则查询语法：`GET`。

- 示例2

查询关键词为`GET`或`POST`相关的日志。则查询语法：`GET or POST`。

- 示例3

查询以`Jo`开头相关的日志，例如Joe、Jon等。则查询语法为：`Jo？`。


针对具体字段名，支持类型化运算（如数值比较、正则表达式），需字段已建立索引。

**重要**

- `indexname1` 是需要查询的字段名，当字段名、表名等专有名词中存在特殊字符（空格、中文等）、语法关键词（`and`、`or`等）等内容时，则需要使用`""`（双引号）包裹。在查询中使用引号，请参见 [如何在查询和分析语句中使用引号](https://help.aliyun.com/zh/sls/how-do-i-use-quotation-marks-in-query-statements "")。

- 字段索引涉及`long`、`double`类型，可以使用比较运算符`>`、`>=`、`<`、`<=`、`=`、`in`。


#### **查询语法**

```sql
indexname1 [ : | > | >= | < | <= | = | in ] keyword1 [ [ and | or | not ] indexname2 ... ]
```

#### **示例**

- 示例1

查询 `request_method`为 `GET`相关的日志，则查询语法为：`request_method: GET`。

- 示例2

查询 `request_time_msec`大于 `50` 相关的日志，则查询语法为`request_time_msec>50`（该字段索引类型为 **double**）。

- 示例3

查询 `request_method`为 `GET`且`request_time_msec`大于`50` 相关的日志。则查询语法为：`request_method: GET and request_time_msec>50`。


### **步骤二：确定字段类型**

编写查询语句时需要考虑字段类型的特点，合理使用运算符，快速、精准地锁定目标日志。

#### **字段类型**

|     |     |     |
| --- | --- | --- |
| **字段类型** | **说明** | **可用运算符** |
| [text类型](https://help.aliyun.com/zh/sls/data-types#section-gul-kwi-n9n "") | 字符串类型的字段。开启全文索引后，日志服务默认将整条日志（除`__time__`以外所有字段）设置为 **text** 类型。 | `and`、`or`、`not`、`()`、`:`、`""`、`\`、`*`、`?`。 |
| [long和double类型](https://help.aliyun.com/zh/sls/data-types#section-4ml-735-4ms "") | 只有设置字段的数据类型为 **long** 或 **double** 后，才能通过数值范围查询该字段的值。<br>- 如果字段的数据类型不被设置为 **double**、 **long** 或者查询时数值范围的语法错误，那么日志服务会按照全文查询方式进行查询，这样查询到的结果可能与期望的结果不同。<br>  <br>  例如字段`owner_id`不是 **double**、 **long** 类型，则执行查询语句`owner_id>100`时，会返回同时包含`owner_id`、`>`（非分词符）、`100`这三个词的日志。<br>  <br>- 如果将字段的类型从 **text** 类型改成 **double**、 **long** 类型，则只支持等号`=`查询。如果需要使用范围查询、大于号（>）、小于号（<）等运算符，必须 [重建索引](https://help.aliyun.com/zh/sls/reindex-logs-for-a-logstore "")。 | `and`、`or`、`not`、`()`、`>`、`>=`、`<`、`<=`、`=`、`in`。 |
| [JSON类型](https://help.aliyun.com/zh/sls/data-types#section-nsn-cfm-wa3 "") | 针对JSON对象中的字段，可根据其值，将数据类型设置为 **long**、 **double** 或 **text**，并开启统计功能。 | 根据JSON对象中的字段的类型使用不同的运算符。 |

#### **运算符**

**重要**

- in运算符只能小写，其他运算符不区分大小写。

- 日志服务保留以下运算符的使用权，如果您需要使用以下运算符作为查询关键字，请使用`""`（双引号）包裹：`sort`、`asc`、`desc`、`group by`、`avg`、`sum`、`min`、`max`和`limit`。

- 运算符的优先级由高到低排序如下所示：

1. 冒号（:）

2. 双引号（""）

3. 圆括号（）

4. and、not

5. or

|     |     |
| --- | --- |
| **运算符** | **说明** |
| `:` | 用于字段查询（Key:Value），例如`request_method:GET`。<br>如果字段名称或者字段值内有空格、冒号（:）、连字符（-）等特殊字符，请使用双引号（""）包裹字段名称或者字段值，例如`"file info":apsara`。 |
| `and` | `and`运算符。例如`request_method:GET and status:200`。<br>如果多个关键词之间没有语法关键词，默认为`and`关系，例如`GET 200 cn-shanghai`等同于`GET and 200 and cn-shanghai`。 |
| `or` | `or`运算符。例如`request_method:GET or status:200`。 |
| `not` | `not`运算符。例如`request_method:GET not status:200`、`not status:200`。 |
| `( )` | 用于提高括号内查询条件的优先级。例如`(request_method:GET or request_method:POST) and status:200`。 |
| `""` | 使用`""`（双引号）包裹一个语法关键词，可以将该语法关键词转换成普通字符。在字段查询中`""`内的所有词被当成一个整体。<br>- 当字段名或字段值中存在特殊字符（空格、中文、`:`、`-`等）、语法关键词（`and`、`or`等）等内容时，需要使用`""`包裹。例如`"and"`表示查询包含and的日志，此处的and不代表运算符。<br>  <br>- 日志服务保留以下运算符的使用权，如果需要使用以下运算符作为查询关键字，请使用`""`包裹：`sort`、`asc`、`desc`、`group by`、`avg`、`sum`、`min`、`max`和`limit`。<br>  <br>- 通过数据加工或者Logtail插件处理的日志，其tag中的key会被转换成普通key，即查询时需使用`""`包裹字段名，例如`"__tag__:__client_ip__":192.0.2.1`，此处的`__tag__:__client_ip__`为日志服务保留字段，表示日志所在主机的IP地址。更多信息，请参见 [保留字段](https://help.aliyun.com/zh/sls/reserved-fields#concept-adr-ktr-gfb "")。 |
| `\` | 转义符号，用于转义`""`（双引号），转义后的双引号表示符号本身。例如日志内容为`instance_id:nginx"01"`，您可以使用`instance_id:nginx\"01\"`进行查询。 |
| `*` | 通配符查询，匹配零个、单个、多个字符。例如`host:www*com`。<br>**说明**<br>日志服务会在所有日志中为您查询到符合条件的100个词，返回包含这100个词并满足查询条件的所有日志。 |
| `?` | 通配符查询，匹配单个字符。例如`host:aliyund?c`。 |
| `>` | 查询某字段值大于某数值的日志。例如`request_time>100`。 |
| `>=` | 查询某字段值大于或等于某数值的日志。例如`request_time>=100`。 |
| `<` | 查询某字段值小于某数值的日志。例如`request_time<100`。 |
| `<=` | 查询某字段值小于或等于某数值的日志。例如`request_time<=100`。 |
| `=` | 查询某字段值等于某数值的日志。针对double、long类型的字段，`=`和`:`作用相同。例如`request_time=100`等同于`request_time:100`。 |
| `in` | 查询某字段值处于某数值范围内的日志，中括号表示闭区间，小括号表示开区间，两个数字之间使用空格分隔。例如`request_time in [100 200]`或`request_time in (100 200]`。<br>**重要**<br>in只能为小写字母。 |
| `__source__` | 查询某个日志源的日志，支持通配符。例如`__source__:192.0.2.*`。<br>**重要**<br>日志服务中的\_\_source\_\_为保留字段，可缩写为source。如果您自定义的字段中存在source字段，则会与日志服务保留字段source冲突，此时您需要使用Source、SOURCE等词查询自定义的字段。 |
| `__tag__` | 通过元数据信息查询日志。例如`__tag__:__receive_time__:1609837139`。 |
| `__topic__` | 查询某日志主题下的日志。例如`__topic__:nginx_access_log`。 |

### **步骤三：确定匹配模式**

根据掌握的关键词信息及实际业务场景的需要灵活控制使用精准查询还是模糊查询。

|     |     |     |
| --- | --- | --- |
| **查询方式** | **说明** | **示例** |
| 精确查询 | 使用完整的词进行查询。<br>日志服务查询采用的是分词法，精确查询时并不能完全匹配关键词。例如查询语句为`abc def`，查询结果将包含所有`abc`和`def`的日志，无法完全匹配目标短语。如果您要完全匹配短语`abc def`，可以使用短语查询或者Like语法。更多信息，请参见 [短语查询](https://help.aliyun.com/zh/sls/phrase-search#concept-2197127 "")、 [如何精准查询日志](https://help.aliyun.com/zh/sls/how-do-i-query-logs-by-using-exact-match#concept-2089193 "")。 | - `host:example.com`表示查询`host`字段值包含`example.com`的日志。<br>  <br>- `PUT and cn-shanghai`表示查询同时包含关键字`PUT`和`cn-shanghai`的日志。<br>  <br>- `* | Select * where http_user_agent like '%like Gecko%'`表示查询`http_user_agent`字段值中包含短语`like Gecko`的日志。<br>  <br>- `#"redo_index/1"`表示查询包含短语`redo_index/1`的日志。 |
| 模糊查询 | 在查询语句中指定一个64个字符以内的词，在词的中间或者末尾加上模糊查询关键字，即星号（\*）或问号（?），日志服务会在所有日志中为您查询到符合条件的100个词，返回包含这100个词并满足查询条件的所有日志。指定的词越精确，查询结果越精确。<br>**重要**<br>- 星号（\*）或问号（?）不能用在词的开头。<br>  <br>- long数据类型和double数据类型不支持使用星号（\*）或问号（?）进行模糊查询。可以使用数值范围进行模糊查询，例如status in \[200 299\]。<br>  <br>模糊查询是一种采样查询，查询机制如下所示：<br>- 开启字段索引，且指定某个字段进行查询时，日志服务从该字段的索引数据中随机采样，返回部分结果并不是全量扫描底层数据。<br>  <br>- 开启全文索引，且没有指定某个字段进行查询时，日志服务从全文索引数据中随机采样，返回部分结果并不是全量扫描底层数据。 | - `request_time>60 and request_method:Ge*`表示查询`request_time`字段值大于`60`且`request_method`字段值以`Ge`开头的日志。<br>  <br>- `addr*`表示在所有日志中查找以`addr`开头的100个词，并返回包含这些词的日志。<br>  <br>- `host:www.yl*`表示在所有日志中查找`host`字段值以`www.yl`开头的100个词，并返回包含这些词的日志。<br>  <br>更多信息，请参见 [如何模糊查询日志？](https://help.aliyun.com/zh/sls/how-do-i-query-logs-by-using-fuzzy-match#concept-2495512 "")。 |

## 查询语句示例

同一条查询语句，针对不同的日志内容和索引配置时，会有不同的查询结果。本文基于如下日志样例和索引介绍查询语句示例。

text、double、long类型

json类型

### 日志样例

本文以Nginx访问日志为例，介绍常见的查询语句。

![日志样例 ](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4630055461/p407021.png)

### 索引配置

在查询日志前，请确保已 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#task-jqz-v55-cfb "")。检查索引配置的步骤，如下所示：

1. 在LogStore的 **查询/分析** 页面，选择**查询分析属性** \> **属性**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9020091371/p872705.png)

2. 在打开的查询分析页面，查看是否已配置字段索引。![索引](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5865116461/p409681.png)


### 普通查询示例

|     |     |     |
| --- | --- | --- |
| **查询需求** | **查询语句** | **调试** |
| 查询GET请求成功（状态码为200~299）的日志。 | ```sql<br>request_method:GET and status in [200 299]<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/waf-demo-log/logsearch/waf-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF9tZXRob2Q6R0VUIGFuZCBzdGF0dXMgaW4gWzIwMCAyOTld) |
| 查询来自非杭州地域的GET请求的日志。 | ```sql<br>request_method:GET not region:cn-hangzhou<br>``` | 无 |
| 查询GET请求或POST请求的日志。 | ```sql<br>request_method:GET or request_method:POST<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF9tZXRob2Q6R0VUIG9yIHJlcXVlc3RfbWV0aG9kOlBPU1Q%3D) |
| 查询非GET请求的日志。 | ```sql<br>not request_method:GET<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3Dbm90IHJlcXVlc3RfbWV0aG9kOkdFVA%3D%3D) |
| 查询GET请求或POST请求成功的日志。 | ```sql<br>(request_method:GET or request_method:POST) and status in [200 299]<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKHJlcXVlc3RfbWV0aG9kOkdFVCBvciByZXF1ZXN0X21ldGhvZDpQT1NUKSBub3Qgc3RhdHVzIGluIFsyMDAgMjk5XQ%3D%3D) |
| 查询GET请求或POST请求失败的日志。 | ```sql<br>(request_method:GET or request_method:POST) not status in [200 299]<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DKHJlcXVlc3RfbWV0aG9kOkdFVCBvciByZXF1ZXN0X21ldGhvZDpQT1NUKSBub3Qgc3RhdHVzIGluIFsyMDAgMjk5XQ%3D%3D) |
| 查询GET请求成功（状态码为200~299）且请求时间小于60秒的日志。 | ```sql<br>request_method:GET and status in [200 299] not request_time>=60<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF9tZXRob2Q6R0VUIGFuZCBzdGF0dXMgaW4gWzIwMCAyOTldIG5vdCByZXF1ZXN0X3RpbWU%2BPTYw) |
| 查询请求时间为60秒的日志。 | ```sql<br>request_time:60<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log%3FqueryString=request_time:60) |
| ```sql<br>request_time=60<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log%3FqueryString=request_time=60) |
| 查询请求时间大于等于60秒，并且小于200秒的日志。 | ```sql<br>request_time>=60 and request_time<200<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF90aW1lPj02MCBhbmQgcmVxdWVzdF90aW1lPDIwMA%3D%3D) |
| ```sql<br>request_time in [60 200)<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF90aW1lIGluIFs2MCAyMDAp) |\
| 查询request\_time字段是否存在。 | ```sql<br>request_time:*<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF90aW1lOiogbm90IHJlcXVlc3RfdGltZSA%2BIC0xMDAwMDAwMDAwMA%3D%3D%26queryTimeType%3D99) |\
| 查询request\_time字段值为空或非法数字的日志。 | ```sql<br>(request_time:"") or (not request_time > -10000000000)<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF90aW1lOiogbm90IHJlcXVlc3RfdGltZSA%2BIC0xMDAwMDAwMDAwMA%3D%3D%26queryTimeType%3D99) |\
| 查询包含request\_time字段且字段值为数字的日志。 | ```sql<br>request_time > -1000000000<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF90aW1lID4gLTEwMDAwMDAwMDA%3D) |\
| 查询包含and的日志。 | ```sql<br>"and"<br>```<br>**说明**<br>此处的and为普通字符串，不代表运算符。 | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DImFuZCI%3D) |\
| 查询request method字段值是PUT的日志。 | ```sql<br>"request method":PUT<br>```<br>**重要**<br>字段名request method中存在空格，在查询时需使用双引号（""）包裹。 | 无 |\
| 查询日志主题为HTTPS或HTTP的日志。 | ```sql<br>__topic__:HTTPS or __topic__:HTTP<br>``` | 无 |\
| 查询采集于192.0.2.1主机的日志。 | ```sql<br>__tag__:__client_ip__:192.0.2.1<br>```<br>此处的`__tag__:__client_ip__`为日志服务保留字段，表示日志所在主机的IP地址。更多信息，请参见 [保留字段](https://help.aliyun.com/zh/sls/reserved-fields#concept-adr-ktr-gfb "")。<br>**重要**<br>通过数据加工或者Logtail插件处理的日志，其tag中的key会被转换成普通key，即查询时需使用双引号（""）包裹字段名，例如`"__tag__:__client_ip__":192.0.2.1`。 | 无 |\
| 查询包含`192.168.XX.XX`的日志。 | ```sql<br>* | select * from log where key like '192.168.%.%'<br>```<br>更多信息，请参见 [通过SQL的like语法进行精确的模糊查询](https://help.aliyun.com/zh/sls/how-do-i-query-logs-by-using-fuzzy-match#section-am6-sxf-dav "")。 | 无 |\
| 查询remote\_user字段值不为空的日志。 | ```sql<br>not remote_user:""<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3Dbm90IHJlbW90ZV91c2VyOiIi) |\
| 查询remote\_user字段值为空的日志。 | ```sql<br>remote_user:""<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVtb3RlX3VzZXI6IiI%3D) |\
| 查询remote\_user字段值不为null的日志。 | ```sql<br>not remote_user:"null"<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3Dbm90IHJlbW90ZV91c2VyOiJudWxsIg%3D%3D) |\
| 查询不存在remote\_user字段的日志。 | ```sql<br>not remote_user:*<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3Dbm90IHJlbW90ZV91c2VyOio%3D) |\
| 查询存在remote\_user字段的日志。 | ```sql<br>remote_user:*<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVtb3RlX3VzZXI6Kg%3D%3D) |\
| 查询城市字段值不为上海的日志。 | ```sql<br>not 城市:上海<br>```<br>**说明**<br>当查询中文字符串时，需要在配置索引时，打开 **包含中文** 开关。更多信息，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#task-jqz-v55-cfb "")。 | 无 |\
\
### **模糊查询** 示例\
\
|     |     |     |\
| --- | --- | --- |\
| **查询需求** | **查询语句** | **调试** |\
| 查询包含以cn开头的词的日志。 | ```sql<br>cn*<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DY24q) |\
| 查询region字段值是以cn开头的日志。 | ```sql<br>region:cn*<br>``` | 无 |\
| 查询region字段值包含cn\*的日志。 | ```sql<br>region:"cn*"<br>```<br>**说明**<br>此处的`cn*`为一个独立词。例如：<br>- 如果日志内容为`region:cn*,en`，分词符为半角逗号（,），则该日志内容被拆分为`region`、`cn*`和`en`，您可以通过上述语句查询到该日志。<br>  <br>- 如果日志内容为`region:cn*hangzhou`，则`cn*hangzhou`为一个整体，您执行上述语句无法查询到该日志。 | 无 |\
| 查询包含以mozi开头，以la结尾，中间还有一个字符的词的日志。 | ```sql<br>mozi?la<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DbW96aT9sYQ%3D%3D) |\
| 查询包含以mo开头，以la结尾，中间包含零个、单个或多个字符的词的日志。 | ```sql<br>mo*la<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DbW8qbGE%3D%26queryTimeType%3D99) |\
| 查询包含以moz开头的词和以sa开头的词的日志。 | ```sql<br>moz* and sa*<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DbW96KiBhbmQgc2Eq) |\
| 查询region字段值以hai结尾的所有日志。 | 目前使用查询语句无法查询到对应的日志，您可以使用SQL分析中的Like语法进行查询。更多信息，请参见 [通过SQL的like语法进行精确的模糊查询](https://help.aliyun.com/zh/sls/how-do-i-query-logs-by-using-fuzzy-match#section-am6-sxf-dav "")。<br>```sql<br>*| select * from log where region like '%hai'<br>``` | 无 |\
| 查询message字段值以`"get_time: 0.`开头的所有日志。 | 使用SQL分析中的 [like](https://help.aliyun.com/zh/sls/how-do-i-query-logs-by-using-fuzzy-match "") 语法进行查询。<br>```sql<br>*| select message where message like '"get_time: 0.%'<br>```<br>或者使用 [SPL中的where指令](https://help.aliyun.com/zh/sls/spl-instructions-and-functions/#745dfd92b6yyn "") 进行过滤查询。<br>```sql<br>*| where message like '"get_time: 0.%'<br>``` | 无 |\
\
### **基于分词符的查询** 示例\
\
日志服务会根据分词符，将日志内容拆分成多个词。日志服务默认配置的分词符为`, '";=()[]{}?@&<>/:\n\t\r`。如果设置 **分词符** 为空，则字段值将被当成一个整体，您只能通过完整字符串或模糊查询查找对应的日志。如何设置分词符，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#task-jqz-v55-cfb "")。\
\
例如http\_user\_agent字段值为`Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.2 (KHTML, like Gecko) Chrome/192.0.2.0 Safari/537.2`。\
\
- 设置 **分词符** 为空时，该字段值将被当成一个整体，则使用`http_user_agent:Chrome`查询语句进行查询时，无法查询到日志。\
\
- 设置 **分词符** 为`, '";=()[]{}?@&<>/:\n\t\r`后，该字段值拆分为`Mozilla`、`5.0`、`Windows`、`NT`、`6.1`、`AppleWebKit`、`537.2`、`KHTML`、`like`、`Gecko`、`Chrome`、`192.0.2.0`、`Safari`、`537.2`。可以使用`http_user_agent:Chrome`等查询语句进行查询。\
\
\
**重要**\
\
当查询关键字中包含分词符时，您可以使用短语查询或者Like语法。例如：\
\
- 短语查询：`#"redo_index/1"`。更多信息，请参见 [短语查询](https://help.aliyun.com/zh/sls/phrase-search#concept-2197127 "")。\
\
- Like语法：`* | select * from log where key like 'redo_index/1'`。\
\
\
|     |     |     |\
| --- | --- | --- |\
| **查询需求** | **查询语句** | **调试** |\
| 查询http\_user\_agent字段值中包含Chrome的日志。 | ```sql<br>http_user_agent:Chrome<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DaHR0cF91c2VyX2FnZW50OkNocm9tZQ%3D%3D) |\
| 查询http\_user\_agent字段值中包含Linux和Chrome的日志。 | ```sql<br>http_user_agent:Linux and http_user_agent:Chrome<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DaHR0cF91c2VyX2FnZW50OkxpbnV4IGFuZCBodHRwX3VzZXJfYWdlbnQ6Q2hyb21l) |\
| ```sql<br>http_user_agent:"Linux Chrome"<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DaHR0cF91c2VyX2FnZW50OiJMaW51eCBDaHJvbWUi) |\
| 查询http\_user\_agent字段值中包含Firefox或Chrome的日志。 | ```sql<br>http_user_agent:Firefox or http_user_agent:Chrome<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DaHR0cF91c2VyX2FnZW50OkZpcmVmb3ggb3IgaHR0cF91c2VyX2FnZW50OkNocm9tZQ%3D%3D) |\
| 查询request\_uri字段值包含/request/path-2的日志。 | ```sql<br>request_uri:/request/path-2<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF91cmk6L3JlcXVlc3QvcGF0aC0y) |\
| 查询request\_uri字段值以/request开头，但不包含/file-0的日志。 | ```sql<br>request_uri:/request* not request_uri:/file-0<br>``` | [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log?encode%3Dbase64%26queryString%3DcmVxdWVzdF91cmk6L3JlcXVlc3QqIG5vdCByZXF1ZXN0X3VyaTovZmlsZS0w) |\
| 完全匹配包含短语`redo_index/1`的日志。 | - `#"redo_index/1"`<br>  <br>- `* | select * from log where key like 'redo_index/1'`<br>  <br>**说明**<br>通过短语查询或者Like语法，可完全匹配目标短语。使用普通的精确查询，将匹配`redo_index`、`1`等词。 | 无 |\
\
### **关键词转义示例**\
\
- #### **在查询语句中**\
\
\
\
使用`""`（双引号）包裹一个语法关键词，可以将该语法关键词转换成普通字符。在字段查询中`""`内的所有词被当成一个整体。\
\
\
\
  - 当字段名或字段值中存在特殊字符（空格、中文、`:`、`-`等）、语法关键词（`and`、`or`等）等内容时，需要使用`""`包裹。例如`"and"`表示查询包含and的日志，此处的and不代表运算符。\
\
  - 日志服务保留以下运算符的使用权，如果需要使用以下运算符作为查询关键字，请使用`""`包裹：`sort`、`asc`、`desc`、`group by`、`avg`、`sum`、`min`、`max`和`limit`。\
\
  - 通过数据加工或者Logtail插件处理的日志，其tag中的key会被转换成普通key，即查询时需使用`""`包裹字段名，例如`"__tag__:__client_ip__":192.0.2.1`，此处的`__tag__:__client_ip__`为日志服务保留字段，表示日志所在主机的IP地址。更多信息，请参见 [保留字段](https://help.aliyun.com/zh/sls/reserved-fields#concept-adr-ktr-gfb "")。\
\
\
|     |     |\
| --- | --- |\
| **查询需求** | **查询语句** |\
| 查询`request method`字段值为`PUT`的日志。字段名`request method`中存在空格，需使用双引号（""）包裹。 | ```sql<br>"request method":PUT<br>``` |\
| 查询`system error description`字段值中包含`DB`的日志。字段名`system error description`中存在空格。 | ```sql<br>"system error description":DB*<br>``` |\
| 查询`region`字段值包含`cn*`的日志。这里的`cn*`为一个字符串。如果日志内容为`region:cn*,en`，分词符为半角逗号（,），则该日志内容被拆分为`region`、`cn*`和`en`，可通过右侧语句查询到该日志。 | ```sql<br>region:"cn*"<br>``` |\
| 查询`remote_user`字段值为空的日志。 | ```sql<br>remote_user:""<br>``` |\
| 查询`Authorization`字段值为`Bearer 12345`的日志。字段值`Bearer 12345`中存在空格。 | ```sql<br>"Authorization": "Bearer 12345"<br>``` |\
| 分析`errorContent`字段值包含`The body is not valid json string`的日志。字段值中存在空格。 | ```sql<br>* | select * where errorContent like '%The body is not valid json string%'<br>``` |\
| 查询采集于`192.0.2.1`主机的日志。 | ```sql<br>"__tag__:__client_ip__":192.0.2.1<br>``` |\
\
- #### **在分析语句中**\
\
\
\
  - 当字段名、表名等专有名词中存在特殊字符（空格、中文、`:`、`-`等）、语法关键词（`and`、`or`等）等内容时，需要使用`""`包裹。\
\
  - 表示字符串的字符必须使用`''`（单引号）包裹。无符号包裹或被`""`（双引号）包裹的字符表示字段名或列名。例如：`'status'`表示字符串status，`status`或`"status"`表示日志字段status。\
\
\
|     |     |\
| --- | --- |\
| **查询需求** | **查询语句** |\
| 查询包含`192.168.XX.XX`的日志。 | ```sql<br>* | select * from log where key like '192.168.%.%'<br>``` |\
| 计算请求时长的前10名。 | 列名`top 10`中存在空格，需使用双引号（""）包裹。<br>```sql<br>* | SELECT max(request_time,10) AS "top 10"<br>``` |\
| 统计不同请求状态对应的日志数量。 | 此处`content`字段的索引为JSON类型。更多信息，请参见 [如何查询和分析有索引的JSON字段](https://help.aliyun.com/zh/sls/faq-about-the-query-and-analysis-of-json-logs#section-b2i-0tc-ba3 "")。<br>```sql<br>* | SELECT "content.status", COUNT(*) AS PV GROUP BY "content.status"<br>``` |\
\
### **日志样例**\
\
```json\
{\
  "timestamp": "2025-03-21T14:35:18Z",\
  "level": "ERROR",\
  "service": {\
    "name": "payment-processor",\
    "version": "v2.8.1",\
    "environment": "production"\
  },\
  "error": {\
    "code": 5031,\
    "message": "Failed to connect to third-party API",\
    "details": {\
      "endpoint": "https://api.paymentgateway.com/v3/verify",\
      "attempts": 3,\
      "last_response": {\
        "status_code": 504,\
        "headers": {\
          "Content-Type": "application/json",\
          "X-RateLimit-Limit": "100"\
        }\
      }\
    }\
  },\
  "user": {\
    "id": "usr-9a2b3c4d",\
    "session": {\
      "id": "sess-zxy987",\
      "device": {\
        "type": "mobile",\
        "os": "Android 14",\
        "network": "4G"\
      }\
    }\
  },\
  "trace": {\
    "correlation_id": "corr-6f5e4d3c",\
    "span_id": "span-00a1b2"\
  }\
}\
```\
\
### **索引配置**\
\
在查询日志前，请确保已 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#task-jqz-v55-cfb "")。检查索引配置的步骤，如下所示：\
\
1. 在LogStore的 **查询/分析** 页面，选择**查询分析属性** \> **属性**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9020091371/p872705.png)\
\
2. 在打开的查询分析页面，查看是否已配置字段索引。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2604082471/p932759.png)\
\
\
### **示例**\
\
|     |     |\
| --- | --- |\
| **查询需求** | **查询语句** |\
| 查询请求错误的日志。 | ```sql<br>level:error<br>``` |\
| 查询用户ID为`usr-9a2b3c4d`的所有请求。 | ```sql<br>user.id:usr-9a2b3c4d<br>``` |\
| 查询用户ID为`usr-9a2b3c4d`，并且查看错误状态。 | ```sql<br>user.id:usr-9a2b3c4d and error.details.last_response.status_code :504<br>``` |\
\
## **常见问题**\
\
### **无法找到想要的日志**\
\
[查询不到日志的排查思路](https://help.aliyun.com/zh/sls/user-guide/what-do-i-do-if-no-results-are-returned-when-i-query-a-log "")。\
\
### **JSON日志问题**\
\
[查询和分析JSON日志的常见问题](https://help.aliyun.com/zh/sls/faq-about-the-query-and-analysis-of-json-logs "")\
\
### **查询错误排查**\
\
- [日志查询常见问题](https://help.aliyun.com/zh/sls/user-guide/faq-about-log-query "")\
\
- [查询与分析日志的常见报错](https://help.aliyun.com/zh/sls/resolve-common-errors-that-may-occur-when-i-query-and-analyze-logs "")\
\
\
## 相关文档\
\
- 分析函数和语法，请参见 [分析函数和语法](https://help.aliyun.com/zh/sls/log-analysis-overview#section-x2l-vkq-tdb "")。\
\
- [优化查询的方法](https://help.aliyun.com/zh/sls/optimize-queries "")\
\
- 日志查询示例\
\
  - [如何精确的按照时间排序查询日志](https://help.aliyun.com/zh/sls/how-to-precisely-sort-query-logs-by-time "")\
\
  - [查询和分析网站日志](https://help.aliyun.com/zh/sls/query-and-analyze-website-logs "")\
\
  - [分析负载均衡7层访问日志](https://help.aliyun.com/zh/sls/analyze-layer-7-access-logs-of-slb "")\
\
  - 查询JSON日志（字段值为JSON对象、JSON数组）的查询和分析的示例，请参见 [查询和分析JSON日志](https://help.aliyun.com/zh/sls/query-and-analyze-json-logs#section-nzs-og7-z2n "")。