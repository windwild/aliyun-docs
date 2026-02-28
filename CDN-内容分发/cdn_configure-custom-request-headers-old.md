### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 修改入站请求头

# 修改入站请求头

更新时间：2025-06-12 23:06:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

操作步骤

相关文档

配置回源HTTP请求头（旧版）是老版本的回源HTTP请求头功能。默认情况下，CDN控制台上不再展示回源HTTP请求头（旧版）功能。只有在域名之前，在回源HTTP请求头（旧版）功能上，添加过配置的情况下，才会展示出该功能，并且只能查看或者删除配置，无法新增或者修改配置。

## 背景信息

HTTP请求头是HTTP的请求消息头的组成部分之一，可携带特定请求参数信息并传递给服务器。

当CDN节点上没有缓存用户请求的内容时，CDN节点会回源站拉取资源，源站可获取到CDN节点回源请求头中携带的信息。为了便于源站识别用户信息，您可以配置回源HTTP请求头功能，改写用户回源请求中的HTTP Header信息，携带特定的参数信息给源站。例如，通过X-Forwarded-For头部携带真实客户端IP至源站。

![HTTP消息头](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4046109361/p87913.png)

**说明**

目前CDN提供了升级版的配置回源HTTP请求头功能（升级版功能支持替换、变更、删除等更加丰富的改写操作方式、是否允许重复和跨域校验等功能），具体操作，请参见 [修改出站请求头](https://help.aliyun.com/zh/cdn/user-guide/configure-custom-request-headers#task-2429551 "")。

## 操作步骤

1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **回源配置**。

5. 单击 **修改出站请求头** 页签。

6. 您可以在下方 **回源HTTP请求头（旧版）** 区域查看已配置的存量请求头设置。



![回源HTTP请求头（旧版）](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1126892761/p547585.png)


## 相关文档

- [批量配置域名](https://help.aliyun.com/zh/cdn/api-batchsetcdndomainconfig#doc-api-Cdn-BatchSetCdnDomainConfig "")