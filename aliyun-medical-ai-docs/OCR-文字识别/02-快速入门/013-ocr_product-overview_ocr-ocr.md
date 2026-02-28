### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[产品概述](https://help.aliyun.com/zh/ocr/product-overview/)[产品简介](https://help.aliyun.com/zh/ocr/product-overview/product-introduction/)[OCR统一识别](https://help.aliyun.com/zh/ocr/product-overview/ocr-unified-identification/)OCR统一识别

# OCR统一识别

更新时间：2024-07-10 06:26:28

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

产品介绍

产品功能

特色优势

应用场景

联系我们

## 产品介绍

[OCR统一识别](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-recognizealltext "") 是阿里云OCR团队重磅推出的新品，一个接口集成了59种不同场景识别能力，可满足多功能需求，提升客户接入的便捷性、易用性及高效性，降低客户同时接入多个OCR场景能力的门槛，欢迎大家使用。

## 产品功能

- 一个接口即可满足59种不同的单场景及混贴票证识别。

- 覆盖现有六大类场景：通用文字识别、个人证照识别、车辆物流识别、票据凭证识别、企业资质识别和混贴。

- 混贴票证支持类型包含：下表内（除车辆VIN码、车牌、电子面单、国际护照、国际身份证、公章、医疗器械经营许可证、医疗器械生产许可证、化妆品生产许可证、国际企业执照、商标注册证、食品经营许可证、食品生产许可证、第二类医疗器械经营备案凭证、银行开户许可证外）其他个人证照、车辆物流、票据凭证、企业资质类型图片的混贴识别。


具体支持的识别能力类型见下图：

