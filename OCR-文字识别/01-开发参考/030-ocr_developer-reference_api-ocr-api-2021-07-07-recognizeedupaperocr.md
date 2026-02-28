支持K12全学科扫描场景的整页内容文字识别。接口支持印刷体文本及公式的OCR识别和坐标返回，此外，接口还可对题目中的配图位置进行检测并返回坐标位置。

## 接口说明

#### 本接口适用场景

- 阿里云整页试卷识别，是阿里云官方自研 OCR 文字识别产品，适用于对练习册、教辅、教材等内容进行整页识别与题目检索场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i4/O1CN016bI8WV1TWfQ4ocurU_!!6000000002390-2-tps-739-450.png)

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
| 1 | 开通 [教育场景识别](https://common-buy.aliyun.com/?commodityCode=ocr_education_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=edu&subtype=paper_ocr#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [教育场景识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_education_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_education_dp_cn_20211103164555_0789%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeEduPaperOcr?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 接口响应速度和图片中的文字数量有关，如果图片中文字数量越多，接口响应可能越慢。<br>- 接口会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeEduPaperOcr)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeEduPaperOcr)

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
| ocr:RecognizeEduPaperOcr |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241223/alfbwq/%E6%95%B4%E9%A1%B5%E8%AF%95%E5%8D%B7%E8%AF%86%E5%88%AB.png |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |
| ImageType | string | 是 | - 图片类型。<br>- scan：扫描图， photo：实拍图。 | scan：扫描图， photo：实拍图 |
| Subject | string | 否 | - 年级学科。<br>- default:默认, Math:数学, PrimarySchool\_Math:小学数学, JHighSchool\_Math: 初中数学, Chinese:语文, PrimarySchool\_Chinese:小学语文, JHighSchool\_Chinese:初中语文, English:英语, PrimarySchool\_English:小学英语, JHighSchool\_English:初中英语, Physics:物理, JHighSchool\_Physics:初中物理, Chemistry: 化学, JHighSchool\_Chemistry:初中化学, Biology:生物, JHighSchool\_Biology:初中生物, History:历史, JHighSchool\_History:初中历史, Geography:地理, JHighSchool\_Geography:初中地理, Politics:政治, JHighSchool\_Politics:初中政治。 | default:默认, Math:数学, PrimarySchool\_Math:小学数学, JHighSchool\_Math: 初中数学, Chinese:语文, PrimarySchool\_Chinese:小学语文, JHighSchool\_Chinese:初中语文, English:英语, PrimarySchool\_English:小学英语, JHighSchool\_English:初中英语, Physics:物理, JHighSchool\_Physics:初中物理, Chemistry: 化学, JHighSchool\_Chemistry:初中化学, Biology:生物, JHighSchool\_Biology:初中生物, History:历史, JHighSchool\_History:初中历史, Geography:地理, JHighSchool\_Geography:初中地理, Politics:政治, JHighSchool\_Politics:初中政治 |
| OutputOricoord | boolean | 否 | - 是否输出原图坐标信息（如果图片被做过旋转，图片校正等处理），默认不需要。<br>- true：需要；false：不需要。 | false |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"content":"√技能提升练 √拓展创新练 12.对于同一平面内的三条直线,给出下列5个论断: 15.「2018春·如皋期末\]在一个","figure":\[{"type":"subject\_pattern","x":1605,"y":3087,"w":645,"h":804,"box":{"x":0,"y":0,"w":0,"h":0,"angle":0},"points":\[{"x":1605,"y":3087},{"x":2250,"y":3087},{"x":2250,"y":3891},{"x":1605,"y":3891}\]}\],"height":7000,"orgHeight":7000,"orgWidth":4716,"prism\_version":"1.0.9","prism\_wnum":64,"prism\_wordsInfo":\[{"angle":0,"direction":0,"height":85,"pos":\[{"x":207,"y":508},{"x":826,"y":506},{"x":826,"y":592},{"x":208,"y":594}\],"prob":96,"recClassify":0,"width":618,"word":"√技能提升练","x":207,"y":506}\],"width":4716} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| angle | int | 图片的角度。0 表示正向，90 表示图片朝右，180 朝下，270 朝左。 |
| content | string | 识别出图片的文字块汇总，可能包含 latex 公式，需要自行解析还原。 |
| figure | list | 图片中的图案信息。当 ImageType=scan 才返回该字段。 |
| prism\_wordsInfo | list | 文字块信息。 |
| prism\_wnum | int | 识别的文字块的数量，prism\_wordsInfo 数组的大小。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |

#### 文字块信息（prism\_wordsInfo 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| angle | int | 文字块的角度。 |
| height | int | 文字块的高度（需考虑文字块的角度） |
| width | int | 文字块的宽度（需考虑文字块的角度） |
| pos | list | 文字块的外矩形四个点的坐标按顺时针排列（左上、右上、右下、左下）。当 NeedRotate=true 时，如果最外层的 angle 不为 0，需要按照 angle 矫正图片后，坐标才准确。 |
| word | string | 文字块的文字内容。 |
| charInfo | list | 单字信息。 |

#### 单字信息（charInfo 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| word | string | 单字文字。 |
| prob | int | 置信度。 |
| recClassify | int | 文字属性分类。（0：中文印刷，1：拉丁语种，2：手写体，3：韩语，4：泰文，5：公式） |
| x | int | 单字左上角横坐标。 |
| y | int | 单字左上角纵坐标。 |
| w | int | 单字宽度。 |
| h | int | 单字高度。 |

#### 图案位置信息（figure 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

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

```yaml
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "content": "√技能提升练 √拓展创新练 12.对于同一平面内的三条直线,给出下列5个论断: 15.「2018春·如皋期末]在一个",
    "figure": [\
      {\
        "type": "subject_pattern",\
        "x": 1605,\
        "y": 3087,\
        "w": 645,\
        "h": 804,\
        "box": {\
          "x": 0,\
          "y": 0,\
          "w": 0,\
          "h": 0,\
          "angle": 0\
        },\
        "points": [\
          {\
            "x": 1605,\
            "y": 3087\
          },\
          {\
            "x": 2250,\
            "y": 3087\
          },\
          {\
            "x": 2250,\
            "y": 3891\
          },\
          {\
            "x": 1605,\
            "y": 3891\
          }\
        ]\
      }\
    ],
    "height": 7000,
    "orgHeight": 7000,
    "orgWidth": 4716,
    "prism_version": "1.0.9",
    "prism_wnum": 64,
    "prism_wordsInfo": [\
      {\
        "angle": 0,\
        "direction": 0,\
        "height": 85,\
        "pos": [\
          {\
            "x": 207,\
            "y": 508\
          },\
          {\
            "x": 826,\
            "y": 506\
          },\
          {\
            "x": 826,\
            "y": 592\
          },\
          {\
            "x": 208,\
            "y": 594\
          }\
        ],\
        "prob": 96,\
        "recClassify": 0,\
        "width": 618,\
        "word": "√技能提升练",\
        "x": 207,\
        "y": 506\
      }\
    ],
    "width": 4716
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
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeEduPaperOcr?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[教育场景识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-education-scene-recognition/)RecognizeEduPaperOcr - 整页试卷识别

# RecognizeEduPaperOcr - 整页试卷识别

更新时间：2025-12-08 21:12:05

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

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