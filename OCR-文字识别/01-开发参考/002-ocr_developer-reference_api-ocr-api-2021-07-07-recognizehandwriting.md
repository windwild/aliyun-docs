支持中文手写体、英文手写体、数字手写体等各种复杂场景的手写文字识别。

## 接口说明

#### 本接口适用场景

- 阿里云通用手写体识别，是阿里云官方自研 OCR 文字识别产品，适用于获取手写体书面形式的文字场景，适用于各类手写笔记、板书等。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/tfs/TB1xvaLcggP7K4jSZFqXXamhVXa-1600-920.jpg)

#### 本接口核心能力

| 分类 | 概述 |
| --- | --- |

| 分类 | 概述 |
| --- | --- |
| 多文字形式 | 支持中文手写体、英文手写体、数字手写体。 |
| 图像增强 | 默认支持图像增强，包括图像自动旋转、畸变自动矫正、模糊图片自动增强等能力。 |
| 多类型覆盖 | 支持模糊、光照不均、透视畸变、任意背景等低质量图像识别。 |
| 高精度识别 | 总体识别准确率可达 98%。 |

#### 如何使用本接口

| 步骤 | 概述 |
| --- | --- |

| 步骤 | 概述 |
| --- | --- |
| 1 | 开通 [通用文字识别](https://common-buy.aliyun.com/?commodityCode=ocr_general_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=universal&subtype=shouxie#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [通用手写体识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_general_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_general_dp_cn_20211103172431_0249%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeHandwriting?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。<br>- 图片尺寸过小，会影响识别精度。图片内单字大小在 10-50px 内时，识别效果较好。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 接口响应速度和图片中的文字数量有关，如果图片中文字数量越多，接口响应可能越慢。<br>- 接口会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |
| 相关能力 | - [云市场手写体识别。](https://market.aliyun.com/apimarket/detail/cmapi00040832) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeHandwriting)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeHandwriting)

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
| ocr:RecognizeHandwriting |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241223/brwyrd/%E9%80%9A%E7%94%A8%E6%89%8B%E5%86%99%E4%BD%93%E8%AF%86%E5%88%AB.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |
| OutputCharInfo | boolean | 否 | - 是否输出单字识别结果，默认不需要。<br>- true：需要；false：不需要。 | false |
| NeedRotate | boolean | 否 | - 是否需要自动旋转功能，默认不需要。<br>- true：需要；false：不需要。 | false |
| OutputTable | boolean | 否 | - 是否输出表格识别结果，包含单元格信息，默认不需要。<br>- true：需要；false：不需要。 | false |
| NeedSortPage | boolean | 否 | - 是否按顺序输出文字块，默认为 false。<br>- false 表示从左往右，从上到下的顺序；true 表示从上到下，从左往右的顺序。 | false |
| Paragraph | boolean | 否 | - 是否需要分段功能，默认不需要。<br>- true：需要；false：不需要。 | false |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"content":"炼句 提问方式 1.请赏析诗歌某一联(句) 2.赏析某一联(句)的妙处 3.请赏析诗歌某、角度抒胸意、借景抒情、托物","height":1277,"orgHeight":1277,"orgWidth":1080,"prism\_version":"1.0.9","prism\_wnum":26,"prism\_wordsInfo":\[{"angle":-87,"direction":0,"height":83,"pos":\[{"x":177,"y":56},{"x":260,"y":60},{"x":259,"y":88},{"x":176,"y":84}\],"prob":96,"width":28,"word":"炼句","x":203,"y":30}\],"width":1080} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| angle | int | 图片的角度（当 NeedRotate=true 时，返回此字段）。0 表示正向，90 表示图片朝右，180 朝下，270 朝左。 |
| content | string | 识别出图片的文字块汇总。 |
| prism\_wordsInfo | list | 文字块信息。 |
| prism\_paragraphsInfo | list | 段落信息（当 Paragraph=true 时，返回此字段）。 |
| prism\_tablesInfo | list | 表格信息（当 OutputTable=true 时，返回此字段）。 |
| prism\_wnum | int | 识别的文字块的数量，prism\_wordsInfo 数组的大小。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 文字块信息（prism\_wordsInfo 字段。）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| angle | int | 文字块的角度。 |
| height | int | 文字块的高度（需考虑文字块的角度） |
| width | int | 文字块的宽度（需考虑文字块的角度） |
| pos | list | 文字块的外矩形四个点的坐标按顺时针排列（左上、右上、右下、左下）。当 NeedRotate=true 时，如果最外层的 angle 不为 0，需要按照 angle 矫正图片后，坐标才准确。 |
| word | string | 文字块的文字内容。 |
| tableId | int | 表格的 id（当 OutputTable=true 时，返回此字段）。 |
| tableCellId | int | 表格中单元格的 id（当 OutputTable=true 时，返回此字段）。 |
| charInfo | list | 单字信息。 |

#### 单字信息（charInfo 字段。当 OutputCharInfo=true 时，返回此字段。）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| word | string | 单字文字。 |
| prob | int | 置信度。 |
| x | int | 单字左上角横坐标。 |
| y | int | 单字左上角纵坐标。 |
| w | int | 单字宽度。 |
| h | int | 单字高度。 |

#### 表格信息（prism\_tablesInfo 字段。当 OutputTable=true 时，返回此字段。）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| tableId | int | 表格 id，和 prism\_wordsInfo 信息中的 tableId 对应。 |
| xCellSize | int | 表格中横坐标单元格的数量。 |
| yCellSize | int | 表格中纵坐标单元格的数量。 |
| cellInfos | list | 单元格信息。 |

#### 单元格信息（cellInfos 字段。）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| tableCellId | int | 表格中单元格 id，和 prism\_wordsInfo 信息中的 tableCellId 对应。 |
| word | string | 单元格中的文字。 |
| xsc | int | xStartCell 缩写，表示横轴方向该单元格起始在第几个单元格，第一个单元格值为 0。 |
| xec | int | xEndCell 缩写，表示横轴方向该单元格结束在第几个单元格，第一个单元格值为 0，如果 xsc 和 xec 都为 0 说明该文字在横轴方向占据了一个单元格并且在第一个单元格内。 |
| ysc | int | yStartCell 缩写，表示纵轴方向该单元格起始在第几个单元格，第一个单元格值为 0。 |
| yec | int | yEndCell 缩写，表示纵轴方向该单元格结束在第几个单元格，第一个单元格值为 0。 |
| pos | list | 单元格位置，按照单元格四个角的坐标顺时针排列，分别为左上 XY 坐标、右上 XY 坐标、右下 XY 坐标、左下 XY 坐标。 |

#### 段落信息（prism\_paragraphsInfo 字段。当 Paragraph=true 时，返回此字段。）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| paragraphId | int | 段落 id，和 prism\_wordsInfo 信息中的 paragraphId 对应。 |
| word | string | 段落文字。 |

## 示例

正常返回示例

`JSON`格式

```css
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "content": "炼句 提问方式 1.请赏析诗歌某一联(句) 2.赏析某一联(句)的妙处 3.请赏析诗歌某、角度抒胸意、借景抒情、托物",
    "height": 1277,
    "orgHeight": 1277,
    "orgWidth": 1080,
    "prism_version": "1.0.9",
    "prism_wnum": 26,
    "prism_wordsInfo": [\
      {\
        "angle": -87,\
        "direction": 0,\
        "height": 83,\
        "pos": [\
          {\
            "x": 177,\
            "y": 56\
          },\
          {\
            "x": 260,\
            "y": 60\
          },\
          {\
            "x": 259,\
            "y": 88\
          },\
          {\
            "x": 176,\
            "y": 84\
          }\
        ],\
        "prob": 96,\
        "width": 28,\
        "word": "炼句",\
        "x": 203,\
        "y": 30\
      }\
    ],
    "width": 1080
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
| 2024-01-23 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeHandwriting?updateTime=2024-01-23#workbench-doc-change-demo) |
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeHandwriting?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[通用文字识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-general-character-recognition/)RecognizeHandwriting - 通用手写体识别

# RecognizeHandwriting - 通用手写体识别

更新时间：2025-12-08 21:05:39

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeAdvanced - 全文识别高精版](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeadvanced)[下一篇：RecognizeBasic - 电商图片文字识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizebasic)

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