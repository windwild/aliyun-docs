### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据处理](https://help.aliyun.com/zh/sls/data-processing-sls/)[SPL语法](https://help.aliyun.com/zh/sls/spl-overview/)SPL基础语法

# SPL基础语法

更新时间：2025-08-14 04:28:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SPL语法](https://help.aliyun.com/zh/sls/spl-overview/)[下一篇：SPL指令与函数](https://help.aliyun.com/zh/sls/spl-instructions-and-functions/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

SPL语法

SPL语句

数据源

SPL指令表达式

指令表达式语法

参数说明

语法符号列表

SPL数据类型

本文介绍日志服务SPL基础语法。

## **SPL语法**

### **SPL语句**

SPL语句是多级数据处理语句，通过英文管道符（\|）连接，以英文分号（;）作为语句结束符。SPL语法结构如下：

- 语法















```default_language
<data-source> | <spl-expr> | <spl-expr> ;
```

- 参数说明




| **参数** | **说明** | **示例** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **说明** | **示例** |
| data-source | 数据源，包括SLS Logstore，以及SPL定义的 [数据集](https://help.aliyun.com/zh/sls/spl-general-reference#6cf6bde21flxz "")。在不同场景中的SPL数据源，请参见 [通用参考](https://help.aliyun.com/zh/sls/spl-general-reference#5f519d4b15z8x "")。 | `* | project status, body;` |
| \| | SPL管道。管道前面指令的输出会作为管道后面指令的输入。 |
| spl-expr | SPL指令表达式，详情请参见 [SPL语法](https://help.aliyun.com/zh/sls/spl-overview/#67a977403d4dc "")。 |


## 数据源

日志服务在不同场景中使用 SPL，数据源的定义存在差异，细节如下：

| **功能类型** | **Logstore索引过滤结果作为输入** | **字段名大小写敏感** | **全文字段\_\_line\_\_** | **最佳实践** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **功能类型** | **Logstore索引过滤结果作为输入** | **字段名大小写敏感** | **全文字段\_\_line\_\_** | **最佳实践** |
| **Logtail采集** | 不支持。使用星号（`*`）表示Logtail采集的全部原始数据作为输入，比如`* | parse-json content` | 敏感 | 不支持 | [使用SPL采集文本日志](https://help.aliyun.com/zh/sls/use-spl-to-collect-text-logs "") |
| **写入处理器** | 不支持。使用星号（`*`）表示写入的全部原始数据作为输入。 | 敏感 | 不支持 | [使用写入处理器处理云产品日志](https://help.aliyun.com/zh/sls/use-ingest-processors-to-process-cloud-product-logs "") |
| **实时消费** | 不支持。使用星号（`*`）表示Logstore全部原始数据作为输入。比如`* | where msg like '%wrong%'` | 敏感 | 不支持 | - [使用SDK基于SPL消费日志](https://help.aliyun.com/zh/sls/use-sdk-to-consume-logs-based-on-consumption-processor-spl "")<br>  <br>- [使用消费组基于SPL消费日志](https://help.aliyun.com/zh/sls/consume-logs-using-consumer-group-based-on-consumption-processor-spl "")<br>  <br>- [Flink SQL基于SPL实现行过滤与列裁剪](https://help.aliyun.com/zh/sls/flink-sql-implements-row-filtering-and-column-pruning-based-on-spl "")<br>  <br>- [Flink SQL基于SPL实现弱结构化分析](https://help.aliyun.com/zh/sls/flink-sql-implements-weakly-structured-analysis-based-on-spl "") |
| **数据加工（新版）** | 不支持。使用星号（`*`）表示Logstore全部原始数据作为输入。 | 敏感 | 不支持 | [最佳实践](https://help.aliyun.com/zh/sls/data-transformation-best-practices/ "") |
| **扫描查询** | 支持。先执行索引过滤，过滤结果再执行SPL处理。比如`error and msg:wrong | project level, msg` | 不敏感 | 支持 | [扫描（Scan）日志](https://help.aliyun.com/zh/sls/scan-logs "") |

## **SPL指令表达式**

SPL支持的指令请参见 [SPL指令与函数](https://help.aliyun.com/zh/sls/spl-instructions-and-functions/ "")。

### 指令表达式语法

```default_language
cmd -option=<option> -option ... <expression>, ... as <output>, ...
```

### 参数说明

|     |     |
| --- | --- |
| **参数** | **说明** |
| cmd | 指令名称。 |
| option | 指令执行参数，可选。使用时必须指定参数名，参数名以中划线`（-）`开头，参数顺序无要求。<br>支持如下2种参数类别：<br>- 键值参数`-option=<option>：`使用指令时以键值对的形式输入。<br>  <br>- 开关参数-option：指令定义中默认均为关闭状态，添加该参数即表示打开开关。 |
| expression | 指令对数据源执行处理逻辑，必填。使用时，无需指定参数名，但参数顺序必须与指令的定义保持一致。<br>表达式类别：<br>- SPL表达式<br>  <br>  - 字段名及其通配模式表达式，例如content。如果包含\[a-zA-Z\_\]以外的字符，需要使用双引号（""）包裹，例如`"__tag__:__path__"`。<br>    <br>  - 字段赋值表达式，直接对字段赋值例如`level='INFO'`，或者将正则表达式的提取结果赋值给字段例如`msg=regex_extract(content, '\S+')`。<br>- SQL表达式<br>  <br>  - 数据计算表达式返回值，例如`cast(status as int)>=500`。 |
| output | 处理结果中的输出字段。例如`| parse-csv content as a, b, c`。 |

## **语法符号列表**

在使用SPL语法时，以下是语法符号说明。

| **符号** | **说明** | **示例** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **符号** | **说明** | **示例** |
| \* | SLS Logstore数据作为SPL输入数据时的占位符。 | 将访问日志基于状态码进行过滤和分类处理，然后将其输出。<br>- SPL语句<br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  ```sql<br>  -- SPL处理结果定义为命名数据集src，作为后续SPL表达式的输入<br>  .let src = * <br>  | where status=cast(status as BIGINT);<br>  <br>  -- 以命名数据集src作为输入，筛选status字段为5xx的数据，定义数据集err，不输出<br>  .let err = $src<br>  | where status >= 500<br>  | extend msg='ERR';<br>  <br>  -- 以命名数据集src作为输入，筛选status字段为2xx的数据，定义数据集ok，不输出<br>  .let ok = $src<br>  | where status >= 200 and status < 300<br>  | extend msg='OK';<br>  <br>  -- 输出命名数据集err和ok<br>  $err;<br>  $ok;<br>  ```<br>  <br>- 输入数据<br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  ```yaml<br>  # 条目1<br>  status: '200'<br>  body: 'this is a test'<br>  <br>  # 条目2<br>  status: '500'<br>  body: 'internal error'<br>  <br>  # 条目3<br>  status: '404'<br>  body: 'not found'<br>  ```<br>  <br>- 输出结果<br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  ```yaml<br>  # 条目1: 数据集为err<br>  status: '500'<br>  body: 'internal error'<br>  msg: 'ERR'<br>  <br>  # 条目2: 数据集为ok<br>  status: '200'<br>  body: 'this is a test'<br>  msg: 'OK'<br>  ``` |
| . | 作为SPL语句的第一个字符时，表示SPL语法关键字。 |
| \| | SPL管道符，用于引出SPL指令表达式，语法格式为`| <spl-cmd> ...`。 |
| ; | SPL语句结束标识。单条语句，或多语句中最后一条的结束符可选。 |
| '...' | 字符串常量引用符号。 |
| "..." | 字段名称、字段名模式引用符号。 |
| -- | 注释单行内容。 |
| /\*...\*/ | 注释多行内容。 |
| $ | 命名数据集引用符，语法格式为`$<dataset-name>`。 |

## **SPL数据类型**

SPL日志字段数据类型说明如下表：

|     |     |     |
| --- | --- | --- |
| **类型类别** | **类型名称** | **类型说明** |
| 基本数值类型 | BOOLEAN | 布尔类型。 |
| TINYINT | 宽度为8位的整数类型。 |
| SMALLINT | 宽度为16位的整数类型。 |
| INTEGER | 宽度为32位的整数类型。 |
| BIGINT | 宽度为64位的整数类型。 |
| HUGEINT | 宽度为128位的整数类型。 |
| REAL | 宽度为32位可变精度浮点数类型。 |
| DOUBLE | 宽度为64位可变精度浮点数类型。 |
| TIMESTAMP | 精度为纳秒的UNIX时间戳类型。 |
| DATE | 日期数据类型，格式为YYYY-MM-DD。 |
| VARCHAR | 可变长度字符数据类型。 |
| VARBINARY | 可变长度二进制数据类型。 |
| 结构化数值类型 | ARRAY | 数组类型。元素访问使用`[]`，元素访问下标从1开始。<br>例如`* | extend a = ARRAY[0, 1, 2] | extend b = a[1]`。 |
| MAP | 字典类型，键只能是基本数值类型，值可以是任意类型。元素访问使用`[]`。<br>例如`* | extend a = MAP(ARRAY['foo', 'bar'], ARRAY[0, 1]) | extend b = a['foo']`。 |
| JSON类型 | JSON | JSON类型。 |

SPL数据处理过程中的数据类型转换说明，请参见 [通用参考](https://help.aliyun.com/zh/sls/spl-general-reference "")。