支持包括税务机关、纳税人识别号、纳税人名称、合计金额、填票人、完税详单等关键字段的结构化识别输出。

## 接口说明

#### 本接口适用场景

- 阿里云税收完税证明识别，是阿里云官方自研 OCR 文字识别产品，适用于识别非税收入证明所包含的税务机关、纳税人识别号、纳税人名称、合计金额、填票人、完税详单等关键信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i4/O1CN01hmLCcX1JV9xJF1joS_!!6000000001033-2-tps-757-472.png)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |

| 分类 | 概述 |
| --- | --- |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 总体识别准确率可达 98%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [票据凭证识别](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=bill&subtype=tax_clearance_certificate#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [票据凭证识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_invoice_dp_cn_20211222173940_0304%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeTaxClearanceCertificate?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。<br>- 图片尺寸过小，会影响识别精度。图片内单字大小在 10-50px 内时，识别效果较好。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 接口会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeTaxClearanceCertificate)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeTaxClearanceCertificate)

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
| ocr:RecognizeTaxClearanceCertificate | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/imgextra/i1/O1CN0131X3Xs1d1CHG8oypS\_!!6000000003675-0-tps-1080-712.jpg |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | { "angle": 0, "data": { "issueDate": "HLELLA", "certificateNumber": "01008454", "taxAuthorityName": "", "formType": "", "taxNumbe": "stalzitsiatw0rdzl2", "name": "●△●", "totalAmountInWords": "", "totalAmount": "", "drawer": "RAG612412", "remarks": "ILE号:14010181043B455", "taxClearanceDetails": \[ { "voucherNumber": "126210004111262000004110126200041112621000004111262900000411012621000004", "taxType": "fhkNMOAPTERN●LHAK", "itemName": "开业机", "taxPeriod": "liHi-80H801M1-01404", "date": "RESHR801M1", "amount": "100.00" }, { "voucherNumber": "", "taxType": "●", "itemName": "", "taxPeriod": "", "date": "", "amount": "" } \] }, "ftype": 0, "height": 177, "orgHeight": 177, "orgWidth": 285, "prism\_keyValueInfo": \[ { "key": "issueDate", "keyProb": 74, "value": "HLELLA", "valuePos": \[ { "x": 170, "y": 32 }, { "x": 170, "y": 38 }, { "x": 118, "y": 38 }, { "x": 118, "y": 31 } \], "valueProb": 74 }, { "key": "certificateNumber", "keyProb": 91, "value": "01008454", "valuePos": \[ { "x": 216, "y": 30 }, { "x": 217, "y": 24 }, { "x": 267, "y": 27 }, { "x": 267, "y": 32 } \], "valueProb": 91 }, { "key": "taxAuthorityName", "keyProb": 100, "value": "", "valueProb": 100 }, { "key": "formType", "keyProb": 100, "value": "", "valueProb": 100 }, { "key": "taxNumbe", "keyProb": 78, "value": "stalzitsiatw0rdzl2", "valuePos": \[ { "x": 94, "y": 41 }, { "x": 94, "y": 47 }, { "x": 44, "y": 47 }, { "x": 44, "y": 41 } \], "valueProb": 78 }, { "key": "name", "keyProb": 93, "value": "●△●", "valuePos": \[ { "x": 277, "y": 47 }, { "x": 277, "y": 70 }, { "x": 273, "y": 70 }, { "x": 273, "y": 47 } \], "valueProb": 91 }, { "key": "totalAmountInWords", "keyProb": 100, "value": "", "valueProb": 100 }, { "key": "totalAmount", "keyProb": 100, "value": "", "valueProb": 100 }, { "key": "drawer", "keyProb": 71, "value": "RAG612412", "valuePos": \[ { "x": 127, "y": 149 }, { "x": 127, "y": 155 }, { "x": 94, "y": 155 }, { "x": 94, "y": 149 } \], "valueProb": 71 }, { "key": "remarks", "keyProb": 76, "value": "ILE号:14010181043B455", "valuePos": \[ { "x": 222, "y": 135 }, { "x": 222, "y": 140 }, { "x": 158, "y": 140 }, { "x": 158, "y": 135 } \], "valueProb": 76 }, { "key": "taxClearanceDetails", "keyProb": 100, "value": "\[{\\"voucherNumber\\":\\"126210004111262000004110126200041112621000004111262900000411012621000004\\",\\"taxType\\":\\"fhkNMOAPTERN●LHAK\\",\\"itemName\\":\\"开业机\\",\\"taxPeriod\\":\\"liHi-80H801M1-01404\\",\\"date\\":\\"RESHR801M1\\",\\"amount\\":\\"100.00\\"},{\\"voucherNumber\\":\\"\\",\\"taxType\\":\\"●\\",\\"itemName\\":\\"\\",\\"taxPeriod\\":\\"\\",\\"date\\":\\"\\",\\"amount\\":\\"\\"}\]", "valueProb": 100 } \], "sliceRect": { "x0": 0, "y0": 0, "x1": 283, "y1": 0, "x2": 283, "y2": 174, "x3": 0, "y3": 174 }, "width": 285 } |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
| angle | int | 图片的角度，0 表示正向，90 表示图片朝右，180 朝下，270 朝左。 |
| ftype | int | 是否为复印件（1：是，0：否）。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |
| sliceRect | list | 检测出的子图坐标信息。 |

#### 结构化信息（data 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| certificateNumber | string | 编号。 |
| drawer | string | 填票人。 |
| formType | string | 联次。 |
| issueDate | string | 填发日期。 |
| name | string | 纳税人名称。 |
| remarks | string | 备注。 |
| taxAuthorityName | string | 税务机关。 |
| taxClearanceDetails | list | 完税详单。 |
| taxNumbe | string | 纳税人识别号。 |
| totalAmount | string | 合计金额（小写）。 |
| totalAmountInWords | string | 合计金额（大写）。 |

#### 完税详单（taxClearanceDetails 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| amount | string | 实缴（退）金额。 |
| date | string | 入（退）库时间。 |
| itemName | string | 品目名称。 |
| taxPeriod | string | 税款所属期。 |
| taxType | string | 税种。 |
| voucherNumber | string | 原凭证号。 |

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
    "angle": 0,
    "data": {
      "issueDate": "HLELLA",
      "certificateNumber": "01008454",
      "taxAuthorityName": "",
      "formType": "",
      "taxNumbe": "stalzitsiatw0rdzl2",
      "name": "●△●",
      "totalAmountInWords": "",
      "totalAmount": "",
      "drawer": "RAG612412",
      "remarks": "ILE号:14010181043B455",
      "taxClearanceDetails": [\
        {\
          "voucherNumber": 1.26210004111262e+71,\
          "taxType": "fhkNMOAPTERN●LHAK",\
          "itemName": "开业机",\
          "taxPeriod": "liHi-80H801M1-01404",\
          "date": "RESHR801M1",\
          "amount": 100\
        },\
        {\
          "voucherNumber": "",\
          "taxType": "●",\
          "itemName": "",\
          "taxPeriod": "",\
          "date": "",\
          "amount": ""\
        }\
      ]
    },
    "ftype": 0,
    "height": 177,
    "orgHeight": 177,
    "orgWidth": 285,
    "prism_keyValueInfo": [\
      {\
        "key": "issueDate",\
        "keyProb": 74,\
        "value": "HLELLA",\
        "valuePos": [\
          {\
            "x": 170,\
            "y": 32\
          },\
          {\
            "x": 170,\
            "y": 38\
          },\
          {\
            "x": 118,\
            "y": 38\
          },\
          {\
            "x": 118,\
            "y": 31\
          }\
        ],\
        "valueProb": 74\
      },\
      {\
        "key": "certificateNumber",\
        "keyProb": 91,\
        "value": "01008454",\
        "valuePos": [\
          {\
            "x": 216,\
            "y": 30\
          },\
          {\
            "x": 217,\
            "y": 24\
          },\
          {\
            "x": 267,\
            "y": 27\
          },\
          {\
            "x": 267,\
            "y": 32\
          }\
        ],\
        "valueProb": 91\
      },\
      {\
        "key": "taxAuthorityName",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "formType",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "taxNumbe",\
        "keyProb": 78,\
        "value": "stalzitsiatw0rdzl2",\
        "valuePos": [\
          {\
            "x": 94,\
            "y": 41\
          },\
          {\
            "x": 94,\
            "y": 47\
          },\
          {\
            "x": 44,\
            "y": 47\
          },\
          {\
            "x": 44,\
            "y": 41\
          }\
        ],\
        "valueProb": 78\
      },\
      {\
        "key": "name",\
        "keyProb": 93,\
        "value": "●△●",\
        "valuePos": [\
          {\
            "x": 277,\
            "y": 47\
          },\
          {\
            "x": 277,\
            "y": 70\
          },\
          {\
            "x": 273,\
            "y": 70\
          },\
          {\
            "x": 273,\
            "y": 47\
          }\
        ],\
        "valueProb": 91\
      },\
      {\
        "key": "totalAmountInWords",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "totalAmount",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "drawer",\
        "keyProb": 71,\
        "value": "RAG612412",\
        "valuePos": [\
          {\
            "x": 127,\
            "y": 149\
          },\
          {\
            "x": 127,\
            "y": 155\
          },\
          {\
            "x": 94,\
            "y": 155\
          },\
          {\
            "x": 94,\
            "y": 149\
          }\
        ],\
        "valueProb": 71\
      },\
      {\
        "key": "remarks",\
        "keyProb": 76,\
        "value": "ILE号:14010181043B455",\
        "valuePos": [\
          {\
            "x": 222,\
            "y": 135\
          },\
          {\
            "x": 222,\
            "y": 140\
          },\
          {\
            "x": 158,\
            "y": 140\
          },\
          {\
            "x": 158,\
            "y": 135\
          }\
        ],\
        "valueProb": 76\
      },\
      {\
        "key": "taxClearanceDetails",\
        "keyProb": 100,\
        "value": [\
          {\
            "voucherNumber": 1.26210004111262e+71,\
            "taxType": "fhkNMOAPTERN●LHAK",\
            "itemName": "开业机",\
            "taxPeriod": "liHi-80H801M1-01404",\
            "date": "RESHR801M1",\
            "amount": 100\
          },\
          {\
            "voucherNumber": "",\
            "taxType": "●",\
            "itemName": "",\
            "taxPeriod": "",\
            "date": "",\
            "amount": ""\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 0,
      "y0": 0,
      "x1": 283,
      "y1": 0,
      "x2": 283,
      "y2": 174,
      "x3": 0,
      "y3": 174
    },
    "width": 285
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

暂无变更历史

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[票据凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-bill-voucher-identification/)RecognizeTaxClearanceCertificate - 税收完税证明识别

# RecognizeTaxClearanceCertificate - 税收完税证明识别

更新时间：2025-12-08 21:09:36

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeTollInvoice - 过路过桥费发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizetollinvoice)[下一篇：RecognizeUsedCarInvoice - 二手车统一销售发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeusedcarinvoice)

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