|     |     |     |     |
| --- | --- | --- | --- |
| 场景 | 识别能力类型 |
| 通用文字识别<br>（共8类） | [通用文字识别高精版](https://help.aliyun.com/zh/ocr/product-overview/common-character-recognition-1#title-412-7m6-e38 "") | [通用文字识别基础版](https://help.aliyun.com/zh/ocr/product-overview/common-character-recognition-1#title-ruy-khj-m7o "") | [手写文字](https://help.aliyun.com/zh/ocr/product-overview/common-character-recognition-1#title-dfv-pz3-wz7 "") |
| [电商图片文字](https://help.aliyun.com/zh/ocr/product-overview/common-character-recognition-1#title-q6q-nmb-ecr "") | [多语言文字](https://help.aliyun.com/zh/ocr/product-overview/recognition-of-characters-in-languages-except-for-chinese-and-english-1#title-jj7-5la-wgn "") | [表格](https://help.aliyun.com/zh/ocr/product-overview/common-character-recognition-1#title-oco-dlx-al6 "") |
| 二维码 | 条形码 |  |
| 个人证照识别<br>（共13类） | [身份证](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-60c-iia-3ww "") | [银行卡](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-cr0-gim-7oy "") | [社保卡](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#0359b1e1e4sgg "") |
| [户口本首页](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-r3q-3c9-zz5 "") | [户口本常住人口页](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-r3q-3c9-zz5 "") | [出生证明](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-ejy-2p1-mll "") |
| [中国护照](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-b9e-g8d-m4o "") | [国际护照](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-i40-vm4-kv0 "") | [往来港澳台通行证](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-yi0-q6z-piw "") |
| [来往中国大陆（内地）通行证](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-ysz-wz8-row "") | [中国香港身份证](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-b5m-01z-qrp "") | [国际身份证](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#0a48c90137htr "") |
| [不动产权证](https://help.aliyun.com/zh/ocr/product-overview/personal-certificate-recognition-1#title-vb0-jxn-5u7 "") |  |  |
| 车辆物流识别<br>（共7类） | [行驶证](https://help.aliyun.com/zh/ocr/product-overview/vehicle-logistics-recognition-1#title-sc3-jkk-khg "") | [驾驶证](https://help.aliyun.com/zh/ocr/product-overview/vehicle-logistics-recognition-1#title-g5l-ias-eb5 "") | [车牌](https://help.aliyun.com/zh/ocr/product-overview/vehicle-logistics-recognition-1#title-td3-jow-b6h "") |
| [车辆vin码](https://help.aliyun.com/zh/ocr/product-overview/vehicle-logistics-recognition-1#title-g9p-i1j-y39 "") | [车辆合格证](https://help.aliyun.com/zh/ocr/product-overview/vehicle-logistics-recognition-1#title-e06-k5h-mep "") | [机动车注册登记证](https://help.aliyun.com/zh/ocr/product-overview/vehicle-logistics-recognition-1#title-xhk-wpb-yq0 "") |
| [电子面单](https://help.aliyun.com/zh/ocr/product-overview/vehicle-logistics-recognition-1#title-6yc-35y-zq8 "") |  |  |
| 票据凭证识别<br>（共19类） | [增值税发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-48m-64l-3ha "") | [机动车销售统一发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-wup-bjj-bql "") | [定额发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-oys-bhm-wwt "") |
| [增值税发票卷票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-via-bfw-ff3 "") | [通用机打发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-2ft-sn0-6y1 "") | [非税收入发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-ytq-3rq-v2t "") |
| [二手车销售统一发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#09e6af4388ygd "") | [出租车发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-pyk-lpp-2pz "") | [税收完税证明](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-49u-gba-2r9 "") |
| [银行承兑汇票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-c7x-z3r-8mj "") | [客运车船票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-q9r-4ox-ml1 "") | [火车票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-38u-u2c-qr4 "") |
| [航空行程单](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-ui8-3bh-dzp "") | [酒店流水](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-de0-13m-6ky "") | [购物小票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-jez-rwx-uky "") |
| [电商订单页](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-0ic-v6j-2ib "") | [网约车行程单](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#d2c7ee2130hgu "") | [支付详情页](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-q87-eze-fd1 "") |
| [过路过桥费发票](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-bf6-brt-rpo "") |  |  |
| 企业资质识别<br>（共11类） | [营业执照](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-tg7-zh7-v16 "") | [公章](https://duguang.aliyun.com/experience?type=other&subtype=seal_discern#intro) | [医疗器械经营许可证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-3q0-kvb-nyw "") |
| [医疗器械生产许可证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-znp-qvs-wj0 "") | [化妆品生产许可证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-w3b-kwj-k7s "") | [国际企业执照](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#f21599215bwlt "") |
| [商标注册证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-w7i-8dw-brk "") | [食品经营许可证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-oco-981-9pu "") | [食品生产许可证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-ne1-fq4-1s5 "") |
| [第二类医疗器械经营备案凭证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-vt3-f2g-w30 "") | [银行开户许可证](https://help.aliyun.com/zh/ocr/product-overview/enterprise-qualification-certificate-recognition-1#title-59m-a70-wdu "") |  |
| 混贴识别<br>（共1类） | [混贴票证](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-recognition-1#title-4g1-3pv-pac "") |  |  |

注：

- “通用文字识别高精版”能力与现有“全文识别高精版”一致，相比原接口开放了更多配置项。

- “通用文字识别基础版”能力与现有“通用文字识别”一致，相比原接口开放了更多配置项。


## 特色优势

- #### **兼容多数据类型**


多能力复用一个接口，可以识别多场景数据类型，无需对接多个接口，一次搞定接入成本。

- #### **计费划档清晰**


OCR统一识别支持按量付费和共享资源包两种计费方式，多种能力共用资源包消耗，采购更方便。

- #### **实时性高**


依托于阿里自建的EAS在线服务集群，精益求精优化Inference技术，提供弹性伸缩的低延时服务。

- #### **服务稳定**


根据调用量提供弹性服务，扩展性好，算法持续迭代优化对客户稳定性不会造成影响。


## 应用场景

- #### **图片内容审核**


各类通用型接口，可针对不同场景，识别内容进行内容审核。及时发现违规行为，大大降低人力成本，广泛应用于电商内容治理场景。

- #### **物流/运输/汽车**


应用于二手车交易、智慧停车、物流运输、快递驿站、汽车保险等场景，提供个人身份、车辆信息、快递信息记录并认证服务。支持行驶证、驾驶证、车牌、VIN码、电子面单、身份证、车辆合格证等卡证信息文字识别。

- #### **金融/银行/保险**


为远程开户、身份核验/实名认证/信息录入、合同/保单数字化、银行流水/财报信息录入等场景，提供人工智能识别服务，大大降低人力成本。支持身份证、护照、往来通行证、银行卡、印章、表格等识别文字服务。

- #### **政务/医疗**


应用于财税报销、纸质电子化（文档/卷/合同）、医疗票据/药房、简历/论文扫描编辑等场景，提供图片、扫描件等非文本格式转换为可编辑文本服务。支持增值税发票、发票核验、各类票据凭证、全文识别高精版、手写体、表格等识别文字服务。

- #### **零售/互联网/电商**


为内容治理（海报/宣传页/商品详情页）、资质审核（商家入驻）、商机/品牌挖掘等场景，提供图片识别文字服务，支持电商图片、营业执照、房产证、银行开户许可证、表格、高精、通用等识别能力。


## 联系我们

如果您有任何需求、反馈或者期望与工程师即时沟通，欢迎联系我们。

您可以通过如下方式联系我们：

- 加入官方钉钉群：35208328

- [OCR在线咨询](https://chatbot.aliyuncs.com/intl/index.htm?locale=zh-CN&from=gYHE9tnzce)

- OCR商务联系邮箱：ocr\_support@list.alibaba-inc.com，并留下您的联系方式。