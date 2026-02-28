### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 开通授权

# 开通授权

更新时间：2023-03-27 22:46:10

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

步骤一：注册账号并创建访问密钥

（可选）步骤二：购买所需个数的SDK授权

步骤三：创建离线语音合成项目

步骤四：配置SDK

步骤五：激活SDK

本文为您介绍如何开通、购买、配置并激活语音唤醒功能对应的SDK授权。

## **背景信息**

语音唤醒使用场景为离线端设备，因此我们提供商业版SDK加载并运行唤醒能力。授权服务为您的唤醒能力的透出、使用和知识产权提供了有力保障，是SDK初始化阶段必须检验的过程。语音唤醒与离线语音合成能力共用一套授权机制，如果您仅需要一句话识别/实时转写/云端语音合成等已售卖纯云端的产品，请前往 [阿里云官网](https://ai.aliyun.com/) 进行购买和接入。

开通授权后，登录阿里云账号，在语音交互控制台将获得一定配额的设备端解决方案授权量，并绑定到一个新建项目上，获取该项目的Appkey，用于SDK初始化时的参数设置。

下表为您介绍语音唤醒SDK初始化鉴权过程中所需的参数以及对应说明，更多信息，参见 [接口说明](https://help.aliyun.com/zh/isi/sdk-reference-12 "")。

|     |     |
| --- | --- |
| 参数 | 说明 |
| ak\_id | 阿里云AccessKey ID，更多信息，请参见 [步骤一：注册账号并创建访问密钥](https://help.aliyun.com/zh/isi/enable-authorization-1#yFzzI "")。 |
| ak\_secret | 阿里云AccessKey Secret，更多信息，请参见 [步骤一：注册账号并创建访问密钥](https://help.aliyun.com/zh/isi/enable-authorization-1#yFzzI "")。 |
| app\_key | 智能语音交互控制台创建项目的Appkey，更多信息，请参见 [步骤三：创建离线语音合成项目](https://help.aliyun.com/zh/isi/enable-authorization-1#FYGp9 "")。 |
| sdk\_code | SDK售卖码，根据 [步骤三](https://help.aliyun.com/zh/isi/enable-authorization-1) SDK类型的不同选择，sdk\_code对应不同的值：<br>- 选择 **设备端解决方案**，sdk\_code对应值为 **nls\_asrttssdk\_public\_cn**。<br>  <br>- 选择 **标准版离线语音合成SDK**，sdk\_code对应值为 **software\_nls\_tts\_offline\_standard**。<br>  <br>- 选择 **精品版离线语音合成SDK**，sdk\_code对应值为 **software\_nls\_tts\_offline**。 |
| device\_id | 设备标识，唯一标识一台设备（如Mac地址/SN/UniquePsuedoID）。请您自行设置，确保设备唯一，否则将可能导致鉴权失败。 |

## 步骤一：注册账号并创建访问密钥

关于注册阿里云账号以及创建访问密钥的具体操作，请参见 [准备账号](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1 "")。

您需要记录创建的 **AccessKey ID** 和 **AccessKey Secret**，用于后续初始化参数设置。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9626333761/p548169.png)

## （可选）步骤二：购买所需个数的SDK授权

离线语音合成为您提供5个SDK免费试用授权，如您仅试用语音唤醒能力，暂时无需购买授权，可跳过本步骤。如有更多商用需求，请执行此步骤。

1. 登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/overview)。

2. 单击左侧导航栏 **服务管理与开通**，切换到 **设备端解决方案** 页签，选择 **标准版离线语音合成SDK**，单击右侧 **购买资源包**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9626333761/p548186.png)



**说明**





由于语音唤醒和离线语音合成共用一套授权服务，因此在设备端解决方案页签下未单独设置唤醒类别，仅有标准版离线语音合成SDK和精品版离线语音合成SDK两项服务，如果您使用语音唤醒，选择标准版离线语音合成SDK即可。您可以通过钉钉搜索群号 **21295019391**，加入智能语音交互产品咨询群联系我们，确认购买的授权单价和授权量。

3. 在购买页面，再次选择商业版SDK **规格类型**，并设置 **规格数量**，确认费用后，单击右下角 **立即购买**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8626333761/p548196.png)



**说明**





   - 当购买了商用版离线语音合成SDK后，对应的试用版离线语音合成SDK将失效。例如，用户购买了2个标准版SDK授权，则可用SDK数量为2个，原来免费试用的5个SDK授权失效。

   - 商用版离线语音合成SDK的有效期为永久授权，购买产品后可永久使用。

   - 商用版SDK计费标准，请参见 [计费说明](https://help.aliyun.com/zh/isi/product-overview/billing-10 "")。


## 步骤三：创建离线语音合成项目

1. 登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/overview)。

2. 单击左侧导航栏 **全部项目**。

3. 在 **我的所有项目** 页面，单击左上角 **创建项目**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9626333761/p548207.png)

4. 配置项目信息。

1. 输入 **项目名称**。

2. **项目类型** 选择 **设备端解决方案。**

3. **SDK类型** 选择 **标准版离线语音合成SDK。**

4. （可选）输入 **项目场景描述**。

5. 单击 **确定**。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9626333761/p548209.png)

## 步骤四：配置SDK

1. 在 **我的所有项目** 页面，找到步骤二中创建的项目，单击右侧 **操作** 栏中的 **项目功能配置**。

2. 修改 **应用配额**。![image](<Base64-Image-Removed>)



**说明**





应用配额为同一用户在不同项目（Appkey）中最多使用的配额数量。例如，某用户共购买500个标准版离线TTS SDK授权，则SDK剩余额度/总额度为500/500。该用户有两个项目使用到了标准版离线TTS SDK，如果项目1配置300个，则项目2最多只能配置200个。

3. 单击 **复制**，拷贝 **appkey** 到SDK集成代码中使用。![image](<Base64-Image-Removed>)


## 步骤五：激活SDK

1. 下载公版唤醒识别SDK。

2. 激活并初始化SDK，具体操作，请参见语音唤醒 [接口说明](https://help.aliyun.com/zh/isi/sdk-reference-12 "")。


**说明**

每台设备消耗一个SDK授权，详情请参见 [配额消耗规则](https://help.aliyun.com/zh/isi/faq-about-wake-up-word-recognition#0f03e8a08fkog "")。