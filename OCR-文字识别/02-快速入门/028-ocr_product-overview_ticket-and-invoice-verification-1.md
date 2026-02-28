### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[产品概述](https://help.aliyun.com/zh/ocr/product-overview/)[产品简介](https://help.aliyun.com/zh/ocr/product-overview/product-introduction/)票证核验

# 票证核验

更新时间：2025-01-07 01:32:44

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：医疗场景识别](https://help.aliyun.com/zh/ocr/product-overview/medical-scenario-recognition-1)[下一篇：OCR文档自学习概述](https://help.aliyun.com/zh/ocr/product-overview/overview-of-ocr-document-self-learning)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

产品介绍

产品功能

营业执照核验

发票核验

应用场景

API快捷入口

本文介绍阿里云文字识别-票证核验系列相关产品的功能、特色优势及应用场景，并为您提供产品的API快捷入口。

## **产品介绍**

读光OCR票证核验产品提供针对发票及企业执照等各类票证单据的真伪核验能力。作为读光OCR票据凭证识别、企业资质识别的能力补充，票证核验不提供内容识别功能，仅支持输入要求字段后返回真伪核验结果。

**说明**

开通可享50次免费额度： [https://ocr.console.aliyun.com/overview](https://ocr.console.aliyun.com/overview)

购买地址： [https://common-buy.aliyun.com/?commodityCode=ocr\_cardverification\_dp\_cn](https://common-buy.aliyun.com/?commodityCode=ocr_cardverification_dp_cn)

## **产品功能**

### **营业执照核验**

读光OCR营业执照核验提供营业执照的验真能力（不含营业执照识别功能）。输入企业全称、统一社会信用代码、法定代表人姓名三要素信息进行验证，返回对应的核验结果。

**说明**

如遇数字或特殊符号，请认真核对信息为半角/全角格式。

![营业执照核验final](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5179819661/p521814.png)

### **发票核验**

读光OCR发票核验提供各类发票的验真能力（不含发票识别功能）。发票核验接口支持包括：增值税专用发票、增值税普通发票（折叠票）、增值税普通发票（卷票）、增值税电子普通发票（含收费公路通行费增值税电子普通发票）、机动车销售统一发票、二手车销售统一发票多种类型发票核验。您可以通过输入发票的关键验证字段，返回真实的票面信息，包括发票类型、发票代码、发票号码、作废标志、开票日期、购方税号及其他发票信息等。当天开具发票当日可查验（T+0）。注意：可能有几小时到十几小时的延迟。

**说明**

如遇数字或特殊符号，请认真核对信息为半角/全角格式。

![发票核验final](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5179819661/p521815.png)

## **应用场景**

- 适用于企业费控报销场景，通过票面信息核验，提高费控报销审核效率。

- 适用于供应商信息管理场景，通过企业执照、发票信息审核，提高电商、零售、O2O等行业对合作伙伴的管理效率。


## **API快捷入口**

|     |     |
| --- | --- |
| 云市场API快捷入口（旧） | 官网API快捷入口（新） |
| 营业执照核验 | [VerifyBusinessLicense](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-verifybusinesslicense) |
| 发票核验 | [VerifyVATInvoice](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-verifyvatinvoice) |