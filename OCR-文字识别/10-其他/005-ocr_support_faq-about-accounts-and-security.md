### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[服务支持](https://help.aliyun.com/zh/ocr/support/)[常见问题](https://help.aliyun.com/zh/ocr/support/faq/)账号与安全相关

# 账号与安全相关

更新时间：2025-01-22 01:46:56

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：产品功能相关](https://help.aliyun.com/zh/ocr/support/faq-about-features)[下一篇：API/SDK](https://help.aliyun.com/zh/ocr/support/api-sdk)

该文章对您有帮助吗？

反馈

本章节介绍阿里云文字识别（OCR）关于账号与安全相关的常见问题与解答。

### 是否可以设置IP白名单呢？

OCR是API服务，暂不支持白名单设置，您可以在自己的服务器上调用我们的服务。如果担心AccessKey泄露，可以考虑通过创建RAM角色并使用STS临时授权的账号调用服务。

### OCR传输的数据是否经过加密呢？

阿里云文字识别采用阿里云官网标准网关，数据传输过程有全链路安全保障。

若您的数据有强敏感要求的话，可考虑使用私有化部署。阿里云OCR服务支持私有化部署和离线SDK部署两种方式。为您提供更加安全的服务保障。

### 使用OCR服务，图片数据是否会存储？

阿里云文字识别承诺公共云服务不落盘，用户的原始图片和识别数据均不作保留，识别返回后立即释放。具体可参看阿里云服务协议。

### RAM账户怎么设置产品调用权限？

需要确保RAM账号拥有 [AliyunOCRFullAccess](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "") 权限，否则无法通过该账号调用服务。

### 上传图片报错怎么解决？

请确保您上传的图片可以通过公网正常访问。

### 调用报错InvalidAccessKeyId.Inactive如何解决？

使用的子用户密钥已经被禁止，请启用密钥或更换密钥。密钥是否被禁止请通过 [RAM访问控制](https://ram.console.aliyun.com/users) >用户详情>AccessKey确认并开启。