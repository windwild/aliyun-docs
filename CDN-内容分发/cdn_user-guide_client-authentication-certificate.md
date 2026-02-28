### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/) [HTTPS配置](https://help.aliyun.com/zh/cdn/user-guide/https-for-cdn-or-dcdn/) 客户端认证证书

# 客户端认证证书

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置HSTS](https://help.aliyun.com/zh/cdn/user-guide/configure-hsts)[下一篇：相关参考](https://help.aliyun.com/zh/cdn/user-guide/cdn-https-references/)

该文章对您有帮助吗？

反馈

默认情况，HTTPS证书仅支持客户端单向验证服务器的安全性。阿里云CDN支持客户端证书认证，通过自定义的CA证书实现服务器对客户端进行身份验证，从而实现双向认证，加强网站通信的安全性。本文为您介绍如何开启和配置客户端证书认证。

## 前提条件

- 您已开启并配置HTTPS证书功能，请参见 [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate "")。

- 您已经自行签发一份 **客户端CA证书**。


## 操作步骤

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **HTTPS配置**。

5. 打开 **客户端证书认证** 并输入自行签发的 **客户端CA证书**。



![开关](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9687937571/p378242.png)



输入自行签发的私有证书（公钥）。CA证书的格式有以下要求：



   - 以“-----BEGIN CERTIFICATE-----”开头，以“-----END CERTIFICATE-----”结尾。

   - 每行64个字符，最后一行可以不足64个字符。


![开启](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7157380461/p374208.png)

6. 单击 **确定**。



开启 **客户端证书认证** 后，客户端以HTTPS请求访问资源时，阿里云CDN会验证客户端证书有效性，验证成功，通过请求；验证失败，则拒绝访问。