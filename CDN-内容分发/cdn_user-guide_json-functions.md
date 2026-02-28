### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/) [边缘脚本](https://help.aliyun.com/zh/cdn/user-guide/edgescript/) [EdgeScript内置函数库](https://help.aliyun.com/zh/cdn/user-guide/edgescript-built-in-functions/) JSON相关

# JSON相关

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：密码算法相关](https://help.aliyun.com/zh/cdn/user-guide/cipher-algorithm-functions)[下一篇：Misc相关](https://help.aliyun.com/zh/cdn/user-guide/miscellaneous-functions)

该文章对您有帮助吗？

反馈

本文为您介绍JSON相关函数的语法、说明、参数、返回值和示例。

## json\_enc

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `json_enc(d)` |
| 说明 | JSON编码。 |
| 参数 | d：待编码的字典对象。 |
| 返回值 | 成功返回编码后的字符串，失败返回`false`。 |
| 示例 | ```javascript<br>var_a = []<br>var_b = ['v1', 'v2']<br>set(var_a, 'k1', 'v1')<br>set(var_a, 'k2', var_b)<br>var_c = '{"k1":"v1","k2":["v1","v2"]}'<br>say(concat('json_enc=', json_enc(var_a)))<br>say(concat('json_dec=', get(json_dec(var_c), 'k1')))<br>输出：<br>json_enc={"k1":"v1","k2":["v1","v2"]}<br>json_dec=v1<br>``` |

## json\_dec

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `json_dec(s)` |
| 说明 | JSON解码。 |
| 参数 | s：待解码的JSON格式字符串。 |
| 返回值 | 成功返回解码后的字典，失败返回`false`。<br>**说明**<br>"123"这样的纯数字字符串也可以被成功解码为一个number类型的变量，如果后续对返回的字典有关联操作（比如get某个值），请配合使用 [type](https://help.aliyun.com/zh/cdn/user-guide/debug-functions#f6667f7388pro "") 函数进行变量类型的判断。 |
| 示例 | ```javascript<br>var_c = '123'<br>type_var_c = type(json_dec(var_c))<br>if eq(type_var_c, 'table') {<br>  say(concat('json_dec=', get(json_dec(var_c), 'k1')))<br>} else {<br>  say(type_var_c)<br>}<br>var_c = '{"k1":"v1","k2":["v1","v2"]}'<br>type_var_c = type(json_dec(var_c))<br>if eq(type_var_c, 'table') {<br>  say(concat('json_dec=', get(json_dec(var_c), 'k1')))<br>} else {<br>  say(type_var_c)<br>}<br>输出：<br>number<br>json_dec=v1<br>``` |