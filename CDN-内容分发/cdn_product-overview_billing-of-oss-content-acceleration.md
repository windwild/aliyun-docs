### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[产品概述](https://help.aliyun.com/zh/cdn/product-overview/)[产品计费](https://help.aliyun.com/zh/cdn/product-overview/billing/)CDN加速OSS计费说明

# CDN加速OSS计费说明

更新时间：2026-01-12 04:08:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置资源包预警](https://help.aliyun.com/zh/cdn/product-overview/configure-low-capacity-alerts)[下一篇：变更计费方式](https://help.aliyun.com/zh/cdn/product-overview/change-the-metering-method)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费说明

优惠资源包说明

相关文档

阿里云OSS可提供低成本的存储，CDN可以实现静态资源加速分发。您可将静态资源（包括静态脚本、音视频、图片、附件等文件）托管在阿里云OSS中，并使用CDN加速，降低存储成本的同时，加速资源分发并减轻源站压力。

## 计费说明

当OSS作为CDN源站时，可能会产生以下费用：**CDN服务费**+**OSS服务费**。

**重要**

CDN服务费与OSS服务费各自独立计费（例如流量费），价格存在差异，具体价格请查看对应产品的计费规则。

计费项和流量费说明如下：

- **可能产生的计费项**




| **计费项** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **计费项** | **说明** |
| CDN服务费 | 主要为“CDN下行流量费”。<br>根据实际业务情况，可能还会存在“静态HTTPS请求费”等其他费用。详细计费项，请参见 [CDN计费概述](https://help.aliyun.com/zh/cdn/product-overview/billing-overview#concept-2331052 "")。 |
| OSS服务费 | 主要为“OSS流出到CDN流量费+数据存储费”。<br>根据实际业务情况，可能还会存在“OSS请求费用”等其他费用。详细计费项，请参见 [OSS计量计费概述](https://help.aliyun.com/zh/oss/billing-overview#concept-n4t-mwg-tdb "")。 |

- **流量费说明**



当OSS作为CDN源站时，可能会产生**CDN下行流量费（由CDN计费）**和**OSS流出到CDN流量费（由OSS计费）**。



  - CDN下行流量费：用户从CDN节点请求资源，节点将资源下发给客户端时产生的流量费用；流量从CDN流向客户端，消耗的流量由CDN计费。价格详见[CDN定价-按流量计费](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.5be031c9TyAAu1#/cdn/detail/cdn)。

  - CDN节点回源到OSS产生的流量，不计费。

  - OSS流出到CDN节点产生的流量费：流量从OSS流向CDN，由OSS计费。价格详见[OSS定价-流量费用-OSS流出到CDN流量](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.26443048xzpfk5#/oss/detail/ossbag)。



    **说明**





    阿里云CDN回源阿里云OSS的流量优惠说明：



    - 用户需要在控制台上把源站类型设置为“OSS域名”，这样阿里云OSS产品会将来自阿里云CDN产品的回源流量识别为“CDN回源流出流量”，从而享受到更优惠的价格。

    - 如果用户在控制台上把源站类型误设为“源站域名”，阿里云OSS产品会将来自阿里云CDN产品的回源流量识别为“外网流出流量”，这种情况下就享受不到优惠价格。

    - 当CDN回源节点和回源的OSS的存储空间均在非中国内地区域时，OSS流出到CDN的流量免费。


![OSS计费](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3015821861/p377442.png)

## 优惠资源包说明

如果您使用CDN加速OSS中的资源，OSS和CDN均提供了资源包，可有效降低您的回源成本。

| **资源包** | **使用说明** |
| --- | --- |

|     |     |
| --- | --- |
| **资源包** | **使用说明** |
| [CDN下行流量包](https://common-buy.aliyun.com/?spm=5176.197032.J_5834642020.4.141442c417YQT6&commodityCode=dcdnpaybag#/buy) | 用于抵扣CDN节点将资源下发给客户端时产生的流量费用，超出部分自动按量计费。 |
| [CDN静态HTTPS请求数资源包](https://common-buy.aliyun.com/?spm=5176.197032.J_5834642020.4.141442c417YQT6&commodityCode=dcdnpaybag#/buy) | 用于抵扣CDN加速服务中产生的静态HTTPS请求费用，超出部分自动按量计费。 |
| [OSS回源流量包](https://common-buy.aliyun.com/?spm=5176.8064714.J_323065.pricedetail1111.59762bc6BGAZfq&commodityCode=ossbag&request=%7B%22region%22%3A%22china-common%22%7D#/buy) | 用于抵扣CDN回源时产生的流量费用，超出部分自动按量计费。 |
| [OSS标准存储包](https://common-buy.aliyun.com/?spm=5176.8064714.J_323065.pricedetail1111.59762bc6BGAZfq&commodityCode=ossbag&request=%7B%22region%22%3A%22china-common%22%7D#/buy) | 用于抵扣“标准存储-本地冗余”和“ECS快照”的存储容量，超出部分自动按量计费。 |

## 相关文档

- [CDN加速OSS资源](https://help.aliyun.com/zh/cdn/use-cases/accelerate-the-retrieval-of-resources-from-an-oss-bucket-in-the-alibaba-cloud-cdn-console#task-1937765 "")