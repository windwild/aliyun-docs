支持包括发票代码、开票号码、开票日期、发票金额、增值税税额、合格证号、购买方名称、购买方身份证号/代码等关键字段结构化识别输出。

## 接口说明

#### 本接口适用场景

- 阿里云机动车销售发票识别，是阿里云官方自研 OCR 文字识别产品，适用于识别购车发票上的发票金额、购买方名称、车辆类型、厂牌型号、销售方名称等关键信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/tfs/TB1k5AyamslXu8jSZFuXXXg7FXa-2060-1000.jpg)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |

| 分类 | 概述 |
| --- | --- |
| 图片格式 | 支持 PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。 |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 总体识别准确率可达 98%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [票据凭证识别](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=bill&subtype=car_invoice#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [机动车销售发票识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_invoice_dp_cn_20211103182712_0430%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCarInvoice?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

* * *

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 相关能力 | - [云市场机动车销售发票识别。](https://market.aliyun.com/products/57124001/cmapi029811.html?spm=a2c4g.11186623.0.0.6dcb4dcdaoX2WN#sku=yuncode2381100001) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCarInvoice)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCarInvoice)

## 授权信息

下表是API对应的授权信息，可以在RAM权限策略语句的`Action`元素中使用，用来给RAM用户或RAM角色授予调用此API的权限。具体说明如下：

- 操作：是指具体的权限点。
- 访问级别：是指每个操作的访问级别，取值为写入（Write）、读取（Read）或列出（List）。
- 资源类型：是指操作中支持授权的资源类型。具体说明如下：
  - 对于必选的资源类型，用前面加 \\* 表示。
  - 对于不支持资源级授权的操作，用`全部资源`表示。
- 条件关键字：是指云产品自身定义的条件关键字。
- 关联操作：是指成功执行操作所需要的其他权限。操作者必须同时具备关联操作的权限，操作才能成功。

| 操作 | 访问级别 | 资源类型 | 条件关键字 | 关联操作 |
| --- | --- | --- | --- | --- |

| 操作 | 访问级别 | 资源类型 | 条件关键字 | 关联操作 |
| --- | --- | --- | --- | --- |
| ocr:RecognizeCarInvoice |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/tfs/TB1hC7bXCzqK1RjSZPcXXbTepXa-832-616.jpg |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {<br> "data": {<br> "taxCode": "0492725/\*+0/法55337\*<56-24/\*184-/\*<94 16-6+9\*-897+98546/<>74\*++16<43800\*>+-< 116\*丰1<4201/\*18+-/</56-7不5<+8-3839263 +5/+-0/48<<336/30983/96550\*8<+75326252 728\*3+\*032\*9\*9\*900430086-956347/250+",<br> "invoiceDate": "2017-12-28",<br> "invoiceCode": "141001720076",<br> "invoiceNumber": "00357144",<br> "machineCode": "661403540093",<br> "purchaserName": "国军",<br> "purchaseCode": "41052319206046072",<br> "vehicleType": "轿车",<br> "brandMode": "FV7152BAMBG",<br> "origin": "长春市",<br> "certificateNumber": "WAB011715201804",<br> "importCertificateNumber": "",<br> "commodityInspectionNumber": "",<br> "engineNumber": "144878",<br> "vinCode": "LFV2A1151H3201804",<br> "invoiceAmountCn": "99000",<br> "invoiceAmount": "99000.00",<br> "sellerName": "安阳市汽车销售服务有限公司",<br> "sellerContact": "0372-5378818",<br> "sellerTaxNumber": "914105001924458113",<br> "sellerBankAccount": "41001501210050224848",<br> "sellerAddress": "安阳市文峰区光专路商段路(汽车市场对面)"，<br> "sellerDepositaryBank": "中国建设银行安阳分行",<br> "taxRate": "17%",<br> "tax": "14384.62",<br> "taxAuthoritiesInfo": "安阳县国家税务局341052200",<br> "taxAuthoritiesName": "安阳县国家税务局",<br> "taxAuthoritiesCode": "341052200",<br> "preTaxAmount": "84615.38",<br> "passengerLimitNumber": "5",<br> "issuer": "赵迪",<br> "tonnage": "",<br> "purchaserTaxNumber": "410523197206046072",<br> "taxPaymentNumber": ""<br> },<br> "height": 616,<br> "orgHeight": 616,<br> "orgWidth": 832,<br> "prism\_keyValueInfo": \[<br> {<br> "key": "taxCode",<br> "keyProb": 94,<br> "value": "0492725/\*+0/法55337\*<56-24/\*184-/\*<94 16-6+9\*-897+98546/<>74\*++16<43800\*>+-< 116\*丰1<4201/\*18+-/</56-7不5<+8-3839263 +5/+-0/48<<336/30983/96550\*8<+75326252 728\*3+\*032\*9\*9\*900430086-956347/250+",<br> "valuePos": \[<br> {<br> "x": 744,<br> "y": 131<br> },<br> {<br> "x": 744,<br> "y": 210<br> },<br> {<br> "x": 412,<br> "y": 210<br> },<br> {<br> "x": 412,<br> "y": 131<br> }<br> \],<br> "valueProb": 96<br> },<br> {<br> "key": "invoiceDate",<br> "keyProb": 100,<br> "value": "2017-12-28",<br> "valuePos": \[<br> {<br> "x": 233,<br> "y": 98<br> },<br> {<br> "x": 233,<br> "y": 112<br> },<br> {<br> "x": 142,<br> "y": 112<br> },<br> {<br> "x": 142,<br> "y": 98<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "invoiceCode",<br> "keyProb": 100,<br> "value": "141001720076",<br> "valuePos": \[<br> {<br> "x": 764,<br> "y": 72<br> },<br> {<br> "x": 764,<br> "y": 88<br> },<br> {<br> "x": 647,<br> "y": 88<br> },<br> {<br> "x": 647,<br> "y": 72<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "invoiceNumber",<br> "keyProb": 100,<br> "value": "00357144",<br> "valuePos": \[<br> {<br> "x": 728,<br> "y": 92<br> },<br> {<br> "x": 728,<br> "y": 108<br> },<br> {<br> "x": 647,<br> "y": 108<br> },<br> {<br> "x": 647,<br> "y": 92<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "machineCode",<br> "keyProb": 100,<br> "value": "661403540093",<br> "valuePos": \[<br> {<br> "x": 288,<br> "y": 188<br> },<br> {<br> "x": 288,<br> "y": 202<br> },<br> {<br> "x": 176,<br> "y": 202<br> },<br> {<br> "x": 176,<br> "y": 188<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "purchaserName",<br> "keyProb": 100,<br> "value": "国军",<br> "valuePos": \[<br> {<br> "x": 214,<br> "y": 228<br> },<br> {<br> "x": 214,<br> "y": 243<br> },<br> {<br> "x": 185,<br> "y": 243<br> },<br> {<br> "x": 185,<br> "y": 228<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "purchaseCode",<br> "keyProb": 99,<br> "value": "41052319206046072",<br> "valuePos": \[<br> {<br> "x": 326,<br> "y": 249<br> },<br> {<br> "x": 326,<br> "y": 262<br> },<br> {<br> "x": 176,<br> "y": 262<br> },<br> {<br> "x": 176,<br> "y": 249<br> }<br> \],<br> "valueProb": 99<br> },<br> {<br> "key": "vehicleType",<br> "keyProb": 100,<br> "value": "轿车",<br> "valuePos": \[<br> {<br> "x": 202,<br> "y": 276<br> },<br> {<br> "x": 202,<br> "y": 291<br> },<br> {<br> "x": 175,<br> "y": 291<br> },<br> {<br> "x": 175,<br> "y": 276<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "brandMode",<br> "keyProb": 99,<br> "value": "FV7152BAMBG",<br> "valuePos": \[<br> {<br> "x": 457,<br> "y": 278<br> },<br> {<br> "x": 457,<br> "y": 291<br> },<br> {<br> "x": 383,<br> "y": 291<br> },<br> {<br> "x": 383,<br> "y": 278<br> }<br> \],<br> "valueProb": 99<br> },<br> {<br> "key": "origin",<br> "keyProb": 100,<br> "value": "长春市",<br> "valuePos": \[<br> {<br> "x": 698,<br> "y": 277<br> },<br> {<br> "x": 698,<br> "y": 293<br> },<br> {<br> "x": 661,<br> "y": 293<br> },<br> {<br> "x": 661,<br> "y": 277<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "certificateNumber",<br> "keyProb": 100,<br> "value": "WAB011715201804",<br> "valuePos": \[<br> {<br> "x": 270,<br> "y": 311<br> },<br> {<br> "x": 270,<br> "y": 323<br> },<br> {<br> "x": 174,<br> "y": 323<br> },<br> {<br> "x": 174,<br> "y": 311<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "importCertificateNumber",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> },<br> {<br> "key": "commodityInspectionNumber",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> },<br> {<br> "key": "engineNumber",<br> "keyProb": 100,<br> "value": "144878",<br> "valuePos": \[<br> {<br> "x": 215,<br> "y": 344<br> },<br> {<br> "x": 215,<br> "y": 356<br> },<br> {<br> "x": 175,<br> "y": 356<br> },<br> {<br> "x": 175,<br> "y": 344<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "vinCode",<br> "keyProb": 97,<br> "value": "LFV2A1151H3201804",<br> "valuePos": \[<br> {<br> "x": 708,<br> "y": 345<br> },<br> {<br> "x": 708,<br> "y": 359<br> },<br> {<br> "x": 551,<br> "y": 359<br> },<br> {<br> "x": 551,<br> "y": 345<br> }<br> \],<br> "valueProb": 97<br> },<br> {<br> "key": "invoiceAmountCn",<br> "keyProb": 100,<br> "value": "99000",<br> "valuePos": \[<br> {<br> "x": 270,<br> "y": 373<br> },<br> {<br> "x": 270,<br> "y": 388<br> },<br> {<br> "x": 193,<br> "y": 388<br> },<br> {<br> "x": 193,<br> "y": 373<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "invoiceAmount",<br> "keyProb": 100,<br> "value": "99000.00",<br> "valuePos": \[<br> {<br> "x": 631,<br> "y": 388<br> },<br> {<br> "x": 632,<br> "y": 374<br> },<br> {<br> "x": 722,<br> "y": 375<br> },<br> {<br> "x": 722,<br> "y": 390<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "sellerName",<br> "keyProb": 100,<br> "value": "安阳市汽车销售服务有限公司",<br> "valuePos": \[<br> {<br> "x": 363,<br> "y": 406<br> },<br> {<br> "x": 363,<br> "y": 421<br> },<br> {<br> "x": 176,<br> "y": 421<br> },<br> {<br> "x": 176,<br> "y": 406<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "sellerContact",<br> "keyProb": 100,<br> "value": "0372-5378818",<br> "valuePos": \[<br> {<br> "x": 647,<br> "y": 408<br> },<br> {<br> "x": 647,<br> "y": 421<br> },<br> {<br> "x": 570,<br> "y": 421<br> },<br> {<br> "x": 570,<br> "y": 408<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "sellerTaxNumber",<br> "keyProb": 96,<br> "value": "914105001924458113",<br> "valuePos": \[<br> {<br> "x": 363,<br> "y": 436<br> },<br> {<br> "x": 363,<br> "y": 452<br> },<br> {<br> "x": 176,<br> "y": 454<br> },<br> {<br> "x": 175,<br> "y": 438<br> }<br> \],<br> "valueProb": 96<br> },<br> {<br> "key": "sellerBankAccount",<br> "keyProb": 100,<br> "value": "41001501210050224848",<br> "valuePos": \[<br> {<br> "x": 696,<br> "y": 441<br> },<br> {<br> "x": 696,<br> "y": 454<br> },<br> {<br> "x": 569,<br> "y": 454<br> },<br> {<br> "x": 569,<br> "y": 441<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "sellerAddress",<br> "keyProb": 80,<br> "value": "安阳市文峰区光专路商段路(汽车市场对面)", "valuePos": \[<br> {<br> "x": 175,<br> "y": 473<br> },<br> {<br> "x": 403,<br> "y": 472<br> },<br> {<br> "x": 403,<br> "y": 484<br> },<br> {<br> "x": 176,<br> "y": 486<br> }<br> \],<br> "valueProb": 80<br> },<br> {<br> "key": "sellerDepositaryBank",<br> "keyProb": 100,<br> "value": "中国建设银行安阳分行",<br> "valuePos": \[<br> {<br> "x": 632,<br> "y": 471<br> },<br> {<br> "x": 632,<br> "y": 485<br> },<br> {<br> "x": 506,<br> "y": 487<br> },<br> {<br> "x": 505,<br> "y": 472<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "taxRate",<br> "keyProb": 99,<br> "value": "17%",<br> "valuePos": \[<br> {<br> "x": 203,<br> "y": 510<br> },<br> {<br> "x": 203,<br> "y": 524<br> },<br> {<br> "x": 176,<br> "y": 524<br> },<br> {<br> "x": 176,<br> "y": 510<br> }<br> \],<br> "valueProb": 99<br> },<br> {<br> "key": "tax",<br> "keyProb": 100,<br> "value": "14384.62",<br> "valuePos": \[<br> {<br> "x": 413,<br> "y": 509<br> },<br> {<br> "x": 413,<br> "y": 524<br> },<br> {<br> "x": 323,<br> "y": 524<br> },<br> {<br> "x": 323,<br> "y": 509<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "taxAuthoritiesInfo",<br> "keyProb": 100,<br> "value": "安阳县国家税务局341052200",<br> "valuePos": \[<br> {<br> "x": 633,<br> "y": 498<br> },<br> {<br> "x": 633,<br> "y": 525<br> },<br> {<br> "x": 537,<br> "y": 525<br> },<br> {<br> "x": 537,<br> "y": 498<br> }<br> \],<br> "valueProb": 99<br> },<br> {<br> "key": "taxAuthoritiesName",<br> "keyProb": 100,<br> "value": "安阳县国家税务局",<br> "valuePos": \[<br> {<br> "x": 633,<br> "y": 498<br> },<br> {<br> "x": 633,<br> "y": 525<br> },<br> {<br> "x": 537,<br> "y": 525<br> },<br> {<br> "x": 537,<br> "y": 498<br> }<br> \],<br> "valueProb": 99<br> },<br> {<br> "key": "taxAuthoritiesCode",<br> "keyProb": 100,<br> "value": "341052200",<br> "valuePos": \[<br> {<br> "x": 633,<br> "y": 498<br> },<br> {<br> "x": 633,<br> "y": 525<br> },<br> {<br> "x": 537,<br> "y": 525<br> },<br> {<br> "x": 537,<br> "y": 498<br> }<br> \],<br> "valueProb": 99<br> },<br> {<br> "key": "preTaxAmount",<br> "keyProb": 97,<br> "value": "84615.38",<br> "valuePos": \[<br> {<br> "x": 216,<br> "y": 557<br> },<br> {<br> "x": 216,<br> "y": 543<br> },<br> {<br> "x": 305,<br> "y": 544<br> },<br> {<br> "x": 305,<br> "y": 559<br> }<br> \],<br> "valueProb": 97<br> },<br> {<br> "key": "passengerLimitNumber",<br> "keyProb": 100,<br> "value": "5",<br> "valuePos": \[<br> {<br> "x": 723,<br> "y": 545<br> },<br> {<br> "x": 723,<br> "y": 557<br> },<br> {<br> "x": 714,<br> "y": 557<br> },<br> {<br> "x": 714,<br> "y": 545<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "issuer",<br> "keyProb": 100,<br> "value": "赵迪",<br> "valuePos": \[<br> {<br> "x": 437,<br> "y": 573<br> },<br> {<br> "x": 437,<br> "y": 588<br> },<br> {<br> "x": 410,<br> "y": 588<br> },<br> {<br> "x": 410,<br> "y": 573<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "tonnage",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> },<br> {<br> "key": "purchaserTaxNumber",<br> "keyProb": 100,<br> "value": "410523197206046072",<br> "valuePos": \[<br> {<br> "x": 730,<br> "y": 240<br> },<br> {<br> "x": 730,<br> "y": 253<br> },<br> {<br> "x": 569,<br> "y": 253<br> },<br> {<br> "x": 569,<br> "y": 240<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "taxPaymentNumber",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> }<br> \],<br> "width": 832<br>} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| sliceRect | list | 检测出的子图坐标信息。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
| ftype | int | 是否为复印件（1：是，0：否）。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 识别结果（data 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| taxCode | string | 税控码。 |
| invoiceDate | string | 开票日期。 |
| invoiceCode | string | 发票代码。 |
| invoiceNumber | string | 发票号码。 |
| machineCode | string | 机器编号。 |
| purchaserName | string | 购买方名称。 |
| purchaseCode | string | 购买方身份证号码/组织机构代码。 |
| vehicleType | string | 车辆类型。 |
| brandMode | string | 厂牌型号。 |
| origin | string | 产地。 |
| certificateNumber | string | 合格证号。 |
| importCertificateNumber | string | 进口证明书号。 |
| commodityInspectionNumber | string | 商检单号。 |
| engineNumber | string | 发动机号码。 |
| vinCode | string | 车辆识别代号/车架号码。 |
| invoiceAmountCn | string | 价税合计（大写）。 |
| invoiceAmount | string | 价税合计（小写）。 |
| sellerName | string | 销货单位名称。 |
| sellerContact | string | 销货单位电话。 |
| sellerTaxNumber | string | 销货单位纳税人识别号。 |
| sellerBankAccount | string | 销货单位账号。 |
| sellerAddress | string | 销货单位地址。 |
| sellerDepositaryBank | string | 销货单位开户银行。 |
| taxRate | string | 增值税税率或征收率。 |
| tax | string | 增值税税额。 |
| taxAuthoritiesInfo | string | 主管税务机关及代码。 |
| taxAuthoritiesName | string | 主管税务机关。 |
| taxAuthoritiesCode | string | 主管税务代码。 |
| preTaxAmount | string | 不含税价。 |
| passengerLimitNumber | string | 限乘人数。 |
| issuer | string | 开票人。 |
| tonnage | string | 吨位。 |
| purchaserTaxNumber | string | 购买方纳税人识别号。 |
| taxPaymentNumber | string | 完税凭证号码。 |

#### 结构化坐标信息（prism\_keyValueInfo 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| key | string | 识别出的字段名称。 |
| keyProb | int | 字段名称置信度。 |
| value | string | 识别出的字段名称对应的值。 |
| valueProb | int | 字段名称对应值的置信度。 |
| valuePos | list | 字段在原图中的四个点坐标（左上、右上、右下、左下）。 |

## 示例

正常返回示例

`JSON`格式

```swift
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": "{\n      \"data\": {\n            \"taxCode\": \"0492725/*+0/法55337*<56-24/*184-/*<94 16-6+9*-897+98546/<>74*++16<43800*>+-< 116*丰1<4201/*18+-/</56-7不5<+8-3839263 +5/+-0/48<<336/30983/96550*8<+75326252 728*3+*032*9*9*900430086-956347/250+\",\n            \"invoiceDate\": \"2017-12-28\",\n            \"invoiceCode\": \"141001720076\",\n            \"invoiceNumber\": \"00357144\",\n            \"machineCode\": \"661403540093\",\n            \"purchaserName\": \"国军\",\n            \"purchaseCode\": \"41052319206046072\",\n            \"vehicleType\": \"轿车\",\n            \"brandMode\": \"FV7152BAMBG\",\n            \"origin\": \"长春市\",\n            \"certificateNumber\": \"WAB011715201804\",\n            \"importCertificateNumber\": \"\",\n            \"commodityInspectionNumber\": \"\",\n            \"engineNumber\": \"144878\",\n            \"vinCode\": \"LFV2A1151H3201804\",\n            \"invoiceAmountCn\": \"99000\",\n            \"invoiceAmount\": \"99000.00\",\n            \"sellerName\": \"安阳市汽车销售服务有限公司\",\n            \"sellerContact\": \"0372-5378818\",\n            \"sellerTaxNumber\": \"914105001924458113\",\n            \"sellerBankAccount\": \"41001501210050224848\",\n            \"sellerAddress\": \"安阳市文峰区光专路商段路(汽车市场对面)\"，\n            \"sellerDepositaryBank\": \"中国建设银行安阳分行\",\n            \"taxRate\": \"17%\",\n            \"tax\": \"14384.62\",\n            \"taxAuthoritiesInfo\": \"安阳县国家税务局341052200\",\n            \"taxAuthoritiesName\": \"安阳县国家税务局\",\n            \"taxAuthoritiesCode\": \"341052200\",\n            \"preTaxAmount\": \"84615.38\",\n            \"passengerLimitNumber\": \"5\",\n            \"issuer\": \"赵迪\",\n            \"tonnage\": \"\",\n            \"purchaserTaxNumber\": \"410523197206046072\",\n            \"taxPaymentNumber\": \"\"\n      },\n      \"height\": 616,\n      \"orgHeight\": 616,\n      \"orgWidth\": 832,\n      \"prism_keyValueInfo\": [\n            {\n                  \"key\": \"taxCode\",\n                  \"keyProb\": 94,\n                  \"value\": \"0492725/*+0/法55337*<56-24/*184-/*<94 16-6+9*-897+98546/<>74*++16<43800*>+-< 116*丰1<4201/*18+-/</56-7不5<+8-3839263 +5/+-0/48<<336/30983/96550*8<+75326252 728*3+*032*9*9*900430086-956347/250+\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 744,\n                              \"y\": 131\n                        },\n                        {\n                              \"x\": 744,\n                              \"y\": 210\n                        },\n                        {\n                              \"x\": 412,\n                              \"y\": 210\n                        },\n                        {\n                              \"x\": 412,\n                              \"y\": 131\n                        }\n                  ],\n                  \"valueProb\": 96\n            },\n            {\n                  \"key\": \"invoiceDate\",\n                  \"keyProb\": 100,\n                  \"value\": \"2017-12-28\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 233,\n                              \"y\": 98\n                        },\n                        {\n                              \"x\": 233,\n                              \"y\": 112\n                        },\n                        {\n                              \"x\": 142,\n                              \"y\": 112\n                        },\n                        {\n                              \"x\": 142,\n                              \"y\": 98\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"invoiceCode\",\n                  \"keyProb\": 100,\n                  \"value\": \"141001720076\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 764,\n                              \"y\": 72\n                        },\n                        {\n                              \"x\": 764,\n                              \"y\": 88\n                        },\n                        {\n                              \"x\": 647,\n                              \"y\": 88\n                        },\n                        {\n                              \"x\": 647,\n                              \"y\": 72\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"invoiceNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"00357144\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 728,\n                              \"y\": 92\n                        },\n                        {\n                              \"x\": 728,\n                              \"y\": 108\n                        },\n                        {\n                              \"x\": 647,\n                              \"y\": 108\n                        },\n                        {\n                              \"x\": 647,\n                              \"y\": 92\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"machineCode\",\n                  \"keyProb\": 100,\n                  \"value\": \"661403540093\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 288,\n                              \"y\": 188\n                        },\n                        {\n                              \"x\": 288,\n                              \"y\": 202\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 202\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 188\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"purchaserName\",\n                  \"keyProb\": 100,\n                  \"value\": \"国军\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 214,\n                              \"y\": 228\n                        },\n                        {\n                              \"x\": 214,\n                              \"y\": 243\n                        },\n                        {\n                              \"x\": 185,\n                              \"y\": 243\n                        },\n                        {\n                              \"x\": 185,\n                              \"y\": 228\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"purchaseCode\",\n                  \"keyProb\": 99,\n                  \"value\": \"41052319206046072\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 326,\n                              \"y\": 249\n                        },\n                        {\n                              \"x\": 326,\n                              \"y\": 262\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 262\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 249\n                        }\n                  ],\n                  \"valueProb\": 99\n            },\n            {\n                  \"key\": \"vehicleType\",\n                  \"keyProb\": 100,\n                  \"value\": \"轿车\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 202,\n                              \"y\": 276\n                        },\n                        {\n                              \"x\": 202,\n                              \"y\": 291\n                        },\n                        {\n                              \"x\": 175,\n                              \"y\": 291\n                        },\n                        {\n                              \"x\": 175,\n                              \"y\": 276\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"brandMode\",\n                  \"keyProb\": 99,\n                  \"value\": \"FV7152BAMBG\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 457,\n                              \"y\": 278\n                        },\n                        {\n                              \"x\": 457,\n                              \"y\": 291\n                        },\n                        {\n                              \"x\": 383,\n                              \"y\": 291\n                        },\n                        {\n                              \"x\": 383,\n                              \"y\": 278\n                        }\n                  ],\n                  \"valueProb\": 99\n            },\n            {\n                  \"key\": \"origin\",\n                  \"keyProb\": 100,\n                  \"value\": \"长春市\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 698,\n                              \"y\": 277\n                        },\n                        {\n                              \"x\": 698,\n                              \"y\": 293\n                        },\n                        {\n                              \"x\": 661,\n                              \"y\": 293\n                        },\n                        {\n                              \"x\": 661,\n                              \"y\": 277\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"certificateNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"WAB011715201804\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 270,\n                              \"y\": 311\n                        },\n                        {\n                              \"x\": 270,\n                              \"y\": 323\n                        },\n                        {\n                              \"x\": 174,\n                              \"y\": 323\n                        },\n                        {\n                              \"x\": 174,\n                              \"y\": 311\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"importCertificateNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"\",\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"commodityInspectionNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"\",\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"engineNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"144878\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 215,\n                              \"y\": 344\n                        },\n                        {\n                              \"x\": 215,\n                              \"y\": 356\n                        },\n                        {\n                              \"x\": 175,\n                              \"y\": 356\n                        },\n                        {\n                              \"x\": 175,\n                              \"y\": 344\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"vinCode\",\n                  \"keyProb\": 97,\n                  \"value\": \"LFV2A1151H3201804\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 708,\n                              \"y\": 345\n                        },\n                        {\n                              \"x\": 708,\n                              \"y\": 359\n                        },\n                        {\n                              \"x\": 551,\n                              \"y\": 359\n                        },\n                        {\n                              \"x\": 551,\n                              \"y\": 345\n                        }\n                  ],\n                  \"valueProb\": 97\n            },\n            {\n                  \"key\": \"invoiceAmountCn\",\n                  \"keyProb\": 100,\n                  \"value\": \"99000\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 270,\n                              \"y\": 373\n                        },\n                        {\n                              \"x\": 270,\n                              \"y\": 388\n                        },\n                        {\n                              \"x\": 193,\n                              \"y\": 388\n                        },\n                        {\n                              \"x\": 193,\n                              \"y\": 373\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"invoiceAmount\",\n                  \"keyProb\": 100,\n                  \"value\": \"99000.00\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 631,\n                              \"y\": 388\n                        },\n                        {\n                              \"x\": 632,\n                              \"y\": 374\n                        },\n                        {\n                              \"x\": 722,\n                              \"y\": 375\n                        },\n                        {\n                              \"x\": 722,\n                              \"y\": 390\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"sellerName\",\n                  \"keyProb\": 100,\n                  \"value\": \"安阳市汽车销售服务有限公司\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 363,\n                              \"y\": 406\n                        },\n                        {\n                              \"x\": 363,\n                              \"y\": 421\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 421\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 406\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"sellerContact\",\n                  \"keyProb\": 100,\n                  \"value\": \"0372-5378818\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 647,\n                              \"y\": 408\n                        },\n                        {\n                              \"x\": 647,\n                              \"y\": 421\n                        },\n                        {\n                              \"x\": 570,\n                              \"y\": 421\n                        },\n                        {\n                              \"x\": 570,\n                              \"y\": 408\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"sellerTaxNumber\",\n                  \"keyProb\": 96,\n                  \"value\": \"914105001924458113\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 363,\n                              \"y\": 436\n                        },\n                        {\n                              \"x\": 363,\n                              \"y\": 452\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 454\n                        },\n                        {\n                              \"x\": 175,\n                              \"y\": 438\n                        }\n                  ],\n                  \"valueProb\": 96\n            },\n            {\n                  \"key\": \"sellerBankAccount\",\n                  \"keyProb\": 100,\n                  \"value\": \"41001501210050224848\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 696,\n                              \"y\": 441\n                        },\n                        {\n                              \"x\": 696,\n                              \"y\": 454\n                        },\n                        {\n                              \"x\": 569,\n                              \"y\": 454\n                        },\n                        {\n                              \"x\": 569,\n                              \"y\": 441\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"sellerAddress\",\n                  \"keyProb\": 80,\n                  \"value\": \"安阳市文峰区光专路商段路(汽车市场对面)\",                   \"valuePos\": [\n                        {\n                              \"x\": 175,\n                              \"y\": 473\n                        },\n                        {\n                              \"x\": 403,\n                              \"y\": 472\n                        },\n                        {\n                              \"x\": 403,\n                              \"y\": 484\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 486\n                        }\n                  ],\n                  \"valueProb\": 80\n            },\n            {\n                  \"key\": \"sellerDepositaryBank\",\n                  \"keyProb\": 100,\n                  \"value\": \"中国建设银行安阳分行\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 632,\n                              \"y\": 471\n                        },\n                        {\n                              \"x\": 632,\n                              \"y\": 485\n                        },\n                        {\n                              \"x\": 506,\n                              \"y\": 487\n                        },\n                        {\n                              \"x\": 505,\n                              \"y\": 472\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"taxRate\",\n                  \"keyProb\": 99,\n                  \"value\": \"17%\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 203,\n                              \"y\": 510\n                        },\n                        {\n                              \"x\": 203,\n                              \"y\": 524\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 524\n                        },\n                        {\n                              \"x\": 176,\n                              \"y\": 510\n                        }\n                  ],\n                  \"valueProb\": 99\n            },\n            {\n                  \"key\": \"tax\",\n                  \"keyProb\": 100,\n                  \"value\": \"14384.62\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 413,\n                              \"y\": 509\n                        },\n                        {\n                              \"x\": 413,\n                              \"y\": 524\n                        },\n                        {\n                              \"x\": 323,\n                              \"y\": 524\n                        },\n                        {\n                              \"x\": 323,\n                              \"y\": 509\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"taxAuthoritiesInfo\",\n                  \"keyProb\": 100,\n                  \"value\": \"安阳县国家税务局341052200\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 633,\n                              \"y\": 498\n                        },\n                        {\n                              \"x\": 633,\n                              \"y\": 525\n                        },\n                        {\n                              \"x\": 537,\n                              \"y\": 525\n                        },\n                        {\n                              \"x\": 537,\n                              \"y\": 498\n                        }\n                  ],\n                  \"valueProb\": 99\n            },\n            {\n                  \"key\": \"taxAuthoritiesName\",\n                  \"keyProb\": 100,\n                  \"value\": \"安阳县国家税务局\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 633,\n                              \"y\": 498\n                        },\n                        {\n                              \"x\": 633,\n                              \"y\": 525\n                        },\n                        {\n                              \"x\": 537,\n                              \"y\": 525\n                        },\n                        {\n                              \"x\": 537,\n                              \"y\": 498\n                        }\n                  ],\n                  \"valueProb\": 99\n            },\n            {\n                  \"key\": \"taxAuthoritiesCode\",\n                  \"keyProb\": 100,\n                  \"value\": \"341052200\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 633,\n                              \"y\": 498\n                        },\n                        {\n                              \"x\": 633,\n                              \"y\": 525\n                        },\n                        {\n                              \"x\": 537,\n                              \"y\": 525\n                        },\n                        {\n                              \"x\": 537,\n                              \"y\": 498\n                        }\n                  ],\n                  \"valueProb\": 99\n            },\n            {\n                  \"key\": \"preTaxAmount\",\n                  \"keyProb\": 97,\n                  \"value\": \"84615.38\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 216,\n                              \"y\": 557\n                        },\n                        {\n                              \"x\": 216,\n                              \"y\": 543\n                        },\n                        {\n                              \"x\": 305,\n                              \"y\": 544\n                        },\n                        {\n                              \"x\": 305,\n                              \"y\": 559\n                        }\n                  ],\n                  \"valueProb\": 97\n            },\n            {\n                  \"key\": \"passengerLimitNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"5\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 723,\n                              \"y\": 545\n                        },\n                        {\n                              \"x\": 723,\n                              \"y\": 557\n                        },\n                        {\n                              \"x\": 714,\n                              \"y\": 557\n                        },\n                        {\n                              \"x\": 714,\n                              \"y\": 545\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"issuer\",\n                  \"keyProb\": 100,\n                  \"value\": \"赵迪\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 437,\n                              \"y\": 573\n                        },\n                        {\n                              \"x\": 437,\n                              \"y\": 588\n                        },\n                        {\n                              \"x\": 410,\n                              \"y\": 588\n                        },\n                        {\n                              \"x\": 410,\n                              \"y\": 573\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"tonnage\",\n                  \"keyProb\": 100,\n                  \"value\": \"\",\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"purchaserTaxNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"410523197206046072\",\n                  \"valuePos\": [\n                        {\n                              \"x\": 730,\n                              \"y\": 240\n                        },\n                        {\n                              \"x\": 730,\n                              \"y\": 253\n                        },\n                        {\n                              \"x\": 569,\n                              \"y\": 253\n                        },\n                        {\n                              \"x\": 569,\n                              \"y\": 240\n                        }\n                  ],\n                  \"valueProb\": 100\n            },\n            {\n                  \"key\": \"taxPaymentNumber\",\n                  \"keyProb\": 100,\n                  \"value\": \"\",\n                  \"valueProb\": 100\n            }\n      ],\n      \"width\": 832\n}",
  "Code": "noPermission",
  "Message": "You are not authorized to perform this operation."
}
```

## 错误码

访问[错误中心](https://api.aliyun.com/document/ocr-api/2021-07-07/errorCode)查看更多错误码。

## 变更历史

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |
| 2022-11-25 | API 内部配置变更，不影响调用 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeCarInvoice?updateTime=2022-11-25#workbench-doc-change-demo) |
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeCarInvoice?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[票据凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-bill-voucher-identification/)RecognizeCarInvoice - 机动车销售统一发票识别

# RecognizeCarInvoice - 机动车销售统一发票识别

更新时间：2025-12-08 21:07:57

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeInvoice - 增值税发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeinvoice)[下一篇：RecognizeQuotaInvoice - 定额发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizequotainvoice)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

接口说明

调试

授权信息

请求参数

返回参数

示例

错误码

变更历史