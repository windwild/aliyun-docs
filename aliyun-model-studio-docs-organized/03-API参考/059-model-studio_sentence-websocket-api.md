### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音识别](https://help.aliyun.com/zh/model-studio/speech-recognition-api-reference/)[实时短语音识别（Gummy）](https://help.aliyun.com/zh/model-studio/sentence-recognition-and-translation-api-reference/)WebSocket API

# Gummy一句话识别、翻译WebSocket API

更新时间：2026-02-11 02:28:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Python SDK](https://help.aliyun.com/zh/model-studio/sentence-python-sdk)[下一篇：Android SDK](https://help.aliyun.com/zh/model-studio/sentence-android-sdk)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型与价格

前提条件

客户端与服务端的交互流程

WebSocket客户端编程与消息处理

一、建立WebSocket连接

二、异步监听服务器返回的消息

三、给服务器发送消息

四、关闭WebSocket连接

关于建连开销和连接复用

示例代码

错误码

常见问题

功能特性

故障排查

更多问题

本文介绍如何通过WebSocket连接访问Gummy一句话识别、翻译服务。

DashScope SDK目前仅支持Java和Python。若想使用其他编程语言开发Gummy实时语音识别、翻译应用程序，可以通过WebSocket连接与服务进行通信。

**用户指南：** 关于模型介绍和选型建议请参见 [实时语音识别-Fun-ASR/Gummy/Paraformer](https://help.aliyun.com/zh/model-studio/real-time-speech-recognition "") 和 [实时语音翻译-Gummy](https://help.aliyun.com/zh/model-studio/real-time-speech-translation "")。

**在线体验**： [模型体验](https://bailian.console.aliyun.com/#/efm/model_experience_center/voice?currentTab=voiceTts)

WebSocket是一种支持全双工通信的网络协议。客户端和服务器通过一次握手建立持久连接，双方可以互相主动推送数据，因此在实时性和效率方面具有显著优势。

对于常用编程语言，有许多现成的WebSocket库和示例可供参考，例如：

- Go：`gorilla/websocket`

- PHP：`Ratchet`

- Node.js：`ws`


建议您先了解WebSocket的基本原理和技术细节，再参照本文进行开发。

**说明**

- 音频时长不能超过一分钟，否则将报错断连。

- 一句话的结束，通过静音时长来判断，当语音后面出现的静音时长超过预设的静音时长（默认为700ms，可在 [发送run-task指令](https://help.aliyun.com/zh/model-studio/sentence-websocket-api#a4566139berwo "") 时通过请求参数`max_end_silence`设置），系统会认为当前的一句话已结束。如果语音时长超过了一分钟，则认为这一分钟内的语音是一句话。


## **模型与价格**

| **模型名** | **模型简介** | **单价** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名** | **模型简介** | **单价** |
| gummy-chat-v1 | Gummy一句话识别、翻译模型，在识别、翻译出一句话后会结束任务。默认进行标点符号预测和逆文本正则化（INT，Inverse Text Normalization）。支持 [定制热词](https://help.aliyun.com/zh/model-studio/custom-hot-words-for-gummy "")。 | 0.00015元/秒<br>**重要**<br>语音识别与翻译功能分别计费，费用按各自调用量独立计算。两项服务的单价一致。 |

## **前提条件**

已开通服务并获得API-KEY： [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。建议您 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")，从而避免在代码里显式配置API Key，降低泄漏风险。

## **客户端与服务端的交互流程**

按时间顺序，客户端与服务端的交互流程如下：

1. 建立连接：客户端与服务端建立WebSocket连接。

2. 开启任务：

   - 客户端发送`run-task`指令以开启任务。

   - 客户端收到服务端返回的`task-started`事件，标志着任务已成功开启，可以进行后续步骤。
3. 发送音频流：

   - 客户端开始发送音频流，并同时接收服务端持续返回的`result-generated`事件，该事件包含语音识别结果。
4. 通知服务端结束任务：

   - 客户端发送`finish-task`指令通知服务端结束任务，并继续接收服务端返回的`result-generated`事件。
5. 任务结束：

   - 客户端收到服务端返回的`task-finished`事件，标志着任务结束。
6. 关闭连接：客户端关闭WebSocket连接。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2394970771/CAEQURiBgMCczta5pxkiIGY0N2Q2YjIwZTM1MTQyNTY4ZmFkY2MwN2JmOTllODFl4709861_20241015153444.149.svg)

## WebSocket客户端编程与消息处理

在编写WebSocket客户端代码时，为了同时发送和接收消息，通常采用异步编程。您可以按照以下步骤来编写程序：

1. 建立WebSocket连接：首先，初始化并建立与服务器的WebSocket连接。

2. 异步监听服务器消息：启动一个单独的线程（具体实现方式因编程语言而异）来监听服务器返回的消息，根据消息内容进行相应的操作。

3. 发送消息：在不同于监听服务器消息的线程中（例如主线程，具体实现方式因编程语言而异），向服务器发送消息。

4. 关闭连接：在程序结束前，确保关闭WebSocket连接以释放资源。


当然，编程思路不止这一种，您或许有更好的想法。本文主要介绍通过WebSocket连接访问服务时的鉴权细节及客户端与服务端之间的消息交互。由于篇幅有限，其他思路将不再赘述。

接下来将按照上述思路，为您详细说明。

### **一、建立WebSocket连接**

调用WebSocket库函数（具体实现方式因编程语言或库函数而异），将请求头和URL传入以建立WebSocket连接。

请求头中需添加如下鉴权信息：

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| Authorization | string | 是 | 鉴权令牌，格式为`Bearer <your_api_key>`，使用时，将“`<your_api_key>`”替换为实际的API Key。 |
| user-agent | string | 否 | 客户端标识，便于服务端追踪来源。 |
| X-DashScope-WorkSpace | string | 否 | 阿里云百炼 [业务空间ID](https://help.aliyun.com/zh/model-studio/use-workspace#c5222ec081sbo "")。 |
| X-DashScope-DataInspection | string | 否 | 是否启用数据合规检测功能。默认不传或设为`enable`。如非必要，请勿启用该参数。 |

WebSocket URL固定如下：

```http
wss://dashscope.aliyuncs.com/api-ws/v1/inference
```

### **二、异步监听服务器返回的消息**

如上所述，您可以启动一个线程（具体实现因编程语言而异）来监听服务器返回的消息。WebSocket库通常会提供回调函数（观察者模式）来处理这些消息。您可以在回调函数中根据不同的消息类型实现相应的功能。

服务端返回给客户端的消息叫做事件，事件代表不同的处理阶段，为JSON格式，由`header`和`payload`这两部分组成：

- `header`：包含基础信息，格式较为统一。






除`task-failed`外，所有事件的`header`格式统一。



`header`示例：

















```json
{
      "header": {
          "task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx",
          "event": "task-started",
          "attributes": {}
      }
}
```





`header`参数：



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| header | object | 请求头 |
| header.event | string | 事件类型<br>  - task-started<br>    <br>  - result-generated<br>    <br>  - task-finished<br>    <br>  - task-failed<br>    <br>详细说明参见下文。 |
| header.task\_id | string | 客户端生成的task\_id |

- `payload`：包含基础信息外的其他信息。不同事件的`payload`格式可能不同。


共有如下四种事件：

##### 1、task-started事件：语音识别任务已开启

当监听到服务端返回的`task-started`事件时，标志着任务已成功开启。只有在接收到该事件后，才能向服务器发送待识别音频或`finish-task`指令；否则，任务将执行失败。

`task-started`事件的`payload`没有内容。

示例：

```json
{
    "header": {
        "task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx",
        "event": "task-started",
        "attributes": {}
    },
    "payload": {}
}
```

##### 2、result-generated事件：包含语音识别响应结果

客户端发送待识别音频和`finish-task`指令的同时，服务端持续返回`result-generated`事件，该事件包含语音识别的结果。

可以通过`result-generated`事件中的`sentence_end`是否为True来判断该结果是中间结果还是最终结果。

示例：

```json
{
	"header": {
		"task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx",
		"event": "result-generated",
		"attributes": {}
	},
	"payload": {
		"output": {
			"translations": [{\
				"sentence_id": 0,\
				"begin_time": 100,\
				"end_time": 2720,\
				"text": "This is a text used for testing.",\
				"lang": "en",\
				"words": [{\
						"begin_time": 100,\
						"end_time": 427,\
						"text": "This"\
					},\
					{\
						"begin_time": 427,\
						"end_time": 755,\
						"text": " is"\
					},\
					{\
						"begin_time": 755,\
						"end_time": 1082,\
						"text": " a"\
					},\
					{\
						"begin_time": 1082,\
						"end_time": 1410,\
						"text": " text"\
					},\
					{\
						"begin_time": 1410,\
						"end_time": 1737,\
						"text": " used"\
					},\
					{\
						"begin_time": 1737,\
						"end_time": 2065,\
						"text": " for"\
					},\
					{\
						"begin_time": 2065,\
						"end_time": 2392,\
						"text": " testing"\
					},\
					{\
						"begin_time": 2392,\
						"end_time": 2720,\
						"text": "."\
					}\
				],\
				"sentence_end": true\
			}],
			"transcription": {
				"sentence_id": 0,
				"begin_time": 100,
				"end_time": 2720,
				"text": "这是一句用来测试的文本。",
				"words": [{\
						"begin_time": 100,\
						"end_time": 427,\
						"text": "这"\
					},\
					{\
						"begin_time": 427,\
						"end_time": 755,\
						"text": "是一"\
					},\
					{\
						"begin_time": 755,\
						"end_time": 1082,\
						"text": "句"\
					},\
					{\
						"begin_time": 1082,\
						"end_time": 1410,\
						"text": "用来"\
					},\
					{\
						"begin_time": 1410,\
						"end_time": 1737,\
						"text": "测试"\
					},\
					{\
						"begin_time": 1737,\
						"end_time": 2065,\
						"text": "的"\
					},\
					{\
						"begin_time": 2065,\
						"end_time": 2392,\
						"text": "文本"\
					},\
					{\
						"begin_time": 2392,\
						"end_time": 2720,\
						"text": "。"\
					}\
				],
				"sentence_end": true
			}
		}
	}
}
```

**重要**

当sentence\_end=false时，为中间结果，在中间结果中，不保证识别和翻译进度同步，需要等待一句话结束（sentence\_end=true）时同步。

`payload`参数说明：

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| output | object | output.translations为翻译结果，output.transcription为识别结果，详细内容见下文。 |

`payload.output.transcription`格式如下：

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| sentence\_id | integer | 句子ID。 |
| begin\_time | integer | 句子开始时间，单位为ms。 |
| end\_time | integer | 句子结束时间，单位为ms。 |
| text | string | 识别文本。 |
| words | array\[Word\] | 字时间戳信息。 |
| sentence\_end | boolean | 当前文本是否构成完整的句子。<br>- true：当前文本构成完整句子，识别结果为最终结果。<br>  <br>- false：当前文本未构成完整句子，识别结果可能会更新。 |

`payload.output.translations`的值为数组，代表不同翻译目标语言对应的结果。数组元素格式如下：

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| sentence\_id | integer | 句子ID。 |
| lang | string | 翻译语种。 |
| begin\_time | integer | 句子开始时间，单位为ms。 |
| end\_time | integer | 句子结束时间，单位为ms。 |
| text | string | 识别文本。 |
| words | array\[Word\] | 字时间戳信息。 |
| sentence\_end | boolean | 当前文本是否构成完整的句子。<br>- true：当前文本构成完整句子，翻译结果为最终结果。<br>  <br>- false：当前文本未构成完整句子，翻译结果可能会更新。 |

`transcription`或`translations`中的`words`为字时间戳信息，其中每一个word格式如下：

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| begin\_time | integer | 字开始时间，单位为ms。 |
| end\_time | integer | 字结束时间，单位为ms。 |
| text | string | 字。 |

##### 3、task-finished事件：语音识别任务已结束

当监听到服务端返回的`task-finished`事件时，说明任务已结束。此时可以关闭WebSocket连接并结束程序。

示例：

```json
{
    "header": {
        "task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx",
        "event": "task-finished",
        "attributes": {}
    },
    "payload": {
        "output": {},
        "usage": null
    }
}
```

##### 4、task-failed事件：任务失败

如果接收到`task-failed`事件，表示任务失败。此时需要关闭WebSocket连接并处理错误。通过分析报错信息，如果是由于编程问题导致的任务失败，您可以调整代码进行修正。

示例：

```json
{
    "header": {
        "task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx",
        "event": "task-failed",
        "error_code": "CLIENT_ERROR",
        "error_message": "request timeout after 23 seconds.",
        "attributes": {}
    },
    "payload": {}
}
```

`header`参数说明：

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| header.error\_code | string | 报错类型描述。 |
| header.error\_message | string | 具体报错原因。 |

### 三、给服务器发送消息

在与监听服务器消息不同的线程中（比如主线程，具体实现因编程语言而异），向服务器发送消息。

客户端发送给服务端的消息有两种：

1. 音频流（须为单声道音频）。

2. 指令：以Text Frame方式发送的JSON格式的数据，用于控制任务的起止和标识任务边界。






指令由`header`和`payload`这两部分组成：



   - header：包含基础信息，格式统一。






     `header`示例：

















     ```json
     {
         "header": {
             "action": "run-task",
             "task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx", // 随机uuid
             "streaming": "duplex"
         }
     }
     ```





     `header`参数：



     |     |     |     |     |
     | --- | --- | --- | --- |
     | **参数** | **类型** | **是否必选** | **说明** |
     | header | object | - | 请求头 |
     | header.action | string | 是 | 指令类型，可以选填<br>     - "run-task"<br>       <br>     - "finish-task"<br>       <br>用法参见下文。 |
     | header.task\_id | string | 是 | 当次任务ID，随机生成的32位唯一ID。<br>为32位通用唯一识别码（UUID），由32个随机生成的字母和数字组成。可以带横线（如 `"2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx"`）或不带横线（如 `"2bf83b9abaeb4fda8d9axxxxxxxxxxxx"`）。大多数编程语言都内置了生成UUID的API，例如Python：<br>```python<br>import uuid<br>def generateTaskId():<br>    # 生成随机UUID<br>    return uuid.uuid4().hex<br>``` |
     | header.streaming | string | 是 | 固定字符串："duplex" |

   - `payload`：包含基础信息外的其他信息。不同指令的`payload`格式可能不同。


向服务器发送消息需要遵循如下时序，否则会导致任务失败：首先发送`run-task`指令，待监听到服务器返回的`task-started`事件后，再发送待识别的音频流。在音频流发送结束后，发送`finish-task`指令。

##### 1、发送run-task指令：开启语音识别任务（支持定制热词）

该指令用于开启语音识别、翻译任务。`task_id`在后续发送`finish-task`指令时也需要使用，必须保持一致。

示例：

```json
{
	"header": {
		"streaming": "duplex",
		"task_id": "e34730287cf643a6b0f1c7114c3ee899",
		"action": "run-task"
	},
	"payload": {
		"model": "gummy-chat-v1",
		"parameters": {
			"sample_rate": 16000,
			"format": "pcm",
			"source_language": null,
			"transcription_enabled": true,
			"translation_enabled": true,
			"translation_target_languages": ["en"]
		},
		"input": {},
		"task": "asr",
		"task_group": "audio",
		"function": "recognition"
	}
}
```

`payload`参数说明：

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| payload.task\_group | string | 是 | 固定字符串："audio"。 |
| payload.task | string | 是 | 固定字符串："asr"。 |
| payload.function | string | 是 | 固定字符串："recognition"。 |
| payload.model | string | 是 | 模型名称，详情请参见 [模型与价格](https://help.aliyun.com/zh/model-studio/sentence-websocket-api#b59cf24502dxr "")。 |
| payload.input | object | 是 | 固定格式：{}。 |

payload.parameters支持参数：

| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| sample\_rate | integer | - | 是 | 设置待识别音频采样率（单位Hz）。只支持16000Hz。 |
| format | string | - | 是 | 设置待识别音频格式。<br>支持的音频格式：pcm、wav、mp3、opus、speex、aac、amr。<br>**重要**<br>opus/speex：必须使用Ogg封装；<br>wav：必须为PCM编码；<br>amr：仅支持AMR-NB类型。 |
| vocabulary\_id | string | - | 否 | 设置热词ID，若未设置则不生效。<br>在本次语音识别中，将应用与该热词ID对应的热词信息。具体使用方法请参见 [定制热词](https://help.aliyun.com/zh/model-studio/custom-hot-words-for-gummy "")。 |
| source\_language | string | auto | 否 | 设置源（待识别/翻译语言）语言代码。如果无法提前确定语种，可不设置，默认为`auto`。<br>支持语音识别的语言代码：<br>- zh：中文<br>  <br>- en：英文<br>  <br>- ja：日语<br>  <br>- ko：韩语<br>  <br>- yue：粤语<br>  <br>- de：德语<br>  <br>- fr：法语<br>  <br>- ru：俄语<br>  <br>- es：西班牙语<br>  <br>- it：意大利语<br>  <br>- pt：葡萄牙语<br>  <br>- id：印尼语<br>  <br>- ar：阿拉伯语<br>  <br>- th：泰语<br>  <br>支持翻译的语言代码：<br>- zh：中文<br>  <br>- en：英文<br>  <br>- ja：日语<br>  <br>- ko：韩语<br>  <br>- yue：粤语<br>  <br>- de：德语<br>  <br>- fr：法语<br>  <br>- ru：俄语<br>  <br>- es：西班牙语<br>  <br>- it：意大利语<br>  <br>- pt：葡萄牙语<br>  <br>- id：印尼语<br>  <br>- ar：阿拉伯语<br>  <br>- th：泰语<br>  <br>- hi：印地语<br>  <br>- da：丹麦语<br>  <br>- ur：乌尔都语<br>  <br>- tr：土耳其语<br>  <br>- nl：荷兰语<br>  <br>- ms：马来语<br>  <br>- vi：越南语 |
| transcription\_enabled | boolean | true | 否 | 设置是否启用识别功能。<br>模型支持单独开启识别或翻译功能，也可同时启用两种功能，但至少需要开启其中一种能力。<br>**重要**<br>语音识别与翻译功能分别计费，费用按各自调用量独立计算。两项服务的单价一致。 |
| translation\_enabled | boolean | false | 否 | 设置是否启用翻译功能。要正常输出翻译结果，需配置`translation_target_languages`参数。<br>模型支持单独开启识别或翻译功能，也可同时启用两种功能，但至少需要开启其中一种能力。 |
| translation\_target\_languages | array\[string\] | - | 否 | 设置翻译目标语言代码。目标语言的代码与`source_language`参数一致。<br>目前支持的翻译包括：<br>- 中文（zh） → 英文（en）／日语（ja）／韩语（ko）／法语（fr）／德语（de）／西班牙语（es）／俄语（ru）／意大利语（it）<br>  <br>- 英文（en） → 中文（zh）／日语（ja）／韩语（ko）／葡萄牙语（pt）／法语（fr）／德语（de）／俄语（ru）／越南语（vi）／西班牙语（es）／荷兰语（nl）／丹麦语（da）／阿拉伯语（ar）／意大利语（it）／印地语（hi）／粤语（yue）／土耳其语（tr）／马来语（ms）／乌尔都语（ur）／印尼语（id）<br>  <br>- 日语（ja） → 泰语（th）／英文（en）／中文（zh）／越南语（vi）／法语（fr）／意大利语（it）／德语（de）／西班牙语（es）<br>  <br>- 韩语（ko） → 泰语（th）／英文（en）／中文（zh）／越南语（vi）／法语（fr）／西班牙语（es）／俄语（ru）／德语（de）<br>  <br>- 法语（fr） → 泰语（th）／英文（en）／日语（ja）／中文（zh）／越南语（vi）／德语（de）／意大利语（it）／西班牙语（es）／俄语（ru）／葡萄牙语（pt）<br>  <br>- 德语（de） → 泰语（th）／英文（en）／日语（ja）／中文（zh）／法语（fr）／越南语（vi）／俄语（ru）／西班牙语（es）／意大利语（it）／葡萄牙语（pt）<br>  <br>- 西班牙语（es） → 泰语（th）／英文（en）／日语（ja）／中文（zh）／法语（fr）／越南语（vi）／意大利语（it）／德语（de）／俄语（ru）／葡萄牙语（pt）<br>  <br>- 俄语（ru） → 泰语（th）／英文（en）／日语（ja）／中文（zh）／法语（fr）／越南语（vi）／德语（de）／西班牙语（es）／意大利语（it）／粤语（yue）／葡萄牙语（pt）<br>  <br>- 意大利语（it） → 泰语（th）／英文（en）／日语（ja）／中文（zh）／法语（fr）／越南语（vi）／西班牙语（es）／俄语（ru）／德语（de）<br>  <br>- 葡萄牙语（pt） → 英文（en）<br>  <br>- 印尼语（id） → 英文（en）<br>  <br>- 阿拉伯语（ar） → 英文（en）<br>  <br>- 泰语（th） → 日语（ja）／越南语（vi）／法语（fr）<br>  <br>- 印地语（hi） → 英文（en）<br>  <br>- 丹麦语（da） → 英文（en）<br>  <br>- 乌尔都语（ur） → 英文（en）<br>  <br>- 土耳其语（tr） → 英文（en）<br>  <br>- 荷兰语（nl） → 英文（en）<br>  <br>- 马来语（ms） → 英文（en）<br>  <br>- 越南语（vi） → 日语（ja）／法语（fr）<br>  <br>- 粤语（yue） → 中文（zh）／英文（en）<br>  <br>**重要**<br>目前暂不支持同时翻译为多种语言，请仅设置一个目标语言以完成翻译。 |
| max\_end\_silence | integer | 700 | 否 | 设置最大结束静音时长，单位为毫秒（ms），取值范围为200ms至6000ms。<br>若语音结束后静音时长超过该预设值，系统将判定当前语句已结束。 |

##### 2、发送二进制待识别音频流（单声道）

客户端需在收到`task-started`事件后，再发送待识别的音频流。

可以发送实时音频流（比如从话筒中实时获取到的）或者录音文件音频流，音频应是单声道。

音频通过WebSocket的二进制通道上传。建议每次发送100ms的音频，并间隔100ms。

##### 3、发送finish-task指令：结束语音识别任务

该指令用于结束语音识别任务。音频发送完毕后，客户端可以发送此指令以结束任务。

示例：

```json
{
    "header": {
        "action": "finish-task",
        "task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx",
        "streaming": "duplex"
    },
    "payload": {
        "input": {}
    }
}
```

`payload`参数说明：

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| payload.input | object | 是 | 固定格式：{}。 |

### **四、关闭WebSocket连接**

在程序正常结束、运行中出现异常或接收到`task-finished`、`task-failed`事件时，关闭WebSocket连接。通常通过调用工具库中的`close`函数来实现。

## **关于建连开销和连接复用**

WebSocket服务支持连接复用以提升资源的利用效率，避免建立连接开销。

当服务收到 `run-task` 指令后，将启动一个新的任务，并在任务完成时下发 `task-finished` 指令以结束该任务。结束任务后webSocket连接可以被复用，发送`run-task`指令开启下一个任务。

**重要**

1. 在复用连接中的不同任务需要使用不同 task\_id。

2. 如果在任务执行过程中发生失败，服务将依然下发 `task-failed` 指令，并关闭该连接。此时这个连接无法继续复用。

3. 如果在任务结束后60秒没有新的任务，连接会超时自动断开。


## **示例代码**

示例代码请参见 [Gummy实时语音识别、翻译websocket API](https://help.aliyun.com/zh/model-studio/real-time-websocket-api "")，在 [发送run-task指令](https://help.aliyun.com/zh/model-studio/sentence-websocket-api#a4566139berwo "") 时，请留意参数（模型名等）的差异； [监听result-generated事件](https://help.aliyun.com/zh/model-studio/sentence-websocket-api#d1f0f8ded9lf6 "") 时，请关注响应结果的不同。

## **错误码**

如遇报错问题，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行排查。

若问题仍未解决，请加入 [开发者群](https://github.com/aliyun/alibabacloud-bailian-speech-demo) 反馈遇到的问题，并提供Request ID，以便进一步排查问题。

## **常见问题**

### **功能特性**

#### **Q：为什么使用WebSocket协议而非HTTP/HTTPS协议？为什么不提供RESTful API？**

语音服务选择 WebSocket 而非 HTTP/HTTPS/RESTful，根本在于其依赖全双工通信能力——WebSocket 允许服务端与客户端主动双向传输数据（如实时推送语音合成/识别进度），而基于 HTTP 的 RESTful 仅支持客户端发起的单向请求-响应模式，无法满足实时交互需求。

### **故障排查**

如遇代码报错问题，请根据 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行排查。

#### **Q：为什么没有输出翻译结果？**

[run-task指令](https://help.aliyun.com/zh/model-studio/sentence-websocket-api#a4566139berwo "") 中的请求参数配置要正确。

1. 需将参数`translation_enabled`设置为`true`。

2. 需通过参数`translation_target_languages`指定翻译目标语言。注意，该参数类型为数组而非字符串。


### **更多问题**

请参见GitHub [QA](https://github.com/aliyun/alibabacloud-bailian-speech-demo/blob/master/docs/QA/cosyvoice.md)。