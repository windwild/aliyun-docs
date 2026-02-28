### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[了解计费](https://help.aliyun.com/zh/oss/understanding-billing/)计费概述

# 计费概述

更新时间：2026-02-05 05:54:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费单价

计费项

计费方式

新用户免费试用额度

计费周期

相关文档

对象存储 OSS **按实际使用量付费**。

将数据存储到 OSS 后，会按存储时长产生 **存储费用**；每次上传、下载或访问数据产生 **请求费用**；通过公网分发数据则会产生 **外网流出流量费用**。此外，启用 CDN 加速、图片处理、传输加速、DDoS 防护等增值服务，会产生对应的 **增值计费项**。

如果业务的访问模式稳定，具备可预期的存储量、请求量和外网流出流量，建议根据账单中的具体计费项购买资源包进行抵扣，以降低成本。 **资源包必须与计费项精准对应**（如下行流量包仅能抵扣外网流出流量费用），买错将导致无法抵扣。

## **计费单价**

关于OSS的定价详情，请参见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)。

## **计费项**

OSS的计费项包含以下类型：

- 基础计费项：大多数用户使用OSS过程中都会产生的费用，包括存储数据产生的 [存储费用](https://help.aliyun.com/zh/oss/storage-fees "")、从OSS下载文件或通过CDN分发文件产生的 [流量费用](https://help.aliyun.com/zh/oss/traffic-fees "")、以及对数据的每一次读写请求产生的 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees "")。

- 增值计费项：少数用户使用OSS过程中，主动开通并使用增值服务产生的费用。增值服务旨在提高数据处理效率或改善用户体验，这些增值服务包括但不限于图片处理、传输加速、DDoS防护等。更多信息，请参见 [增值计费项](https://help.aliyun.com/zh/oss/value-added-billing-item/ "")。


#### **OSS计费图**

当前OSS可能产生的所有计费项如下图所示：

![oss费用组成-cn-zh](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7669164571/p686969.png)

## 计费方式

OSS常用计费方式如下：

- [按量付费](https://help.aliyun.com/zh/oss/pay-as-you-go-1#concept-2247263 "")：后付费方式，先使用、后付费，按照各计费项的实际用量结算费用。适用于业务用量经常有变化的场景。

- [资源包](https://help.aliyun.com/zh/oss/resource-plan/#concept-l43-j4h-tdb "")：预付费方式，先预付、后使用，针对部分常用计费项（例如存储费用、流量费用）支持专用的资源包。预先购买针对不同计费项推出的优惠资源包，在费用结算时，优先从资源包抵扣用量，超出资源包额度的部分，采用按量付费。适用于业务用量相对稳定的场景。


**适用于存储费用的其他预付费方式**

针对部分存储费用计费项，还支持以下预付费方式：

- [存储容量单位包SCU](https://help.aliyun.com/zh/oss/scu#concept-2005963 "")：针对部分存储费用支持SCU。SCU除了用于抵扣OSS的存储费用，还可用于抵扣多种云存储产品存储容量费用。

- [预留空间](https://help.aliyun.com/zh/oss/reserved-capacity#main-2309838 "")：针对有地域属性Bucket产生的标准存储（本地冗余）容量费用以及ECS快照存储费用的预付费产品。预先购买预留空间，在费用结算时，优先从预留空间抵扣用量，先购买，后抵扣。

- [无地域属性预留空间](https://help.aliyun.com/zh/oss/anywhere-reserved-capacity#main-2309689 "")：针对无地域属性Bucket产生的标准存储（本地冗余）容量费用的预付费产品。预先购买无地域属性的预留空间，在费用结算时，优先从无地域属性预留空间抵扣用量，先购买，后抵扣。


## **新用户免费试用额度**

首次开通OSS的用户可享受 [新用户免费试用额度](https://help.aliyun.com/zh/oss/free-quota-for-new-users "")，免费享用一定额度的标准存储（本地冗余）容量、外网流出流量以及请求次数费用。

## 计费周期

OSS以小时为周期统计所有资源的使用量，并按照使用量计算产生的费用。

**说明**

以存储费用为例，[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)中明确了存储费用的单价为`元/GB/月`，但账单中的计费项按小时计费，计算方法为`实际资源使用量×每小时单价`。因此，计算费用时，需将存储费用的单价转换为小时单价。例如标准型（本地冗余存储）单价为`0.12元/GB/月`，其按小时计费的单价约为`0.000167元/GB/小时（0.12÷30÷24）`。

## 相关文档

- [计费项](https://help.aliyun.com/zh/oss/billable-items/ "")

- [计费方式](https://help.aliyun.com/zh/oss/billing-method/ "")

- [新用户免费试用额度](https://help.aliyun.com/zh/oss/free-quota-for-new-users "")

- [查询OSS小时数据](https://help.aliyun.com/zh/oss/query-oss-billing-data-generated-on-an-hourly-basis "")

- [查询账号级别的用量情况](https://help.aliyun.com/zh/oss/query-resource-usage-of-an-alibaba-cloud-account "")

- [账单查询](https://help.aliyun.com/zh/oss/query-bills "")

- [计费案例](https://help.aliyun.com/zh/oss/billing-examples "")

- [成本优化](https://help.aliyun.com/zh/oss/faq-6/ "")

- [欠费说明](https://help.aliyun.com/zh/oss/overdue-payments "")