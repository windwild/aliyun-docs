预置能力现有：UIE抽取，适用于通用智能预标注。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/documentAutoml/2022-12-29/PredictPreTrainModel)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/documentAutoml/2022-12-29/PredictPreTrainModel)

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
| documentautoml:PredictPreTrainModel | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Content | string | 否 | 预测内容，格式为 JSON 字符串。<br>UIE 抽取参数格式{"query":"xxx","schema":\["字段 1","字段 2"\]}, query 对应图片 URL，schema 对应要抽取的字段数组 | {"query":"https://doc-automl-public.oss-cn-hangzhou.aliyuncs.com/demo/extractBill.png", "schema":\["姓名", "住址"\]} |
| ServiceVersion | string | 否 | 预置能力服务版本，默认 V1 | V1 |
| ServiceName | string | 否 | 预置能力服务名称，必填<br>UIE 抽取对应“FormUIE” | FormUIE |
| BinaryToText | boolean | 否 | content 字段内容为图片 URL 时：false，<br>body 字段内容为图片 base64 时：true | false |
| Body | string | 否 | 图片传递 base64 编码时的预测内容，格式为 json 字符串。<br>UIE 抽取参数格式{"query":"xxx","schema":\["字段 1","字段 2"\]}, query 对应图片 base64 编码，schema 对应要抽取的字段数组 | {"query":"data:image/png;base64,xxxxx","schema":\["姓名", "住址"\]} |

BinaryToText 为非必填项

