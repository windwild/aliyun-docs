可快速精准的识别医疗器械生产许可证所包含许可证编号、法定代表人、企业名称、注册地址、生产地址、生产范围、企业负责人、有效期限等关键字段信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeMedicalDeviceProduceLicense)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeMedicalDeviceProduceLicense)

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
| ocr:RecognizeMedicalDeviceProduceLicense |  | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | 图片链接（长度不超 2048 字节，不支持 base64） | https://img.alicdn.com/tfs/TB13MJ.MuT2gK0jSZFvXXXnFXXa-1417-994.png |
| body | byte | 否 | 图片二进制文件，最大 10MB，与 URL 二选一。 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制文件 |

### 支持的图片格式

- PNG、JPG、JPEG、BMP、GIF、TIFF、WebP

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | { "data": { "registeredAddress": "深圳市龙岗区龙升路79号新意物流大厦", "issueDate": "二〇一三年十月二十九日", "licenseNumber": "粤食药监械生产许20132464号", "issueAuthority": "", "legalRepresentative": "王晶晶", "productionAddress": "深圳市龙岗区龙升路79号新意物流大厦", "responsiblePerson": "王晶晶", "companyName": "深圳永保科技有限公司", "validToDate": "2018年10月28日", "officeAddress": "", "productionScope": "Ⅱ类6826物理治疗及康复设备。" }, "figure": \[{ "type": "round\_stamp", "x": 992, "y": 681, "w": 158, "h": 162, "box": { "x": 0, "y": 0, "w": 0, "h": 0, "angle": -90 }, "points": \[{ "x": 992, "y": 682 }, { "x": 1149, "y": 681 }, { "x": 1150, "y": 842 }, { "x": 992, "y": 843 }\] }, { "type": "national\_emblem", "x": 635, "y": 14, "w": 174, "h": 184, "box": { "x": 0, "y": 0, "w": 0, "h": 0, "angle": -90 }, "points": \[{ "x": 635, "y": 14 }, { "x": 809, "y": 14 }, { "x": 808, "y": 198 }, { "x": 635, "y": 198 }\] }, { "type": "blicense\_title", "x": 264, "y": 274, "w": 911, "h": 105, "box": { "x": 0, "y": 0, "w": 0, "h": 0, "angle": -90 }, "points": \[{ "x": 264, "y": 274 }, { "x": 1172, "y": 274 }, { "x": 1175, "y": 379 }, { "x": 264, "y": 378 }\] }\], "height": 994, "orgHeight": 994, "orgWidth": 1417, "prism\_keyValueInfo": \[{ "key": "registeredAddress", "keyProb": 100, "value": "深圳市龙岗区龙升路79号新意物流大厦", "valuePos": \[{ "x": 627, "y": 510 }, { "x": 627, "y": 530 }, { "x": 304, "y": 530 }, { "x": 304, "y": 510 }\], "valueProb": 100 }, { "key": "issueDate", "keyProb": 99, "value": "二〇一三年十月二十九日", "valuePos": \[{ "x": 966, "y": 810 }, { "x": 1166, "y": 806 }, { "x": 1167, "y": 824 }, { "x": 967, "y": 828 }\], "valueProb": 99 }, { "key": "licenseNumber", "keyProb": 100, "value": "粤食药监械生产许20132464号", "valuePos": \[{ "x": 551, "y": 414 }, { "x": 551, "y": 433 }, { "x": 304, "y": 433 }, { "x": 304, "y": 414 }\], "valueProb": 100 }, { "key": "issueAuthority", "keyProb": 100, "value": "", "valueProb": 100 }, { "key": "legalRepresentative", "keyProb": 100, "value": "王晶晶", "valuePos": \[{ "x": 1028, "y": 420 }, { "x": 1028, "y": 435 }, { "x": 978, "y": 435 }, { "x": 978, "y": 420 }\], "valueProb": 100 }, { "key": "productionAddress", "keyProb": 100, "value": "深圳市龙岗区龙升路79号新意物流大厦", "valuePos": \[{ "x": 630, "y": 603 }, { "x": 630, "y": 622 }, { "x": 307, "y": 622 }, { "x": 307, "y": 603 }\], "valueProb": 100 }, { "key": "responsiblePerson", "keyProb": 100, "value": "王晶晶", "valuePos": \[{ "x": 1029, "y": 463 }, { "x": 1029, "y": 479 }, { "x": 980, "y": 479 }, { "x": 980, "y": 463 }\], "valueProb": 100 }, { "key": "companyName", "keyProb": 100, "value": "深圳永保科技有限公司", "valuePos": \[{ "x": 481, "y": 462 }, { "x": 481, "y": 481 }, { "x": 311, "y": 481 }, { "x": 311, "y": 462 }\], "valueProb": 100 }, { "key": "validToDate", "keyProb": 100, "value": "2018年10月28日", "valuePos": \[{ "x": 434, "y": 816 }, { "x": 434, "y": 835 }, { "x": 306, "y": 835 }, { "x": 306, "y": 816 }\], "valueProb": 100 }, { "key": "officeAddress", "keyProb": 100, "value": "", "valueProb": 100 }, { "key": "productionScope", "keyProb": 99, "value": "Ⅱ类6826物理治疗及康复设备。", "valuePos": \[{ "x": 308, "y": 686 }, { "x": 494, "y": 684 }, { "x": 495, "y": 704 }, { "x": 309, "y": 707 }\], "valueProb": 99 }\], "width": 1417 } |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

