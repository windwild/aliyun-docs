### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/) [边缘脚本](https://help.aliyun.com/zh/cdn/user-guide/edgescript/) [EdgeScript内置函数库](https://help.aliyun.com/zh/cdn/user-guide/edgescript-built-in-functions/) 时间相关

# 时间相关

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：缓存相关](https://help.aliyun.com/zh/cdn/user-guide/cache-functions)[下一篇：密码算法相关](https://help.aliyun.com/zh/cdn/user-guide/cipher-algorithm-functions)

该文章对您有帮助吗？

反馈

本文为您介绍时间相关函数的语法、说明、参数、返回值和示例。

## today

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `today()`。 |
| 说明 | 返回当前时间（本地时间）字符串，格式：yyyy-mm-dd。 |
| 参数 | 无。 |
| 返回值 | 返回当前时间字符串，格式：yyyy-mm-dd。 |
| 示例 | ```plaintext<br>say(concat('today:', today()))<br>```<br>输出：<br>```plaintext<br>today:2019-05-23<br>``` |

## time

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `time()`。 |
| 说明 | 返回当前的UNIX时间戳（不包含毫秒的小数部分），单位：秒。<br>**说明** <br>UNIX时间戳不区分时区，表示的是从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。 |
| 参数 | 无。 |
| 返回值 | 返回当前的UNIX时间戳。 |
| 示例 | ```plaintext<br>say(concat('time:', time()))<br>```<br>输出：<br>```plaintext<br>time:1559109666<br>``` |

## now

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `now()`。 |
| 说明 | 返回当前的UNIX时间戳（数值类型，包含毫秒的小数部分），单位：秒。<br>**说明** <br>UNIX时间戳不区分时区，表示的是从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。 |
| 参数 | 无。 |
| 返回值 | 返回当前的UNIX时间戳（数值类型，包含毫秒的小数部分），单位：秒。 |
| 示例 | ```plaintext<br>say(concat('now:', now()))<br>```<br>输出：<br>```plaintext<br>now:1559109666.644<br>``` |

## localtime

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `localtime()`。 |
| 说明 | 返回当前时间（本地时间）字符串，格式：yyyy-mm-dd hh:mm:ss。 |
| 参数 | 无。 |
| 返回值 | 返回当前时间字符串，格式：yyyy-mm-dd hh:mm:ss。 |
| 示例 | ```plaintext<br>say(concat('localtime:', localtime()))<br>```<br>输出：<br>```plaintext<br>localtime:2019-05-29 14:02:41<br>``` |

## utctime

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `utctime()`。 |
| 说明 | 返回当前时间字符串（UTC时间），格式：yyyy-mm-dd hh:mm:ss。 |
| 参数 | 无。 |
| 返回值 | 返回当前时间字符串，格式：yyyy-mm-dd hh:mm:ss。 |
| 示例 | ```plaintext<br>say(concat('utctime:', utctime()))<br>```<br>输出：<br>```plaintext<br>utctime:2019-05-29 06:02:41<br>``` |

## cookie\_time

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `cookie_time(sec)`。 |
| 说明 | 生成cookie格式的GMT时间字符串。 |
| 参数 | sec：UNIX时间戳。例如：调用`time()`获取。 |
| 返回值 | 基于`sec`表示的UNIX时间戳，返回cookie格式的时间字符串。 |
| 示例 | ```plaintext<br>say(concat('cookie_time:', cookie_time(time())))<br>```<br>输出：<br>```plaintext<br>cookie_time:Wed, 29-May-19 06:02:41 GMT<br>``` |

## http\_time

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `http_time(sec)`。 |
| 说明 | 生成HTTP header格式的时间字符串。例如：Last-Modified。<br>**重要** <br>该函数只能生成GMT标准的时间。 |
| 参数 | sec：UNIX时间戳。例如：调用`time()`获取。 |
| 返回值 | 基于`sec`表示的UNIX时间戳，返回HTTP header格式的时间字符串，用于HTTP头的时间。 |
| 示例 | ```plaintext<br>say(concat('http_time:', http_time(time())))<br>```<br>输出<br>```plaintext<br>http_time:Wed, 29 May 2019 06:02:41 GMT<br>``` |

## parse\_http\_time

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `parse_http_time(str)`。 |
| 说明 | 解析HTTP header格式的时间字符串，并返回对应的UNIX时间戳。<br>**重要** <br>该函数不识别时区，因此需要把本地时间先转换为GMT标准的时间以后再传递给该函数。 |
| 参数 | str：待转换的HTTP header格式的时间字符串。格式：`Wed, 29 May 2019 06:02:41 GMT`。调用`http_time()`获取。 |
| 返回值 | 成功返回UNIX时间戳，失败返回`false`。 |
| 示例 | ```plaintext<br>say(concat('parse_http_time:', parse_http_time(http_time(time()))))<br>```<br>输出<br>```plaintext<br>parse_http_time:1559109761<br>``` |

## unixtime

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `unixtime(year, month, day, hour, min, sec)`。 |
| 说明 | 根据本地时间的年、月、日、时、分、秒，生成UNIX时间戳并返回。<br>**说明** <br>UNIX时间戳不区分时区，表示的是从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数。 |
| 参数 | - year：指定年。<br>  <br>- month：指定月。<br>  <br>- day：指定日。<br>  <br>- hour：指定小时。<br>  <br>- min：指定分钟。<br>  <br>- sec：指定秒。 |
| 返回值 | 返回转换后的UNIX时间戳。 |
| 示例 | - 示例一：<br>  <br>  <br>  ```plaintext<br>  t = unixtime(1970, 1, 1, 8, 0, 0)<br>  say(concat('unixtime()=', t))<br>  ```<br>  <br>  <br>  输出<br>  <br>  <br>  ```plaintext<br>  unixtime()=0<br>  ```<br>  <br>- 示例二：<br>  <br>  <br>  ```plaintext<br>  t = unixtime(2021,12,23,0,0,0)<br>  say(concat('unixtime()=', t))<br>  ```<br>  <br>  <br>  输出<br>  <br>  <br>  ```plaintext<br>  unixtime()=1640188800<br>  ``` |