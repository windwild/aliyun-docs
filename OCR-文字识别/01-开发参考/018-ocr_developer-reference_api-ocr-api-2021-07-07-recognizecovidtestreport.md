支持对全国各地区不同版式的核酸检测记录中姓名、证件号码、采样日期、采样时间、检测机构、检测结果等6个关键字段的结构化结果输出。

## 接口说明

#### 本接口适用场景

- 阿里云核酸检测报告识别，是阿里云官方自研 OCR 文字识别产品，适用于识别核酸检测报告上的姓名、证件号码、采样时间、检测结果等关键信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i2/O1CN01qWUm4s1kF7eX52tJy_!!6000000004653-2-tps-1921-831.png)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |
| 图片格式 | 支持 PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。 |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 总体识别准确率可达 98%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [医疗场景识别](https://common-buy.aliyun.com/?commodityCode=ocr_medical_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=medicalCare&subtype=covid_test_report#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [核酸检测报告识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_medical_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_medical_dp_cn_20220506154332_0030%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCovidTestReport?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 接口响应速度和图片中的文字数量有关，如果图片中文字数量越多，接口响应可能越慢。<br>- 接口会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCovidTestReport)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCovidTestReport)

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
| ocr:RecognizeCovidTestReport | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | http://duguang-database-public.oss-cn-hangzhou.aliyuncs.com/covid\_init\_covid\_test\_report/test\_report\_\_data\_pool\_15a4f85478cb1bd69a5d631b182aba69.jpg\_item\_0\_cls\_covid\_test\_report.jpg |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |
| MultipleResult | boolean | 否 | - 当一张图有多个子图时，是否要返回多个识别结果,默认不需要。<br>- true：返回所有子图识别结果；false：返回检测日期最新的一个结果。 | false |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"data": {"name": "张德周", "idNumber": "612401\*\*\*\*\*\*\*\*22010", "samplingDate": "2022-03-30", "samplingTime": "330", "testOrganization": "", "testItem": "", "testResult": ""}, "ftype": 0, "height": 991, "orgHeight": 998, "orgWidth": 1076, "prism\_keyValueInfo": \[{"key": "name", "keyProb": 100, "value": "张德周", "valuePos": \[{"x": 291, "y": 465}, {"x": 473, "y": 463}, {"x": 474, "y": 526}, {"x": 291, "y": 527}\], "valueProb": 100}, {"key": "idNumber", "keyProb": 91, "value": "612401\*\*\*\*\*\*\*\*22010", "valuePos": \[{"x": 791, "y": 180}, {"x": 791, "y": 227}, {"x": 300, "y": 226}, {"x": 300, "y": 179}\], "valueProb": 91}, {"key": "samplingDate", "keyProb": 100, "value": "2022-03-30", "valuePos": \[{"x": 597, "y": 775}, {"x": 597, "y": 826}, {"x": 296, "y": 826}, {"x": 296, "y": 775}\], "valueProb": 100}, {"key": "samplingTime", "keyProb": 100, "value": "330", "valuePos": \[{"x": 412, "y": 684}, {"x": 413, "y": 741}, {"x": 268, "y": 742}, {"x": 268, "y": 686}\], "valueProb": 100}, {"key": "testOrganization", "keyProb": 100, "value": "", "valueProb": 100}, {"key": "testItem", "keyProb": 100, "value": "", "valueProb": 100}, {"key": "testResult", "keyProb": 28, "value": "", "valuePos": \[{"x": 417, "y": 873}, {"x": 417, "y": 941}, {"x": 298, "y": 941}, {"x": 298, "y": 873}\], "valueProb": 28}\], "sliceRect": {"x0": 0, "y0": 10, "x1": 1076, "y1": 6, "x2": 1076, "y2": 995, "x3": 0, "y3": 996}, "width": 1076} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| sliceRect | list | 结构化信息的坐标信息。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
| ftype | int | 是否为复印件（1：是，0：否）。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 结构化信息（data 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| name | string | 姓名。 |
| idNumber | string | 证件号码。 |
| samplingDate | string | 采样日期。 |
| samplingTime | string | 采样时间。 |
| testOrganization | string | 检测机构。 |
| testItem | string | 检测项目。 |
| testResult | string | 检测结果。 |