content 字段和 body 字段传参二选一，图片内容是 URL，在传递 content 字段，内容是 base64，传递 body 字段，且 BinaryToText 传 true

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | Id of the request | 29413C69-11EF-15CB-BE20-70D318E2F4E9 |
| Code | integer | 请求结果状态，200 为成功 | 200 |
| Message | string | 错误信息 | success |
| Data | object | 接口返回信息 | {<br> "RequestId": "29413C69-11EF-15CB-BE20-70D318E2F4E9",<br> "Message": "success",<br> "Data": {<br> "score": 1,<br> "data": \[<br> {<br> "prob": 0.9138551354408264,<br> "fieldWordRaw": "xx",<br> "wordInfo": \[<br> {<br> "prob": 0.9138551354408264,<br> "pos": \[<br> {<br> "x": 468,<br> "y": 139<br> },<br> {<br> "x": 476,<br> "y": 139<br> },<br> {<br> "x": 476,<br> "y": 153<br> },<br> {<br> "x": 468,<br> "y": 153<br> }<br> \],<br> "word": "xx",<br> "charInfo": \[<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 468,<br> "y": 139<br> },<br> {<br> "x": 471,<br> "y": 139<br> },<br> {<br> "x": 471,<br> "y": 153<br> },<br> {<br> "x": 468,<br> "y": 153<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 473,<br> "y": 139<br> },<br> {<br> "x": 476,<br> "y": 139<br> },<br> {<br> "x": 476,<br> "y": 153<br> },<br> {<br> "x": 473,<br> "y": 153<br> }<br> \],<br> "word": "x"<br> }<br> \]<br> }<br> \],<br> "name": "姓名",<br> "location": \[<br> {<br> "x": 468,<br> "y": 139<br> },<br> {<br> "x": 476,<br> "y": 139<br> },<br> {<br> "x": 476,<br> "y": 153<br> },<br> {<br> "x": 468,<br> "y": 153<br> }<br> \],<br> "fieldWord": "xx"<br> },<br> {<br> "prob": 0.9594210982322693,<br> "fieldWordRaw": "xxxxxxxxxxx",<br> "wordInfo": \[<br> {<br> "prob": 0.9594210982322693,<br> "pos": \[<br> {<br> "x": 168,<br> "y": 164<br> },<br> {<br> "x": 467,<br> "y": 164<br> },<br> {<br> "x": 467,<br> "y": 239<br> },<br> {<br> "x": 168,<br> "y": 239<br> }<br> \],<br> "word": "xxxxxxxxxxx",<br> "charInfo": \[<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 366,<br> "y": 164<br> },<br> {<br> "x": 383,<br> "y": 164<br> },<br> {<br> "x": 383,<br> "y": 179<br> },<br> {<br> "x": 366,<br> "y": 179<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 384,<br> "y": 164<br> },<br> {<br> "x": 401,<br> "y": 164<br> },<br> {<br> "x": 401,<br> "y": 179<br> },<br> {<br> "x": 384,<br> "y": 179<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 402,<br> "y": 164<br> },<br> {<br> "x": 414,<br> "y": 164<br> },<br> {<br> "x": 414,<br> "y": 179<br> },<br> {<br> "x": 402,<br> "y": 179<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 418,<br> "y": 164<br> },<br> {<br> "x": 427,<br> "y": 164<br> },<br> {<br> "x": 427,<br> "y": 179<br> },<br> {<br> "x": 418,<br> "y": 179<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 429,<br> "y": 164<br> },<br> {<br> "x": 438,<br> "y": 164<br> },<br> {<br> "x": 438,<br> "y": 179<br> },<br> {<br> "x": 429,<br> "y": 179<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 439,<br> "y": 164<br> },<br> {<br> "x": 448,<br> "y": 164<br> },<br> {<br> "x": 448,<br> "y": 179<br> },<br> {<br> "x": 439,<br> "y": 179<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 450,<br> "y": 164<br> },<br> {<br> "x": 467,<br> "y": 164<br> },<br> {<br> "x": 467,<br> "y": 179<br> },<br> {<br> "x": 450,<br> "y": 179<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 168,<br> "y": 224<br> },<br> {<br> "x": 180,<br> "y": 224<br> },<br> {<br> "x": 180,<br> "y": 239<br> },<br> {<br> "x": 168,<br> "y": 239<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 180,<br> "y": 224<br> },<br> {<br> "x": 192,<br> "y": 224<br> },<br> {<br> "x": 192,<br> "y": 239<br> },<br> {<br> "x": 180,<br> "y": 239<br> }<br> \],<br> "word": "x"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 195,<br> "y": 224<br> },<br> {<br> "x": 209,<br> "y": 224<br> },<br> {<br> "x": 209,<br> "y": 239<br> },<br> {<br> "x": 195,<br> "y": 239<br> }<br> \],<br> "word": "1"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 211,<br> "y": 224<br> },<br> {<br> "x": 223,<br> "y": 224<br> },<br> {<br> "x": 223,<br> "y": 239<br> },<br> {<br> "x": 211,<br> "y": 239<br> }<br> \],<br> "word": "7"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 224,<br> "y": 224<br> },<br> {<br> "x": 236,<br> "y": 224<br> },<br> {<br> "x": 236,<br> "y": 239<br> },<br> {<br> "x": 224,<br> "y": 239<br> }<br> \],<br> "word": "2"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 237,<br> "y": 224<br> },<br> {<br> "x": 249,<br> "y": 224<br> },<br> {<br> "x": 249,<br> "y": 239<br> },<br> {<br> "x": 237,<br> "y": 239<br> }<br> \],<br> "word": "7"<br> },<br> {<br> "prob": 0.99,<br> "pos": \[<br> {<br> "x": 253,<br> "y": 224<br> },<br> {<br> "x": 270,<br> "y": 224<br> },<br> {<br> "x": 270,<br> "y": 239<br> },<br> {<br> "x": 253,<br> "y": 239<br> }<br> \],<br> "word": "x"<br> }<br> \]<br> }<br> \],<br> "name": "住址",<br> "location": \[<br> {<br> "x": 168,<br> "y": 164<br> },<br> {<br> "x": 467,<br> "y": 164<br> },<br> {<br> "x": 467,<br> "y": 239<br> },<br> {<br> "x": 168,<br> "y": 239<br> }<br> \],<br> "fieldWord": "xxxxxxxx"<br> }<br> \],<br> "specificType": "formuie-anti",<br> "classType": "preDefinedServer",<br> "predictFile": "https://xxxx"<br> },<br> "Code": 200<br>} |

模板服务预测接口，返回 Data 字段解释说明：

score 预测服务置信度 0-1

data. 算法返回的预测结果，数组格式

prob 算法结果置信度 0-1

name 抽取 key

fieldWord 抽取 value

location 抽取结果坐标位置 { "x": 119,"y": 48 }表示页面坐标点

wordInfo 抽取内容详细信息，包括了每个字符的位置信息

specificType 算法类型（formuie-anti:UIE 抽取）

classType preDefinedServer: 预置能力

predictFile 预测文件地址（失效时间 60 分钟）

## 示例

正常返回示例

`JSON`格式

