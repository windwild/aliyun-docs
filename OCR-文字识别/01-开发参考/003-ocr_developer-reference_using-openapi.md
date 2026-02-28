### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)使用OpenAPI

# 使用OpenAPI

更新时间：2023-08-22 06:23:25

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：文字识别自定义权限策略参考](https://help.aliyun.com/zh/ocr/security-and-compliance/text-recognition-custom-permission-policy-reference)[下一篇：SDK概述](https://help.aliyun.com/zh/ocr/developer-reference/sdk-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

基本信息

版本说明

接入点说明

用户身份

接口风格

调用方式支持情况

注意事项

本文为您介绍使用文字识别（OCR）OpenAPI的基本信息及注意事项。

**说明**

关于如何使用阿里云OpenAPI，请参见学习文档： [使用OpenAPI](https://help.aliyun.com/document_detail/2391383.html "")。

## 基本信息

### **版本说明**

| **版本号** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **版本号** | **说明** |
| [2021-07-07](https://next.api.aliyun.com/document/ocr-api/2021-07-07/overview) | 推荐 |

### **接入点说明**

参见 [服务接入点](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-endpoint "")。

### 用户身份

| **用户身份** | **支持情况** |
| --- | --- |

|     |     |
| --- | --- |
| **用户身份** | **支持情况** |
| [阿里云账号](https://help.aliyun.com/document_detail/2391618.html "") | 支持 |
| [RAM用户](https://help.aliyun.com/document_detail/2391619.html "")（推荐） | 支持 |
| [RAM角色](https://help.aliyun.com/document_detail/2391620.html "")（推荐） | 支持 |

推荐您使用 **RAM用户** 或 **RAM角色**，根据业务的实际情况按需分配权限后进行接口调用。

### **接口风格**

RPC风格。更多关于接口风格介绍请参见 [OpenAPI 风格](https://help.aliyun.com/document_detail/2392109.html "")。

### **调用方式支持情况**

| **调用方式** | **支持情况** | **备注** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **调用方式** | **支持情况** | **备注** |
| 阿里云SDK（推荐） | 支持 | - 文字识别（OCR）支持语言及依赖安装方法请参考[印刷文字识别 SDK](https://next.api.aliyun.com/api-tools/sdk/ocr-api?version=2021-07-07&language=java-tea)，也可以参考以下文档：<br>  <br>  - [Java SDK快速开始](https://help.aliyun.com/zh/sdk/developer-reference/v2-java-quick-start "")<br>    <br>  - [Python SDK快速开始](https://help.aliyun.com/zh/sdk/developer-reference/v2-python-quick-start "")<br>- 阿里云SDK集成方式说明请参见 [阿里云SDK](https://help.aliyun.com/zh/openapi/alibaba-cloud-sdks "")。 |
| 阿里云CLI | 不支持 | 阿里云CLI调用方式说明请参见 [阿里云CLI](https://help.aliyun.com/zh/openapi/alibaba-cloud-cli "")。 |
| 资源编排 | 不支持 | 阿里云资源编排调用方式说明请参见 [资源编排](https://help.aliyun.com/zh/openapi/ros "")。 |
| Terraform | 不支持 | Terraform编排调用方式说明请参见 [Terraform](https://help.aliyun.com/zh/openapi/terraform "")。 |

若以上方案均无法满足您的业务需要，可自行封装请求调用OpenAPI，详情请参见 [自定义封装](https://help.aliyun.com/document_detail/2392103.html "")。

## 注意事项

推荐您使用阿里云SDK方式集成文字识别（OCR）OpenAPI。