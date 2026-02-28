### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[产品概述](https://help.aliyun.com/zh/ocr/product-overview/)产品计费

# 产品计费

更新时间：2025-05-12 01:56:01

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：票证批量导出轻应用](https://help.aliyun.com/zh/ocr/product-overview/use-a-light-application-to-export-multiple-tickets)[下一篇：免费额度](https://help.aliyun.com/zh/ocr/product-overview/free-quota)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

售卖渠道

计费类型

免费额度

资源包（预付费）

按量付费（后付费）

QPS叠加包

计费示例

资源包（预付费）

按量付费（后付费）

常见问题

长图识别服务如何开通与计费？

阿里云文字识别OCR支持按照调用次数付费（按量后付费）、购买专用或者共享资源包抵扣（预付费）两种付费模式。如果默认并发数无法满足业务需求时，您还可以通过购买QPS叠加包进行扩容，本文向您介绍付费的具体规则。

## **售卖渠道**

您可以通过 [阿里云官网](https://ocr.console.aliyun.com/overview) 和 [云市场](https://market.aliyun.com/apimarket/collection/57124001) 购买OCR服务，两个渠道购买的服务，其计费、消费明细账单、退款均各自独立，具体以实际购买页面为准。

| **操作** | **阿里云官网** | **云市场** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **操作** | **阿里云官网** | **云市场** |
| 开通 | 先开通再调用，每类识别服务需要单独 [开通](https://help.aliyun.com/zh/ocr/getting-started/use-process#4e7db41c583z8 "")。 | 无需开通， [购买资源包](https://help.aliyun.com/zh/ocr/support/billing-of-resource-plans-for-alibaba-cloud-marketplace "") 即可调用。 |
| 计费方式 | 按量付费、资源包抵扣。 | 资源包抵扣 |
| 扣费顺序 | 按顺序依次抵扣：免费额度 > 专用资源包 > 共享资源包 \> 按量后付费。 | 资源包抵扣 |
| 查看调用明细 | 通过控制台 [数据监控](https://ocr.console.aliyun.com/monitoring) 页面查看。 | 查看 [已购买服务](https://market.console.aliyun.com/#/?_k=5nsqxu)。 |
| 查看资源包余量 | 通过控制台 [服务列表](https://ocr.console.aliyun.com/overview) 查看。 | 查看 [资源包使用量](https://market.console.aliyun.com/#/?_k=5nsqxu)。 |
| 资源包管理与告警配置 | 通过控制台 [设置](https://ocr.console.aliyun.com/setup) 功能进行配置。 | 前往 [设置](https://market.console.aliyun.com/imageconsole/index.htm?spm=5176.23043878.0.0.72491cdcwRH8S9#/apiTools?_k=7m56b5)。 |
| 查看密钥信息 | 查看 [AccessKey](https://ram.console.aliyun.com/profile/access-keys)。 | 查看 [AppCode](https://market.console.aliyun.com/#/?_k=5nsqxu)。 |

## **计费类型**

**系统会按照如下顺序，依次抵扣：免费额度 > 专用资源包 > 共享资源包 \> 按量后付费**。

当免费额度用完后，如果存在有效且未耗尽的资源包，系统将优先抵扣资源包，直到有效资源包全部抵扣完，如此时仍在发生调用，则会自动进入后付费扣款。

### **免费额度**

开通OCR文字识别服务后，产品会赠送一定额度的 [免费调用量](https://help.aliyun.com/zh/ocr/product-overview/free-quota)，以便您评测OCR识别效果、接入联调，当发生API调用时，系统会优先使用免费额度。

- 识别类API：每个API每月赠送200次免费调用。

- 核验类API：每个账号累计赠送50次免费调用。


### **资源包（预付费）**

开通OCR文字识别服务后，可选择采购预付费 [资源包](https://help.aliyun.com/zh/ocr/product-overview/resource-plans)。当发生API调用后，系统会自动从已购买的资源包中，抵扣对应调用次数或点数。

预付费资源包，分为如下2类：

- **共享资源包**：该资源包可供多个API使用，推荐您优先采购共享资源包。

- **专用资源包**：该资源包仅可供指定API使用。


请注意：

- OCR统一识别服务（一个API可以识别59种证照/材料）仅支持共享资源包，不支持专用资源包。

- 预付费资源包的价格，相较按量付费（后付费）更优惠，推荐您预先采购预付费资源包。

- 资源包购买后有效期1年，请按需购买。


### **按量付费（后付费）**

开通OCR文字识别服务后，系统会默认为您开通按量后付费模式。

- 当您的账号产生API调用，且免费额度和资源包都消耗尽时，系统会按照本账号 **实际成功调用量\*后付费单价**，从阿里云账户里自动扣款。

- 按量付费单价为阶梯定价，即： **账号的自然月累计调用量越大，单价越便宜，** 详情参见 [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)。



**重要**





  - 开通OCR服务会自动开通后付费模式且不可关闭，用于保障您的服务平稳。请保证您的阿里云账户余额充足，以免账户欠费影响您的OCR业务。

  - **未发生成功调用，或产生了调用但未超过免费额度、资源包剩余额度时，均不会出现后付费扣款。**


- 系统 **每月1日会产生上月后付费账单**，您可以在账单内查看计费明细。


### **QPS叠加包**

开通OCR文字识别服务后，系统会默认为您提供每API 10 QPS 的并发。如果并发不能满足您的业务需求，可以通过购买 [QPS叠加包](https://help.aliyun.com/zh/ocr/product-overview/qps-resource-packages) 包进行扩容。

请注意：

- 身份证识别、全文识别高精版、通用文字识别：您可以通过直接购买开通。

- 其他API：请联系官方钉钉群【35208328】反馈需求。


## **计费示例**

### **资源包（预付费）**

假设某用户已经购买了某API 1000次专用资源包，且用户当月调用次数为5000次、系统赠送免费200次。

- 首先，扣除每月200次免费额度，计费调用4800次。

- 其次，从专用资源包抵扣1000个，抵扣后，专用资源包余额为0。剩余3800个调用未抵扣。

- 最后，用后付费方式扣款3800次。


### **按量付费（后付费）**

当月某用户调用身份证识别的总次数中，需 [付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go) 的调用量为 120200次，其中免费额度200次，费用计算如下：

| **付费阶梯** | **单价** | **当前阶梯次数** | **费用** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **付费阶梯** | **单价** | **当前阶梯次数** | **费用** |
| 0 < 月调用量 ≤ 1万 | 0.0825元/次 | 1万次 | 825元 |
| 1万 < 月调用量 ≤ 10万 | 0.0495元/次 | 9万次 | 4455元 |
| 10万 < 月调用量 ≤ 50万 | 0.0415元/次 | 2万次 | 830元 |

因此，本月调用该接口产生的费用为 200 x 0 + 10000 x 0.0825 + 90000 x 0.0495 + 20000 x 0.0415 = **6110元**

## **常见问题**

### **长图识别服务如何开通与计费？**

如您有长图识别需求，请通过官方钉钉群【35208328】联系技术支持。