中英文字段映射

```nginx
registeredAddress 注册地址
issueDate 发证日期
licenseNumber 许可证编号
issueAuthority 发证部门
legalRepresentative 法定代表人
productionAddress 生产地址
responsiblePerson 企业负责人
companyName 企业名称
validToDate 有效期限
officeAddress 住所
productionScope 生产范围
```

## 示例

正常返回示例

`JSON`格式

```prolog
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "data": {
      "registeredAddress": "深圳市龙岗区龙升路79号新意物流大厦",
      "issueDate": "二〇一三年十月二十九日",
      "licenseNumber": "粤食药监械生产许20132464号",
      "issueAuthority": "",
      "legalRepresentative": "王晶晶",
      "productionAddress": "深圳市龙岗区龙升路79号新意物流大厦",
      "responsiblePerson": "王晶晶",
      "companyName": "深圳永保科技有限公司",
      "validToDate": "2018年10月28日",
      "officeAddress": "",
      "productionScope": "Ⅱ类6826物理治疗及康复设备。"
    },
    "figure": [\
      {\
        "type": "round_stamp",\
        "x": 992,\
        "y": 681,\
        "w": 158,\
        "h": 162,\
        "box": {\
          "x": 0,\
          "y": 0,\
          "w": 0,\
          "h": 0,\
          "angle": -90\
        },\
        "points": [\
          {\
            "x": 992,\
            "y": 682\
          },\
          {\
            "x": 1149,\
            "y": 681\
          },\
          {\
            "x": 1150,\
            "y": 842\
          },\
          {\
            "x": 992,\
            "y": 843\
          }\
        ]\
      },\
      {\
        "type": "national_emblem",\
        "x": 635,\
        "y": 14,\
        "w": 174,\
        "h": 184,\
        "box": {\
          "x": 0,\
          "y": 0,\
          "w": 0,\
          "h": 0,\
          "angle": -90\
        },\
        "points": [\
          {\
            "x": 635,\
            "y": 14\
          },\
          {\
            "x": 809,\
            "y": 14\
          },\
          {\
            "x": 808,\
            "y": 198\
          },\
          {\
            "x": 635,\
            "y": 198\
          }\
        ]\
      },\
      {\
        "type": "blicense_title",\
        "x": 264,\
        "y": 274,\
        "w": 911,\
        "h": 105,\
        "box": {\
          "x": 0,\
          "y": 0,\
          "w": 0,\
          "h": 0,\
          "angle": -90\
        },\
        "points": [\
          {\
            "x": 264,\
            "y": 274\
          },\
          {\
            "x": 1172,\
            "y": 274\
          },\
          {\
            "x": 1175,\
            "y": 379\
          },\
          {\
            "x": 264,\
            "y": 378\
          }\
        ]\
      }\
    ],
    "height": 994,
    "orgHeight": 994,
    "orgWidth": 1417,
    "prism_keyValueInfo": [\
      {\
        "key": "registeredAddress",\
        "keyProb": 100,\
        "value": "深圳市龙岗区龙升路79号新意物流大厦",\
        "valuePos": [\
          {\
            "x": 627,\
            "y": 510\
          },\
          {\
            "x": 627,\
            "y": 530\
          },\
          {\
            "x": 304,\
            "y": 530\
          },\
          {\
            "x": 304,\
            "y": 510\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "issueDate",\
        "keyProb": 99,\
        "value": "二〇一三年十月二十九日",\
        "valuePos": [\
          {\
            "x": 966,\
            "y": 810\
          },\
          {\
            "x": 1166,\
            "y": 806\
          },\
          {\
            "x": 1167,\
            "y": 824\
          },\
          {\
            "x": 967,\
            "y": 828\
          }\
        ],\
        "valueProb": 99\
      },\
      {\
        "key": "licenseNumber",\
        "keyProb": 100,\
        "value": "粤食药监械生产许20132464号",\
        "valuePos": [\
          {\
            "x": 551,\
            "y": 414\
          },\
          {\
            "x": 551,\
            "y": 433\
          },\
          {\
            "x": 304,\
            "y": 433\
          },\
          {\
            "x": 304,\
            "y": 414\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "issueAuthority",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "legalRepresentative",\
        "keyProb": 100,\
        "value": "王晶晶",\
        "valuePos": [\
          {\
            "x": 1028,\
            "y": 420\
          },\
          {\
            "x": 1028,\
            "y": 435\
          },\
          {\
            "x": 978,\
            "y": 435\
          },\
          {\
            "x": 978,\
            "y": 420\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "productionAddress",\
        "keyProb": 100,\
        "value": "深圳市龙岗区龙升路79号新意物流大厦",\
        "valuePos": [\
          {\
            "x": 630,\
            "y": 603\
          },\
          {\
            "x": 630,\
            "y": 622\
          },\
          {\
            "x": 307,\
            "y": 622\
          },\
          {\
            "x": 307,\
            "y": 603\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "responsiblePerson",\
        "keyProb": 100,\
        "value": "王晶晶",\
        "valuePos": [\
          {\
            "x": 1029,\
            "y": 463\
          },\
          {\
            "x": 1029,\
            "y": 479\
          },\
          {\
            "x": 980,\
            "y": 479\
          },\
          {\
            "x": 980,\
            "y": 463\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "companyName",\
        "keyProb": 100,\
        "value": "深圳永保科技有限公司",\
        "valuePos": [\
          {\
            "x": 481,\
            "y": 462\
          },\
          {\
            "x": 481,\
            "y": 481\
          },\
          {\
            "x": 311,\
            "y": 481\
          },\
          {\
            "x": 311,\
            "y": 462\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "validToDate",\
        "keyProb": 100,\
        "value": "2018年10月28日",\
        "valuePos": [\
          {\
            "x": 434,\
            "y": 816\
          },\
          {\
            "x": 434,\
            "y": 835\
          },\
          {\
            "x": 306,\
            "y": 835\
          },\
          {\
            "x": 306,\
            "y": 816\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "officeAddress",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "productionScope",\
        "keyProb": 99,\
        "value": "Ⅱ类6826物理治疗及康复设备。",\
        "valuePos": [\
          {\
            "x": 308,\
            "y": 686\
          },\
          {\
            "x": 494,\
            "y": 684\
          },\
          {\
            "x": 495,\
            "y": 704\
          },\
          {\
            "x": 309,\
            "y": 707\
          }\
        ],\
        "valueProb": 99\
      }\
    ],
    "width": 1417
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
| 2021-08-17 | OpenAPI 入参发生变更 | [查看变更详情](https://api.aliyun.com/document/ocr-api/2021-07-07/RecognizeMedicalDeviceProduceLicense?updateTime=2021-08-17#workbench-doc-change-demo) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[企业资质识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-enterprise-qualification-identification/)RecognizeMedicalDeviceProduceLicense - 医疗器械生产许可证识别

# RecognizeMedicalDeviceProduceLicense - 医疗器械生产许可证识别

更新时间：2025-12-08 21:10:32

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeMedicalDeviceManageLicense - 医疗器械经营许可证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizemedicaldevicemanagelicense)[下一篇：RecognizeCtwoMedicalDeviceManageLicense - 第二类医疗器械经营备案凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizectwomedicaldevicemanagelicense)

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