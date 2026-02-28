### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/) [边缘脚本](https://help.aliyun.com/zh/cdn/user-guide/edgescript/) [EdgeScript内置函数库](https://help.aliyun.com/zh/cdn/user-guide/edgescript-built-in-functions/) Debug相关

# Debug相关

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：请求判断相关](https://help.aliyun.com/zh/cdn/user-guide/request-logic-functions)[下一篇：附录：地区和运营商编码](https://help.aliyun.com/zh/cdn/user-guide/appendix)

该文章对您有帮助吗？

反馈

本文为您介绍Debug相关函数的语法、参数、示例和返回值。

## type

函数详细信息，请参见下表：

|     |     |
| --- | --- |
| **项目** | **描述** |
| 语法 | `type(s)` |
| 说明 | 测试s变量的类型。 |
| 参数 | 仅接受1个参数。 |
| 返回值 | 返回s变量的类型。 |
| 示例 | ```json<br>m = type('100')<br>n = type(100)<br>t = type(['a', 'b'])<br>say(concat('type(m)=', m))<br>say(concat('type(n)=', n))<br>say(concat('type(t)=', t))<br>输出：<br>type(m)=string<br>type(n)=number<br>type(t)=table<br>```<br>**说明** <br>type的返回值为字符串类型。 |