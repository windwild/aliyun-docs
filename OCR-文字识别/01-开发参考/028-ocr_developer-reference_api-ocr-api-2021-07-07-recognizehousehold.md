可结构化识别户口常住人口登记卡页面及户主页的内容，有效识别户口本上的相关户籍证明信息。

## 接口说明

#### 本接口适用场景

- 阿里云户口本识别，是阿里云官方自研 OCR 文字识别产品，可用于识别户口本户主页的户主姓名、住址、户号等字段。也适用于识别户口本常住人口页的出生日期、出生地、姓名、民族等信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i2/O1CN01XgQQf11PBoxYZP19J_!!6000000001803-2-tps-2458-1318.png)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 总体识别准确率可达 98%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [个人证照识别](https://common-buy.aliyun.com/?commodityCode=ocr_personalcard_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=standard&subtype=household#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [个人证照识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_personalcard_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_personalcard_dp_cn_20211018150333_0555%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeHousehold?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。<br>- 图片尺寸过小，会影响识别精度。图片内单字大小在 10-50px 内时，识别效果较好。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeHousehold)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeHousehold)

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
| ocr:RecognizeHousehold |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/tfs/TB11ZxTMxD1gK0jSZFsXXbldVXa-920-606.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |
| IsResidentPage | boolean | 否 | - 是否是户口本常住人口页，默认为否。<br>- true：需要；false：不需要。 | false |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"angle": 0, "data": {"sectionNo": "4401030023005", "householdType": "居民户口家庭户", "householderName": "张无忌", "householderCommunity": "", "householdNumber": "000028901", "address": "广东省广州市荔湾区芳村大道中350号", "Registrar": "罗敏", "issueDate": "2012年04月17日"}, "ftype": 0, "height": 606, "orgHeight": 606, "orgWidth": 920, "prism\_keyValueInfo": \[{"key": "sectionNo", "keyProb": 100, "value": "4401030023005", "valuePos": \[{"x": 106, "y": 5}, {"x": 289, "y": 4}, {"x": 289, "y": 28}, {"x": 107, "y": 30}\], "valueProb": 100}, {"key": "householdType", "keyProb": 100, "value": "居民户口家庭户", "valuePos": \[{"x": 137, "y": 46}, {"x": 317, "y": 43}, {"x": 317, "y": 73}, {"x": 138, "y": 76}\], "valueProb": 100}, {"key": "householderName", "keyProb": 100, "value": "张无忌", "valuePos": \[{"x": 523, "y": 48}, {"x": 523, "y": 74}, {"x": 457, "y": 74}, {"x": 457, "y": 48}\], "valueProb": 100}, {"key": "householderCommunity", "keyProb": 100, "value": "", "valueProb": 100}, {"key": "householdNumber", "keyProb": 100, "value": "000028901", "valuePos": \[{"x": 225, "y": 108}, {"x": 225, "y": 126}, {"x": 145, "y": 126}, {"x": 145, "y": 108}\], "valueProb": 100}, {"key": "address", "keyProb": 100, "value": "广东省广州市荔湾区芳村大道中350号", "valuePos": \[{"x": 379, "y": 88}, {"x": 807, "y": 84}, {"x": 807, "y": 114}, {"x": 379, "y": 119}\], "valueProb": 100}, {"key": "Registrar", "keyProb": 100, "value": "罗敏", "valuePos": \[{"x": 332, "y": 499}, {"x": 332, "y": 529}, {"x": 279, "y": 529}, {"x": 279, "y": 499}\], "valueProb": 100}, {"key": "issueDate", "keyProb": 100, "value": "2012年04月17日", "valuePos": \[{"x": 738, "y": 497}, {"x": 738, "y": 538}, {"x": 462, "y": 538}, {"x": 462, "y": 497}\], "valueProb": 100}\], "sliceRect": {"x0": 1, "y0": 7, "x1": 918, "y1": 4, "x2": 920, "y2": 600, "x3": 5, "y3": 606}, "width": 920} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

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

#### 结构化信息（户主页 _**data**_ 字段，当 **IsResidentPage** 不传或传 false。）

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| Registrar | string | 承办人签章。 |
| address | string | 住址。 |
| householdNumber | string | 户号。 |
| householdType | string | 户别。 |
| householderCommunity | string | 户主社区。 |
| householderName | string | 户主姓名。 |
| issueDate | string | 签发日期。 |
| sectionNo | string | 地段号。 |

