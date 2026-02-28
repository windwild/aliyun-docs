文档自学习分类器预测接口。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/documentAutoml/2022-12-29/PredictClassifierModel)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/documentAutoml/2022-12-29/PredictClassifierModel)

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
| documentautoml:PredictClassifierModel | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| ClassifierId | long | 否 | 分类器 ID | 1 |
| AutoPrediction | boolean | 否 | 是否开启自动预测，false：不开启， true：开启，默认开启 | true |
| Content | string | 否 | 图片或 pdf 文件可访问地址 | https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/demo/table.png |
| Body | string | 否 | 图片 base64 编码内容 | data:image/png;base64,xxxxx |
| BinaryToText | boolean | 否 | content 字段是图片 URL 时：false <br>body 为 base64 的内容时：true | false |

content 字段和 body 字段传参二选一，图片 URL 则 content 为图片访问地址。内容为 base64 编码则传参 body，且 BinaryToText 传 true。

pdf 限制 20Mb，10 页。
除了长文档类型的模型预测以外，其他预测服务只会取第一页进行预测。

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | Id of the request | 232B91A8-9938-5C10-B522-127D1E342A57 |
| Code | integer | 成功 | 200 |
| Data | object | 返回数据。 | {<br> "score": 1,<br> "classID": "269\_2b6819527769749d962bf51d034b1820",<br> "tables": \[<br> {<br> "columns": \[<br> {<br> "header\_value": "姓名",<br> "bodies": \[<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生1",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 99<br> },<br> {<br> "x": 187,<br> "y": 99<br> },<br> {<br> "x": 187,<br> "y": 123<br> },<br> {<br> "x": 76,<br> "y": 123<br> }<br> \],<br> "value": "学生1"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生2",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 123<br> },<br> {<br> "x": 187,<br> "y": 123<br> },<br> {<br> "x": 187,<br> "y": 146<br> },<br> {<br> "x": 76,<br> "y": 146<br> }<br> \],<br> "value": "学生2"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生3",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 146<br> },<br> {<br> "x": 187,<br> "y": 146<br> },<br> {<br> "x": 187,<br> "y": 169<br> },<br> {<br> "x": 76,<br> "y": 169<br> }<br> \],<br> "value": "学生3"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生4",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 169<br> },<br> {<br> "x": 187,<br> "y": 169<br> },<br> {<br> "x": 187,<br> "y": 191<br> },<br> {<br> "x": 76,<br> "y": 191<br> }<br> \],<br> "value": "学生4"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生5",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 191<br> },<br> {<br> "x": 187,<br> "y": 191<br> },<br> {<br> "x": 187,<br> "y": 215<br> },<br> {<br> "x": 76,<br> "y": 215<br> }<br> \],<br> "value": "学生5"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生6",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 215<br> },<br> {<br> "x": 187,<br> "y": 215<br> },<br> {<br> "x": 187,<br> "y": 238<br> },<br> {<br> "x": 76,<br> "y": 238<br> }<br> \],<br> "value": "学生6"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生7",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 238<br> },<br> {<br> "x": 187,<br> "y": 238<br> },<br> {<br> "x": 187,<br> "y": 261<br> },<br> {<br> "x": 76,<br> "y": 261<br> }<br> \],<br> "value": "学生7"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生8",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 261<br> },<br> {<br> "x": 187,<br> "y": 261<br> },<br> {<br> "x": 187,<br> "y": 283<br> },<br> {<br> "x": 76,<br> "y": 283<br> }<br> \],<br> "value": "学生8"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生9",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 283<br> },<br> {<br> "x": 187,<br> "y": 283<br> },<br> {<br> "x": 187,<br> "y": 307<br> },<br> {<br> "x": 76,<br> "y": 307<br> }<br> \],<br> "value": "学生9"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "学生10",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 307<br> },<br> {<br> "x": 187,<br> "y": 307<br> },<br> {<br> "x": 187,<br> "y": 330<br> },<br> {<br> "x": 76,<br> "y": 330<br> }<br> \],<br> "value": "学生10"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 330<br> },<br> {<br> "x": 187,<br> "y": 330<br> },<br> {<br> "x": 187,<br> "y": 352<br> },<br> {<br> "x": 76,<br> "y": 352<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 352<br> },<br> {<br> "x": 187,<br> "y": 352<br> },<br> {<br> "x": 187,<br> "y": 375<br> },<br> {<br> "x": 76,<br> "y": 375<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 375<br> },<br> {<br> "x": 187,<br> "y": 375<br> },<br> {<br> "x": 187,<br> "y": 399<br> },<br> {<br> "x": 76,<br> "y": 399<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 399<br> },<br> {<br> "x": 187,<br> "y": 399<br> },<br> {<br> "x": 187,<br> "y": 422<br> },<br> {<br> "x": 76,<br> "y": 422<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 422<br> },<br> {<br> "x": 187,<br> "y": 422<br> },<br> {<br> "x": 187,<br> "y": 444<br> },<br> {<br> "x": 76,<br> "y": 444<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 444<br> },<br> {<br> "x": 187,<br> "y": 444<br> },<br> {<br> "x": 187,<br> "y": 467<br> },<br> {<br> "x": 76,<br> "y": 467<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 467<br> },<br> {<br> "x": 187,<br> "y": 467<br> },<br> {<br> "x": 187,<br> "y": 491<br> },<br> {<br> "x": 76,<br> "y": 491<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 491<br> },<br> {<br> "x": 187,<br> "y": 491<br> },<br> {<br> "x": 187,<br> "y": 514<br> },<br> {<br> "x": 76,<br> "y": 514<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 514<br> },<br> {<br> "x": 187,<br> "y": 514<br> },<br> {<br> "x": 187,<br> "y": 536<br> },<br> {<br> "x": 76,<br> "y": 536<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 76,<br> "y": 536<br> },<br> {<br> "x": 187,<br> "y": 536<br> },<br> {<br> "x": 187,<br> "y": 559<br> },<br> {<br> "x": 76,<br> "y": 559<br> }<br> \],<br> "value": ""<br> }<br> \],<br> "header\_box": \[<br> {<br> "x": 96,<br> "y": 79<br> },<br> {<br> "x": 162,<br> "y": 79<br> },<br> {<br> "x": 162,<br> "y": 98<br> },<br> {<br> "x": 96,<br> "y": 98<br> }<br> \],<br> "col\_name": "name"<br> },<br> {<br> "header\_value": "性别",<br> "bodies": \[<br> {<br> "prob": 0,<br> "fieldWordRaw": "男",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 100<br> },<br> {<br> "x": 296,<br> "y": 100<br> },<br> {<br> "x": 296,<br> "y": 123<br> },<br> {<br> "x": 187,<br> "y": 123<br> }<br> \],<br> "value": "男"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "男",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 123<br> },<br> {<br> "x": 296,<br> "y": 123<br> },<br> {<br> "x": 296,<br> "y": 146<br> },<br> {<br> "x": 187,<br> "y": 146<br> }<br> \],<br> "value": "男"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "男",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 146<br> },<br> {<br> "x": 296,<br> "y": 146<br> },<br> {<br> "x": 296,<br> "y": 169<br> },<br> {<br> "x": 187,<br> "y": 169<br> }<br> \],<br> "value": "男"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "男",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 169<br> },<br> {<br> "x": 296,<br> "y": 169<br> },<br> {<br> "x": 296,<br> "y": 191<br> },<br> {<br> "x": 187,<br> "y": 191<br> }<br> \],<br> "value": "男"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "男",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 191<br> },<br> {<br> "x": 296,<br> "y": 191<br> },<br> {<br> "x": 296,<br> "y": 215<br> },<br> {<br> "x": 187,<br> "y": 215<br> }<br> \],<br> "value": "男"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "男",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 215<br> },<br> {<br> "x": 296,<br> "y": 215<br> },<br> {<br> "x": 296,<br> "y": 238<br> },<br> {<br> "x": 187,<br> "y": 238<br> }<br> \],<br> "value": "男"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "女",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 238<br> },<br> {<br> "x": 296,<br> "y": 238<br> },<br> {<br> "x": 296,<br> "y": 261<br> },<br> {<br> "x": 187,<br> "y": 261<br> }<br> \],<br> "value": "女"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "女",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 261<br> },<br> {<br> "x": 296,<br> "y": 261<br> },<br> {<br> "x": 296,<br> "y": 283<br> },<br> {<br> "x": 187,<br> "y": 283<br> }<br> \],<br> "value": "女"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "女",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 283<br> },<br> {<br> "x": 296,<br> "y": 283<br> },<br> {<br> "x": 296,<br> "y": 307<br> },<br> {<br> "x": 187,<br> "y": 307<br> }<br> \],<br> "value": "女"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "女",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 307<br> },<br> {<br> "x": 296,<br> "y": 307<br> },<br> {<br> "x": 296,<br> "y": 330<br> },<br> {<br> "x": 187,<br> "y": 330<br> }<br> \],<br> "value": "女"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 330<br> },<br> {<br> "x": 296,<br> "y": 330<br> },<br> {<br> "x": 296,<br> "y": 352<br> },<br> {<br> "x": 187,<br> "y": 352<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 352<br> },<br> {<br> "x": 296,<br> "y": 352<br> },<br> {<br> "x": 296,<br> "y": 375<br> },<br> {<br> "x": 187,<br> "y": 375<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 375<br> },<br> {<br> "x": 296,<br> "y": 375<br> },<br> {<br> "x": 296,<br> "y": 399<br> },<br> {<br> "x": 187,<br> "y": 399<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 399<br> },<br> {<br> "x": 296,<br> "y": 399<br> },<br> {<br> "x": 296,<br> "y": 422<br> },<br> {<br> "x": 187,<br> "y": 422<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 422<br> },<br> {<br> "x": 296,<br> "y": 422<br> },<br> {<br> "x": 296,<br> "y": 444<br> },<br> {<br> "x": 187,<br> "y": 444<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 444<br> },<br> {<br> "x": 296,<br> "y": 444<br> },<br> {<br> "x": 296,<br> "y": 467<br> },<br> {<br> "x": 187,<br> "y": 467<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 467<br> },<br> {<br> "x": 296,<br> "y": 467<br> },<br> {<br> "x": 296,<br> "y": 491<br> },<br> {<br> "x": 187,<br> "y": 491<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 491<br> },<br> {<br> "x": 296,<br> "y": 491<br> },<br> {<br> "x": 296,<br> "y": 514<br> },<br> {<br> "x": 187,<br> "y": 514<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 514<br> },<br> {<br> "x": 296,<br> "y": 514<br> },<br> {<br> "x": 296,<br> "y": 536<br> },<br> {<br> "x": 187,<br> "y": 536<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 187,<br> "y": 536<br> },<br> {<br> "x": 296,<br> "y": 536<br> },<br> {<br> "x": 296,<br> "y": 559<br> },<br> {<br> "x": 187,<br> "y": 559<br> }<br> \],<br> "value": ""<br> }<br> \],<br> "header\_box": \[<br> {<br> "x": 210,<br> "y": 78<br> },<br> {<br> "x": 267,<br> "y": 78<br> },<br> {<br> "x": 267,<br> "y": 100<br> },<br> {<br> "x": 210,<br> "y": 100<br> }<br> \],<br> "col\_name": "sex"<br> },<br> {<br> "header\_value": "档案号",<br> "bodies": \[<br> {<br> "prob": 0,<br> "fieldWordRaw": "D001",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 100<br> },<br> {<br> "x": 520,<br> "y": 100<br> },<br> {<br> "x": 520,<br> "y": 123<br> },<br> {<br> "x": 406,<br> "y": 123<br> }<br> \],<br> "value": "D001"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D002",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 123<br> },<br> {<br> "x": 520,<br> "y": 123<br> },<br> {<br> "x": 520,<br> "y": 146<br> },<br> {<br> "x": 406,<br> "y": 146<br> }<br> \],<br> "value": "D002"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D003",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 146<br> },<br> {<br> "x": 520,<br> "y": 146<br> },<br> {<br> "x": 520,<br> "y": 169<br> },<br> {<br> "x": 406,<br> "y": 169<br> }<br> \],<br> "value": "D003"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D004",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 169<br> },<br> {<br> "x": 520,<br> "y": 169<br> },<br> {<br> "x": 520,<br> "y": 191<br> },<br> {<br> "x": 406,<br> "y": 191<br> }<br> \],<br> "value": "D004"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D005",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 191<br> },<br> {<br> "x": 520,<br> "y": 191<br> },<br> {<br> "x": 520,<br> "y": 215<br> },<br> {<br> "x": 406,<br> "y": 215<br> }<br> \],<br> "value": "D005"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D006",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 215<br> },<br> {<br> "x": 520,<br> "y": 215<br> },<br> {<br> "x": 520,<br> "y": 238<br> },<br> {<br> "x": 406,<br> "y": 238<br> }<br> \],<br> "value": "D006"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D007",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 238<br> },<br> {<br> "x": 520,<br> "y": 238<br> },<br> {<br> "x": 520,<br> "y": 261<br> },<br> {<br> "x": 406,<br> "y": 261<br> }<br> \],<br> "value": "D007"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D008",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 261<br> },<br> {<br> "x": 520,<br> "y": 261<br> },<br> {<br> "x": 520,<br> "y": 283<br> },<br> {<br> "x": 406,<br> "y": 283<br> }<br> \],<br> "value": "D008"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D009",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 283<br> },<br> {<br> "x": 520,<br> "y": 283<br> },<br> {<br> "x": 520,<br> "y": 307<br> },<br> {<br> "x": 406,<br> "y": 307<br> }<br> \],<br> "value": "D009"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "D010",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 307<br> },<br> {<br> "x": 520,<br> "y": 307<br> },<br> {<br> "x": 520,<br> "y": 330<br> },<br> {<br> "x": 406,<br> "y": 330<br> }<br> \],<br> "value": "D010"<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 330<br> },<br> {<br> "x": 520,<br> "y": 330<br> },<br> {<br> "x": 520,<br> "y": 352<br> },<br> {<br> "x": 406,<br> "y": 352<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 352<br> },<br> {<br> "x": 520,<br> "y": 352<br> },<br> {<br> "x": 520,<br> "y": 375<br> },<br> {<br> "x": 406,<br> "y": 375<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 375<br> },<br> {<br> "x": 520,<br> "y": 375<br> },<br> {<br> "x": 520,<br> "y": 398<br> },<br> {<br> "x": 406,<br> "y": 398<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 398<br> },<br> {<br> "x": 520,<br> "y": 398<br> },<br> {<br> "x": 520,<br> "y": 422<br> },<br> {<br> "x": 406,<br> "y": 422<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 422<br> },<br> {<br> "x": 520,<br> "y": 422<br> },<br> {<br> "x": 520,<br> "y": 444<br> },<br> {<br> "x": 406,<br> "y": 444<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 444<br> },<br> {<br> "x": 520,<br> "y": 444<br> },<br> {<br> "x": 520,<br> "y": 467<br> },<br> {<br> "x": 406,<br> "y": 467<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 467<br> },<br> {<br> "x": 520,<br> "y": 467<br> },<br> {<br> "x": 520,<br> "y": 491<br> },<br> {<br> "x": 406,<br> "y": 491<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 491<br> },<br> {<br> "x": 520,<br> "y": 491<br> },<br> {<br> "x": 520,<br> "y": 514<br> },<br> {<br> "x": 406,<br> "y": 514<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 514<br> },<br> {<br> "x": 520,<br> "y": 514<br> },<br> {<br> "x": 520,<br> "y": 536<br> },<br> {<br> "x": 406,<br> "y": 536<br> }<br> \],<br> "value": ""<br> },<br> {<br> "prob": 0,<br> "fieldWordRaw": "",<br> "wordInfo": \[\],<br> "location": \[<br> {<br> "x": 406,<br> "y": 536<br> },<br> {<br> "x": 520,<br> "y": 536<br> },<br> {<br> "x": 520,<br> "y": 559<br> },<br> {<br> "x": 406,<br> "y": 559<br> }<br> \],<br> "value": ""<br> }<br> \],<br> "header\_box": \[<br> {<br> "x": 430,<br> "y": 78<br> },<br> {<br> "x": 493,<br> "y": 78<br> },<br> {<br> "x": 493,<br> "y": 99<br> },<br> {<br> "x": 430,<br> "y": 99<br> }<br> \],<br> "col\_name": "ID"<br> }<br> \],<br> "table\_id": 1675670984484<br> }<br> \],<br> "code": 0,<br> "data": \[<br> {<br> "prob": 0.99,<br> "fieldWordRaw": "班级：初二3班",<br> "wordInfo": \[<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 2,<br> "y": 34<br> },<br> {<br> "x": 124,<br> "y": 34<br> },<br> {<br> "x": 124,<br> "y": 51<br> },<br> {<br> "x": 2,<br> "y": 51<br> }<br> \],<br> "word": "班级：初二3班",<br> "charInfo": \[<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 2,<br> "y": 34<br> },<br> {<br> "x": 18,<br> "y": 34<br> },<br> {<br> "x": 18,<br> "y": 48<br> },<br> {<br> "x": 2,<br> "y": 48<br> }<br> \],<br> "word": "班"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 18,<br> "y": 34<br> },<br> {<br> "x": 32,<br> "y": 34<br> },<br> {<br> "x": 32,<br> "y": 48<br> },<br> {<br> "x": 18,<br> "y": 48<br> }<br> \],<br> "word": "级"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 34,<br> "y": 34<br> },<br> {<br> "x": 50,<br> "y": 34<br> },<br> {<br> "x": 50,<br> "y": 48<br> },<br> {<br> "x": 34,<br> "y": 48<br> }<br> \],<br> "word": "："<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 52,<br> "y": 34<br> },<br> {<br> "x": 71,<br> "y": 34<br> },<br> {<br> "x": 71,<br> "y": 48<br> },<br> {<br> "x": 52,<br> "y": 48<br> }<br> \],<br> "word": "初"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 72,<br> "y": 34<br> },<br> {<br> "x": 88,<br> "y": 34<br> },<br> {<br> "x": 88,<br> "y": 48<br> },<br> {<br> "x": 72,<br> "y": 48<br> }<br> \],<br> "word": "二"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 90,<br> "y": 34<br> },<br> {<br> "x": 100,<br> "y": 34<br> },<br> {<br> "x": 100,<br> "y": 48<br> },<br> {<br> "x": 90,<br> "y": 48<br> }<br> \],<br> "word": "3"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 103,<br> "y": 34<br> },<br> {<br> "x": 124,<br> "y": 34<br> },<br> {<br> "x": 124,<br> "y": 48<br> },<br> {<br> "x": 103,<br> "y": 48<br> }<br> \],<br> "word": "班"<br> }<br> \]<br> }<br> \],<br> "name": "班级",<br> "location": \[<br> {<br> "x": 1,<br> "y": 30<br> },<br> {<br> "x": 1102,<br> "y": 30<br> },<br> {<br> "x": 1102,<br> "y": 54<br> },<br> {<br> "x": 1,<br> "y": 54<br> }<br> \],<br> "fieldWord": "班级：初二3班"<br> }<br> \],<br> "specificType": "infoCustomeTableTemp",<br> "className": "自定义表格模板测试cz02064-学生名",<br> "originalFileUrl": "https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/3/xxx/stage/upload/20230208/oss-uwGPIS8AsKcGRHfMRjvIrQVqN0uAxTgk.png?Expires=1675843535&OSSAccessKeyId=xxx&Signature=uPhg6JpDn47TgLt%2FI%2F7j4f%2FsFeA%3D",<br> "templateID": "269\_2b6819527769749d962bf51d034b1820",<br> "message": "",<br> "classType": "template",<br> "predictFile": "https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/3/xxx/stage/upload/20230208/oss-uwGPIS8AsKcGRHfMRjvIrQVqN0uAxTgk.png?Expires=1675843535&OSSAccessKeyId=xxx&Signature=uPhg6JpDn47TgLt%2FI%2F7j4f%2FsFeA%3D"<br>} |
| Message | string | 错误信息 | success |

