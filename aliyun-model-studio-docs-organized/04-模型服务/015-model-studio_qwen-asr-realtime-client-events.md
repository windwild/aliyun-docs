### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音识别](https://help.aliyun.com/zh/model-studio/speech-recognition-api-reference/)[实时语音识别（Qwen-ASR-Realtime）](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-api/)客户端事件

# 实时语音识别（Qwen-ASR-Realtime）客户端事件

更新时间：2026-02-11 02:29:07

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：iOS SDK](https://help.aliyun.com/zh/model-studio/sentence-ios-sdk)[下一篇：服务端事件](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

session.update

input\_audio\_buffer.append

input\_audio\_buffer.commit

session.finish

本文档介绍在与 Qwen-ASR Realtime API 的 WebSocket 会话中，客户端向服务端发送的事件。

**用户指南：** 模型介绍、功能特性和完整示例代码请参见 [实时语音识别-千问](https://help.aliyun.com/zh/model-studio/qwen-real-time-speech-recognition "")

## **session.update**

用于更新会话配置，建议在 WebSocket 连接建立后首先发送该事件。建议在WebSocket连接建立成功后，立即发送此事件作为交互的第一步。如果未发送，系统将使用默认配置。

服务端成功处理此事件后，会发送`服务端事件`事件作为确认。

|     |     |     |     |
| --- | --- | --- | --- |
| |     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| type | string | 是 | 事件类型。固定为`session.update`。 |
| event\_id | string | 是 | 事件ID。 |
| session | object | 是 | 包含会话配置的对象。 |
| session.input\_audio\_format | string | 否 | 音频格式。支持`pcm`和`opus`。<br>默认值：`pcm`。 |
| session.sample\_rate | integer | 否 | 音频采样率（Hz）。支持`16000`和`8000`。<br>默认值：`16000`。<br>设置为 `8000` 时，服务端会先升采样到16000Hz再进行识别，可能引入微小延迟。建议仅在源音频为8000Hz（如电话线路）时使用。 |
| session.input\_audio\_transcription | object | 否 | 语音识别相关配置。 |
| session.input\_audio\_transcription.language | string | 否 | 音频源语言。<br>- zh：中文（普通话、四川话、闽南语、吴语）<br>  <br>- yue：粤语<br>  <br>- en：英文<br>  <br>- ja：日语<br>  <br>- de：德语<br>  <br>- ko：韩语<br>  <br>- ru：俄语<br>  <br>- fr：法语<br>  <br>- pt：葡萄牙语<br>  <br>- ar：阿拉伯语<br>  <br>- it：意大利语<br>  <br>- es：西班牙语<br>  <br>- hi：印地语<br>  <br>- id：印尼语<br>  <br>- th：泰语<br>  <br>- tr：土耳其语<br>  <br>- uk：乌克兰语<br>  <br>- vi：越南语<br>  <br>- cs：捷克语<br>  <br>- da：丹麦语<br>  <br>- fil：菲律宾语<br>  <br>- fi：芬兰语<br>  <br>- is：冰岛语<br>  <br>- ms：马来语<br>  <br>- no：挪威语<br>  <br>- pl：波兰语<br>  <br>- sv：瑞典语 |
| session.turn\_detection | object | 否 | VAD（Voice Activity Detection，语音活动检测）配置。<br>它是启用/关闭VAD模式的开关：若将它设为null，则将关闭 [VAD 模式](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-interaction-process#9b49887720jcw "")，启用 [Manual 模式](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-interaction-process#ee09a3493fsuc "")；反之则相反。 |
| session.turn\_detection.type | string | 否，`turn_dection`存在时必须 | 固定为 `server_vad`。 |
| session.turn\_detection.threshold | float | 否 | VAD检测阈值。推荐将该值设为`0.0`。<br>默认值：`0.2`。<br>取值范围：`[-1, 1]`。<br>较低的阈值会提高 VAD 的灵敏度，可能将背景噪音误判为语音。较高的阈值则降低灵敏度，有助于在嘈杂环境中减少误触发。 |
| session.turn\_detection.silence\_duration\_ms | integer | 否 | VAD断句检测阈值（ms）。静音持续时长超过该阈值将被认为是语句结束。推荐将该值设为`400`。<br>默认值：`800`。<br>取值范围：`[200, 6000]`。<br>较低的值（如 300ms）可使模型更快响应，但可能导致在自然停顿处发生不合理的断句。较高的值（如 1200ms）可更好地处理长句内的停顿，但会增加整体响应延迟。 | | ```json<br>{<br>    "event_id": "event_123",<br>    "type": "session.update",<br>    "session": {<br>        "input_audio_format": "pcm",<br>        "sample_rate": 16000,<br>        "input_audio_transcription": {<br>            "language": "zh"<br>        },<br>        "turn_detection": {<br>            "type": "server_vad",<br>            "threshold": 0.0,<br>            "silence_duration_ms": 400<br>        }<br>    }<br>}<br>``` |

## **input\_audio\_buffer.append**

用于将音频数据块追加到服务端的输入缓冲区。这是流式发送音频的核心事件。

**不同场景下的区别：**

- **VAD 模式**：音频缓冲区用于语音活动检测，服务端会自动决定何时提交音频进行识别。

- **非VAD模式**：客户端可以控制每个事件中的音频数据量，单个 `input_audio_buffer.append` 事件中的 `audio` 字段内容最大为 15 MiB。建议流式发送较小的音频块以获得更快的响应。


**重要提示**：服务端不会对`input_audio_buffer.append`事件发送任何确认响应。

|     |     |     |     |
| --- | --- | --- | --- |
| |     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| type | string | 是 | 事件类型。固定为`input_audio_buffer.append`。 |
| event\_id | string | 是 | 事件ID。 |
| audio | string | 是 | Base64编码的音频数据。 | | ```json<br>{<br>  "event_id": "event_2728",<br>  "type": "input_audio_buffer.append",<br>  "audio": "<audio> by base64"<br>}<br>``` |

## **input\_audio\_buffer.commit**

非VAD模式下，用于手动触发识别。此事件通知服务端，客户端已发送完一段完整的语音，将当前缓冲区内的所有音频数据作为一个整体进行识别。

**禁用场景：** VAD模式。

服务端成功处理后，会发送`input_audio_buffer.committed`事件作为确认响应。

|     |     |     |     |
| --- | --- | --- | --- |
| |     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| type | string | 是 | 事件类型。固定为`input_audio_buffer.commit`。 |
| event\_id | string | 是 | 事件ID。 | | ```json<br>{<br>  "event_id": "event_789",<br>   "type": "input_audio_buffer.commit"<br>}<br>``` |

## **session.finish**

用于结束当前会话。

服务端响应流程：

- 已检测到语音：服务端完成最后的语音识别后，发送包含识别结果的`conversation.item.input_audio_transcription.completed`事件，随后发送 [session.finished](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events#6eaa77339djdv "") 事件作为会话结束标识。

- 未检测到语音：服务端直接发送`session.finished`事件。


客户端监听到`session.finished`事件后，需主动断开连接。

|     |     |     |     |
| --- | --- | --- | --- |
| |     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| type | string | 是 | 事件类型。固定为`session.finish`。 |
| event\_id | string | 是 | 事件ID。 | | ```json<br>{<br>  "event_id": "event_341",<br>  "type": "session.finish",<br>}<br>``` |