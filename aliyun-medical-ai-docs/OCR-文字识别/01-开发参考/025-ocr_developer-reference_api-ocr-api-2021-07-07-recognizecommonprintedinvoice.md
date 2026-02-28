支持包括发票代码、发票号码、销售方名称、销售方识别号、购买方名称、购买方识别号、合计金额等关键字段结构化识别输出。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCommonPrintedInvoice)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCommonPrintedInvoice)

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
| ocr:RecognizeCommonPrintedInvoice | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | 图片链接（长度不超 2048 字节，不支持 base64） | https://img.alicdn.com/imgextra/i2/O1CN01XU9dTh1O4CdHxXhMw\_!!6000000001651-0-tps-1437-909.jpg |
| body | byte | 否 | 图片二进制字节流，最大 10MB | 图片二进制 |

### 支持的图片格式

- PNG、JPG、JPEG、BMP、GIF、TIFF、WebP、OFD、PDF

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {<br> "angle": 0,<br> "data": {<br> "title": "浙江通用机打发票",<br> "formType": "发票联",<br> "invoiceCode": "133041930432",<br> "invoiceNumber": "01488558",<br> "printedInvoiceCode": "",<br> "printedInvoiceNumber": "",<br> "invoiceDate": "2019-11-19",<br> "totalAmount": "170.00",<br> "sellerName": "嘉兴市南湖区余新镇瘦汁味餐饮店",<br> "sellerTaxNumber": "92330402MA28B4LL4B",<br> "purchaserName": "阿里巴巴俪人购（上海）电子商务有限公司",<br> "purchaserTaxNumber": "91310114312356647G",<br> "drawer": "高伟",<br> "recipient": "",<br> "remarks": "",<br> "invoiceDetails": \[<br> {<br> "itemName": "餐饮费",<br> "unit": "",<br> "quantity": "1",<br> "unitPrice": "170.00",<br> "amount": "170.00"<br> }<br> \]<br> },<br> "ftype": 0,<br> "height": 909,<br> "orgHeight": 909,<br> "orgWidth": 1437,<br> "prism\_keyValueInfo": \[<br> {<br> "key": "title",<br> "keyProb": 100,<br> "value": "浙江通用机打发票",<br> "valuePos": \[<br> {<br> "x": 431,<br> "y": 68<br> },<br> {<br> "x": 843,<br> "y": 62<br> },<br> {<br> "x": 843,<br> "y": 125<br> },<br> {<br> "x": 431,<br> "y": 130<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "formType",<br> "keyProb": 100,<br> "value": "发票联",<br> "valuePos": \[<br> {<br> "x": 507,<br> "y": 154<br> },<br> {<br> "x": 767,<br> "y": 152<br> },<br> {<br> "x": 768,<br> "y": 214<br> },<br> {<br> "x": 508,<br> "y": 215<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "invoiceCode",<br> "keyProb": 100,<br> "value": "133041930432",<br> "valuePos": \[<br> {<br> "x": 990,<br> "y": 134<br> },<br> {<br> "x": 1283,<br> "y": 131<br> },<br> {<br> "x": 1283,<br> "y": 167<br> },<br> {<br> "x": 991,<br> "y": 171<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "invoiceNumber",<br> "keyProb": 100,<br> "value": "01488558",<br> "valuePos": \[<br> {<br> "x": 999,<br> "y": 195<br> },<br> {<br> "x": 1197,<br> "y": 193<br> },<br> {<br> "x": 1198,<br> "y": 234<br> },<br> {<br> "x": 999,<br> "y": 235<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "printedInvoiceCode",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> },<br> {<br> "key": "printedInvoiceNumber",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> },<br> {<br> "key": "invoiceDate",<br> "keyProb": 100,<br> "value": "2019-11-19",<br> "valuePos": \[<br> {<br> "x": 153,<br> "y": 280<br> },<br> {<br> "x": 351,<br> "y": 278<br> },<br> {<br> "x": 351,<br> "y": 309<br> },<br> {<br> "x": 154,<br> "y": 312<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "totalAmount",<br> "keyProb": 100,<br> "value": "170.00",<br> "valuePos": \[<br> {<br> "x": 300,<br> "y": 752<br> },<br> {<br> "x": 461,<br> "y": 749<br> },<br> {<br> "x": 462,<br> "y": 786<br> },<br> {<br> "x": 300,<br> "y": 788<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "sellerName",<br> "keyProb": 100,<br> "value": "嘉兴市南湖区余新镇瘦汁味餐饮店",<br> "valuePos": \[<br> {<br> "x": 220,<br> "y": 455<br> },<br> {<br> "x": 612,<br> "y": 450<br> },<br> {<br> "x": 612,<br> "y": 482<br> },<br> {<br> "x": 221,<br> "y": 488<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "sellerTaxNumber",<br> "keyProb": 97,<br> "value": "92330402MA28B4LL4B",<br> "valuePos": \[<br> {<br> "x": 224,<br> "y": 511<br> },<br> {<br> "x": 476,<br> "y": 509<br> },<br> {<br> "x": 477,<br> "y": 537<br> },<br> {<br> "x": 225,<br> "y": 539<br> }<br> \],<br> "valueProb": 97<br> },<br> {<br> "key": "purchaserName",<br> "keyProb": 98,<br> "value": "阿里巴巴俪人购（上海）电子商务有限公司",<br> "valuePos": \[<br> {<br> "x": 213,<br> "y": 327<br> },<br> {<br> "x": 714,<br> "y": 324<br> },<br> {<br> "x": 715,<br> "y": 359<br> },<br> {<br> "x": 214,<br> "y": 363<br> }<br> \],<br> "valueProb": 98<br> },<br> {<br> "key": "purchaserTaxNumber",<br> "keyProb": 100,<br> "value": "91310114312356647G",<br> "valuePos": \[<br> {<br> "x": 221,<br> "y": 406<br> },<br> {<br> "x": 480,<br> "y": 402<br> },<br> {<br> "x": 481,<br> "y": 432<br> },<br> {<br> "x": 221,<br> "y": 435<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "drawer",<br> "keyProb": 100,<br> "value": "高伟",<br> "valuePos": \[<br> {<br> "x": 680,<br> "y": 819<br> },<br> {<br> "x": 680,<br> "y": 850<br> },<br> {<br> "x": 627,<br> "y": 850<br> },<br> {<br> "x": 627,<br> "y": 819<br> }<br> \],<br> "valueProb": 100<br> },<br> {<br> "key": "recipient",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> },<br> {<br> "key": "remarks",<br> "keyProb": 100,<br> "value": "",<br> "valueProb": 100<br> },<br> {<br> "key": "invoiceDetails",<br> "keyProb": 100,<br> "value": "\[{\\"itemName\\":\\"餐饮费\\",\\"unit\\":\\"\\",\\"quantity\\":\\"1\\",\\"unitPrice\\":\\"170.00\\",\\"amount\\":\\"170.00\\"}\]",<br> "valueProb": 100<br> }<br> \],<br> "sliceRect": {<br> "x0": 0,<br> "y0": 7,<br> "x1": 1416,<br> "y1": 0,<br> "x2": 1421,<br> "y2": 907,<br> "x3": 0,<br> "y3": 904<br> },<br> "width": 1437<br>} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

中英文映射字段

```apache
title           标题
formType           发票联次
invoiceCode           发票代码
invoiceNumber           发票号码
printedInvoiceCode          发票代码-机打
printedInvoiceNumber           发票号码-机打
invoiceDate           开票日期
totalAmount           合计金额
sellerName           销售方名称
sellerTaxNumber           销售方纳税人识别号
purchaserName           购买方名称
purchaserTaxNumber           购买方纳税人识别号
drawer           开票人
recipient           收款人
remarks           备注
invoiceDetails           发票详单
itemName           项目名称
unit           单位
quantity           数量
unitPrice           单价
amount           总值
ftype           是否是复印件(1:是，0:否)
```

## 示例

正常返回示例

`JSON`格式

```prolog
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "angle": 0,
    "data": {
      "title": "浙江通用机打发票",
      "formType": "发票联",
      "invoiceCode": 133041930432,
      "invoiceNumber": "01488558",
      "printedInvoiceCode": "",
      "printedInvoiceNumber": "",
      "invoiceDate": "2019-11-19",
      "totalAmount": 170,
      "sellerName": "嘉兴市南湖区余新镇瘦汁味餐饮店",
      "sellerTaxNumber": "92330402MA28B4LL4B",
      "purchaserName": "阿里巴巴俪人购（上海）电子商务有限公司",
      "purchaserTaxNumber": "91310114312356647G",
      "drawer": "高伟",
      "recipient": "",
      "remarks": "",
      "invoiceDetails": [\
        {\
          "itemName": "餐饮费",\
          "unit": "",\
          "quantity": 1,\
          "unitPrice": 170,\
          "amount": 170\
        }\
      ]
    },
    "ftype": 0,
    "height": 909,
    "orgHeight": 909,
    "orgWidth": 1437,
    "prism_keyValueInfo": [\
      {\
        "key": "title",\
        "keyProb": 100,\
        "value": "浙江通用机打发票",\
        "valuePos": [\
          {\
            "x": 431,\
            "y": 68\
          },\
          {\
            "x": 843,\
            "y": 62\
          },\
          {\
            "x": 843,\
            "y": 125\
          },\
          {\
            "x": 431,\
            "y": 130\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "formType",\
        "keyProb": 100,\
        "value": "发票联",\
        "valuePos": [\
          {\
            "x": 507,\
            "y": 154\
          },\
          {\
            "x": 767,\
            "y": 152\
          },\
          {\
            "x": 768,\
            "y": 214\
          },\
          {\
            "x": 508,\
            "y": 215\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceCode",\
        "keyProb": 100,\
        "value": 133041930432,\
        "valuePos": [\
          {\
            "x": 990,\
            "y": 134\
          },\
          {\
            "x": 1283,\
            "y": 131\
          },\
          {\
            "x": 1283,\
            "y": 167\
          },\
          {\
            "x": 991,\
            "y": 171\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceNumber",\
        "keyProb": 100,\
        "value": "01488558",\
        "valuePos": [\
          {\
            "x": 999,\
            "y": 195\
          },\
          {\
            "x": 1197,\
            "y": 193\
          },\
          {\
            "x": 1198,\
            "y": 234\
          },\
          {\
            "x": 999,\
            "y": 235\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "printedInvoiceCode",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "printedInvoiceNumber",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceDate",\
        "keyProb": 100,\
        "value": "2019-11-19",\
        "valuePos": [\
          {\
            "x": 153,\
            "y": 280\
          },\
          {\
            "x": 351,\
            "y": 278\
          },\
          {\
            "x": 351,\
            "y": 309\
          },\
          {\
            "x": 154,\
            "y": 312\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "totalAmount",\
        "keyProb": 100,\
        "value": 170,\
        "valuePos": [\
          {\
            "x": 300,\
            "y": 752\
          },\
          {\
            "x": 461,\
            "y": 749\
          },\
          {\
            "x": 462,\
            "y": 786\
          },\
          {\
            "x": 300,\
            "y": 788\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "sellerName",\
        "keyProb": 100,\
        "value": "嘉兴市南湖区余新镇瘦汁味餐饮店",\
        "valuePos": [\
          {\
            "x": 220,\
            "y": 455\
          },\
          {\
            "x": 612,\
            "y": 450\
          },\
          {\
            "x": 612,\
            "y": 482\
          },\
          {\
            "x": 221,\
            "y": 488\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "sellerTaxNumber",\
        "keyProb": 97,\
        "value": "92330402MA28B4LL4B",\
        "valuePos": [\
          {\
            "x": 224,\
            "y": 511\
          },\
          {\
            "x": 476,\
            "y": 509\
          },\
          {\
            "x": 477,\
            "y": 537\
          },\
          {\
            "x": 225,\
            "y": 539\
          }\
        ],\
        "valueProb": 97\
      },\
      {\
        "key": "purchaserName",\
        "keyProb": 98,\
        "value": "阿里巴巴俪人购（上海）电子商务有限公司",\
        "valuePos": [\
          {\
            "x": 213,\
            "y": 327\
          },\
          {\
            "x": 714,\
            "y": 324\
          },\
          {\
            "x": 715,\
            "y": 359\
          },\
          {\
            "x": 214,\
            "y": 363\
          }\
        ],\
        "valueProb": 98\
      },\
      {\
        "key": "purchaserTaxNumber",\
        "keyProb": 100,\
        "value": "91310114312356647G",\
        "valuePos": [\
          {\
            "x": 221,\
            "y": 406\
          },\
          {\
            "x": 480,\
            "y": 402\
          },\
          {\
            "x": 481,\
            "y": 432\
          },\
          {\
            "x": 221,\
            "y": 435\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "drawer",\
        "keyProb": 100,\
        "value": "高伟",\
        "valuePos": [\
          {\
            "x": 680,\
            "y": 819\
          },\
          {\
            "x": 680,\
            "y": 850\
          },\
          {\
            "x": 627,\
            "y": 850\
          },\
          {\
            "x": 627,\
            "y": 819\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "recipient",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "remarks",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "invoiceDetails",\
        "keyProb": 100,\
        "value": [\
          {\
            "itemName": "餐饮费",\
            "unit": "",\
            "quantity": 1,\
            "unitPrice": 170,\
            "amount": 170\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 0,
      "y0": 7,
      "x1": 1416,
      "y1": 0,
      "x2": 1421,
      "y2": 907,
      "x3": 0,
      "y3": 904
    },
    "width": 1437
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

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[票据凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-bill-voucher-identification/)RecognizeCommonPrintedInvoice - 通用机打发票识别

# RecognizeCommonPrintedInvoice - 通用机打发票识别

更新时间：2025-12-08 21:08:52

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeNonTaxInvoice - 非税收入发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizenontaxinvoice)[下一篇：RecognizeHotelConsume - 酒店流水识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizehotelconsume)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

授权信息

请求参数

支持的图片格式

返回参数

示例

错误码

变更历史