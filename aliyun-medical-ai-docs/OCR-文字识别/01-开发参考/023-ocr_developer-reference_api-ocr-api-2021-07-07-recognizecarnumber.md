可有效识别车辆车牌信息，支持机动车车牌、摩托车车牌以及临时车牌。

## 接口说明

#### 本接口适用场景

- 阿里云车牌识别，是阿里云官方自研 OCR 文字识别产品，可有效识别车辆车牌信息，支持多车牌以及多类车型检测识别。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i1/O1CN01ornmBX24I8d09nFQV_!!6000000007367-0-tps-661-264.jpg)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |

| 分类 | 概述 |
| --- | --- |
| 多地区车牌识别 | 浙、苏、赣、黑、鄂、川、甘、陕、吉、辽、闽、皖等。 |
| 多车型识别 | 大型汽车、小型汽车、新能源车、挂车、临时车牌、警车、军车、使领馆车、教练车、港澳车。 |
| 使用场景 | 广泛应用于车辆安防检控、车辆出入识别等场景。 |
| 高精度识别 | 总体准确率达 93%以上。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [车辆物流识别](https://common-buy.aliyun.com/?commodityCode=ocr_logistics_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=logistics&subtype=driving_license#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [车牌识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_logistics_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_logistics_dp_cn_20211103160032_0692%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCarNumber?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 请保证整张车牌内容及其边缘包含在图像内。 <br>- 本能力会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |
| 相关能力 | - [云市场车牌识别。](https://market.aliyun.com/products/57124001/cmapi020094.html?spm=5176.730005.result.17.517535242WwEyb&innerSource=search_%E8%BD%A6%E7%89%8C%E8%AF%86%E5%88%AB#sku=yuncode1409400000) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCarNumber)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeCarNumber)

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
| ocr:RecognizeCarNumber |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/tfs/TB1Wo7eXAvoK1RjSZFDXXXY3pXa-2512-3509.jpg |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 请求唯一 ID |
| Data | string | 返回数据 | "{"data":{"secondary\_cls":{"type\_str":"小型汽车","prob":0.955191},"data":{"车牌":"黑AF6655"},"score":1.050000,"info":\[{"value":"黑AF6655","key":"车牌","key\_prob":0.999260,"value\_prob":0.999260,"key\_loc":"","value\_loc":"469,450,1220,419,1227,588,476,620"}\]},"height":1200,"orgHeight":1200,"orgWidth":1600,"prism\_keyValueInfo":\[{"key":"车牌","keyProb":99,"value":"黑AF6655","valuePos":\[{"x":469,"y":450},{"x":1220,"y":419},{"x":1227,"y":588},{"x":476,"y":620}\],"valueProb":99}\],"structure\_list":\[{"$ref":"$.data"}\],"width":1600}" |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| structure\_list | list | 车牌信息（如果图中有多张车牌，此字段包含所有的车牌信息。数组中每条车牌数据的字段和 **data** 一致）。 |
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
| secondary\_cls | string | 车牌类型信息。 |
| data | object | 车牌信息。 |
| info | list | 结构化坐标信息。（和 **prism\_keyValueInfo** 字段包含信息一致）。 |

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

#### 结构化坐标信息（info 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| key | string | 识别出的字段名称。 |
| key\_prob | float | 字段名称置信度。 |
| value | string | 识别出的字段名称对应的值。 |
| value\_prob | float | 字段名称对应值的置信度。 |
| value\_pos | list | 车牌在原图中的四个点坐标（左上角横坐标、左上角纵坐标、右上角横坐标、右上角纵坐标、右下角横坐标、右下角纵坐标、左下角横坐标、左下角纵坐标）。 |

## 示例

正常返回示例

`JSON`格式

```swift
{
  "RequestId": "请求唯一 ID",
  "Data": "\"{\"data\":{\"secondary_cls\":{\"type_str\":\"小型汽车\",\"prob\":0.955191},\"data\":{\"车牌\":\"黑AF6655\"},\"score\":1.050000,\"info\":[{\"value\":\"黑AF6655\",\"key\":\"车牌\",\"key_prob\":0.999260,\"value_prob\":0.999260,\"key_loc\":\"\",\"value_loc\":\"469,450,1220,419,1227,588,476,620\"}]},\"height\":1200,\"orgHeight\":1200,\"orgWidth\":1600,\"prism_keyValueInfo\":[{\"key\":\"车牌\",\"keyProb\":99,\"value\":\"黑AF6655\",\"valuePos\":[{\"x\":469,\"y\":450},{\"x\":1220,\"y\":419},{\"x\":1227,\"y\":588},{\"x\":476,\"y\":620}],\"valueProb\":99}],\"structure_list\":[{\"$ref\":\"$.data\"}],\"width\":1600}\"",
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
| 2022-11-25 | API 内部配置变更，不影响调用 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeCarNumber?updateTime=2022-11-25#workbench-doc-change-demo) |
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeCarNumber?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[车辆物流识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-vehicle-logistics-identification/)RecognizeCarNumber - 车牌识别

# RecognizeCarNumber - 车牌识别

更新时间：2025-12-08 21:11:21

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeWaybill - 电子面单识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizewaybill)[下一篇：RecognizeCarVinCode - 车辆vin码识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizecarvincode)

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