### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[访问控制](https://help.aliyun.com/zh/cdn/user-guide/access-control/)[其他安全访问控制](https://help.aliyun.com/zh/cdn/user-guide/other-security-access-control/)[URL鉴权配置](https://help.aliyun.com/zh/cdn/user-guide/url-signing/)鉴权方式A说明

# 鉴权方式A说明

更新时间：2026-02-03 01:17:24

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置URL鉴权](https://help.aliyun.com/zh/cdn/user-guide/configure-url-signing)[下一篇：鉴权方式B说明](https://help.aliyun.com/zh/cdn/user-guide/type-b-signing)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

原理说明

鉴权URL示例

URL鉴权功能主要用于保护用户站点资源不被非法站点下载盗用。本文介绍阿里云CDN提供的鉴权方式A的原理和示例说明。

## 原理说明

- **鉴权方式A加密URL构成**

















```xml
http://DomainName/Filename?auth_key={<timestamp>-rand-uid-<md5hash>}
```







**说明**





`{}`中的内容表示在标准URL基础上添加的加密信息。

- **鉴权字段说明**




| **字段** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **字段** | **描述** |
| DomainName | CDN站点的域名。 |
| Filename | 实际回源访问的URL，鉴权时Filename需以正斜线（`/`）开头。 |
| auth\_key | 本次请求的鉴权信息，由timestamp、rand、uid和md5hash组成。 |
| timestamp | 签算服务器生成鉴权URL的时间，与 **鉴权URL有效时长** 共同控制鉴权URL的失效时间。时间点取自签算服务器的Unix时间戳（从1970年01月01日00时00分00秒到现在的总秒数，固定长度为10）。<br>**说明**<br>多数情况下，鉴权URL的有效时长为CDN配置有效时长。有时在签算增加鉴权URL的有效时长的，此时，timestamp=Unix时间戳+增加的时长；鉴权URL实际有效时长=timestamp+CDN配置的时长。 |
| rand | 随机数。建议使用UUID，不能包含中划线（-），例如：477b3bbc253f467b8def6711128c7bec。 |
| uid | 用户ID，暂未使用，设置成0即可。 |
| md5hash | 通过MD5算法计算出的32位字符串，由数字和小写字母组成。<br>计算方法：<br>```python<br>sstring = "URI-Timestamp-rand-uid-PrivateKey"（URI是用户的请求对象相对地址，不包含参数，如/Filename）<br>md5hash = md5sum(sstring)<br>``` |

- **鉴权逻辑说明**



CDN服务器接到资源访问请求后，判断`timestamp`+`鉴权URL有效时长`是否小于当前时间。



  - 如果`timestamp`+`鉴权URL有效时长`小于当前时间，服务器判定过期失效，并返回HTTP 403错误。

  - 如果`timestamp`+`鉴权URL有效时长`大于当前时间，则以`sstring`方式构造出一个字符串（参考表格中`sstring`构造方式），然后使用MD5算法算出`md5hash`的值，再将计算出的`md5hash`值与用户访问请求中携带的`md5hash`的值进行比对。

    - 结果一致，鉴权通过，返回资源请求。



      **说明**





      当鉴权通过时，会去掉URL中与鉴权相关的部分参数，还原为原始URL，这样可以提高缓存命中率，减少回源流量。例如：



      - 带鉴权参数的URL格式：`http://DomainName/Filename?auth_key={<timestamp>-rand-uid-<md5hash>}`

      - 鉴权通过后：

        - 实际生成缓存key的URL格式：`http://DomainName/FileName`

        - 实际回源的URL格式：`http://DomainName/FileName`

    - 结果不一致，鉴权失败，返回HTTP 403错误。

## 鉴权URL示例

以下示例说明鉴权方式A的实现。

- **示例条件**

  - 回源请求对象：















    ```http
    http://domain.example.com/video/standard/test.mp4
    ```





    **说明**





    如果请求URL中包含中文（或其他非 ASCII 字符），必须先进行 **编码（encode）**，然后再使用编码后的URL进行待哈希字符串的拼接。例如：



    - 原始URL：`https://example.com/image/阿里云.jpg`

    - 编码后的URL：`https://example.com/image/%E9%98%BF%E9%87%8C%E4%BA%91.jpg`


  - 设置密钥为：aliyuncdnexp1234。

  - 签算服务器生成鉴权URL的时间：2015年10月10日08:00:00（UTC+8），转换为十进制的整型数值为1444435200。
- **拼接流程**

1. CDN服务器构造出一个用于计算`md5hash`的待哈希字符串。















     ```json
     /video/standard/test.mp4-1444435200-0-0-aliyuncdnexp1234
     ```

2. 根据该待哈希字符串，CDN服务器计算出`md5hash`。















     ```json
     md5hash = md5sum("/video/standard/test.mp4-1444435200-0-0-aliyuncdnexp1234") = 23bf85053008f5c0e791667a313e28ce
     ```

3. 生成鉴权URL。















     ```xml
     http://domain.example.com/video/standard/test.mp4?auth_key=1444435200-0-0-23bf85053008f5c0e791667a313e28ce
     ```

当使用客户端提供的加密URL进行访问时，如果CDN服务器计算出来的`md5hash`值与访问请求中带的`md5hash`值相同，都为_23bf85053008f5c0e791667a313e28ce_，并且鉴权URL在有效期内，则鉴权通过，反之鉴权失败。