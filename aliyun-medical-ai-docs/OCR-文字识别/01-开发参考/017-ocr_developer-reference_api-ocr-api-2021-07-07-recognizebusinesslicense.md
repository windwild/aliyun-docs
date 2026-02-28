可快速精准的识别企业营业执照中的统一社会信用代码、公司名称、地址、主体类型、法定代表人、注册资金、组成形式、成立日期、营业期限和经营范围等关键有效字段。支持营业执照、民办非企业登记证书、社会团体法人登记证书、事业单位法人证书。

## 接口说明

#### 本接口适用场景

- 阿里云营业执照识别，是阿里云官方自研 OCR 文字识别产品，适用于识别营业执照上的公司名称、地址、主体类型、法定代表人、注册资金、组成形式、成立日期等关键信息的场景。
- 泛营业执照包含民办非企业登记证书、社会团体法人登记证书、事业单位法人证书。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i1/O1CN01bAhaqS1WxdaE0QfbB_!!6000000002855-0-tps-875-391.jpg)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 全字段识别 | 智能识别营业执照上所包含的全部字段。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 企事业名称、法人代表等文字信息准确率超过 95%，营业执照注册号等数字信息准确率超过 98%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [企业资质识别](https://common-buy.aliyun.com/?commodityCode=ocr_enterprisecard_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=assets&subtype=blicense#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [营业执照识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_enterprisecard_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_enterprisecard_dp_cn_20211103184836_0975%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeBusinessLicense?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 请保证整张营业执照内容及其边缘包含在图像内。 <br>- 本能力会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |
| 相关能力 | - [云市场营业执照识别。](https://market.aliyun.com/products/57124001/cmapi013592.html?spm=5176.730005.result.41.7fc03524S3wFYv&innerSource=search_%E8%90%A5%E4%B8%9A%E6%89%A7%E7%85%A7#sku=yuncode759200000) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeBusinessLicense)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeBusinessLicense)

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
| ocr:RecognizeBusinessLicense |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/tfs/TB1nnHJNSrqK1RjSZK9XXXyypXa-564-829.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"algo\_version": "5f161015b0f3e48197b049a587c5b2468d8d0cb9;0c879a80496474870d0b1ff89f9c58fe6a53651d", "codes": \[{"data": "", "points": \[{"x": 42, "y": 558}, {"x": 142, "y": 558}, {"x": 142, "y": 659}, {"x": 42, "y": 659}\], "type": "QRcode"}\], "data": {"RegistrationDate": "2017年01月04日", "businessAddress": "萧山区宁围街道泰宏巷40号联合中心北区", "businessScope": "影视文化艺术活动策划,艺术造型、美术设计,影视道具与服装设计:影视制作技术的研发;会议及展览服务;企业形象策划、影视文化信息咨询、摄影、摄像服务(除冲扩):设计、制作、代理国内广告(除网络广告):艺人经纪服务(营业性演出除外):公关策划:网站建设、软硬件开发维护、技术服务;销售:化妆品(除分装)、日用百货、服装、玩具、母婴用品(除食品药品)、第二类医疗器械\*\*(依法须经批准的项目,经相关部门批准后方可开展经营活动)", "companyForm": "", "companyName": "杭州橘子文化传媒有限公司", "companyType": "有限责任公司(自然人投资或控股)", "creditCode": "913301095U78M2HC4A", "legalPerson": "陈云平", "registeredCapital": "壹佰万元整", "validFromDate": "20170104", "validPeriod": "2017年01月04日至长期", "validToDate": "29991231"}, "figure": \[{"box": {"angle": -90, "h": 109, "w": 108, "x": 434, "y": 695}, "h": 109, "points": \[{"x": 380, "y": 641}, {"x": 489, "y": 642}, {"x": 488, "y": 749}, {"x": 380, "y": 749}\], "type": "round\_stamp", "w": 110, "x": 380, "y": 641}, {"box": {"angle": -90, "h": 114, "w": 114, "x": 422, "y": 129}, "h": 115, "points": \[{"x": 365, "y": 72}, {"x": 479, "y": 72}, {"x": 479, "y": 186}, {"x": 365, "y": 186}\], "type": "round\_stamp", "w": 115, "x": 365, "y": 72}, {"box": {"angle": -90, "h": 94, "w": 93, "x": 100, "y": 635}, "h": 96, "points": \[{"x": 53, "y": 589}, {"x": 147, "y": 589}, {"x": 148, "y": 683}, {"x": 53, "y": 683}\], "type": "qrcode", "w": 96, "x": 53, "y": 588}, {"box": {"angle": -90, "h": 100, "w": 108, "x": 273, "y": 127}, "h": 109, "points": \[{"x": 223, "y": 73}, {"x": 323, "y": 73}, {"x": 323, "y": 181}, {"x": 223, "y": 181}\], "type": "national\_emblem", "w": 101, "x": 223, "y": 73}, {"box": {"angle": -90, "h": 301, "w": 61, "x": 273, "y": 227}, "h": 62, "points": \[{"x": 123, "y": 197}, {"x": 424, "y": 197}, {"x": 424, "y": 257}, {"x": 123, "y": 258}\], "type": "blicense\_title", "w": 302, "x": 123, "y": 197}\], "ftype": 1, "height": 829, "orgHeight": 829, "orgWidth": 564, "prism\_keyValueInfo": \[{"key": "creditCode", "keyProb": 100, "value": "913301095U78M2HC4A", "valuePos": \[{"x": 334, "y": 263}, {"x": 498, "y": 263}, {"x": 498, "y": 276}, {"x": 334, "y": 276}\], "valueProb": 100}, {"key": "companyName", "keyProb": 100, "value": "杭州橘子文化传媒有限公司", "valuePos": \[{"x": 162, "y": 321}, {"x": 322, "y": 321}, {"x": 322, "y": 336}, {"x": 162, "y": 336}\], "valueProb": 100}, {"key": "companyType", "keyProb": 100, "value": "有限责任公司(自然人投资或控股)", "valuePos": \[{"x": 162, "y": 343}, {"x": 377, "y": 343}, {"x": 377, "y": 359}, {"x": 162, "y": 359}\], "valueProb": 100}, {"key": "businessAddress", "keyProb": 100, "value": "萧山区宁围街道泰宏巷40号联合中心北区", "valuePos": \[{"x": 162, "y": 360}, {"x": 383, "y": 360}, {"x": 383, "y": 374}, {"x": 162, "y": 374}\], "valueProb": 100}, {"key": "legalPerson", "keyProb": 100, "value": "陈云平", "valuePos": \[{"x": 163, "y": 390}, {"x": 209, "y": 390}, {"x": 209, "y": 406}, {"x": 163, "y": 406}\], "valueProb": 100}, {"key": "businessScope", "keyProb": 100, "value": "影视文化艺术活动策划,艺术造型、美术设计,影视道具与服装设计:影视制作技术的研发;会议及展览服务;企业形象策划、影视文化信息咨询、摄影、摄像服务(除冲扩):设计、制作、代理国内广告(除网络广告):艺人经纪服务(营业性演出除外):公关策划:网站建设、软硬件开发维护、技术服务;销售:化妆品(除分装)、日用百货、服装、玩具、母婴用品(除食品药品)、第二类医疗器械\*\*(依法须经批准的项目,经相关部门批准后方可开展经营活动)", "valuePos": \[{"x": 164, "y": 486}, {"x": 810, "y": 486}, {"x": 810, "y": 621}, {"x": 164, "y": 621}\], "valueProb": 99}, {"key": "registeredCapital", "keyProb": 100, "value": "壹佰万元整", "valuePos": \[{"x": 163, "y": 415}, {"x": 228, "y": 415}, {"x": 228, "y": 431}, {"x": 163, "y": 431}\], "valueProb": 100}, {"key": "RegistrationDate", "keyProb": 100, "value": "2017年01月04日", "valuePos": \[{"x": 162, "y": 441}, {"x": 278, "y": 440}, {"x": 278, "y": 454}, {"x": 163, "y": 456}\], "valueProb": 100}, {"key": "validPeriod", "keyProb": 100, "value": "2017年01月04日至长期", "valuePos": \[{"x": 163, "y": 464}, {"x": 334, "y": 464}, {"x": 334, "y": 480}, {"x": 163, "y": 480}\], "valueProb": 100}, {"key": "validFromDate", "keyProb": 100, "value": "20170104", "valuePos": \[{"x": 163, "y": 464}, {"x": 334, "y": 464}, {"x": 334, "y": 480}, {"x": 163, "y": 480}\], "valueProb": 100}, {"key": "validToDate", "keyProb": 100, "value": "29991231", "valuePos": \[{"x": 163, "y": 464}, {"x": 334, "y": 464}, {"x": 334, "y": 480}, {"x": 163, "y": 480}\], "valueProb": 100}, {"key": "companyForm", "keyProb": 100, "value": "", "valueProb": 100}\], "sliceRect": {"x0": 9, "x1": 536, "x2": 538, "x3": 11, "y0": 28, "y1": 28, "y2": 782, "y3": 781}, "width": 564} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| figure | list | 图片中的图案信息。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
| ftype | int | 是否为复印件（1：是，0：否）。 |
| sliceRect | list | 检测出的子图坐标信息。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 结构化信息（data 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| creditCode | string | 统一社会信用代码。 |
| companyName | string | 营业名称。 |
| companyType | string | 类型。 |
| businessAddress | string | 营业场所/住所。 |
| legalPerson | string | 法人/负责人。 |
| businessScope | string | 经营范围。 |
| registeredCapital | string | 注册资本。 |
| RegistrationDate | string | 注册日期。 |
| validPeriod | string | 营业期限。 |
| validFromDate | string | 格式化营业期限起始日期。 |
| validToDate | string | 格式化营业期限终止日期。 |
| companyForm | string | 组成形式。 |
| issueDate | string | 发照日期。 |
| title | string | 证照标题。 |

#### 结构化坐标信息（prism\_keyValueInfo 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| key | string | 识别出的字段名称。 |
| keyProb | int | 字段名称置信度。 |
| value | string | 识别出的字段名称对应的值。 |
| valueProb | int | 字段名称对应值的置信度。 |
| valuePos | list | 字段在原图中的四个点坐标（左上、右上、右下、左下）。 |

#### 图案位置信息（figure 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| type | string | 图案类型。 |
| x | int | 图案左上角横坐标。 |
| y | int | 图案左上角纵坐标。 |
| w | int | 图案宽度。 |
| h | int | 图案高度。 |
| box | object | 图案坐标信息：中心横纵坐标，长宽，顺时针旋转角度。定义同 OpenCV 中 RotatedRect，请参见 [OpenCV 文档](https://docs.opencv.org/3.4/db/dd6/classcv_1_1RotatedRect.html#a6bd95a46f9ab83a4f384a4d4845e6332)。 |
| points | list | 图案四个点坐标（左上、右上、右下、左下）。 |

## 示例

正常返回示例

`JSON`格式

```
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "algo_version": "5f161015b0f3e48197b049a587c5b2468d8d0cb9;0c879a80496474870d0b1ff89f9c58fe6a53651d",
    "codes": [\
      {\
        "data": "",\
        "points": [\
          {\
            "x": 42,\
            "y": 558\
          },\
          {\
            "x": 142,\
            "y": 558\
          },\
          {\
            "x": 142,\
            "y": 659\
          },\
          {\
            "x": 42,\
            "y": 659\
          }\
        ],\
        "type": "QRcode"\
      }\
    ],
    "data": {
      "RegistrationDate": "2017年01月04日",
      "businessAddress": "萧山区宁围街道泰宏巷40号联合中心北区",
      "businessScope": "影视文化艺术活动策划,艺术造型、美术设计,影视道具与服装设计:影视制作技术的研发;会议及展览服务;企业形象策划、影视文化信息咨询、摄影、摄像服务(除冲扩):设计、制作、代理国内广告(除网络广告):艺人经纪服务(营业性演出除外):公关策划:网站建设、软硬件开发维护、技术服务;销售:化妆品(除分装)、日用百货、服装、玩具、母婴用品(除食品药品)、第二类医疗器械**(依法须经批准的项目,经相关部门批准后方可开展经营活动)",
      "companyForm": "",
      "companyName": "杭州橘子文化传媒有限公司",
      "companyType": "有限责任公司(自然人投资或控股)",
      "creditCode": "913301095U78M2HC4A",
      "legalPerson": "陈云平",
      "registeredCapital": "壹佰万元整",
      "validFromDate": 20170104,
      "validPeriod": "2017年01月04日至长期",
      "validToDate": 29991231
    },
    "figure": [\
      {\
        "box": {\
          "angle": -90,\
          "h": 109,\
          "w": 108,\
          "x": 434,\
          "y": 695\
        },\
        "h": 109,\
        "points": [\
          {\
            "x": 380,\
            "y": 641\
          },\
          {\
            "x": 489,\
            "y": 642\
          },\
          {\
            "x": 488,\
            "y": 749\
          },\
          {\
            "x": 380,\
            "y": 749\
          }\
        ],\
        "type": "round_stamp",\
        "w": 110,\
        "x": 380,\
        "y": 641\
      },\
      {\
        "box": {\
          "angle": -90,\
          "h": 114,\
          "w": 114,\
          "x": 422,\
          "y": 129\
        },\
        "h": 115,\
        "points": [\
          {\
            "x": 365,\
            "y": 72\
          },\
          {\
            "x": 479,\
            "y": 72\
          },\
          {\
            "x": 479,\
            "y": 186\
          },\
          {\
            "x": 365,\
            "y": 186\
          }\
        ],\
        "type": "round_stamp",\
        "w": 115,\
        "x": 365,\
        "y": 72\
      },\
      {\
        "box": {\
          "angle": -90,\
          "h": 94,\
          "w": 93,\
          "x": 100,\
          "y": 635\
        },\
        "h": 96,\
        "points": [\
          {\
            "x": 53,\
            "y": 589\
          },\
          {\
            "x": 147,\
            "y": 589\
          },\
          {\
            "x": 148,\
            "y": 683\
          },\
          {\
            "x": 53,\
            "y": 683\
          }\
        ],\
        "type": "qrcode",\
        "w": 96,\
        "x": 53,\
        "y": 588\
      },\
      {\
        "box": {\
          "angle": -90,\
          "h": 100,\
          "w": 108,\
          "x": 273,\
          "y": 127\
        },\
        "h": 109,\
        "points": [\
          {\
            "x": 223,\
            "y": 73\
          },\
          {\
            "x": 323,\
            "y": 73\
          },\
          {\
            "x": 323,\
            "y": 181\
          },\
          {\
            "x": 223,\
            "y": 181\
          }\
        ],\
        "type": "national_emblem",\
        "w": 101,\
        "x": 223,\
        "y": 73\
      },\
      {\
        "box": {\
          "angle": -90,\
          "h": 301,\
          "w": 61,\
          "x": 273,\
          "y": 227\
        },\
        "h": 62,\
        "points": [\
          {\
            "x": 123,\
            "y": 197\
          },\
          {\
            "x": 424,\
            "y": 197\
          },\
          {\
            "x": 424,\
            "y": 257\
          },\
          {\
            "x": 123,\
            "y": 258\
          }\
        ],\
        "type": "blicense_title",\
        "w": 302,\
        "x": 123,\
        "y": 197\
      }\
    ],
    "ftype": 1,
    "height": 829,
    "orgHeight": 829,
    "orgWidth": 564,
    "prism_keyValueInfo": [\
      {\
        "key": "creditCode",\
        "keyProb": 100,\
        "value": "913301095U78M2HC4A",\
        "valuePos": [\
          {\
            "x": 334,\
            "y": 263\
          },\
          {\
            "x": 498,\
            "y": 263\
          },\
          {\
            "x": 498,\
            "y": 276\
          },\
          {\
            "x": 334,\
            "y": 276\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "companyName",\
        "keyProb": 100,\
        "value": "杭州橘子文化传媒有限公司",\
        "valuePos": [\
          {\
            "x": 162,\
            "y": 321\
          },\
          {\
            "x": 322,\
            "y": 321\
          },\
          {\
            "x": 322,\
            "y": 336\
          },\
          {\
            "x": 162,\
            "y": 336\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "companyType",\
        "keyProb": 100,\
        "value": "有限责任公司(自然人投资或控股)",\
        "valuePos": [\
          {\
            "x": 162,\
            "y": 343\
          },\
          {\
            "x": 377,\
            "y": 343\
          },\
          {\
            "x": 377,\
            "y": 359\
          },\
          {\
            "x": 162,\
            "y": 359\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "businessAddress",\
        "keyProb": 100,\
        "value": "萧山区宁围街道泰宏巷40号联合中心北区",\
        "valuePos": [\
          {\
            "x": 162,\
            "y": 360\
          },\
          {\
            "x": 383,\
            "y": 360\
          },\
          {\
            "x": 383,\
            "y": 374\
          },\
          {\
            "x": 162,\
            "y": 374\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "legalPerson",\
        "keyProb": 100,\
        "value": "陈云平",\
        "valuePos": [\
          {\
            "x": 163,\
            "y": 390\
          },\
          {\
            "x": 209,\
            "y": 390\
          },\
          {\
            "x": 209,\
            "y": 406\
          },\
          {\
            "x": 163,\
            "y": 406\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "businessScope",\
        "keyProb": 100,\
        "value": "影视文化艺术活动策划,艺术造型、美术设计,影视道具与服装设计:影视制作技术的研发;会议及展览服务;企业形象策划、影视文化信息咨询、摄影、摄像服务(除冲扩):设计、制作、代理国内广告(除网络广告):艺人经纪服务(营业性演出除外):公关策划:网站建设、软硬件开发维护、技术服务;销售:化妆品(除分装)、日用百货、服装、玩具、母婴用品(除食品药品)、第二类医疗器械**(依法须经批准的项目,经相关部门批准后方可开展经营活动)",\
        "valuePos": [\
          {\
            "x": 164,\
            "y": 486\
          },\
          {\
            "x": 810,\
            "y": 486\
          },\
          {\
            "x": 810,\
            "y": 621\
          },\
          {\
            "x": 164,\
            "y": 621\
          }\
        ],\
        "valueProb": 99\
      },\
      {\
        "key": "registeredCapital",\
        "keyProb": 100,\
        "value": "壹佰万元整",\
        "valuePos": [\
          {\
            "x": 163,\
            "y": 415\
          },\
          {\
            "x": 228,\
            "y": 415\
          },\
          {\
            "x": 228,\
            "y": 431\
          },\
          {\
            "x": 163,\
            "y": 431\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "RegistrationDate",\
        "keyProb": 100,\
        "value": "2017年01月04日",\
        "valuePos": [\
          {\
            "x": 162,\
            "y": 441\
          },\
          {\
            "x": 278,\
            "y": 440\
          },\
          {\
            "x": 278,\
            "y": 454\
          },\
          {\
            "x": 163,\
            "y": 456\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "validPeriod",\
        "keyProb": 100,\
        "value": "2017年01月04日至长期",\
        "valuePos": [\
          {\
            "x": 163,\
            "y": 464\
          },\
          {\
            "x": 334,\
            "y": 464\
          },\
          {\
            "x": 334,\
            "y": 480\
          },\
          {\
            "x": 163,\
            "y": 480\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "validFromDate",\
        "keyProb": 100,\
        "value": 20170104,\
        "valuePos": [\
          {\
            "x": 163,\
            "y": 464\
          },\
          {\
            "x": 334,\
            "y": 464\
          },\
          {\
            "x": 334,\
            "y": 480\
          },\
          {\
            "x": 163,\
            "y": 480\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "validToDate",\
        "keyProb": 100,\
        "value": 29991231,\
        "valuePos": [\
          {\
            "x": 163,\
            "y": 464\
          },\
          {\
            "x": 334,\
            "y": 464\
          },\
          {\
            "x": 334,\
            "y": 480\
          },\
          {\
            "x": 163,\
            "y": 480\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "companyForm",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 9,
      "x1": 536,
      "x2": 538,
      "x3": 11,
      "y0": 28,
      "y1": 28,
      "y2": 782,
      "y3": 781
    },
    "width": 564
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
| 2022-11-25 | API 内部配置变更，不影响调用 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeBusinessLicense?updateTime=2022-11-25#workbench-doc-change-demo) |
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeBusinessLicense?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/) [开发参考](https://help.aliyun.com/zh/ocr/developer-reference/) [API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/) [API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/) [企业资质识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-enterprise-qualification-identification/) RecognizeBusinessLicense - 营业执照识别

# RecognizeBusinessLicense - 营业执照识别

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：企业资质识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-enterprise-qualification-identification/)[下一篇：RecognizeBankAccountLicense - 银行开户许可证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizebankaccountlicense)

该文章对您有帮助吗？

反馈