```prolog
{
  "RequestId": "29413C69-11EF-15CB-BE20-70D318E2F4E9",
  "Code": 200,
  "Message": "success",
  "Data": {
    "RequestId": "29413C69-11EF-15CB-BE20-70D318E2F4E9",
    "Message": "success",
    "Data": {
      "score": 1,
      "data": [\
        {\
          "prob": 0.9138551354408264,\
          "fieldWordRaw": "xx",\
          "wordInfo": [\
            {\
              "prob": 0.9138551354408264,\
              "pos": [\
                {\
                  "x": 468,\
                  "y": 139\
                },\
                {\
                  "x": 476,\
                  "y": 139\
                },\
                {\
                  "x": 476,\
                  "y": 153\
                },\
                {\
                  "x": 468,\
                  "y": 153\
                }\
              ],\
              "word": "xx",\
              "charInfo": [\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 468,\
                      "y": 139\
                    },\
                    {\
                      "x": 471,\
                      "y": 139\
                    },\
                    {\
                      "x": 471,\
                      "y": 153\
                    },\
                    {\
                      "x": 468,\
                      "y": 153\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 473,\
                      "y": 139\
                    },\
                    {\
                      "x": 476,\
                      "y": 139\
                    },\
                    {\
                      "x": 476,\
                      "y": 153\
                    },\
                    {\
                      "x": 473,\
                      "y": 153\
                    }\
                  ],\
                  "word": "x"\
                }\
              ]\
            }\
          ],\
          "name": "姓名",\
          "location": [\
            {\
              "x": 468,\
              "y": 139\
            },\
            {\
              "x": 476,\
              "y": 139\
            },\
            {\
              "x": 476,\
              "y": 153\
            },\
            {\
              "x": 468,\
              "y": 153\
            }\
          ],\
          "fieldWord": "xx"\
        },\
        {\
          "prob": 0.9594210982322693,\
          "fieldWordRaw": "xxxxxxxxxxx",\
          "wordInfo": [\
            {\
              "prob": 0.9594210982322693,\
              "pos": [\
                {\
                  "x": 168,\
                  "y": 164\
                },\
                {\
                  "x": 467,\
                  "y": 164\
                },\
                {\
                  "x": 467,\
                  "y": 239\
                },\
                {\
                  "x": 168,\
                  "y": 239\
                }\
              ],\
              "word": "xxxxxxxxxxx",\
              "charInfo": [\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 366,\
                      "y": 164\
                    },\
                    {\
                      "x": 383,\
                      "y": 164\
                    },\
                    {\
                      "x": 383,\
                      "y": 179\
                    },\
                    {\
                      "x": 366,\
                      "y": 179\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 384,\
                      "y": 164\
                    },\
                    {\
                      "x": 401,\
                      "y": 164\
                    },\
                    {\
                      "x": 401,\
                      "y": 179\
                    },\
                    {\
                      "x": 384,\
                      "y": 179\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 402,\
                      "y": 164\
                    },\
                    {\
                      "x": 414,\
                      "y": 164\
                    },\
                    {\
                      "x": 414,\
                      "y": 179\
                    },\
                    {\
                      "x": 402,\
                      "y": 179\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 418,\
                      "y": 164\
                    },\
                    {\
                      "x": 427,\
                      "y": 164\
                    },\
                    {\
                      "x": 427,\
                      "y": 179\
                    },\
                    {\
                      "x": 418,\
                      "y": 179\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 429,\
                      "y": 164\
                    },\
                    {\
                      "x": 438,\
                      "y": 164\
                    },\
                    {\
                      "x": 438,\
                      "y": 179\
                    },\
                    {\
                      "x": 429,\
                      "y": 179\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 439,\
                      "y": 164\
                    },\
                    {\
                      "x": 448,\
                      "y": 164\
                    },\
                    {\
                      "x": 448,\
                      "y": 179\
                    },\
                    {\
                      "x": 439,\
                      "y": 179\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 450,\
                      "y": 164\
                    },\
                    {\
                      "x": 467,\
                      "y": 164\
                    },\
                    {\
                      "x": 467,\
                      "y": 179\
                    },\
                    {\
                      "x": 450,\
                      "y": 179\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 168,\
                      "y": 224\
                    },\
                    {\
                      "x": 180,\
                      "y": 224\
                    },\
                    {\
                      "x": 180,\
                      "y": 239\
                    },\
                    {\
                      "x": 168,\
                      "y": 239\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 180,\
                      "y": 224\
                    },\
                    {\
                      "x": 192,\
                      "y": 224\
                    },\
                    {\
                      "x": 192,\
                      "y": 239\
                    },\
                    {\
                      "x": 180,\
                      "y": 239\
                    }\
                  ],\
                  "word": "x"\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 195,\
                      "y": 224\
                    },\
                    {\
                      "x": 209,\
                      "y": 224\
                    },\
                    {\
                      "x": 209,\
                      "y": 239\
                    },\
                    {\
                      "x": 195,\
                      "y": 239\
                    }\
                  ],\
                  "word": 1\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 211,\
                      "y": 224\
                    },\
                    {\
                      "x": 223,\
                      "y": 224\
                    },\
                    {\
                      "x": 223,\
                      "y": 239\
                    },\
                    {\
                      "x": 211,\
                      "y": 239\
                    }\
                  ],\
                  "word": 7\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 224,\
                      "y": 224\
                    },\
                    {\
                      "x": 236,\
                      "y": 224\
                    },\
                    {\
                      "x": 236,\
                      "y": 239\
                    },\
                    {\
                      "x": 224,\
                      "y": 239\
                    }\
                  ],\
                  "word": 2\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 237,\
                      "y": 224\
                    },\
                    {\
                      "x": 249,\
                      "y": 224\
                    },\
                    {\
                      "x": 249,\
                      "y": 239\
                    },\
                    {\
                      "x": 237,\
                      "y": 239\
                    }\
                  ],\
                  "word": 7\
                },\
                {\
                  "prob": 0.99,\
                  "pos": [\
                    {\
                      "x": 253,\
                      "y": 224\
                    },\
                    {\
                      "x": 270,\
                      "y": 224\
                    },\
                    {\
                      "x": 270,\
                      "y": 239\
                    },\
                    {\
                      "x": 253,\
                      "y": 239\
                    }\
                  ],\
                  "word": "x"\
                }\
              ]\
            }\
          ],\
          "name": "住址",\
          "location": [\
            {\
              "x": 168,\
              "y": 164\
            },\
            {\
              "x": 467,\
              "y": 164\
            },\
            {\
              "x": 467,\
              "y": 239\
            },\
            {\
              "x": 168,\
              "y": 239\
            }\
          ],\
          "fieldWord": "xxxxxxxx"\
        }\
      ],
      "specificType": "formuie-anti",
      "classType": "preDefinedServer",
      "predictFile": "https://xxxx"
    },
    "Code": 200
  }
}
```

