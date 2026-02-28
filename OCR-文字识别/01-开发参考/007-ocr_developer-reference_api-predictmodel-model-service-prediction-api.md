模型预测分为三种类型：长文档信息抽取、单票据信息抽取、表格信息抽取。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://next.api.alibabacloud.com/api/documentAutoml/2022-12-29/PredictModel)

[调试](https://next.api.alibabacloud.com/api/documentAutoml/2022-12-29/PredictModel)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 授权信息

当前API暂无授权信息透出。

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Content | string | 否 | 图片访问URL地址 | https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/demo/extractBill.png |
| ModelVersion | string | 否 | 模型对应的版本号，如果不传入版本号表示默认用模型最新生效的版本。 | 1 |
| ModelId | long | 是 | 模型ID。模型列表页模型ID | 123 |
| BinaryToText | boolean | 否 | content字段是图片URL时：false<br>body为base64的内容时：true | false：表示content传入的是url<br>true：表示body是直接传入图片进行base64的内容 |
| Body | string | 否 | 图片base64编码内容 | data:image/png;base64,xxxxx |

BinaryToText为非必填项

content字段和body字段传参二选一，图片URL则content为图片访问地址。内容为base64编码则传参body，且BinaryToText传true

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | Id of the request | 3EAC98E6-8DD6-511F-8764-DEE8B6EB6BB4 |
| Code | integer | 请求结果状态，200为成功 | 200 |
| Message | string | 错误信息。 | success |
| Data | object | 接口返回信息 |  |

长文档信息抽取模型data返回字段解释说明：

```json
originalFileUrl     原始文件url
predictFile         解析后用于预测的图片url集合
data                具体预测结果
angle               图片的角度，当NeedRotate为true时才会返回，0表示正向，90表示图片朝右，180朝下，270朝左
content             识别出图片的文字块汇总
height              算法矫正图片后的高度
width               算法矫正图片后的宽度
orgHeight           原图的高度
orgWidth            原图的宽度
prism_wnum          识别的文字块的数量，prism_wordsInfo数组的大小
```

prism-wordsInfo文字块数组内的字段说明

```json
angle                文字块的角度，这个角度只影响width和height，当角度为-90、90、-270、270，width和height的值需要自行互换
height               文字块的高度
width                文字块的宽度
pos                  文字块的外矩形四个点的坐标按顺时针排列，左上、右上、右下、左下，当NeedRotate为true时，如果最外层的angle不为0，需要按照angle矫正图片后，坐标才准确
word                 文字块的文字
tableId              当OutputTable为true并且该文字块在表格内则存在该字段，tableId表示表格的id
tableCellId          当OutputTable为true并且该文字块在表格内则存在该字段，表示表格中单元格的id
```

charInfo单字信息

```json
word                  单字文字
x                     单字左上角横坐标
y                     单字左上角纵坐标
w                     单字宽度
h                     单字高度
```

prism-tablesInfo表格数组内的字段说明

```json
tableId            表格id，和prism_wordsInfo信息中的tableId对应
xCellSize          表格中横坐标单元格的数量
yCellSize          表格中纵坐标单元格的数量
```

cellInfos单元格信息，包含单元格在整个表格中的空间拓扑关系

```json
tableCellId        表格中单元格id，和prism_wordsInfo信息中的tableCellId对应
word               单元格中的文字
xsc                xStartCell缩写，表示横轴方向该单元格起始在第几个单元格，第一个单元格值为0
xec                xEndCell缩写，表示横轴方向该单元格结束在第几个单元格，第一个单元格值为0，如果xsc和xec都为0说明该文字在横轴方向占据了一个单元格并且在第一个单元格内
ysc                yStartCell缩写，表示纵轴方向该单元格起始在第几个单元格，第一个单元格值为0
yec                yEndCell缩写，表示纵轴方向该单元格结束在第几个单元格，第一个单元格值为0
pos                单元格位置，按照单元格四个角的坐标顺时针排列，分别为左上XY坐标、右上XY坐标、右下XY坐标、左下XY坐标
```

## 示例

正常返回示例

`JSON`格式

```json
{
  "RequestId": "3EAC98E6-8DD6-511F-8764-DEE8B6EB6BB4",
  "Code": 200,
  "Message": "success",
  "Data": {
    "test": "test",
    "test2": 1
  }
}
```

## 错误码

| HTTP status code | 错误码 | 错误信息 |
| --- | --- | --- |

| HTTP status code | 错误码 | 错误信息 |
| --- | --- | --- |
| 200 | 21002 | 模板预测超时 |
| 200 | 21003 | 模板预测失败 |
| 200 | 10001 | 参数出错 |
| 200 | 10005 | 服务不存在 |
| 200 | 16001 | 未找到可预测的模型 |
| 200 | 13018 | 未找到模型信息 |
| 200 | 16004 | 指定的模型不存在 |
| 200 | 23002 | 获取资源HTTP异常 |
| 200 | 11002 | 账号没有开通服务 |
| 200 | 19999 | 未知异常 |

访问[错误中心](https://next.api.alibabacloud.com/document/documentAutoml/2022-12-29/errorCode)查看更多错误码。

## 变更历史

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |
| 2023-04-10 | OpenAPI 错误码发生变更，OpenAPI 入参发生变更 |  |
| | 变更项 | 变更内容 |
| --- | --- |
| 错误码 | OpenAPI 错误码发生变更 |
|  | 删除错误码：200 |
| 入参 | OpenAPI 入参发生变更 |
|  | 新增入参：Body |
|  | 删除入参：body | |
| 2023-03-31 | OpenAPI 错误码发生变更，OpenAPI 入参发生变更 |  |
| | 变更项 | 变更内容 |
| --- | --- |
| 错误码 | OpenAPI 错误码发生变更 |
|  | 删除错误码：200 |
| 入参 | OpenAPI 入参发生变更 |
|  | 新增入参：body | |
| 2023-03-21 | OpenAPI 错误码发生变更，OpenAPI 返回结构发生变更 |  |
| | 变更项 | 变更内容 |
| --- | --- |
| 错误码 | OpenAPI 错误码发生变更 |
|  | 删除错误码：200 |
| 出参 | OpenAPI 返回结构发生变更 | |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) PredictModel - 模型服务预测API

# PredictModel - 模型服务预测API

更新时间：2023-04-10 21:57:58

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：产品简介](https://help.aliyun.com/zh/ocr/product-overview/product-introduction/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

授权信息

请求参数

返回参数

示例

错误码

变更历史