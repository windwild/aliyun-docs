### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音识别](https://help.aliyun.com/zh/model-studio/speech-recognition-api-reference/)[实时语音识别（Qwen-ASR-Realtime）](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-api/)Python SDK

# 实时语音识别（Qwen-ASR-Realtime）Python SDK-API参考

更新时间：2026-02-11 02:29:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：服务端事件](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events)[下一篇：Java SDK](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-java-sdk)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

请求参数

关键接口

OmniRealtimeConversation类

回调接口（OmniRealtimeCallback）

本文档介绍如何使用 DashScope Python SDK 调用实时语音识别（Qwen-ASR-Realtime）模型。

**用户指南：** 模型介绍、功能特性和完整示例代码请参见 [实时语音识别-千问](https://help.aliyun.com/zh/model-studio/qwen-real-time-speech-recognition "")

## **前提条件**

1. [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")，确保DashScope SDK版本不低于1.25.6。

2. [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。

3. 了解 [交互流程](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-interaction-process "")。


## **请求参数**

- 以下参数通过`OmniRealtimeConversation`的构造方法设置。



**点击查看示例代码**




















```python
class MyCallback(OmniRealtimeCallback):
      """实时识别回调处理"""
      def __init__(self, conversation):
          self.conversation = conversation
          self.handlers = {
              'session.created': self._handle_session_created,
              'conversation.item.input_audio_transcription.completed': self._handle_final_text,
              'conversation.item.input_audio_transcription.text': self._handle_stash_text,
              'input_audio_buffer.speech_started': lambda r: print('======Speech Start======'),
              'input_audio_buffer.speech_stopped': lambda r: print('======Speech Stop======')
          }

      def on_open(self):
          print('Connection opened')

      def on_close(self, code, msg):
          print(f'Connection closed, code: {code}, msg: {msg}')

      def on_event(self, response):
          try:
              handler = self.handlers.get(response['type'])
              if handler:
                  handler(response)
          except Exception as e:
              print(f'[Error] {e}')

      def _handle_session_created(self, response):
          print(f"Start session: {response['session']['id']}")

      def _handle_final_text(self, response):
          print(f"Final recognized text: {response['transcript']}")

      def _handle_stash_text(self, response):
          print(f"Got stash result: {response['stash']}")

conversation = OmniRealtimeConversation(
          model='qwen3-asr-flash-realtime',
          # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/realtime
          url='wss://dashscope.aliyuncs.com/api-ws/v1/realtime',
          callback=MyCallback(conversation=None)  # 暂时传None，稍后注入
      )
# 注入自身到回调
conversation.callback.conversation = conversation
```









| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| `model` | `str` | 是 | 指定要使用的 [模型](https://help.aliyun.com/zh/model-studio/qwen-real-time-speech-recognition#ff8c59ef0busr "") 名称。 |
| `callback` | `OmniRealtimeCallback` | 是 | 用于处理服务端事件的回调对象实例。 |
| `url` | `str` | 是 | 语音识别服务地址：<br>  - 中国内地：`wss://dashscope.aliyuncs.com/api-ws/v1/realtime`<br>    <br>  - 国际：`wss://dashscope-intl.aliyuncs.com/api-ws/v1/realtime`。 |

- 以下参数通过`OmniRealtimeConversation`的`update_session`方法设置。



**点击查看示例代码**




















```python
transcription_params = TranscriptionParams(
      language='zh',
      sample_rate=16000,
      input_audio_format="pcm"
)

conversation.update_session(
      output_modalities=[MultiModality.TEXT],
      enable_turn_detection=True,
      turn_detection_type="server_vad",
      turn_detection_threshold=0.0,
      turn_detection_silence_duration_ms=400,
      enable_input_audio_transcription=True,
      transcription_params=transcription_params
)
```









| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| `output_modalities` | `List[MultiModality]` | 是 | 模型输出模态，固定为`[MultiModality.TEXT]`。 |
| `enable_turn_detection` | `bool` | 否 | 是否开启服务端语音活动检测（VAD）。关闭后，需手动调用`commit()`方法触发识别。<br>默认值：`True`。<br>取值范围：<br>  - `True`：开启<br>    <br>  - `False`：关闭 |
| `turn_detection_type` | `str` | 否 | 服务端VAD类型，固定为 `server_vad`。 |
| `turn_detection_threshold` | `float` | 否 | VAD检测阈值。推荐将该值设为`0.0`。<br>默认值：`0.2`。<br>取值范围：`[-1, 1]`。<br>较低的阈值会提高 VAD 的灵敏度，可能将背景噪音误判为语音。较高的阈值则降低灵敏度，有助于在嘈杂环境中减少误触发。 |
| `turn_detection_silence_duration_ms` | `int` | 否 | VAD断句检测阈值（ms）。静音持续时长超过该阈值将被认为是语句结束。推荐将该值设为`400`。<br>默认值：`800`。<br>取值范围：`[200, 6000]`。<br>较低的值（如 300ms）可使模型更快响应，但可能导致在自然停顿处发生不合理的断句。较高的值（如 1200ms）可更好地处理长句内的停顿，但会增加整体响应延迟。 |
| `transcription_params` | `TranscriptionParams` | 否 | 语音识别相关配置。 |

- 以下参数通过`TranscriptionParams`的构造方法设置。



**点击查看示例代码**




















```python
transcription_params = TranscriptionParams(
      language='zh',
      sample_rate=16000,
      input_audio_format="pcm"
)
```









| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| `language` | `str` | 否 | 音频源语言。<br>  - zh：中文（普通话、四川话、闽南语、吴语）<br>    <br>  - yue：粤语<br>    <br>  - en：英文<br>    <br>  - ja：日语<br>    <br>  - de：德语<br>    <br>  - ko：韩语<br>    <br>  - ru：俄语<br>    <br>  - fr：法语<br>    <br>  - pt：葡萄牙语<br>    <br>  - ar：阿拉伯语<br>    <br>  - it：意大利语<br>    <br>  - es：西班牙语<br>    <br>  - hi：印地语<br>    <br>  - id：印尼语<br>    <br>  - th：泰语<br>    <br>  - tr：土耳其语<br>    <br>  - uk：乌克兰语<br>    <br>  - vi：越南语<br>    <br>  - cs：捷克语<br>    <br>  - da：丹麦语<br>    <br>  - fil：菲律宾语<br>    <br>  - fi：芬兰语<br>    <br>  - is：冰岛语<br>    <br>  - ms：马来语<br>    <br>  - no：挪威语<br>    <br>  - pl：波兰语<br>    <br>  - sv：瑞典语 |
| `sample_rate` | `int` | 否 | 音频采样率（Hz）。支持`16000`和`8000`。<br>默认值：`16000`。<br>设置为 `8000` 时，服务端会先升采样到16000Hz再进行识别，可能引入微小延迟。建议仅在源音频为8000Hz（如电话线路）时使用。 |
| `input_audio_format` | `str` | 否 | 音频格式。支持`pcm`和`opus`。<br>默认值：`pcm`。 |


## **关键接口**

### **OmniRealtimeConversation类**

OmniRealtimeConversation通过`from dashscope.audio.qwen_omni import OmniRealtimeConversation`方法引入。

| **方法签名** | **服务端响应事件（通过回调下发）** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **方法签名** | **服务端响应事件（通过回调下发）** | **说明** |
| ```python<br>def connect(self,) -> None:<br>``` | [session.created](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events#2c04b24bc3wlo "")<br>> 会话已创建<br>[session.updated](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events#4d6ed9dd62vmj "")<br>> 会话配置已更新 | 和服务端创建连接。 |
| ```python<br>def update_session(self,<br>                       output_modalities: List[MultiModality],<br>                       voice: str = None,<br>                       input_audio_format: AudioFormat = AudioFormat.PCM_16000HZ_MONO_16BIT,<br>                       output_audio_format: AudioFormat = AudioFormat.PCM_24000HZ_MONO_16BIT,<br>                       enable_input_audio_transcription: bool = True,<br>                       input_audio_transcription_model: str = None,<br>                       enable_turn_detection: bool = True,<br>                       turn_detection_type: str = 'server_vad',<br>                       prefix_padding_ms: int = 300,<br>                       turn_detection_threshold: float = 0.2,<br>                       turn_detection_silence_duration_ms: int = 800,<br>                       turn_detection_param: dict = None,<br>                       translation_params: TranslationParams = None,<br>                       transcription_params: TranscriptionParams = None,<br>                       **kwargs) -> None:<br>``` | [session.updated](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events#4d6ed9dd62vmj "")<br>> 会话配置已更新 | 用于更新会话配置，建议在连接建立后首先调用该方法进行设置。若未调用该方法，系统将使用默认配置。只需关注 [请求参数](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-python-sdk#21cc616e29q8y "") 中的涉及到的参数。 |
| ```python<br>def append_audio(self, audio_b64: str) -> None:<br>``` | 无 | 将Base64编码后的音频数据片段追加到云端输入音频缓冲区。 <br>- [请求参数](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-python-sdk#21cc616e29q8y "")`enable_turn_detection`设为`True`，音频缓冲区用于检测语音，服务端决定何时提交。<br>  <br>- [请求参数](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-python-sdk#21cc616e29q8y "")`enable_turn_detection`设为`False`，客户端可以选择每个事件中放置多少音频量，最多放置 15 MiB。 例如，从客户端流式处理较小的数据块可以让 VAD 响应更迅速。 |
| ```python<br>def commit(self, ) -> None:<br>``` | [input\_audio\_buffer.committed](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events#1108a3764an0e "")<br>> 服务端收到提交的音频 | 提交之前通过append添加到云端缓冲区的音视频，如果输入的音频缓冲区为空将产生错误。<br>**禁用场景：** [请求参数](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-python-sdk#21cc616e29q8y "")`enable_turn_detection`设为`True`时。 |
| ```python<br>def end_session(self, timeout: int = 20) -> None:<br>``` | [session.finished](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events#6eaa77339djdv "")<br>> 服务端完成语音识别，结束会话 | 通知服务端结束会话，服务端收到会话结束通知后将完成最后的语音识别。<br>**调用时机**：<br>- [VAD 模式（默认）](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-interaction-process#9b49887720jcw "") 下，发送完音频后调用该方法<br>  <br>- [Manual 模式](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-interaction-process#ee09a3493fsuc "") 下，调用commit方法之后调用该方法<br>  <br>`end_session_async` 是 `end_session` 的异步版本，两者功能完全相同。 |
| ```python<br>def close(self, ) -> None:<br>``` | 无 | 终止任务，并关闭连接。 |
| ```python<br>def get_session_id(self) -> str:<br>``` | 无 | 获取当前任务的session\_id。 |
| ```python<br>def get_last_response_id(self) -> str:<br>``` | 无 | 获取最近一次response的response\_id。 |

### **回调接口（OmniRealtimeCallback）**

服务端会通过回调的方式，将服务端响应事件和数据返回给客户端。

继承此类并实现相应方法以处理服务端事件。

通过`from dashscope.audio.qwen_omni import OmniRealtimeCallback`引入。

| **方法签名** | **参数** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **方法签名** | **参数** | **说明** |
| ```python<br>def on_open(self) -> None:<br>``` | 无 | WebSocket连接成功建立时触发。 |
| ```python<br>def on_event(self, message: dict) -> None:<br>``` | message： [服务端事件](https://help.aliyun.com/zh/model-studio/qwen-asr-realtime-server-events "") | 收到服务端事件时触发。 |
| ```python<br>def on_close(self, close_status_code, close_msg) -> None:<br>``` | close\_status\_code：状态码<br>close\_msg：WebSocket连接关闭时的日志信息 | WebSocket连接关闭时触发。 |