### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/) [服务支持](https://help.aliyun.com/zh/ocr/support/) [OCR云市场文档集合](https://help.aliyun.com/zh/ocr/support/ocr-document-collection-in-alibaba-cloud-marketplace/) 云市场常见问题

# 云市场常见问题

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：自定义模板变更通知](https://help.aliyun.com/zh/ocr/support/notice-on-custom-template-change)[下一篇：云市场服务协议](https://help.aliyun.com/zh/ocr/support/alibaba-cloud-marketplace-service-agreement)

该文章对您有帮助吗？

反馈

本章节介绍阿里云OCR在云市场官方店铺（“阿里云计算有限公司”）的常见问题。

## 产品功能相关问题

### 对图片的格式大小有怎样的要求？

阿里云文字识别服务要求单张图片大小不超过10M, 图片最长边不超过4096像素，最短边不小于15像素，当长边超过1024像素时，长宽比不超过1:10； 若对响应时长有较高要求的客户，图片大小建议控制在1.5M以内。

图片像素大小没有具体要求，单字大小在10-50像素内，识别效果比较好；尽量选择图像清晰度高、无反光的图片。若图片有旋转角度，算法会自动修正。具体的识别率与具体图片质量有较大关系。

### 能够识别复印件吗？

目前身份证，银行卡，营业执照三个接口可以判断是否为复印件，但是无法判断真伪（是否PS）；其他证件若有特殊需求可单独加入钉钉答疑群21734896进行需求沟通。

### 哪些接口可以识别多种类图片？

通常情况下阿里云文字识别提供的接口仅支持单张图片的识别，若需要对多种类型图片识别可参考如下产品：

1. 购买卡证合集接口，可支持多种卡证的识别，但卡证需要为单张调用。 [https://market.aliyun.com/products/57124001/cmapi031271.html#sku=yuncode2527100001](https://market.aliyun.com/products/57124001/cmapi031271.html#sku=yuncode2527100001)![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8404231071/p743259.png)

2. 购买票据混贴智能分区识别，可支持一张图片上有多张混贴图的场景，系统可自动进行分区、分类与结构化识别。

[https://market.aliyun.com/products/57124001/cmapi00034969.html](https://market.aliyun.com/products/57124001/cmapi00034969.html)![混贴发票](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6900090661/p479236.png)

3. 购买多卡证智能分类，可对未知分类场景下的图片进行自动分类与结构化识别。

[https://market.aliyun.com/products/57124001/cmapi00034972.html](https://market.aliyun.com/products/57124001/cmapi00034972.html)


### 房产证支持哪几种房产证类型？

房产证目前支持这几种：房权证、房地权证、广东房产证、上海房产证、安徽房产证、浙江台州房产证；

考虑到三证合一，后续推荐使用不动产权证识别，不动产权证将兼容老房产证，且支持全国范围的房产证类型。

### QPS不够用怎么办？

云市场为单个账号提供10QPS的默认流量，最高支持10个并发同时请求。建议您在您的程序中可进行一定的访问限制，避免造成批量服务限流报错的情况。

同时，阿里云官网将于2021年12月份上线QPS叠加包服务，届时您可通过购买QPS叠加包进行容量扩充，可关注产品动态。

## 计量计费相关问题

### 购买错了资源包能否申请退款？

原则上云市场API类产品按规定无法退款，请您购买商品的时候仔细核对所需的产品（可使用 [读光体验馆](https://duguang.aliyun.com/experience?type=universal&subtype=general) 再次验证是否为所需商品）。

若因产品介绍说明有误导致的购买错误 **且资源包尚未使用**，可工单申请退款，预需要计3-4个工作日审批，款项会原路退回。在审批期间，如您急需使用其他产品，可以先购买相应资源包。

工单提交入口：在云市场商品详情页点击“提交工单”，并输入您的问题，会有服务人员联系您。![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6904521071/p742973.png)

### 资源包没用完但快到期了能否退款？

云市场资源包一经售卖且产生正常调用抵扣，不允许进行退款。资源包属于预付费产品，建议您在购买资源包的时候按实际调用情况预估调用量以免造成资源浪费，谢谢配合！

云市场的资源包有效期为1年（自购买之日起算），请合理评估和使用，调用量抵扣情况可以在云市场控制台 -> 已购买的服务 -> 订单上最右下角点击“套餐包列表”-\> 找到需要查明细的套餐包，点右侧的“使用明细”查看，系统每隔10分钟会更新调用明细。

若您无法预估业务的调用量，可选择 [按量付费](https://help.aliyun.com/zh/ocr/product-overview/pay-as-you-go#topic-2084734 "") 的后付费模式，根据实际调用进行扣费。

### 什么情况下会扣资源包次数，识别报错会扣费吗？

资源包扣费规则按照：成功识别才算入计费次数，若识别报错则不计算次数。单张图片算作一次调用；

若您的图片上存在多张图片，可能会导致对应接口识别报错，建议可进行如下操作：

1\. 将所需图片自行拆解成单张图片进行调用识别；

2\. 使用通用票证混贴接口，混贴接口支持多图识别，但所需图片类型仅限阿里云OCR所覆盖的卡证类产品；

### 在哪里可以查询调用量/资源包剩余次数？

调用明细：可在控制台查看，云市场控制台 -> 已购买的服务 -> 订单上最右下角点击“套餐包列表”-\> 找到需要查明细的套餐包，点右侧的“使用明细”；每隔10分钟会更新调用明细

剩余次数：可在云市场管理控制台查看，参考链 [https://market.console.aliyun.com/imageconsole/index.htm](https://market.console.aliyun.com/imageconsole/index.htm)

## 账号安全相关问题

### 是否可以设置IP白名单呢？

OCR是API服务，暂不支持白名单设置。请您通过后端服务器来调用我们的服务，避免AppCode等参数暴露在前端请求里，并保护好AppCode、AppKey、AppSecret等数据。

### OCR传输的数据是否经过加密呢

阿里云文字识别采用云市场标准网关，数据传输过程有全链路安全保障，通过云市场标准网关后数据仅在内部网络中传输，不会暴露在公网。请您通过HTTPS接口而不是HTTP的方式调用我们的接口，确保您的服务器和云市场标准网关之间的数据安全。

若您的数据有安全监管的严格要求（如不能出您的内部网络），您可考虑使用私有化部署。阿里云OCR服务支持私有化部署和离线SDK部署两种方式。为您提供更加安全的服务保障。

### 使用OCR服务，图片数据是否会存储？

阿里云文字识别承诺公共云服务不落盘，用户的原始图片和识别结果数据均不作保留，识别返回后立即释放。具体可参看阿里云服务协议。

同时，云市场提供了API服务体验改进计划，在用户主动同意授权的情况下，可将部分数据用于定向的模型优化训练。（该体验计划为自愿参与，下单时若未勾选该计划不会进行数据保存）

## 故障排查相关问题

### 远程服务器返回错误码460，应该如何解决？

通常是您的请求body部分参数不符合JSON规范。可以通过检查body参数来解决，或者把body参数尝试转换成JSON格式，之后将JSON格式的 {"image","base64图片"} 的string 再转成byte\[\]传进去。
云市场每个接口在商品页面都提供了curl、JAVA、C#、PHP、Python、ObjectC等语言的SDK，请按照示例调通任一种调用方式。

### 远程服务器返回错误码503，应该如何解决？

这是算法超时错误，有两种可能原因，您的调用图片体积过大或者内容过于复杂，可能会造成算法服务不能按时返回，此种情况建议您将图片切成多个小的图片分开调用。

如果持续出现普通图片调用返回503错误，可能是服务总体请求量过大造成。算法服务集群的总容量平常是按照最近30天的调用峰值作为参考加上一定比例的富余容量进行配置的，通常不会出现这种总量不够的情况，但由于各客户调用QPS存在偶发性，在特殊情况下可能会发生总量挤兑，此种情况您可以联系我们进行反馈（我们的运维人员也会自动收到系统的错误监控），我们的运维人员会通过紧急扩容来解决此问题。

### 远程服务器返回错误码464，应该如何解决？

通常是算法服务无法正确处理您的调用图片，如您调用身份证接口，算法服务无法做到100%的正确识别，错误分类的情况下，返回的结果可能是464错误（错误返回情况下并不会扣除您的调用次数）。

OCR算法服务是基于深度学习的AI产品，无论是分类还是文字识别都无法做到100%的正确率。对于不能正确处理的图片，请您人工核对。

### 遇到文字识别错误，应该如何解决？

OCR算法服务是基于深度学习的AI产品，无论是分类还是文字识别都无法做到100%的正确率。对于识别的结果，在使用的时候需要您进行人工核对。少量错误请您通过人工核对的方式解决。如果存在大量的同类型错误，请反馈给我们，以便我们进行针对性的优化。

## 其他常见问题

### 我需要合同进行申请款项要在哪里申请合同？

正式合同是需要在付款后才能申请，未支付无法申请。如有特殊需求，需要申请购买前的合同，需要联系cbm或者电销。合同路径：云市场控制台 \- 订单列表 \- 申请合同。

需要声明的是，付款前的合同预览日期有效期显示为1天（因为并未正式生效而生成的临时预览合同），正式合同有效期是1年，可提前告知您的法务、财务，避免造成困扰。

### OCR可以支持私有化部署吗？

OCR产品支持本地化部署，可部署在客户自有环境中。私有化部署以docker镜像方式进行部署，需要客户自行准备服务器资源（通常为GPU服务器），若有私有化部署需求可进一步 [联系我们](https://ai.alimebot.taobao.com/intl/index.htm?spm=5176.20003231.J_8400342310.link.477f39bbrSiK7A&from=PDw4dNTppm&_user_access_token=aW12WFBXQUdrU3pyc2xGaVFIekEzWEVtZldscWNocHBUWXJTa1daK2lBckpEQU1xcmk4WFpzb2trTUdVWDQ1RDVMZm1rQnJWNXI1L0R5emcxUnVWQkFIMytqdG1oT3E5QzZjNGFvTHo1T2xzbXJvN0p1SjVEc0FzdnljZ0pQVjkwejduM0I0Sm9aRC9FbU1NdXI5N0swRVFSc3hmMm5lVU9TTlBYRG1rOEYwPQ==)。

### OCR有离线SDK吗？

OCR支持特定场景的SDK，包含身份证识别SDK、银行卡识别SDK、手机号提取SDK、指尖检测SDK、图像矫正SDK、扫读SDK等。若有离线SDK需求可进一步 [联系我们](https://ai.alimebot.taobao.com/intl/index.htm?spm=5176.20003231.J_8400342310.link.477f39bbrSiK7A&from=PDw4dNTppm&_user_access_token=aW12WFBXQUdrU3pyc2xGaVFIekEzWEVtZldscWNocHBUWXJTa1daK2lBckpEQU1xcmk4WFpzb2trTUdVWDQ1RDVMZm1rQnJWNXI1L0R5emcxUnVWQkFIMytqdG1oT3E5QzZjNGFvTHo1T2xzbXJvN0p1SjVEc0FzdnljZ0pQVjkwejduM0I0Sm9aRC9FbU1NdXI5N0swRVFSc3hmMm5lVU9TTlBYRG1rOEYwPQ==)。