### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) Apache缓存策略的设置

# Apache缓存策略的设置

更新时间：2021-09-24 06:09:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

> **免责声明：** 本文档可能包含第三方产品信息，该信息仅供参考。阿里云对第三方产品的性能、可靠性以及操作可能带来的潜在影响，不做任何暗示或其他形式的承诺。

## 概述

本文主要介绍如何通过Apache的mod\_expires和mod\_headers模块设置Apache缓存策略。

## 详细信息

### mod\_expires模块设置

Apache可以通过配置文件的mod\_expires模块控制HTTP协议的Expires和Cache-Control头部信息。mod\_expires模块的主要作用是自动生成页面头部信息中的Expires标签和Cache-Control标签，从而降低客户端的访问频率和次数，达到减少不必要流量和增加访问速度的目的。

#### mod\_expires模块的介绍

mod\_expires是Apache众多模块中配置比较简单的模块，一共有以下三条指令。

- ExpiresActive指令：打开或关闭产生Expires和Cache-Control标签的功能。
- ExpiresByType指令：指定MIME类型文档的过期时间，例如text/html文档。
- ExpiresDefault指令：所有文档的默认过期时间。

过期时间的写法如下。

- access plus 1 month
- access plus 4 weeks
- now plus 30 days
- modification plus 5 hours 3 minutes
- A2592000
- M604800

> 提示：
>
> - access plus 1 month、access plus 4 weeks、now plus 30 days和A2592000写法的意义相同，指过期时间是从访问时开始计算。
> - modification plus 5 hours 3 minutes和M604800意义相同，指过期时间是以被访问文件的最后修改时间开始计算。
> - M604800只对静态文件起作用，脚本生成的动态页面不起作用。

#### 配置示例

1. mod\_expires模块的配置如下所示。
   - ExpiresActive On：开启mod\_expires功能。
   - ExpiresDefault "access plus 6 months"：默认的过期时间是6个月。
   - ExpiresByType image/\* "access plus 10 years"：图片的文件类型缓存时间为10年。
   - ExpiresByType text/\* "access plus 10 years"：文本类型缓存时间为10年。
   - ExpiresByType application/\* "access plus 30 minutes"：application文件类型缓存30分钟。
2. 访问image/jpeg类型的缓存时间为315360000秒，即10年，如下所示。

![缓存时间验证](http://help-static-aliyun-doc.aliyuncs.com/assets/img/4384870751/p3988.png)
3. 如果将image/jpeg类型设置为不缓存，即将max-age设置为0秒，配置如下所示。
















```
#ExpiresByType image/* "access plus 10 years"
ExpiresByType image/* A0
```

4. 再次访问时，发现缓存时间为0秒。

![max-age](http://help-static-aliyun-doc.aliyuncs.com/assets/img/4384870751/p3989.png)

### mod\_headers模块设置

mod\_headers模块配置示例如下所示，详细介绍请参考 [Apache官方网站](https://httpd.apache.org/docs/current/mod/mod_headers.html)。

```
# YEAR
Header set Cache-Control "max-age=2592000″

# WEEK
Header set Cache-Control "max-age=604800″

# NEVER CACHE
Header set Expires "Thu, 01 Dec 2003 16:00:00 GMT"
Header set Cache-Control "no-store, no-cache, must-revalidate"
Header set Pragma "no-cache"
```

## 适用于

- CDN

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

详细信息

mod\_expires模块设置

mod\_headers模块设置

适用于