### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[服务支持](https://help.aliyun.com/zh/ocr/support/)[常见问题](https://help.aliyun.com/zh/ocr/support/faq/)产品功能相关

# 产品功能相关

更新时间：2024-10-11 06:09:12

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：计量计费相关](https://help.aliyun.com/zh/ocr/support/billing-faq)[下一篇：账号与安全相关](https://help.aliyun.com/zh/ocr/support/faq-about-accounts-and-security)

该文章对您有帮助吗？

反馈

本章节介绍阿里云文字识别（OCR) 关于产品功能、产品性能、系统逻辑等常见问题与解答。

### OCR能否提供100%识别准确率？

OCR识别准确率与上传的图片质量相关，同时也存在一定概率的误差，无法做到100%识别准确率。如您对当前使用的OCR产品服务有识别准确率相关问题，您可 [联系我们](https://help.aliyun.com/zh/ocr/support/contact-us#9339f26054yfr "")；

### 对图片的格式大小有怎样的要求？

阿里云文字识别服务要求单张图片大小不超过10M, 图片最长边不超过8192像素，最短边不小于15像素，当长边超过1024像素时，长宽比不超过1:50； 若对响应时长有较高要求的客户，图片大小建议控制在1.5M以内，并且通过传图片链接调用接口。

图片像素大小没有具体要求，单字大小在10-50像素内，识别效果比较好；尽量选择图像清晰度高、无反光的图片。若图片有旋转角度，算法有自动修正功能。具体的识别率与具体图片质量有较大关系。有关支持文件类型可参考 [支持文件类型说明](https://help.aliyun.com/zh/ocr/product-overview/supported-file-types "") 文档；

### 能够识别复印件吗？

目前身份证，银行卡，营业执照三个接口可以判断是否为复印件，但是无法判断真伪（是否PS）；其他证件若有特殊需求可单独加入钉钉答疑群35208328进行需求沟通；

### 哪些接口可以识别多种类图片？

通常情况下阿里云文字识别提供的接口仅支持单张图片的识别，若需要对多种类型图片识别可参考如下产品：

混贴发票识别，可支持一张图片上有多张混贴图的场景，系统可自动进行分区、分类与结构化识别。体验地址为 [OCR读光体验中心](https://duguang.aliyun.com/experience?type=bill&subtype=multi_invoice#intro)。

![混贴发票](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6900090661/p479236.png)

### 房产证支持哪几种房产证类型？

OCR官网不动产权证兼容“不动产证”和“房产证”两类证件，能够适用于全国各地的不同不动产证以及房地权证识别，详情可至 [读光](https://duguang.aliyun.com/experience?type=standard&subtype=estate_cert#intro) 体验；

### QPS不够用怎么办？

官网为单个账号提供10QPS的默认流量，最高支持10个并发同时请求。建议您在程序中可以进行一定的请求限制，避免收到大量限流报错（Throttling.User）。需要注意的是，如果您的程序在OCR识别失败时有重试机制，当OCR接口返回Throttling.User错误码时，请不要重试，否则可能加重限流报错情况。更多错误码，详见 [错误码文档](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-errorcodes)；

同时，阿里云官网已上线QPS叠加包服务，您可通过购买QPS叠加包进行容量扩充，可至 [OCR控制台](https://ocr.console.aliyun.com/overview) 购买。

### OCR接口支持哪些格式？

读光OCR识别接口均支持图片格式数据，包括：png/.jpg/.jpeg/.jpe/.bmp/.gif/.tiff/.tif/.webp，部分接口支持单页PDF，PDF大小不超过10M，详情可见 [支持文件类型说明](https://help.aliyun.com/zh/ocr/product-overview/supported-file-types "")；如需识别更多格式文件，请 [联系我们](https://help.aliyun.com/zh/ocr/support/contact-us "")；

### OCR服务已购买资源包为何还是未开通状态？

您需要 [开通](https://ocr.console.aliyun.com/overview) 文字识别OCR后付费服务才可以使用OCR服务，后付费服务开通后会优先抵扣资源包，资源包消耗完后会默认采用后付费计费方式，具体可见 [计费概述](https://help.aliyun.com/zh/ocr/product-overview/billing-overview "")；

### OCR服务是否支持离线识别？

印刷文字识别OCR支持离线SDK售卖，当前已有离线识别SDK包括：身份证识别、银行卡、物流面单识别、扫读识别、指尖点读离线SDK等，售卖地址可见 [OCR云市场服务中心](https://market.aliyun.com/store/1334330.html?spm=5176.product-detail.market-shop.1.601946a0wGf58P#/list?keywords=SDK)；如您有更多需求，也可 [联系我们](https://help.aliyun.com/zh/ocr/support/contact-us#9339f26054yfr "")；

**重要**

离线sdk现暂不提供支持，如有变动，将于此处更新。

### OCR服务是否支持私有化部署？

印刷文字识别OCR支持专有云、混合云的私有化部署，您可 [联系我们](https://help.aliyun.com/zh/ocr/support/contact-us#9339f26054yfr "") 沟通私有化部署相关合作；

### OCR服务是否支持境外部署？

印刷文字识别OCR服务暂不支持境外服务器，如有需求可 [联系我们](https://help.aliyun.com/zh/ocr/support/contact-us#9339f26054yfr "")。