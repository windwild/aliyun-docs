### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音分析](https://help.aliyun.com/zh/isi/developer-reference/speech-analysis/)[说话人识别](https://help.aliyun.com/zh/isi/developer-reference/speaker-recognition/)Java SDK

# Java SDK

更新时间：2025-01-23 22:55:43

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-4)[下一篇：接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-5)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

下载安装

关键接口

示例代码

本文介绍如何使用阿里云智能语音服务提供的Java SDK，包括SDK的安装方法及SDK代码示例。

## 注意事项

在使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-4#topic-2211155 "")。

## 下载安装

从Maven服务器下载最新版本SDK。您可以下载包含集成SDK的完整示例，无需从零构建项目即可体验说话人识别功能： [nls-common-sdk-demos](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20240424/alzyzm/nls-common-sdk-demos.zip)。

```javascript
<dependency>
    <groupId>com.alibaba.nls</groupId>
    <artifactId>nls-sdk-common</artifactId>
    <version>2.2.1</version>
</dependency>
<dependency>
    <groupId>com.alibaba.nls</groupId>
    <artifactId>nls-sdk-request</artifactId>
    <version>2.2.1</version>
</dependency>
```

## 关键接口

- NlsClient：语音处理客户端，利用该客户端可以处理语音任务。该客户端为线程安全，建议全局仅创建一个实例。

- CommonRequest：通用请求类，通过该接口设置请求参数，发送请求及声音数据。非线程安全。

- CommonRequestListener：通用结果监听类，监听识别结果。非线程安全。



**说明**





SDK调用注意事项：



  - NlsClient使用了Netty框架，NlsClient对象的创建会消耗一定时间和资源，一经创建可以重复使用。建议调用程序将NlsClient的创建和关闭与程序本身的生命周期相结合。

  - CommonRequest对象不可重复使用，一个任务对应一个CommonRequest对象。例如，N个音频文件要进行N次任务，创建N个CommonRequest对象。

  - CommonRequestListener对象和CommonRequest对象是一一对应的，不能在不同CommonRequest对象使用同一个CommonRequestListener对象，否则不能将各任务区分开。

  - Java SDK依赖Netty网络库，如果您的应用依赖Netty，其版本需更新至4.1.17.Final及以上。


## 示例代码

```java
package com.alibaba.nls.demo;

import com.alibaba.nls.client.protocol.NlsClient;
import com.alibaba.nls.client.protocol.commonrequest.CommonRequest;
import com.alibaba.nls.client.protocol.commonrequest.CommonRequestListener;
import com.alibaba.nls.client.protocol.commonrequest.CommonRequestResponse;

public class VprloginApplyDigitDemo {

    private static CommonRequestListener getListener() {
        CommonRequestListener listener = new CommonRequestListener() {
            @Override
            public void onStarted(CommonRequestResponse response) {
                System.out.println(
                    "onStarted, taskId: " + response.getTaskId() + ", header: " + response.header + ", payload: "
                        + response.payload);
            }

            @Override
            public void onEvent(CommonRequestResponse response) {
                System.out.println(
                    "onEvent, taskId: " + response.getTaskId() + ", header: " + response.header + ", payload: "
                        + response.payload);
            }

            @Override
            public void onStopped(CommonRequestResponse response) {
                System.out.println(
                    "onStopped, taskId: " + response.getTaskId() + ", header: " + response.header + ", payload: "
                        + response.payload);
            }

            @Override
            public void onFailed(CommonRequestResponse response) {
                System.out.println(
                    "onFailed, taskId: " + response.getTaskId() + ", header: " + response.header + ", payload: "
                        + response.payload);
            }
        };
        return listener;
    }

    public static void main(String[] args) {
        String appkey = "";
        String token = "";

        NlsClient client = new NlsClient(token);
        try {
            CommonRequestListener listener = getListener();
            CommonRequest commonRequest = new CommonRequest(client, listener, "SpeakerVerification");
            commonRequest.setAppKey(appkey);
            commonRequest.addCustomedParam("action", "ApplyDigit");
            commonRequest.addCustomedParam("speaker_id", "test_speaker");

            commonRequest.start();
            commonRequest.stop();
            commonRequest.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        client.shutdown();
    }
}
```