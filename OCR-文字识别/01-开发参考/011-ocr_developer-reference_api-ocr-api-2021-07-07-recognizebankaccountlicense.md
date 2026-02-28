可快速精准的识别银行开户许可证中的账号、法定代表人、开户银行、核准号、企业名称、编号等关键信息。

## 接口说明

#### 本接口适用场景

- 阿里云银行开户许可证识别，是阿里云官方自研 OCR 文字识别产品，适用于识别银行开户许可证所包含的账号、核准号、企业名称、法人姓名以及开户行等关键信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i1/O1CN01h572VA1PARjgZ1TyV_!!6000000001800-2-tps-819-316.png)

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
| 1 | 开通 [票据凭证识别](https://common-buy.aliyun.com/?commodityCode=ocr_invoice_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=assets&subtype=bank_account_permit#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [银行开户许可证识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_enterprisecard_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_enterprisecard_dp_cn_20211103184836_0059%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeBankAccountLicense?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。<br>- 图片尺寸过小，会影响识别精度。图片内单字大小在 10-50px 内时，识别效果较好。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 接口会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |
| 相关能力 | - [云市场银行开户许可证识别。](https://market.aliyun.com/products/57124001/cmapi00042885.html?#sku=yuncode3688500001) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeBankAccountLicense)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeBankAccountLicense)

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
| ocr:RecognizeBankAccountLicense |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/tfs/TB17liGda67gK0jSZFHXXa9jVXa-1375-1000.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | { "data": { "bankAccount": "689163495证异户称", "legalRepresentative": "王嘉琪", "depositaryBank": "中国民生银行股份有限公司上海武宁支行", "approvalNumber": "J2900193652101", "customerName": "杭州读光技术团队有限责任公司", "permitNumber": "2900-02611984", "title": "开户许可证" }, "height": 1000, "orgHeight": 1000, "orgWidth": 1375, "prism\_keyValueInfo": \[{ "key": "bankAccount", "keyProb": 96, "value": "689163495证异户称", "valuePos": \[{ "x": 505, "y": 640 }, { "x": 505, "y": 658 }, { "x": 331, "y": 658 }, { "x": 331, "y": 640 }\], "valueProb": 96 }, { "key": "legalRepresentative", "keyProb": 100, "value": "王嘉琪", "valuePos": \[{ "x": 591, "y": 545 }, { "x": 591, "y": 562 }, { "x": 522, "y": 562 }, { "x": 522, "y": 545 }\], "valueProb": 100 }, { "key": "depositaryBank", "keyProb": 100, "value": "中国民生银行股份有限公司上海武宁支行", "valuePos": \[{ "x": 841, "y": 513 }, { "x": 1200, "y": 505 }, { "x": 1201, "y": 550 }, { "x": 842, "y": 558 }\], "valueProb": 100 }, { "key": "approvalNumber", "keyProb": 100, "value": "J2900193652101", "valuePos": \[{ "x": 247, "y": 257 }, { "x": 411, "y": 252 }, { "x": 412, "y": 269 }, { "x": 248, "y": 274 }\], "valueProb": 100 }, { "key": "customerName", "keyProb": 100, "value": "杭州读光技术团队有限责任公司", "valuePos": \[{ "x": 445, "y": 351 }, { "x": 777, "y": 351 }, { "x": 777, "y": 368 }, { "x": 445, "y": 368 }\], "valueProb": 100 }, { "key": "permitNumber", "keyProb": 100, "value": "2900-02611984", "valuePos": \[{ "x": 1175, "y": 260 }, { "x": 1175, "y": 277 }, { "x": 989, "y": 277 }, { "x": 989, "y": 260 }\], "valueProb": 100 }, { "key": "title", "keyProb": 100, "value": "开户许可证", "valuePos": \[{ "x": 910, "y": 165 }, { "x": 910, "y": 204 }, { "x": 454, "y": 203 }, { "x": 454, "y": 164 }\], "valueProb": 100 }\], "width": 1375 } |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 结构化信息（data 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| bankAccount | string | 账号。 |
| legalRepresentative | string | 法定代表人。 |
| depositaryBank | string | 开户银行。 |
| approvalNumber | string | 核准号。 |
| customerName | string | 名称。 |
| permitNumber | string | 编号。 |
| title | string | 标题。 |

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
      "bankAccount": "689163495证异户称",
      "legalRepresentative": "王嘉琪",
      "depositaryBank": "中国民生银行股份有限公司上海武宁支行",
      "approvalNumber": "J2900193652101",
      "customerName": "杭州读光技术团队有限责任公司",
      "permitNumber": "2900-02611984",
      "title": "开户许可证"
    },
    "height": 1000,
    "orgHeight": 1000,
    "orgWidth": 1375,
    "prism_keyValueInfo": [\
      {\
        "key": "bankAccount",\
        "keyProb": 96,\
        "value": "689163495证异户称",\
        "valuePos": [\
          {\
            "x": 505,\
            "y": 640\
          },\
          {\
            "x": 505,\
            "y": 658\
          },\
          {\
            "x": 331,\
            "y": 658\
          },\
          {\
            "x": 331,\
            "y": 640\
          }\
        ],\
        "valueProb": 96\
      },\
      {\
        "key": "legalRepresentative",\
        "keyProb": 100,\
        "value": "王嘉琪",\
        "valuePos": [\
          {\
            "x": 591,\
            "y": 545\
          },\
          {\
            "x": 591,\
            "y": 562\
          },\
          {\
            "x": 522,\
            "y": 562\
          },\
          {\
            "x": 522,\
            "y": 545\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "depositaryBank",\
        "keyProb": 100,\
        "value": "中国民生银行股份有限公司上海武宁支行",\
        "valuePos": [\
          {\
            "x": 841,\
            "y": 513\
          },\
          {\
            "x": 1200,\
            "y": 505\
          },\
          {\
            "x": 1201,\
            "y": 550\
          },\
          {\
            "x": 842,\
            "y": 558\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "approvalNumber",\
        "keyProb": 100,\
        "value": "J2900193652101",\
        "valuePos": [\
          {\
            "x": 247,\
            "y": 257\
          },\
          {\
            "x": 411,\
            "y": 252\
          },\
          {\
            "x": 412,\
            "y": 269\
          },\
          {\
            "x": 248,\
            "y": 274\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "customerName",\
        "keyProb": 100,\
        "value": "杭州读光技术团队有限责任公司",\
        "valuePos": [\
          {\
            "x": 445,\
            "y": 351\
          },\
          {\
            "x": 777,\
            "y": 351\
          },\
          {\
            "x": 777,\
            "y": 368\
          },\
          {\
            "x": 445,\
            "y": 368\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "permitNumber",\
        "keyProb": 100,\
        "value": "2900-02611984",\
        "valuePos": [\
          {\
            "x": 1175,\
            "y": 260\
          },\
          {\
            "x": 1175,\
            "y": 277\
          },\
          {\
            "x": 989,\
            "y": 277\
          },\
          {\
            "x": 989,\
            "y": 260\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "title",\
        "keyProb": 100,\
        "value": "开户许可证",\
        "valuePos": [\
          {\
            "x": 910,\
            "y": 165\
          },\
          {\
            "x": 910,\
            "y": 204\
          },\
          {\
            "x": 454,\
            "y": 203\
          },\
          {\
            "x": 454,\
            "y": 164\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "width": 1375
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
| 2022-11-25 | API 内部配置变更，不影响调用 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeBankAccountLicense?updateTime=2022-11-25#workbench-doc-change-demo) |
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeBankAccountLicense?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[企业资质识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-enterprise-qualification-identification/)RecognizeBankAccountLicense - 银行开户许可证识别

# RecognizeBankAccountLicense - 银行开户许可证识别

更新时间：2025-12-08 21:10:01

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeBusinessLicense - 营业执照识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizebusinesslicense)[下一篇：RecognizeTradeMarkCertification - 商标注册证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizetrademarkcertification)

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