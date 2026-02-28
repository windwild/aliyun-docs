### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[模型推理](https://help.aliyun.com/zh/model-studio/model-inference/)[语音翻译](https://help.aliyun.com/zh/model-studio/speech-translation/)实时音视频翻译-千问

# 实时音视频翻译-千问

更新时间：2026-02-12 02:59:51

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：实时语音翻译-Gummy](https://help.aliyun.com/zh/model-studio/real-time-speech-translation)[下一篇：音视频文件翻译-千问](https://help.aliyun.com/zh/model-studio/qwen3-livetranslate-flash)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

如何使用

1\. 配置连接

2\. 配置语种、输出模态与音色

3\. 输入音频与图片

4\. 接收模型响应

支持的模型

快速开始

利用图像提升翻译准确率

通过函数计算一键部署

交互流程

API 参考

计费说明

支持的语种

支持的音色

qwen3-livetranslate-flash-realtime 是视觉增强型实时翻译模型，支持 18 种语言（中、英、俄、法等）互译，可同时处理音频与图像输入，适用于实时视频流或本地视频文件，利用视觉上下文信息提升翻译准确性，并实时输出高质量的翻译文本与音频。

> 在线体验参见 [通过函数计算一键部署](https://help.aliyun.com/zh/model-studio/qwen3-livetranslate-flash-realtime#7727c7c1ed6du "")。

## **如何使用**

### **1\. 配置连接**

qwen3-livetranslate-flash-realtime 模型通过 WebSocket 协议接入，连接时需要以下配置项：

| **配置项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **配置项** | **说明** |
| 调用地址 | 中国大陆版：wss://dashscope.aliyuncs.com/api-ws/v1/realtime<br>国际版：wss://dashscope-intl.aliyuncs.com/api-ws/v1/realtime |
| 查询参数 | 查询参数为model，需指定为访问的模型名。示例：`?model=qwen3-livetranslate-flash-realtime` |
| 消息头 | 使用 Bearer Token 鉴权：Authorization: Bearer DASHSCOPE\_API\_KEY<br>> DASHSCOPE\_API\_KEY 是您在百炼上申请的API-KEY。 |

可通过以下 Python 示例代码建立连接。

**WebSocket 连接 Python示例代码**

```python
# pip install websocket-client
import json
import websocket
import os

API_KEY=os.getenv("DASHSCOPE_API_KEY")
API_URL = "wss://dashscope.aliyuncs.com/api-ws/v1/realtime?model=qwen3-livetranslate-flash-realtime"

headers = [\
    "Authorization: Bearer " + API_KEY\
]

def on_open(ws):
    print(f"Connected to server: {API_URL}")
def on_message(ws, message):
    data = json.loads(message)
    print("Received event:", json.dumps(data, indent=2))
def on_error(ws, error):
    print("Error:", error)

ws = websocket.WebSocketApp(
    API_URL,
    header=headers,
    on_open=on_open,
    on_message=on_message,
    on_error=on_error
)

ws.run_forever()
```

### **2\. 配置语种、输出模态与音色**

发送客户端事件 [session.update](https://help.aliyun.com/zh/model-studio/live-translator-client-events#af43722339yva "")：

- **语种**


  - **源语种：** 通过`session.input_audio_transcription.language`参数配置。


    > 默认值为`en`（英语）。

  - **目标语种：** 通过`session.translation.language`参数配置。


    > 默认值为`en`（英语）。


取值范围参见 [支持的语种](https://help.aliyun.com/zh/model-studio/qwen3-livetranslate-flash-realtime#4ffd192226f0s "")。

- **输出源语言识别结果**

通过`session.input_audio_transcription.model`参数配置。设置为`qwen3-asr-flash-realtime`后，服务端会在翻译的同时返回输入音频的语音识别结果（源语言原文）。

启用后，服务端会返回以下事件：
  - `conversation.item.input_audio_transcription.text`：流式返回识别结果。

  - `conversation.item.input_audio_transcription.completed`：识别完成后返回最终结果。
- **输出模态**

通过`session.modalities`参数配置。支持设置为`["text"]`（仅输出文本）或`["text","audio"]`（输出文本与音频）。

- **音色**

通过`session.voice`参数配置。参见 [支持的音色](https://help.aliyun.com/zh/model-studio/qwen3-livetranslate-flash-realtime#0a5bde7593gdk "")。


### **3\. 输入音频与图片**

客户端通过 [input\_audio\_buffer.append](https://help.aliyun.com/zh/model-studio/live-translator-client-events#8d11313f2198k "") 和 [input\_image\_buffer.append](https://help.aliyun.com/zh/model-studio/live-translator-client-events#e27908854eaht "") 事件发送 Base64 编码的音频和图片数据。音频输入是必需的；图片输入是可选的。

> 图片可以来自本地文件，或从视频流中实时采集。

> 服务端自动检测音频的起始和结束，并据此触发模型响应。

### **4\. 接收模型响应**

当服务端检测到音频终止时，模型会开始回复。模型的响应格式取决于配置的输出模态。

- **仅输出文本**

服务端通过发送 [response.text.done](https://help.aliyun.com/zh/model-studio/live-translator-server-events#d675635a94jfb "") 事件返回完整的翻译文本。

- **输出文本+音频**
  - **文本**

    通过 [response.audio\_transcript.done](https://help.aliyun.com/zh/model-studio/live-translator-server-events#f4d1698567bsm "") 事件返回完整的翻译文本。

  - **音频**

    通过 [response.audio.delta](https://help.aliyun.com/zh/model-studio/live-translator-server-events#a25cc50a15car "") 事件返回 Base64 编码的增量音频数据。

## **支持的模型**

qwen3-livetranslate-flash-realtime 是一款多语言音视频实时翻译模型，可识别 18 种语言，并实时翻译为 10 种语言的音频。

核心特性：

- **多语言支持**：支持 18 种语言和 6 种汉语方言，包括中文、英语、法语、德语、俄语、日语、韩语，以及普通话、粤语、四川话等。

- **视觉增强**：利用视觉内容提升翻译准确性。模型通过分析画面中的口型、动作和文字，改善在嘈杂环境下或一词多义场景中的翻译效果。

- **3秒延迟**：实现低至 3 秒的同传延迟。

- **无损同传**：通过语义单元预测技术，解决跨语言语序问题。实时翻译质量接近离线翻译结果。

- **音色自然**：生成音色自然的拟人语音。模型能根据源语音内容，自适应调节语气和情感。


| **模型名称** | **版本** | **上下文长度** | **最大输入** | **最大输出** |
| --- | --- | --- | --- | --- |
| **（Token数）** |
| --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **模型名称** | **版本** | **上下文长度** | **最大输入** | **最大输出** |
| **（Token数）** |
| **qwen3-livetranslate-flash-realtime**<br>> 当前能力等同 qwen3-livetranslate-flash-realtime-2025-09-22 | 稳定版 | 53,248 | 49,152 | 4,096 |
| qwen3-livetranslate-flash-realtime-2025-09-22 | 快照版 |

## **快速开始**

1. **准备运行环境**

您的 Python 版本需要不低于 3.10。

首先安装 pyaudio。






macOS



Debian/Ubuntu



CentOS



Windows

































```bash
brew install portaudio && pip install pyaudio
```



















```bash
sudo apt-get install python3-pyaudio

或者

pip install pyaudio
```



















```bash
sudo yum install -y portaudio portaudio-devel && pip install pyaudio
```



















```powershell
pip install pyaudio
```




安装完成后，通过 pip 安装 websocket 相关的依赖：















```bash
pip install websocket-client==1.8.0 websockets
```

2. **创建客户端**

在本地新建一个 Python 文件，命名为`livetranslate_client.py`，并将以下代码复制进文件中：



客户端代码-livetranslate\_client.py




















```python
import os
import time
import base64
import asyncio
import json
import websockets
import pyaudio
import queue
import threading
import traceback

class LiveTranslateClient:
       def __init__(self, api_key: str, target_language: str = "en", voice: str | None = "Cherry", *, audio_enabled: bool = True):
           if not api_key:
               raise ValueError("API key cannot be empty.")

           self.api_key = api_key
           self.target_language = target_language
           self.audio_enabled = audio_enabled
           self.voice = voice if audio_enabled else "Cherry"
           self.ws = None
           self.api_url = "wss://dashscope.aliyuncs.com/api-ws/v1/realtime?model=qwen3-livetranslate-flash-realtime"

           # 音频输入配置 (来自麦克风)
           self.input_rate = 16000
           self.input_chunk = 1600
           self.input_format = pyaudio.paInt16
           self.input_channels = 1

           # 音频输出配置 (用于播放)
           self.output_rate = 24000
           self.output_chunk = 2400
           self.output_format = pyaudio.paInt16
           self.output_channels = 1

           # 状态管理
           self.is_connected = False
           self.audio_player_thread = None
           self.audio_playback_queue = queue.Queue()
           self.pyaudio_instance = pyaudio.PyAudio()

       async def connect(self):
           """建立到翻译服务的 WebSocket 连接。"""
           headers = {"Authorization": f"Bearer {self.api_key}"}
           try:
               self.ws = await websockets.connect(self.api_url, additional_headers=headers)
               self.is_connected = True
               print(f"成功连接到服务端: {self.api_url}")
               await self.configure_session()
           except Exception as e:
               print(f"连接失败: {e}")
               self.is_connected = False
               raise

       async def configure_session(self):
           """配置翻译会话，设置目标语言、声音等。"""
           config = {
               "event_id": f"event_{int(time.time() * 1000)}",
               "type": "session.update",
               "session": {
                   # 'modalities' 控制输出类型。
                   # ["text", "audio"]: 同时返回翻译文本和合成音频（推荐）。
                   # ["text"]: 仅返回翻译文本。
                   "modalities": ["text", "audio"] if self.audio_enabled else ["text"],
                   **({"voice": self.voice} if self.audio_enabled and self.voice else {}),
                   "input_audio_format": "pcm",
                   "output_audio_format": "pcm",
                   # 'input_audio_transcription' 配置源语言识别。
                   # 设置 'model' 为 'qwen3-asr-flash-realtime' 可同时输出源语言识别结果。
                   # "input_audio_transcription": {
                   #     "model": "qwen3-asr-flash-realtime",
                   #     "language": "zh"  # 源语言，默认 'en'
                   # },
                   "translation": {
                       "language": self.target_language
                   }
               }
           }
           print(f"发送会话配置: {json.dumps(config, indent=2, ensure_ascii=False)}")
           await self.ws.send(json.dumps(config))

       async def send_audio_chunk(self, audio_data: bytes):
           """将音频数据块编码并发送到服务端。"""
           if not self.is_connected:
               return

           event = {
               "event_id": f"event_{int(time.time() * 1000)}",
               "type": "input_audio_buffer.append",
               "audio": base64.b64encode(audio_data).decode()
           }
           await self.ws.send(json.dumps(event))

       async def send_image_frame(self, image_bytes: bytes, *, event_id: str | None = None):
           #将图像数据发送到服务端
           if not self.is_connected:
               return

           if not image_bytes:
               raise ValueError("image_bytes 不能为空")

           # 编码为 Base64
           image_b64 = base64.b64encode(image_bytes).decode()

           event = {
               "event_id": event_id or f"event_{int(time.time() * 1000)}",
               "type": "input_image_buffer.append",
               "image": image_b64,
           }

           await self.ws.send(json.dumps(event))

       def _audio_player_task(self):
           stream = self.pyaudio_instance.open(
               format=self.output_format,
               channels=self.output_channels,
               rate=self.output_rate,
               output=True,
               frames_per_buffer=self.output_chunk,
           )
           try:
               while self.is_connected or not self.audio_playback_queue.empty():
                   try:
                       audio_chunk = self.audio_playback_queue.get(timeout=0.1)
                       if audio_chunk is None: # 结束信号
                           break
                       stream.write(audio_chunk)
                       self.audio_playback_queue.task_done()
                   except queue.Empty:
                       continue
           finally:
               stream.stop_stream()
               stream.close()

       def start_audio_player(self):
           """启动音频播放线程（仅当启用音频输出时）。"""
           if not self.audio_enabled:
               return
           if self.audio_player_thread is None or not self.audio_player_thread.is_alive():
               self.audio_player_thread = threading.Thread(target=self._audio_player_task, daemon=True)
               self.audio_player_thread.start()

       async def handle_server_messages(self, on_text_received):
           """循环处理来自服务端的消息。"""
           try:
               async for message in self.ws:
                   event = json.loads(message)
                   event_type = event.get("type")
                   if event_type == "response.audio.delta" and self.audio_enabled:
                       audio_b64 = event.get("delta", "")
                       if audio_b64:
                           audio_data = base64.b64decode(audio_b64)
                           self.audio_playback_queue.put(audio_data)

                   elif event_type == "response.done":
                       print("\n[INFO] 一轮响应完成。")
                       usage = event.get("response", {}).get("usage", {})
                       if usage:
                           print(f"[INFO] Token 使用情况: {json.dumps(usage, indent=2, ensure_ascii=False)}")
                   # 处理源语言识别结果（需启用 input_audio_transcription.model）
                   # elif event_type == "conversation.item.input_audio_transcription.text":
                   #     stash = event.get("stash", "")  # 待确认的识别文本
                   #     print(f"[识别中] {stash}")
                   # elif event_type == "conversation.item.input_audio_transcription.completed":
                   #     transcript = event.get("transcript", "")  # 完整识别结果
                   #     print(f"[源语言] {transcript}")
                   elif event_type == "response.audio_transcript.done":
                       print("\n[INFO] 翻译文本完成。")
                       text = event.get("transcript", "")
                       if text:
                           print(f"[INFO] 翻译文本: {text}")
                   elif event_type == "response.text.done":
                       print("\n[INFO] 翻译文本完成。")
                       text = event.get("text", "")
                       if text:
                           print(f"[INFO] 翻译文本: {text}")

           except websockets.exceptions.ConnectionClosed as e:
               print(f"[WARNING] 连接已关闭: {e}")
               self.is_connected = False
           except Exception as e:
               print(f"[ERROR] 消息处理时发生未知错误: {e}")
               traceback.print_exc()
               self.is_connected = False

       async def start_microphone_streaming(self):
           """从麦克风捕获音频并流式传输到服务端。"""
           stream = self.pyaudio_instance.open(
               format=self.input_format,
               channels=self.input_channels,
               rate=self.input_rate,
               input=True,
               frames_per_buffer=self.input_chunk
           )
           print("麦克风已启动，请开始说话...")
           try:
               while self.is_connected:
                   audio_chunk = await asyncio.get_event_loop().run_in_executor(
                       None, stream.read, self.input_chunk
                   )
                   await self.send_audio_chunk(audio_chunk)
           finally:
               stream.stop_stream()
               stream.close()

       async def close(self):
           """优雅地关闭连接和资源。"""
           self.is_connected = False
           if self.ws:
               await self.ws.close()
               print("WebSocket 连接已关闭。")

           if self.audio_player_thread:
               self.audio_playback_queue.put(None) # 发送结束信号
               self.audio_player_thread.join(timeout=1)
               print("音频播放线程已停止。")

           self.pyaudio_instance.terminate()
           print("PyAudio 实例已释放。")
```

3. **与模型互动**

在`livetranslate_client.py`的同级目录下新建另一个 Python 文件，命名为`main.py`，并将以下代码复制进文件中：



**main.py**




















```python
import os
import asyncio
from livetranslate_client import LiveTranslateClient

def print_banner():
       print("=" * 60)
       print("  基于千问 qwen3-livetranslate-flash-realtime")
       print("=" * 60 + "\n")

def get_user_config():
       """获取用户配置"""
       print("请选择模式:")
       print("1. 语音+文本 [默认] | 2. 仅文本")
       mode_choice = input("请输入选项 (直接回车选择语音+文本): ").strip()
       audio_enabled = (mode_choice != "2")

       if audio_enabled:
           lang_map = {
               "1": "en", "2": "zh", "3": "ru", "4": "fr", "5": "de", "6": "pt",
               "7": "es", "8": "it", "9": "ko", "10": "ja", "11": "yue"
           }
           print("请选择翻译目标语言 (音频+文本 模式):")
           print("1. 英语 | 2. 中文 | 3. 俄语 | 4. 法语 | 5. 德语 | 6. 葡萄牙语 | 7. 西班牙语 | 8. 意大利语 | 9. 韩语 | 10. 日语 | 11. 粤语")
       else:
           lang_map = {
               "1": "en", "2": "zh", "3": "ru", "4": "fr", "5": "de", "6": "pt", "7": "es", "8": "it",
               "9": "id", "10": "ko", "11": "ja", "12": "vi", "13": "th", "14": "ar",
               "15": "yue", "16": "hi", "17": "el", "18": "tr"
           }
           print("请选择翻译目标语言 (仅文本 模式):")
           print("1. 英语 | 2. 中文 | 3. 俄语 | 4. 法语 | 5. 德语 | 6. 葡萄牙语 | 7. 西班牙语 | 8. 意大利语 | 9. 印尼语 | 10. 韩语 | 11. 日语 | 12. 越南语 | 13. 泰语 | 14. 阿拉伯语 | 15. 粤语 | 16. 印地语 | 17. 希腊语 | 18. 土耳其语")

       choice = input("请输入选项 (默认取第一个): ").strip()
       target_language = lang_map.get(choice, next(iter(lang_map.values())))

       voice = None
       if audio_enabled:
           print("\n请选择语音合成声音:")
           voice_map = {"1": "Cherry", "2": "Nofish", "3": "Sunny", "4": "Jada", "5": "Dylan", "6": "Peter", "7": "Eric", "8": "Kiki"}
           print("1. Cherry (女声) [默认] | 2. Nofish (男声) | 3. 晴儿 Sunny (四川女声) | 4. 阿珍 Jada (上海女声) | 5. 晓东 Dylan (北京男声) | 6. 李彼得 Peter (天津男声) | 7. 程川 Eric (四川男声) | 8. 阿清 Kiki (粤语女声)")
           voice_choice = input("请输入选项 (直接回车选择Cherry): ").strip()
           voice = voice_map.get(voice_choice, "Cherry")
       return target_language, voice, audio_enabled

async def main():
       """主程序入口"""
       print_banner()

       api_key = os.environ.get("DASHSCOPE_API_KEY")
       if not api_key:
           print("[ERROR] 请设置环境变量 DASHSCOPE_API_KEY")
           print("  例如: export DASHSCOPE_API_KEY='your_api_key_here'")
           return

       target_language, voice, audio_enabled = get_user_config()
       print("\n配置完成:")
       print(f"  - 目标语言: {target_language}")
       if audio_enabled:
           print(f"  - 合成声音: {voice}")
       else:
           print("  - 输出模式: 仅文本")

       client = LiveTranslateClient(api_key=api_key, target_language=target_language, voice=voice, audio_enabled=audio_enabled)

       # 定义回调函数
       def on_translation_text(text):
           print(text, end="", flush=True)

       try:
           print("正在连接到翻译服务...")
           await client.connect()

           # 根据模式启动音频播放
           client.start_audio_player()

           print("\n" + "-" * 60)
           print("连接成功！请对着麦克风说话。")
           print("程序将实时翻译您的语音并播放结果。按 Ctrl+C 退出。")
           print("-" * 60 + "\n")

           # 并发运行消息处理和麦克风录音
           message_handler = asyncio.create_task(client.handle_server_messages(on_translation_text))
           tasks = [message_handler]
           # 无论是否启用音频输出，都需要从麦克风捕获音频进行翻译
           microphone_streamer = asyncio.create_task(client.start_microphone_streaming())
           tasks.append(microphone_streamer)

           await asyncio.gather(*tasks)

       except KeyboardInterrupt:
           print("\n\n用户中断，正在退出...")
       except Exception as e:
           print(f"\n发生严重错误: {e}")
       finally:
           print("\n正在清理资源...")
           await client.close()
           print("程序已退出。")

if __name__ == "__main__":
       asyncio.run(main())
```






运行`main.py`，通过麦克风说出要翻译的句子，模型会实时返回翻译完成的音频与文本。系统会检测您的音频起始位置并自动发送到服务端，无需手动发送。


## 利用图像提升翻译准确率

qwen3-livetranslate-flash-realtime 模型可以接收图像输入，辅助音频翻译，适用于同音异义、低频专有名词识别场景。建议每秒发送不超过2张图片。

将以下示例图片下载到本地： [口罩.png](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/wbclir/%E5%8F%A3%E7%BD%A9.png) [面具.png](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250923/ohelwv/%E9%9D%A2%E5%85%B7.png)

将以下代码下载到`livetranslate_client.py`同级目录并运行，向麦克风说`"What is mask?"`，在输入口罩图片时，模型会翻译为“什么是口罩？”；输入面具图片时，模型会翻译为“什么是面具？”

```python
import os
import time
import json
import asyncio
import contextlib
import functools

from livetranslate_client import LiveTranslateClient

IMAGE_PATH = "口罩.png"
# IMAGE_PATH = "面具.png"

def print_banner():
    print("=" * 60)
    print("  基于千问 qwen3-livetranslate-flash-realtime —— 单轮交互示例 (mask)")
    print("=" * 60 + "\n")

async def stream_microphone_once(client: LiveTranslateClient, image_bytes: bytes):
    pa = client.pyaudio_instance
    stream = pa.open(
        format=client.input_format,
        channels=client.input_channels,
        rate=client.input_rate,
        input=True,
        frames_per_buffer=client.input_chunk,
    )
    print(f"[INFO] 开始录音，请讲话……")
    loop = asyncio.get_event_loop()
    last_img_time = 0.0
    frame_interval = 0.5  # 2 fps
    try:
        while client.is_connected:
            data = await loop.run_in_executor(None, stream.read, client.input_chunk)
            await client.send_audio_chunk(data)

            # 每 0.5 秒追加一帧图片
            now = time.time()
            if now - last_img_time >= frame_interval:
                await client.send_image_frame(image_bytes)
                last_img_time = now
    finally:
        stream.stop_stream()
        stream.close()

async def main():
    print_banner()
    api_key = os.environ.get("DASHSCOPE_API_KEY")
    if not api_key:
        print("[ERROR] 请先在环境变量 DASHSCOPE_API_KEY 中配置 API KEY")
        return

    client = LiveTranslateClient(api_key=api_key, target_language="zh", voice="Cherry", audio_enabled=True)

    def on_text(text: str):
        print(text, end="", flush=True)

    try:
        await client.connect()
        client.start_audio_player()
        message_task = asyncio.create_task(client.handle_server_messages(on_text))
        with open(IMAGE_PATH, "rb") as f:
            img_bytes = f.read()
        await stream_microphone_once(client, img_bytes)
        await asyncio.sleep(15)
    finally:
        await client.close()
        if not message_task.done():
            message_task.cancel()
            with contextlib.suppress(asyncio.CancelledError):
                await message_task

if __name__ == "__main__":
    asyncio.run(main())
```

## **通过函数计算一键部署**

控制台暂不支持体验。可通过以下方式一键部署：

1. 打开我们写好的[函数计算模板](https://fcnext.console.aliyun.com/applications/create?template=qwen-livetranslate-flash-realtime@0.0.1)，填入 API Key， 单击 **创建并部署默认环境** 即可在线体验。

2. 等待约一分钟，在 **环境详情 \> 环境信息** 中获取访问域名， **将访问域名的**`http` **改成**`https`（例如https://qwen-livetranslate-flash-realtime.fcv3.xxx.cn-hangzhou.fc.devsapp.net/），通过该链接与模型交互。



**重要**





此链接使用自签名证书，仅用于临时测试。首次访问时，浏览器会显示安全警告，这是预期行为， **请勿在生产环境使用**。如需继续，请按浏览器提示操作（如点击“高级” → “继续前往（不安全）”）。


> 如需开通访问控制权限，请跟随页面指引操作。

> 通过 **资源信息**- **函数资源** 查看项目源代码。

> [函数计算](https://help.aliyun.com/zh/functioncompute/fc/product-overview/trial-quota-1 "") 与 [阿里云百炼](https://help.aliyun.com/zh/model-studio/new-free-quota "") 均为新用户提供免费额度，可以覆盖简单调试所需成本，额度耗尽后按量计费。只有在访问的情况下会产生费用。

## **交互流程**

实时语音翻译的交互流程遵循标准的 WebSocket 事件驱动模型，服务端自动检测语音起止并进行响应。

| **生命周期** | **客户端事件** | **服务端事件** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **生命周期** | **客户端事件** | **服务端事件** |
| 会话初始化 | session.update<br>> 会话配置 | session.created<br>> 会话已创建<br>session.updated<br>> 会话配置已更新 |
| 用户音频输入 | input\_audio\_buffer.append<br>> 添加音频到缓冲区<br>input\_image\_buffer.append<br>> 添加图片到缓冲区 | 无 |
| 服务端音频输出 | 无 | response.created<br>> 服务端开始生成响应<br>response.output\_item.added<br>> 响应时有新的输出内容<br>response.content\_part.added<br>> 新的输出内容添加到assistant message<br>response.audio\_transcript.text<br>> 增量生成的转录文字<br>response.audio.delta<br>> 模型增量生成的音频<br>response.audio\_transcript.done<br>> 文本转录完成<br>response.audio.done<br>> 音频生成完成<br>response.content\_part.done<br>> Assistant message 的文本或音频内容流式输出完成<br>response.output\_item.done<br>> Assistant message 的整个输出项流式传输完成<br>response.done<br>> 响应完成 |

## **API 参考**

请参见 [实时音视频翻译（Qwen-Livetranslate-Realtime）](https://help.aliyun.com/zh/model-studio/live-translator-api/ "")。

## **计费说明**

- **音频**：输入或输出每秒音频均消耗 12.5 Token。

- **图片**：每输入 28\*28 像素消耗 0.5 Token。

- **文本**：启用源语言语音识别功能后，服务除返回翻译结果外，还会返回输入音频的语音识别文本（即源语言原文），该识别文本将按输出文本的 Token 标准计费。


Token 费用请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

## **支持的语种**

下表中的语种代码可用于指定源语种与目标语种。

> 部分目标语种仅支持输出文本，不支持输出音频。

| **语种代码** | **语种** | **支持的输出模态** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **语种代码** | **语种** | **支持的输出模态** |
| en | 英语 | 音频+文本 |
| zh | 中文 | 音频+文本 |
| ru | 俄语 | 音频+文本 |
| fr | 法语 | 音频+文本 |
| de | 德语 | 音频+文本 |
| pt | 葡萄牙语 | 音频+文本 |
| es | 西班牙语 | 音频+文本 |
| it | 意大利语 | 音频+文本 |
| id | 印尼语 | 文本 |
| ko | 韩语 | 音频+文本 |
| ja | 日语 | 音频+文本 |
| vi | 越南语 | 文本 |
| th | 泰语 | 文本 |
| ar | 阿拉伯语 | 文本 |
| yue | 粤语 | 音频+文本 |
| hi | 印地语 | 文本 |
| el | 希腊语 | 文本 |
| tr | 土耳其语 | 文本 |

## **支持的音色**

| **音色名** | `voice` **参数** | **音色效果** | **描述** | **支持的语种** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **音色名** | `voice` **参数** | **音色效果** | **描述** | **支持的语种** |
| 芊悦 | Cherry |  | 阳光积极、亲切自然小姐姐。 | 中文、英语、法语、德语、俄语、意大利语、西班牙语、葡萄牙语、日语、韩语 |
| 不吃鱼 | Nofish |  | 不会翘舌音的设计师。 | 中文、英语、法语、德语、俄语、意大利语、西班牙语、葡萄牙语、日语、韩语 |
| 上海-阿珍 | Jada |  | 风风火火的沪上阿姐。 | 中文 |
| 北京-晓东 | Dylan |  | 北京胡同里长大的少年。 | 中文 |
| 四川-晴儿 | Sunny |  | 甜到你心里的川妹子。 | 中文 |
| 天津-李彼得 | Peter |  | 天津相声，专业捧人。 | 中文 |
| 粤语-阿清 | Kiki |  | 甜美的港妹闺蜜。 | 粤语 |
| 四川-程川 | Eric |  | 一个跳脱市井的四川成都男子。 | 中文 |