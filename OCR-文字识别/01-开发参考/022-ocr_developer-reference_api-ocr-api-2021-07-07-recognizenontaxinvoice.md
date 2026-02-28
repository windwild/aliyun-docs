支持包括票据代码、交款人、票据号码、合计金额、收款单位等关键字段结构化识别输出。

## 接口说明

#### 本接口适用场景

- 阿里云非税收入发票识别，是阿里云官方自研 OCR 文字识别产品，适用于识别非税收入发票所包含的票据号码、标题、开票日期、合计金额、收款人等关键信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i4/O1CN01jraEpU29O9qPIWKaT_!!6000000008057-0-tps-2977-1800.jpg)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |

| 分类 | 概述 |
| --- | --- |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 总体识别准确率可达 97%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [票据凭证识别](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=bill&subtype=nontax_invoice#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [车辆物流识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_invoice_dp_cn_20220303112214_0050%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeNonTaxInvoice?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

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
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeNonTaxInvoice)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeNonTaxInvoice)

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
| ocr:RecognizeNonTaxInvoice | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241223/bsrdwj/%E9%9D%9E%E7%A8%8E%E6%94%B6%E5%85%A5%E5%8F%91%E7%A5%A8%E8%AF%86%E5%88%AB.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"data": {"title": "中央非税收入统一票据(电子)", "invoiceCode": "00010120", "payerCreditCode": "", "payerName": "上饶市合诚娱乐设备有限公司", "invoiceNumber": "0026421031", "validationCode": "656aa9", "invoiceDate": "2021-03-19", "totalAmountInWords": "陆佰元整", "totalAmount": "600.00", "additionalInfo": "申请号:2012306329368 缴费日期:2021-03-17 缴费方式:网上支付 订单号:1105000114740512", "payeeName": "国家知识产权局专利局", "reviewer": "胡文举", "recipient": "刘代彬", "invoiceDetails": \[{"number": "056990126100", "name": "外观设计专利第10年年费", "unit": "元", "quantity": "0.3", "specification": "2,000.00", "amount": "600.00", "remark": ""}\]}, "ftype": 0, "height": 1800, "orgHeight": 1800, "orgWidth": 2977, "prism\_keyValueInfo": \[{"key": "title", "keyProb": 100, "value": "中央非税收入统一票据(电子)", "valuePos": \[{"x": 680, "y": 63}, {"x": 1618, "y": 62}, {"x": 1618, "y": 139}, {"x": 681, "y": 141}\], "valueProb": 100}, {"key": "invoiceCode", "keyProb": 100, "value": "00010120", "valuePos": \[{"x": 421, "y": 228}, {"x": 421, "y": 276}, {"x": 242, "y": 276}, {"x": 242, "y": 228}\], "valueProb": 100}, {"key": "payerCreditCode", "keyProb": 100, "value": "", "valueProb": 100}, {"key": "payerName", "keyProb": 100, "value": "上饶市合诚娱乐设备有限公司", "valuePos": \[{"x": 189, "y": 357}, {"x": 664, "y": 356}, {"x": 664, "y": 403}, {"x": 190, "y": 404}\], "valueProb": 100}, {"key": "invoiceNumber", "keyProb": 100, "value": "0026421031", "valuePos": \[{"x": 1934, "y": 222}, {"x": 1935, "y": 272}, {"x": 1718, "y": 274}, {"x": 1718, "y": 224}\], "valueProb": 100}, {"key": "validationCode", "keyProb": 100, "value": "656aa9", "valuePos": \[{"x": 1800, "y": 303}, {"x": 1800, "y": 349}, {"x": 1666, "y": 351}, {"x": 1665, "y": 304}\], "valueProb": 100}, {"key": "invoiceDate", "keyProb": 100, "value": "2021-03-19", "valuePos": \[{"x": 1924, "y": 382}, {"x": 1924, "y": 431}, {"x": 1711, "y": 431}, {"x": 1711, "y": 382}\], "valueProb": 100}, {"key": "totalAmountInWords", "keyProb": 100, "value": "陆佰元整", "valuePos": \[{"x": 607, "y": 1110}, {"x": 607, "y": 1167}, {"x": 417, "y": 1167}, {"x": 417, "y": 1110}\], "valueProb": 100}, {"key": "totalAmount", "keyProb": 100, "value": "600.00", "valuePos": \[{"x": 1702, "y": 1113}, {"x": 1702, "y": 1163}, {"x": 1576, "y": 1163}, {"x": 1576, "y": 1113}\], "valueProb": 100}, {"key": "additionalInfo", "keyProb": 100, "value": "申请号:2012306329368 缴费日期:2021-03-17 缴费方式:网上支付 订单号:1105000114740512", "valuePos": \[{"x": 121, "y": 1197}, {"x": 1869, "y": 1194}, {"x": 1870, "y": 1252}, {"x": 122, "y": 1254}\], "valueProb": 100}, {"key": "payeeName", "keyProb": 100, "value": "国家知识产权局专利局", "valuePos": \[{"x": 886, "y": 1645}, {"x": 886, "y": 1698}, {"x": 424, "y": 1700}, {"x": 423, "y": 1646}\], "valueProb": 100}, {"key": "reviewer", "keyProb": 100, "value": "胡文举", "valuePos": \[{"x": 1559, "y": 1653}, {"x": 1559, "y": 1708}, {"x": 1418, "y": 1708}, {"x": 1418, "y": 1653}\], "valueProb": 100}, {"key": "recipient", "keyProb": 100, "value": "刘代彬", "valuePos": \[{"x": 2090, "y": 1653}, {"x": 2090, "y": 1708}, {"x": 1947, "y": 1708}, {"x": 1947, "y": 1653}\], "valueProb": 100}, {"key": "invoiceDetails", "keyProb": 100, "value": "\[{\\"number\\":\\"056990126100\\",\\"name\\":\\"外观设计专利第10年年费\\",\\"unit\\":\\"元\\",\\"quantity\\":\\"0.3\\",\\"specification\\":\\"2,000.00\\",\\"amount\\":\\"600.00\\",\\"remark\\":\\"\\"}\]", "valueProb": 100}\], "sliceRect": {"x0": 288, "y0": 0, "x1": 2669, "y1": 0, "x2": 2669, "y2": 1800, "x3": 287, "y3": 1800}, "width": 2977} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
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
| additionalInfo | string | 其他信息。 |
| invoiceCode | string | 票据代码。 |
| invoiceDate | string | 开票日期。 |
| invoiceDetails | list | 项目详单。 |
| invoiceNumber | string | 票据号码。 |
| payeeName | string | 收款单位。 |
| payerCreditCode | string | 交款人统一社会信用代码。 |
| payerName | string | 交款人。 |
| recipient | string | 收款人。 |
| reviewer | string | 复核人。 |
| title | string | 标题。 |
| totalAmount | string | 合计金额（小写）。 |
| totalAmountInWords | string | 合计金额（大写）。 |
| validationCode | string | 校验码。 |

