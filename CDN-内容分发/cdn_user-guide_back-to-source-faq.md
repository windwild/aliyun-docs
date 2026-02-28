### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[回源配置](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-settings/)回源常见问题

# 回源常见问题

更新时间：2024-02-04 00:52:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：修改入站响应头](https://help.aliyun.com/zh/cdn/user-guide/rewrite-http-response-headers)[下一篇：资源监控](https://help.aliyun.com/zh/cdn/user-guide/resource-monitoring)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

配置回源协议为HTTPS后，无法访问网站，提示502报错时如何解决？

Common Name白名单校验的是什么？

如何在HTTPS回源时配置自定义端口？

CDN配置开启HTTPS功能后回源时使用的协议是HTTP还是HTTPS？

回源指您通过客户端请求访问资源时，如果CDN节点上未缓存该资源，或者您部署预热任务给CDN节点时，CDN节点会回源站获取资源。本文为您介绍关于回源的常见问题。

## **配置回源协议为HTTPS后，无法访问网站，提示502报错时如何解决？**

1. 检查域名是否能正确解析。

2. 检查源站是否能正常访问。

3. 检查源站是否支持HTTPS访问。

4. 如果源站IP绑定了多个域名，请 [配置回源SNI](https://help.aliyun.com/zh/cdn/user-guide/configure-sni "") 指明所请求的具体域名，服务器会根据配置的SNI名称正确返回域名对应的SSL证书，以确保正常回源。


## **Common Name白名单校验的是什么？**

发生回源时，将校验CDN节点回源请求中SNI和源站返回证书的CommonName值，两者需一致方可成功回源。

如果您未修改回源SNI，CDN节点回源请求携带的Host值默认是加速域名，所以校验的是加速域名的证书的Common Name。

## **如何在HTTPS回源时配置自定义端口？**

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **回源配置**。

5. 在 **回源协议** 区域，打开 **回源协议** 开关。

6. 单击 **修改配置**。

7. 根据需要配置自定义端口即可。


## CDN **配置开启HTTPS功能后回源时使用的协议是HTTP还是HTTPS？**

在CDN上配置HTTPS证书与回源协议无关，默认情况下回源协议以 [配置源站](https://help.aliyun.com/zh/cdn/user-guide/configure-an-origin-server#task-270231 "") 中设置的回源端口为准：

- 回源端口设置为443：以HTTPS协议回源。

- 回源端口设置为80或其他：以HTTP协议回源。


如果您需要指定回源协议，可根据需要 [配置回源协议](https://help.aliyun.com/zh/cdn/user-guide/configure-the-origin-protocol-policy "")。