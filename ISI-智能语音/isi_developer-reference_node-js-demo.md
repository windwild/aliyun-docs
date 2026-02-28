### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition/)[调用示例](https://help.aliyun.com/zh/isi/developer-reference/sample-code/)Node.js Demo

# Node.js Demo

更新时间：2024-04-16 01:51:59

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：.NET Demo](https://help.aliyun.com/zh/isi/developer-reference/net-demo)[下一篇：PHP Demo](https://help.aliyun.com/zh/isi/developer-reference/php-demo)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

示例说明

SDK安装

调用步骤

代码示例

本文介绍如何使用阿里云智能语音服务提供的Node.js SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-2#topic-2572231 "")。

- 已开通智能语音交互并获取AccessKey ID和AccessKey Secret，详情请参见 [从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here "")。


## 示例说明

- 录音文件识别示例使用Node.js SDK提交识别请求和查询识别结果，采用的是RPC风格的POP API调用方式。

- 关于阿里云Node.js SDK请参见 [快速开始](https://help.aliyun.com/document_detail/57342.html#concept-b43-j4j-zdb "")。


## SDK安装

**说明**

阿里云Node.js SDK适用于Node.js 4.x和Node.js 6.x 两个LTS版本。您可以通过执行命令`node -v`查看Node.js版本。

所有阿里云官方的Node.js SDK均位于`@alicloud`下 **。** 录音文件识别的Node.js示例依赖`@alicloud/nls-filetrans-2018-08-17`，在示例文件所在目录，执行如下命令安装Node.js依赖模块：

```javascript
npm install @alicloud/nls-filetrans-2018-08-17 --save
```

## 调用步骤

1. 创建并初始化阿里云鉴权对象。

2. 设置请求参数，提交录音文件识别请求，处理服务端返回的响应并获取任务ID。

3. 设置查询参数为任务ID，轮询该任务的识别结果。


## 代码示例

- [下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)。该录音文件为PCM编码格式16000Hz采样率，管控台设置的模型为通用模型；如果使用其他录音文件，请填入对应的编码格式和采样率，并在管控台设置对应的模型，模型设置请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **ALIYUN\_AK\_ID**、 **ALIYUN\_AK\_SECRET**、 **NLS\_APP\_KEY**。


```javascript
'use strict';
const Client = require('@alicloud/nls-filetrans-2018-08-17');
function fileTrans(akID, akSecret, appKey, fileLink) {
    //地域ID，固定值。
    var ENDPOINT = 'http://filetrans.cn-shanghai.aliyuncs.com';
    var API_VERSION = '2018-08-17';
    /**
     * 创建阿里云鉴权client
     */
    var client = new Client({
        accessKeyId: akID,     //获取AccessKey ID和AccessKey Secret请前往控制台：https://ram.console.aliyun.com/manage/ak
        secretAccessKey: akSecret,
        endpoint: ENDPOINT,
        apiVersion: API_VERSION
    });
    /**
     * 提交录音文件识别请求，请求参数组合成JSON格式的字符串作为task的值。
     * 请求参数appkey：项目appkey，获取Appkey请前往控制台：https://nls-portal.console.aliyun.com/applist
     * 请求参数file_link：需要识别的录音文件。
     */
    var task = {
        appkey : appKey,
        file_link : fileLink,
        version : "4.0",        // 新接入请使用4.0版本，已接入（默认2.0）如需维持现状，请注释掉该参数设置。
        enable_words : false     // 设置是否输出词信息，默认值为false，开启时需要设置version为4.0。
    };
    task = JSON.stringify(task);
    var taskParams = {
        Task : task
    };
    var options = {
            method: 'POST'
        };
    // 提交录音文件识别请求，处理服务端返回的响应。
    client.submitTask(taskParams, options).then((response) => {
        console.log(response);
        // 服务端响应信息的状态描述StatusText。
        var statusText = response.StatusText;
        if (statusText != 'SUCCESS') {
            console.log('录音文件识别请求响应失败!')
            return;
        }
        console.log('录音文件识别请求响应成功!');
        // 获取录音文件识别请求任务的TaskId，以供识别结果查询使用。
        var taskId = response.TaskId;
        /**
         * 以TaskId为查询参数，提交识别结果查询请求。
         * 以轮询的方式进行识别结果的查询，直到服务端返回的状态描述为"SUCCESS"、SUCCESS_WITH_NO_VALID_FRAGMENT，
         * 或者为错误描述，则结束轮询。
        */
        var taskIdParams = {
            TaskId : taskId
        };
        var timer = setInterval(() => {
            client.getTaskResult(taskIdParams).then((response) => {
                console.log('识别结果查询响应：');
                console.log(response);
                var statusText = response.StatusText;
                if (statusText == 'RUNNING' || statusText == 'QUEUEING') {
                    // 继续轮询，注意间隔周期。
                }
                else {
                    if (statusText == 'SUCCESS' || statusText == 'SUCCESS_WITH_NO_VALID_FRAGMENT') {
                        console.log('录音文件识别成功：');
                        var sentences = response.Result;
                        console.log(sentences);
                    }
                    else {
                        console.log('录音文件识别失败!');
                    }
                    // 退出轮询
                    clearInterval(timer);
                }
            }).catch((error) => {
                console.error(error);
                // 异常情况，退出轮询。
                clearInterval(timer);
            });
        }, 10000);
    }).catch((error) => {
        console.error(error);
    });
}
var akId = process.env.ALIYUN_AK_ID;
var akSecret = process.env.ALIYUN_AK_SECRET;
var appKey = process.env.NLS_APP_KEY;
var fileLink = 'https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav';
fileTrans(akId, akSecret, appKey, fileLink);
```