#### 发票详单信息（invoiceDetails 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| amount | string | 金额。 |
| name | string | 项目名称。 |
| number | string | 项目编号。 |
| quantity | string | 数量。 |
| remark | string | 备注。 |
| specification | string | 标准。 |
| unit | string | 单位。 |

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
      "title": "中央非税收入统一票据(电子)",
      "invoiceCode": "00010120",
      "payerCreditCode": "",
      "payerName": "上饶市合诚娱乐设备有限公司",
      "invoiceNumber": "0026421031",
      "validationCode": "656aa9",
      "invoiceDate": "2021-03-19",
      "totalAmountInWords": "陆佰元整",
      "totalAmount": 600,
      "additionalInfo": "申请号:2012306329368 缴费日期:2021-03-17 缴费方式:网上支付 订单号:1105000114740512",
      "payeeName": "国家知识产权局专利局",
      "reviewer": "胡文举",
      "recipient": "刘代彬",
      "invoiceDetails": [\
        {\
          "number": "056990126100",\
          "name": "外观设计专利第10年年费",\
          "unit": "元",\
          "quantity": 0.3,\
          "specification": "2,000.00",\
          "amount": 600,\
          "remark": ""\
        }\
      ]
    },
    "ftype": 0,
    "height": 1800,
    "orgHeight": 1800,
    "orgWidth": 2977,
    "prism_keyValueInfo": [\
      {\
        "key": "title",\
        "keyProb": 100,\
        "value": "中央非税收入统一票据(电子)",\
        "valuePos": [\
          {\
            "x": 680,\
            "y": 63\
          },\
          {\
            "x": 1618,\
            "y": 62\
          },\
          {\
            "x": 1618,\
            "y": 139\
          },\
          {\
            "x": 681,\
            "y": 141\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceCode",\
        "keyProb": 100,\
        "value": "00010120",\
        "valuePos": [\
          {\
            "x": 421,\
            "y": 228\
          },\
          {\
            "x": 421,\
            "y": 276\
          },\
          {\
            "x": 242,\
            "y": 276\
          },\
          {\
            "x": 242,\
            "y": 228\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "payerCreditCode",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "payerName",\
        "keyProb": 100,\
        "value": "上饶市合诚娱乐设备有限公司",\
        "valuePos": [\
          {\
            "x": 189,\
            "y": 357\
          },\
          {\
            "x": 664,\
            "y": 356\
          },\
          {\
            "x": 664,\
            "y": 403\
          },\
          {\
            "x": 190,\
            "y": 404\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceNumber",\
        "keyProb": 100,\
        "value": "0026421031",\
        "valuePos": [\
          {\
            "x": 1934,\
            "y": 222\
          },\
          {\
            "x": 1935,\
            "y": 272\
          },\
          {\
            "x": 1718,\
            "y": 274\
          },\
          {\
            "x": 1718,\
            "y": 224\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "validationCode",\
        "keyProb": 100,\
        "value": "656aa9",\
        "valuePos": [\
          {\
            "x": 1800,\
            "y": 303\
          },\
          {\
            "x": 1800,\
            "y": 349\
          },\
          {\
            "x": 1666,\
            "y": 351\
          },\
          {\
            "x": 1665,\
            "y": 304\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceDate",\
        "keyProb": 100,\
        "value": "2021-03-19",\
        "valuePos": [\
          {\
            "x": 1924,\
            "y": 382\
          },\
          {\
            "x": 1924,\
            "y": 431\
          },\
          {\
            "x": 1711,\
            "y": 431\
          },\
          {\
            "x": 1711,\
            "y": 382\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "totalAmountInWords",\
        "keyProb": 100,\
        "value": "陆佰元整",\
        "valuePos": [\
          {\
            "x": 607,\
            "y": 1110\
          },\
          {\
            "x": 607,\
            "y": 1167\
          },\
          {\
            "x": 417,\
            "y": 1167\
          },\
          {\
            "x": 417,\
            "y": 1110\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "totalAmount",\
        "keyProb": 100,\
        "value": 600,\
        "valuePos": [\
          {\
            "x": 1702,\
            "y": 1113\
          },\
          {\
            "x": 1702,\
            "y": 1163\
          },\
          {\
            "x": 1576,\
            "y": 1163\
          },\
          {\
            "x": 1576,\
            "y": 1113\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "additionalInfo",\
        "keyProb": 100,\
        "value": "申请号:2012306329368 缴费日期:2021-03-17 缴费方式:网上支付 订单号:1105000114740512",\
        "valuePos": [\
          {\
            "x": 121,\
            "y": 1197\
          },\
          {\
            "x": 1869,\
            "y": 1194\
          },\
          {\
            "x": 1870,\
            "y": 1252\
          },\
          {\
            "x": 122,\
            "y": 1254\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "payeeName",\
        "keyProb": 100,\
        "value": "国家知识产权局专利局",\
        "valuePos": [\
          {\
            "x": 886,\
            "y": 1645\
          },\
          {\
            "x": 886,\
            "y": 1698\
          },\
          {\
            "x": 424,\
            "y": 1700\
          },\
          {\
            "x": 423,\
            "y": 1646\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "reviewer",\
        "keyProb": 100,\
        "value": "胡文举",\
        "valuePos": [\
          {\
            "x": 1559,\
            "y": 1653\
          },\
          {\
            "x": 1559,\
            "y": 1708\
          },\
          {\
            "x": 1418,\
            "y": 1708\
          },\
          {\
            "x": 1418,\
            "y": 1653\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "recipient",\
        "keyProb": 100,\
        "value": "刘代彬",\
        "valuePos": [\
          {\
            "x": 2090,\
            "y": 1653\
          },\
          {\
            "x": 2090,\
            "y": 1708\
          },\
          {\
            "x": 1947,\
            "y": 1708\
          },\
          {\
            "x": 1947,\
            "y": 1653\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceDetails",\
        "keyProb": 100,\
        "value": [\
          {\
            "number": "056990126100",\
            "name": "外观设计专利第10年年费",\
            "unit": "元",\
            "quantity": 0.3,\
            "specification": "2,000.00",\
            "amount": 600,\
            "remark": ""\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 288,
      "y0": 0,
      "x1": 2669,
      "y1": 0,
      "x2": 2669,
      "y2": 1800,
      "x3": 287,
      "y3": 1800
    },
    "width": 2977
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
| 2022-03-16 | 新增 OpenAPI | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeNonTaxInvoice?updateTime=2022-03-16#workbench-doc-change-demo) |

SDK 调用
通过 SDK 调用此接口的示例请参考 [开发者中心](https://next.api.aliyun.com/api-tools/sdk/ocr-api?version=2021-07-07&language=java-tea)

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[票据凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-bill-voucher-identification/)RecognizeNonTaxInvoice - 非税收入发票识别

# RecognizeNonTaxInvoice - 非税收入发票识别

更新时间：2025-12-08 21:08:46

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeBusShipTicket - 客运车船票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizebusshipticket)[下一篇：RecognizeCommonPrintedInvoice - 通用机打发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizecommonprintedinvoice)

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