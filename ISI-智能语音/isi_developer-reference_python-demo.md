### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[录音文件识别闲时版](https://help.aliyun.com/zh/isi/developer-reference/recording-file-recognition-off-peak-edition/)[调用示例](https://help.aliyun.com/zh/isi/developer-reference/sample-code-1/)Python Demo

# Python Demo

更新时间：2024-04-16 01:49:53

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PHP Demo](https://help.aliyun.com/zh/isi/developer-reference/php-demo-1)[下一篇：快速开始](https://help.aliyun.com/zh/isi/developer-reference/quick-start)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

SDK说明

SDK安装

调用步骤

示例代码

本文介绍如何使用阿里云智能语音服务提供的Python SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference#topic-2170103 "")。

- 已开通智能语音交互并获取AccessKey ID和AccessKey Secret，详情请参见 [从这里开始](https://help.aliyun.com/zh/isi/getting-started/start-here "")。


## SDK说明

- 录音文件识别的Python示例使用了阿里云Python SDK的CommonRequest提交录音文件识别请求和查询识别结果，采用RPC风格的POP API调用方式。

- 关于使用阿里云Python SDK请参见 [使用Python SDK](https://help.aliyun.com/document_detail/67117.html#concept-mkk-vpj-zdb "")。

- 关于Python SDK CommonRequest的使用方法请参见 [使用CommonRequest进行调用](https://help.aliyun.com/document_detail/61476.html#concept-ivk-p1k-zdb "")。


## SDK安装

运行录音文件识别Python示例，只需安装阿里云Python SDK的核心库。

阿里云Python SDK支持Python版本如下，并提供pip和GitHub两种安装方式。

- Python 2.6及以上

- Python 2.7及以上

- Python 3及以上


使用pip安装（推荐）：执行如下命令，通过pip安装Python SDK，版本为2.13.3。

```python
pip install aliyun-python-sdk-core==2.13.3
```

## 调用步骤

1. 创建并初始化AcsClient实例。

2. 创建录音文件识别请求，设置请求参数。

3. 提交录音文件识别请求，处理服务端返回的响应，获取任务ID。

4. 创建识别结果查询请求，设置查询参数为任务ID。

5. 轮询识别结果。


## 示例代码

- [下载nls-sample-16k.wav](https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav)。示例中使用的录音文件为PCM编码格式16000 Hz采样率，管控台设置的模型为通用模型；如果使用其他录音文件，请填入对应的编码格式和采样率，并在管控台设置对应的模型，关于模型设置参见 [管理项目](https://help.aliyun.com/zh/isi/getting-started/manage-projects#topic-2572199 "")。

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **ALIYUN\_AK\_ID**、 **ALIYUN\_AK\_SECRET**、 **NLS\_APP\_KEY**。


```python
# -*- coding: utf8 -*-
import json
import time
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.request import CommonRequest
def fileTrans(akId, akSecret, appKey, fileLink) :
    # 地域ID，固定值。
    REGION_ID = "cn-shanghai"
    PRODUCT = "SpeechFileTranscriberLite"
    DOMAIN = "speechfiletranscriberlite.cn-shanghai.aliyuncs.com"
    API_VERSION = "2021-12-21"
    POST_REQUEST_ACTION = "SubmitTask"
    GET_REQUEST_ACTION = "GetTaskResult"
    # 请求参数
    KEY_APP_KEY = "appkey"
    KEY_FILE_LINK = "file_link"
    KEY_VERSION = "version"
    KEY_ENABLE_WORDS = "enable_words"
    # 是否开启智能分轨
    KEY_AUTO_SPLIT = "auto_split"
    # 响应参数
    KEY_TASK = "Task"
    KEY_TASK_ID = "TaskId"
    KEY_STATUS_TEXT = "StatusText"
    KEY_RESULT = "Result"
    # 状态值
    STATUS_SUCCESS = "SUCCESS"
    STATUS_RUNNING = "RUNNING"
    STATUS_QUEUEING = "QUEUEING"
    # 创建AcsClient实例
    client = AcsClient(akId, akSecret, REGION_ID)
    # 提交录音文件识别请求
    postRequest = CommonRequest()
    postRequest.set_domain(DOMAIN)
    postRequest.set_version(API_VERSION)
    postRequest.set_product(PRODUCT)
    postRequest.set_action_name(POST_REQUEST_ACTION)
    postRequest.set_method('POST')
    task = {KEY_APP_KEY : appKey, KEY_FILE_LINK : fileLink, KEY_ENABLE_WORDS : False}
    # 开启智能分轨，如果开启智能分轨，task中设置KEY_AUTO_SPLIT为True。
    # task = {KEY_APP_KEY : appKey, KEY_FILE_LINK : fileLink, KEY_ENABLE_WORDS : False, KEY_AUTO_SPLIT : True}
    task = json.dumps(task)
    print(task)
    postRequest.add_body_params(KEY_TASK, task)
    taskId = ""
    try :
        postResponse = client.do_action_with_exception(postRequest)
        postResponse = json.loads(postResponse)
        print (postResponse)
        statusText = postResponse[KEY_STATUS_TEXT]
        if statusText == STATUS_SUCCESS :
            print ("录音文件识别请求成功响应！")
            taskId = postResponse[KEY_TASK_ID]
        else :
            print ("录音文件识别请求失败！")
            return
    except ServerException as e:
        print (e)
    except ClientException as e:
        print (e)
    # 创建CommonRequest，设置任务ID。
    getRequest = CommonRequest()
    getRequest.set_domain(DOMAIN)
    getRequest.set_version(API_VERSION)
    getRequest.set_product(PRODUCT)
    getRequest.set_action_name(GET_REQUEST_ACTION)
    getRequest.set_method('GET')
    getRequest.add_query_param(KEY_TASK_ID, taskId)
    # 提交录音文件识别结果查询请求
    # 以轮询的方式进行识别结果的查询，直到服务端返回的状态描述符为"SUCCESS"、"SUCCESS_WITH_NO_VALID_FRAGMENT"，
    # 或者为错误描述，则结束轮询。
    statusText = ""
    while True :
        try :
            getResponse = client.do_action_with_exception(getRequest)
            getResponse = json.loads(getResponse)
            print (getResponse)
            statusText = getResponse[KEY_STATUS_TEXT]
            if statusText == STATUS_RUNNING or statusText == STATUS_QUEUEING :
                # 继续轮询
                time.sleep(10)
            else :
                # 退出轮询
                break
        except ServerException as e:
            print (e)
        except ClientException as e:
            print (e)
    if statusText == STATUS_SUCCESS :
        print ("录音文件识别成功！")
    else :
        print ("录音文件识别失败！")
    return
accessKeyId = os.getenv('ALIYUN_AK_ID')
accessKeySecret = os.getenv('ALIYUN_AK_SECRET')
appKey = os.getenv('NLS_APP_KEY')
fileLink = "https://gw.alipayobjects.com/os/bmw-prod/0574ee2e-f494-45a5-820f-63aee583045a.wav"
# 执行录音文件识别
fileTrans(accessKeyId, accessKeySecret, appKey, fileLink)
```