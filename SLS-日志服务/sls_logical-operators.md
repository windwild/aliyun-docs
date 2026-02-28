### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)[SQL分析语法与功能](https://help.aliyun.com/zh/sls/sql-syntax-and-functions/)[SQL函数](https://help.aliyun.com/zh/sls/sql-function/)逻辑运算符

# 逻辑运算符

更新时间：2024-03-11 03:25:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：比较运算符](https://help.aliyun.com/zh/sls/comparison-operators)[下一篇：单位换算函数](https://help.aliyun.com/zh/sls/unit-conversion-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

AND运算符

语法

参数说明

返回值类型

示例

OR运算符

语法

参数说明

返回值类型

示例

NOT运算符

语法

参数说明

返回值类型

示例

附录：真值表

本文介绍逻辑运算符的基本语法及示例。

日志服务支持如下逻辑运算符。

**重要**

- 在日志服务分析语句中，表示字符串的字符必须使用单引号（''）包裹，无符号包裹或被双引号（""）包裹的字符表示字段名或列名。例如：'status'表示字符串status，status或"status"表示日志字段status。

- 逻辑运算符优先级从高到低为not、and、or。您可以使用圆括号改变默认的计算顺序。

- 逻辑运算只支持输入值为true、false或null的布尔表达式。


| **运算符** | **语法** | **说明** | 支持SQL | 支持SPL |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **运算符** | **语法** | **说明** | 支持SQL | 支持SPL |
| [AND运算符](https://help.aliyun.com/zh/sls/logical-operators#section-pw8-5ul-lcn "") | _x_ AND _y_ | _x_和_y_的值都为true时，返回结果为true。 | √ | √ |
| [OR运算符](https://help.aliyun.com/zh/sls/logical-operators#section-cog-9xl-z3f "") | _x_ OR _y_ | _x_和_y_中任意一个的值为true时，返回结果为true。 | √ | √ |
| [NOT运算符](https://help.aliyun.com/zh/sls/logical-operators#section-nes-1zb-hjv "") | NOT _x_ | _x_的值为false时，返回结果为true。 | √ | √ |

## AND运算符

_x_和_y_的值都为true时，返回结果为true。

### 语法

```plaintext
x AND y
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为布尔表达式。 |
| _y_ | 参数值为布尔表达式。 |

### 返回值类型

boolean类型。

### 示例

SQL

SPL

如果status字段值为200且request\_method字段值为GET，则返回true。否则返回false。

- 查询和分析语句















```sql
*|SELECT status=200 AND request_method='GET'
```

- 查询和分析结果![AND运算符](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1786948261/p302497.png)


如果status字段值为200且request\_method字段值为GET，则返回true。否则返回false。

- SPL语句


```routeros
*|extend a = status=200 AND request_method='GET'
```

- SPL结果![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0174843071/p750449.png)


## OR运算符

_x_和_y_中任意一个的值为true时，返回结果为true。

### 语法

```plaintext
x OR y
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为布尔表达式。 |
| _y_ | 参数值为布尔表达式。 |

### 返回值类型

boolean类型。

### 示例

SQL

SPL

查找request\_uri字段值是以file-8或file-6的结尾的日志。

- 查询和分析语句















```plaintext
*|SELECT *  WHERE request_uri LIKE '%file-8' OR request_uri LIKE '%file-6'
```

- 查询和分析结果![OR](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2702282361/p302513.png)


查找request\_uri字段值是以file-8或file-6的结尾的日志。

- SPL语句


```routeros
*|WHERE request_uri LIKE '%file-8' OR request_uri LIKE '%file-6'
```

- SPL结果![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0174843071/p750454.png)


## NOT运算符

_x_的值为false时，返回结果为true。

### 语法

```plaintext
 NOT x
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为布尔表达式。 |

### 返回值类型

boolean类型。

### 示例

SQL

SPL

统计请求状态码不为200时的请求时长。

- 查询和分析语句















```plaintext
*|SELECT request_time WHERE NOT status=200
```

- 查询和分析结果![NOT](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2786948261/p302506.png)


查询请求状态码不为200时的日志信息。

- SPL语句


```routeros
*|WHERE NOT status=200
```

- SPL结果![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2107563071/p751579.png)


## 附录：真值表

_x_和_y_的值为true、false或null时，真值表如下所示。

| _x_ | _y_ | _x_ **AND** _y_ | _x_ **OR** _y_ | **NOT** _x_ |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| _x_ | _y_ | _x_ **AND** _y_ | _x_ **OR** _y_ | **NOT** _x_ |
| true | true | true | true | false |
| true | false | false | true | false |
| true | null | null | true | false |
| false | true | false | true | true |
| false | false | false | false | true |
| false | null | false | null | true |
| null | true | null | true | null |
| null | false | false | null | null |
| null | null | null | null | null |