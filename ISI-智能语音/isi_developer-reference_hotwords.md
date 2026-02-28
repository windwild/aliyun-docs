### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[自学习平台](https://help.aliyun.com/zh/isi/developer-reference/customization-platform/)热词

# 热词

更新时间：2024-12-02 00:56:10

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：最佳实践](https://help.aliyun.com/zh/isi/developer-reference/best-practices)[下一篇：在控制台创建热词](https://help.aliyun.com/zh/isi/developer-reference/create-hotwords)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

创建热词方式

应用举例

热词通常是指对在特定业务领域需要优先准确识别的关键词或短语。如果您的业务领域有部分词汇识别效果不够好，可以考虑使用热词功能，将这些词添加到热词词表从而改善识别结果。

## **创建热词方式**

您可以通过 [在控制台创建热词](https://help.aliyun.com/zh/isi/developer-reference/create-hotwords "") 或 [使用POP API创建业务专属热词](https://help.aliyun.com/zh/isi/developer-reference/call-the-pop-api-to-manage-business-specific-hotwords "") 方式创建热词。具体区别如下：

- 在控制台上配置项目热词与项目Appkey绑定，无需在代码中指定热词表；POP API仅支持创建 **业务专属** 热词表，需要您在客户端代码中调用SDK接口设置业务专属热词表ID，该热词表才能生效。

- 在控制台上配置项目热词时，每个热词占一行，无需设置热词权重；使用POP API创建 **业务专属** 热词表，需要指定每个热词的权重。


## 应用举例

为了提高电影名称识别率，将如下电影名称作为热词添加到项目中。

```javascript
肖申克的救赎
霸王别姬
这个杀手不太冷
阿甘正传
美丽人生
泰坦尼克号
千与千寻
辛德勒的名单
盗梦空间
机器人总动员
忠犬八公的故事
三傻大闹宝莱坞
海上钢琴师
放牛班的春天
楚门的世界
教父
龙猫
星际穿越
```