适用于非结构化文字识别，支持返回文字内容和位置坐标信息。

## 接口说明

#### 本接口适用场景

- 阿里云通用文字识别，是阿里云官方自研 OCR 文字识别产品，适用于各类常见文档图片或文档扫描件中的文字信息按照文档原有的格式智能识别文字并结构化输出识别结果。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i3/O1CN01g9tMm71eQDRRu7U3C_!!6000000003865-2-tps-899-243.png)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 全字段识别 | 结构化识别图片上所包含的全字段，并返回 JSON。 |
| 图像增强 | 默认支持图像增强，包括图像畸变自动矫正、模糊图片自动增强等能力。 |
| 高精度高性能 | 超高精度及性能；识别准确率位于行业前列，识别速度显著高于国内其他 OCR 云服务。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [通用文字识别](https://common-buy.aliyun.com/?commodityCode=ocr_general_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=universal&subtype=general_text#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [通用文字识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_general_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_general_dp_cn_20211103172431_0908%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeGeneral?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 接口响应速度和图片中的文字数量有关，如果图片中文字数量越多，接口响应可能越慢。<br>- 接口会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeGeneral)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeGeneral)

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
| ocr:RecognizeGeneral |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250102/oqzwva/%E9%80%9A%E7%94%A8%E6%96%87%E5%AD%97%E8%AF%86%E5%88%AB.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | 本示例将会返回图片上的文字信息以及对应点位：<br>{"content":"iPhone 12 升维大提速。 RMB 229/月或RMB 5499起, 还可折抵换购1。 进一步了解 > 你可以立即在线购买并享受免费送货服务,也可以预约到附近的 Apple Store零售店购买+。 如果你已加入iPhone年年焕新计划, 请先查询你的升级换购资格, 然后预约前往Apple Store零售店换购新款iPhone。 查询升级换购资格> in ","height":655,"orgHeight":655,"orgWidth":805,"prism\_version":"1.0.9","prism\_wnum":11,"prism\_wordsInfo":\[{"angle":-88,"direction":0,"height":111,"pos":\[{"x":351,"y":45},{"x":461,"y":46},{"x":461,"y":67},{"x":351,"y":66}\],"prob":99,"width":20,"word":"iPhone 12","x":396,"y":0}\],"width":805} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| content | string | 识别出图片的文字块汇总。 |
| prism\_wordsInfo | list | 文字块信息。 |
| prism\_wnum | int | 识别的文字块的数量，prism\_wordsInfo 数组的大小。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 文字块信息（prism\_wordsInfo 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| angle | int | 文字块的角度。 |
| height | int | 文字块的高度（需考虑文字块的角度） |
| width | int | 文字块的宽度（需考虑文字块的角度） |
| pos | list | 文字块的外矩形四个点的坐标按顺时针排列（左上、右上、右下、左下）。 |
| word | string | 文字块的文字内容。 |

## 示例

正常返回示例

`JSON`格式

```
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": "本示例将会返回图片上的文字信息以及对应点位：\n{\"content\":\"iPhone 12 升维大提速。 RMB 229/月或RMB 5499起, 还可折抵换购1。 进一步了解 > 你可以立即在线购买并享受免费送货服务,也可以预约到附近的 Apple Store零售店购买+。 如果你已加入iPhone年年焕新计划, 请先查询你的升级换购资格, 然后预约前往Apple Store零售店换购新款iPhone。 查询升级换购资格> in \",\"height\":655,\"orgHeight\":655,\"orgWidth\":805,\"prism_version\":\"1.0.9\",\"prism_wnum\":11,\"prism_wordsInfo\":[{\"angle\":-88,\"direction\":0,\"height\":111,\"pos\":[{\"x\":351,\"y\":45},{\"x\":461,\"y\":46},{\"x\":461,\"y\":67},{\"x\":351,\"y\":66}],\"prob\":99,\"width\":20,\"word\":\"iPhone 12\",\"x\":396,\"y\":0}],\"width\":805}",
  "Code": "noPermission",
  "Message": "You are not authorized to perform this operation."
}
```

## 错误码

访问[错误中心](https://api.aliyun.com/document/ocr-api/2021-07-07/errorCode)查看更多错误码。

## 变更历史

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeGeneral?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/) [开发参考](https://help.aliyun.com/zh/ocr/developer-reference/) [API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/) [API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/) [通用文字识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-general-character-recognition/) RecognizeGeneral - 通用文字识别

# RecognizeGeneral - 通用文字识别

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeBasic - 电商图片文字识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizebasic)[下一篇：RecognizeTableOcr - 表格识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizetableocr)

该文章对您有帮助吗？

反馈