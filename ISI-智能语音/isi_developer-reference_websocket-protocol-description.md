### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/developer-reference/cosvoice-large-model-for-speech-synthesis/)[流式文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/siso-text-to-speech-synthesis-for-cosyvoice/)WebSocket协议说明

# WebSocket协议说明

更新时间：2026-01-06 03:41:27

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：C++ SDK](https://help.aliyun.com/zh/isi/developer-reference/c-sdk-3)[下一篇：简介与SDK代码示例](https://help.aliyun.com/zh/isi/developer-reference/cosyvoice-sound-replica)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

鉴权

请求指令

1\. Header格式说明

2\. StartSynthesis指令

3\. RunSynthesis指令

4\. StopSynthesis指令

下行数据

事件

1\. SynthesisStarted事件

2\. SentenceXXX事件

5\. SynthesisCompleted事件

下行音频流

JavaScript示例代码

流式播放器说明

测试工具

本文介绍如何使用智能语音交互流式文本WebSocket协议使用语音合成。如果您不希望引入阿里云智能语音交互产品SDK，或者目前提供的SDK不能满足您的要求，可以基于本文描述自行开发代码访问阿里语音服务。

## **前提条件**

在使用WebSocket协议对接之前，请先阅读 [API详情](https://help.aliyun.com/zh/isi/cosyvoice-api-details "") 中的服务交互流程说明 。

## 鉴权

服务端通过临时Token进行鉴权，请求时需要在URL中携带Token参数，Token获取方式请参见 [获取Token概述](https://help.aliyun.com/zh/isi/overview-of-obtaining-an-access-token#587dee8029x7r "")。获取Token之后通过如下方式访问语音服务端。

| **访问类型** | **说明** | **URL** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **访问类型** | **说明** | **URL** |
| 外网访问（默认北京地域） | 所有服务器均可使用外网访问URL（SDK中默认设置了外网访问URL）。 | 北京：`wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1` |
| ECS内网访问 | 使用阿里云北京ECS（即ECS地域为华北2（北京）），可使用内网访问URL。 ECS的经典网络不能访问AnyTunnel，即不能在内网访问语音服务；如果希望使用AnyTunnel，需要创建专有网络在其内部访问。<br>**说明**<br>使用内网访问方式，将不产生ECS实例的公网流量费用。<br>关于ECS的网络类型请参见 [网络类型](https://help.aliyun.com/zh/ecs/user-guide/network-types#concept-nfj-dz2-5db "")。 | 北京：`ws://nls-gateway-cn-beijing-internal.aliyuncs.com:80/ws/v1` |

## **请求指令**

请求指令用于控制语音识别任务的起止，标识任务边界，以JSON格式的Text Frame方式发送服务端请求，需要在Header中设置请求的基础信息。指令由Header和Payload两部分组成，其中Header部分为统一格式，不同指令的Payload部分格式各不相同。

### **1\. Header格式说明**

Header格式如下：

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| header | 请求头 | - | - |
| header.appkey | String | 是 | [管控台](https://nls-portal.console.aliyun.com/applist) 创建的项目Appkey。 |
| header.message\_id | String | 是 | 当次消息请求ID，随机生成32位唯一ID。 |
| header.task\_id | String | 是 | 整个实时语音合成的会话ID，整个请求中需要保持一致，32位唯一ID。 |
| header.namespace | String | 是 | 访问的产品名称，固定为“FlowingSpeechSynthesizer”。 |
| header.name | String | 是 | 指令名称，包含StartSynthesis和StopSynthesis指令。 |

### **2\. StartSynthesis指令**

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| payload.voice | String | 否 | 发音人，默认是longxiaochun。发音人，默认是longxiaochun。 |
| payload.format | String | 否 | 音频编码格式，支持pcm、wav和mp3格式，默认值：pcm。音频编码格式，支持pcm、wav和mp3格式，默认值：pcm。 |
| payload.sample\_rate | Integer | 否 | 音频采样率，默认值：16000Hz。 |
| payload.volume | Integer | 否 | 音量，取值范围：0～100。默认值：50。 |
| payload.speech\_rate | Integer | 否 | 语速，取值范围：-500～500，默认值：0。<br>\[-500,0,500\]对应的语速倍速区间为 \[0.5,1.0,2.0\]。 |
| payload.pitch\_rate | Integer | 否 | 语调，取值范围：-500～500，默认值：0。 |
| payload.enable\_aigc\_tag | Boolean | 否 | 是否在生成的音频中添加AIGC隐性标识。设置为true时，会将隐性标识嵌入到支持格式（wav/mp3/opus）的音频中。<br>默认值：false。 |
| payload.aigc\_propagator | String | 否 | 设置AIGC隐性标识中的 `ContentPropagator` 字段，用于标识内容的传播者。仅在 `enable_aigc_tag` 为 `true` 时生效。<br>默认值：阿里云UID。 |
| payload.aigc\_propagate\_id | String | 否 | 设置AIGC隐性标识中的 `PropagateID` 字段，用于唯一标识一次具体的传播行为。仅在 `enable_aigc_tag` 为 `true` 时生效。<br>默认值：本次语音合成请求Task ID。 |

```json
{
    "header": {
        "message_id": "05450bf69c53413f8d88aed1ee60****",
        "task_id": "640bc797bb684bd6960185651307****",
        "namespace": "FlowingSpeechSynthesizer",
        "name": "StartSynthesis",
        "appkey": "17d4c634****"
    },
    "payload": {
        "voice": "longxiaochun",
        "format": "wav",
        "sample_rate": 16000,
        "volume": 50,
        "speech_rate": 0,
        "pitch_rate": 0,
        "enable_subtitle": true
    }
}
```

### **3\. RunSynthesis指令**

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| text | String | 是 | 需要合成的文本 |

```json
{
    "header": {
        "message_id": "05450bf69c53413f8d88aed1ee60****",
        "task_id": "640bc797bb684bd6960185651307****",
        "namespace": "FlowingSpeechSynthesizer",
        "name": "RunSynthesis",
        "appkey": "17d4c634****"
    },
    "payload": {
        "text": "流式输入文本"
    }
}
```

### **4\. StopSynthesis指令**

StopSynthesis指令要求服务端停止语音合成，并且合成所有缓存文本。

**重要**

由于流式文本语音合成服务端会分句合成音频，因此服务端存在未满足分句条件的缓存文本，需要在文本流发送结束后立刻发送此指令，否则有可能丢失文本。

Payload为空。示例代码如下：

```json
{
    "header": {
        "message_id": "05450bf69c53413f8d88aed1ee60****",
        "task_id": "640bc797bb684bd6960185651307****",
        "namespace": "FlowingSpeechSynthesizer",
        "name": "StopSynthesis",
        "appkey": "17d4c634****"
    }
}
```

## **下行数据**

WebSocket 数据帧分为文本帧 (text frame)、二进制帧 (binary frame)、关闭帧 (close frame)、Ping帧和Pong帧。我们使用文本帧下发事件，使用二进制帧下发音频数据流。

以Python中的websocket-client为例，可以参考下述示例代码解析WebSocket收到的数据：

```python
audio_data = None

# 监听消息的回调函数
def on_message(self, ws, message):
    if isinstance(message, str):
        # 将文本帧解析为json
        try:
            json_data = json.loads(message)
            # TODO: 解析事件
        except json.JSONDecodeError:
            print("Failed to parse message as JSON.")
    elif isinstance(message, (bytes, bytearray)):
        # 将二进制帧作为音频帧保存
        # TODO: 保存音频或使用支持流式输入的播放器播放，例如pyaudio
        if audio_data is None:
            audio_data = bytes(message)
        else:
            audio_data = self._audio_data + bytes(message)

ws = websocket.WebSocketApp(
    url,
    header={
        "X-NLS-Token": token,
    },
    on_message=on_message,
    on_error=None,
    on_close=None,
)
```

关于Websocket详细介绍可以参考 [链接](https://websockets.spec.whatwg.org/)

## 事件

事件指的是服务端返回给客户端的处理进度事件，代表不同的处理阶段，客户端可获取不同处理阶段的事件实现不同的业务逻辑。以JSON格式返回，事件由Header和Payload两部分组成，其中Header部分为统一格式，不同事件的Payload部分格式可能不同。

### **1\. SynthesisStarted事件**

```json
{
    "header": {
        "message_id": "05450bf69c53413f8d88aed1ee60****",
        "task_id": "640bc797bb684bd6960185651307****",
        "namespace": "FlowingSpeechSynthesizer",
        "name": "SynthesisStarted",
        "status": 20000000,
        "status_message": "GATEWAY|SUCCESS|Success."
    }
}
```

### **2\. SentenceXXX事件**

SentenceBegin、SentenceSynthesis、SentenceEnd为时间戳相关事件，CosyVoice大模型当前不支持时间戳功能，无需解析。

### **5\. SynthesisCompleted事件**

SynthesisCompleted事件表示服务端已停止了语音合成并且所有音频数据下发完毕。

只有发送了StopSynthesis指令，才能接收到该事件。

```json
{
    "header": {
        "message_id": "05450bf69c53413f8d88aed1ee60****",
        "task_id": "640bc797bb684bd6960185651307****",
        "namespace": "FlowingSpeechSynthesizer",
        "name": "SynthesisCompleted",
        "status": 20000000,
        "status_message": "GATEWAY|SUCCESS|Success."
    },
    "payload": {
        "measureType": "TextLengthHD",
        "measureLength": 57
    }
}
```

## **下行音频流**

在流式语音合成中，音频会以数据流的方式分帧下发。下发的所有音频为一个完整的音频文件，可以通过支持流式播放的播放器，例如：ffmpeg、pyaudio (Python)、AudioFormat (Java)、MediaSource (Javascript)等，实时播放。

**重要**

1. 从第一次发起RunSynthesis指令发送文本开始，到收到SynthesisCompleted之间会收到音频流。

2. 在流式语音合成中，是将一个完整的音频文件分多次返回。在播放流式音频时，需要使用支持流式播放的音频播放器，而不是将每一帧当作一个独立的音频播放，这样无法成功解码。

3. 在保存音频时，请使用追加模式写入同一个文件。

4. 在使用wav/mp3格式合成音频时，由于文件按照流式合成，因此只在第一帧中包含当前任务的文件头信息。


## **JavaScript示例代码**

可以参考 [流式语音合成JS播放示例](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250205/jsenot/javascript%E7%A4%BA%E4%BE%8B%E6%92%AD%E6%94%BEpcm.zip) 使用JavaScript实现流式语音合成协议并播放。

请在打开index.html前首先替换app.js中的appkey和token，并且将voice参数替换为cosyvoice大模型音色，例如longxiaochun。之后您可以通过下面的python命令在当前目录下启动一个简单的 HTTP 服务器，并在浏览器中输入`http://localhost:8000`打开网页。

```python
python -m http.server 8000
```

在网页中，您可以点击按钮发送对应指令。点击RunSynthesis会发送您在文本框中输入的文本片段到服务器，在一次流程中，RunSynthesis可以点击多次。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2715478371/p911966.png)

### **流式播放器说明**

在`audio_player.js`中，我们使用 Web Audio API 开发了 PCMAudioPlayer 播放器播放流式PCM格式的音频，将16bit采样点转化为float写入audioBuffer播放，并且在上一段音频播放结束的onended回调中立刻播放下一段音频。

**重要**

1. 使用MediaSource播放流式音频是一个更加简洁的方案，但是MediaSource不支持如下浏览器：Safari、基于Safari的iOS WebView、微信小程序。更多兼容信息请参见 [MediaSource](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaSource)。

2. 使用 [openai-realtime-console](https://github.com/openai/openai-realtime-console/tree/websockets) 中集成的wavtools在移动端和safari浏览器中播放时会有噪声。


## **测试工具**

在根据Websocket协议开发接口过程中，可以下载 [NlsStreamInputTtsMockServer.py](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20240722/jlklar/NlsStreamInputTtsMockServer.py) 脚本，运行如下命令安装依赖，并在本地模拟公有云流式语音合成服务进行调试：

```bash
pip install websocket-client
python NlsStreamInputTtsMockServer.py
```

在成功执行脚本后，将默认在本地的 ws://127.0.0.1:12345 运行模拟服务。请在可以成功调用本地的模拟服务后再切换到线上服务调试。