### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 运行SDK

# 运行SDK

更新时间：2022-09-08 07:44:01

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

调用语音识别服务

后续步骤

本文介绍如何使用SDK调用语音交互服务。

## 前提条件

- 创建阿里云账号，开通智能语音交互服务权限，并取得账号对应的AccessKey ID和AccessKey Secret，详情请参见 [开通服务](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-2572187 "")。

- 在智能语音交互管理控制台创建项目，获得项目appkey，详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#topic-2572188 "")。


## 调用语音识别服务

以Java SDK为例，为您介绍调用语音交互服务的操作步骤。

1. 安装 [Maven工具](https://maven.apache.org/)。

2. [下载SDK包](https://gw.alipayobjects.com/os/bmw-prod/f0ba9e30-861a-462e-ab0d-c593988b49aa.zip) 并解压。

3. 运行代码调用语音交互服务。


   - 调用一句话识别示例。

     示例文件解压后，在pom目录运行`mvn package`，在target目录将生成可执行JAR：nls-example-recognizer-2.0.0-jar-with-dependencies.jar，将此JAR文件拷贝至目标服务器，运行如下代码段，将在JAR包同目录生成logs/nls.log。















     ```java
     参见：java -cp nls-example-recognizer-2.0.0-jar-with-dependencies.jar com.alibaba.nls.client.SpeechRecognizerDemo <app-key> <token> [<url>]      //获取Token具体操作，请参见：https://help.aliyun.com/document_detail/450514.html
     ```

   - 调用实时语音识别示例。

     示例文件解压后，在pom目录运行`mvn package`，在target目录将生成可执行JAR：nls-example-transcriber-2.0.0-jar-with-dependencies.jar，将此JAR文件拷贝至目标服务器，运行如下代码段，将在JAR包同目录生成logs/nls.log。















     ```java
     java -cp nls-example-transcriber-2.0.0-jar-with-dependencies.jar com.alibaba.nls.client.SpeechTranscriberDemo <app-key> <token> [<url>]      //获取Token具体操作，请参见：https://help.aliyun.com/document_detail/450514.html
     ```

   - 调用语音合成示例。

     示例文件解压后，在pom目录运行`mvn package`，在target目录将生成可执行JAR：nls-example-tts-2.0.0-jar-with-dependencies.jar，将此JAR拷贝至目标服务器，运行如下代码段，将在JAR包同目录生成logs/nls.log。















     ```java
     java -cp nls-example-tts-2.0.0-jar-with-dependencies.jar com.alibaba.nls.client.SpeechSynthesizerDemo  <app-key> <token> [<url>]      //获取Token具体操作，请参见：https://help.aliyun.com/document_detail/450514.html
     ```


## 后续步骤

- 阅读SDK包中的示例代码，了解SDK调用流程。

- 了解智能语音交互服务相关术语，帮助您更好地理解产品，详情请参见 [基本概念](https://help.aliyun.com/zh/isi/product-overview/concepts#topic-2572192 "")。

- 学习如何调用智能语音交互服务，详情请参见 [使用前须知](https://help.aliyun.com/zh/isi/before-you-begin#2572191 "")。