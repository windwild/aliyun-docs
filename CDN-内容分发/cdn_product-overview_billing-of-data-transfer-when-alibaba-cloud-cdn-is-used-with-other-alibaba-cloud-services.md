### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[产品概述](https://help.aliyun.com/zh/cdn/product-overview/)[产品计费](https://help.aliyun.com/zh/cdn/product-overview/billing/)[计费常见问题](https://help.aliyun.com/zh/cdn/product-overview/faq-about-billing/)阿里云CDN与阿里云其他产品配合使用时流量如何计费？

# 阿里云CDN与阿里云其他产品配合使用时流量如何计费？

更新时间：2024-02-05 04:15:28

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

可能原因

阿里云CDN可与阿里云其他产品配合使用，例如ECS、OSS。由于CDN节点在全球均有分布，所以与其他云产品之间的流量需通过公网传输，流量费用如何计算？

## 可能原因

CDN流量与其他云产品流量各自独立计费，之间并无关系。每个产品的收费请查看其产品的计费规则。

例如，某客户购买了CDN和OSS来提供文件下载服务，当客户端访问CDN时，如果CDN节点无对应的资源缓存，则需要回源请求，此时会产生两次流量费用，分别是CDN的流出流量和OSS的流出流量，这两个流出流量由两个产品分别进行计费。![CDN回源流量](https://help-static-aliyun-doc.aliyuncs.com/assets/img/9607343751/p3734.png)

- 当CDN回源从OSS获取资源时：流量从OSS流向CDN，CDN不计费，OSS计费。

- 当OSS资源缓存到CDN时：流量从CDN流出，CDN计费，OSS不计费。


**说明**

阿里云各产品配套使用会有一定的优惠和折扣。例如，CDN回源OSS获取资源时，OSS的流出流量将有非常优惠的价格。