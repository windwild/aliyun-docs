支持包括票号、出发站、到达站、开车时间、票价、座位类型、旅客信息、座位号、车次等字段结构化识别输出。
2024.12.31更新后，支持电子火车票，增加返回以下新字段：电子客票号、购买方名称、购买方统一信用代码、标题、开票日期、备注。

## 接口说明

#### 本接口适用场景

- 阿里云火车票识别，是阿里云官方自研 OCR 文字识别产品，适用于识别火车票上车次、座位号、旅客信息、座位类型、票价等关键信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/tfs/TB1n9tZccVl614jSZKPXXaGjpXa-1600-800.jpg)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |

| 分类 | 概述 |
| --- | --- |
| 图片格式 | 支持 PNG、JPG、JPEG、BMP、GIF、TIFF、WebP、OFD、PDF。 |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 总体识别准确率可达 98%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [票据凭证识别](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=bill&subtype=train_ticket#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [火车票识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_invoice_dp_cn_20211103182712_0135%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeTrainInvoice?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

* * *

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP、OFD、PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。<br>- 图片尺寸过小，会影响识别精度。图片内单字大小在 10-50px 内时，识别效果较好。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 相关能力 | - [云市场火车票识别。](https://market.aliyun.com/products/57124001/cmapi020096.html?spm=a2c4g.11186623.0.0.6dcb4dcdaoX2WN&innerSource=search#sku=yuncode1409600000) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeTrainInvoice)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeTrainInvoice)

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
| ocr:RecognizeTrainInvoice |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/tfs/TB1u1HrUmzqK1RjSZFpXXakSXXa-1200-900.jpg |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"data": {"departureStation": "杭州东站", "arrivalStation": "南京南站", "trainNumber": "G7608", "departureTime": "2016年10月15日14:10开", "seatNumber": "12车05F号", "fare": "117.5", "seatType": "二等座", "passengerInfo": "3201061982\*\*\*\*0417曹思培", "passengerName": "曹思培", "ticketNumber": "12H010481", "ticketCode": "90041000121016H010481", "saleInfo": "杭州东站售", "ticketGate": "检票口3A"}, "ftype": 0, "height": 900, "orgHeight": 900, "orgWidth": 1200, "prism\_keyValueInfo": \[{"key": "departureStation", "keyProb": 100, "value": "杭州东站", "valuePos": \[{"x": 107, "y": 138}, {"x": 108, "y": 78}, {"x": 288, "y": 81}, {"x": 287, "y": 141}\], "valueProb": 100}, {"key": "arrivalStation", "keyProb": 100, "value": "南京南站", "valuePos": \[{"x": 576, "y": 147}, {"x": 578, "y": 87}, {"x": 760, "y": 90}, {"x": 759, "y": 151}\], "valueProb": 100}, {"key": "trainNumber", "keyProb": 100, "value": "G7608", "valuePos": \[{"x": 379, "y": 140}, {"x": 379, "y": 96}, {"x": 537, "y": 99}, {"x": 537, "y": 144}\], "valueProb": 100}, {"key": "departureTime", "keyProb": 100, "value": "2016年10月15日14:10开", "valuePos": \[{"x": 72, "y": 221}, {"x": 73, "y": 179}, {"x": 467, "y": 187}, {"x": 466, "y": 230}\], "valueProb": 100}, {"key": "seatNumber", "keyProb": 100, "value": "12车05F号", "valuePos": \[{"x": 564, "y": 233}, {"x": 565, "y": 193}, {"x": 734, "y": 195}, {"x": 733, "y": 235}\], "valueProb": 100}, {"key": "fare", "keyProb": 99, "value": "117.5", "valuePos": \[{"x": 242, "y": 233}, {"x": 242, "y": 271}, {"x": 78, "y": 273}, {"x": 77, "y": 234}\], "valueProb": 99}, {"key": "seatType", "keyProb": 100, "value": "二等座", "valuePos": \[{"x": 729, "y": 241}, {"x": 730, "y": 282}, {"x": 620, "y": 283}, {"x": 619, "y": 242}\], "valueProb": 100}, {"key": "passengerInfo", "keyProb": 100, "value": "3201061982\*\*\*\*0417曹思培", "valuePos": \[{"x": 69, "y": 422}, {"x": 69, "y": 376}, {"x": 567, "y": 382}, {"x": 566, "y": 428}\], "valueProb": 100}, {"key": "passengerName", "keyProb": 100, "value": "曹思培", "valuePos": \[{"x": 69, "y": 422}, {"x": 69, "y": 376}, {"x": 567, "y": 382}, {"x": 566, "y": 428}\], "valueProb": 100}, {"key": "ticketNumber", "keyProb": 100, "value": "12H010481", "valuePos": \[{"x": 55, "y": 77}, {"x": 56, "y": 33}, {"x": 318, "y": 39}, {"x": 317, "y": 83}\], "valueProb": 100}, {"key": "ticketCode", "keyProb": 100, "value": "90041000121016H010481", "valuePos": \[{"x": 74, "y": 565}, {"x": 75, "y": 530}, {"x": 404, "y": 536}, {"x": 403, "y": 571}\], "valueProb": 100}, {"key": "saleInfo", "keyProb": 100, "value": "杭州东站售", "valuePos": \[{"x": 425, "y": 572}, {"x": 426, "y": 530}, {"x": 603, "y": 535}, {"x": 602, "y": 576}\], "valueProb": 100}, {"key": "ticketGate", "keyProb": 100, "value": "检票口3A", "valuePos": \[{"x": 664, "y": 79}, {"x": 666, "y": 34}, {"x": 833, "y": 40}, {"x": 832, "y": 85}\], "valueProb": 100}\], "sliceRect": {"x0": 61, "y0": 93, "x1": 1016, "y1": 108, "x2": 1010, "y2": 708, "x3": 51, "y3": 696}, "width": 1200} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误码（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

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
| departureStation | string | 出发站。 |
| arrivalStation | string | 到达站。 |
| trainNumber | string | 车次。 |
| departureTime | string | 开车时间。 |
| seatNumber | string | 座位号。 |
| fare | string | 票价。 |
| ticketGate | string | 检票口。 |
| seatType | string | 座位类型。 |
| passengerInfo | string | 旅客信息。 |
| passengerName | string | 旅客姓名。 |
| ticketNumber | string | 票号。 |
| ticketCode | string | 售票码。 |
| saleInfo | string | 售票车站信息。 |
| electronicTicketNumber | string | 电子客票号。 |
| buyerName | string | 购买方名称。 |
| buyerCreditCode | string | 购买方统一信用代码。 |
| title | string | 标题。 |
| invoiceDate | string | 开票日期。 |
| remarks | string | 备注。 |

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

```prolog
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "data": {
      "departureStation": "杭州东站",
      "arrivalStation": "南京南站",
      "trainNumber": "G7608",
      "departureTime": "2016年10月15日14:10开",
      "seatNumber": "12车05F号",
      "fare": 117.5,
      "seatType": "二等座",
      "passengerInfo": "3201061982****0417曹思培",
      "passengerName": "曹思培",
      "ticketNumber": "12H010481",
      "ticketCode": "90041000121016H010481",
      "saleInfo": "杭州东站售",
      "ticketGate": "检票口3A"
    },
    "ftype": 0,
    "height": 900,
    "orgHeight": 900,
    "orgWidth": 1200,
    "prism_keyValueInfo": [\
      {\
        "key": "departureStation",\
        "keyProb": 100,\
        "value": "杭州东站",\
        "valuePos": [\
          {\
            "x": 107,\
            "y": 138\
          },\
          {\
            "x": 108,\
            "y": 78\
          },\
          {\
            "x": 288,\
            "y": 81\
          },\
          {\
            "x": 287,\
            "y": 141\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "arrivalStation",\
        "keyProb": 100,\
        "value": "南京南站",\
        "valuePos": [\
          {\
            "x": 576,\
            "y": 147\
          },\
          {\
            "x": 578,\
            "y": 87\
          },\
          {\
            "x": 760,\
            "y": 90\
          },\
          {\
            "x": 759,\
            "y": 151\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "trainNumber",\
        "keyProb": 100,\
        "value": "G7608",\
        "valuePos": [\
          {\
            "x": 379,\
            "y": 140\
          },\
          {\
            "x": 379,\
            "y": 96\
          },\
          {\
            "x": 537,\
            "y": 99\
          },\
          {\
            "x": 537,\
            "y": 144\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "departureTime",\
        "keyProb": 100,\
        "value": "2016年10月15日14:10开",\
        "valuePos": [\
          {\
            "x": 72,\
            "y": 221\
          },\
          {\
            "x": 73,\
            "y": 179\
          },\
          {\
            "x": 467,\
            "y": 187\
          },\
          {\
            "x": 466,\
            "y": 230\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "seatNumber",\
        "keyProb": 100,\
        "value": "12车05F号",\
        "valuePos": [\
          {\
            "x": 564,\
            "y": 233\
          },\
          {\
            "x": 565,\
            "y": 193\
          },\
          {\
            "x": 734,\
            "y": 195\
          },\
          {\
            "x": 733,\
            "y": 235\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "fare",\
        "keyProb": 99,\
        "value": 117.5,\
        "valuePos": [\
          {\
            "x": 242,\
            "y": 233\
          },\
          {\
            "x": 242,\
            "y": 271\
          },\
          {\
            "x": 78,\
            "y": 273\
          },\
          {\
            "x": 77,\
            "y": 234\
          }\
        ],\
        "valueProb": 99\
      },\
      {\
        "key": "seatType",\
        "keyProb": 100,\
        "value": "二等座",\
        "valuePos": [\
          {\
            "x": 729,\
            "y": 241\
          },\
          {\
            "x": 730,\
            "y": 282\
          },\
          {\
            "x": 620,\
            "y": 283\
          },\
          {\
            "x": 619,\
            "y": 242\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "passengerInfo",\
        "keyProb": 100,\
        "value": "3201061982****0417曹思培",\
        "valuePos": [\
          {\
            "x": 69,\
            "y": 422\
          },\
          {\
            "x": 69,\
            "y": 376\
          },\
          {\
            "x": 567,\
            "y": 382\
          },\
          {\
            "x": 566,\
            "y": 428\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "passengerName",\
        "keyProb": 100,\
        "value": "曹思培",\
        "valuePos": [\
          {\
            "x": 69,\
            "y": 422\
          },\
          {\
            "x": 69,\
            "y": 376\
          },\
          {\
            "x": 567,\
            "y": 382\
          },\
          {\
            "x": 566,\
            "y": 428\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "ticketNumber",\
        "keyProb": 100,\
        "value": "12H010481",\
        "valuePos": [\
          {\
            "x": 55,\
            "y": 77\
          },\
          {\
            "x": 56,\
            "y": 33\
          },\
          {\
            "x": 318,\
            "y": 39\
          },\
          {\
            "x": 317,\
            "y": 83\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "ticketCode",\
        "keyProb": 100,\
        "value": "90041000121016H010481",\
        "valuePos": [\
          {\
            "x": 74,\
            "y": 565\
          },\
          {\
            "x": 75,\
            "y": 530\
          },\
          {\
            "x": 404,\
            "y": 536\
          },\
          {\
            "x": 403,\
            "y": 571\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "saleInfo",\
        "keyProb": 100,\
        "value": "杭州东站售",\
        "valuePos": [\
          {\
            "x": 425,\
            "y": 572\
          },\
          {\
            "x": 426,\
            "y": 530\
          },\
          {\
            "x": 603,\
            "y": 535\
          },\
          {\
            "x": 602,\
            "y": 576\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "ticketGate",\
        "keyProb": 100,\
        "value": "检票口3A",\
        "valuePos": [\
          {\
            "x": 664,\
            "y": 79\
          },\
          {\
            "x": 666,\
            "y": 34\
          },\
          {\
            "x": 833,\
            "y": 40\
          },\
          {\
            "x": 832,\
            "y": 85\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 61,
      "y0": 93,
      "x1": 1016,
      "y1": 108,
      "x2": 1010,
      "y2": 708,
      "x3": 51,
      "y3": 696
    },
    "width": 1200
  },
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
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeTrainInvoice?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[票据凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-bill-voucher-identification/)RecognizeTrainInvoice - 火车票识别

# RecognizeTrainInvoice - 火车票识别

更新时间：2025-12-08 21:08:15

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeAirItinerary - 航空行程单识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeairitinerary)[下一篇：RecognizeTaxiInvoice - 出租车发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizetaxiinvoice)

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