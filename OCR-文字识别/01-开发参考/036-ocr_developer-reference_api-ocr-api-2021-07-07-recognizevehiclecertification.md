支持车辆型号、车辆识别代号、底盘型号、发动机型号等字段进行结构化提取。

## 接口说明

#### 本接口适用场景

- 阿里云车辆合格证识别，是阿里云官方自研 OCR 文字识别产品，适用于识别车辆合格证所包含的车辆型号、车辆识别代号、地盘型号、发动机型号等关键信息的场景。
- 阿里云 OCR 产品基于阿里巴巴达摩院强大的 AI 技术及海量数据，历经多年沉淀打磨，具有服务稳定、操作简易、实时性高、能力全面等几大优势。
- 本接口图片示例

![](https://img.alicdn.com/imgextra/i1/O1CN01myFZQ91pMyaGJpRZn_!!6000000005347-2-tps-562-316.png)

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
| 1 | 开通 [车辆物流识别](https://common-buy.aliyun.com/?commodityCode=ocr_logistics_public_cn) 服务。开通服务前后，您可以通过 [体验馆](https://duguang.aliyun.com/experience?type=logistics&subtype=vehicle_certificate#intro) 免费体验本功能识别效果。 |
| 2 | 购买 [车辆合格证识别资源包](https://common-buy.aliyun.com/?commodityCode=ocr_logistics_dp_cn&request=%7B%22ord_time%22:%221:Year%22,%22order_num%22:1,%22pack%22:%22ocr_logistics_dp_cn_20211222171406_0433%22,%22flowout_spec%22:%22500%22%7D)。本 API 会赠送免费额度，可使用免费额度测试。您也可以不购买资源包，系统会通过“ [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go)”方式按实际调用量自动扣款。 |
| 3 | 可以参照 [调试页面](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeVehicleCertification?sdkStyle=dara) 提供的代码示例完成 API 接入开发。接入完成后，调用 API 获取识别结果。如果使用子账号调用接口，需要阿里云账号（主账号）对 RAM 账号进行授权。创建 RAM 用户的具体操作，请参考： [创建 RAM 用户。](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user) 文字识别服务提供一种系统授权策略，即 **AliyunOCRFullAccess**。具体授权操作，请参见 [在用户页面为 RAM 用户授权。](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user) |

#### 重要提示

| 类型 | 概述 |
| --- | --- |

| 类型 | 概述 |
| --- | --- |
| 图片格式 | - 本接口支持：PNG、JPG、JPEG、BMP、GIF、TIFF、WebP。暂不支持 PDF 格式。 |
| 图片尺寸 | - 图片长宽需要大于 15 像素，小于 8192 像素。<br>- 长宽比需要小于 50。<br>- 如需达到较好识别效果，建议长宽均大于 500px。<br>- 图片尺寸过小，会影响识别精度。图片内单字大小在 10-50px 内时，识别效果较好。 |
| 图片大小 | - 图片二进制文件不能超过 10MB。<br>- 图片过大会影响接口响应速度，建议使用小于 1.5M 图片进行识别，且通过传图片 URL 的方式调用接口。 |
| 其他提示 | - 接口会自动处理反光、扭曲等干扰信息，但会影响精度。请尽量选择清晰度高、无反光、无扭曲的图片。 |
| 相关能力 | - [云市场车辆合格证识别。](https://market.aliyun.com/products/57124001/cmapi00049687.html?#sku=yuncode4368700002) |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI\\
Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeVehicleCertification)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)调试](https://api.aliyun.com/api/ocr-api/2021-07-07/RecognizeVehicleCertification)

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
| ocr:RecognizeVehicleCertification | get | \*全部资源<br>`*` | 无 | 无 |

## 请求参数

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| Url | string | 否 | - 本字段和 body 字段二选一，不可同时透传或同时为空。<br>- 图片链接（长度不超 2048 字节，不支持 base64）。 | https://img.alicdn.com/imgextra/i1/O1CN0196uE7i1FXD9TpYqLy\_!!6000000000496-0-tps-3024-4032.jpg |
| body | byte | 否 | - 本字段和 URL 字段二选一，不可同时透传或同时为空。<br>- 图片二进制文件，最大 10MB。<br>- 使用 HTTP 方式调用，把图片二进制文件放到 HTTP body 中上传即可。<br>- 使用 SDK 的方式调用，把图片放到 SDK 的 body 中即可。 | 图片二进制 |

## 返回参数

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |

| 名称 | 类型 | 描述 | 示例值 |
| --- | --- | --- | --- |
|  | object | Schema of Response |  |
| RequestId | string | 请求唯一 ID | 43A29C77-405E-4CC0-BC55-EE694AD00655 |
| Data | string | 返回数据 | {"data":{"certificateNumber":"YG170ZLM1234567","issueDate":"2021年01月01日","manufactureName":"中国重汽集团济南卡车股份有限公司","vehicleBrand":"豪沃牌","vehicleName":"自卸汽车","vehicleModel":"ZZ3257N414GE1","vinCode":"LZZ1ELSEXLW644557","vehicleColor":"水晶红","chassisModel":"ZZ3257N384GE1","chassisId":"2578516","chassisCertificateNumber":"","engineModel":"WP10H400E50","engineNumber":"7520K064819","fuelType":"柴油","displacement":"9500","power":"294","emissionStandard":"GB17691-2005国V","fuelConsumption":"","overallDimension":"8920×2550×3450","containerDimension":"6000×2350×1500","springNumber":"11/12","tireNumber":"10","tireSize":"12.00R2016PR","frontWheelTrack":"2022","rearWheelTrack":"1850/1850","wheelbase":"4125+1350","axleLoad":"7000/18000(二轴组)","axleNumber":"3","steeringForm":"方向盘","totalWeight":"25000","equipmentWeight":"12500","maximumLadenMass":"12370","massUtilizationCoefficient":"1.00","tractionWeight":"","MaximumLoadMass":"","cabPassengerCapacity":"2","passengerCapacity":"","maxDesignSpeed":"80","manufactureDate":"2020年12月03日","remarks":"备注:货厢自卸方式为后卸。"},"ftype":1,"height":4032,"orgHeight":4032,"orgWidth":3024,"prism\_keyValueInfo":\[{"key":"certificateNumber","keyProb":100,"value":"YG170ZLM1234567","valuePos":\[{"x":554,"y":85},{"x":932,"y":84},{"x":932,"y":133},{"x":554,"y":135}\],"valueProb":100},{"key":"issueDate","keyProb":100,"value":"2021年01月01日","valuePos":\[{"x":1637,"y":132},{"x":1639,"y":82},{"x":2002,"y":91},{"x":2001,"y":142}\],"valueProb":100},{"key":"manufactureName","keyProb":100,"value":"中国重汽集团济南卡车股份有限公司","valuePos":\[{"x":552,"y":212},{"x":554,"y":164},{"x":1265,"y":180},{"x":1264,"y":229}\],"valueProb":100},{"key":"vehicleBrand","keyProb":100,"value":"豪沃牌","valuePos":\[{"x":554,"y":292},{"x":556,"y":240},{"x":693,"y":243},{"x":692,"y":296}\],"valueProb":100},{"key":"vehicleName","keyProb":100,"value":"自卸汽车","valuePos":\[{"x":1338,"y":257},{"x":1338,"y":307},{"x":1161,"y":307},{"x":1161,"y":257}\],"valueProb":100},{"key":"vehicleModel","keyProb":100,"value":"ZZ3257N414GE1","valuePos":\[{"x":550,"y":366},{"x":551,"y":319},{"x":846,"y":325},{"x":845,"y":372}\],"valueProb":100},{"key":"vinCode","keyProb":100,"value":"LZZ1ELSEXLW644557","valuePos":\[{"x":1636,"y":373},{"x":1638,"y":328},{"x":2016,"y":352},{"x":2013,"y":397}\],"valueProb":100},{"key":"vehicleColor","keyProb":100,"value":"水晶红","valuePos":\[{"x":554,"y":447},{"x":554,"y":395},{"x":690,"y":398},{"x":689,"y":449}\],"valueProb":100},{"key":"chassisModel","keyProb":100,"value":"ZZ3257N384GE1","valuePos":\[{"x":550,"y":521},{"x":550,"y":474},{"x":848,"y":480},{"x":847,"y":526}\],"valueProb":100},{"key":"chassisId","keyProb":100,"value":"2578516","valuePos":\[{"x":1635,"y":529},{"x":1637,"y":485},{"x":1801,"y":489},{"x":1800,"y":534}\],"valueProb":100},{"key":"chassisCertificateNumber","keyProb":100,"value":"","valueProb":100},{"key":"engineModel","keyProb":100,"value":"WP10H400E50","valuePos":\[{"x":1634,"y":607},{"x":1635,"y":562},{"x":1886,"y":570},{"x":1884,"y":614}\],"valueProb":100},{"key":"engineNumber","keyProb":100,"value":"7520K064819","valuePos":\[{"x":548,"y":672},{"x":549,"y":631},{"x":804,"y":635},{"x":804,"y":676}\],"valueProb":100},{"key":"fuelType","keyProb":100,"value":"柴油","valuePos":\[{"x":641,"y":705},{"x":641,"y":755},{"x":550,"y":755},{"x":550,"y":705}\],"valueProb":100},{"key":"displacement","keyProb":100,"value":"9500","valuePos":\[{"x":1631,"y":760},{"x":1631,"y":719},{"x":1728,"y":722},{"x":1727,"y":762}\],"valueProb":100},{"key":"power","keyProb":100,"value":"294","valuePos":\[{"x":2002,"y":729},{"x":2002,"y":769},{"x":1930,"y":769},{"x":1930,"y":729}\],"valueProb":100},{"key":"emissionStandard","keyProb":100,"value":"GB17691-2005国V","valuePos":\[{"x":545,"y":828},{"x":545,"y":782},{"x":904,"y":789},{"x":903,"y":835}\],"valueProb":100},{"key":"fuelConsumption","keyProb":100,"value":"","valueProb":100},{"key":"overallDimension","keyProb":100,"value":"8920×2550×3450","valuePos":\[{"x":547,"y":979},{"x":548,"y":939},{"x":1042,"y":950},{"x":1041,"y":989}\],"valueProb":100},{"key":"containerDimension","keyProb":100,"value":"6000×2350×1500","valuePos":\[{"x":1628,"y":992},{"x":1629,"y":949},{"x":2119,"y":962},{"x":2117,"y":1005}\],"valueProb":100},{"key":"springNumber","keyProb":100,"value":"11/12","valuePos":\[{"x":662,"y":1017},{"x":663,"y":1059},{"x":549,"y":1060},{"x":548,"y":1018}\],"valueProb":100},{"key":"tireNumber","keyProb":100,"value":"10","valuePos":\[{"x":1676,"y":1032},{"x":1676,"y":1073},{"x":1628,"y":1073},{"x":1628,"y":1032}\],"valueProb":100},{"key":"tireSize","keyProb":100,"value":"12.00R2016PR","valuePos":\[{"x":545,"y":1133},{"x":546,"y":1094},{"x":839,"y":1099},{"x":839,"y":1139}\],"valueProb":100},{"key":"frontWheelTrack","keyProb":100,"value":"2022","valuePos":\[{"x":640,"y":1169},{"x":640,"y":1208},{"x":545,"y":1210},{"x":544,"y":1170}\],"valueProb":100},{"key":"rearWheelTrack","keyProb":100,"value":"1850/1850","valuePos":\[{"x":1148,"y":1223},{"x":1149,"y":1183},{"x":1349,"y":1186},{"x":1349,"y":1227}\],"valueProb":100},{"key":"wheelbase","keyProb":100,"value":"4125+1350","valuePos":\[{"x":546,"y":1286},{"x":547,"y":1244},{"x":752,"y":1248},{"x":751,"y":1290}\],"valueProb":100},{"key":"axleLoad","keyProb":100,"value":"7000/18000(二轴组)","valuePos":\[{"x":539,"y":1364},{"x":539,"y":1316},{"x":946,"y":1325},{"x":945,"y":1372}\],"valueProb":100},{"key":"axleNumber","keyProb":100,"value":"3","valuePos":\[{"x":567,"y":1398},{"x":567,"y":1438},{"x":541,"y":1438},{"x":541,"y":1398}\],"valueProb":100},{"key":"steeringForm","keyProb":100,"value":"方向盘","valuePos":\[{"x":1757,"y":1412},{"x":1757,"y":1463},{"x":1622,"y":1464},{"x":1622,"y":1413}\],"valueProb":100},{"key":"totalWeight","keyProb":100,"value":"25000","valuePos":\[{"x":536,"y":1512},{"x":538,"y":1471},{"x":658,"y":1475},{"x":657,"y":1515}\],"valueProb":100},{"key":"equipmentWeight","keyProb":100,"value":"12500","valuePos":\[{"x":1735,"y":1491},{"x":1736,"y":1532},{"x":1620,"y":1534},{"x":1620,"y":1492}\],"valueProb":100},{"key":"maximumLadenMass","keyProb":100,"value":"12370","valuePos":\[{"x":539,"y":1590},{"x":539,"y":1547},{"x":656,"y":1549},{"x":656,"y":1592}\],"valueProb":100},{"key":"massUtilizationCoefficient","keyProb":100,"value":"1.00","valuePos":\[{"x":1712,"y":1568},{"x":1712,"y":1608},{"x":1617,"y":1610},{"x":1616,"y":1569}\],"valueProb":100},{"key":"tractionWeight","keyProb":100,"value":"","valueProb":100},{"key":"MaximumLoadMass","keyProb":100,"value":"","valueProb":100},{"key":"cabPassengerCapacity","keyProb":100,"value":"2","valuePos":\[{"x":560,"y":1777},{"x":560,"y":1817},{"x":532,"y":1817},{"x":532,"y":1777}\],"valueProb":100},{"key":"passengerCapacity","keyProb":100,"value":"","valueProb":100},{"key":"maxDesignSpeed","keyProb":100,"value":"80","valuePos":\[{"x":581,"y":1931},{"x":581,"y":1971},{"x":530,"y":1971},{"x":530,"y":1931}\],"valueProb":100},{"key":"manufactureDate","keyProb":100,"value":"2020年12月03日","valuePos":\[{"x":840,"y":2003},{"x":841,"y":2048},{"x":523,"y":2052},{"x":522,"y":2006}\],"valueProb":100},{"key":"remarks","keyProb":100,"value":"备注:货厢自卸方式为后卸。","valuePos":\[{"x":620,"y":2080},{"x":620,"y":2130},{"x":54,"y":2134},{"x":53,"y":2083}\],"valueProb":100}\],"sliceRect":{"x0":330,"y0":466,"x1":2530,"y1":420,"x2":2544,"y2":3811,"x3":229,"y3":3746},"width":3024} |
| Code | string | 错误码（如果识别成功，不会返回此字段） | noPermission |
| Message | string | 错误提示（如果识别成功，不会返回此字段） | You are not authorized to perform this operation. |

#### 返回参数说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| data | object | 结构化信息。 |
| angle | int | 图片的角度，0 表示正向，90 表示图片朝右，180 朝下，270 朝左。 |
| prism\_keyValueInfo | list | 结构化信息的坐标信息。 |
| ftype | int | 是否为复印件（1：是，0：否）。 |
| height | int | 算法矫正图片后的高度。 |
| width | int | 算法矫正图片后的宽度。 |
| orgHeight | int | 原图的高度。 |
| orgWidth | int | 原图的宽度。 |
| sliceRect | list | 检测出的子图坐标信息。 |

#### 结构化信息（data 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| MaximumLoadMass | string | 半挂车鞍座最大允许总质量。 |
| axleLoad | string | 轴荷。 |
| axleNumber | string | 轴数。 |
| cabPassengerCapacity | string | 驾驶室准驾人数。 |
| certificateNumber | string | 合格证编号。 |
| chassisCertificateNumber | string | 底盘合格证编号。 |
| chassisId | string | 底盘 ID。 |
| chassisModel | string | 底盘型号。 |
| containerDimension | string | 货箱内部尺寸。 |
| displacement | string | 排量。 |
| emissionStandard | string | 排放标准。 |
| engineModel | string | 发动机型号。 |
| engineNumber | string | 发动机号。 |
| equipmentWeight | string | 装备质量。 |
| frontWheelTrack | string | 轮距前。 |
| fuelConsumption | string | 油耗。 |
| fuelType | string | 燃料种类。枚举值为：天然气、汽油、混合动力、柴油、纯电动 |
| issueDate | string | 发证日期。 |
| manufactureDate | string | 车辆制造日期。 |
| manufactureName | string | 车辆制造企业名称。 |
| massUtilizationCoefficient | string | 载质量利用系数。 |
| maxDesignSpeed | string | 最高设计车速。 |
| maximumLadenMass | string | 额定载质量。 |
| overallDimension | string | 外廓尺寸。 |
| passengerCapacity | string | 额定载客。 |
| power | string | 功率。 |
| rearWheelTrack | string | 轮距后。 |
| remarks | string | 备注。 |
| springNumber | string | 钢板弹簧数。 |
| steeringForm | string | 转向形式。 |
| tireNumber | string | 轮胎数。 |
| tireSize | string | 轮胎规格。 |
| totalWeight | string | 总质量。 |
| tractionWeight | string | 准牵引总质量。 |
| vehicleBrand | string | 车辆品牌。 |
| vehicleColor | string | 车身颜色。 |
| vehicleModel | string | 车辆型号。 |
| vehicleName | string | 车辆名称。 |
| vinCode | string | 车辆识别代号/车架号。 |
| wheelbase | string | 轴距。 |

#### 结构化坐标信息（prism\_keyValueInfo 字段）

| 字段 | 类型 | 说明 |
| --- | --- | --- |

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| key | string | 识别出的字段名称。 |
| keyProb | int | 字段名称置信度。 |
| value | string | 识别出的字段名称对应的值。 |
| valueProb | int | 字段名称对应值的置信度。 |
| valuePos | list | 字段在原图中的四个点坐标（左上、右上、右下、左下）。 |

## 示例

正常返回示例

`JSON`格式

```yaml
{
  "RequestId": "43A29C77-405E-4CC0-BC55-EE694AD00655",
  "Data": {
    "data": {
      "certificateNumber": "YG170ZLM1234567",
      "issueDate": "2021年01月01日",
      "manufactureName": "中国重汽集团济南卡车股份有限公司",
      "vehicleBrand": "豪沃牌",
      "vehicleName": "自卸汽车",
      "vehicleModel": "ZZ3257N414GE1",
      "vinCode": "LZZ1ELSEXLW644557",
      "vehicleColor": "水晶红",
      "chassisModel": "ZZ3257N384GE1",
      "chassisId": 2578516,
      "chassisCertificateNumber": "",
      "engineModel": "WP10H400E50",
      "engineNumber": "7520K064819",
      "fuelType": "柴油",
      "displacement": 9500,
      "power": 294,
      "emissionStandard": "GB17691-2005国V",
      "fuelConsumption": "",
      "overallDimension": "8920×2550×3450",
      "containerDimension": "6000×2350×1500",
      "springNumber": "11/12",
      "tireNumber": 10,
      "tireSize": "12.00R2016PR",
      "frontWheelTrack": 2022,
      "rearWheelTrack": "1850/1850",
      "wheelbase": "4125+1350",
      "axleLoad": "7000/18000(二轴组)",
      "axleNumber": 3,
      "steeringForm": "方向盘",
      "totalWeight": 25000,
      "equipmentWeight": 12500,
      "maximumLadenMass": 12370,
      "massUtilizationCoefficient": 1,
      "tractionWeight": "",
      "MaximumLoadMass": "",
      "cabPassengerCapacity": 2,
      "passengerCapacity": "",
      "maxDesignSpeed": 80,
      "manufactureDate": "2020年12月03日",
      "remarks": "备注:货厢自卸方式为后卸。"
    },
    "ftype": 1,
    "height": 4032,
    "orgHeight": 4032,
    "orgWidth": 3024,
    "prism_keyValueInfo": [\
      {\
        "key": "certificateNumber",\
        "keyProb": 100,\
        "value": "YG170ZLM1234567",\
        "valuePos": [\
          {\
            "x": 554,\
            "y": 85\
          },\
          {\
            "x": 932,\
            "y": 84\
          },\
          {\
            "x": 932,\
            "y": 133\
          },\
          {\
            "x": 554,\
            "y": 135\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "issueDate",\
        "keyProb": 100,\
        "value": "2021年01月01日",\
        "valuePos": [\
          {\
            "x": 1637,\
            "y": 132\
          },\
          {\
            "x": 1639,\
            "y": 82\
          },\
          {\
            "x": 2002,\
            "y": 91\
          },\
          {\
            "x": 2001,\
            "y": 142\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "manufactureName",\
        "keyProb": 100,\
        "value": "中国重汽集团济南卡车股份有限公司",\
        "valuePos": [\
          {\
            "x": 552,\
            "y": 212\
          },\
          {\
            "x": 554,\
            "y": 164\
          },\
          {\
            "x": 1265,\
            "y": 180\
          },\
          {\
            "x": 1264,\
            "y": 229\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "vehicleBrand",\
        "keyProb": 100,\
        "value": "豪沃牌",\
        "valuePos": [\
          {\
            "x": 554,\
            "y": 292\
          },\
          {\
            "x": 556,\
            "y": 240\
          },\
          {\
            "x": 693,\
            "y": 243\
          },\
          {\
            "x": 692,\
            "y": 296\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "vehicleName",\
        "keyProb": 100,\
        "value": "自卸汽车",\
        "valuePos": [\
          {\
            "x": 1338,\
            "y": 257\
          },\
          {\
            "x": 1338,\
            "y": 307\
          },\
          {\
            "x": 1161,\
            "y": 307\
          },\
          {\
            "x": 1161,\
            "y": 257\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "vehicleModel",\
        "keyProb": 100,\
        "value": "ZZ3257N414GE1",\
        "valuePos": [\
          {\
            "x": 550,\
            "y": 366\
          },\
          {\
            "x": 551,\
            "y": 319\
          },\
          {\
            "x": 846,\
            "y": 325\
          },\
          {\
            "x": 845,\
            "y": 372\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "vinCode",\
        "keyProb": 100,\
        "value": "LZZ1ELSEXLW644557",\
        "valuePos": [\
          {\
            "x": 1636,\
            "y": 373\
          },\
          {\
            "x": 1638,\
            "y": 328\
          },\
          {\
            "x": 2016,\
            "y": 352\
          },\
          {\
            "x": 2013,\
            "y": 397\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "vehicleColor",\
        "keyProb": 100,\
        "value": "水晶红",\
        "valuePos": [\
          {\
            "x": 554,\
            "y": 447\
          },\
          {\
            "x": 554,\
            "y": 395\
          },\
          {\
            "x": 690,\
            "y": 398\
          },\
          {\
            "x": 689,\
            "y": 449\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "chassisModel",\
        "keyProb": 100,\
        "value": "ZZ3257N384GE1",\
        "valuePos": [\
          {\
            "x": 550,\
            "y": 521\
          },\
          {\
            "x": 550,\
            "y": 474\
          },\
          {\
            "x": 848,\
            "y": 480\
          },\
          {\
            "x": 847,\
            "y": 526\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "chassisId",\
        "keyProb": 100,\
        "value": 2578516,\
        "valuePos": [\
          {\
            "x": 1635,\
            "y": 529\
          },\
          {\
            "x": 1637,\
            "y": 485\
          },\
          {\
            "x": 1801,\
            "y": 489\
          },\
          {\
            "x": 1800,\
            "y": 534\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "chassisCertificateNumber",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "engineModel",\
        "keyProb": 100,\
        "value": "WP10H400E50",\
        "valuePos": [\
          {\
            "x": 1634,\
            "y": 607\
          },\
          {\
            "x": 1635,\
            "y": 562\
          },\
          {\
            "x": 1886,\
            "y": 570\
          },\
          {\
            "x": 1884,\
            "y": 614\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "engineNumber",\
        "keyProb": 100,\
        "value": "7520K064819",\
        "valuePos": [\
          {\
            "x": 548,\
            "y": 672\
          },\
          {\
            "x": 549,\
            "y": 631\
          },\
          {\
            "x": 804,\
            "y": 635\
          },\
          {\
            "x": 804,\
            "y": 676\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "fuelType",\
        "keyProb": 100,\
        "value": "柴油",\
        "valuePos": [\
          {\
            "x": 641,\
            "y": 705\
          },\
          {\
            "x": 641,\
            "y": 755\
          },\
          {\
            "x": 550,\
            "y": 755\
          },\
          {\
            "x": 550,\
            "y": 705\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "displacement",\
        "keyProb": 100,\
        "value": 9500,\
        "valuePos": [\
          {\
            "x": 1631,\
            "y": 760\
          },\
          {\
            "x": 1631,\
            "y": 719\
          },\
          {\
            "x": 1728,\
            "y": 722\
          },\
          {\
            "x": 1727,\
            "y": 762\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "power",\
        "keyProb": 100,\
        "value": 294,\
        "valuePos": [\
          {\
            "x": 2002,\
            "y": 729\
          },\
          {\
            "x": 2002,\
            "y": 769\
          },\
          {\
            "x": 1930,\
            "y": 769\
          },\
          {\
            "x": 1930,\
            "y": 729\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "emissionStandard",\
        "keyProb": 100,\
        "value": "GB17691-2005国V",\
        "valuePos": [\
          {\
            "x": 545,\
            "y": 828\
          },\
          {\
            "x": 545,\
            "y": 782\
          },\
          {\
            "x": 904,\
            "y": 789\
          },\
          {\
            "x": 903,\
            "y": 835\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "fuelConsumption",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "overallDimension",\
        "keyProb": 100,\
        "value": "8920×2550×3450",\
        "valuePos": [\
          {\
            "x": 547,\
            "y": 979\
          },\
          {\
            "x": 548,\
            "y": 939\
          },\
          {\
            "x": 1042,\
            "y": 950\
          },\
          {\
            "x": 1041,\
            "y": 989\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "containerDimension",\
        "keyProb": 100,\
        "value": "6000×2350×1500",\
        "valuePos": [\
          {\
            "x": 1628,\
            "y": 992\
          },\
          {\
            "x": 1629,\
            "y": 949\
          },\
          {\
            "x": 2119,\
            "y": 962\
          },\
          {\
            "x": 2117,\
            "y": 1005\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "springNumber",\
        "keyProb": 100,\
        "value": "11/12",\
        "valuePos": [\
          {\
            "x": 662,\
            "y": 1017\
          },\
          {\
            "x": 663,\
            "y": 1059\
          },\
          {\
            "x": 549,\
            "y": 1060\
          },\
          {\
            "x": 548,\
            "y": 1018\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "tireNumber",\
        "keyProb": 100,\
        "value": 10,\
        "valuePos": [\
          {\
            "x": 1676,\
            "y": 1032\
          },\
          {\
            "x": 1676,\
            "y": 1073\
          },\
          {\
            "x": 1628,\
            "y": 1073\
          },\
          {\
            "x": 1628,\
            "y": 1032\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "tireSize",\
        "keyProb": 100,\
        "value": "12.00R2016PR",\
        "valuePos": [\
          {\
            "x": 545,\
            "y": 1133\
          },\
          {\
            "x": 546,\
            "y": 1094\
          },\
          {\
            "x": 839,\
            "y": 1099\
          },\
          {\
            "x": 839,\
            "y": 1139\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "frontWheelTrack",\
        "keyProb": 100,\
        "value": 2022,\
        "valuePos": [\
          {\
            "x": 640,\
            "y": 1169\
          },\
          {\
            "x": 640,\
            "y": 1208\
          },\
          {\
            "x": 545,\
            "y": 1210\
          },\
          {\
            "x": 544,\
            "y": 1170\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "rearWheelTrack",\
        "keyProb": 100,\
        "value": "1850/1850",\
        "valuePos": [\
          {\
            "x": 1148,\
            "y": 1223\
          },\
          {\
            "x": 1149,\
            "y": 1183\
          },\
          {\
            "x": 1349,\
            "y": 1186\
          },\
          {\
            "x": 1349,\
            "y": 1227\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "wheelbase",\
        "keyProb": 100,\
        "value": "4125+1350",\
        "valuePos": [\
          {\
            "x": 546,\
            "y": 1286\
          },\
          {\
            "x": 547,\
            "y": 1244\
          },\
          {\
            "x": 752,\
            "y": 1248\
          },\
          {\
            "x": 751,\
            "y": 1290\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "axleLoad",\
        "keyProb": 100,\
        "value": "7000/18000(二轴组)",\
        "valuePos": [\
          {\
            "x": 539,\
            "y": 1364\
          },\
          {\
            "x": 539,\
            "y": 1316\
          },\
          {\
            "x": 946,\
            "y": 1325\
          },\
          {\
            "x": 945,\
            "y": 1372\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "axleNumber",\
        "keyProb": 100,\
        "value": 3,\
        "valuePos": [\
          {\
            "x": 567,\
            "y": 1398\
          },\
          {\
            "x": 567,\
            "y": 1438\
          },\
          {\
            "x": 541,\
            "y": 1438\
          },\
          {\
            "x": 541,\
            "y": 1398\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "steeringForm",\
        "keyProb": 100,\
        "value": "方向盘",\
        "valuePos": [\
          {\
            "x": 1757,\
            "y": 1412\
          },\
          {\
            "x": 1757,\
            "y": 1463\
          },\
          {\
            "x": 1622,\
            "y": 1464\
          },\
          {\
            "x": 1622,\
            "y": 1413\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "totalWeight",\
        "keyProb": 100,\
        "value": 25000,\
        "valuePos": [\
          {\
            "x": 536,\
            "y": 1512\
          },\
          {\
            "x": 538,\
            "y": 1471\
          },\
          {\
            "x": 658,\
            "y": 1475\
          },\
          {\
            "x": 657,\
            "y": 1515\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "equipmentWeight",\
        "keyProb": 100,\
        "value": 12500,\
        "valuePos": [\
          {\
            "x": 1735,\
            "y": 1491\
          },\
          {\
            "x": 1736,\
            "y": 1532\
          },\
          {\
            "x": 1620,\
            "y": 1534\
          },\
          {\
            "x": 1620,\
            "y": 1492\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "maximumLadenMass",\
        "keyProb": 100,\
        "value": 12370,\
        "valuePos": [\
          {\
            "x": 539,\
            "y": 1590\
          },\
          {\
            "x": 539,\
            "y": 1547\
          },\
          {\
            "x": 656,\
            "y": 1549\
          },\
          {\
            "x": 656,\
            "y": 1592\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "massUtilizationCoefficient",\
        "keyProb": 100,\
        "value": 1,\
        "valuePos": [\
          {\
            "x": 1712,\
            "y": 1568\
          },\
          {\
            "x": 1712,\
            "y": 1608\
          },\
          {\
            "x": 1617,\
            "y": 1610\
          },\
          {\
            "x": 1616,\
            "y": 1569\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "tractionWeight",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "MaximumLoadMass",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "cabPassengerCapacity",\
        "keyProb": 100,\
        "value": 2,\
        "valuePos": [\
          {\
            "x": 560,\
            "y": 1777\
          },\
          {\
            "x": 560,\
            "y": 1817\
          },\
          {\
            "x": 532,\
            "y": 1817\
          },\
          {\
            "x": 532,\
            "y": 1777\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "passengerCapacity",\
        "keyProb": 100,\
        "value": "",\
        "valueProb": 100\
      },\
      {\
        "key": "maxDesignSpeed",\
        "keyProb": 100,\
        "value": 80,\
        "valuePos": [\
          {\
            "x": 581,\
            "y": 1931\
          },\
          {\
            "x": 581,\
            "y": 1971\
          },\
          {\
            "x": 530,\
            "y": 1971\
          },\
          {\
            "x": 530,\
            "y": 1931\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "manufactureDate",\
        "keyProb": 100,\
        "value": "2020年12月03日",\
        "valuePos": [\
          {\
            "x": 840,\
            "y": 2003\
          },\
          {\
            "x": 841,\
            "y": 2048\
          },\
          {\
            "x": 523,\
            "y": 2052\
          },\
          {\
            "x": 522,\
            "y": 2006\
          }\
        ],\
        "valueProb": 100\
      },\
      {\
        "key": "remarks",\
        "keyProb": 100,\
        "value": "备注:货厢自卸方式为后卸。",\
        "valuePos": [\
          {\
            "x": 620,\
            "y": 2080\
          },\
          {\
            "x": 620,\
            "y": 2130\
          },\
          {\
            "x": 54,\
            "y": 2134\
          },\
          {\
            "x": 53,\
            "y": 2083\
          }\
        ],\
        "valueProb": 100\
      }\
    ],
    "sliceRect": {
      "x0": 330,
      "y0": 466,
      "x1": 2530,
      "y1": 420,
      "x2": 2544,
      "y2": 3811,
      "x3": 229,
      "y3": 3746
    },
    "width": 3024
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

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)[API目录](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir/)[车辆物流识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-dir-vehicle-logistics-identification/)RecognizeVehicleCertification - 车辆合格证识别

# RecognizeVehicleCertification - 车辆合格证识别

更新时间：2025-12-08 21:11:39

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RecognizeVehicleRegistration - 机动车注册登记证识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizevehicleregistration)[下一篇：RecognizeEduFormula - 印刷体数学公式识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizeeduformula)

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