### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[服务支持](https://help.aliyun.com/zh/ocr/support/)[常见问题](https://help.aliyun.com/zh/ocr/support/faq/)API/SDK

# API/SDK

更新时间：2025-01-22 05:18:51

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：账号与安全相关](https://help.aliyun.com/zh/ocr/support/faq-about-accounts-and-security)[下一篇：联系我们](https://help.aliyun.com/zh/ocr/support/contact-us)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

接口调用报错的常见原因有哪些？

可以直接通过HTTP方式调用不通过SDK调用么？

本章节介绍阿里云文字识别（OCR）关于API/SDK相关的常见问题与解答。

## **接口调用报错的常见原因有哪些？**

接口调用报错时，您可以尝试以下步骤进行排查：

1. 检查参数格式：确保传入的参数格式正确。如果使用`url`参数，需确保URL为公网可访问地址；如果使用`body`参数，需要将图片文件转换为二进制传入。

2. 检查接口调用代码：参考 [调用文字识别OCR接口](https://help.aliyun.com/zh/ocr/developer-reference/sdk-overview#12c4c58fdechk "")，确保您的代码中正确配置了`AccessKeyId`和`AccessKeySecret`，并且指定了正确的Endpoint。

3. 查看错误信息：根据返回的错误信息，进一步诊断问题。您可以参考 [错误码诊断](https://error-center.aliyun.com/status/product/ocr-api) 来获取详细的错误信息和推荐处理方案。


如果以上步骤仍无法解决问题，请通过钉钉加入答疑群（群号码：35208328），以获取问题解答和支持。

## **可以直接通过HTTP方式调用不通过SDK调用么？**

建议您使用在线调试，如果使用HTTP调用需要自行计算签名等一些参数，比较麻烦。您可以在阿里云 [OpenAPI文字识别](https://next.api.aliyun.com/api/ocr-api/2021-07-07/RecognizeAllText?sdkStyle=dara) 在线调试成功之后，下载完整工程到您的项目中使用即可，SDK已经封装好了计算签名等一些公共参数的方法，能够显著简化开发过程，降低错误率，提高开发效率和代码的可维护性。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0311457371/p909829.png)