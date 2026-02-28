### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/) [边缘脚本](https://help.aliyun.com/zh/cdn/user-guide/edgescript/) [EdgeScript内置函数库](https://help.aliyun.com/zh/cdn/user-guide/edgescript-built-in-functions/) 请求处理相关

# 请求处理相关

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：字典类型相关](https://help.aliyun.com/zh/cdn/user-guide/dictionary-functions)[下一篇：限速相关](https://help.aliyun.com/zh/cdn/user-guide/throttling-functions)

该文章对您有帮助吗？

反馈

本文为您介绍请求处理相关函数的语法、说明、参数、返回值和示例。

## add\_req\_header

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `add_req_header(name, value [, append])`。 |
| 说明 | 添加请求头，即回源请求头。 |
| 参数 | - name：待添加的请求头`name`，字符类型。<br>  <br>- value：待添加的请求头`value`，字符类型。<br>  <br>- append：若请求头已添加，`append`决定是否追加`value`，默认覆盖（即默认不追加），布尔类型。 |
| 返回值 | 默认返回`true`，无效请求头返回`false`。 |
| 示例 | ```plaintext<br>add_req_header('USER-DEFINED-REQ-1', '1')<br>add_req_header('USER-DEFINED-REQ-1', 'x', true)<br>说明：添加2个请求头，分别为<br>USER-DEFINED-REQ-1: 1<br>USER-DEFINED-REQ-1: x<br>``` |

## del\_req\_header

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `del_req_header(name)`。 |
| 说明 | 删除请求头，即回源请求头。 |
| 参数 | name：待删除的请求头`name`，字符类型。 |
| 返回值 | 默认返回`true`，无效请求头返回`false`。 |
| 示例 | ```plaintext<br>add_req_header('USER-DEFINED-REQ-2', '2')<br>del_req_header('USER-DEFINED-REQ-2')<br>USER-DEFINED-REQ-2先添加、后删除，故回源请求头中无USER-DEFINED-REQ-2<br>``` |

## add\_rsp\_header

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `add_rsp_header(name, value [, append])`。 |
| 说明 | 添加响应头。 |
| 参数 | - name：待添加的响应头`name`，字符类型。<br>  <br>- value：待添加的响应头`value`，字符类型。 <br>  <br>  <br>  <br>  `value`可包含如下标记，用于在响应阶段执行动态替换： <br>  <br>  <br>  <br>  - ${x} ：将替换为`ngx.var.x`的值。<br>    <br>  - @{y}：将替换为`响应头y`的值。<br>    <br>- append：若响应头已添加，`append`决定是否追加`value`，默认覆盖，布尔类型。<br>  <br>。 |
| 返回值 | 默认返回`true`，无效响应头返回`false`。 |
| 示例 | ```plaintext<br>add_rsp_header('USER-DEFINED-RSP-1', '1')<br>add_rsp_header('USER-DEFINED-RSP-1', 'x', true)<br>说明：添加2个响应头，分别为<br>USER-DEFINED-RSP-1：1<br>USER-DEFINED-RSP-1：x<br>``` |

## del\_rsp\_header

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `del_rsp_header(name)`。 |
| 说明 | 删除响应头。 |
| 参数 | name：待删除的响应头`name`，字符类型。 |
| 返回值 | 默认返回`true`，无效响应头返回`false`。 |
| 示例 | ```plaintext<br>add_rsp_header('USER-DEFINED-RSP-2', '2')<br>del_rsp_header('USER-DEFINED-RSP-2')<br>USER-DEFINED-RSP-2先添加、后删除，故响应头中无USER-DEFINED-RSP-2<br>``` |

## encode\_args

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `encode_args(d)`。 |
| 说明 | 将字典`d`中的`k/v`，转换为URI编码的k1=v1&k2=v2格式的字符串。 |
| 参数 | d：字典类型。 |
| 返回值 | 返回URI编码格式的字符串。 |
| 示例 | ```plaintext<br>my_args = []<br>set(my_args, 'key1', 'value1')<br>set(my_args, 'key2', 'value2')<br>my_args_str = encode_args(my_args)<br>say(concat('encode_args result: ', my_args_str))<br>```<br>输出：<br>```plaintext<br>encode_args result: key1=value1&key2=value2<br>``` |

## decode\_args

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `decode_args(s)`。 |
| 说明 | 将URI编码的k1=v1&k2=v2格式的字符串，转换为字典类型。 |
| 参数 | s：目标字符串。 |
| 返回值 | 返回转换后的字典对象。 |
| 示例 | ```plaintext<br>my_args = decode_args('key1=value1&key2=value2')<br>def echo_each(k, v, u) {<br>    say(concat(k, '=', v))<br>}<br>foreach(my_args, echo_each, [])<br>```<br>输出：<br>```plaintext<br>key1=value1<br>key2=value2<br>``` |

## rewrite

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `rewrite(url, flag, code)`。 |
| 说明 | 改写操作或重定向操作。 |
| 参数 | - url：目标URL，字符类型。 <br>  <br>  - 当flag=redirect或flag=break时，仅改写URI，则参数URL表示改写后的目标URI。<br>    <br>  - 当flag=enhance\_redirect或flag=enhance\_break时，修改整个URI和参数，参数URL表示改写后的目标URI和参数。<br>- flag：重写模式，字符类型。 <br>  <br>  - redirect ：仅修改URI，不修改参数；默认执行302跳转至URL；如果指定参数`code`，则响应码可自定义为：301、302（默认）、303、307或308。<br>    <br>  - break ：仅修改URI，不修改参数，将URI修改为URL。<br>    <br>  - enhance\_redirect：与`redirect`类似，但是修改整个URI和参数。<br>    <br>  - enhance\_break：与`break`类似，但是修改整个URI和参数。<br>- code：为响应码，数字类型 。 <br>  <br>  当flag=redirect或flag=enhance\_redirect时，可自定义响应码。 |
| 返回值 | - 对于改写操作，默认返回`true`。<br>  <br>- 对于重定向操作，默认不返回。 |
| 示例 | ```plaintext<br>if and($arg_mode, eq($arg_mode, 'rewrite:enhance_break')) {<br>  rewrite('/a/example/examplefile.txt?k=v', 'enhance_break')<br>}<br>说明：回源和缓存的uri+参数，修改为/a/example/examplefile.txt?k=v<br>if and($arg_mode, eq($arg_mode, 'rewrite:enhance_redirect')) {<br>  rewrite('/a/example/examplefile.txt?k=v', 'enhance_redirect')<br>}<br>if and($arg_mode, eq($arg_mode, 'rewrite:enhance_redirect_301')) {<br>  rewrite('/a/example/examplefile.txt?k=v', 'enhance_redirect', 301)<br>}<br>说明：302或301跳转至/a/example/examplefile.txt?k=v<br>if and($arg_mode, eq($arg_mode, 'rewrite:break')) {<br>  rewrite('/a/example/examplefile.txt', 'break')<br>}<br>说明：回源和缓存的uri，修改为/a/example/examplefile.txt，保持原参数不变<br>if and($arg_mode, eq($arg_mode, 'rewrite:redirect')) {<br>  rewrite('/a/example/examplefile.txt', 'redirect')<br>}<br>if and($arg_mode, eq($arg_mode, 'rewrite:redirect_301')) {<br>  rewrite('/a/example/examplefile.txt', 'redirect', 301)<br>}<br>说明：302或301跳转至/a/example/examplefile.txt，保持原参数不变<br>``` |

## say

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `say(arg)`。 |
| 说明 | 输出响应体，并在行尾追加换行符。 |
| 参数 | arg：任意类型。 |
| 返回值 | 无。 |
| 示例 | ```plaintext<br>say('hello')<br>say('hello')<br>输出：<br>hello<br>hello<br>``` |

## print

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `print(arg)`。 |
| 说明 | 输出响应体与`say()`相同，但不会在行尾追加换行符。 |
| 参数 | arg：任意类型。 |
| 返回值 | 无。 |
| 示例 | ```plaintext<br>print('byebye')<br>print('byebye')<br>输出：<br>byebyebyebye<br>``` |

## exit

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `exit(code [, body])`。 |
| 说明 | 以状态码`code`结束当前请求。若有`body`，则为响应体。 |
| 参数 | - code：响应状态码。<br>  <br>- body：响应体。 |
| 返回值 | 无。 |
| 示例 | - 示例1 <br>  <br>  <br>  ```plaintext<br>  if not($arg_key) {<br>      exit(403)<br>  }<br>  说明：如果请求未携带参数key时，403拒绝请求。<br>  <br>  if not($cookie_user) {<br>      exit(403, 'not cookie user')<br>  }<br>  说明：当请求未携带cookie user时，403拒绝请求，响应body为'not cookie user'<br>  <br>  if not(0) {<br>      exit(403)<br>  }<br>  说明：not(0)的结果为false<br>  <br>  if not(false) {<br>      exit(403)<br>  }<br>  说明：not(false)的结果为true<br>  ```<br>  <br>- 示例2 <br>  <br>  <br>  ```plaintext<br>  pcs = capture_re($request_uri,'^/([^/]+)/([^/]+)([^?]+)\?(.*)')<br>  sec1 = get(pcs, 1)<br>  sec2 = get(pcs, 2)<br>  sec3 = get(pcs, 3)<br>  if or(not(sec1), not(sec2), not(sec3)) {<br>     add_rsp_header('X-TENGINE-ERROR', 'auth failed - missing necessary uri set')<br>     exit(403)<br>  }<br>  digest = md5(concat(sec1, sec3))<br>  if ne(digest, sec2) {<br>      add_rsp_header('X-TENGINE-ERROR', 'auth failed - invalid digest')<br>      exit(403)<br>  }<br>  ``` |

## get\_rsp\_header

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `get_rsp_header(str)`。 |
| 说明 | 获取响应头。 |
| 参数 | str：string类型。 |
| 返回值 | 返回string、number、字典和boolean类型。<br>- 头存在：返回对应的值，可以为字典和字符串类型。<br>  <br>- 头不存在：返回false。 |
| 示例 | ```plaintext<br>ct = get_rsp_header('content-type')<br>if ct {<br>    add_rsp_header('origin-content-type', 'is')<br>} else {<br>      add_rsp_header('origin-content-type', 'no')<br>}<br>``` |

## add\_rsp\_cookie

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `add_rsp_cookie(k, v [,properties])`。 |
| 说明 | 设置响应cookie，每次调用均会生成一个新的Set-Cookie响应头。 |
| 参数 | - k：cookie名称。<br>  <br>- v：cookie值。<br>  <br>- properties（可选参数）：cookie属性。详细信息，请参见 [Set-Cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie)。 |
| 返回值 | 成功返回true，失败返回false。 |
| 示例 | ```plaintext<br>add_rsp_cookie('user', 'edgescript')<br>add_rsp_cookie('login_time', tostring(now()), [<br>    'path' = '/'<br>])<br>expires = cookie_time(time())<br>add_rsp_cookie('psid', 'SDF93745HFSDF2934JKHG', [<br>    'path' = '/play',<br>    'domain' = 'foo.com',<br>    'secure' = true,<br>    'httponly' = true,<br>    'expires' = expires,<br>    'max_age' = 100,<br>    'samesite' = 'Strict',<br>    'extension' = 'xxt3s'<br>])<br>```<br>响应：<br>```plaintext<br>Set-Cookie: user=edgescript<br>Set-Cookie: login_time=1582538968.912; Path=/<br>Set-Cookie: psid=SDF93745HFSDF2934JKHG; Expires=Mon, 24-Feb-20 10:09:28 GMT; Max-Age=100; Domain=foo.com; Path=/play; Secure; HttpOnly; SameSite=Strict; xxt3s<br>``` |