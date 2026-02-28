## 错误码

| HTTP status code | 错误码 | 错误信息 | 描述 | 操作 |
| --- | --- | --- | --- | --- |

| HTTP status code | 错误码 | 错误信息 | 描述 | 操作 |
| --- | --- | --- | --- | --- |
| 503 | algorithmError | An algorithm error occurred. | 识别服务异常，请稍后重试 | [诊断](https://api.aliyun.com/troubleshoot?q=algorithmError) |
| 413 | exceededImageContent | The image content size exceeds the 10 MB limit. | 图像内容大小超过 10M | [诊断](https://api.aliyun.com/troubleshoot?q=exceededImageContent) |
| 400 | illegalCutType | The specified cutType is invalid. | 不支持的cutType参数，支持的cutType类型为：question、answer。<br>1\. question：图片类型为图题目<br>2\. answer：图片类型为答案<br>详情请参考API文档：https://help.aliyun.com/document\_detail/442309.html | [诊断](https://api.aliyun.com/troubleshoot?q=illegalCutType) |
| 400 | illegalImageContent | The corresponding image content is missing. | 缺少对应的图像内容，导致切图失败 | [诊断](https://api.aliyun.com/troubleshoot?q=illegalImageContent) |
| 400 | illegalImageType | The specified imageType is invalid. | 不支持的 imageType 参数 | [诊断](https://api.aliyun.com/troubleshoot?q=illegalImageType) |
| 400 | IllegalImageUrl | The image URL is unavailable or has timed out. | 图片 URL 资源不可用或超时 | [诊断](https://api.aliyun.com/troubleshoot?q=IllegalImageUrl) |
| 400 | illegalSignature | The signature is incorrect. | 签名错误 | [诊断](https://api.aliyun.com/troubleshoot?q=illegalSignature) |
| 400 | illegalSubject | The specified Subject is invalid. | 不支持的 subject（科目） 参数 | [诊断](https://api.aliyun.com/troubleshoot?q=illegalSubject) |
| 400 | invalidStsToken | The STS token is invalid. | STS token 错误 | [诊断](https://api.aliyun.com/troubleshoot?q=invalidStsToken) |
| 400 | MissingImageUrl | You must specify image URL. | 图片URL为空 | [诊断](https://api.aliyun.com/troubleshoot?q=MissingImageUrl) |
| 401 | noPermission | You are not authorized to perform this operation. | 子账号或角色未授权 | [诊断](https://api.aliyun.com/troubleshoot?q=noPermission) |
| 400 | notSafeImageUrl | The image URL is not safe. | 图片 URL 不安全 | [诊断](https://api.aliyun.com/troubleshoot?q=notSafeImageUrl) |
| 401 | ocrServiceNotOpen | You have not activated the OCR service. | 当前正在调用的服务尚未开通，请登录文字识别控制台，单击服务管理与开通，检查并开通相应服务。 | [诊断](https://api.aliyun.com/troubleshoot?q=ocrServiceNotOpen) |
| 400 | unmatchedImageType | The image type does not match the API operation. | 图像类型与API接口不匹配 | [诊断](https://api.aliyun.com/troubleshoot?q=unmatchedImageType) |
| 400 | unsupportedEncodeImageUrl | The image URL encoding cannot be parsed. | 图片 URL 编码无法解析 | [诊断](https://api.aliyun.com/troubleshoot?q=unsupportedEncodeImageUrl) |
| 415 | unsupportedImageFormat | The image format or content is not supported. | 图像内容错误或格式不支持 | [诊断](https://api.aliyun.com/troubleshoot?q=unsupportedImageFormat) |
| 400 | unsupportedLanguage | The language is not supported. | 不支持的 language 参数 | [诊断](https://api.aliyun.com/troubleshoot?q=unsupportedLanguage) |
| 401 | OcrServiceExpired | The OCR service has expired. | OCR服务已经欠费过期 | [诊断](https://api.aliyun.com/troubleshoot?q=OcrServiceExpired) |
| 400 | MissingLanguages | You must specify Language. | 缺少 language 参数 | [诊断](https://api.aliyun.com/troubleshoot?q=MissingLanguages) |
| 503 | AlgorithmTimeout | The requested algorithm service is unavailable. Please try again with a smaller image. | 算法服务不可用，请尝试内容较少的图像。 | [诊断](https://api.aliyun.com/troubleshoot?q=AlgorithmTimeout) |
| 416 | illegalImageSize | The image size must not be less than 5px or greater than 8192px. | 图像尺寸不合法 | [诊断](https://api.aliyun.com/troubleshoot?q=illegalImageSize) |
| 400 | ExceededImageSize | The image length\*width must be less than 1024\*1024. | 图像尺寸的长度\*宽度必须小于等于1024\*1024。 | [诊断](https://api.aliyun.com/troubleshoot?q=ExceededImageSize) |
| 400 | PaperCutEmptyImage | The image is empty. No paper is found in the image. | 在用于切题的图像中没有找到任何试卷，请检查图像。 | [诊断](https://api.aliyun.com/troubleshoot?q=PaperCutEmptyImage) |
| 400 | ExceededFaceBackCount | The number of the front and back sides of the image exceeds the limit. | 图片正反面数量超过了限制 | [诊断](https://api.aliyun.com/troubleshoot?q=ExceededFaceBackCount) |
| 400 | exceededImageUrlLength | The image URL length exceeds 2048 characters. | 图片 URL 长度超过2048 | [诊断](https://api.aliyun.com/troubleshoot?q=exceededImageUrlLength) |
| 504 | ServiceTimeout | The requested service is timed out. | 后端服务超时 | [诊断](https://api.aliyun.com/troubleshoot?q=ServiceTimeout) |
| 400 | imageUrlOrBodyEmpty | The image URL or body is empty. | 图片URL或BODY为空 | [诊断](https://api.aliyun.com/troubleshoot?q=imageUrlOrBodyEmpty) |
| 400 | imageTimeOut | Get image data time out. | 获取图片超时 | [诊断](https://api.aliyun.com/troubleshoot?q=imageTimeOut) |
| 400 | deprecatedApi | The api is deprecated. | 此API已经废弃，请使用新版本的API | [诊断](https://api.aliyun.com/troubleshoot?q=deprecatedApi) |
| 400 | convertPDFToImgError | Failed to convert PDF file to image. | pdf转图片失败 | [诊断](https://api.aliyun.com/troubleshoot?q=convertPDFToImgError) |
| 413 | exceededPDFContent | Size of PDF content has exceeded the 10M limit. | PDF大小超过10M | [诊断](https://api.aliyun.com/troubleshoot?q=exceededPDFContent) |
| 400 | illegalPDFContent | Corresponding pdf content is missing | PDF内容缺失或不是有效的PDF文件 | [诊断](https://api.aliyun.com/troubleshoot?q=illegalPDFContent) |
| 400 | InvalidCountry | Specified parameter Country is not valid. | 不支持的国家。 | [诊断](https://api.aliyun.com/troubleshoot?q=InvalidCountry) |
| 400 | InvalidSignatureVerssion | Invalid signature version. | 签名版本错误 | [诊断](https://api.aliyun.com/troubleshoot?q=InvalidSignatureVerssion) |
| 400 | illegalApiName | Invalid API name. | API名称出错 | [诊断](https://api.aliyun.com/troubleshoot?q=illegalApiName) |
| 400 | Throttling.User | Request denied because the throttling threshold is reached. | 超过限流阈值 | [诊断](https://api.aliyun.com/troubleshoot?q=Throttling.User) |
| 400 | MissingAccessKeyId | AccessKey ID is required. | 缺少AccessKeyId | [诊断](https://api.aliyun.com/troubleshoot?q=MissingAccessKeyId) |
| 400 | InvalidVersion | Invalid parameter version. | 参数版本错误 | [诊断](https://api.aliyun.com/troubleshoot?q=InvalidVersion) |
| 400 | SignatureNonceUsed | The signature nounce is already in use. | 签名已经被使用过，请参考文档，重新计算签名：https://help.aliyun.com/document\_detail/469176.html | [诊断](https://api.aliyun.com/troubleshoot?q=SignatureNonceUsed) |
| 503 | ServiceUnavailable | Server error. | 服务器错误 | [诊断](https://api.aliyun.com/troubleshoot?q=ServiceUnavailable) |
| 400 | SignatureDoesNotMatch | Signature error. | 构造的签名出错：<br>1\. 建议您通过SDK调用API，以访问密钥（AccessKey）识别调用者身份，无需构造签名。（SDK文档：https://help.aliyun.com/document\_detail/295361.html）<br>2\. 如业务强依赖于自主构造的签名，请参照签名文档构造签名。（签名文档：https://help.aliyun.com/document\_detail/469176.html） | [诊断](https://api.aliyun.com/troubleshoot?q=SignatureDoesNotMatch) |
| 400 | MissingImageType | ImageType is required. | 缺少图片类型 | [诊断](https://api.aliyun.com/troubleshoot?q=MissingImageType) |
| 400 | MissingSignature | Signature is required. | 缺少签名 | [诊断](https://api.aliyun.com/troubleshoot?q=MissingSignature) |

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[开发参考](https://help.aliyun.com/zh/ocr/developer-reference/)[API参考](https://help.aliyun.com/zh/ocr/developer-reference/api-reference-1/)公共错误码

# 公共错误码

更新时间：2025-12-08 21:14:16

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：VerifyVATInvoice - 发票核验](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-verifyvatinvoice)[下一篇：版本说明](https://help.aliyun.com/zh/ocr/developer-reference/api-ocr-api-2021-07-07-changeset)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

错误码