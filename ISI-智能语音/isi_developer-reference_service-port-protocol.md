### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 服务端交互协议

# 服务端交互协议

更新时间：2026-02-26 21:01:56

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

管理链路接口

数据链路接口

鉴权

连接保持

消息简介

请求消息公共Header

异常处理

开始会话

结束会话

服务端下发状态切换事件

请求上传语音

上传语音指令

语音识别结束

指定应答内容

AI语音应答状态

端侧播放事件

文本下发事件

交互流程

服务状态

语音传输

时序图

常见问题


语音对话支持哪些LLM？

是否支持RAG？

本文为您介绍语音对话服务的端口协议详情。

## **管理链路接口**

由于安全原因，AK/SK信息不能直接提供给客户端应用，您可以在服务端通过API获取短时Token（24小时内有效）进行鉴权。数据链路调用只需此Token即可完成用户身份验证。

具体操作，请参见 [使用SDK方式获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token#e4e706203aucr "")。

## **数据链路接口**

服务端与客户端采用双工通讯方式，双方都可以主动给对方发送数据。对应WebSocket协议，文本帧用来发送消息，二进制帧用来发送音频流。

客户端提交的指令为 **Request**，服务端下发的事件为 **Response**。

### **鉴权**

在客户端与服务端进行WebSocket握手时进行鉴权，客户端需要在HTTP请求头中设置X-NLS-Token，值为通过上一步调用POP接口得到的token。

### **连接保持**

服务端为了避免资源浪费，有超时关闭连接的逻辑。当客户端和服务端超过10秒没有消息交互时，会主动关闭连接。客户端如果不想服务端关闭连接，需要定期发送WebSocket ping-pong消息来保活。

示例场景：

- 在等待用户语音输入时，如果用户长时间不说话，可能触发10秒断连。

- 当VoiceChat下发的语音比较长，客户端播放时间可能超过10秒，触发断连。


### **消息简介**

- **类型**

消息分为以下两种类型：
  - 指令：是客户端给服务端发送的消息，表示客户端希望服务端执行某个动作。

  - 事件：是服务端给客户端发送的消息，表示服务端执行某个动作有了结果或有了进展。
- **语音流**

在客户端发送某些指令之后，还需要发送音频数据。例如下文提到的SendSpeech指令。同样，服务端发送某些事件之后也会发送音频数据。

音频数据以流式发送，一个音频流会有多个二进制帧。


### **请求消息公共Header**

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| namespace | String | 是 | 访问的功能，固定为：VoiceChat |
| name | String | 是 | 指令名称，如Start、SendSpeech。 |
| appkey | String | 是 | 语音对话服务接入的key。详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#2572188 "")。 |
| message\_id | String | 是 | 当次消息请求ID，随机生成32位唯一ID。 |

```json
//request Header 示例
{
    "header": {
        "namespace": "VoiceChat",
        "name": "Start",
        "appkey": "appkey",
        "message_id": "d2a2987e2f8a********4ed7464d9593",
        "task_id": "b39398c9dd8147********35cdea81f7"
    }
}
```

### **异常处理**

**Response**

当系统出错无法继续会话时返回TaskFailed，此时 **服务会主动断连**。

客户端需要根据错误信息判断如何处理，也可以使用此dialog\_id重新连接，继续会话。

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| header.status | Int | 是 | 错误码，4开头是客户端错误，5开头是服务端错误。 |
| header.status\_text | String | 是 | 错误消息。 |

### 开始会话

- **Start（Request）**




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 否 | 对话ID，空代表新的对话，传入则代表继续通话。格式为32位随机字符串。 |
| user\_agent | String | 否 | 客户端userAgent，用来记录和鉴权。 |
| dialog\_attributes |  | 是 | AI角色属性。 |
| dialog\_attributes.model\_id | String | 是 | 大模型ID，目前只支持千问（qwen-plus）和通义星尘（xingchen-model）。当指定通义星尘时，需要设置advanced\_attributes.xingchen参数。 |
| dialog\_attributes.promptv | String | 是 | 大模型prompt，最长800个字符。 |
| dialog\_attributes.voice | String | 是 | TTS音色（成品音色，比如 longxiaochun，或者客户克隆voiceName， 补充权限校验）。 |
| dialog\_attributes.voice\_detection\_enabled | String | 否 | 是否开启语音检测，去掉开始和结束的静音，并且当句尾静音长度超过X（服务端控制）的时候认为指令结束。<br>默认为true，push2talk模式可设为false。 |
| advanced\_attributes |  | 否 | 高级属性。 |
| advanced\_attributes.xingchen | String | 否 | model\_id为xingchen-model时，表示调用 [星辰平台](https://xingchen.aliyun.com/xingchen/) 的模型，必传此内容。<br>JSON格式字符串，内容如下：<br>```<br>"{\"character_id\":\"3cdcxxxxxxxxxd020\",\"user_id\":\"876xxxxxxxxx717\"}"<br>```<br>  - character\_id：在星尘平台创建的角色ID，可在角色对话页面查看，例如`https://xingchen.aliyun.com/xingchen/chat?characterId=3cdcxxxxxxxxxd020`。<br>    <br>  - user\_id：星辰平台用来区分不同用户的字符串，可自定义。 |

















```python
//Start请求样例
{
      "header": {
          "namespace": "VoiceChat",
          "name": "Start",
          "appkey": "appkey",
          "message_id": "d2a2987e2f8a********4ed7464d9593",
          "task_id": "b39398c9dd8147********35cdea81f7"
      },
      "payload": {
          "user_agent": "python",
          "device_id": "test_device_id",
          "dialog_attributes": {
              "model_id": "qwen-plus",
              "prompt": "你是一个有用的语音助手",
              "voice": "longxiaochun"
          }
      }
}
```

- **Started（Response）**




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 服务创建的会话ID，后续每个消息都携带此ID。 |

















```python
//Started返回消息样例
{
      "header": {
          "namespace": "VoiceChat",
          "name": "Started",
          "status": 20000000,
          "message_id": "d2a2987e2f8a********4ed7464d9593",
          "task_id": "b39398c9dd8147********35cdea81f7",
          "status_text": "Gateway:SUCCESS:Success."
      },
      "payload": {
          "dialog_id": "83b90a6edfee4ec08b9acede7199cedc"
      }
}
```


### **结束会话**

- **Stop（Request）**















```python
//Stop请求样例
{
      "header": {
          "namespace": "VoiceChat",
          "name": "Stop",
          "appkey": "appkey",
          "message_id": "d2a2987e2f8a********4ed7464d9593",
          "task_id": "b39398c9dd8147********35cdea81f7"
      }
}
```

- **Stopped（Response）**




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |


### **服务端下发状态切换事件**

**DialogStateChanged**

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |
| state | String | 是 | AI交互状态，如：Listening、Thinking、Responding。<br>其中Listening表示SDK可以发语音给服务端，不代表端侧是否开麦。 |

```python
//DialogStateChanged返回样例
{
    "header": {
        "namespace": "VoiceChat",
        "name": "DialogStateChanged",
        "status": 20000000,
        "message_id": "d2a2987e2f8a********4ed7464d9593",
        "task_id": "b39398c9dd8147********35cdea81f7",
        "status_text": "Gateway:SUCCESS:Success."
    },
    "payload": {
        "dialog_id": "83b90a6edf********9acede7199cedc",
        "state": "Listening"
    }
}
```

### **请求上传语音**

- **RequestToSpeak（Request）**

当前状态不是Listening，且用户想说话时，先提交此事件，等待服务端应答。

具体触发此事件的用户行为根据交互类型有所不同，比如用户按下按钮、语音打断（依赖双工模块）等。




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |

















```python
//RequestToSpeak样例
{
      "header": {
          "namespace": "VoiceChat",
          "name": "RequestToSpeak",
          "appkey": "O6HgE6gwqx3nGf8M",
          "message_id": "d2a2987e2f8a********4ed7464d9593",
          "task_id": "b39398c9dd8147********35cdea81f7"
      },
      "payload": {
          "dialog_id": "83b90a6edf********9acede7199cedc"
      }
}
```

- **RequestAccepted（Response）：请求被准许**




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |

















```python
{
      "header": {
          "namespace": "VoiceChat",
          "name": "RequestAccepted",
          "status": 20000000,
          "message_id": "d2a2987e2f8a********4ed7464d9593",
          "task_id": "b39398c9dd8147********35cdea81f7",
          "status_text": "Gateway:SUCCESS:Success."
      },
      "payload": {
          "dialog_id": "83b90a6edf********9acede7199cedc"
      }
}
```


### **上传语音指令**

- **SendSpeech（Request）**

在Listening状态时，通知服务端开始上传语音，语音数据应紧接着此事件之后发送。




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |

















```python
//SendSpeech样例
{
      "header": {
          "namespace": "VoiceChat",
          "name": "SendSpeech",
          "appkey": "O6HgE6gwqx3nGf8M",
          "message_id": "d2a2987e2f8a********4ed7464d9593",
          "task_id": "b39398c9dd8147********35cdea81f7"
      },
      "payload": {
          "dialog_id": "83b90a6edf********9acede7199cedc"
      }
}
```

- **StopSpeech（Request）**

当voice\_detection\_enabled设置为false的时候，用户必须使用StopSpeech结束语音指令输入。




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |

















```python
//StopSpeech样例
{
      "header": {
          "namespace": "VoiceChat",
          "name": "StopSpeech",
          "appkey": "O6HgE6gwqx3nGf8M",
          "message_id": "d2a2987e2f8a********4ed7464d9593",
          "task_id": "b39398c9dd8147********35cdea81f7"
      },
      "payload": {
          "dialog_id": "83b90a6edf********9acede7199cedc"
      }
}
```


### **语音识别结束**

**SpeechEnded（Response）**

当服务端检测到ASR语音尾点时下发此事件，如果客户端还在上传音频，则收到此事件后应停止上传音频。

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |

```python
{
    "header": {
        "namespace": "VoiceChat",
        "name": "SpeechEnded",
        "status": 20000000,
        "message_id": "6281c250f********41426912e2209a3",
        "task_id": "b39398c9dd8147********35cdea81f7",
        "status_text": "Gateway:SUCCESS:Success."
    },
    "payload": {
        "dialog_id": "83b90a6edf********9acede7199cedc"
    }
}
```

### **指定应答内容**

**RequestToRespond（Request）**

在Listening状态时，通知服务端与用户主动交互，可以直接把上传的文本转换为语音下发，也可以上传文本调用大模型，返回的结果再转换为语音下发。

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |
| type | String | 是 | 服务应该采取的交互类型，取值如下：<br>- transcript：表示直接把文本转语音。<br>  <br>- prompt：表示把文本送大模型回答。 |
| text | String | 是 | 要处理的文本。 |

```python
//RequestToRespond请求样例
{
    "header": {
        "namespace": "VoiceChat",
        "name": "RequestToRespond",
        "appkey": "appkey",
        "message_id": "d2a2987e2f8a********4ed7464d9593",
        "task_id": "b39398c9dd8147********35cdea81f7"
    },
    "payload": {
        "dialog_id": "83b90a6edf********9acede7199cedc",
        "type": "prompt",
        "text": "你好，你有什么想聊的呢"
    }
}
```

### **AI语音应答状态**

- **RespondingStarted（Response）**















```python
//RespondingStarted
{
      "header": {
          "namespace": "VoiceChat",
          "name": "RespondingStarted",
          "status": 20000000,
          "message_id": "6281c250f********41426912e2209a3",
          "task_id": "b39398c9dd8147********35cdea81f7",
          "status_text": "Gateway:SUCCESS:Success."
      },
      "payload": {
          "dialog_id": "83b90a6edf********9acede7199cedc"
      }
}
//（以下应答状态雷同，不再赘述）
```



AI语音应答开始，SDK准备接收服务端下发的语音数据。

- **RespondingEnded（Response）**

AI语音应答结束。




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |


### **端侧播放事件**

- **LocalRespondingStarted（Request）：端侧开始播放。**

- **LocalRespondingEnded（Request）：端侧播放结束。**




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |


### **文本下发事件**

- **SpeechContent（Response）**




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |
| text | String | 是 | 用户语音识别出的文本，流式全量输出。 |
| finished | Boolean | 是 | 输出是否结束。 |

















```python
{
      "header": {
          "namespace": "VoiceChat",
          "name": "SpeechContent",
          "status": 20000000,
          "message_id": "c253024********54260fd00d73ad",
          "task_id": "b39398c9dd8147********35cdea81f7",
          "status_text": "Gateway:SUCCESS:Success."
      },
      "payload": {
          "dialog_id": "83b90a6edf********9acede7199cedc",
          "text": "一二三",
          "finished": false
      }
}
```

- **RespondingContent（Response）**




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| dialog\_id | String | 是 | 对话ID。格式为32位随机字符串。 |
| text | String | 是 | 用户语音识别出的文本，流式全量输出。 |
| finished | Boolean | 是 | 输出是否结束。 |

















```python
{
      "header": {
          "namespace": "VoiceChat",
          "name": "RespondingContent",
          "status": 20000000,
          "message_id": "6c85fdaa6********5d4ca81e21949",
          "task_id": "b39398c9dd8147********35cdea81f7",
          "status_text": "Gateway:SUCCESS:Success."
      },
      "payload": {
          "dialog_id": "83b90a6edf********9acede7199cedc",
          "text": "您输入了数字序列“12345”。如果您有关于这些数字的问题或者需要我用它们来完成某项任务，请告诉我更多的细节，我会尽力帮助您。",
          "finished": true
      }
}
```


## **交互流程**

### **服务状态**

会话中服务包括三种状态： **听**（Listening）、 **想**（Thinking）、 **说**（Responding），通过DialogStateChanged消息下发通知客户端。

只有在 **听** 的状态用户可以说话，其他状态如果要打断服务处理，可以上传RequestToSpeek指令，服务收到请求会切换状态到 **听**。

### **语音传输**

- 上传语音：在 **听** 的状态下，用户可以说话，方法是先上传SendSpeech指令，然后即可发送音频数据。

音频数据格式为单通道PCM，采样率为16000Hz。

- 下发语音：服务下发语音前会先下发RespondingStarted事件，然后下发音频数据，最后会下发RespondingEnded事件表示音频发送完成。

音频格式为单通道PCM，采样率为24000Hz。


### **时序图**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5177512771/CAEQUBiBgIC_7r7PlBkiIDJhM2NkYjQyNDA5YzQyYzI5Y2U4ZWM5ZmMwN2ZhMzcz4705034_20241012144303.065.svg)

## **常见问题**

### **语音对话支持哪些LLM？**

目前只支持千问大模型（包括Qwen\_turbo、Qwen\_plus等），不支持替换其他大模型。千问大模型支持列表，详情请参见 [千问大语言模型介绍](https://help.aliyun.com/zh/model-studio/what-is-qwen-llm "")。

### **是否支持RAG？**

支持。如果您有业务需求，请 [提交工单](https://smartservice.console.aliyun.com/service/create-ticket) 进行咨询。