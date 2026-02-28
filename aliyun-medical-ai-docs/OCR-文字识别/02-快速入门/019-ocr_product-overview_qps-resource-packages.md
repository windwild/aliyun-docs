### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[产品概述](https://help.aliyun.com/zh/ocr/product-overview/)[产品计费](https://help.aliyun.com/zh/ocr/product-overview/product-billing/)QPS叠加包

# QPS叠加包

更新时间：2024-12-02 04:03:40

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)[下一篇：OCR文档自学习计费](https://help.aliyun.com/zh/ocr/product-overview/billing-of-ocr-document-self-learning)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

什么是QPS

计费信息

本文为您介绍QPS叠加包计费信息。

## 什么是QPS

QPS（Query Per Second）是指，每秒钟请求或任务的数量，即QPS=并发数/平均响应时间。其中并发数是指，系统同时处理的请求或任务的数量。例如，若身份证识别接口平均响应时间为500ms，您拥有4个并发，则需要购买的QPS为4/0.5=8。如果您不想启动全部的并发，可根据实际业务需求套用公式。

## 计费信息

- 开通OCR文字识别API服务后，默认10QPS的并发，同时您也可购买QPS叠加包来提升API并发量。

- 当前支持QPS叠加包的API包括：身份证识别、通用文字识别、全文识别高精版。您可根据业务需求按天、按月、按年购买。

- 购买限制：叠加包10QPS起售，您每日最多可在线购买单接口100QPS，如需更多QPS，请提交工单或通过钉钉群：35208328联系我们。

- 生效日期：工作日当天12:00前购买，第二天00:00生效；其他时间购买，一个工作日后00:00生效。例如：

  - 周四12:00前购买，周五00:00生效；周四12:01购买，周六00:00生效。

  - 周五12:00前购买，周六00:00生效；周五12:01购买，周二00:00生效。

| 服务名称 | 购买QPS数量 | 按天购买 | 按月购买 | 按年购买 | 购买入口 |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 服务名称 | 购买QPS数量 | 按天购买 | 按月购买 | 按年购买 | 购买入口 |
| 通用文字识别 | 10<=QPS<50 | 23元/天/QPS | 260元/月/QPS | 2650元/年/QPS | [通用文字识别QPS叠加包](https://common-buy.aliyun.com/?commodityCode=ocr_qps_public_cn&request=%7B%22ord_time%22:%227:Day%22%2C%22number%22:10%2C%22API%22:%22RecognizeGeneral%22%7D) |
| 50<=QPS<=100 | 20元/天/QPS | 260元/月/QPS | 2450元/年/QPS |
| 全文识别高精版 | 10<=QPS<50 | 25元/天/QPS | 350元/月/QPS | 3600元/年/QPS | [全文识别高精版QPS叠加包](https://common-buy.aliyun.com/?commodityCode=ocr_qps_public_cn&request=%7B%22ord_time%22:%227:Day%22%2C%22number%22:10%2C%22API%22:%22RecognizeAdvanced%22%7D) |
| 50<=QPS<=100 | 23元/天/QPS | 350元/月/QPS | 3312元/年/QPS |
| 身份证识别 | 10<=QPS<50 | 25元/天/QPS | 350元/月/QPS | 3600元/年/QPS | [身份证识别QPS叠加包](https://common-buy.aliyun.com/?commodityCode=ocr_qps_public_cn&request=%7B%22ord_time%22:%227:Day%22%2C%22number%22:10%2C%22API%22:%22RecognizeIdcard%22%7D) |
| 50<=QPS<=100 | 23元/天/QPS | 350元/月/QPS | 3312元/年/QPS |