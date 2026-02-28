支持包括开票方名称、开票日期、联系电话、地址、合计（实际）金额等关键字段结构化识别输出。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeShoppingReceipt)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeShoppingReceipt)

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
| ocr:RecognizeShoppingReceipt | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | 图片链接（长度不超 2048 字节，不支持 base64） | http://duguang-database-public.oss-cn-hangzhou.aliyuncs.com/multi\_receipt\_shopping\_receipt/shop\_receipt\_\_ticket\_2020-05-14-11-59-30.540668\_01\_List.jpg |
| body | byte | 否 | 图片二进制字节流，最大 10MB | 图片二进制 |

### 支持的图片格式

- PNG、JPG、JPEG、BMP、GIF、TIFF、WebP

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"algo\_version": "", "data": {"contactNumber": "", "receiptDate": "2020-04-23", "receiptDetails": \[{"amount": "5.30", "itemName": "雕牌超效加酶无砖", "quantity": "", "unitPrice": ""}\], "receiptTime": "20:26:00", "shopAddress": "", "shopName": "世纪联华椒江巾府大道店", "totalAmount": "5.00元"}, "ftype": 0, "height": 1042, "orgHeight": 1055, "orgWidth": 690, "prism\_keyValueInfo": \[{"key": "shopName", "keyProb": 99, "value": "世纪联华椒江巾府大道店", "valuePos": \[{"x": 56, "y": 208}, {"x": 452, "y": 230}, {"x": 451, "y": 258}, {"x": 54, "y": 236}\], "valueProb": 99}, {"key": "receiptDate", "keyProb": 100, "value": "2020-04-23", "valuePos": \[{"x": 300, "y": 644}, {"x": 434, "y": 647}, {"x": 434, "y": 675}, {"x": 299, "y": 671}\], "valueProb": 100}, {"key": "receiptTime", "keyProb": 100, "value": "20:26:00", "valuePos": \[{"x": 442, "y": 648}, {"x": 553, "y": 651}, {"x": 552, "y": 679}, {"x": 441, "y": 676}\], "valueProb": 100}, {"key": "contactNumber", "keyProb": 100, "value": "", "valueProb": 100}, {"key": "shopAddress", "keyProb": 100, "value": "", "valueProb": 100}, {"key": "totalAmount", "keyProb": 100, "value": "5.00元", "valuePos": \[{"x": 480, "y": 437}, {"x": 574, "y": 435}, {"x": 574, "y": 466}, {"x": 480, "y": 467}\], "valueProb": 100}, {"key": "receiptDetails", "keyProb": 100, "value": "\[{\\"amount\\":\\"5.30\\",\\"itemName\\":\\"雕牌超效加酶无砖\\",\\"quantity\\":\\"\\",\\"unitPrice\\":\\"\\"}\]", "valueProb": 100}\], "sliceRect": {"x0": 11, "x1": 690, "x2": 689, "x3": 1, "y0": 13, "y1": 43, "y2": 1055, "y3": 1055}, "width": 689} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

## 中英文字段映射

```apache
data    结构化信息
prism_keyValueInfo    结构化信息的坐标信息
ftype    是否是复印件（1:是，0:否）
```

- **data 内字段说明**

```mipsasm
shopName    开票方名称
receiptDate    开票日期
receiptTime    开票时间
contactNumber    联系电话
shopAddress    地址
totalAmount    合计(实付)金额
receiptDetails    商品详单
```

- **prism\_keyValueInfo 数组** 字段说明

```gauss
key    识别出的字段名称
keyProb    字段名称置信度
value    识别出的字段名称对应的值
valueProb    字段名称对应值的置信度
valuePos    字段在原图中的四个点坐标（左上、右上、右下、左下）
```

- **receiptDetails 数组** 字段说明

```nginx
amount    小记
itemName    品名
quantity    数量
unitPrice   单价
```

## 示例

正常返回示例

`JSON`格式

```prolog
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "algo_version": "",
    "data": {
      "contactNumber": "",
      "receiptDate": "2020-04-23",
      "receiptDetails": [\
        {\
          "amount": 5.3,\
          "itemName": "雕牌超效加酶无砖",\
          "quantity": "",\
          "unitPrice": ""\
        }\
      ],
      "receiptTime": "20:26:00",
      "shopAddress": "",
      "shopName": "世纪联华椒江巾府大道店",
      "totalAmount": "5.00元"
    },
    "ftype": 0,
    "height": 1042,
    "orgHeight": 1055,
    "orgWidth": 690,
    "prism_keyValueInfo": [\
      {\
        "key": "shopName",\
        "keyProb": 99,\
        "value": "世纪联华椒江巾府大道店",\
        "valuePos": [\
          {\
            "x": 56,\
            "y": 208\
          },\
          {\
            "x": 452,\
            "y": 230\
          },\
          {\
            "x": 451,\
            "y": 258\
          },\
          {\
            "x": 54,\
            "y": 236\
          }\
        ],\
        "valueProb": 99\
      },\
      {\
        "key": "receiptDate",\
        "keyProb": 100,\
        "value": "2020-04-23",\
        "valuePos": [\
          {\
            "x": 300,\
            "y": 644\
          },\
          {\
            "x": 434,\
            "y": 647\
          },\
          {\
            "x": 434,\
            "y": 675\
          },\
          {\
            "x": 299,\
            "y": 671\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "receiptTime",\
        "keyProb": 100,\
        "value": "20:26:00",\
        "valuePos": [\
          {\
            "x": 442,\
            "y": 648\
          },\
          {\
            "x": 553,\
            "y": 651\
          },\
          {\
            "x": 552,\
            "y": 679\
          },\
          {\
            "x": 441,\
            "y": 676\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "contactNumber",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "shopAddress",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "totalAmount",\
        "keyProb": 100,\
        "value": "5.00元",\
        "valuePos": [\
          {\
            "x": 480,\
            "y": 437\
          },\
          {\
            "x": 574,\
            "y": 435\
          },\
          {\
            "x": 574,\
            "y": 466\
          },\
          {\
            "x": 480,\
            "y": 467\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "receiptDetails",\
        "keyProb": 100,\
        "value": [\
          {\
            "amount": 5.3,\
            "itemName": "雕牌超效加酶无砖",\
            "quantity": "",\
            "unitPrice": ""\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 11,
      "x1": 690,
      "x2": 689,
      "x3": 1,
      "y0": 13,
      "y1": 43,
      "y2": 1055,
      "y3": 1055
    },
    "width": 689
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

暂无变更历史

SDK 调用
通过 SDK 调用此接口的示例请参考 [开发者中心](https://next.api.aliyun.com/api-tools/sdk/ocr-api?version=2021-07-07&language=java-tea)

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[票据凭证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-bill-voucher-identification/)RecognizeShoppingReceipt - 购物小票识别

# RecognizeShoppingReceipt - 购物小票识别

更新时间：2025-12-08 21:09:21

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeRideHailingItinerary - 网约车行程单识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeridehailingitinerary)[下一篇：RecognizeTollInvoice - 过路过桥费发票识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizetollinvoice)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

授权信息

请求参数

支持的图片格式

返回参数

中英文字段映射

示例

错误码

变更历史