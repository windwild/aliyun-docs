### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[访问控制](https://help.aliyun.com/zh/cdn/user-guide/access-control/)[其他安全访问控制](https://help.aliyun.com/zh/cdn/user-guide/other-security-access-control/)[URL鉴权配置](https://help.aliyun.com/zh/cdn/user-guide/url-signing/)鉴权方式F说明

# 鉴权方式F说明

更新时间：2026-02-03 01:20:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：鉴权方式C说明](https://help.aliyun.com/zh/cdn/user-guide/type-c-signing)[下一篇：鉴权代码示例](https://help.aliyun.com/zh/cdn/user-guide/url-signing-examples)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

原理说明

鉴权URL示例

URL鉴权功能主要用于保护用户站点资源不被非法站点下载或盗用。阿里云CDN为您提供了四种鉴权方式，本文为您详细介绍鉴权方式F的原理和示例说明。

## 原理说明

- **鉴权方式F加密URL构成**



访问URL格式：

















```xml
http://DomainName/FileName?{sign=<md5hash>&time=<timestamp>}
```







**说明**





  - `{}`中的内容表示在标准URL基础上添加的加密信息。

  - 访问URL中不能包含中文。

  - 不支持包含`?`带参数的URL鉴权。


- **鉴权字段说明**




| **字段** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **字段** | **描述** |
| DomainName | CDN站点的域名。 |
| PrivateKey | 用户自定义鉴权key，由16~32个字符（支持大写字母、小写字母、数字）组成。 |
| FileName | 实际回源访问的URL，鉴权时Filename需以`/`开头。 |
| timestamp | 签算服务器生成鉴权URL的时间，与 **鉴权URL有效时长** 共同控制鉴权URL的失效时间。时间点取自签算服务器的Unix时间戳（Unix时间戳是从UTC时间1970年01月01日00时00分00秒到现在的总秒数，是十进制的整型正数，固定长度为10，与时区无关），以十六进制形式表示。<br>**说明**<br>多数情况下，鉴权URL的有效时长为CDN配置有效时长。有时在签算增加鉴权URL的有效时长的，此时，timestamp=Unix时间戳+增加的时长；鉴权URL实际有效时长=timestamp+CDN配置的时长。 |
| md5hash | 通过MD5算法计算出的字符串，由数字0~9和小写英文字母a~z混合组成，固定长度32。<br>`md5hash`的值通过以下字符串计算得到。<br>```json<br>sstring = "Privatekey+URI+timestamp" (URI是用户的请求对象相对地址，不包含参数，如/Filename)<br>md5hash = md5sum(sstring)<br>``` |

- **鉴权逻辑说明**

CDN服务器接到资源访问请求后，判断`timestamp`+`鉴权URL有效时长`是否小于当前时间。

  - 如果`timestamp`+`鉴权URL有效时长`小于当前时间，服务器判定过期失效，并返回HTTP 403错误。

  - 如果`timestamp`+`鉴权URL有效时长`大于当前时间，则以`sstring`方式构造出一个字符串（参考表格中`sstring`构造方式），然后使用MD5算法算出`md5hash`的值，再将计算出的`md5hash`值与用户访问请求中携带的`md5hash`的值进行比对。

    - 结果一致，鉴权通过，返回资源请求。



      **说明**





      当鉴权通过时，会去掉URL中与鉴权相关的部分参数，还原为原始URL，这样可以提高缓存命中率，减少回源流量。例如：



      - 带鉴权参数的URL格式：`http://DomainName/FileName?{sign=<md5hash>&time=<timestamp>}`

      - 鉴权通过后：

        - 实际生成缓存key的URL格式：`http://DomainName/FileName`

        - 实际回源的URL格式：`http://DomainName/FileName`

    - 结果不一致，鉴权失败，返回HTTP 403错误。

## 鉴权URL示例

通过以下示例说明，您可以准确理解鉴权方式F的实现方式。

- **示例条件**

  - 回源请求对象：















    ```http
    http://domain.example.com/test.flv
    ```





    **说明**





    如果请求URL中包含中文（或其他非 ASCII 字符），必须先进行 **编码（encode）**，然后再使用编码后的URL进行待哈希字符串的拼接。例如：



    - 原始URL：`https://example.com/image/阿里云.jpg`

    - 编码后的URL：`https://example.com/image/%E9%98%BF%E9%87%8C%E4%BA%91.jpg`


  - PrivateKey取值：`aliyuncdnexp1234`。

  - timestamp取值：`55CE8100`。

- **拼接流程**

1. CDN服务器构造一个用于计算`md5hash`的待哈希字符串。















     ```json
     aliyuncdnexp1234/test.flv55CE8100
     ```

2. 根据该待哈希字符串，CDN服务器会计算出`md5hash`。















     ```json
     md5hash = md5sum(aliyuncdnexp1234/test.flv55CE8100) = a37fa50a5fb8f71214b1e7c95ec7a1bd
     ```

3. 生成鉴权URL。

     鉴权URL格式：















     ```plaintext
     http://domain.example.com/test.flv?sign=a37fa50a5fb8f71214b1e7c95ec7a1bd&time=55CE8100
     ```

当使用客户端提供的加密URL进行访问时，如果CDN服务器计算出来的`md5hash`值与访问请求中带的`md5hash`值相同，都为_a37fa50a5fb8f71214b1e7c95ec7a1bd_，并且鉴权URL在有效期内，则鉴权通过，反之鉴权失败。