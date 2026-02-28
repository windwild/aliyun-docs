### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[边缘脚本](https://help.aliyun.com/zh/cdn/user-guide/edgescript/)[EdgeScript内置函数库](https://help.aliyun.com/zh/cdn/user-guide/edgescript-built-in-functions/)Misc相关

# Misc相关

更新时间：2024-09-13 23:34:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：JSON相关](https://help.aliyun.com/zh/cdn/user-guide/json-functions)[下一篇：数组类型相关](https://help.aliyun.com/zh/cdn/user-guide/array-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

base64\_enc

base64\_dec

url\_escape

url\_unescape

rand

rand\_hit

crc

tonumber

base64\_enc\_safe

base64\_dec\_safe

randomseed

rand\_bytes

uuid

本文为您介绍Misc相关函数的语法、说明、参数、返回值和示例。

## base64\_enc

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `base64_enc(s [, no_padding])`。 |
| 说明 | base64编码。 |
| 参数 | - s：待编码的字符串。<br>  <br>- no\_padding：`true`表示无填充，默认`false`。 |
| 返回值 | base64编码后的字符串。 |
| 示例脚本 | ```javascript<br>if $http_data {<br> encdata = base64_enc($http_data)<br> say(concat('base64_encdata=', encdata))<br>}<br>``` |
| 请求头示例 | header: `"data: hello world"` |
| 示例返回结果 | `base64_encdata=aGVsbG8gd29ybGQ=` |

## base64\_dec

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `base64_dec(s)`。 |
| 说明 | base64解码。 |
| 参数 | s：待解码的字符串。 |
| 返回值 | base64解码后的字符串。 |
| 示例脚本 | ```javascript<br>if $http_data {<br> decdata = base64_dec($http_data)<br> say(concat('base64_decdata=', decdata))<br>}<br>``` |
| 请求头示例 | header: `"data: aGVsbG8gd29ybGQ="` |
| 示例返回结果 | `base64_decdata=hello world` |

## url\_escape

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `url_escape(s)`。 |
| 说明 | URL编码。 |
| 参数 | s：待编码的字符串。 |
| 返回值 | URL编码后的字符串。 |
| 示例 | ```javascript<br>raw = '/abc/123/ dd/file.m3u8'<br>esdata = url_escape(raw)<br>dsdata = url_unescape(esdata)<br>if eq(raw, dsdata) {<br>    say(concat('raw=', raw))<br>    say(concat('esdata=', esdata))<br>}<br>```<br>输出：<br>```<br>raw=/abc/123/ dd/file.m3u8<br>esdata=%2Fabc%2F123%2F%20dd%2Ffile.m3u8<br>``` |

## url\_unescape

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `url_unescape(s)`。 |
| 说明 | URL解码。 |
| 参数 | s：待解码的字符串。 |
| 返回值 | URL解码后的字符串。 |
| 示例 | ```javascript<br>raw = '/abc/123/ dd/file.m3u8'<br>esdata = url_escape(raw)<br>dsdata = url_unescape(esdata)<br>if eq(raw, dsdata) {<br>  say(concat('raw=', raw))<br>  say(concat('dsdata=', dsdata))<br>}<br>```<br>输出：<br>```plaintext<br>raw=/abc/123/ dd/file.m3u8<br>dsdata=/abc/123/ dd/file.m3u8<br>``` |

## rand

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `rand(n1, n2)`。 |
| 说明 | 生成随机数，随机数范围：n1 <= 返回值 <= n2。 |
| 参数 | - n1：随机数下限。<br>  <br>- n2：随机数上限。 |
| 返回值 | 返回生成的随机数。 |
| 示例 | ```plaintext<br>r = rand(1,100)<br>say(concat('r=', r))<br>``` |

## rand\_hit

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `rand_hit(ratio)`。 |
| 说明 | 按指定概率返回真假。 |
| 参数 | ratio：为真概率，有效值范围为\[0-100\]。 |
| 返回值 | 按ratio概率返回`true`。例如：当ratio为100时，返回`true`，当ratio为0时，返回`false`。 |
| 示例 | ```plaintext<br>ratio = rand_hit(80)<br>say(concat('ratio=', ratio))<br>``` |

## crc

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `crc(s)`。 |
| 说明 | 计算crc摘要。 |
| 参数 | s：待计算摘要的字符串。 |
| 返回值 | 返回`s`的crc摘要。 |
| 示例 | ```plaintext<br>crc('hello edgescript')<br>``` |

## tonumber

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `tonumber(s [, base])`。 |
| 说明 | 类型转换，将字符串类型转换为数字类型。 |
| 参数 | - s：待转换的字符串。<br>  <br>- base：可指定待转换目标的进制，可用值：10和16，默认10进制。 |
| 示例 | ```<br>n = tonumber('100')<br>say(concat('tonumber()=', n))<br>```<br>输出：<br>```<br>tonumber()=100<br>``` |

## base64\_enc\_safe

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `base64_enc_safe(str)`。 |
| 说明 | 对输入的字符串进行Base64安全编码。安全编码后输出时，需要将“+”替换成“-”、“/”替换成“\_”，同时去掉编码后的“=”。 |
| 参数 | str：待加密的字符串。 |
| 返回值 | 返回字符串类型 |
| 示例 | ```plaintext<br>add_rsp_header('X-RESPOND-OUTPUT', concat('base64_enc_safe=', base64_enc_safe('hello, dsl')), true)<br>```<br>输出响应头：<br>```plaintext<br>X-RESPOND-OUTPUT：base64_enc_safe=aGVsbG8sIGRzbA<br>``` |

## base64\_dec\_safe

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `base64_dec_safe(str)`。 |
| 说明 | 对输入的字符串进行Base64安全解码。安全解码后输出时，需要将“-”替换成“+”、“\_”替换成“/”，末尾用“=”按照4的余数补齐。 |
| 参数 | str：Base64加密后的内容。 |
| 返回值 | 返回字符串类型。 |
| 示例 | ```plaintext<br>add_rsp_header('X-RESPOND-OUTPUT', concat('base64_dec_safe=', base64_dec_safe(base64_enc_safe('hello, dsl'))), true)<br>```<br>输出响应头：<br>```plaintext<br>X-RESPOND-OUTPUT:base64_dec_safe=hello, dsl<br>``` |

## randomseed

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `randomseed()`。 |
| 说明 | 指定生成随机数种子。 |
| 参数 | 无。 |
| 返回值 | 无。 |
| 示例 | ```plaintext<br>randomseed()<br>r = rand(1,100)<br>say(concat('r=', r))<br>``` |

## rand\_bytes

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `rand_bytes(len)`。 |
| 说明 | 生成随机数字符串。 |
| 参数 | len：指定生成的随机数字符串的长度。 |
| 返回值 | 返回生成的随机数字符串。 |
| 示例 | ```plaintext<br>rand_bytes(16)<br>``` |

## uuid

函数详细信息，请参见下表：

| **项目** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `uuid()`。 |
| 说明 | 返回uuid格式的字符串。 |
| 参数 | 无。 |
| 返回值 | 返回uuid，示例：16903a86-4173-4dea-842c-926c5860fe05。 |
| 示例 | ```plaintext<br>uuid = uuid()<br>say(concat('uuid=', uuid))<br>```<br>输出：<br>```<br>uuid=54853c52-4c57-47dc-9b73-fb95d30b3d75<br>``` |