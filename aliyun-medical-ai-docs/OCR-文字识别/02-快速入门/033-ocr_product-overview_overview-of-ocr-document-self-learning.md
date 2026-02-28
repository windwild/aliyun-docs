### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[产品概述](https://help.aliyun.com/zh/ocr/product-overview/)[产品简介](https://help.aliyun.com/zh/ocr/product-overview/product-introduction/)[OCR文档自学习](https://help.aliyun.com/zh/ocr/product-overview/document-self-learning/)OCR文档自学习概述

# OCR文档自学习概述

更新时间：2023-06-29 07:23:15

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：票证核验](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-verification-1)[下一篇：自定义KV模板](https://help.aliyun.com/zh/ocr/product-overview/custom-kv-template-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能简介

功能详情

模板：

模型：

工具箱：

价值主张

产品优势

应用场景

联系我们

## **功能简介**

OCR文档自学习，是面向“无算法基础”的企业与个人开发者用户，通过全流程可视化操作，支持用户完成模板配置、数据处理&标注、模型构建&训练、部署发布等操作的一站式工具平台。本平台采用少样本训练、智能预标注，视觉-语义联合学习等前沿AI技术，支持客户低成本实现个性化场景的文档数字化和信息化业务。

- **提供用户可控的定制化工具**，帮助用户实现其业务场景下的模型定制，实现业务数据驱动AI服务。

- **多模态信息抽取**，帮助客户实现 **多模态自定义信息抽取**，可达到服务可用、好用的效果。

- **支持少样本冷启动**，最少可支持用户通过一张图进行服务定制。

- **定制化效率提升**，支持用户端到端 **小时级AI模型定制，** 大大缩短业务等待时间。

- **交互友好型**，通过 **可视化人机交互，** 降低模型训练的进入与使用门槛。


## **功能详情**

OCR文档自学习平台现支持模板和模型两大类项目的自主训练。用户可以通过配置模板或少量标注数据，训练出更满足业务场景需求的AI智能模型。

### **模板：**

- #### [自定义KV模板](https://help.aliyun.com/zh/ocr/product-overview/custom-kv-template-1 "")


  - 配置一张模板图片，包括字段信息和规则，无需额外标注其他图片，也无需等待训练，即可完成固定版式票证的自定义字段抽取。更多信息及操作详见 [操作指南](https://help.aliyun.com/zh/ocr/product-overview/custom-kv-template-1#952e5ec0a8rye "")。
- #### [自定义表格模板](https://help.aliyun.com/zh/ocr/product-overview/custom-table-templates "")


  - 配置一张模板表格图片，包括字段信息和规则，无需额外标注其他图片，也无需等待训练，完成固定版式且有框线的单页表格自定义单元格抽取。更多信息及操作详见 [操作指南](https://help.aliyun.com/zh/ocr/product-overview/custom-table-templates#1fad6680a8gbk "")。

### **模型：**

- #### [单据票证信息抽取](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-information-extraction "")


  - 数据驱动，通过小样本数据标注、训练，实现对版式相对固定的单据、证件、凭证的关键字段进行信息抽取，更多信息及操作详见 [操作指南](https://help.aliyun.com/zh/ocr/product-overview/ticket-and-invoice-information-extraction#c5dbb0c0a8pg6 "")。
- #### [表格信息抽取](https://help.aliyun.com/zh/ocr/product-overview/table-information-extraction "")


  - 数据驱动，通过小样本数据标注、训练，实现对版式相对固定的表格、表单的关键字段进行信息抽取。更多信息及操作详见 [操作指南](https://help.aliyun.com/zh/ocr/product-overview/table-information-extraction#7e825e30a9z29 "")。
- #### [长文档信息抽取](https://help.aliyun.com/zh/ocr/product-overview/long-document-information-extraction "")


  - 数据驱动，通过小样本数据标注、训练，实现对多版式、非结构化的长文档关键信息进行抽取。更多信息及操作详见 [操作指南](https://help.aliyun.com/zh/ocr/product-overview/long-document-information-extraction#620e7c70a9of0 "")。

### [工具箱](https://help.aliyun.com/zh/ocr/product-overview/toolbox "") **：**

- #### [分类器管理](https://help.aliyun.com/zh/ocr/product-overview/toolbox\#bdf22d60a98ii "")


  - 通过添加关键词、分类数据实现将不同的模板或模型类型通过一个分类器关联，以实现同一接口接收多类型样本数据实现对应能力的路由与信息抽取；
- #### [字段类型管理](https://help.aliyun.com/zh/ocr/product-overview/toolbox\#e7883c00a960i "")


  - 支持对字段类型配置，主要针对业务/行业通用属性的字段，用于字段纠错以提升识别准确率或作归一化处理。

**说明**

#### **「自定义模板」和「信息抽取模型」功能都能够做抽取的任务，那么我们如何确定什么情况下选择什么能力呢？**

**自定义模板**：仅通过一张样本图配置，无需进行模型训练，适用于数据版式固定，对字段抽取准确率要求不高的业务冷启动快速验证阶段。

**信息抽取模型**：标准的“标注数据-模型训练”流程，通过可视化的模型标训完成业务专属的模型定制，适用于数据版式相对固定或可枚举，样本数量较为充足，对信息抽取准确率要求较高的业务稳定阶段。

## **价值主张**

- **数据资产化**：

  - 支持数据资产的闭环管理（上传、处理、标注等），提供一站式预处理与标注工具，通过平台可视化引导， **服务无算法基础的用户，5分钟内完成自定义模板任务从创建到发布全流程**，从而持续沉淀数据资产，助力业务的转型升级。
- **模型业务化**：

  - 通过预置的通用多模态AI能力，通过沉淀的数据资产，支持用户一键训练更满足业务场景需求的自主定制化模型，通过预训练模型、图文多模态算法和少样本信息抽取等核心技术能力，更高效、高精度地满足业务场景的需求。
- **管理平台化**：

  - 通过一站式的工具平台，提供从数据资产管理、模型构建、训练、部署的全流程管理工具，支持用户对模型评测与业务效果持续跟踪，未来通过持续业务正、负样本回流，实现业务运营管理的终生学习与持续迭代升级。提升业务场景的闭环与价值的持续提升。

## **产品优势**

#### **多模态文档信息抽取**

围绕“视觉文档信息抽取”中心，致力于解决复杂视觉文档的个性化信息抽取痛点，构建服务稳定、效果精准、链路智能的自学习信息抽取平台。

#### **零代码自主定制**

通过 **少样本** 等技术手段，降低模型训练门槛，让无算法基础的用户结合自己场景数据，自主完成模型定制，将数据资产转化成服务资产。

#### **高精度模型效果**

内置超大规模多模态预训练模型、多场景高精度文字识别模型，和统一的信息抽取模型，满足不同场景零代码建模的精度需求。

#### **高效模型生产效率**

内置智能化预标注和方便易用的一站式标注套件极大提升标注效率，内置基础预训练模型大幅提升模型在微调阶段的训练效率。

#### **灵活的部署形态**

支持高可用公共云形态与本地私有化部署，满足不同客户的落地需求。

## **应用场景**

#### **票据单证抽取**

支持对各类单据、票证的KV信息抽取，识别率可达95%，适用于版式相对固定且可枚举的场景。

#### **表格表单解析**

可实现对各类表格表单的信息抽取，识别率可达95%，适用于版式相对固定且可枚举的场景。

#### **非结构化长文档解析**

支持对各类非结构化文档进行自动化信息抽取，识别率可达85%，适用于处理非结构化的多页文档。

#### **公告公文处理**

支持公告公文等类型的文档信息抽取，通过文档自学习平台实现版式样式不固定下的文档处理。

## **联系我们**

如需更多沟通可通过钉钉群联系我们

【官方】阿里云OCR文档自学习用户答疑群：26560014923

【官方】阿里云OCR公共云客户交流群：35208328

【官方】阿里云文档智能客户交流群：44854217