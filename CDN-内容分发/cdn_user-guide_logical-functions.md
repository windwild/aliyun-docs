### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[边缘脚本](https://help.aliyun.com/zh/cdn/user-guide/edgescript/)[EdgeScript内置函数库](https://help.aliyun.com/zh/cdn/user-guide/edgescript-built-in-functions/)条件判断相关

# 条件判断相关

更新时间：2025-01-06 04:05:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：内置函数概述](https://help.aliyun.com/zh/cdn/user-guide/tag-overview)[下一篇：数字类型相关](https://help.aliyun.com/zh/cdn/user-guide/numeric-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

and

or

not

eq

ne

null

本文为您介绍条件判断相关函数的语法、说明、参数、返回值和示例。

## and

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `and(arg, ...)`。 |
| 说明 | - 逻辑与运算符。<br>  <br>- 支持短路语义，即某个参数为假时，后续参数不再进行求值。 |
| 参数 | 一个或多个参数，参数类型不限。 |
| 返回值 | 全部参数为真时返回`true`，任一参数为假时返回`false`。 |
| 示例 | ```java<br>if and($arg_mode, eq($arg_mode, 'set_header')) {<br>   add_rsp_header('USER-DEFINED-1','path1')<br>}<br>```<br>- 当请求携带mode参数且mode参数等于set\_header时，设置响应头USER-DEFINED-1。<br>  <br>- 当请求不携带mode参数，短路语义生效，不再执行后续的eq比较；由于and()为假，不会设置响应头USER-DEFINED-1。 |

## or

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `or(arg, ...)`。 |
| 说明 | - 逻辑或运算符。<br>  <br>- 支持短路语义，即某个参数为真时，后续参数不再进行求值。 |
| 参数 | 一个或多个参数，参数类型不限。 |
| 返回值 | 任一参数为真时返回`true`，全部参数为假时返回`false`。 |
| 示例 | ```java<br>if and($http_from, or(eq($http_from, 'wap'), eq($http_from, 'comos'))) {<br>    rewrite(concat('http://example.com.cn/zt_d/we2015/', $http_from), 'enhance_redirect')<br>}<br>```<br>- 当请求头from存在，且其值为\[wap\|comos\]时，302重定向至http://example.com.cn/zt\_d/we2015/\[wap\|comos\]。<br>  <br>- 当请求头from存在，且其值为wap时，短路语义生效，不再执行后续eq和comos比较，同时or()返回true。 |

## not

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `not(arg)`。 |
| 说明 | 逻辑运算符取反。参数`undef`和`false`为假，其余为真。 |
| 参数 | 仅接受1个参数，参数类型不限。 |
| 返回值 | - true<br>  <br>- false |
| 示例 | ```java<br>if not($arg_key) {<br>    exit(403)<br>}<br>if not($cookie_user) {<br>    exit(403, 'not cookie user')<br>}<br>if not(0) {<br>    exit(403)<br>}<br>if not(false) {<br>    exit(403)<br>}<br>```<br>- 如果请求未携带参数key时，403拒绝请求。<br>  <br>- 当请求未携带`cookie user`时，403拒绝请求，响应body为`'not cookie user'`。<br>  <br>- `not(0)`的结果为false。<br>  <br>- `not(false)`的结果为true。 |

## eq

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `eq(arg1, arg2)`。 |
| 说明 | 比较2个参数是否相等。 |
| 参数 | - arg1：任意类型。<br>  <br>- arg2：应与`arg1`类型相同。 |
| 返回值 | 参数相等返回`true`，否则返回`false`。 |
| 示例 | ```java<br>key1 = 'value1'<br>if eq(key1, $arg_k1) {<br>    say('match condition')<br>}<br>```<br>- eq: 请求参数k1的值是否等于value1。<br>  <br>- 当请求参数k1等于value1，输出响应体match condition。 |

## ne

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `ne(arg1, arg2)`。 |
| 说明 | 比较2个参数是否不等。 |
| 参数 | - arg1：任意类型。<br>  <br>- arg2：应与`arg1`类型相同。 |
| 返回值 | 参数不等返回`true`，否则返回`false`。 |
| 示例 | ```java<br>key2 = 'value2'<br>if ne(key2, $arg_k2) {<br>    say('match condition')<br>}<br>```<br>- ne: 请求参数k2的值不等于value2。<br>  <br>- 当请求参数k2不等于value2时，输出响应体match condition。 |

## null

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `null(v)`。 |
| 说明 | 判断ES数据类型是否为空。 |
| 参数 | v：需要传入的参数，类型为数组、字典和字符串，其他类型均返回false。 |
| 返回值 | 返回值为bool类型<br>- v是数组和字典，如果为空，返回true。<br>  <br>- v是字符串，如果值为空串，返回true。<br>  <br>- 其他情况均返回false。 |
| 示例 | ```plaintext<br>d = []<br>say(null(d))<br>set(d, 1, 'v1')<br>say(null(d))<br>say(tostring(null('x')))<br>say(tostring(null('')))<br>```<br>输出：<br>```plaintext<br>true<br>false<br>false<br>true<br>``` |