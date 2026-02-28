### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition/)[调用示例](https://help.aliyun.com/zh/isi/developer-reference/sample-code/)PHP Demo

# PHP Demo

更新时间：2024-04-16 01:52:01

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Node.js Demo](https://help.aliyun.com/zh/isi/developer-reference/node-js-demo)[下一篇：Python Demo](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-python-3)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

SDK说明

安装PHP SDK

调用步骤

代码示例

本文介绍如何使用阿里云智能语音服务提供的PHP SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-2#topic-2572231 "")。

- 已开通智能语音交互并获取AccessKey ID和AccessKey Secret，详情请参见 [从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here "")。


**说明**

- 本文PHP示例基于阿里云新版PHP SDK（ [Alibaba Cloud SDK for PHP](https://github.com/aliyun/openapi-sdk-php)）开发。如果您已接入阿里云旧版PHP SDK（ [aliyun-openapi-php-sdk](https://github.com/aliyun/aliyun-openapi-php-sdk.git)），仍然可以继续使用或者更新到新版SDK（推荐）。

- 后续录音文件识别的PHP示例更新将基于新版PHP SDK。


## SDK说明

- 录音文件识别的PHP示例使用了阿里云的PHP SDK提交录音文件识别请求和查询识别结果，采用RPC风格的POP API调用方式。

- 关于阿里云PHP SDK的详细介绍，请参见 [PHP SDK](https://help.aliyun.com/document_detail/53111.html#concept-b43-j4j-zdb "")。


**重要**

阿里云PHP SDK适用于PHP的5.5.0或更高版本 **。**

## 安装PHP SDK

阅读PHP SDK的安装方式，详情请参见 [安装Alibaba Cloud SDK for PHP](https://github.com/aliyun/openapi-sdk-php/blob/master/docs/zh-CN/1-Installation.md)。

## 调用步骤

1. 创建一个全局客户端。

2. 设置请求参数，提交录音文件识别请求；处理服务端返回的响应，获取任务ID，用于后续的识别结果轮询。

3. 根据任务ID，轮询识别结果。


## 代码示例

- [下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)。该录音文件为PCM编码格式16000Hz采样率，管控台设置的模型为通用模型；如果使用其他录音文件，请填入对应的编码格式和采样率，并在管控台设置对应的模型，模型设置请参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **ALIYUN\_AK\_ID**、 **ALIYUN\_AK\_SECRET**、 **NLS\_APP\_KEY**。


```javascript
<?php
require __DIR__ . '/vendor/autoload.php';
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;
class NLSFileTrans {
    // 请求参数
    private const KEY_APP_KEY = "appkey";
    private const KEY_FILE_LINK = "file_link";
    private const KEY_VERSION = "version";
    private const KEY_ENABLE_WORDS = "enable_words";
    // 响应参数
    private const KEY_TASK_ID = "TaskId";
    private const KEY_STATUS_TEXT = "StatusText";
    private const KEY_RESULT = "Result";
    // 状态值
    private const STATUS_SUCCESS = "SUCCESS";
    private const STATUS_RUNNING = "RUNNING";
    private const STATUS_QUEUEING = "QUEUEING";
    function submitFileTransRequest($appKey, $fileLink) {
        // 获取task JSON字符串，包含appkey和file_link参数等。
        // 新接入请使用4.0版本，已接入（默认2.0）如需维持现状，请注释掉该参数设置。
        // 设置是否输出词信息，默认为false，开启时需要设置version为4.0。
        $taskArr = array(self::KEY_APP_KEY => $appKey, self::KEY_FILE_LINK => $fileLink, self::KEY_VERSION => "4.0", self::KEY_ENABLE_WORDS => FALSE);
        $task = json_encode($taskArr);
        print $task . "\n";
        try {
            // 提交请求，返回服务端的响应。
            $submitTaskResponse = AlibabaCloud::nlsFiletrans()
                                              ->v20180817()
                                              ->submitTask()
                                              ->withTask($task)
                                              ->request();
            print $submitTaskResponse . "\n";
            // 获取录音文件识别请求任务的ID，以供识别结果查询使用。
            $taskId = NULL;
            $statusText = $submitTaskResponse[self::KEY_STATUS_TEXT];
            if (strcmp(self::STATUS_SUCCESS, $statusText) == 0) {
                $taskId = $submitTaskResponse[self::KEY_TASK_ID];
            }
            return $taskId;
        } catch (ClientException $exception) {
            // 获取错误消息
            print_r($exception->getErrorMessage());
        } catch (ServerException $exception) {
            // 获取错误消息
            print_r($exception->getErrorMessage());
        }
    }
    function getFileTransResult($taskId) {
        $result = NULL;
        while (TRUE) {
            try {
                $getResultResponse = AlibabaCloud::nlsFiletrans()
                                                 ->v20180817()
                                                 ->getTaskResult()
                                                 ->withTaskId($taskId)
                                                 ->request();
                print "识别查询结果: " . $getResultResponse . "\n";
                $statusText = $getResultResponse[self::KEY_STATUS_TEXT];
                if (strcmp(self::STATUS_RUNNING, $statusText) == 0 || strcmp(self::STATUS_QUEUEING, $statusText) == 0) {
                    // 继续轮询
                    sleep(10);
                }
                else {
                    if (strcmp(self::STATUS_SUCCESS, $statusText) == 0) {
                        $result = $getResultResponse;
                    }
                    // 退出轮询
                    break;
                }
            } catch (ClientException $exception) {
                // 获取错误消息
                print_r($exception->getErrorMessage());
            } catch (ServerException $exception) {
                // 获取错误消息
                print_r($exception->getErrorMessage());
            }
        }
        return $result;
    }
}
$accessKeyId = getenv('ALIYUN_AK_ID');
$accessKeySecret = getenv('ALIYUN_AK_SECRET');
$appKey = getenv('NLS_APP_KEY');
$fileLink = "https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav";
/**
  * 第一步：设置一个全局客户端。
  * 使用阿里云RAM账号的AccessKey ID和AccessKey Secret进行鉴权。
 */
AlibabaCloud::accessKeyClient($accessKeyId, $accessKeySecret)
            ->regionId("cn-shanghai")
            ->asGlobalClient();
$fileTrans = new NLSFileTrans();
/**
  *  第二步：提交录音文件识别请求，获取任务ID，用于后续的识别结果轮询。
 */
$taskId = $fileTrans->submitFileTransRequest($appKey, $fileLink);
if ($taskId != NULL) {
    print "录音文件识别请求成功，task_id: " . $taskId . "\n";
}
else {
    print "录音文件识别请求失败!";
    return ;
}
/**
  * 第三步：根据任务ID轮询识别结果。
 */
$result = $fileTrans->getFileTransResult($taskId);
if ($result != NULL) {
    print "录音文件识别结果查询成功: " . $result . "\n";
}
else {
    print "录音文件识别结果查询失败!";
}
```