#### 结构化坐标信息（prism\_keyValueInfo 字段）

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

```
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "data": {
      "name": "张德周",
      "idNumber": "612401********22010",
      "samplingDate": "2022-03-30",
      "samplingTime": 330,
      "testOrganization": "",
      "testItem": "",
      "testResult": ""
    },
    "ftype": 0,
    "height": 991,
    "orgHeight": 998,
    "orgWidth": 1076,
    "prism_keyValueInfo": [\
      {\
        "key": "name",\
        "keyProb": 100,\
        "value": "张德周",\
        "valuePos": [\
          {\
            "x": 291,\
            "y": 465\
          },\
          {\
            "x": 473,\
            "y": 463\
          },\
          {\
            "x": 474,\
            "y": 526\
          },\
          {\
            "x": 291,\
            "y": 527\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "idNumber",\
        "keyProb": 91,\
        "value": "612401********22010",\
        "valuePos": [\
          {\
            "x": 791,\
            "y": 180\
          },\
          {\
            "x": 791,\
            "y": 227\
          },\
          {\
            "x": 300,\
            "y": 226\
          },\
          {\
            "x": 300,\
            "y": 179\
          }\
        ],\
        "valueProb": 91\
      },\
      {\
        "key": "samplingDate",\
        "keyProb": 100,\
        "value": "2022-03-30",\
        "valuePos": [\
          {\
            "x": 597,\
            "y": 775\
          },\
          {\
            "x": 597,\
            "y": 826\
          },\
          {\
            "x": 296,\
            "y": 826\
          },\
          {\
            "x": 296,\
            "y": 775\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "samplingTime",\
        "keyProb": 100,\
        "value": 330,\
        "valuePos": [\
          {\
            "x": 412,\
            "y": 684\
          },\
          {\
            "x": 413,\
            "y": 741\
          },\
          {\
            "x": 268,\
            "y": 742\
          },\
          {\
            "x": 268,\
            "y": 686\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "testOrganization",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "testItem",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "testResult",\
        "keyProb": 28,\
        "value": "",\
        "valuePos": [\
          {\
            "x": 417,\
            "y": 873\
          },\
          {\
            "x": 417,\
            "y": 941\
          },\
          {\
            "x": 298,\
            "y": 941\
          },\
          {\
            "x": 298,\
            "y": 873\
          }\
        ],\
        "valueProb": 28\
      }\
    ],
    "sliceRect": {
      "x0": 0,
      "y0": 10,
      "x1": 1076,
      "y1": 6,
      "x2": 1076,
      "y2": 995,
      "x3": 0,
      "y3": 996
    },
    "width": 1076
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
| 2022-11-25 | API 内部配置变更，不影响调用 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeCovidTestReport?updateTime=2022-11-25#workbench-doc-change-demo) |
| 2022-06-19 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeCovidTestReport?updateTime=2022-06-19#workbench-doc-change-demo) |
| 2022-05-30 | 新增 OpenAPI | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeCovidTestReport?updateTime=2022-05-30#workbench-doc-change-demo) |

SDK 调用
通过 SDK 调用此接口的示例请参考 [开发者中心](https://next.api.aliyun.com/api-tools/sdk/ocr-api?version=2021-07-07&language=java-tea)

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/) [开发参考](https://help.aliyun.com/zh/ocr/developer-reference/) [API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/) [API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/) [医疗场景识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-medical-scene-recognition/) RecognizeCovidTestReport - 核酸检测报告识别

# RecognizeCovidTestReport - 核酸检测报告识别

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：医疗场景识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-medical-scene-recognition/)[下一篇：票证核验](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-ticket-verification/)

该文章对您有帮助吗？

反馈