分类器服务预测接口，返回 Data 字段解释说明：

```json
score         预测服务置信度 0-1
data          算法返回的预测结果，数组格式
tables        表格区域预测结果
prob          算法结果置信度 0-1
fieldName     抽取 key
fieldWord     抽取 value
location      抽取结果坐标位置 { "x": 119,"y": 48 }表示页面坐标点
wordInfo      抽取内容详细信息，包括了每个字符的位置信息
specificType  算法类型（infoCustomeKvTemp:自定义 KV 模板，infoCustomeTableTemp:自定义表格模板，ocr_infoExtractBill:信息抽取 OCR 识别，infoExtractBill:单据票证抽取，infoExtractDoc:长文档信息抽取 ）
classType     模型预测服务、模板预测服务
predictFile   预测文件地址（失效时间 60 分钟）
```

## 示例

正常返回示例

`JSON`格式

```prolog
{
  "RequestId": "232B91A8-9938-5C10-B522-127D1E342A57",
  "Code": 200,
  "Data": {
    "score": 1,
    "classID": "269_2b6819527769749d962bf51d034b1820",
    "tables": [\
      {\
        "columns": [\
          {\
            "header_value": "姓名",\
            "bodies": [\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生1",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 99\
                  },\
                  {\
                    "x": 187,\
                    "y": 99\
                  },\
                  {\
                    "x": 187,\
                    "y": 123\
                  },\
                  {\
                    "x": 76,\
                    "y": 123\
                  }\
                ],\
                "value": "学生1"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生2",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 123\
                  },\
                  {\
                    "x": 187,\
                    "y": 123\
                  },\
                  {\
                    "x": 187,\
                    "y": 146\
                  },\
                  {\
                    "x": 76,\
                    "y": 146\
                  }\
                ],\
                "value": "学生2"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生3",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 146\
                  },\
                  {\
                    "x": 187,\
                    "y": 146\
                  },\
                  {\
                    "x": 187,\
                    "y": 169\
                  },\
                  {\
                    "x": 76,\
                    "y": 169\
                  }\
                ],\
                "value": "学生3"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生4",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 169\
                  },\
                  {\
                    "x": 187,\
                    "y": 169\
                  },\
                  {\
                    "x": 187,\
                    "y": 191\
                  },\
                  {\
                    "x": 76,\
                    "y": 191\
                  }\
                ],\
                "value": "学生4"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生5",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 191\
                  },\
                  {\
                    "x": 187,\
                    "y": 191\
                  },\
                  {\
                    "x": 187,\
                    "y": 215\
                  },\
                  {\
                    "x": 76,\
                    "y": 215\
                  }\
                ],\
                "value": "学生5"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生6",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 215\
                  },\
                  {\
                    "x": 187,\
                    "y": 215\
                  },\
                  {\
                    "x": 187,\
                    "y": 238\
                  },\
                  {\
                    "x": 76,\
                    "y": 238\
                  }\
                ],\
                "value": "学生6"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生7",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 238\
                  },\
                  {\
                    "x": 187,\
                    "y": 238\
                  },\
                  {\
                    "x": 187,\
                    "y": 261\
                  },\
                  {\
                    "x": 76,\
                    "y": 261\
                  }\
                ],\
                "value": "学生7"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生8",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 261\
                  },\
                  {\
                    "x": 187,\
                    "y": 261\
                  },\
                  {\
                    "x": 187,\
                    "y": 283\
                  },\
                  {\
                    "x": 76,\
                    "y": 283\
                  }\
                ],\
                "value": "学生8"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生9",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 283\
                  },\
                  {\
                    "x": 187,\
                    "y": 283\
                  },\
                  {\
                    "x": 187,\
                    "y": 307\
                  },\
                  {\
                    "x": 76,\
                    "y": 307\
                  }\
                ],\
                "value": "学生9"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "学生10",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 307\
                  },\
                  {\
                    "x": 187,\
                    "y": 307\
                  },\
                  {\
                    "x": 187,\
                    "y": 330\
                  },\
                  {\
                    "x": 76,\
                    "y": 330\
                  }\
                ],\
                "value": "学生10"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 330\
                  },\
                  {\
                    "x": 187,\
                    "y": 330\
                  },\
                  {\
                    "x": 187,\
                    "y": 352\
                  },\
                  {\
                    "x": 76,\
                    "y": 352\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 352\
                  },\
                  {\
                    "x": 187,\
                    "y": 352\
                  },\
                  {\
                    "x": 187,\
                    "y": 375\
                  },\
                  {\
                    "x": 76,\
                    "y": 375\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 375\
                  },\
                  {\
                    "x": 187,\
                    "y": 375\
                  },\
                  {\
                    "x": 187,\
                    "y": 399\
                  },\
                  {\
                    "x": 76,\
                    "y": 399\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 399\
                  },\
                  {\
                    "x": 187,\
                    "y": 399\
                  },\
                  {\
                    "x": 187,\
                    "y": 422\
                  },\
                  {\
                    "x": 76,\
                    "y": 422\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 422\
                  },\
                  {\
                    "x": 187,\
                    "y": 422\
                  },\
                  {\
                    "x": 187,\
                    "y": 444\
                  },\
                  {\
                    "x": 76,\
                    "y": 444\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 444\
                  },\
                  {\
                    "x": 187,\
                    "y": 444\
                  },\
                  {\
                    "x": 187,\
                    "y": 467\
                  },\
                  {\
                    "x": 76,\
                    "y": 467\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 467\
                  },\
                  {\
                    "x": 187,\
                    "y": 467\
                  },\
                  {\
                    "x": 187,\
                    "y": 491\
                  },\
                  {\
                    "x": 76,\
                    "y": 491\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 491\
                  },\
                  {\
                    "x": 187,\
                    "y": 491\
                  },\
                  {\
                    "x": 187,\
                    "y": 514\
                  },\
                  {\
                    "x": 76,\
                    "y": 514\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 514\
                  },\
                  {\
                    "x": 187,\
                    "y": 514\
                  },\
                  {\
                    "x": 187,\
                    "y": 536\
                  },\
                  {\
                    "x": 76,\
                    "y": 536\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 76,\
                    "y": 536\
                  },\
                  {\
                    "x": 187,\
                    "y": 536\
                  },\
                  {\
                    "x": 187,\
                    "y": 559\
                  },\
                  {\
                    "x": 76,\
                    "y": 559\
                  }\
                ],\
                "value": ""\
              }\
            ],\
            "header_box": [\
              {\
                "x": 96,\
                "y": 79\
              },\
              {\
                "x": 162,\
                "y": 79\
              },\
              {\
                "x": 162,\
                "y": 98\
              },\
              {\
                "x": 96,\
                "y": 98\
              }\
            ],\
            "col_name": "name"\
          },\
          {\
            "header_value": "性别",\
            "bodies": [\
              {\
                "prob": 0,\
                "fieldWordRaw": "男",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 100\
                  },\
                  {\
                    "x": 296,\
                    "y": 100\
                  },\
                  {\
                    "x": 296,\
                    "y": 123\
                  },\
                  {\
                    "x": 187,\
                    "y": 123\
                  }\
                ],\
                "value": "男"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "男",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 123\
                  },\
                  {\
                    "x": 296,\
                    "y": 123\
                  },\
                  {\
                    "x": 296,\
                    "y": 146\
                  },\
                  {\
                    "x": 187,\
                    "y": 146\
                  }\
                ],\
                "value": "男"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "男",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 146\
                  },\
                  {\
                    "x": 296,\
                    "y": 146\
                  },\
                  {\
                    "x": 296,\
                    "y": 169\
                  },\
                  {\
                    "x": 187,\
                    "y": 169\
                  }\
                ],\
                "value": "男"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "男",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 169\
                  },\
                  {\
                    "x": 296,\
                    "y": 169\
                  },\
                  {\
                    "x": 296,\
                    "y": 191\
                  },\
                  {\
                    "x": 187,\
                    "y": 191\
                  }\
                ],\
                "value": "男"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "男",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 191\
                  },\
                  {\
                    "x": 296,\
                    "y": 191\
                  },\
                  {\
                    "x": 296,\
                    "y": 215\
                  },\
                  {\
                    "x": 187,\
                    "y": 215\
                  }\
                ],\
                "value": "男"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "男",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 215\
                  },\
                  {\
                    "x": 296,\
                    "y": 215\
                  },\
                  {\
                    "x": 296,\
                    "y": 238\
                  },\
                  {\
                    "x": 187,\
                    "y": 238\
                  }\
                ],\
                "value": "男"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "女",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 238\
                  },\
                  {\
                    "x": 296,\
                    "y": 238\
                  },\
                  {\
                    "x": 296,\
                    "y": 261\
                  },\
                  {\
                    "x": 187,\
                    "y": 261\
                  }\
                ],\
                "value": "女"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "女",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 261\
                  },\
                  {\
                    "x": 296,\
                    "y": 261\
                  },\
                  {\
                    "x": 296,\
                    "y": 283\
                  },\
                  {\
                    "x": 187,\
                    "y": 283\
                  }\
                ],\
                "value": "女"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "女",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 283\
                  },\
                  {\
                    "x": 296,\
                    "y": 283\
                  },\
                  {\
                    "x": 296,\
                    "y": 307\
                  },\
                  {\
                    "x": 187,\
                    "y": 307\
                  }\
                ],\
                "value": "女"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "女",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 307\
                  },\
                  {\
                    "x": 296,\
                    "y": 307\
                  },\
                  {\
                    "x": 296,\
                    "y": 330\
                  },\
                  {\
                    "x": 187,\
                    "y": 330\
                  }\
                ],\
                "value": "女"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 330\
                  },\
                  {\
                    "x": 296,\
                    "y": 330\
                  },\
                  {\
                    "x": 296,\
                    "y": 352\
                  },\
                  {\
                    "x": 187,\
                    "y": 352\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 352\
                  },\
                  {\
                    "x": 296,\
                    "y": 352\
                  },\
                  {\
                    "x": 296,\
                    "y": 375\
                  },\
                  {\
                    "x": 187,\
                    "y": 375\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 375\
                  },\
                  {\
                    "x": 296,\
                    "y": 375\
                  },\
                  {\
                    "x": 296,\
                    "y": 399\
                  },\
                  {\
                    "x": 187,\
                    "y": 399\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 399\
                  },\
                  {\
                    "x": 296,\
                    "y": 399\
                  },\
                  {\
                    "x": 296,\
                    "y": 422\
                  },\
                  {\
                    "x": 187,\
                    "y": 422\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 422\
                  },\
                  {\
                    "x": 296,\
                    "y": 422\
                  },\
                  {\
                    "x": 296,\
                    "y": 444\
                  },\
                  {\
                    "x": 187,\
                    "y": 444\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 444\
                  },\
                  {\
                    "x": 296,\
                    "y": 444\
                  },\
                  {\
                    "x": 296,\
                    "y": 467\
                  },\
                  {\
                    "x": 187,\
                    "y": 467\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 467\
                  },\
                  {\
                    "x": 296,\
                    "y": 467\
                  },\
                  {\
                    "x": 296,\
                    "y": 491\
                  },\
                  {\
                    "x": 187,\
                    "y": 491\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 491\
                  },\
                  {\
                    "x": 296,\
                    "y": 491\
                  },\
                  {\
                    "x": 296,\
                    "y": 514\
                  },\
                  {\
                    "x": 187,\
                    "y": 514\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 514\
                  },\
                  {\
                    "x": 296,\
                    "y": 514\
                  },\
                  {\
                    "x": 296,\
                    "y": 536\
                  },\
                  {\
                    "x": 187,\
                    "y": 536\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 187,\
                    "y": 536\
                  },\
                  {\
                    "x": 296,\
                    "y": 536\
                  },\
                  {\
                    "x": 296,\
                    "y": 559\
                  },\
                  {\
                    "x": 187,\
                    "y": 559\
                  }\
                ],\
                "value": ""\
              }\
            ],\
            "header_box": [\
              {\
                "x": 210,\
                "y": 78\
              },\
              {\
                "x": 267,\
                "y": 78\
              },\
              {\
                "x": 267,\
                "y": 100\
              },\
              {\
                "x": 210,\
                "y": 100\
              }\
            ],\
            "col_name": "sex"\
          },\
          {\
            "header_value": "档案号",\
            "bodies": [\
              {\
                "prob": 0,\
                "fieldWordRaw": "D001",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 100\
                  },\
                  {\
                    "x": 520,\
                    "y": 100\
                  },\
                  {\
                    "x": 520,\
                    "y": 123\
                  },\
                  {\
                    "x": 406,\
                    "y": 123\
                  }\
                ],\
                "value": "D001"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D002",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 123\
                  },\
                  {\
                    "x": 520,\
                    "y": 123\
                  },\
                  {\
                    "x": 520,\
                    "y": 146\
                  },\
                  {\
                    "x": 406,\
                    "y": 146\
                  }\
                ],\
                "value": "D002"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D003",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 146\
                  },\
                  {\
                    "x": 520,\
                    "y": 146\
                  },\
                  {\
                    "x": 520,\
                    "y": 169\
                  },\
                  {\
                    "x": 406,\
                    "y": 169\
                  }\
                ],\
                "value": "D003"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D004",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 169\
                  },\
                  {\
                    "x": 520,\
                    "y": 169\
                  },\
                  {\
                    "x": 520,\
                    "y": 191\
                  },\
                  {\
                    "x": 406,\
                    "y": 191\
                  }\
                ],\
                "value": "D004"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D005",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 191\
                  },\
                  {\
                    "x": 520,\
                    "y": 191\
                  },\
                  {\
                    "x": 520,\
                    "y": 215\
                  },\
                  {\
                    "x": 406,\
                    "y": 215\
                  }\
                ],\
                "value": "D005"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D006",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 215\
                  },\
                  {\
                    "x": 520,\
                    "y": 215\
                  },\
                  {\
                    "x": 520,\
                    "y": 238\
                  },\
                  {\
                    "x": 406,\
                    "y": 238\
                  }\
                ],\
                "value": "D006"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D007",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 238\
                  },\
                  {\
                    "x": 520,\
                    "y": 238\
                  },\
                  {\
                    "x": 520,\
                    "y": 261\
                  },\
                  {\
                    "x": 406,\
                    "y": 261\
                  }\
                ],\
                "value": "D007"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D008",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 261\
                  },\
                  {\
                    "x": 520,\
                    "y": 261\
                  },\
                  {\
                    "x": 520,\
                    "y": 283\
                  },\
                  {\
                    "x": 406,\
                    "y": 283\
                  }\
                ],\
                "value": "D008"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D009",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 283\
                  },\
                  {\
                    "x": 520,\
                    "y": 283\
                  },\
                  {\
                    "x": 520,\
                    "y": 307\
                  },\
                  {\
                    "x": 406,\
                    "y": 307\
                  }\
                ],\
                "value": "D009"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "D010",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 307\
                  },\
                  {\
                    "x": 520,\
                    "y": 307\
                  },\
                  {\
                    "x": 520,\
                    "y": 330\
                  },\
                  {\
                    "x": 406,\
                    "y": 330\
                  }\
                ],\
                "value": "D010"\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 330\
                  },\
                  {\
                    "x": 520,\
                    "y": 330\
                  },\
                  {\
                    "x": 520,\
                    "y": 352\
                  },\
                  {\
                    "x": 406,\
                    "y": 352\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 352\
                  },\
                  {\
                    "x": 520,\
                    "y": 352\
                  },\
                  {\
                    "x": 520,\
                    "y": 375\
                  },\
                  {\
                    "x": 406,\
                    "y": 375\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 375\
                  },\
                  {\
                    "x": 520,\
                    "y": 375\
                  },\
                  {\
                    "x": 520,\
                    "y": 398\
                  },\
                  {\
                    "x": 406,\
                    "y": 398\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 398\
                  },\
                  {\
                    "x": 520,\
                    "y": 398\
                  },\
                  {\
                    "x": 520,\
                    "y": 422\
                  },\
                  {\
                    "x": 406,\
                    "y": 422\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 422\
                  },\
                  {\
                    "x": 520,\
                    "y": 422\
                  },\
                  {\
                    "x": 520,\
                    "y": 444\
                  },\
                  {\
                    "x": 406,\
                    "y": 444\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 444\
                  },\
                  {\
                    "x": 520,\
                    "y": 444\
                  },\
                  {\
                    "x": 520,\
                    "y": 467\
                  },\
                  {\
                    "x": 406,\
                    "y": 467\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 467\
                  },\
                  {\
                    "x": 520,\
                    "y": 467\
                  },\
                  {\
                    "x": 520,\
                    "y": 491\
                  },\
                  {\
                    "x": 406,\
                    "y": 491\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 491\
                  },\
                  {\
                    "x": 520,\
                    "y": 491\
                  },\
                  {\
                    "x": 520,\
                    "y": 514\
                  },\
                  {\
                    "x": 406,\
                    "y": 514\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 514\
                  },\
                  {\
                    "x": 520,\
                    "y": 514\
                  },\
                  {\
                    "x": 520,\
                    "y": 536\
                  },\
                  {\
                    "x": 406,\
                    "y": 536\
                  }\
                ],\
                "value": ""\
              },\
              {\
                "prob": 0,\
                "fieldWordRaw": "",\
                "wordInfo": [],\
                "location": [\
                  {\
                    "x": 406,\
                    "y": 536\
                  },\
                  {\
                    "x": 520,\
                    "y": 536\
                  },\
                  {\
                    "x": 520,\
                    "y": 559\
                  },\
                  {\
                    "x": 406,\
                    "y": 559\
                  }\
                ],\
                "value": ""\
              }\
            ],\
            "header_box": [\
              {\
                "x": 430,\
                "y": 78\
              },\
              {\
                "x": 493,\
                "y": 78\
              },\
              {\
                "x": 493,\
                "y": 99\
              },\
              {\
                "x": 430,\
                "y": 99\
              }\
            ],\
            "col_name": "ID"\
          }\
        ],\
        "table_id": 1675670984484\
      }\
    ],
    "code": 0,
    "data": [\
      {\
        "prob": 0.99,\
        "fieldWordRaw": "班级：初二3班",\
        "wordInfo": [\
          {\
            "prob": 0.99,\
            "pos": [\
              {\
                "x": 2,\
                "y": 34\
              },\
              {\
                "x": 124,\
                "y": 34\
              },\
              {\
                "x": 124,\
                "y": 51\
              },\
              {\
                "x": 2,\
                "y": 51\
              }\
            ],\
            "word": "班级：初二3班",\
            "charInfo": [\
              {\
                "prob": 0.99,\
                "pos": [\
                  {\
                    "x": 2,\
                    "y": 34\
                  },\
                  {\
                    "x": 18,\
                    "y": 34\
                  },\
                  {\
                    "x": 18,\
                    "y": 48\
                  },\
                  {\
                    "x": 2,\
                    "y": 48\
                  }\
                ],\
                "word": "班"\
              },\
              {\
                "prob": 0.99,\
                "pos": [\
                  {\
                    "x": 18,\
                    "y": 34\
                  },\
                  {\
                    "x": 32,\
                    "y": 34\
                  },\
                  {\
                    "x": 32,\
                    "y": 48\
                  },\
                  {\
                    "x": 18,\
                    "y": 48\
                  }\
                ],\
                "word": "级"\
              },\
              {\
                "prob": 0.99,\
                "pos": [\
                  {\
                    "x": 34,\
                    "y": 34\
                  },\
                  {\
                    "x": 50,\
                    "y": 34\
                  },\
                  {\
                    "x": 50,\
                    "y": 48\
                  },\
                  {\
                    "x": 34,\
                    "y": 48\
                  }\
                ],\
                "word": "："\
              },\
              {\
                "prob": 0.99,\
                "pos": [\
                  {\
                    "x": 52,\
                    "y": 34\
                  },\
                  {\
                    "x": 71,\
                    "y": 34\
                  },\
                  {\
                    "x": 71,\
                    "y": 48\
                  },\
                  {\
                    "x": 52,\
                    "y": 48\
                  }\
                ],\
                "word": "初"\
              },\
              {\
                "prob": 0.99,\
                "pos": [\
                  {\
                    "x": 72,\
                    "y": 34\
                  },\
                  {\
                    "x": 88,\
                    "y": 34\
                  },\
                  {\
                    "x": 88,\
                    "y": 48\
                  },\
                  {\
                    "x": 72,\
                    "y": 48\
                  }\
                ],\
                "word": "二"\
              },\
              {\
                "prob": 0.99,\
                "pos": [\
                  {\
                    "x": 90,\
                    "y": 34\
                  },\
                  {\
                    "x": 100,\
                    "y": 34\
                  },\
                  {\
                    "x": 100,\
                    "y": 48\
                  },\
                  {\
                    "x": 90,\
                    "y": 48\
                  }\
                ],\
                "word": 3\
              },\
              {\
                "prob": 0.99,\
                "pos": [\
                  {\
                    "x": 103,\
                    "y": 34\
                  },\
                  {\
                    "x": 124,\
                    "y": 34\
                  },\
                  {\
                    "x": 124,\
                    "y": 48\
                  },\
                  {\
                    "x": 103,\
                    "y": 48\
                  }\
                ],\
                "word": "班"\
              }\
            ]\
          }\
        ],\
        "name": "班级",\
        "location": [\
          {\
            "x": 1,\
            "y": 30\
          },\
          {\
            "x": 1102,\
            "y": 30\
          },\
          {\
            "x": 1102,\
            "y": 54\
          },\
          {\
            "x": 1,\
            "y": 54\
          }\
        ],\
        "fieldWord": "班级：初二3班"\
      }\
    ],
    "specificType": "infoCustomeTableTemp",
    "className": "自定义表格模板测试cz02064-学生名",
    "originalFileUrl": "https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/3/xxx/stage/upload/20230208/oss-uwGPIS8AsKcGRHfMRjvIrQVqN0uAxTgk.png?Expires=1675843535&OSSAccessKeyId=xxx&Signature=uPhg6JpDn47TgLt%2FI%2F7j4f%2FsFeA%3D",
    "templateID": "269_2b6819527769749d962bf51d034b1820",
    "message": "",
    "classType": "template",
    "predictFile": "https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/3/xxx/stage/upload/20230208/oss-uwGPIS8AsKcGRHfMRjvIrQVqN0uAxTgk.png?Expires=1675843535&OSSAccessKeyId=xxx&Signature=uPhg6JpDn47TgLt%2FI%2F7j4f%2FsFeA%3D"
  },
  "Message": "success"
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
| 200 | 10002 | 没有权限 |
| 200 | 10003 | 非法状态 |
| 200 | 10005 | 服务不存在 |
| 200 | 21018 | 未找到模板信息 |
| 200 | 16001 | 未找到可预测的模型 |
| 200 | 16004 | 指定的模型不存在 |
| 200 | 23002 | 获取资源HTTP异常 |
| 200 | 22002 | ocr服务异常 |
| 200 | 11002 | 账号没有开通服务 |
| 200 | 19999 | 未知异常 |

访问[错误中心](https://api.aliyun.com/document/documentAutoml/2022-12-29/errorCode)查看更多错误码。

## 变更历史

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |
| 2023-05-05 | OpenAPI 错误码发生变更、OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/documentAutoml/2022-12-29/PredictClassifierModel?updateTime=2023-05-05#workbench-doc-change-demo) |
| 2023-04-10 | OpenAPI 错误码发生变更、OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/documentAutoml/2022-12-29/PredictClassifierModel?updateTime=2023-04-10#workbench-doc-change-demo) |
| 2023-03-31 | OpenAPI 错误码发生变更、OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/documentAutoml/2022-12-29/PredictClassifierModel?updateTime=2023-03-31#workbench-doc-change-demo) |
| 2023-03-23 | OpenAPI 错误码发生变更、OpenAPI 返回结构发生变更 | [查看变更详情](https://api.aliyun.com/document/documentAutoml/2022-12-29/PredictClassifierModel?updateTime=2023-03-23#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[OCR文档自学习](https://help.aliyun.com/zh/ocr/developer-reference/ocr-document-self-learning/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-documentautoml-2022-12-29-dir-ocr/)PredictClassifierModel - 分类器服务预测API

# PredictClassifierModel - 分类器服务预测API

更新时间：2025-12-22 21:36:10

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PredictModel - 模型服务预测API](https://help.aliyun.com/zh/ocr/developer-reference/api-documentautoml-2022-12-29-predictmodel-ocr)[下一篇：CreateModelAsyncPredict - 模型异步预测API](https://help.aliyun.com/zh/ocr/developer-reference/api-documentautoml-2022-12-29-createmodelasyncpredict-ocr)

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