### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[快速入门](https://help.aliyun.com/zh/isi/getting-started/)从这里开始

# 从这里开始

更新时间：2025-01-16 03:47:51

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：功能发布记录](https://help.aliyun.com/zh/isi/product-overview/release-notes)[下一篇：管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

入门流程

步骤1：准备账号

步骤2：创建AccessKey

创建阿里云账号的AccessKey

创建RAM用户的AccessKey

步骤3：开通服务

步骤4：管理项目

步骤5：获取Token

步骤6：集成开发

智能语音交互产品基于语音识别、语音合成、自然语言理解等技术，实现“能听、会说、懂你”式的智能人机交互体验，适用于智能客服、质检、会议纪要、实时字幕等多个企业应用场景。本文为您介绍如何使用智能语音交互，帮助您快速了解其使用流程和具体操作。

## **入门流程**

快速入门文档介绍使用智能语音服务需要的步骤，帮助您快速开通服务、创建测试项目和调用语音服务。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0727107371/CAEQORiBgIDTwZ7G6BgiIDI1NjM0ZWUyNWUxOTRiYWY5YmYzYzMzNTM1OTBkYzQ54024891_20231008151700.663.svg)

## **步骤1：准备账号**

1. 注册阿里云账号。

阿里云账号作为阿里云系统识别的资源消费账户，有阿里云所有产品和管理权限。具体操作，请参见 [注册阿里云账号](https://help.aliyun.com/document_detail/324609.html "")。

2. 个人实名认证。

为了确保您可以正常使用阿里云产品和服务，您需要完成个人实名认证。具体操作，请参见 [个人实名认证](https://help.aliyun.com/document_detail/324614.html "")。

3. （可选）创建并授权RAM用户。

当您的企业存在多用户协同访问资源的场景时，可以创建RAM用户，使用RAM可以按需为用户分配最小权限，避免多用户共享阿里云账号密码或访问密钥，从而降低企业的安全风险。具体操作，请参见 [创建RAM用户](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "")。关于RAM用户的更多信息，请参见 [什么是访问控制](https://help.aliyun.com/zh/ram/product-overview/what-is-ram/#concept-oyr-zzv-tdb "")。

如果使用RAM用户调用智能语音交互产品，请前往 [控制台](https://ram.console.aliyun.com/users) 为RAM用户授予 **AliyunNLSFullAccess** 权限。具体操作，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")。

![RAM授权](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3287483661/p493338.png)



**说明**





创建RAM用户时，请设置登录密码，否则无法单独登录RAM账号。


## 步骤2： **创建AccessKey**

在调用阿里云API时您需要使用AccessKey完成身份验证，AccessKey包括AccessKey ID和AccessKey Secret，具体说明如下：

- AccessKey ID：用于标识用户。

- AccessKey Secret：用于验证用户的密钥。AccessKey Secret必须保密。


### **创建阿里云账号的AccessKey**

登录 [RAM访问控制台](https://ram.console.aliyun.com/manage/ak)，使用阿里云账号创建AccessKey。具体操作，请参见 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair#section-ynu-63z-ujz "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3794716071/p762511.png)

### **创建RAM用户的AccessKey**

使用阿里云账号登录 [RAM访问控制台](https://ram.console.aliyun.com/users)，为RAM用户创建AccessKey。具体操作，请参见 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair#section-rjh-18m-7kp "")。

**重要**

RAM用户的AccessKey Secret仅在创建时显示，创建后将无法查看。请在创建时进行备份（比如保存到本地），以便您后续查看其内容。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2794716071/p762512.png)

## 步骤3： **开通服务**

如果您是第一次使用智能语音交互，推荐您使用阿里云账号开通智能语音交互服务。

进入 [智能语音交互产品首页](https://ai.aliyun.com/nls)，单击 **开通并购买**，然后在产品开通页面，选择服务类型并选中 **服务协议**，单击 **立即开通**，即可开通智能语音交互服务。

| **类型** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **类型** | **说明** |
| 免费试用版 | 默认全部试用。长文本语音合成、录音文件识别（闲时版）和录音文件识别（极速版）无试用版。<br>新开通服务的用户可免费试用3个月，支持2路并发（即同时最大2个任务）或每日2小时的录音文件识别额度。<br>**重要**<br>新用户试用期3个月内，每隔24小时可免费识别2小时时长的文件转写服务。免费额度用完后，间隔24小时后可继续试用。 |
| 商用版 | 选择某个或多个语音服务为商用，开通后按量计费，根据实际使用量从您的阿里云账户余额中扣费。更多信息，请参见 [计费方式](https://help.aliyun.com/zh/isi/product-overview/billing-10 "")。 |

![立即开通](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3287483661/p493555.png)

## 步骤4： **管理项目**

登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/applist)，创建项目生成对应的Appkey。具体操作，请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects "")。

## 步骤5： **获取Token**

访问令牌（ Token）是调用智能语音交互服务的服务鉴权凭证。

Token在不同项目间、不同进程间、不同线程间都可以共用，Token有效期根据服务端返回为准，过期前必须提前重新获取Token，建议每天重新获取。为了安全起见，建议您在服务端集成Token SDK，客户端从服务端获取Token。

| **获取Token方式** | **建议使用场景** |
| --- | --- |

|     |     |
| --- | --- |
| **获取Token方式** | **建议使用场景** |
| [通过控制台获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token-in-the-console#0196f89028lk2 "") | 仅供测试使用，在控制台获取Token。 |
| [通过SDK获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token#title-u2l-tam-gms "") | 正式环境使用，通过传入AccessKey ID和AccessKey Secret，在SDK通过代码定期自动获取Token。 |
| [获取Token协议说明](https://help.aliyun.com/zh/isi/getting-started/use-http-or-https-to-obtain-an-access-token#title-edc-op8-z5d "") | 若对应的编程语言缺少SDK，或者需要控制依赖组件，可以通过OpenAPI获取Token。 |

## 步骤6： **集成开发**

根据以上几步获取到账号对应的 **AccessKey ID**、 **AccessKey Secret**、 **服务鉴权Token**、以及 **项目Appkey**，必须确保这几项数值归属于同一阿里云账号或同一RAM用户。

您可以根据以上信息，通过命令行等方式快速体验智能语音交互产品能力，具体操作，请参见 [运行示例](https://help.aliyun.com/zh/isi/getting-started/examples-of-using-sdks-and-managing-restful-apis "")。也可以通过 [SDK和API概览](https://help.aliyun.com/zh/isi/getting-started/sdk-and-api-references "") 详细了解在各类平台如何将 [语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/) 或 [语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/) 功能集成到您的服务当中。

| **集成运行** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **集成运行** | **说明** |
| [运行示例](https://help.aliyun.com/zh/isi/getting-started/examples-of-using-sdks-and-managing-restful-apis "") | 基于使用阿里云主账号且从控制台获取测试Token来体验产品。<br>主要通过控制台、curl命令行、postman、以及Java SDK等方式快速体验智能语音交互能力。 |
| [SDK和API概览](https://help.aliyun.com/zh/isi/getting-started/sdk-and-api-references "") | RESTful API、移动端、服务端、微信小程序以及WebSocket等多种接入方式。 |