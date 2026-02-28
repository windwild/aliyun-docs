支持对行驶证正页、副页关键字段的自动定位和识别，同时也支持对正副页在同一张图片的场景进行自动分割与结构化识别。

## 接口说明

#### 本接口适用场景

- 阿里云行驶证识别，是阿里云官方自研 OCR 文字识别产品，精准定位和识别行驶证正、副页所包含的关键信息，支持正副页在同一张图片的场景进行自动分割与结构化识别。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i2/O1CN01ZihUIy1bCzJiSNPrk_!!6000000003430-0-tps-1323-828.jpg)

![](https://img.alicdn.com/imgextra/i2/O1CN017IZ97Q1TdzkT25B2F_!!6000000002406-0-tps-989-517.jpg)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |

| 分类 | 概述 |
| --- | --- |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 行驶证混贴 | 支持对正副页在同一张图片的场景进行自动分割与结构化识别。 |
| 高精度识别 | 总体准确率达 93%以上。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [车辆物流识别](https://common-buy.aliyun.com/?commodityCode=ocr_logistics_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=logistics&subtype=vehicle_license#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [行驶证识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_logistics_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_logistics_dp_cn_20211103160032_0739%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeVehicleLicense?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 国家与语言 | - 本接口只支持中国行驶证。 |
| 其他提示 | - 请保证整张行驶证内容及其边缘包含在图像内。 <br>- 本能力会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |
| 相关能力 | - [行驶证识别。](https://market.aliyun.com/products/57124001/cmapi011791.html?spm=5176.730005.result.13.291d3524fc1E2j&innerSource=search_%E8%A1%8C%E9%A9%B6%E8%AF%81#sku=yuncode579100000) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeVehicleLicense)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeVehicleLicense)

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
| ocr:RecognizeVehicleLicense |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241223/bzyhho/%E8%A1%8C%E9%A9%B6%E8%AF%81%E8%AF%86%E5%88%AB.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"algo\_version":"7a6241b9ccce3746da42ff09ee692b27721728bb","data":{"face":{"algo\_version":"1cef3d8e5c2d82e6180feca6bba3591559c2dc55","angle":0,"data":{"address":"成都市龙泉驿区山泉镇联合村","engineNumber":"8B213508","issueDate":"2015-06-04","model":"北京现代牌BH7164MX","owner":"叶晴晴","licensePlateNumber":"川A7809C","registrationDate":"2008-07-08","useNature":"非营运","vehicleType":"小型轿车","vinCode":"LBEHDAEB58Y038860","issueAuthority":"四川省成都市公安局交通警察支队"},"ftype":0,"height":293,"orgHeight":293,"orgWidth":427,"prism\_keyValueInfo":\[{"key":"address","keyProb":100,"value":"成都市龙泉驿区山泉镇联合村","valuePos":\[{"x":79,"y":121},{"x":323,"y":125},{"x":322,"y":144},{"x":79,"y":139}\],"valueProb":100},{"key":"engineNumber","keyProb":99,"value":"8B213508","valuePos":\[{"x":201,"y":228},{"x":277,"y":230},{"x":277,"y":246},{"x":200,"y":244}\],"valueProb":99},{"key":"issueDate","keyProb":100,"value":"2015-06-04","valuePos":\[{"x":325,"y":266},{"x":419,"y":268},{"x":419,"y":286},{"x":324,"y":283}\],"valueProb":100},{"key":"model","keyProb":100,"value":"北京现代牌BH7164MX","valuePos":\[{"x":228,"y":159},{"x":398,"y":161},{"x":397,"y":180},{"x":227,"y":177}\],"valueProb":100},{"key":"owner","keyProb":100,"value":"叶晴晴","valuePos":\[{"x":80,"y":85},{"x":131,"y":85},{"x":131,"y":103},{"x":80,"y":103}\],"valueProb":100},{"key":"licensePlateNumber","keyProb":100,"value":"川A7809C","valuePos":\[{"x":81,"y":52},{"x":160,"y":52},{"x":160,"y":71},{"x":81,"y":71}\],"valueProb":100},{"key":"registrationDate","keyProb":100,"value":"2008-07-08","valuePos":\[{"x":175,"y":262},{"x":269,"y":265},{"x":269,"y":282},{"x":174,"y":278}\],"valueProb":100},{"key":"useNature","keyProb":100,"value":"非营运","valuePos":\[{"x":80,"y":155},{"x":135,"y":156},{"x":134,"y":175},{"x":79,"y":174}\],"valueProb":100},{"key":"vehicleType","keyProb":100,"value":"小型轿车","valuePos":\[{"x":268,"y":53},{"x":343,"y":56},{"x":342,"y":75},{"x":267,"y":73}\],"valueProb":100},{"key":"vinCode","keyProb":100,"value":"LBEHDAEB58Y038860","valuePos":\[{"x":215,"y":192},{"x":375,"y":196},{"x":375,"y":214},{"x":214,"y":209}\],"valueProb":100},{"key":"issueAuthority","keyProb":100,"value":"四川省成都市公安局交通警察支队","valuePos":\[{"x":17,"y":190},{"x":102,"y":190},{"x":102,"y":271},{"x":17,"y":271}\],"valueProb":100}\],"sliceRect":{"x0":0,"y0":0,"x1":427,"y1":0,"x2":427,"y2":293,"x3":0,"y3":293},"width":427}},"height":293,"orgHeight":293,"orgWidth":427,"width":427} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息，正面为 face 字段，反面为 back 字段。 |
| sliceRect | list | 检测出的子图坐标信息。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
| ftype | int | 是否为复印件（1：是，0：否）。 |
| angle | int | 图片的角度，0 表示正向，90 表示图片朝右，180 朝下，270 朝左。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 正面识别结果（face 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| address | string | 住址。 |
| engineNumber | string | 发动机号码。 |
| issueDate | string | 发证日期。 |
| model | string | 品牌型号。 |
| owner | string | 所有人。 |
| licensePlateNumber | string | 号牌号码。 |
| registrationDate | string | 注册日期。 |
| useNature | string | 使用性质。 |
| vehicleType | string | 车辆类型。 |
| vinCode | string | 车辆识别代码。 |
| issueAuthority | string | 签发机关。 |

#### 反面识别结果（back 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| licensePlateNumber | string | 号牌号码。 |
| inspectionRecord | string | 检验记录。 |
| passengerCapacity | string | 核定载人数。 |
| totalWeight | string | 总质量。 |
| curbWeight | string | 整备质量。 |
| permittedWeight | string | 核定载质量。 |
| overallDimension | string | 外廓尺寸。 |
| tractionWeight | string | 准牵引总质量。 |
| energySign | string | 能源标志。 |
| recordNumber | string | 档案编号。 |
| remarks | string | 备注。 |
| barcodeNumber | string | 条形码编号。 |

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
    "algo_version": "7a6241b9ccce3746da42ff09ee692b27721728bb",
    "data": {
      "face": {
        "algo_version": "1cef3d8e5c2d82e6180feca6bba3591559c2dc55",
        "angle": 0,
        "data": {
          "address": "成都市龙泉驿区山泉镇联合村",
          "engineNumber": "8B213508",
          "issueDate": "2015-06-04",
          "model": "北京现代牌BH7164MX",
          "owner": "叶晴晴",
          "licensePlateNumber": "川A7809C",
          "registrationDate": "2008-07-08",
          "useNature": "非营运",
          "vehicleType": "小型轿车",
          "vinCode": "LBEHDAEB58Y038860",
          "issueAuthority": "四川省成都市公安局交通警察支队"
        },
        "ftype": 0,
        "height": 293,
        "orgHeight": 293,
        "orgWidth": 427,
        "prism_keyValueInfo": [\
          {\
            "key": "address",\
            "keyProb": 100,\
            "value": "成都市龙泉驿区山泉镇联合村",\
            "valuePos": [\
              {\
                "x": 79,\
                "y": 121\
              },\
              {\
                "x": 323,\
                "y": 125\
              },\
              {\
                "x": 322,\
                "y": 144\
              },\
              {\
                "x": 79,\
                "y": 139\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "engineNumber",\
            "keyProb": 99,\
            "value": "8B213508",\
            "valuePos": [\
              {\
                "x": 201,\
                "y": 228\
              },\
              {\
                "x": 277,\
                "y": 230\
              },\
              {\
                "x": 277,\
                "y": 246\
              },\
              {\
                "x": 200,\
                "y": 244\
              }\
            ],\
            "valueProb": 99\
          },\
          {\
            "key": "issueDate",\
            "keyProb": 100,\
            "value": "2015-06-04",\
            "valuePos": [\
              {\
                "x": 325,\
                "y": 266\
              },\
              {\
                "x": 419,\
                "y": 268\
              },\
              {\
                "x": 419,\
                "y": 286\
              },\
              {\
                "x": 324,\
                "y": 283\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "model",\
            "keyProb": 100,\
            "value": "北京现代牌BH7164MX",\
            "valuePos": [\
              {\
                "x": 228,\
                "y": 159\
              },\
              {\
                "x": 398,\
                "y": 161\
              },\
              {\
                "x": 397,\
                "y": 180\
              },\
              {\
                "x": 227,\
                "y": 177\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "owner",\
            "keyProb": 100,\
            "value": "叶晴晴",\
            "valuePos": [\
              {\
                "x": 80,\
                "y": 85\
              },\
              {\
                "x": 131,\
                "y": 85\
              },\
              {\
                "x": 131,\
                "y": 103\
              },\
              {\
                "x": 80,\
                "y": 103\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "licensePlateNumber",\
            "keyProb": 100,\
            "value": "川A7809C",\
            "valuePos": [\
              {\
                "x": 81,\
                "y": 52\
              },\
              {\
                "x": 160,\
                "y": 52\
              },\
              {\
                "x": 160,\
                "y": 71\
              },\
              {\
                "x": 81,\
                "y": 71\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "registrationDate",\
            "keyProb": 100,\
            "value": "2008-07-08",\
            "valuePos": [\
              {\
                "x": 175,\
                "y": 262\
              },\
              {\
                "x": 269,\
                "y": 265\
              },\
              {\
                "x": 269,\
                "y": 282\
              },\
              {\
                "x": 174,\
                "y": 278\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "useNature",\
            "keyProb": 100,\
            "value": "非营运",\
            "valuePos": [\
              {\
                "x": 80,\
                "y": 155\
              },\
              {\
                "x": 135,\
                "y": 156\
              },\
              {\
                "x": 134,\
                "y": 175\
              },\
              {\
                "x": 79,\
                "y": 174\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "vehicleType",\
            "keyProb": 100,\
            "value": "小型轿车",\
            "valuePos": [\
              {\
                "x": 268,\
                "y": 53\
              },\
              {\
                "x": 343,\
                "y": 56\
              },\
              {\
                "x": 342,\
                "y": 75\
              },\
              {\
                "x": 267,\
                "y": 73\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "vinCode",\
            "keyProb": 100,\
            "value": "LBEHDAEB58Y038860",\
            "valuePos": [\
              {\
                "x": 215,\
                "y": 192\
              },\
              {\
                "x": 375,\
                "y": 196\
              },\
              {\
                "x": 375,\
                "y": 214\
              },\
              {\
                "x": 214,\
                "y": 209\
              }\
            ],\
            "valueProb": 100\
          },\
          {\
            "key": "issueAuthority",\
            "keyProb": 100,\
            "value": "四川省成都市公安局交通警察支队",\
            "valuePos": [\
              {\
                "x": 17,\
                "y": 190\
              },\
              {\
                "x": 102,\
                "y": 190\
              },\
              {\
                "x": 102,\
                "y": 271\
              },\
              {\
                "x": 17,\
                "y": 271\
              }\
            ],\
            "valueProb": 100\
          }\
        ],
        "sliceRect": {
          "x0": 0,
          "y0": 0,
          "x1": 427,
          "y1": 0,
          "x2": 427,
          "y2": 293,
          "x3": 0,
          "y3": 293
        },
        "width": 427
      }
    },
    "height": 293,
    "orgHeight": 293,
    "orgWidth": 427,
    "width": 427
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
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeVehicleLicense?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[车辆物流识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-vehicle-logistics-identification/)RecognizeVehicleLicense - 行驶证识别

# RecognizeVehicleLicense - 行驶证识别

更新时间：2025-12-08 21:11:03

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeInternationalBusinessLicense - 国际企业执照识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeinternationalbusinesslicense)[下一篇：RecognizeDrivingLicense - 驾驶证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizedrivinglicense)

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