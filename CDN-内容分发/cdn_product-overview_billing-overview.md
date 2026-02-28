### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[产品概述](https://help.aliyun.com/zh/cdn/product-overview/)[产品计费](https://help.aliyun.com/zh/cdn/product-overview/billing/)计费概述

# 计费概述

更新时间：2026-01-16 02:25:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：阿里云CDN支持新一代传输协议QUIC](https://help.aliyun.com/zh/cdn/product-overview/alibaba-cloud-cdn-supports-quic)[下一篇：基础服务计费](https://help.aliyun.com/zh/cdn/product-overview/billing-rules-of-basic-services)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速选择付费方式

计费组成

核心计费概念

下行流量与回源流量

计费区域

计费周期

视频讲解

相关文档

通过阅读本文，您可以快速了解阿里云CDN的付费方式、计费组成和定价等计费信息。

**重要**

- CDN所有计费方式均按照 **账户UID** 维度进行统计收费。

- 无特别说明的情况下，CDN的按流量计费、按带宽峰值计费和月结95带宽峰值计费，都是指在CDN的L1节点上产生的下行流量带宽。


- 在CDN控制台添加的且“业务类型”为 **全站加速** 的加速域名，将根据全站加速产品的价格计费。您可以前往[全站加速控制台](https://dcdn.console.aliyun.com/)查看和使用这些域名。

- CDN可与全站加速 **共享** 下行流量资源包、静态HTTPS请求数包和边缘WAF请求数包。

- CDN产品出账存在3~4小时延迟。


## 快速选择付费方式

CDN支持 **按量付费**（默认）和 **资源包**（针对常用付费服务）两种付费方式，根据业务流量特征，可参考下表快速选择付费方式。

| **业务流量是否稳定？** | **付费方式** | **优势** | **说明** | **定价详情** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **业务流量是否稳定？** | **付费方式** | **优势** | **说明** | **定价详情** |
| **波动较大**，有明显波峰波谷或无法预估 | 按量付费（后付费） | 按实际使用量结算，用多少付多少，灵活应对业务变化。 | 按照各计费项的实际用量结算费用， **先使用，后付费**。 | 阿里云CDN各计费项价格：可参见[按流量计费](https://help.aliyun.com/zh/cdn/product-overview/billing-rules-of-basic-services#section-ymq-7ae-3th "")。 |
| **相对稳定**，可预估月度用量 | 资源包（预付费） | 价格比按量付费更优惠，适合成本可控的业务。 | - 预先购买针对不同的计费项推出的优惠资源包，在费用结算时，优先从资源包抵扣用量， **先购买，后抵扣**。<br>  <br>- 超出资源包抵扣额度的用量将计入按量计费，会产生后付费账单，请根据您的所需服务、业务量，购买适合业务额度的资源包。关于资源包的介绍、选购和抵扣规则等，请参见 [资源包介绍](https://help.aliyun.com/zh/cdn/product-overview/resource-plan-overview#task-2183641 "")、 [资源包选购](https://help.aliyun.com/zh/cdn/product-overview/guidelines-for-choosing-resource-plans#concept-2102901 "") 和 [资源包抵扣规则](https://help.aliyun.com/zh/cdn/product-overview/rules-for-applying-resource-plans#concept-2102902 "")。 | 资源包定价：可参见[资源包定价](https://common-buy.aliyun.com/?spm=5176.7933777.J_3537169050.2.2429496ezmVFeY&commodityCode=dcdnpaybag#/buy)。 |

## 计费组成

CDN计费分为，**基础服务计费**（必选）+**增值服务计费**（可选），计费项组成如下图：

- [基础服务计费](https://help.aliyun.com/zh/cdn/product-overview/billing-rules-of-basic-services#concept-m3l-kvl-zdb "")（必选）：CDN加速产生的核心费用。基础服务费需要在 **按流量计费** 和 **按带宽峰值计费** 和**月结95带宽峰值计费**中选择一种，默认为 **按流量计费**。

- [增值服务计费](https://help.aliyun.com/zh/cdn/product-overview/billing-of-value-added-services/ "")（可选，单独计费）：如使用了静态HTTPS请求、实时日志投递等高级功能，会产生相应的额外费用。


![CDN计费](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1189736461/p406686.png)

## **核心计费概念**

### 下行流量与回源流量

- **下行流量（计费）**：指用户通过浏览器或客户端访问业务时，从 **CDN边缘节点** 下载数据所产生的流量。这是CDN **基础服务费** 的主要计费内容。

- **回源流量（不计费）**：指CDN边缘节点因未缓存或缓存过期，返回源站（如ECS、OSS）拉取数据时产生的流量。这部分流量不计入CDN的计费，但源站可能会因此产生出方向流量费用。


### 计费区域

系统会根据访问用户的IP地址判断其所属区域，并按该区域的单价进行计费。

阿里云CDN在全球各计费大区均部署了节点，可根据访问者IP地址进行精准的区域计费。各计费大区覆盖的国家和地区详情，请参见 [节点分布](https://help.aliyun.com/zh/cdn/product-overview/pop-distribution#concept-uqm-5h3-tdb "")。

| **计费区域** | **英文缩写** | **覆盖区域** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **计费区域** | **英文缩写** | **覆盖区域** |
| 中国内地 | CN | 中国内地 |
| 北美 | NA | 美国 |
| 欧洲 | EU | 乌克兰、英国、法国、荷兰、意大利、瑞典、德国、西班牙 |
| 亚太1区 | AP1 | 中国香港、日本、新加坡、泰国、菲律宾、马来西亚 |
| 亚太2区 | AP2 | 印度尼西亚、印度、韩国、巴基斯坦 |
| 亚太3区 | AP3 | 澳大利亚 |
| 中东/非洲 | MEAA | 土耳其、阿联酋、科威特、卡塔尔、阿曼、尼日利亚、南非 |
| 南美 | SA | 巴西 |

### **计费周期**

CDN服务的计费周期如下：

| **计费周期** | **扣费及出账时间** | **适用的计费项** |
| --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **计费周期** | **扣费及出账时间** | **适用的计费项** |
| 小时 | 按小时结算，账单出账时间通常在当前计费周期结束后3~4小时左右，具体以系统实际出账时间为准。 | 基础服务 | [按流量计费](https://help.aliyun.com/zh/cdn/product-overview/billing-rules-of-basic-services#concept-m3l-kvl-zdb "") |
| 增值服务 | - [静态HTTPS请求数](https://help.aliyun.com/zh/cdn/product-overview/billing-of-https-requests-for-static-content#concept-2186401 "")<br>  <br>- [静态QUIC请求数](https://help.aliyun.com/zh/cdn/product-overview/billing-of-quic-requests-for-static-content#concept-2186404 "")<br>  <br>- [CDN WAF请求数](https://help.aliyun.com/zh/cdn/product-overview/alibaba-cloud-cdn-waf-requests#concept-2186405 "")<br>  <br>- [实时日志投递](https://help.aliyun.com/zh/cdn/product-overview/billing-of-real-time-log-delivery#concept-2186407 "") |
| 日 | 按日计费，每日凌晨4点左右出前一日账单并扣费，具体出账时间以系统为准。 | 基础服务 | [按带宽峰值计费](https://help.aliyun.com/zh/cdn/product-overview/billing-rules-of-basic-services#concept-m3l-kvl-zdb "") |
| 月 | 当前计费周期结束的下个自然月1日凌晨4点左右。 | 基础服务 | [月结95带宽峰值计费](https://help.aliyun.com/zh/cdn/product-overview/billing-rules-of-basic-services#concept-m3l-kvl-zdb "") |

## 视频讲解

计费概述

## 相关文档

|     |     |
| --- | --- |
| **选择加速服务计费方式** | - [基础服务计费](https://help.aliyun.com/zh/cdn/product-overview/billing-rules-of-basic-services "")<br>  <br>- [增值服务计费](https://help.aliyun.com/zh/cdn/product-overview/billing-of-value-added-services/ "")<br>  <br>- [变更计费方式](https://help.aliyun.com/zh/cdn/product-overview/change-the-metering-method "")<br>  <br>- [CDN定价详情](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.10.1b444ee22Dxy8y#/cdn/detail/cdn) |
| **资源包** | - [资源包选购](https://help.aliyun.com/zh/cdn/product-overview/guidelines-for-choosing-resource-plans "")<br>  <br>- [资源包抵扣规则](https://help.aliyun.com/zh/cdn/product-overview/rules-for-applying-resource-plans "")<br>  <br>- [查询资源包明细](https://help.aliyun.com/zh/cdn/product-overview/query-the-details-of-resource-plans-1 "")<br>  <br>- [设置资源包预警](https://help.aliyun.com/zh/cdn/product-overview/configure-low-capacity-alerts "")<br>  <br>- [退款说明](https://help.aliyun.com/zh/cdn/product-overview/money-back-guarantees "") |
| **更多参考** | - [欠费说明](https://help.aliyun.com/zh/cdn/product-overview/overdue-payments "")<br>  <br>- [用量概述](https://help.aliyun.com/zh/cdn/user-guide/resource-usage-overview "")<br>  <br>- [账单查询](https://help.aliyun.com/zh/cdn/product-overview/query-bills "")<br>  <br>- [高额账单风险警示](https://help.aliyun.com/zh/cdn/product-overview/configure-high-bill-alerts "")<br>  <br>- [计费常见问题](https://help.aliyun.com/zh/cdn/product-overview/faq-about-billing/ "") |