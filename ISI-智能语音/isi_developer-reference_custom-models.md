### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/) [开发参考](https://help.aliyun.com/zh/isi/developer-reference/) [语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/) [自学习平台](https://help.aliyun.com/zh/isi/developer-reference/customization-platform/) 语言模型定制

# 语言模型定制

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用SDK设置业务专属热词](https://help.aliyun.com/zh/isi/developer-reference/use-an-sdk-to-specify-the-id-of-a-business-specific-hotword-vocabulary)[下一篇：定制语言模型](https://help.aliyun.com/zh/isi/developer-reference/create-a-custom-linguistic-model)

该文章对您有帮助吗？

反馈

阿里云智能语音交互对某些场景（包括通用、教育、司法、医疗等）进行了大量语音识别训练，提供了高准确率场景模型。当您的语音识别需求超出预设模型范畴，或是希望对现有的标准模型进行个性化定制时，可以通过自学习平台的语言模型定制功能，根据自身业务相关的语料进行针对性训练和优化，从而提升语音识别效果。

## 功能优势

通过使用阿里云语音自学习工具，您可以在操作界面上传训练语料文本，并选择对应领域的语言基础模型，对训练语料做模型训练，从而有效提高该场景的语音识别率。尤其针对专有名词和高频词汇，有较好的优化效果。

## 定制语言模型的方式

您可以通过 [定制语言模型](https://help.aliyun.com/zh/isi/developer-reference/create-a-custom-linguistic-model "") 或 [使用POP API创建自学习模型](https://help.aliyun.com/zh/isi/developer-reference/call-api-operations-to-manage-custom-linguistic-models "") 方式定制语言模型。具体区别如下：

- 使用控制台训练和管理自学习模型，可以界面化操作，在控制台 **项目功能配置** 中，单击 **切换场景**，选择自学习模型，发布上线后将与Appkey绑定，无需在代码中设置。

- 使用POP API创建的自学习模型，需要您在客户端代码中调用SDK的接口设置自学习模型的ID后，该模型才能生效。


## 应用举例

[下载训练语料](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20221013/etnz/demo-data-text.zip)，以阿里巴巴简介为例：

```javascript
一九九九年九月，马云带领下的十八位创始人在杭州的公寓中正式成立了阿里巴巴集团，集团的首个网站是英文全球批发贸易市场阿里巴巴。
一九九九年十月，阿里巴巴集团从数家投资机构融资五百万美元。
一九九九年十月，阿里巴巴集团从数家投资机构融资五百万美元。
二零零零年一月，阿里巴巴集团从软银等数家投资机构融资两千万美元。
二零零零年一月，阿里巴巴集团从软银等数家投资机构融资两千万美元。
二零零零年九月，阿里巴巴集团举办首届西湖论剑，汇聚互联网界的商业和意见领袖讨论业界重要议题。
```

如果“融资”、“互联网”等是业务关键词，可以将含这两个词的句子多复制几遍。

训练流程如下：

1. 选择基础模型：采用通用模型（具体选择何种模型可根据实际场景进行调整）。

2. 训练语料采集：请将如上训练语料保存至训练文本。如果需要自行设置训练语料，请根据标点做裁剪，将每句话保存为训练文本中的一行。

3. 操作训练模型：通过自学习服务提交语料并训练之后，采用训练出的模型，能够有效识别出训练语料中的词汇，获得理想的识别效果。