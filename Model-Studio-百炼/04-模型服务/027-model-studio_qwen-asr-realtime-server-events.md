### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音识别](https://help.aliyun.com/zh/model-studio/speech-recognition-api-reference/)[实时语音识别（Qwen-ASR-Realtime）](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-api/)服务端事件

# 实时语音识别（Qwen-ASR-Realtime）服务端事件

更新时间：2026-02-11 02:29:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：客户端事件](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-client-events)[下一篇：Python SDK](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-python-sdk)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

error

session.created

session.updated

input\_audio\_buffer.speech\_started

input\_audio\_buffer.speech\_stopped

input\_audio\_buffer.committed

conversation.item.created

conversation.item.input\_audio\_transcription.text

conversation.item.input\_audio\_transcription.completed

conversation.item.input\_audio\_transcription.failed

session.finished

本文档介绍在与 Qwen-ASR Realtime API 的 WebSocket 会话中，服务端向客户端发送的事件。

**用户指南：** 模型介绍、功能特性和完整示例代码请参见 [实时语音识别-千问](https://help.aliyun.com/zh/model-studio/qwen-real-time-speech-recognition "")

## **error**

当服务端检测到错误（包括客户端错误和服务端错误）时，向客户端发送的事件。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`error`。 |
| event\_id | string | 事件ID。 |
| error.type | string | 错误类型。 |
| error.code | string | 错误代码。 |
| error.message | string | 具体的报错信息。请按 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 所示的解决方案进行处理。 |
| error.param | string | 与错误相关的参数。 |
| error.event\_id | string | 与错误相关的事件ID。 | | ```json<br>{<br>  "event_id": "event_B2uoU7VOt1AAITsPRPH9n",<br>  "type": "error",<br>  "error": {<br>    "type": "invalid_request_error",<br>    "code": "invalid_value",<br>    "message": "Invalid value: 'whisper-1xx'. Supported values are: 'whisper-1'.",<br>    "param": "session.input_audio_transcription.model",<br>    "event_id": "event_123"<br>  }<br>}<br>``` |

## **session.created**

当客户端成功连接到服务端后，服务端响应的第一个事件。该事件包含服务端为此次连接设置的默认配置信息。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`session.created`。 |
| event\_id | string | 事件ID。 |
| session.id | string | 本次 WebSocket 会话的ID。 |
| session.object | string | 固定为`realtime.session`。 |
| session.model | string | 当前调用的 [模型](https://help.aliyun.com/zh/model-studio/qwen-real-time-speech-recognition#ff8c59ef0busr "") 名称。 |
| session.modalities | array\[string\] | 模型输出模态，固定为`["text"]`。 |
| session.input\_audio\_format | string | 输入音频格式。 |
| session.input\_audio\_transcription | object | 语音识别相关配置参数。详情参见客户端 [session.update](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-client-events#af43722339yva "") 事件`input_audio_transcription`参数。 |
| session.turn\_detection | object | VAD（Voice Activity Detection，语音活动检测）配置。 |
| session.turn\_detection.type | string | 固定为`server_vad`。 |
| session.turn\_detection.threshold | float | VAD检测阈值。 |
| session.turn\_detection.silence\_duration\_ms | integer | VAD断句检测阈值（ms）。 | | ```json<br>{<br>    "event_id": "event_1234",<br>    "type": "session.created",<br>    "session": {<br>        "id": "sess_001",<br>        "object": "realtime.session",<br>        "model": "qwen3-asr-flash-realtime",<br>        "modalities": ["text"],<br>        "input_audio_format": "pcm16",<br>        "input_audio_transcription": null,<br>        "turn_detection": {<br>            "type": "server_vad",<br>            "threshold": 0.5,<br>            "silence_duration_ms": 200<br>        }<br>    }<br>}<br>``` |

## **session.updated**

当客户端发送 [session.update](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-client-events#af43722339yva "") 事件并成功被服务端处理后，服务端将发送该事件。如果处理过程中出现错误，则直接发送 error 事件。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`session.updated`。 |

其他参数含义同 [session.created](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events?spm=a2c4g.11186623.help-menu-2400256.d_2_7_4_1.1d1f35a3h7Kvq2#2c04b24bc3wlo "")。 | ```json<br>{<br>    "event_id": "event_1234",<br>    "type": "session.updated",<br>    "session": {<br>        "id": "sess_001",<br>        "object": "realtime.session",<br>        "model": "gpt-4o-realtime-preview-2024-12-17",<br>        "modalities": ["text"],<br>        "input_audio_format": "pcm16",<br>        "input_audio_transcription": null,<br>        "turn_detection": {<br>            "type": "server_vad",<br>            "threshold": 0.5,<br>            "silence_duration_ms": 200<br>        }<br>    }<br>}<br>``` |

## **input\_audio\_buffer.** speech\_started

此事件仅在 VAD 模式下发送。当服务端在音频缓冲区中检测到语音开始时发送。

该事件可能在每次音频添加到缓冲区时发生（除非已检测到语音开始）。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`input_audio_buffer.speech_started`。 |
| event\_id | string | 事件ID。 |
| audio\_start\_ms | integer | 在会话期间，从音频开始写入缓冲区到首次检测到语音时的毫秒数。 |
| item\_id | string | 将创建的用户消息项的 ID。 | | ```json<br>{<br>  "event_id": "event_B1lV7FPbgTv9qGxPI1tH4",<br>  "type": "input_audio_buffer.speech_started",<br>  "audio_start_ms": 64,<br>  "item_id": "item_B1lV7jWLscp4mMV8hSs8c"<br>}<br>``` |

## **input\_audio\_buffer.** speech\_stopped

此事件仅在 VAD 模式下发送。当服务端在音频缓冲区中检测到语音结束时发送。

该事件触发后，服务端将紧接着发送一个 [conversation.item.created](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events?spm=a2c4g.11186623.help-menu-2400256.d_2_7_4_1.1d1f35a3h7Kvq2#04dabbb9b6eto "") 事件，包含从音频缓冲区创建的用户消息项。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`input_audio_buffer.speech_stopped`。 |
| event\_id | string | 事件ID。 |
| audio\_end\_ms | integer | 从会话开始到语音停止的毫秒数。 |
| item\_id | string | 当语音停止时将创建的用户消息项的 ID。 | | ```json<br>{<br>  "event_id": "event_B3GGEYh2orwNIdhUagZPz",<br>  "type": "input_audio_buffer.speech_stopped",<br>  "audio_end_ms": 28128,<br>  "item_id": "item_B3GGE8ry4yqbqJGzrVhEM"<br>}<br>``` |

## **input\_audio\_buffer.committed**

- **VAD模式：** 当客户端完成音频数据发送（通过 [input\_audio\_buffer.append](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-client-events#a42f8e9111n72 "") 事件）后，服务端发送该事件。

- **非VAD模式：** 客户端完成音频数据发送（通过 [input\_audio\_buffer.append](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-client-events#a42f8e9111n72 "") 事件）并发送 [input\_audio\_buffer.commit](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-client-events#d6d5cd90f3q4c "") 事件后，服务端发送该事件。


|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`input_audio_buffer.committed`。 |
| event\_id | string | 事件ID。 |
| previous\_item\_id | string | 前一个对话项的ID |
| item\_id | string | 将创建的用户对话项的 ID。 | | ```json<br>{<br>    "event_id": "event_1121",<br>    "type": "input_audio_buffer.committed",<br>    "previous_item_id": "msg_001",<br>    "item_id": "msg_002"<br>}<br>``` |

## conversation.item.created

当对话项（item）创建时发送该事件。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`conversation.item.created`。 |
| event\_id | string | 事件ID。 |
| previous\_item\_id | string | 前一个对话项的ID |
| item | object | 要添加到对话中的条目。 |
| item.id | string | 对话项的唯一ID。 |
| item.object | string | 固定为 `realtime.item` 。 |
| item.type | string | 固定为`message`。 |
| item.status | string | 对话项的状态。 |
| item.role | string | 消息发送的角色。 |
| item.content | array\[object\] | 消息的内容。 |
| item.content.type | string | 固定为`input_audio`。 |
| item.content.transcript | string | 固定为`null`。完整的识别结果通过 [conversation.item.input\_audio\_transcription.completed](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events?spm=a2c4g.11186623.help-menu-2400256.d_2_7_4_1.1d1f35a3h7Kvq2#403ecacd74qqg "") 事件提供。 | | ```json<br>{<br>  "type": "conversation.item.created",<br>  "event_id": "event_B3GGKbCfBZTpqFHZ0P8vg",<br>  "previous_item_id": "item_B3GGE8ry4yqbqJGzrVhEM",<br>  "item": {<br>    "id": "item_B3GGEPlolCqdMiVbYIf5L",<br>    "object": "realtime.item",<br>    "type": "message",<br>    "status": "completed",<br>    "role": "user",<br>    "content": [<br>      {<br>        "type": "input_audio",<br>        "transcript": null<br>      }<br>    ]<br>  }<br>}<br>``` |

## conversation.item.input\_audio\_transcription.text

此事件会高频发送，用于展示实时识别结果。

|     |     |     |     |
| --- | --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`conversation.item.input_audio_transcription.text`。 |
| event\_id | string | 事件ID。 |
| item\_id | string | 关联的对话项ID。 |
| content\_index | integer | 包含音频的内容部分的索引。 |
| language | string | 被识别音频的语种。当请求参数`language`已指定语种时，该值与所指定的参数一致。<br>可能的值如下：<br>- zh：中文（普通话、四川话、闽南语、吴语）<br>  <br>- yue：粤语<br>  <br>- en：英文<br>  <br>- ja：日语<br>  <br>- de：德语<br>  <br>- ko：韩语<br>  <br>- ru：俄语<br>  <br>- fr：法语<br>  <br>- pt：葡萄牙语<br>  <br>- ar：阿拉伯语<br>  <br>- it：意大利语<br>  <br>- es：西班牙语<br>  <br>- hi：印地语<br>  <br>- id：印尼语<br>  <br>- th：泰语<br>  <br>- tr：土耳其语<br>  <br>- uk：乌克兰语<br>  <br>- vi：越南语 |
| emotion | string | 被识别音频的情感。支持的情感如下：<br>- `surprised`：惊讶<br>  <br>- `neutral`：平静<br>  <br>- `happy`：愉快<br>  <br>- `sad`：悲伤<br>  <br>- `disgusted`：厌恶<br>  <br>- `angry`：愤怒<br>  <br>- `fearful`：恐惧 |
| text | string | 已确认的文本前缀。这是当前句子中，模型已确认不会再变更的部分。 |
| stash | string | 预识别的文本后缀。这是紧跟在已确认部分之后，模型仍在处理、可能会被修正的临时草稿。 | | ```json
{
"event_id": "event_R7Pfu8QVBfP5HmpcbEFSd",
"type": "conversation.item.input_audio_transcription.text",
"item_id": "item_MpJQPNQzqVRc9aC9zMwSj",
"content_index": 0,
"language": "zh",
"emotion": "neutral",
"text": "",
"stash": "北京的"
}
```

在任何时刻，要获取当前最完整的句子预览，都需要将这两个字段拼接起来：实时预览句子 = `text` + `stash`。

**点击查看示例**

假设用户正在说：“今天天气不错，阳光明媚。”

以下是您可能会收到的事件流以及如何解读它们：

|     |     |     |     |
| --- | --- | --- | --- |
| **时间点** | **用户说话进度** | **API 响应 (text 和 stash)** | **客户端 UI 应显示 (text + stash)** |
| T1 | “今天……” | text: ""<br>stash: "今天" | 今天 |
| T2 | “……天气……” | text: ""<br>stash: "今天天气" | 今天天气 |
| T3 | “……不错” | text: "今天"<br>stash: "天气不错" | 今天天气不错<br>（注意，“今天”已被确认并移入text） |
| T4 | （短暂停顿） | text: "今天天气不错，"<br>stash: "" | 今天天气不错，<br>（前半句完全确认） |
| T5 | “……阳光……” | text: "今天天气不错，"<br>stash: "阳光" | 今天天气不错，阳光 |
| T6 | “……明媚。” | text: "今天天气不错，"<br>stash: "阳光明媚。" | 今天天气不错，阳光明媚。 |
| T7 | （结束说话） | - | 使用 [conversation.item.input\_audio\_transcription.completed](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events?spm=a2c4g.11186623.help-menu-2400256.d_2_7_4_1.1d1f35a3h7Kvq2#403ecacd74qqg "") 的transcript的内容作为最终结果。 | |

## conversation.item.input\_audio\_transcription.completed

向客户端发送最终识别结果。此事件标志着一个对话项（item）的结束。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`conversation.item.input_audio_transcription.completed`。 |
| event\_id | string | 事件ID。 |
| item\_id | string | 关联的对话项ID。 |
| content\_index | integer | 包含音频的内容部分的索引。 |
| language | string | 被识别音频的语种。当请求参数`language`已指定语种时，该值与所指定的参数一致。<br>可能的值如下：<br>- zh：中文（普通话、四川话、闽南语、吴语）<br>  <br>- yue：粤语<br>  <br>- en：英文<br>  <br>- ja：日语<br>  <br>- de：德语<br>  <br>- ko：韩语<br>  <br>- ru：俄语<br>  <br>- fr：法语<br>  <br>- pt：葡萄牙语<br>  <br>- ar：阿拉伯语<br>  <br>- it：意大利语<br>  <br>- es：西班牙语<br>  <br>- hi：印地语<br>  <br>- id：印尼语<br>  <br>- th：泰语<br>  <br>- tr：土耳其语<br>  <br>- uk：乌克兰语<br>  <br>- vi：越南语 |
| emotion | string | 被识别音频的情感。支持的情感如下：<br>- `surprised`：惊讶<br>  <br>- `neutral`：平静<br>  <br>- `happy`：愉快<br>  <br>- `sad`：悲伤<br>  <br>- `disgusted`：厌恶<br>  <br>- `angry`：愤怒<br>  <br>- `fearful`：恐惧 |
| transcript | string | 识别结果。 | | ```json<br>{<br>  "event_id": "event_B3GGEjPT2sLzjBM74W6kB",<br>  "type": "conversation.item.input_audio_transcription.completed",<br>  "item_id": "item_B3GGC53jGOuIFcjZkmEQ9",<br>  "content_index": 0,<br>  "language": "zh",<br>  "emotion": "neutral",<br>  "transcript": "今天天气怎么样"<br>}<br>``` |

## conversation.item.input\_audio\_transcription.failed

当输入了音频但是识别失败时，服务端发送该事件。与其他 `error` 事件分开处理，便于客户端识别相关的具体项目。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`conversation.item.input_audio_transcription.failed`。 |
| item\_id | string | 关联的对话项ID。 |
| content\_index | integer | 包含音频的内容部分的索引。 |
| error.code | string | 错误代码。 |
| error.message | string | 错误消息。 |
| error.param | string | 错误相关的参数。 | | ```json<br>{<br>  "type": "conversation.item.input_audio_transcription.failed",<br>  "item_id": "<item_id>",<br>  "content_index": 0,<br>  "error": {<br>    "code": "<code>",<br>    "message": "<message>",<br>    "param": "<param>"<br>  }<br>}<br>``` |

## session.finished

会话结束事件，表示当前会话中，所有音频识别已完成。

该事件只有在客户端发送`session.finish`后才会发送，客户端接收到该事件后可主动断开连接。

|     |     |     |
| --- | --- | --- |
| |     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| type | string | 事件类型。固定为`session.finished`。 |
| event\_id | string | 事件ID。 | | ```json<br>{<br>  "event_id": "event_2239",<br>  "type": "session.finished"<br>}<br>``` |