#### 结构化信息（常住人口页 _**data**_ 字段，当 **IsResidentPage=true**。）

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| birthDate | string | 出生日期。 |
| birthPlace | string | 出生地。 |
| bloodGroup | string | 血型。 |
| educationalDegree | string | 文化程度。 |
| employer | string | 服务处所。 |
| ethnicity | string | 民族。 |
| formerName | string | 曾用名。 |
| householdNumber | string | 户号。 |
| idCardNumber | string | 身份证编号。 |
| immigratedToCityInfo | string | 何时何地迁来本市。 |
| immigratedToResidenceInfo | string | 何时由何地迁来本址。 |
| maritalStatus | string | 婚姻状况。 |
| militaryServiceStatus | string | 兵役状况。 |
| name | string | 姓名。 |
| nativePlace | string | 籍贯。 |
| occupation | string | 职业。 |
| otherResidence | string | 本市其他住址。 |
| registrar | string | 承办人签章。 |
| registrationDate | string | 登记日期。 |
| relation | string | 与户主关系。 |
| religious | string | 宗教信仰。 |
| sex | string | 性别。 |
| stature | string | 身高。 |

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
    "angle": 0,
    "data": {
      "sectionNo": 4401030023005,
      "householdType": "居民户口家庭户",
      "householderName": "张无忌",
      "householderCommunity": "",
      "householdNumber": "000028901",
      "address": "广东省广州市荔湾区芳村大道中350号",
      "Registrar": "罗敏",
      "issueDate": "2012年04月17日"
    },
    "ftype": 0,
    "height": 606,
    "orgHeight": 606,
    "orgWidth": 920,
    "prism_keyValueInfo": [\
      {\
        "key": "sectionNo",\
        "keyProb": 100,\
        "value": 4401030023005,\
        "valuePos": [\
          {\
            "x": 106,\
            "y": 5\
          },\
          {\
            "x": 289,\
            "y": 4\
          },\
          {\
            "x": 289,\
            "y": 28\
          },\
          {\
            "x": 107,\
            "y": 30\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "householdType",\
        "keyProb": 100,\
        "value": "居民户口家庭户",\
        "valuePos": [\
          {\
            "x": 137,\
            "y": 46\
          },\
          {\
            "x": 317,\
            "y": 43\
          },\
          {\
            "x": 317,\
            "y": 73\
          },\
          {\
            "x": 138,\
            "y": 76\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "householderName",\
        "keyProb": 100,\
        "value": "张无忌",\
        "valuePos": [\
          {\
            "x": 523,\
            "y": 48\
          },\
          {\
            "x": 523,\
            "y": 74\
          },\
          {\
            "x": 457,\
            "y": 74\
          },\
          {\
            "x": 457,\
            "y": 48\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "householderCommunity",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "householdNumber",\
        "keyProb": 100,\
        "value": "000028901",\
        "valuePos": [\
          {\
            "x": 225,\
            "y": 108\
          },\
          {\
            "x": 225,\
            "y": 126\
          },\
          {\
            "x": 145,\
            "y": 126\
          },\
          {\
            "x": 145,\
            "y": 108\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "address",\
        "keyProb": 100,\
        "value": "广东省广州市荔湾区芳村大道中350号",\
        "valuePos": [\
          {\
            "x": 379,\
            "y": 88\
          },\
          {\
            "x": 807,\
            "y": 84\
          },\
          {\
            "x": 807,\
            "y": 114\
          },\
          {\
            "x": 379,\
            "y": 119\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "Registrar",\
        "keyProb": 100,\
        "value": "罗敏",\
        "valuePos": [\
          {\
            "x": 332,\
            "y": 499\
          },\
          {\
            "x": 332,\
            "y": 529\
          },\
          {\
            "x": 279,\
            "y": 529\
          },\
          {\
            "x": 279,\
            "y": 499\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "issueDate",\
        "keyProb": 100,\
        "value": "2012年04月17日",\
        "valuePos": [\
          {\
            "x": 738,\
            "y": 497\
          },\
          {\
            "x": 738,\
            "y": 538\
          },\
          {\
            "x": 462,\
            "y": 538\
          },\
          {\
            "x": 462,\
            "y": 497\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 1,
      "y0": 7,
      "x1": 918,
      "y1": 4,
      "x2": 920,
      "y2": 600,
      "x3": 5,
      "y3": 606
    },
    "width": 920
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
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeHousehold?updateTime=2021-08-17#workbench-doc-change-demo) |

SDK 调用
通过 SDK 调用此接口的示例请参考 [开发者中心](https://next.api.aliyun.com/api-tools/sdk/ocr-api?version=2021-07-07&language=java-tea)

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/) [开发参考](https://help.aliyun.com/zh/ocr/developer-reference/) [API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/) [API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/) [个人证照识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-personal-license-identification/) RecognizeHousehold - 户口本识别

# RecognizeHousehold - 户口本识别

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizePassport - 国际护照识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizepassport)[下一篇：RecognizeEstateCertification - 不动产权证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeestatecertification)

该文章对您有帮助吗？

反馈