### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音合成](https://help.aliyun.com/zh/model-studio/speech-synthesis-api-reference/)[实时语音合成（CosyVoice）](https://help.aliyun.com/zh/model-studio/cosyvoice-large-model-for-speech-synthesis/)Python SDK

# 语音合成CosyVoice Python SDK

更新时间：2026-02-10 08:56:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Java SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk)[下一篇：WebSocket API](https://help.aliyun.com/zh/model-studio/cosyvoice-websocket-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

模型与价格

语音合成文本限制与格式规范

文本长度限制

字符计算规则

编码格式

数学表达式支持说明

SSML标记语言支持说明

快速开始

非流式调用

单向流式调用

双向流式调用

请求参数

关键接口

SpeechSynthesizer类

回调接口（ResultCallback）

响应结果

错误码

更多示例

常见问题

功能特性/计量计费/限流

故障排查

权限与认证

更多问题

本文介绍语音合成CosyVoice Python SDK的参数和接口细节。

**用户指南：** 关于模型介绍和选型建议请参见 [实时语音合成-CosyVoice/Sambert](https://help.aliyun.com/zh/model-studio/text-to-speech "")。

## **前提条件**

- 已开通服务并 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。请 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")，而非硬编码在代码中，防范因代码泄露导致的安全风险。





**说明**





当您需要为第三方应用或用户提供临时访问权限，或者希望严格控制敏感数据访问、删除等高风险操作时，建议使用 [临时鉴权Token](https://help.aliyun.com/zh/model-studio/generate-temporary-api-key "")。



与长期有效的 API Key 相比，临时鉴权 Token 具备时效性短（60秒）、安全性高的特点，适用于临时调用场景，能有效降低API Key泄露的风险。



使用方式：在代码中，将原本用于鉴权的 API Key 替换为获取到的临时鉴权 Token 即可。

- [安装最新版DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


## **模型与价格**

参见 [实时语音合成-CosyVoice/Sambert](https://help.aliyun.com/zh/model-studio/text-to-speech "")

## **语音合成文本限制与格式规范**

### **文本长度限制**

- [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#8341058094tc3 "") 或 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#cc2a504f344s2 "")：单次发送文本长度不得超过 20000 字符。

- [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ba023aacfbr84 "")：单次发送文本长度不得超过 20000 字符，且累计发送文本总长度不得超过 20 万字符。


### **字符计算规则**

- 汉字（包括简/繁体汉字、日文汉字和韩文汉字）按2个字符计算，其他所有字符（如标点符号、字母、数字、日韩文假名/谚文等）均按 1个字符计算

- 计算文本长度时，不包含SSML 标签内容

- 示例：

  - `"你好"` → 2(你)+2(好)=4字符

  - `"中A文123"` → 2(中)+1(A)+2(文)+1(1)+1(2)+1(3)=8字符

  - `"中文。"` → 2(中)+2(文)+1(。)=5字符

  - `"中 文。"` → 2(中)+1(空格)+2(文)+1(。)=6字符

  - `"<speak>你好</speak>"` → 2(你)+2(好)=4字符

### **编码格式**

需采用UTF-8编码。

### **数学表达式支持说明**

当前数学表达式解析功能仅适用于`cosyvoice-v2`、`cosyvoice-v3-flash`和`cosyvoice-v3-plus`模型，支持识别中小学常见的数学表达式，包括但不限于基础运算、代数、几何等内容。

详情请参见 [LaTeX 公式转语音](https://help.aliyun.com/zh/model-studio/latex-capability-support-description "")。

### [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") **标记语言支持说明**

当前SSML（Speech Synthesis Markup Language，语音合成标记语言）功能仅适用于cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持的系统音色，使用时需满足以下条件：

- 使用 [DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 1.23.4 或更高版本

- 仅支持 [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#8341058094tc3 "") 和 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#cc2a504f344s2 "")（即 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`call`方法），不支持 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ba023aacfbr84 "")（即 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`streaming_call`方法）

- 使用方法与普通语音合成一致：将包含SSML的文本传入 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`call`方法即可


## **快速开始**

[SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 提供了语音合成的关键接口，支持以下几种调用方式：

- 非流式调用：阻塞式，一次性发送完整文本，直接返回完整音频。适合短文本语音合成场景。

- 单向流式调用：非阻塞式，一次性发送完整文本，通过回调函数接收音频数据（可能分片）。适用于对实时性要求高的短文本语音合成场景。

- 双向流式调用：非阻塞式，可分多次发送文本片段，通过回调函数实时接收增量合成的音频流。适合实时性要求高的长文本语音合成场景。


### **非流式调用**

提交单个语音合成任务，无需调用回调函数，进行语音合成（无流式输出中间结果），最终一次性获取完整结果。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8971370771/CAEQURiBgMDRr9T4phkiIGNmYzBiZjFkZjQ4MDQzZGU4NDIyZDU2NWJjYjkyZTQ04709861_20241015153444.149.svg)

实例化 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 绑定 [请求参数](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#2fe363ace1l4k "")，调用`call`方法进行合成并获取二进制音频数据。

发送的文本长度不得超过20000字符（详情请参见 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`call`方法）。

**重要**

每次调用`call`方法前，需要重新初始化`SpeechSynthesizer`实例。

点击查看完整示例

```python
# coding=utf-8

import dashscope
from dashscope.audio.tts_v2 import *
import os

# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 若没有配置环境变量，请用百炼API Key将下行替换为：dashscope.api_key = "sk-xxx"
dashscope.api_key = os.environ.get('DASHSCOPE_API_KEY')

# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
dashscope.base_websocket_api_url='wss://dashscope.aliyuncs.com/api-ws/v1/inference'

# 模型
model = "cosyvoice-v3-flash"
# 音色
voice = "longanyang"

# 实例化SpeechSynthesizer，并在构造方法中传入模型（model）、音色（voice）等请求参数
synthesizer = SpeechSynthesizer(model=model, voice=voice)
# 发送待合成文本，获取二进制音频
audio = synthesizer.call("今天天气怎么样？")
# 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
print('[Metric] requestId为：{}，首包延迟为：{}毫秒'.format(
    synthesizer.get_last_request_id(),
    synthesizer.get_first_package_delay()))

# 将音频保存至本地
with open('output.mp3', 'wb') as f:
    f.write(audio)
```

### **单向流式调用**

提交单个语音合成任务，通过回调的方式流式输出中间结果，合成结果通过`ResultCallback`中的回调函数流式获取。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9971370771/CAEQVRiBgIDv9fShrBkiIDhmNTk5YmQ1ZDgwNzRjZjRiN2VlMTU5YzI1ZGMwMTlm4709861_20241015153444.149.svg)

实例化 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 绑定 [请求参数](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#2fe363ace1l4k "") 和 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "")，调用`call`方法进行合成并通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "") 的`on_data`方法实时获取合成结果。

发送的文本长度不得超过20000字符（详情请参见 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`call`方法）。

**重要**

每次调用`call`方法前，需要重新初始化`SpeechSynthesizer`实例。

点击查看完整示例

```python
# coding=utf-8

import os
import dashscope
from dashscope.audio.tts_v2 import *

from datetime import datetime

def get_timestamp():
    now = datetime.now()
    formatted_timestamp = now.strftime("[%Y-%m-%d %H:%M:%S.%f]")
    return formatted_timestamp

# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 若没有配置环境变量，请用百炼API Key将下行替换为：dashscope.api_key = "sk-xxx"
dashscope.api_key = os.environ.get('DASHSCOPE_API_KEY')

# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
dashscope.base_websocket_api_url='wss://dashscope.aliyuncs.com/api-ws/v1/inference'

# 模型
model = "cosyvoice-v3-flash"
# 音色
voice = "longanyang"

# 定义回调接口
class Callback(ResultCallback):
    _player = None
    _stream = None

    def on_open(self):
        self.file = open("output.mp3", "wb")
        print("连接建立：" + get_timestamp())

    def on_complete(self):
        print("语音合成完成，所有合成结果已被接收：" + get_timestamp())
        # 当任务完成（on_complete 回调触发）后，才可调用 get_first_package_delay 获取延迟
        # 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        print('[Metric] requestId为：{}，首包延迟为：{}毫秒'.format(
            synthesizer.get_last_request_id(),
            synthesizer.get_first_package_delay()))

    def on_error(self, message: str):
        print(f"语音合成出现异常：{message}")

    def on_close(self):
        print("连接关闭：" + get_timestamp())
        self.file.close()

    def on_event(self, message):
        pass

    def on_data(self, data: bytes) -> None:
        print(get_timestamp() + " 二进制音频长度为：" + str(len(data)))
        self.file.write(data)

callback = Callback()

# 实例化SpeechSynthesizer，并在构造方法中传入模型（model）、音色（voice）等请求参数
synthesizer = SpeechSynthesizer(
    model=model,
    voice=voice,
    callback=callback,
)

# 发送待合成文本，在回调接口的on_data方法中实时获取二进制音频
synthesizer.call("今天天气怎么样？")
```

### **双向流式调用**

在同一个语音合成任务中分多次提交文本，并通过回调的方式实时获取合成结果。

**说明**

- 流式输入时可多次调用`streaming_call`按顺序提交文本片段。服务端接收文本片段后自动进行分句：


  - 完整语句立即合成

  - 不完整语句缓存至完整后合成


调用 `streaming_complete` 时，服务端会强制合成所有已接收但未处理的文本片段（包括未完成的句子）。

- 发送文本片段的间隔不得超过23秒，否则触发“request timeout after 23 seconds”异常。

若无待发送文本，需及时调用 `streaming_complete`结束任务。


> 服务端强制设定23秒超时机制，客户端无法修改该配置。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9971370771/CAEQVRiBgMDb7PahrBkiIDVkNjEwOTMxYjEwOTRmOWFhMmI1OTRiY2Q3ZDgzZmE54709861_20241015153444.149.svg)

1. 实例化SpeechSynthesizer类

实例化 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 绑定 [请求参数](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#2fe363ace1l4k "") 和 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "")。

2. 流式传输

多次调用 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`streaming_call`方法分片提交待合成文本，将待合成文本分段发送至服务端。

在发送文本的过程中，服务端会通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "") 的`on_data`方法，将合成结果实时返回给客户端。

每次调用`streaming_call`方法发送的文本片段（即`text`）长度不得超过20000字符，累计发送的文本总长度不得超过20万字符。

3. 结束处理

调用 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`streaming_complete`方法结束语音合成。

该方法会阻塞当前线程，直到 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "") 的`on_complete`或者`on_error`回调触发后才会释放线程阻塞。

请务必确保调用该方法，否则可能会导致结尾部分的文本无法成功转换为语音。


点击查看完整示例

```python
# coding=utf-8
#
# pyaudio安装说明：
# 如果是macOS操作系统，执行如下命令：
#   brew install portaudio
#   pip install pyaudio
# 如果是Debian/Ubuntu操作系统，执行如下命令：
#   sudo apt-get install python-pyaudio python3-pyaudio
#   或者
#   pip install pyaudio
# 如果是CentOS操作系统，执行如下命令：
#   sudo yum install -y portaudio portaudio-devel && pip install pyaudio
# 如果是Microsoft Windows，执行如下命令：
#   python -m pip install pyaudio

import os
import time
import pyaudio
import dashscope
from dashscope.api_entities.dashscope_response import SpeechSynthesisResponse
from dashscope.audio.tts_v2 import *

from datetime import datetime

def get_timestamp():
    now = datetime.now()
    formatted_timestamp = now.strftime("[%Y-%m-%d %H:%M:%S.%f]")
    return formatted_timestamp

# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 若没有配置环境变量，请用百炼API Key将下行替换为：dashscope.api_key = "sk-xxx"
dashscope.api_key = os.environ.get('DASHSCOPE_API_KEY')

# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
dashscope.base_websocket_api_url='wss://dashscope.aliyuncs.com/api-ws/v1/inference'

# 模型
model = "cosyvoice-v3-flash"
# 音色
voice = "longanyang"

# 定义回调接口
class Callback(ResultCallback):
    _player = None
    _stream = None

    def on_open(self):
        print("连接建立：" + get_timestamp())
        self._player = pyaudio.PyAudio()
        self._stream = self._player.open(
            format=pyaudio.paInt16, channels=1, rate=22050, output=True
        )

    def on_complete(self):
        print("语音合成完成，所有合成结果已被接收：" + get_timestamp())

    def on_error(self, message: str):
        print(f"语音合成出现异常：{message}")

    def on_close(self):
        print("连接关闭：" + get_timestamp())
        # 停止播放器
        self._stream.stop_stream()
        self._stream.close()
        self._player.terminate()

    def on_event(self, message):
        pass

    def on_data(self, data: bytes) -> None:
        print(get_timestamp() + " 二进制音频长度为：" + str(len(data)))
        self._stream.write(data)

callback = Callback()

test_text = [\
    "流式文本语音合成SDK，",\
    "可以将输入的文本",\
    "合成为语音二进制数据，",\
    "相比于非流式语音合成，",\
    "流式合成的优势在于实时性",\
    "更强。用户在输入文本的同时",\
    "可以听到接近同步的语音输出，",\
    "极大地提升了交互体验，",\
    "减少了用户等待时间。",\
    "适用于调用大规模",\
    "语言模型（LLM），以",\
    "流式输入文本的方式",\
    "进行语音合成的场景。",\
]

# 实例化SpeechSynthesizer，并在构造方法中传入模型（model）、音色（voice）等请求参数
synthesizer = SpeechSynthesizer(
    model=model,
    voice=voice,
    format=AudioFormat.PCM_22050HZ_MONO_16BIT,
    callback=callback,
)

# 流式发送待合成文本。在回调接口的on_data方法中实时获取二进制音频
for text in test_text:
    synthesizer.streaming_call(text)
    time.sleep(0.1)
# 结束流式语音合成
synthesizer.streaming_complete()

# 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
print('[Metric] requestId为：{}，首包延迟为：{}毫秒'.format(
    synthesizer.get_last_request_id(),
    synthesizer.get_first_package_delay()))
```

## **请求参数**

请求参数通过 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的构造方法进行设置。

| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| model | str | 是 | 语音合成[模型](https://help.aliyun.com/zh/model-studio/models#7a960cc042zwt "")。<br>不同模型版本需要使用对应版本的音色：<br>- cosyvoice-v3-flash/cosyvoice-v3-plus：使用longanyang等音色。<br>  <br>- cosyvoice-v2：使用longxiaochun\_v2等音色。<br>  <br>- cosyvoice-v1：使用longwan等音色。<br>  <br>- 完整音色列表请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")。 |
| voice | str | 是 | 语音合成所使用的音色。<br>支持系统音色和复刻音色：<br>- **系统音色**：参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")。<br>  <br>- **复刻音色**：通过 [声音复刻](https://help.aliyun.com/zh/model-studio/voice-replica-1/ "") 功能定制。使用复刻音色时，请确保声音复刻与语音合成使用同一账号。详细操作步骤请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api#da30eeebc4uwk "")。<br>  <br>  使用声音复刻生成的复刻音色时，本请求的`model`参数值，必须与创建该音色时所用的模型版本（即`target_model`参数）完全一致。 |
| format | enum | 否 | 指定音频编码格式及采样率。<br>若未指定`format`，则合成音频采样率为22.05kHz，格式为mp3。<br>**说明**<br>默认采样率代表当前音色的最佳采样率，缺省条件下默认按照该采样率输出，同时支持降采样或升采样。<br>可指定的音频编码格式及采样率如下：<br>- 所有模型均支持的音频编码格式及采样率：<br>  <br>  - AudioFormat.WAV\_8000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为8kHz<br>    <br>  - AudioFormat.WAV\_16000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为16kHz<br>    <br>  - AudioFormat.WAV\_22050HZ\_MONO\_16BIT，代表音频格式为wav，采样率为22.05kHz<br>    <br>  - AudioFormat.WAV\_24000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为24kHz<br>    <br>  - AudioFormat.WAV\_44100HZ\_MONO\_16BIT，代表音频格式为wav，采样率为44.1kHz<br>    <br>  - AudioFormat.WAV\_48000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为48kHz<br>    <br>  - AudioFormat.MP3\_8000HZ\_MONO\_128KBPS，代表音频格式为mp3，采样率为8kHz<br>    <br>  - AudioFormat.MP3\_16000HZ\_MONO\_128KBPS，代表音频格式为mp3，采样率为16kHz<br>    <br>  - AudioFormat.MP3\_22050HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为22.05kHz<br>    <br>  - AudioFormat.MP3\_24000HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为24kHz<br>    <br>  - AudioFormat.MP3\_44100HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为44.1kHz<br>    <br>  - AudioFormat.MP3\_48000HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为48kHz<br>    <br>  - AudioFormat.PCM\_8000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为8kHz<br>    <br>  - AudioFormat.PCM\_16000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为16kHz<br>    <br>  - AudioFormat.PCM\_22050HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为22.05kHz<br>    <br>  - AudioFormat.PCM\_24000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为24kHz<br>    <br>  - AudioFormat.PCM\_44100HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为44.1kHz<br>    <br>  - AudioFormat.PCM\_48000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为48kHz<br>- 除`cosyvoice-v1`外，其他模型支持的音频编码格式及采样率：<br>  <br>  音频格式为opus时，支持通过`bit_rate`参数调整码率。仅对1.24.0及之后版本的DashScope适用。<br>  <br>  - AudioFormat.OGG\_OPUS\_8KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为8kHz，码率为32kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_16KHZ\_MONO\_16KBPS，代表音频格式为opus，采样率为16kHz，码率为16kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_16KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为16kHz，码率为32kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_16KHZ\_MONO\_64KBPS，代表音频格式为opus，采样率为16kHz，码率为64kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_24KHZ\_MONO\_16KBPS，代表音频格式为opus，采样率为24kHz，码率为16kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_24KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为24kHz，码率为32kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_24KHZ\_MONO\_64KBPS，代表音频格式为opus，采样率为24kHz，码率为64kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_48KHZ\_MONO\_16KBPS，代表音频格式为opus，采样率为48kHz，码率为16kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_48KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为48kHz，码率为32kbps<br>    <br>  - AudioFormat.OGG\_OPUS\_48KHZ\_MONO\_64KBPS，代表音频格式为opus，采样率为48kHz，码率为64kbps |
| volume | int | 否 | 音量。<br>默认值：50。<br>取值范围：\[0, 100\]。50代表标准音量。音量大小与该值呈线性关系，0为静音，100为最大音量。<br>**重要**<br>该字段在不同版本的DashScope SDK中有所不同：<br>- 1.20.10及以后版本的SDK：volume<br>  <br>- 1.20.10以前版本的SDK：volumn |
| speech\_rate | float | 否 | 语速。<br>默认值：1.0。<br>取值范围：\[0.5, 2.0\]。1.0为标准语速，小于1.0则减慢，大于1.0则加快。 |
| pitch\_rate | float | 否 | 音高。该值作为音高调节的乘数，但其与听感上的音高变化并非严格的线性或对数关系，建议通过测试选择合适的值。<br>默认值：1.0。<br>取值范围：\[0.5, 2.0\]。1.0为音色自然音高。大于1.0则音高变高，小于1.0则音高变低。 |
| bit\_rate | int | 否 | 音频码率（单位kbps）。音频格式为opus时，支持通过`bit_rate`参数调整码率。<br>默认值：32。<br>取值范围：\[6, 510\]。<br>`cosyvoice-v1`模型不支持该参数。<br>**说明**<br>`bit_rate`需要通过`additional_params`参数进行设置：<br>```python<br>synthesizer = SpeechSynthesizer(model="cosyvoice-v3-flash",<br>                                voice="longanyang",<br>                                format=AudioFormat.OGG_OPUS_16KHZ_MONO_16KBPS,<br>                                additional_params={"bit_rate": 32})<br>``` |
| word\_timestamp\_enabled | bool | 否 | 是否开启字级别时间戳。<br>默认值：False。<br>- True：开启。<br>  <br>- False：关闭。<br>  <br>该功能仅适用于cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持的系统音色。<br>> 时间戳结果仅能通过回调接口获取<br>**说明**<br>`word_timestamp_enabled`需要通过`additional_params`参数进行设置：<br>```python<br>synthesizer = SpeechSynthesizer(model="cosyvoice-v3-flash",<br>                                voice="longyingjing_v3",<br>                                callback=callback, # 时间戳结果仅能通过回调接口获取<br>                                additional_params={'word_timestamp_enabled': True})<br>```<br>**点击查看完整示例代码**<br>```python<br># coding=utf-8<br>import dashscope<br>from dashscope.audio.tts_v2 import *<br>import json<br>from datetime import datetime<br>def get_timestamp():<br>    now = datetime.now()<br>    formatted_timestamp = now.strftime("[%Y-%m-%d %H:%M:%S.%f]")<br>    return formatted_timestamp<br># 若没有将API Key配置到环境变量中，需将your-api-key替换为自己的API Key<br># dashscope.api_key = "your-api-key"<br>model = "cosyvoice-v3-flash"<br># 音色<br>voice = "longyingjing_v3"<br># 定义回调接口<br>class Callback(ResultCallback):<br>    _player = None<br>    _stream = None<br>    def on_open(self):<br>        self.file = open("output.mp3", "wb")<br>        print("连接建立：" + get_timestamp())<br>    def on_complete(self):<br>        print("语音合成完成，所有合成结果已被接收：" + get_timestamp())<br>    def on_error(self, message: str):<br>        print(f"语音合成出现异常：{message}")<br>    def on_close(self):<br>        print("连接关闭：" + get_timestamp())<br>        self.file.close()<br>    def on_event(self, message):<br>        json_data = json.loads(message)<br>        if json_data['payload'] and json_data['payload']['output'] and json_data['payload']['output']['sentence']:<br>            sentence = json_data['payload']['output']['sentence']<br>            print(f'sentence: {sentence}')<br>            # 获取句子的编号<br>            # index = sentence['index']<br>            words = sentence['words']<br>            if words:<br>                for word in words:<br>                    print(f'word: {word}')<br>                    # 示例值：word: {'text': '今', 'begin_index': 0, 'end_index': 1, 'begin_time': 80, 'end_time': 200}<br>    def on_data(self, data: bytes) -> None:<br>        print(get_timestamp() + " 二进制音频长度为：" + str(len(data)))<br>        self.file.write(data)<br>callback = Callback()<br># 实例化SpeechSynthesizer，并在构造方法中传入模型（model）、音色（voice）等请求参数<br>synthesizer = SpeechSynthesizer(<br>    model=model,<br>    voice=voice,<br>    callback=callback,<br>    additional_params={'word_timestamp_enabled': True}<br>)<br># 发送待合成文本，在回调接口的on_data方法中实时获取二进制音频<br>synthesizer.call("今天天气怎么样？")<br># 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时<br>print('[Metric] requestId为：{}，首包延迟为：{}毫秒'.format(<br>    synthesizer.get_last_request_id(),<br>    synthesizer.get_first_package_delay()))<br>``` |
| seed | int | 否 | 生成时使用的随机数种子，使合成的效果产生变化。在模型版本、文本、音色及其他参数均相同的前提下，使用相同的seed可复现相同的合成结果。<br>默认值0。<br>取值范围：\[0, 65535\]。<br>cosyvoice-v1不支持该功能。 |
| language\_hints | list\[str\] | 否 | 指定语音合成的目标语言，提升合成效果。cosyvoice-v1不支持该功能。<br>当数字、缩写、符号等朗读方式或者小语种合成效果不符合预期时使用，例如：<br>- 数字朗读方式不符合预期，“hello, this is 110”读成“hello, this is one one zero”而非“hello, this is 幺幺零”<br>  <br>- 符号朗读不准确，“@”读成“艾特”而非“at”<br>  <br>- 小语种合成效果差，合成不自然<br>  <br>取值范围：<br>- zh：中文<br>  <br>- en：英文<br>  <br>- fr：法语<br>  <br>- de：德语<br>  <br>- ja：日语<br>  <br>- ko：韩语<br>  <br>- ru：俄语<br>  <br>**注意**：此参数为数组，但当前版本仅处理第一个元素，因此建议只传入一个值。<br>**重要**<br>此参数用于指定语音合成的目标语言，该设置与声音复刻时的样本音频的语种无关。如果您需要设置复刻任务的源语言，请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api "")。 |
| instruction | str | 否 | 设置指令，用于控制方言、情感或角色等合成效果。该功能仅适用于cosyvoice-v3-flash模型的复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色。<br>**使用要求**：<br>- 指令必须使用固定格式和内容（见下方说明）<br>  <br>- 不设置时不生效（无默认值）<br>  <br>**支持的功能**：<br>- 指定方言<br>  <br>  - 适用音色：仅复刻音色<br>    <br>  - 格式：“`请用<方言>表达。`”（注意，结尾一定不要遗漏句号，使用时将“`<方言>`”替换为具体的`方言`，例如替换为`广东话`）。<br>    <br>  - 示例：“`请用广东话表达。`”<br>    <br>  - 支持的方言：广东话、东北话、甘肃话、贵州话、河南话、湖北话、江西话、闽南话、宁夏话、山西话、陕西话、山东话、上海话、四川话、天津话、云南话。<br>- 指定情感<br>  <br>  - 适用音色<br>    <br>    - 复刻音色<br>      <br>    - [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色<br>  - 格式：<br>    <br>    - 复刻音色：<br>      <br>      <br>      <br>      点击查看复刻音色指令格式<br>      <br>      <br>      <br>      <br>      <br>      <br>      - `请尽可能非常大声地说一句话。`<br>        <br>      - `请用尽可能慢地语速说一句话。`<br>        <br>      - `请用尽可能快地语速说一句话。`<br>        <br>      - `请非常轻声地说一句话。`<br>        <br>      - `你可以慢一点说吗`<br>        <br>      - `你可以非常快一点说吗`<br>        <br>      - `你可以非常慢一点说吗`<br>        <br>      - `你可以快一点说吗`<br>        <br>      - `请非常生气地说一句话。`<br>        <br>      - `请非常开心地说一句话。`<br>        <br>      - `请非常恐惧地说一句话。`<br>        <br>      - `请非常伤心地说一句话。`<br>        <br>      - `请非常惊讶地说一句话。`<br>        <br>      - `请尽可能表现出坚定的感觉。`<br>        <br>      - `请尽可能表现出愤怒的感觉。`<br>        <br>      - `请尝试一下亲和的语调。`<br>        <br>      - `请用冷酷的语调讲话。`<br>        <br>      - `请用威严的语调讲话。`<br>        <br>      - `我想体验一下自然的语气。`<br>        <br>      - `我想看看你如何表达威胁。`<br>        <br>      - `我想看看你怎么表现智慧。`<br>        <br>      - `我想看看你怎么表现诱惑。`<br>        <br>      - `我想听听用活泼的方式说话。`<br>        <br>      - `我想听听你用激昂的感觉说话。`<br>        <br>      - `我想听听用沉稳的方式说话的样子。`<br>        <br>      - `我想听听你用自信的感觉说话。`<br>        <br>      - `你能用兴奋的感觉和我交流吗？`<br>        <br>      - `你能否展示狂傲的情绪表达？`<br>        <br>      - `你能展现一下优雅的情绪吗？`<br>        <br>      - `你可以用幸福的方式回答问题吗？`<br>        <br>      - `你可以做一个温柔的情感演示吗？`<br>        <br>      - `能用冷静的语调和我谈谈吗？`<br>        <br>      - `能用深沉的方法回答我吗？`<br>        <br>      - `能用粗犷的情绪态度和我对话吗？`<br>        <br>      - `用阴森的声音告诉我这个答案。`<br>        <br>      - `用坚韧的声音告诉我这个答案。`<br>        <br>      - `用自然亲切的闲聊风格叙述。`<br>        <br>      - `用广播剧博客主的语气讲话。`<br>        <br>    - 系统音色：系统音色和复刻音色的情感指令格式不同，详情请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")<br>- 指定场景、角色或身份等<br>  <br>  - 适用音色： [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色<br>    <br>  - 格式：请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") |
| enable\_aigc\_tag | bool | 否 | 是否在生成的音频中添加AIGC隐性标识。设置为True时，会将隐性标识嵌入到支持格式（wav/mp3/opus）的音频中。<br>默认值：False。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。<br>**说明**<br>`enable_aigc_tag`需要通过`additional_params`参数进行设置：<br>```python<br>synthesizer = SpeechSynthesizer(model="cosyvoice-v3-flash",<br>                                voice="longanyang",<br>                                format=AudioFormat.OGG_OPUS_16KHZ_MONO_16KBPS,<br>                                additional_params={"enable_aigc_tag": True})<br>``` |
| aigc\_propagator | str | 否 | 设置AIGC隐性标识中的 `ContentPropagator` 字段，用于标识内容的传播者。仅在 `enable_aigc_tag` 为 `True` 时生效。<br>默认值：阿里云UID。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。<br>**说明**<br>`aigc_propagator`需要通过`additional_params`参数进行设置：<br>```python<br>synthesizer = SpeechSynthesizer(model="cosyvoice-v3-flash",<br>                                voice="longanyang",<br>                                format=AudioFormat.OGG_OPUS_16KHZ_MONO_16KBPS,<br>                                additional_params={"enable_aigc_tag": True, "aigc_propagator": "xxxx"})<br>``` |
| aigc\_propagate\_id | str | 否 | 设置AIGC隐性标识中的 `PropagateID` 字段，用于唯一标识一次具体的传播行为。仅在 `enable_aigc_tag` 为 `True` 时生效。<br>默认值：本次语音合成请求Request ID。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。<br>**说明**<br>`aigc_propagate_id`需要通过`additional_params`参数进行设置：<br>```python<br>synthesizer = SpeechSynthesizer(model="cosyvoice-v3-flash",<br>                                voice="longanyang",<br>                                format=AudioFormat.OGG_OPUS_16KHZ_MONO_16KBPS,<br>                                additional_params={"enable_aigc_tag": True, "aigc_propagate_id": "xxxx"})<br>``` |
| callback | ResultCallback | 否 | [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s ""). |

## **关键接口**

### `SpeechSynthesizer`类

`SpeechSynthesizer`通过“`from dashscope.audio.tts_v2 import *`”方式引入，提供语音合成的关键接口。

| **方法** | **参数** | **返回值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **方法** | **参数** | **返回值** | **描述** |
| ```python<br>def call(self, text: str, timeout_millis=None)<br>``` | - `text`：待合成文本<br>  <br>- `timeout_millis`：阻塞线程的超时时间，单位为毫秒，不设置或值为0时不生效 | 没有指定`ResultCallback`时返回二进制音频数据，否则返回None | 将整段文本（无论是纯文本还是包含 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") 的文本）转换为语音。<br>在创建`SpeechSynthesizer`实例时，存在以下两种情况：<br>- 没有指定`ResultCallback`：`call`方法会阻塞当前线程直到语音合成完成并返回二进制音频数据。使用方法请参见 [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#8341058094tc3 "")。<br>  <br>- 指定了`ResultCallback`：`call`方法会立刻返回None，并通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "") 的`on_data`方法返回语音合成的结果。使用方法请参见 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#cc2a504f344s2 "")。<br>  <br>**重要**<br>每次调用`call`方法前，需要重新初始化`SpeechSynthesizer`实例。 |
| ```python<br>def streaming_call(self, text: str)<br>``` | `text`：待合成文本片段 | 无 | 流式发送待合成文本（不支持包含SSML的文本）。<br>您可以多次调用该接口，将待合成文本分多次发送给服务端。合成结果通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "") 的`on_data`方法获取。<br>使用方法请参见 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ba023aacfbr84 "")。 |
| ```python<br>def streaming_complete(self, complete_timeout_millis=600000)<br>``` | `complete_timeout_millis`：等待时间，单位为毫秒 | 无 | 结束流式语音合成。<br>该方法阻塞当前线程N毫秒（具体时长由`complete_timeout_millis`决定），直到任务结束。如果`completeTimeoutMillis`设置为0，则无限期等待。<br>默认情况下，如果等待时间超过10分钟，则停止等待。<br>使用方法请参见 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ba023aacfbr84 "")。<br>**重要**<br>在 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ba023aacfbr84 "") 时，请务必确保调用该方法，否则可能会出现合成语音缺失的问题。 |
| ```python<br>def get_last_request_id(self)<br>``` | 无 | 上一个任务的request\_id | 获取上一个任务的request\_id。 |
| ```python<br>def get_first_package_delay(self)<br>``` | 无 | 首包延迟 | 获取当前任务的首包延迟，任务结束后使用。首包延迟是开始发送文本和接收第一个音频包之间的时间，单位为毫秒。<br>**影响首包延迟的因素：**<br>- WebSocket连接建立耗时（首次调用）<br>  <br>- 音色加载时间（不同音色加载时间不同）<br>  <br>- 服务承载量（高峰期可能出现排队等待）<br>  <br>- 网络延迟<br>  <br>**典型延迟范围：**<br>- 复用连接且音色已加载：500ms左右<br>  <br>- 首次连接或切换音色：可能达到1500~2000ms<br>  <br>若首包延迟持续过高（>2000ms），建议：<br>1. 使用高并发场景下的连接池功能提前建立连接<br>   <br>2. 检查网络连接质量<br>   <br>3. 避免在高峰时段调用 |
| ```python<br>def get_response(self)<br>``` | 无 | 最后一次报文 | 获取最后一次报文（为JSON格式的数据），可以用于获取task-failed报错。 |

### **回调接口（**`ResultCallback`）

[单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#cc2a504f344s2 "") 或 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ba023aacfbr84 "") 时，服务端会通过回调的方式，将关键流程信息和数据返回给客户端。您需要实现回调方法，处理服务端返回的信息或者数据。

通过“`from dashscope.audio.tts_v2 import *`”方式引入。

点击查看示例

```python
class Callback(ResultCallback):
    def on_open(self) -> None:
        print('连接成功')

    def on_data(self, data: bytes) -> None:
        # 实现接收合成二进制音频结果的逻辑

    def on_complete(self) -> None:
        print('合成完成')

    def on_error(self, message) -> None:
        print('出现异常：', message)

    def on_close(self) -> None:
        print('连接关闭')

callback = Callback()
```

| **方法** | **参数** | **返回值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **方法** | **参数** | **返回值** | **描述** |
| ```python<br>def on_open(self) -> None<br>``` | 无 | 无 | 当和服务端建立连接完成后，该方法立刻被回调。 |
| ```python<br>def on_event( self, message: str) -> None<br>``` | `message`：服务端返回的信息 | 无 | 当服务有回复时会被回调。`message`为JSON字符串，解析可获取Task ID（`task_id`参数）、本次请求中计费的有效字符数（`characters`参数）等信息。 |
| ```python<br>def on_complete(self) -> None<br>``` | 无 | 无 | 当所有合成数据全部返回（语音合成完成）后被回调。 |
| ```python<br>def on_error(self, message) -> None<br>``` | `message`：异常信息 | 无 | 发生异常时该方法被回调。 |
| ```python<br>def on_data(self, data: bytes) -> None<br>``` | `data`：服务器返回的二进制音频数据 | 无 | 当服务器有合成音频返回时被回调。<br>您可以将二进制音频数据合成为一个完整的音频文件后使用播放器播放，也可以通过支持流式播放的播放器实时播放。<br>**重要**<br>- 流式语音合成中，对于mp3/opus等压缩格式，音频分段传输需使用流式播放器，不可逐帧播放，避免解码失败。<br>  <br>  <br>> 支持流式播放的播放器：ffmpeg、pyaudio (Python)、AudioFormat (Java)、MediaSource (Javascript)等。<br>  <br>- 将音频数据合成完整的音频文件时，应以追加模式写入同一文件。<br>  <br>- 流式语音合成的wav/mp3 格式音频仅首帧包含头信息，后续帧为纯音频数据。 |
| ```python<br>def on_close(self) -> None<br>``` | 无 | 无 | 当服务已经关闭连接后被回调。 |

## **响应结果**

服务器返回二进制音频数据：

- [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#8341058094tc3 "")：对 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`call`方法返回的二进制音频数据进行处理。

- [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#cc2a504f344s2 "") 或 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ba023aacfbr84 "")：对 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "") 的`on_data`方法的参数（bytes类型数据）进行处理。


## **错误码**

如遇报错问题，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行排查。

## **更多示例**

更多示例，请参见 [GitHub](https://github.com/aliyun/alibabacloud-bailian-speech-demo)。

## **常见问题**

### **功能特性/计量计费/限流**

#### **Q：当遇到发音不准的情况时，有什么解决方案可以尝试？**

通过 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") 可以对语音合成效果进行个性化定制。

#### **Q：** 语音合成是按文本字符数计费的，要如何查看或获取每次合成的文本长度？

根据是否开启日志，有不同的获取方式：

1. 未开启日志

   - [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#8341058094tc3 "")：需要按照字符计算规则自行计算。

   - 其他调用方式：通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "")`on_event`方法的`message`参数获取。`message`为JSON字符串，解析可获取本次请求中计费的有效字符数（`characters`参数）。请以收到的最后一个`message`为准。
2. 开启日志

在控制台会打印如下日志，`characters`即为本次请求中计费的有效字符数。请以打印的最后一个日志为准。















```bash
2025-08-27 11:02:09,429 - dashscope - speech_synthesizer.py - on_message - 454 - DEBUG - <<<recv {"header":{"task_id":"62ebb7d6cb0a4080868f0edb######","event":"result-generated","attributes":{}},"payload":{"output":{"sentence":{"words":[]}},"usage":{"characters":15}}}
```


**点击查看如何开启日志**

通过在命令行设置环境变量开启日志：

- Windows系统：`$env:DASHSCOPE_LOGGING_LEVEL="debug"`

- Linux/macOS系统：`export DASHSCOPE_LOGGING_LEVEL=debug`


### **故障排查**

如遇代码报错问题，请根据 [错误码](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#ca4936efd2bim "") 中的信息进行排查。

#### **Q：如何获取** Request ID **？**

通过以下两种方式可以获取：

- 在 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#85d698b9f9g8s "") 的`on_event`方法中对JSON字符串`message`进行解析。

- 调用 [SpeechSynthesizer](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`get_last_request_id`方法。


#### **Q：使用SSML功能失败是什么原因？**

请按以下步骤排查：

1. 确保 [限制与约束](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#923300b3e9a3z "") 正确

2. [安装最新版本 DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")

3. 确保使用正确的接口：只有 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`call`方法支持SSML

4. 确保待合成文本为纯文本格式且符合格式要求，详情请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "")


#### **Q：为什么音频无法播放？**

请根据以下场景逐一排查：

1. 音频保存为完整文件（如xx.mp3）的情况

1. 音频格式一致性：确保请求参数中设置的音频格式与文件后缀一致。例如，如果请求参数设置的音频格式为wav，但文件后缀为mp3，可能会导致播放失败。

2. 播放器兼容性：确认使用的播放器是否支持该音频文件的格式和采样率。例如，某些播放器可能不支持高采样率或特定编码的音频文件。
2. 流式播放音频的情况

1. 将音频流保存为完整文件，尝试使用播放器播放。如果文件无法播放，请参考场景 1 的排查方法。

2. 如果文件可以正常播放，则问题可能出在流式播放的实现上。请确认使用的播放器是否支持流式播放。

      常见的支持流式播放的工具和库包括：ffmpeg、pyaudio (Python)、AudioFormat (Java)、MediaSource (Javascript)等。

#### **Q：为什么音频播放卡顿？**

请根据以下场景逐一排查：

1. 检查文本发送速度：
确保发送文本的间隔合理，避免前一句音频播放完毕后，下一句文本未能及时发送。

2. 检查回调函数性能：

   - 检查回调函数中是否存在过多业务逻辑，导致阻塞。

   - 回调函数运行在 WebSocket 线程中，若被阻塞，可能会影响 WebSocket 接收网络数据包，进而导致音频接收卡顿。

   - 建议将音频数据写入一个独立的音频缓冲区（audio buffer），然后在其他线程中读取并处理，避免阻塞 WebSocket 线程。
3. 检查网络稳定性：
确保网络连接稳定，避免因网络波动导致音频传输中断或延迟。


#### **Q：语音合成慢（合成时间长）是什么原因？**

请按以下步骤排查：

1. 检查输入间隔

如果是流式语音合成，请确认文字发送间隔是否过长（如上段发出后延迟数秒才发送下段），过久间隔会导致合成总时长增加。

2. 分析性能指标

   - 首包延迟：正常500ms左右。

   - RTF（RTF = 合成总耗时/音频时长）：正常小于1.0。

#### **Q：合成的语音发音错误如何处理？**

请使用SSML的 [<phoneme>标签](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#title-m9h-7yc-48k "") 指定正确的发音。

#### **Q：为什么没有返回语音？为什么结尾部分的文本没能成功转换成语音？（合成语音缺失）**

请检查是否遗漏了调用 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#d6bc1f133f871 "") 的`streaming_complete`方法。在语音合成过程中，服务端会在缓存足够文本后才开始合成。如果未调用`streaming_complete`方法，可能会导致缓存中的结尾部分文本未能被合成为语音。

#### **Q：SSL证书校验失败如何处理？**

1. 安装系统根证书















```bash
sudo yum install -y ca-certificates
sudo update-ca-trust enable
```

2. 代码中添加如下内容















```python
import os
os.environ["SSL_CERT_FILE"] = "/etc/ssl/certs/ca-bundle.crt"
```


#### **Q：Mac环境下出现“** SSL: CERTIFICATE\_VERIFY\_FAILED **”异常是什么原因？（** websocket closed due to \[SSL: CERTIFICATE\_VERIFY\_FAILED\] certificate verify failed: unable to get local issuer certificate (\_ssl.c:1000)）

在连接 WebSocket 时，可能会遇到 OpenSSL 验证证书失败的问题，提示找不到证书。这通常是由于 Python 环境的证书配置不正确导致的。可以通过以下步骤手动定位并修复证书问题：

1. 导出系统证书并设置环境变量
执行以下命令，将 macOS 系统中的所有证书导出到一个文件，并将其设置为 Python 和相关库的默认证书路径：















```bash
security find-certificate -a -p > ~/all_mac_certs.pem
export SSL_CERT_FILE=~/all_mac_certs.pem
export REQUESTS_CA_BUNDLE=~/all_mac_certs.pem
```

2. 创建符号链接以修复 Python 的 OpenSSL 配置
如果 Python 的 OpenSSL 配置缺失证书，可以通过以下命令手动创建符号链接。请确保替换命令中的路径为本地 Python 版本的实际安装目录：















```bash
# 3.9是示例版本号，请根据您本地安装的 Python 版本调整路径
ln -s /etc/ssl/* /Library/Frameworks/Python.framework/Versions/3.9/etc/openssl
```

3. 重新启动终端并清除缓存
完成上述操作后，请关闭并重新打开终端，以确保环境变量生效。清除可能的缓存后重试连接 WebSocket。


通过以上步骤，可以解决因证书配置错误导致的连接问题。如果问题仍未解决，请检查目标服务器的证书配置是否正确。

#### **Q：运行代码提示“** AttributeError: module 'websocket' has no attribute 'WebSocketApp'. Did you mean: 'WebSocket'? **”是什么原因？**

原因是没有安装websocket-client或websocket-client版本不匹配，请依次执行以下命令：

```bash
pip uninstall websocket-client
pip uninstall websocket
pip install websocket-client
```

### **权限与认证**

#### **Q：** 我希望我的 API Key 仅用于 CosyVoice 语音合成服务，而不被百炼其他模型使用（权限隔离），我该如何做 **？**

可以通过新建业务空间并只授权特定模型来限制API Key的使用范围。详情请参见 [业务空间管理](https://help.aliyun.com/zh/model-studio/use-workspace "")。

##### **Q：使用子业务空间的API Key是否可以调用CosyVoice模型？**

对于默认业务空间，模型均可调用。

对于子业务空间：需要为API Key对应的子业务空间进行 [模型授权](https://help.aliyun.com/zh/model-studio/model-authentication-instructions "")，详情请参见 [子业务空间的模型调用](https://help.aliyun.com/zh/model-studio/model-calling-in-sub-workspace "")。

### **更多问题**

请参见GitHub [QA](https://github.com/aliyun/alibabacloud-bailian-speech-demo/blob/master/docs/QA/cosyvoice.md)。