## 错误码

| HTTP status code | 错误码 | 错误信息 |
| --- | --- | --- |

| HTTP status code | 错误码 | 错误信息 |
| --- | --- | --- |
| 200 | 21002 | 模板预测超时 |
| 200 | 21003 | 模版预测失败 |
| 200 | 10001 | 参数出错 |
| 200 | 16001 | 未找到可预测的模型 |
| 200 | 13018 | 未找到模型信息 |
| 200 | 16004 | 指定模型不存在 |
| 200 | 23002 | 获取资源HTTP异常 |
| 200 | 11002 | 账号没有开通服务 |
| 200 | 19999 | 未知异常 |
| 200 | 50008 | 文件过大 |
| 200 | 50007 | 文件格式不支持 |
| 200 | 10005 | 服务不存在 |

访问[错误中心](https://api.aliyun.com/document/documentAutoml/2022-12-29/errorCode)查看更多错误码。

## 变更历史

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |

| 变更时间 | 变更内容概要 | 操作 |
| --- | --- | --- |

暂无变更历史

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[OCR文档自学习](https://help.aliyun.com/zh/ocr/developer-reference/ocr-document-self-learning/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-documentautoml-2022-12-29-dir-ocr/)PredictPreTrainModel - 预置能力服务预测API

# PredictPreTrainModel - 预置能力服务预测API

更新时间：2025-12-22 21:36:10

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：GetModelAsyncPredict - 获取模型异步预测结果API](https://help.aliyun.com/zh/ocr/developer-reference/api-documentautoml-2022-12-29-getmodelasyncpredict-ocr)[下一篇：版本说明](https://help.aliyun.com/zh/ocr/developer-reference/api-documentautoml-2022-12-29-changeset-ocr)

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