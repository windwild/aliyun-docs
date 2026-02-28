针对图片文档场景下俄文印刷体高效检测和识别，支持旋转、表格、文字坐标等多项基础功能。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeRussian)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeRussian)

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
| ocr:RecognizeRussian |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | 图片链接（长度不超 2048 字节，不支持 base64） | https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241223/jqizki/%E4%BF%84%E8%AF%AD%E8%AF%86%E5%88%AB.png |
| body | byte | 否 | 图片二进制文件，最大 10MB，与 URL 二选一。 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |
| OutputCharInfo | boolean | 否 | 是否输出单字识别结果 | false |
| NeedRotate | boolean | 否 | 是否需要自动旋转功能（结构化检测、混贴场景、教育相关场景会自动做旋转，无需设置），返回角度信息 | false |
| OutputTable | boolean | 否 | 是否输出表格识别结果，包含单元格信息 | false |

### 支持的图片格式

- PNG、JPG、JPEG、BMP、GIF、TIFF、WebP

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"content":"Тэбако (коробочка для косметики) с рисунком в виде колес повозки","height":199,"orgHeight":199,"orgWidth":766,"prism\_version":"1.0.9","prism\_wnum":6,"prism\_wordsInfo":\[{"angle":-89,"direction":0,"height":722,"pos":\[{"x":6,"y":23},{"x":728,"y":26},{"x":727,"y":43},{"x":5,"y":41}\],"prob":99,"width":17,"word":"Тэбако (коробочка для косметики) с рисунком в виде колес повозки， покрытая","x":358,"y":-327}\],"width":766} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

返回数据说明

```jboss-cli
angle                  图片的角度，0 表示正向，90 表示图片朝右，180 朝下，270 朝左</br>
content              识别出图片的文字块汇总</br>
height                算法矫正图片后的高度</br>
width                 算法矫正图片后的宽度</br>
orgHeight          原图的高度</br>
orgWidth           原图的宽度</br>
prism_wnum      识别的文字块的数量，prism_wordsInfo 数组的大小</br>
-------------------------prism-wordsInfo 文字块数组内的字段说明-------------------------</br>
angle                 文字块的角度，这个角度只影响 width 和 height，当角度为-90、90、-270、270，width 和 height 的值需要自行互换</br>
height                文字块的高度</br>
width                 文字块的宽度</br>
pos                    文字块的外矩形四个点的坐标按顺时针排列，左上、右上、右下、左下，当 NeedRotate 为 true 时，如果最外层的 angle 不为 0，需要按照 angle 矫正图片后，坐标才准确</br>
word                  文字块的文字</br>
tableId               当 OutputTable 为 true 并且该文字块在表格内则存在该字段，tableId 表示表格的 id</br>
tableCellId         当 OutputTable 为 true 并且该文字块在表格内则存在该字段，表示表格中单元格的 id</br>
----------------------------------------charInfo 单字信息-----------------------------------------</br>
word                  单字文字</br>
x                        单字左上角横坐标</br>
y                        单字左上角纵坐标</br>
w                       单字宽度
<span>h                       单字高度</span></br>
--------------------------------------------------------------------------------------------------------</br>
--------------------------------------------------------------------------------------------------------</br>
---------------------------prism-tablesInfo 表格数组内的字段说明--------------------------</br>
tableId               表格 id，和 prism_wordsInfo 信息中的 tableId 对应</br>
xCellSize            表格中横坐标单元格的数量</br>
yCellSize            表格中纵坐标单元格的数量</br>
------------cellInfos 单元格信息，包含单元格在整个表格中的空间拓扑关系---------</br>
tableCellId         表格中单元格 id，和 prism_wordsInfo 信息中的 tableCellId 对应</br>
word                 单元格中的文字</br>
xsc                    xStartCell 缩写，表示横轴方向该单元格起始在第几个单元格，第一个单元格值为 0</br>
xec                    xEndCell 缩写，表示横轴方向该单元格结束在第几个单元格，第一个单元格值为 0，如果 xsc 和 xec 都为 0 说明该文字在横轴方向占据了一个单元格并且在第一个单元格内</br>
ysc                    yStartCell 缩写，表示纵轴方向该单元格起始在第几个单元格，第一个单元格值为 0</br>
yec                    yEndCell 缩写，表示纵轴方向该单元格结束在第几个单元格，第一个单元格值为 0</br>
pos                   单元格位置，按照单元格四个角的坐标顺时针排列，分别为左上 XY 坐标、右上 XY 坐标、右下 XY 坐标、左下 XY 坐标</br>
--------------------------------------------------------------------------------------------------------</br>
--------------------------------------------------------------------------------------------------------</br>
```

## 示例

正常返回示例

`JSON`格式

```css
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "content": "Тэбако (коробочка для косметики) с рисунком в виде колес повозки",
    "height": 199,
    "orgHeight": 199,
    "orgWidth": 766,
    "prism_version": "1.0.9",
    "prism_wnum": 6,
    "prism_wordsInfo": [\
      {\
        "angle": -89,\
        "direction": 0,\
        "height": 722,\
        "pos": [\
          {\
            "x": 6,\
            "y": 23\
          },\
          {\
            "x": 728,\
            "y": 26\
          },\
          {\
            "x": 727,\
            "y": 43\
          },\
          {\
            "x": 5,\
            "y": 41\
          }\
        ],\
        "prob": 99,\
        "width": 17,\
        "word": "Тэбако (коробочка для косметики) с рисунком в виде колес повозки， покрытая",\
        "x": 358,\
        "y": -327\
      }\
    ],
    "width": 766
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
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeRussian?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[小语种文字识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-small-language-character-recognition/)RecognizeRussian - 俄语识别

# RecognizeRussian - 俄语识别

更新时间：2025-12-08 21:13:16

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeLatin - 拉丁语识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizelatin)[下一篇：RecognizeCovidTestReport - 核酸检测报告识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizecovidtestreport)

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