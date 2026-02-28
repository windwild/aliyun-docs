模板服务预测目前包括两种类型：自定义KV模板和自定义表格模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://next.api.alibabacloud.com/api/documentAutoml/2022-12-29/PredictTemplateModel)

[调试](https://next.api.alibabacloud.com/api/documentAutoml/2022-12-29/PredictTemplateModel)

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
| TaskId | long | 是 | 任务ID | 1 |
| Content | string | 否 | 图片访问URL地址 | https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/demo/demo.png |
| BinaryToText | boolean | 否 | content字段是图片URL时：false<br>body为base64的内容时：true | false：表示content传入的是url<br>true：表示body是直接传入图片进行base64的内容 |
| Body | string | 否 | 图片base64编码内容 | data:image/png;base64,xxxxx |

content字段和body字段传参二选一，图片URL则content为图片访问地址。内容为base64编码则传参body，且BinaryToText传true

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | Id of the request | F25FBAB4-665A-5D85-8AEF-39AE29F7D588 |
| Data | object | 返回数据 |  |
| Message | string | 返回消息 | successful |
| Code | string | 状态码。说明 200表示成功。 | 200 |

```haskell
模板服务预测接口，返回Data字段解释说明：
score         预测服务置信度 0-1
data.         算法返回的预测结果，数组格式
prob          算法结果置信度 0-1
fieldName     抽取key
fieldWord     抽取value
location      抽取结果坐标位置  { "x": 119,"y": 48  }表示页面坐标点
wordInfo      抽取内容详细信息，包括了每个字符的位置信息
specificType  算法类型（infoCustomeKvTemp:自定义KV 模板，infoCustomeTableTemp:自定义表格模板，ocr_infoExtractBill:信息抽取OCR识别，infoExtractBill:单据票证抽取，infoExtractDoc:长文档信息抽取 ）
classType     模型预测服务、模板预测服务
predictFile   预测文件地址（失效时间60分钟）
```

## 示例

正常返回示例

`JSON`格式

```json
{
  "RequestId": "F25FBAB4-665A-5D85-8AEF-39AE29F7D588",
  "Data": {
    "test": "test",
    "test2": 1
  },
  "Message": "successful",
  "Code": "200"
}
```

## 错误码

| HTTP status code | 错误码 | 错误信息 |
| --- | --- | --- |

| HTTP status code | 错误码 | 错误信息 |
| --- | --- | --- |
| 200 | 21002 | 模板预测超时 |
| 200 | 21003 | 模板预测失败 |
| 200 | 21004 | 模板提交失败 |
| 200 | 10001 | 参数出错 |
| 200 | 10005 | 服务不存在 |
| 200 | 21018 | 未找到模板信息 |
| 200 | 16001 | 未找到可预测的模型 |
| 200 | 16004 | 指定的模型不存在 |
| 200 | 23002 | 获取资源HTTP异常 |
| 200 | 22002 | ocr服务异常 |
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
| 2023-03-23 | OpenAPI 错误码发生变更，OpenAPI 返回结构发生变更 |  |
| | 变更项 | 变更内容 |
| --- | --- |
| 错误码 | OpenAPI 错误码发生变更 |
|  | 删除错误码：200 |
| 出参 | OpenAPI 返回结构发生变更 | |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) PredictTemplateModel - 模板服务预测API

# PredictTemplateModel - 模板服务预测API

更新时间：2023-04-10 21:55:12

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