### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[索引模式查询与分析](https://help.aliyun.com/zh/sls/query-and-analyze-logs-in-index-mode/)创建索引

# 创建索引

更新时间：2025-05-16 01:53:56

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：索引模式查询与分析](https://help.aliyun.com/zh/sls/query-and-analyze-logs-in-index-mode/)[下一篇：数据类型](https://help.aliyun.com/zh/sls/data-types)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

为什么需要创建索引

索引类型

全文索引

字段索引

创建索引

控制台方式

API方式

SDK方式

CLI方式

更新索引

操作步骤

关闭索引

操作步骤

索引配置示例

示例1

示例2

示例3

索引流量说明

全文索引

字段索引

计费说明

按写入数据量计费的logstore

按使用功能计费的logstore

后续步骤

常见问题

如需对采集到Logstore中的日志进行查询和分析，则必须创建索引。本文为您介绍日志服务索引概念、索引类型、创建索引、关闭索引、配置示例和计费说明等。

创建索引

## **为什么需要创建索引**

通常我们使用关键词从原始日志中检索想要的内容，例如包含`curl`的日志：`curl/7.74.0`。如果不进行切分，该日志文本会作为一个整体，不能和关键词`curl`完全对应，因此不会被日志服务检索到。

为了便于检索，需要将日志切分成独立、可搜索的词。日志切分由分词符实现，这些符号决定了日志文本内容被切分的位置。以该日志为例，使用分词符`\n\t\r,;[]{}()&^*#@~=<>/\?:'"`进行分割，得到的词是`curl`、`7.74.0`。日志服务基于切分出的关键词建立索引。创建索引后，您才能对日志进行查询和分析。

日志服务Project支持创建全文索引和字段索引。如果您同时创建了全文索引和字段索引，以字段索引的配置为准。

## **索引类型**

### 全文索引

全文索引根据 **分词符** 直接将整个日志切分成多个 **text** 类型的词语。创建全文索引后，可以通过关键词进行查询，例如查询语句：`Chrome or Safari` ，查询包括`Chrome`或`Safari`的日志。

**重要**

- **分词符** 不支持中文，开启 **包含中文** 选项，日志服务会自动按照中文分词。

- 如果只配置全文索引，则只能使用全文查询功能。更多信息，请参见 [查询语法与功能](https://help.aliyun.com/zh/sls/query-syntax/ "")。


### 字段索引

字段索引将日志根据字段名称（KEY）进行区分，然后在字段内使用分词符进行分割。字段索引支持 **text**、 **long**、 **double** 和 **JSON** 四种类型的数据。更多信息，请参见 [数据类型](https://help.aliyun.com/zh/sls/data-types "")。创建字段索引后，可以指定字段名称和字段值（`Key:Value`）进行查询，也可以使用SELECT语句。更多信息，请参见 [查询语法与功能](https://help.aliyun.com/zh/sls/query-syntax/#835e539d9flba "")。

**重要**

- 如需对字段进行查询或分析（SELECT语句），必须创建字段索引。字段索引的优先级高于全文索引，如果同时创建了全文索引和字段索引，以字段索引的配置为准。

- **text** 类型的字段，可以使用全文查询语句、字段查询语句和分析语句（SELECT）。

  - 如果未开启全文索引，全文查询语句是从所有text类型的字段中查询结果。

  - 如果已开启全文索引，全文查询语句是从所有日志中查询结果。
- **long** 和 **double** 类型的字段，可以使用字段查询语句和分析语句（SELECT）进行查询和分析。


## **创建索引**

**重要**

- 不同的索引配置，会产生不同的查询和分析结果，请根据您的需求，合理创建索引。创建索引后需要大约一分钟生效。

- 创建索引只对增量日志有效。如需查询历史日志，请使用 [重建索引](https://help.aliyun.com/zh/sls/reindex-logs-for-a-logstore "") 功能。

- 日志服务已为部分保留字段创建索引。更多信息，请参见 [保留字段](https://help.aliyun.com/zh/sls/reserved-fields#concept-adr-ktr-gfb "")。

其中`__topic__`和`__source__`的索引分词符为空，查询这两个字段时，关键字必须完全匹配。

- `__tag__`为前缀的字段不支持全文索引。只支持创建text类型的字段索引。您需要创建字段索引后，才能执行查询和分析操作，例如`*| select "__tag__:__receive_time__"`。

- 日志中存在同名字段（例如都为request\_time）时，日志服务会将其中一个字段名显示为request\_time\_0，底层存储的字段名仍为request\_time。因此在创建索引、查询、分析、投递、加工时，只能使用原始字段名request\_time。


### **控制台方式**

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。

2. 在Project列表区域，单击目标Project。

3. 在**日志存储** \> **日志库**页签中，单击目标Logstore。

4. 在Logstore的 **查询和分析** 页面，单击 **开启索引**。



**说明**





开启后等待1min左右即可查询最新数据。





![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8217682371/p870353.png)

5. （可选）关闭自动更新索引

当Logstore为云产品专属Logstore或内部Logstore时，默认打开索引 **自动更新** 开关，后续如有版本更新时可以升级到内置索引最新版本。如果需要创建索引，请在 **查询分析** 面板中，关闭 **自动更新** 开关。



**警告**





删除云产品专属Logstore的索引会影响相关报表、告警等功能的使用。





![自动更新索引](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6185572561/p439697.png)

6. 创建索引




##### 创建全文索引







单击 **开启索引** 后， **全文索引** 开关默认打开。您可根据需要选择是否打开 **日志聚类**、 **大小写敏感**、 **包含中文** 功能，也可选择指定 **分词符** 或自定义 **分词符**。



页面配置如下所示：



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1579182371/p870418.png)





##### **配置项说明如下所示：**







|     |     |
| --- | --- |
| **参数** | **说明** |
| **日志聚类** | 打开 **日志聚类** 开关后，日志服务在采集文本日志时会自动聚合相似度高的日志，提取共同的日志模式，帮助您快速掌握日志整体情况。更多信息，请参见 [日志聚类](https://help.aliyun.com/zh/sls/logreduce#concept-fkn-zwm-cgb "")。 |
| **大小写敏感** | 查询时是否区分英文字母的大小写。 <br>   - 打开 **大小写敏感** 开关，则查询时区分大小写。例如某条日志含有`internalError`，那么您只能使用`internalError`才能查询到该日志。<br>     <br>   - 关闭 **大小写敏感** 开关，则查询时不区分大小写。例如某条日志含有`internalError`，那么您使用关键字`INTERNALERROR`和`internalerror`都能查到该日志。 |
| **包含中文** | 查询时是否区分中英文。 <br>   - 打开 **包含中文** 开关后，如果日志中包含中文，则按照中文语法拆分中文内容，按照分词符的设置拆分英文内容。<br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     中文分词对写入速度会有一定影响，请根据需求谨慎设置。<br>     <br>   - 关闭 **包含中文** 开关后，按照分词符的设置拆分所有内容。<br>     <br>例如日志内容为user:SLS日志服务用户张先生。<br>   - 关闭 **包含中文** 开关后，按照分词符半角冒号（:）进行拆分，日志会被拆分为`user`、`SLS日志服务用户张先生`，您可以通过`user`或`SLS日志服务用户张先生`查找该日志。<br>     <br>   - 打开 **包含中文** 开关后，日志服务后台分词器将日志拆分为`user`、`SLS`、`日志服务`、`用户`和`张先生`，您通过`日志服务`或`张先生`等词都可以查找到该日志。 |
| **分词符** | 根据指定分词符，将日志内容拆分成多个词。日志服务的默认分词符为`, '";=()[]{}?@&<>/:\n\t\r`。当默认设置不能满足您的需求时，您可以自定义设置分词符。所有的ASCII码都可被定义为分词符。<br>如果设置 **分词符** 为空，则字段值将被当成一个整体，您只能通过完整字符串或模糊查询查找对应的日志。<br>例如日志内容为`/url/pic/abc.gif`。<br>   - 如果不设置任何分词符，整条日志被作为一个词`/url/pic/abc.gif`，您只能通过完整字符串`/url/pic/abc.gif`或模糊查询`/url/pic/*`查找该日志。<br>     <br>   - 如果设置分词符为正斜线（/），则原始日志被拆分为`url`、`pic`和`abc.gif`三个词，您通过任意一个词或词的模糊查询都可以找到该日志，例如`url`、`abc.gif`、`pi*`、`/url/pic/abc.gif`。<br>     <br>   - 如果设置分词符为正斜线（/）和半角句号（.），则原始日志被拆分为`url`、`pic`、`abc`和`gif`四个词，您通过任意一个词或词的模糊查询都可以找到该日志。 |









##### 创建字段索引







单击 **开启索引** 后。您可在 **查询分析** 页面单击 **自动生成索引**。日志服务会根据采集时预览数据中的第一条内容，自动生成字段索引。如需自定义字段索引，可单击页面下方的`+`创建，具体字段说明请参见 [配置项说明](https://help.aliyun.com/zh/sls/create-indexes#4fae80eab5ufa "")。



首次打开时页面如下所示：![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8217682371/p870373.png)



字段索引配置项如下所示：



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8795504371/p879620.png)





##### **配置项说明** 如下所示：







|     |     |
| --- | --- |
| **参数** | **说明** |
| **字段名称** | 日志字段名称（KEY），例如`client_ip`。<br>字段名称只能包括字母、数字或下划线（\_），且只能以字母或下划线（\_）开头。<br>**重要**<br>   - 设置公网IP地址、Unix时间戳等`__tag__`字段的索引时，需设置 **字段名称** 为`__tag__:KEY`形式，例如`__tag__:__receive_time__`。更多信息，请参见 [保留字段](https://help.aliyun.com/zh/sls/reserved-fields#concept-adr-ktr-gfb "")。<br>     <br>   - `__tag__`字段不支持数值类型索引，请将所有`__tag__`字段的索引的 **类型** 设置为 **text**。 |
| **类型** | 日志字段值（Value）的数据类型，可选值为 **text**、 **long**、 **double** 和 **json**。更多信息，请参见 [数据类型](https://help.aliyun.com/zh/sls/data-types#concept-ijf-qs3-ffb "")。 <br>**long** 和 **double** 类型不支持设置 **大小写敏感**、 **包含中文** 和 **分词符**。 |
| **别名** | 字段的别名，例如设置`client_ip`字段的别名为`ip`。 <br>字段别名只能包括字母、数字或下划线（\_），且只能以字母或下划线（\_）开头。<br>**重要**<br>别名仅用于分析语句（SELECT语句），查询语句中仍需使用原始字段名称。更多信息，请参见 [列的别名](https://help.aliyun.com/zh/sls/column-aliases#reference-htb-lmq-zdb "")。 |
| **大小写敏感** | 查询时是否区分英文字母的大小写。 <br>   - 打开 **大小写敏感** 开关，则查询时区分大小写。例如某条日志含有`internalError`，那么您只能使用`internalError`才能查询到该日志。<br>     <br>   - 关闭 **大小写敏感** 开关，则查询时不区分大小写。例如某条日志含有`internalError`，那么您使用关键字`INTERNALERROR`和`internalerror`都能查到该日志。 |
| **分词符** | 根据指定分词符，将日志内容拆分成多个词。日志服务的默认分词符为`, '";=()[]{}?@&<>/:\n\t\r`。当默认设置不能满足您的需求时，您可以自定义设置分词符。所有的ASCII码都可被定义为分词符。<br>如果设置 **分词符** 为空，则字段值将被当成一个整体，您只能通过完整字符串或模糊查询查找对应的日志。<br>例如日志内容为`/url/pic/abc.gif`。<br>   - 如果不设置任何分词符，整条日志被作为一个词`/url/pic/abc.gif`，您只能通过完整字符串`/url/pic/abc.gif`或模糊查询`/url/pic/*`查找该日志。<br>     <br>   - 如果设置分词符为正斜线（/），则原始日志被拆分为`url`、`pic`和`abc.gif`三个词，您通过任意一个词或词的模糊查询都可以找到该日志，例如`url`、`abc.gif`、`pi*`、`/url/pic/abc.gif`。<br>     <br>   - 如果设置分词符为正斜线（/）和半角句号（.），则原始日志被拆分为`url`、`pic`、`abc`和`gif`四个词，您通过任意一个词或词的模糊查询都可以找到该日志。 |
| **包含中文** | 查询时是否区分中英文。 <br>   - 打开 **包含中文** 开关后，如果日志中包含中文，则按照中文语法拆分中文内容，按照分词符的设置拆分英文内容。<br>     <br>     <br>     <br>     **重要**<br>     <br>     <br>     <br>     <br>     <br>     中文分词对写入速度会有一定影响，请根据需求谨慎设置。<br>     <br>   - 关闭 **包含中文** 开关后，按照分词符的设置拆分所有内容。<br>     <br>例如日志内容为user:SLS日志服务用户张先生。<br>   - 关闭 **包含中文** 开关后，按照分词符半角冒号（:）进行拆分，日志会被拆分为`user`、`SLS日志服务用户张先生`，您可以通过`user`或`SLS日志服务用户张先生`查找该日志。<br>     <br>   - 打开 **包含中文** 开关后，日志服务后台分词器将日志拆分为`user`、`SLS`、`日志服务`、`用户`和`张先生`，您通过`日志服务`或`张先生`等词都可以查找到该日志。 |
| **开启统计** | 打开 **开启统计** 功能后，您才能对该字段进行统计分析。 |

7. （可选）设置字段的最大长度

SQL分析过程中，默认为截取一定长度，日志服务的默认配置为`2048`字节，即2KB。如果您需要修改字段值的最大长度，可在 **查询分析** 页面底部设置 **统计字段（text）最大长度**，取值范围为64~16384字节。



**重要**





   - 更新索引配置只对增量数据有效。

   - 如果单个字段值长度超过最大长度，超出部分将被截断，不参与分析。


![设置字段最大长度](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1129372761/p542513.png)

### **API方式**

日志服务支持通过API方式管理索引。具体操作，请参见：

- [CreateIndex - 创建索引](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-createindex "")

- [GetIndex - 获取索引](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-getindex "")

- [UpdateIndex - 更新索引](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-updateindex "")

- [DeleteIndex - 删除索引](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-deleteindex "")


### **SDK方式**

日志服务支持通过多语言SDK进行索引管理，以下列举一些常用的SDK。更多信息，请参见 [SDK参考概述](https://help.aliyun.com/zh/sls/developer-reference/overview-of-log-service-sdk "")。

Java

Python

使用日志服务Java SDK方式管理索引的具体操作，请参见 [使用Java SDK管理索引](https://help.aliyun.com/zh/sls/developer-reference/use-log-service-sdk-for-java-to-manage-indexes "")。

使用日志服务Python SDK方式管理索引的具体操作，请参见 [使用Python SDK管理索引](https://help.aliyun.com/zh/sls/developer-reference/use-log-service-sdk-for-python-to-manage-indexes "")。

日志服务除自研的SDK外，还支持公共的阿里云SDK，关于阿里云SDK的使用方式，请参见[日志服务\_SDK中心-阿里云OpenAPI开发者门户](https://next.api.aliyun.com/api-tools/sdk/Sls?version=2020-12-30&language=python-tea&tab=primer-doc)。

### **CLI方式**

日志服务提供命令行工具CLI（Command Line Interface）管理索引。具体操作，请参见：

- [create\_index](https://help.aliyun.com/zh/sls/developer-reference/create-index "")

- [delete\_index](https://help.aliyun.com/zh/sls/developer-reference/delete-index "")

- [get\_index\_config](https://help.aliyun.com/zh/sls/developer-reference/get-index-config "")

- [update\_index](https://help.aliyun.com/zh/sls/developer-reference/update-index "")


## **更新索引**

### 操作步骤

在目标Logstore的 **查询和分析** 页面，选择**查询分析属性** \> **属性**。不同的索引配置，会产生不同的查询和分析结果，请根据您的需求，合理更新索引。更新索引后需要大约一分钟生效。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3813664371/p890913.png)

## **关闭索引**

**重要**

**关闭索引** 后，历史索引的存储空间将在当前Logstore的数据保存时间到期后，自动被清除。

### 操作步骤

在目标Logstore的 **查询和分析** 页面，选择**查询分析属性** \> **关闭索引**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0194954371/p879758.png)

## **索引配置示例**

### **示例1**

日志内容中有`request_time`字段，执行字段查询语句`request_time>100`。

- 只建立全文索引，返回同时包含`request_time`、`>`（非分词符）、`100`这三个词的日志。

- 只建立 **double**、 **long** 类型的字段索引，返回结果是`request_time`大于100的日志。

- 建立全文索引和 **double**、 **long** 类型的字段索引，`request_time`的全文索引失效，返回结果是`request_time`大于100的日志。


### **示例2**

日志内容中有`request_time`字段，执行全文查询语句`request_time`。

- 只建立 **double**、 **long** 类型的字段索引，无法查询到相关日志。

- 只建立全文索引，从所有日志文本中查询包括`request_time`的日志。

- 只建立text类型的字段索引，从字段索引是text类型的字段中查询包括`request_time`的日志。


### **示例3**

日志内容中有`status`字段，执行分析语句`* | SELECT status, count(*) AS PV GROUP BY status`。

- 只建立全文索引，无法查询到相关日志。

- 为`status`建立字段索引，返回结果是不同的状态码及对应的PV总数。


## 索引流量说明

### **全文索引**

所有字段名和字段值都将作为 **text** 类型存储，即字段名和字段值都被计入索引流量。

### **字段索引**

不同数据类型的字段的索引流量计算方式不同。

- **text** 类型：字段名和字段值都被计入索引流量中。

- **long** 类型和 **double** 类型：字段名不计入索引流量中，每个字段值所占的索引流量统一为8字节。

例如对`status`字段设置了索引（ **long** 类型），字段值为`200`，则字符串`status`不会被计入在索引流量中，`200`的索引流量统一为8字节。

- **JSON** 类型：字段名和字段值都被计入到索引流量中，包括未被创建索引的子节点。更多信息，请参见 [如何计算JSON类型字段的索引流量](https://help.aliyun.com/zh/sls/why-is-index-traffic-generated-for-json-subfields-that-are-not-indexed#concept-2143314 "")。

  - 如果未对子节点设置索引，则其索引流量按照 **text** 类型进行计算。

  - 如果对子节点设置了索引，则其索引流量按照其子节点数据类型（ **text**、 **long** 或 **double**）进行计算。

## 计费说明

### **按写入数据量计费的logstore**

- 创建的索引会占用存储空间，存储类型请参见 [管理智能存储分层](https://help.aliyun.com/zh/sls/data-tiered-storage-overview "")。

- 重建索引不产生费用。

- 索引流量计费请参见 [按写入数据量计费模式计费项](https://help.aliyun.com/zh/sls/billing-items-in-the-pay-per-data-write-mode "")。


### **按使用功能计费的logstore**

- 创建的索引会占用存储空间，存储类型请参见 [管理智能存储分层](https://help.aliyun.com/zh/sls/data-tiered-storage-overview "")。

- 创建索引会产生流量，索引流量计费请参见 [按使用功能计费模式计费项](https://help.aliyun.com/zh/sls/billable-items "") 中的索引流量-日志索引和索引流量-日志索引-查询型。降低索引流量的建议，请参见 [如何降低索引流量费用？](https://help.aliyun.com/zh/sls/how-do-i-reduce-index-traffic-fees "")。

- 重建索引会产生费用。计费项、计费价格和创建索引相同。


## 后续步骤

- 查询和分析的示例，请参见：

  - [Copilot：AI辅助SQL语句自动生成](https://help.aliyun.com/zh/sls/copilot-automatic-generation-of-ai-assisted-sql-statements "")

  - [查询与分析快速指引](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis "")

  - [查询和分析网站日志](https://help.aliyun.com/zh/sls/query-and-analyze-website-logs "")

  - [查询和分析JSON日志](https://help.aliyun.com/zh/sls/query-and-analyze-json-logs "")

  - [采集和查询分析Nginx监控日志](https://help.aliyun.com/zh/sls/collect-and-analyze-nginx-monitoring-logs "")

  - [分析负载均衡7层访问日志](https://help.aliyun.com/zh/sls/analyze-layer-7-access-logs-of-slb "")。

  - [查询轻量消息队列（原MNS）日志](https://help.aliyun.com/zh/sls/query-mns-logs "")
- 优化查询的方法，请参见 [提高查询分析日志速度的方法](https://help.aliyun.com/zh/sls/optimize-queries "")。

- 查询和分析JSON类型的网站日志，请参见 [查询和分析JSON日志](https://help.aliyun.com/zh/sls/query-and-analyze-json-logs "")。


## 常见问题

- 为什么导入日志后查询不到日志？






  - 检查已设置的分词符是否符合要求。

  - 索引配置只对新增日志生效，如果您要查询和分析历史数据，请使用重建索引功能。具体操作，请参见 [重建索引](https://help.aliyun.com/zh/sls/reindex-logs-for-a-logstore#task-2424026 "")。


- 如何完成双重条件查询？






需要使用两个条件查询日志时，只需同时输入两个语句即可。需要在Logstore中查询数据状态不是OK或者Unknown的日志。 直接搜索not OK not Unknown即可得到符合条件的日志。

- 如何查询包括包含多个关键字的日志？






以查询 **http\_user\_agent** 字段值中包含like Gecko的日志为例。



  - 短语查询。http\_user\_agent:#"like Gecko"。 [短语查询](https://help.aliyun.com/zh/sls/phrase-search#concept-2197127 "")

  - like语法。\\* \| Select \* where http\_user\_agent like '%like Gecko%'


- 如何在日志中搜索包含空格的关键字？






例如，当您搜索POS version时，会得到包含POS或者version的所有日志。如果使用双引号包裹，例如“POS version”，则会得到包含关键字POS version的所有日志。

- [日志查询常见问题](https://help.aliyun.com/zh/sls/user-guide/faq-about-log-query "")

- [查询与分析日志的常见报错](https://help.aliyun.com/zh/sls/resolve-common-errors-that-may-occur-when-i-query-and-analyze-logs "")

- [如何模糊查询日志？](https://help.aliyun.com/zh/sls/how-do-i-query-logs-by-using-fuzzy-match "")

- [查询和分析JSON日志的常见问题](https://help.aliyun.com/zh/sls/faq-about-the-query-and-analysis-of-json-logs "")

- [如何将日志下载到本地](https://help.aliyun.com/zh/sls/how-do-i-download-logs-to-a-local-device "")

- [为什么查询和分析时，字段值会被截断？](https://help.aliyun.com/zh/sls/index-and-query-faq/#6c6a39624402v "")