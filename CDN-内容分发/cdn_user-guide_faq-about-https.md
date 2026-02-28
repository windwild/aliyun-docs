### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[HTTPS配置](https://help.aliyun.com/zh/cdn/user-guide/https-for-cdn-or-dcdn/)HTTPS相关常见问题

# HTTPS相关常见问题

更新时间：2025-12-11 21:35:39

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：什么是HTTPS加速](https://help.aliyun.com/zh/cdn/user-guide/what-is-https-secure-acceleration)[下一篇：性能优化概述](https://help.aliyun.com/zh/cdn/user-guide/performance-optimization-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

什么是HTTPS？

常见的HTTP攻击类型有哪些？

站点只有登录才需要HTTPS吗？

配置HTTPS时，需要配置哪些证书？

开启CDN的HTTPS加速后会额外收费吗？

IP黑白名单、User-Agent 黑名单、请求返回403/404时，HTTPS请求数是否会被计费？

源站已经配置了HTTPS，CDN上还需要配置HTTPS吗？

开启HTTPS加速会消耗更多资源或降低访问速度吗？

如何配置HTTPS证书？

上传HTTPS证书，提示证书重复怎么办？

上传第三方证书时，有多个.crt证书，如何上传证书？

配置HTTPS证书时提示“证书格式不对”，如何进行转换？

源站的HTTPS证书更新了，CDN上需要同步更新吗？

配置HSTS时，打开包含子域名后，子域名上是否需要打开HSTS？

已经配置了HTTPS，为什么客户端还是HTTP访问？

为什么大多数设备能够顺利访问通过HTTPS协议加速的域名，但是一些设备却无法访问？

私钥文件如何去除密码保护？

HTTPS是以安全为目标的HTTP通道，为CDN的网络内容传输提供了更好的保障。客户端在极速访问内容的同时，可以更安全有效地浏览网站内容。本文为您介绍关于HTTPS的常见问题。

- [什么是HTTPS？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-zwj-78b-5v6 "")

- [常见的HTTP攻击类型有哪些？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-hfq-h5z-zgb "")

- [站点只有登录才需要HTTPS吗？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-epq-ztz-zgb "")

- [配置HTTPS时，需要配置哪些证书？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#1c411a2e68zvd "")

- [开启CDN的HTTPS加速后会额外收费吗？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-fnh-ptz-zgb "")

- [IP黑白名单、User-Agent 黑名单、请求返回403/404时，HTTPS请求数是否会被计费？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-l9d-h50-2vu "")

- [源站已经配置了HTTPS，CDN上还需要配置HTTPS吗？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-lq1-dyp-bea "")

- [开启HTTPS加速会消耗更多资源或降低访问速度吗？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-hlw-5tz-zgb "")

- [如何配置HTTPS证书？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-8zr-wp5-tzq "")

- [上传HTTPS证书，提示证书重复怎么办？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-37t-zop-u9j "")

- [上传第三方证书时，有多个.crt证书，如何上传证书？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#6d77cf3649q8s "")

- [配置HTTPS证书时提示“证书格式不对”，如何进行转换？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-nn1-mcd-0e7 "")

- [源站的HTTPS证书更新了，CDN上需要同步更新吗？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-zjb-jyq-cc4 "")

- [配置HSTS时，打开包含子域名后，子域名上是否需要打开HSTS？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#8db5405546mux "")

- [已经配置了HTTPS，为什么客户端还是HTTP访问？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-cst-8gc-503 "")

- [为什么大多数设备能够顺利访问通过HTTPS协议加速的域名，但是一些设备却无法访问？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#612fb5afb31yo "")

- [私钥文件如何去除密码保护？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#9b577a1c3bw7a "")


## 什么是HTTPS？

超文本传输安全协议HTTPS（Hypertext Transfer Protocol Secure），是一种在HTTP协议基础上进行传输加密的安全协议，能够有效保障数据传输的安全。HTTP协议以明文方式发送内容，不提供任何方式的数据加密。HTTPS协议是以安全为目标的HTTP通道，简单来说，HTTPS是HTTP的安全版，即将HTTP用SSL或TLS协议进行封装，HTTPS的安全基础是SSL或TLS协议。HTTPS提供了身份验证与加密通讯方法，被广泛用于万维网上安全敏感的通讯，例如交易支付。当您在阿里云CDN上配置HTTPS时，需要提供域名对应的证书，并将证书部署在全网CDN节点，实现全网数据加密传输。

## 常见的HTTP攻击类型有哪些？

HTTPS只是安全访问的其中一环，如需全面保证网络安全，则还需要接入WAF、DDoS等防御能力，以下为常见的HTTP攻击类型：

- SQL注入：利用现有应用程序，可以将恶意的SQL命令注入到后台数据库引擎中并执行。也可以通过在Web表单中输入恶意SQL语句得到一个存在安全漏洞的网站上的数据库，而不是按照设计者意图去执行SQL语句。

- 跨站脚本攻击：跨站脚本攻击XSS（Cross-site scripting）是最常见和基本的攻击Web网站的方法。攻击者在网页上发布包含攻击性代码的数据。当浏览者看到此网页时，特定的脚本就会以浏览者用户的身份和权限来执行。通过XSS可以较容易地修改用户数据、窃取用户信息。

- 跨站请求伪造攻击：跨站请求伪造CSRF（Cross-site request forgery）是另一种常见的攻击。攻击者通过各种方法伪造一个请求，模仿用户提交表单的行为，从而达到修改用户的数据或者执行特定任务的目的。为了假冒用户的身份，CSRF攻击和XSS攻击通常会相互配合，但也可以通过其它手段，例如诱使用户单击一个包含攻击的链接。

- Http Headers攻击：使用浏览器查看任何Web网站，无论您的Web网站采用何种技术和框架，都用到了HTTP协议。HTTP协议在Response header和content之间有一个空行，即两组CRLF（0x0D 0A）字符，这个空行标志着headers的结束和content的开始，攻击者可以利用这一点。只要攻击者有办法将任意字符注入到Headers中，这种攻击就可以发生。

- 重定向攻击：一种常用的攻击手段是“钓鱼”。钓鱼攻击者通常会发送给受害者一个合法链接，当您访问链接时，会被导向一个非法网站，从而达到骗取用户信任、窃取用户资料的目的。为防止这种行为，我们必须对所有的重定向操作进行审核，以避免重定向到一个危险的地方。常见解决方案是白名单，将合法的要重定向的URL添加到白名单中，非白名单上的域名重定向时拒绝。第二种解决方案是重定向token，在合法的URL上加上token，重定向时进行验证。


## 站点只有登录才需要HTTPS吗？

不是。您需要从以下几个方面来分析：

- 从安全方面来看：一些页面为HTTP，一些页面为HTTPS，当通过HTTP或不安全的CDN服务加载其他资源（例如JS或CSS文件）时，网站也存在用户信息暴露的风险，而全站HTTPS是防止这种风险最简单的方法。

- 从性能方面来看：当网站存在HTTPS和HTTP两种协议时，跳转需对服务器进行大量的重定向，当这些重定向被触发时会减慢页面的加载速度。

- 从全网来看：浏览器对HTTPS的支持会更友好，搜索引擎也对HTTPS的收录有更好的支持。


## **配置HTTPS时，需要配置哪些证书？**

如果您仅需要加密客户端至CDN节点的请求，在CDN上配置HTTPS证书即可。

如果您需要配置全链路HTTPS访问，需要在CDN上配置HTTPS证书并在源站上配置HTTPS证书，详情请参见： [什么是HTTPS加速](https://help.aliyun.com/zh/cdn/user-guide/what-is-https-secure-acceleration "")。

## 开启CDN的HTTPS加速后会额外收费吗？

会额外收费。开启CDN的HTTPS加速，实际开启的是客户端到CDN边缘节点这段链路的HTTPS。因为SSL协议的握手和内容解密都需要计算，所以会增加CDN服务器的CPU资源损耗，但不会增加您源站服务器的资源损耗，因为CDN边缘节点到您源站这段链路使用的仍然是HTTP协议，不会额外增加您源站的损耗。

如果您购买不同类型的证书，则需要额外付费。您也可以登录阿里云[数字证书管理服务控制台](https://yundunnext.console.aliyun.com/?p=cas)申请个人测试证书（免费版）。个人测试证书（免费版）等级为DV，每个加速域名可以申请一个个人测试证书（免费版），证书有效期为3个月，到期后可以免费自动续签。设置好HTTPS证书后，该域名在CDN上的所有HTTPS请求数会收费。静态HTTPS请求数收费请参考 [HTTPS请求数计费](https://common-buy.aliyun.com/?spm=5176.7933777.J_3537169050.2.2429496ezmVFeY&commodityCode=dcdnpaybag#/buy)。

## IP黑白名单、User-Agent 黑名单、请求返回403/404时，HTTPS请求数是否会被计费？

HTTPS请求数会被计费，当命中某些策略规则，返回403和404的状态码时，该请求是被正确响应了的，所以会被记一次HTTPS请求数；该请求由于不携带任何的资源内容，所以请求的流量会非常小，计费流量也极小。

## 源站已经配置了HTTPS，CDN上还需要配置HTTPS吗？

HTTPS是客户端和服务端的交互，未使用CDN之前，客户端是直接和源站交互，因此源站需要配置HTTPS。使用CDN之后，是客户端和CDN交互，如果您需要以HTTPS的形式访问CDN，则必须在CDN上配置HTTPS证书。在CDN上配置HTTPS证书的方法，请参见 [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate#task-261642 "")。

## 开启HTTPS加速会消耗更多资源或降低访问速度吗？

当源站开启HTTPS时，相比于源站通过HTTP访问，计算资源的消耗会有所增加，主要来自于HTTPS握手过程中对非对称加解密的消耗，尤其在高并发情况下资源消耗增长明显。对称加解密消耗与HTTP基本一致，因此需要增加Session复用率，但直接通过HTTPS访问源站相比于直接通过HTTP访问源站耗时更长。

通过全站加速进行全链路HTTPS访问时，SSL握手的平均时间会有所缩短，在高并发情况下，源站Session复用率会明显的提高，源站资源消耗会有所降低。

- 对于静态内容：通过边缘分发的方式，在增加握手时间消耗的同时，减少了传输时间的消耗，因此整体访问上会有所减少，且静态资源无需回源，减少了源站的交互，可以降低源站的资源消耗。

- 对于动态内容：在路径选择上比通过传统公网访问更加可控且路径最优，动态请求必须回源，通过全站加速的网络回源，可以增加Session复用率，整体传输速度会有所提升。由于动态请求必须回源，因此非对称加解密是必不可少，源站的资源消耗会有所增加。但通过全站加速回源形成了全链路HTTPS访问的方式，整体资源消耗上是最优。


## 如何配置HTTPS证书？

您可以在CDN控制台中配置HTTPS证书，具体操作请参见 [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate#task-261642 "")。

## 上传HTTPS证书，提示证书重复怎么办？

当您上传 **自定义上传（证书+私钥）** 类型的证书时，如果系统提示证书重复，您需要修改证书名称后再重新上传。

## **上传第三方证书时，有多个.crt证书，如何上传证书？**

中级机构颁发的证书文件包含多份证书，您需要将服务器证书与中间证书拼接成一份完整的证书后再上传。

通过文本编辑器打开所有\*.PEM格式的证书文件，将服务器证书放在第一位，中间证书放在第二位，证书之间不能有空行。通常情况下，证书颁发机构颁发证书时会有对应的说明，请注意查阅规则说明。

拼接后的证书如下图所示。

![拼接后的PEM格式证书](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7167150161/p214007.png)

## 配置HTTPS证书时提示“证书格式不对”，如何进行转换？

HTTPS配置仅支持PEM格式的证书，不同的证书颁发机构对证书内容的上传有不同的要求，具体格式要求请参见 [证书格式说明](https://help.aliyun.com/zh/cdn/user-guide/certificate-formats#concept-grb-4pl-xdb "")。如果您的证书格式不是PEM，请完成格式转换后再上传，具体请参见 [证书格式转换方式](https://help.aliyun.com/zh/cdn/user-guide/certificate-formats#section-cn2-rql-xdb "")。

## 源站的HTTPS证书更新了，CDN上需要同步更新吗？

不需要。源站的HTTPS证书更新后不会影响CDN上的HTTPS证书，当您在CDN上配置的HTTPS证书将要到期或者已经到期时，您才需要在CDN上更新HTTPS证书。具体操作请参见 [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate#task-261642 "")。

## **配置HSTS时，打开包含子域名后，子域名上是否需要打开HSTS？**

子域名上无需打开HSTS，打开“包含子域名”后，HSTS策略将在全部子域名中生效，请确保各子域名支持正常HTTPS访问，否则子域名将无法访问。

## 已经配置了HTTPS，为什么客户端还是HTTP访问？

客户端是以HTTP访问还是HTTPS访问完全是客户端的行为，如果您希望客户端强制使用HTTPS访问，可以在CDN上开启强制HTTPS跳转。具体操作请参见 [配置强制跳转](https://help.aliyun.com/zh/cdn/user-guide/configure-url-redirection#task-261642 "")。

## 为什么大多数设备能够顺利访问通过HTTPS协议加速的域名，但是一些设备却无法访问？

这主要是因为CDN在处理HTTPS请求时依赖于SNI。SNI是TLS协议的一个扩展，它允许客户端在发起HTTPS连接请求时指定想要访问的主机名。

然而，某些较旧或特定配置的客户端（例如，老旧版本的Android或iOS操作系统、Java 6及以下版本、以及一些物联网IoT设备等），可能不支持SNI或者在发起HTTPS请求时不会发送SNI信息。这种情况下，CDN节点无法确定客户端想要访问的确切站点，从而不能提供正确的SSL/TLS证书。结果就是HTTPS连接尝试失败，表现为用户无法访问网站内容。

为了改善这一状况，建议采取以下措施：

- **升级客户端系统**：确保使用的操作系统和软件都是最新版本，以获得对SNI的支持。

- **更新IoT设备固件**：对于物联网设备，定期检查并安装厂商提供的最新固件更新。


## **私钥文件如何去除密码保护？**

1. **确认密钥是否带有密码保护**

如果确定私钥存在密码保护并且清楚私钥的加密方式，可以直接参考步骤2进行解密。不清楚私钥是否存在密码保护或者不清楚私钥的加密方式，请参考以下步骤处理：

1. **RSA算法加密的私钥**

      使用 [OpenSSL](https://www.openssl.org/source/) 运行以下命令，如果私钥是加密的，OpenSSL 会提示你输入密码：`Enter pass phrase for <加密的私钥文件>:`；如果私钥未加密，OpenSSL 不会要求输入密码，则会直接显示私钥信息；如果出现 error 报错信息，则说明该私钥不是RSA加密的文件。















      ```bash
      openssl rsa -in <加密的私钥文件> -text -noout
      ```

2. **ECC/SM2算法加密的私钥**

      使用 [OpenSSL](https://www.openssl.org/source/) 运行以下命令，如果私钥是加密的，OpenSSL 会提示你输入密码：`Enter pass phrase for <加密的私钥文件>:`；如果私钥未加密，OpenSSL 不会要求输入密码，则会直接显示私钥信息；如果出现 error 报错信息，则说明该私钥不是ECC或SM2加密的文件。















      ```bash
      openssl ec -in <加密的私钥文件> -text -noout
      ```
2. 解密方案

   - 证书的加密算法为 RSA 时，您需要在安装了 [OpenSSL](https://www.openssl.org/source/) 或 [BabaSSL](https://github.com/BabaSSL/BabaSSL) 的计算机上执行以下命令来解密私钥。















     ```bash
     openssl rsa -in <加密的私钥文件> -passin pass:<私钥密码> -out <解密的私钥文件>
     ```

   - 证书的加密算法为 ECC或SM2 时，您需要在安装了 [OpenSSL](https://www.openssl.org/source/) 或 [BabaSSL](https://github.com/BabaSSL/BabaSSL) 的计算机上执行以下命令来解密私钥。















     ```bash
     openssl ec -in <加密的私钥文件> -passin pass:<私钥密码> -out <解密的私钥文件>
     ```