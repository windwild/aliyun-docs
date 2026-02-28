### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[访问控制](https://help.aliyun.com/zh/cdn/user-guide/access-control/)访问控制常见问题

# 访问控制常见问题

更新时间：2024-07-26 03:35:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CDN盗刷解决方案之referer拦截](https://help.aliyun.com/zh/cdn/user-guide/cdn-abuse-prevention-by-blocking-referer)[下一篇：什么是缓存](https://help.aliyun.com/zh/cdn/user-guide/what-is-caching)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

IP黑白名单配置时有IP地址数量限制，配置IP地址段算1个还是多个IP地址数？

需要在源站将CDN设置为访问白名单，能提供阿里云CDN访问源站的节点IP吗？

为什么IP黑名单中的IP仍可访问资源？

如何获取客户端真实IP地址？

URL鉴权异常导致访问CDN加速资源返回403错误?

报错信息：X-Tengine-Error:denied by req auth: no url arg auth\_key

报错信息：X-Tengine-Error: denied by req auth: expired timestamp

报错信息：X-Tengine-Error: denied by req auth: invalid md5hash

阿里云CDN URL鉴权和远程鉴权可以同时开启吗？

远程鉴权中鉴权服务器支持配置为内网地址吗？

鉴权服务器返回的状态码既不是成功状态码，也不是失败状态码，CDN为什么会直接放行？

远程鉴权服务器发生故障或宕机时，CDN会直接放行所有请求吗？

配置限制访问CDN资源的用户时，如果遇到疑问请参考以下常见问题及处理建议。

## **IP黑白名单配置时有IP地址数量限制，配置IP地址段算1个还是多个IP地址数？**

CDN配置IP黑白名单时，最多可配置约700个IPv6地址，2000个IPv4地址。

1个IP地址段算1个IP地址数配置。

## **需要在源站将CDN设置为访问白名单，能提供阿里云CDN访问源站的节点IP吗？**

如果您的日峰值带宽为1 Gbps以上，请[填写信息](https://page.aliyun.com/form/act2017566026/index.htm)申请 [DescribeL2VipsByDomain](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-describel2vipsbydomain "") 接口的调用权限，获取指定域名L2节点的IP地址（即回源IP地址列表）。

如果您不满足要求，建议可以在您的源站放开防火墙策略。

## **为什么IP黑名单中的IP仍可访问资源？**

CDN作为服务端，无法控制客户端的访问。配置IP黑名单后，该IP地址请求发送到CDN，会返回错误码403，并且CDN日志中仍会记录该请求记录。查看日志的方法，请参见 [下载离线日志](https://help.aliyun.com/zh/cdn/user-guide/download-logs#task-187634 "")。

## **如何获取客户端真实IP地址？**

使用CDN之后，可以通过X-Forwarded-For字段获取客户端真实IP地址，具体操作请参见 [获取客户端真实IP](https://help.aliyun.com/zh/waf/web-application-firewall-2-0/user-guide/retrieve-the-originating-ip-addresses-of-clients "")。

## **URL鉴权异常导致访问** CDN **加速资源返回403错误?**

为了保护站点的资源不被非法站点下载盗用，采用URL鉴权方式保护源站资源，在开启阿里云CDN的URL鉴权功能后，访问CDN加速资源返回403错误，通过浏览器的开发者工具，在**Response Header**中查看详细错误信息如下：

### **报错信息：** X-Tengine-Error:denied by req auth: no url arg auth\_key

- **问题原因**：没有携带鉴权参数，CDN开启了鉴权，但是实际访问URL中没有携带鉴权参数。

- **解决方案**：如果您需要使用CDN的鉴权功能，请参见[URL鉴权](https://help.aliyun.com/zh/cdn/user-guide/configure-url-signing "")，配置URL鉴权。如果您不需要CDN的鉴权功能，登录[CDN控制台](https://cdn.console.aliyun.com/domain/list)，关闭鉴权即可。


### **报错信息：** X-Tengine-Error: denied by req auth: expired timestamp

- **问题原因**：鉴权过期，CDN开启了鉴权，并且URL携带了鉴权参数，但是鉴权参数过期。

- **解决方案**：如果鉴权过期，请参见[URL鉴权](https://help.aliyun.com/zh/cdn/user-guide/configure-url-signing "")，重新生成鉴权URL。


### **报错信息：** X-Tengine-Error: denied by req auth: invalid md5hash

- **问题原因**：鉴权计算错误，鉴权参数的MD5值计算不正确。

- **解决方案**：建议先使用CDN控制台的地址生成器生成URL来对比自己的鉴权代码，或者参见[鉴权代码示例](https://help.aliyun.com/zh/edge-security-acceleration/dcdn/user-guide/url-signing-examples "")。![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6255874071/p753629.png)


## **阿里云CDN URL鉴权和远程鉴权可以同时开启吗？**

可以，阿里CDN URL鉴权和远程鉴权可以同时开启，请求先经过URL鉴权，再经过远程鉴权。

## **远程鉴权中鉴权服务器支持配置为内网地址吗？**

不支持，远程鉴权服务器需要配置为公网地址。

## **鉴权服务器返回的状态码既不是成功状态码，也不是失败状态码，CDN为什么会直接放行？**

为避免因为一些异常情况阻断所有的用户请求，如果鉴权服务器返回的状态码既不是成功状态码，也不是失败状态码，CDN节点默认放过用户请求（例如：鉴权成功状态码设置为200，鉴权服务器返回201时，结果为放过用户请求）。

您可以在控制台设置 **其他状态码是否放行** 参数，选择是否放行鉴权服务器返回的其他状态码。

## **远程鉴权服务器发生故障或宕机时，CDN会直接放行所有请求吗？**

不会。远程鉴权服务器发生故障或宕机时，CDN与鉴权服务器之间的数据交互超时后，按照设置的 **鉴权超时之后的动作** 参数，选择是否放行鉴权超时的用户请求。