### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[HTTPS配置](https://help.aliyun.com/zh/cdn/user-guide/https-for-cdn-or-dcdn/)配置OCSP Stapling

# 配置OCSP Stapling

更新时间：2024-02-04 00:56:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置HTTP/2](https://help.aliyun.com/zh/cdn/user-guide/enable-http-or-2)[下一篇：配置协议重定向](https://help.aliyun.com/zh/cdn/user-guide/configure-url-redirection)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能说明

前提条件

操作步骤

OCSP Stapling功能可实现由CDN预先缓存在线证书验证结果并下发给客户端，无需客户端直接向CA站点查询证书状态，从而减少证书验证时间，提升用户访问速度。

## 功能说明

OCSP（Online Certificate Status Protocol，在线证书状态协议）是由数字证书颁发机构CA（Certificate Authority）提供，客户端通过OCSP可实时验证证书的合法性和有效性。

未开启OCSP Stapling时：客户端的每次请求都会向CA进行OCSP查询，以确认证书未被吊销，频繁的OCSP查询请求导致TLS握手效率较低，将影响用户访问速度。

开启OCSP Stapling功能后，OCSP信息查询的工作将由CDN服务器完成。CDN通过低频次查询，将查询结果缓存到服务器中（默认缓存时间60分钟）。当客户端向服务器发起TLS握手请求时，CDN服务器将证书的OCSP信息和证书一起发送给客户端，无需再向数字证书认证机构（CA）发送查询请求。极大地提高了TLS握手效率，节省了证书验证时间。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1026207071/d64e3d4a5039g.svg)

**重要**

- OCSP Stapling功能默认关闭。

- OCSP Stapling功能默认缓存时间是1小时，缓存过期后第一个访问请求OCSP Stapling将不生效，直到重新获取OCSP Stapling信息为止。

- 配置了HTTPS加速的域名，可启用或者关闭OCSP Stapling功能，删除HTTPS证书配置后，OCSP Stapling功能会同步失效。

- OCSP信息是无法伪造的，因此这一过程不会产生额外的安全问题。


## 前提条件

执行配置前，请您确保：

- 您已成功配置HTTPS证书，操作方法请参见 [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate#task-261642 "")。

- 客户端需支持OCSP扩展字段，如果客户端版本不支持OCSP扩展字段，则功能无法生效。


## 操作步骤

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **HTTPS配置**。

5. 在 **OCSP Stapling** 区域，打开或关闭 **开关**。![OCSP](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3427278561/p469995.png)