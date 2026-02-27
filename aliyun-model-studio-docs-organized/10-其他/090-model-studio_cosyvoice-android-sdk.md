### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音合成](https://help.aliyun.com/zh/model-studio/speech-synthesis-api-reference/)[实时语音合成（CosyVoice）](https://help.aliyun.com/zh/model-studio/cosyvoice-large-model-for-speech-synthesis/)Android SDK

# 语音合成CosyVoice Android SDK

更新时间：2026-02-11 02:25:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：WebSocket API](https://help.aliyun.com/zh/model-studio/cosyvoice-websocket-api)[下一篇：iOS SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-ios-sdk)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

模型与价格

限制与约束

文本长度限制

文本编码格式

快速开始

调用方式

请求参数

连接与控制参数

语音合成效果参数

关键接口

NativeNui

INativeStreamInputTtsCallback：监听回调

StreamInputTtsEvent：事件类型

高级功能

SSML 标记语言

数学表达式

本文档提供了语音合成CosyVoice Android SDK的详细使用指南，帮助您将文本转换为高质量、富有表现力的语音。

**用户指南：** 关于模型介绍和选型建议请参见 [语音合成-CosyVoice](https://help.aliyun.com/zh/model-studio/text-to-speech "")。

## **模型与价格**

在资源与预算允许的情况下，优先选择 cosyvoice-v3-plus 获取最佳合成效果，对成本敏感时可选 cosyvoice-v3 平衡质量与价格，其余版本仅建议在兼容或低要求场景使用。

| **模型名称** | **单价** | **免费额度** [（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型名称** | **单价** | **免费额度** [（注）](https://help.aliyun.com/zh/model-studio/new-free-quota#591f3dfedfyzj "") |
| cosyvoice-v3-plus | 2元/万字符 | 1万字符<br>有效期：阿里云百炼开通后90天内 |
| cosyvoice-v3-flash | 1元/万字符 |
| cosyvoice-v2 | 2元/万字符 |
| cosyvoice-v1 |

文本字符计算规则：

- 汉字（包括简/繁体汉字、日文汉字和韩文汉字）按2个字符计算，其他所有字符（如标点符号、字母、数字、日韩文假名/谚文等）均按 1个字符计算

- 计算文本长度时，不包含SSML 标签内容

- 示例：

  - `"你好"` → 2(你)+2(好)=4字符

  - `"中A文123"` → 2(中)+1(A)+2(文)+1(1)+1(2)+1(3)=8字符

  - `"中文。"` → 2(中)+2(文)+1(。)=5字符

  - `"中 文。"` → 2(中)+1(空格)+2(文)+1(。)=6字符

  - `"<speak>你好</speak>"` → 2(你)+2(好)=4字符

## **限制与约束**

### **文本长度限制**

- [一次性输入待合成文本](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#f8b7cc6ae3s40 "")：发送文本长度不得超过 20000 字符。

- [流式输入待合成文本](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#2e911197440yt "")：单次发送文本长度不得超过 20000 字符，且累计发送文本总长度不得超过 20 万字符。


### **文本编码格式**

需采用UTF-8编码。

## **快速开始**

1. **获取API Key：** [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，为安全起见，推荐将API Key配置到环境变量。



**说明**





当您需要为第三方应用或用户提供临时访问权限，或者希望严格控制敏感数据访问、删除等高风险操作时，建议使用 [临时API Key](https://help.aliyun.com/zh/model-studio/generate-temporary-api-key "")。临时API Key拥有固定的60秒有效期，过期后需重新获取。

2. **下载SDK并运行示例代码：**

   - [下载最新SDK整合包](https://help.aliyun.com/zh/isi/sdk-selection-and-download "")。

   - 解压 ZIP 包。在 `app/libs` 目录中获取 AAR 格式 SDK，并添加到项目依赖。

     需要 Android CPP 接入时，使用 ZIP 包内的 `android_libs` 与 `android_include` 获取动态库和头文件。

   - 用 Android Studio 打开工程。示例代码位于`DashCosyVoiceStreamTtsActivity.java`，替换 API Key 后体验功能。

### **调用方式**

| **调用方式** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **调用方式** | **说明** |
| 一次性输入待合成文本 | **调用步骤：**<br>1. 初始化 SDK 和播放器组件。<br>   <br>2. 按业务需求设置参数。<br>   <br>3. 调用 [playStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#be00eb5c18hnz "") 或`asyncPlayStreamInputTts`发送文本并开始语音合成。<br>   <br>4. 接收到 `STREAM_INPUT_TTS_EVENT_SYNTHESIS_COMPLETE` 回调，语音合成结束。<br>   <br>**适用场景：**<br>- 短文本合成<br>  <br>- 需要使用 SSML 标记语言 |
| 流式输入待合成文本 | **调用步骤：**<br>1. 初始化 SDK 和播放器组件。<br>   <br>2. 按业务需求设置参数。<br>   <br>3. 调用 `startStreamInputTts` 开始流式文本语音合成。<br>   <br>4. 调用 `sendStreamInputTts` 持续发送文本。<br>   <br>5. 在`onStreamInputTtsDataCallback`中，获取二进制音频数据。<br>   <br>6. 调用 `stopStreamInputTts` 或 `asyncStopStreamInputTts` 结束发送，等待合成完成。<br>   <br>7. 接收到 `STREAM_INPUT_TTS_EVENT_SYNTHESIS_COMPLETE` 回调，语音合成结束。<br>   <br>**适用场景：**<br>- 实时对话、长文本“边说边合”<br>  <br>- 此方式不支持 SSML 标记语言 |

## **请求参数**

### 连接与控制参数

通过在 [startStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#05eab5125e2pm "")、 [playStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#be00eb5c18hnz "") 和 [asyncPlayStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#2d43b13c45u3g "") 接口的`ticket`参数中传入一个JSON字符串来配置。

- **参数示例：** 以下为 JSON 字符串示例，参数未完整列出。请按实际需求在编码时补充：















```json
{
      "url": "wss://dashscope.aliyuncs.com/api-ws/v1/inference",
      "apikey": "st-****",
      "device_id": "my_device_id"
}
```

- **参数说明**




| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| `url` | `String` | 是 | 服务地址，固定为 `wss://dashscope.aliyuncs.com/api-ws/v1/inference`。 |
| `apikey` | `String` | 是 | API Key。建议使用时效性短、安全性更高的 [临时API Key](https://help.aliyun.com/zh/model-studio/generate-temporary-api-key "")，以降低长期有效Key泄露的风险。 |
| `device_id` | `String` | 是 | 用于标识终端用户的唯一字符串，可设为应用内用户ID或客户端生成的设备唯一标识符。此ID主要用于日志追踪和问题排查。 |
| `complete_waiting_ms` | `int` | 否 | 调用stop接口后，等待合成完成事件（STREAM\_INPUT\_TTS\_EVENT\_SYNTHESIS\_COMPLETE）的超时时间（毫秒）。<br>默认值：10000。 |
| `debug_path` | `String` | 否 | 日志文件的存储路径。<br>此参数仅在调用 [startStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#05eab5125e2pm "")、 [playStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#be00eb5c18hnz "") 或 [asyncPlayStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#2d43b13c45u3g "") 接口时将`save_log`设为true时生效。此时必须设置日志文件路径，否则将报错。<br>本地最多保留两个日志文件。 |
| `max_log_file_size` | `int` | 否 | 设定日志文件的最大字节数。<br>此参数仅在调用 [startStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#05eab5125e2pm "")、 [playStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#be00eb5c18hnz "") 或 [asyncPlayStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#2d43b13c45u3g "") 接口时将`save_log`设为true时生效。<br>默认值：104857600（100 \* 1024 \* 1024 字节, 即 100MiB）。 |
| `log_track_level` | `int` | 否 | 控制通过日志回调（`onStreamInputTtsLogTrackCallback`）对外发送的日志内容的过滤级别。<br>默认值：2。<br>取值范围：<br>  - 0：LOG\_LEVEL\_VERBOSE<br>    <br>  - 1：LOG\_LEVEL\_DEBUG<br>    <br>  - 2：LOG\_LEVEL\_INFO<br>    <br>  - 3：LOG\_LEVEL\_WARNING<br>    <br>  - 4：LOG\_LEVEL\_ERROR<br>    <br>  - 5：LOG\_LEVEL\_NONE（表示关闭此功能）<br>    <br>注意：`log_track_level`与`log_level`（通过 [startStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#05eab5125e2pm "")、 [playStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#be00eb5c18hnz "") 或 [asyncPlayStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#2d43b13c45u3g "") 接口设置）共同决定最终回调的日志。一条日志的级别数值必须同时大于或等于`log_track_level`和`log_level`的值，才会被回调。例如，`log_track_level`设为2 (INFO)，`log_level`设为3 (WARNING)，则只有WARNING及以上级别（数值>=3）的日志才会被回调。 |


### **语音合成效果参数**

通过在 [startStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#05eab5125e2pm "")、 [playStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#be00eb5c18hnz "") 和 [asyncPlayStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#2d43b13c45u3g "") 接口的`parameters`参数中传入一个JSON 字符串来配置。

- **参数示例：** 以下为 JSON 字符串示例，参数未完整列出。请按实际需求在编码时补充：















```json
{
      "model": "cosyvoice-v2",
      "voice": "longxiaochun_v2",
      "format": "mp3",
      "sample_rate": 24000,
      "volume": 50,
      "rate": 1,
      "pitch": 1,
      "language_hints": ["zh"]
}
```

- **参数说明**




| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| `model` | `String` | 是 | 语音合成[模型](https://help.aliyun.com/zh/model-studio/models#7a960cc042zwt "")。<br>不同模型版本需要使用对应版本的音色：<br>  - cosyvoice-v3-flash/cosyvoice-v3-plus：使用longanyang等音色。<br>    <br>  - cosyvoice-v2：使用longxiaochun\_v2等音色。<br>    <br>  - cosyvoice-v1：使用longwan等音色。<br>    <br>  - 完整音色列表请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")。 |
| `voice` | `String` | 是 | 语音合成所使用的音色。<br>支持系统音色和复刻音色：<br>  - **系统音色**：参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")。<br>    <br>  - **复刻音色**：通过 [声音复刻](https://help.aliyun.com/zh/model-studio/voice-replica-1/ "") 功能定制。使用复刻音色时，请确保声音复刻与语音合成使用同一账号。详细操作步骤请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api#da30eeebc4uwk "")。<br>    <br>    使用声音复刻生成的复刻音色时，本请求的`model`参数值，必须与创建该音色时所用的模型版本（即`target_model`参数）完全一致。 |
| `format` | `String` | 否 | 音频编码格式。<br>默认值：mp3。<br>取值范围：pcm/wav/mp3/opus（当 `model` 为 `cosyvoice-v1` 时，不支持 `opus` 格式）。 |
| `volume` | `int` | 否 | 音量。<br>默认值：50。<br>取值范围：\[0, 100\]。50代表标准音量。音量大小与该值呈线性关系，0为静音，100为最大音量。 |
| `sample_rate` | `int` | 否 | 采样率（单位Hz）。<br>默认值：22050。<br>取值范围：8000/16000/22050/24000/44100/48000。 |
| `rate` | `float` | 否 | 语速。<br>默认值：1.0。<br>取值范围：\[0.5, 2.0\]。1.0为标准语速，小于1.0则减慢，大于1.0则加快。 |
| `pitch` | `float` | 否 | 音高。该值作为音高调节的乘数，但其与听感上的音高变化并非严格的线性或对数关系，建议通过测试选择合适的值。<br>默认值：1.0。<br>取值范围：\[0.5, 2.0\]。1.0为音色自然音高。大于1.0则音高变高，小于1.0则音高变低。 |
| `bit_rate` | `int` | 否 | 音频码率（单位kbps）。音频格式为opus时，支持通过`bit_rate`参数调整码率。<br>默认值：32。<br>取值范围：\[6, 510\]。<br>`cosyvoice-v1`模型不支持该参数。 |
| `enable_ssml` | `boolean` | 否 | 是否开启SSML功能。<br>默认值：false。<br>  - true：开启。<br>    <br>  - false：关闭。 |
| `word_timestamp_enabled` | `boolean` | 否 | 是否开启字级别时间戳。<br>默认值：false。<br>  - true：开启。<br>    <br>  - false：关闭。<br>    <br>该功能仅适用于cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持的系统音色。<br>> 时间戳结果在 [INativeStreamInputTtsCallback](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#8b030fec74e01 "") 的all\_response中。 |
| `seed` | `int` | 否 | 生成时使用的随机数种子，使合成的效果产生变化。在模型版本、文本、音色及其他参数均相同的前提下，使用相同的seed可复现相同的合成结果。<br>默认值0。<br>取值范围：\[0, 65535\]。<br>cosyvoice-v1不支持该功能。 |
| `language_hints` | `String[]` | 否 | 指定语音合成的目标语言，提升合成效果。cosyvoice-v1不支持该功能。<br>当数字、缩写、符号等朗读方式或者小语种合成效果不符合预期时使用，例如：<br>  - 数字朗读方式不符合预期，“hello, this is 110”读成“hello, this is one one zero”而非“hello, this is 幺幺零”<br>    <br>  - 符号朗读不准确，“@”读成“艾特”而非“at”<br>    <br>  - 小语种合成效果差，合成不自然<br>    <br>取值范围：<br>  - zh：中文<br>    <br>  - en：英文<br>    <br>  - fr：法语<br>    <br>  - de：德语<br>    <br>  - ja：日语<br>    <br>  - ko：韩语<br>    <br>  - ru：俄语<br>    <br>**注意**：此参数为数组，但当前版本仅处理第一个元素，因此建议只传入一个值。<br>**重要**<br>此参数用于指定语音合成的目标语言，该设置与声音复刻时的样本音频的语种无关。如果您需要设置复刻任务的源语言，请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api "")。 |
| `instruction` | `String` | 否 | 设置指令，用于控制方言、情感或角色等合成效果。该功能仅适用于cosyvoice-v3-flash模型的复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色。<br>**使用要求**：<br>  - 指令必须使用固定格式和内容（见下方说明）<br>    <br>  - 不设置时不生效（无默认值）<br>    <br>**支持的功能**：<br>  - 指定方言<br>    <br>    - 适用音色：仅复刻音色<br>      <br>    - 格式：“`请用<方言>表达。`”（注意，结尾一定不要遗漏句号，使用时将“`<方言>`”替换为具体的`方言`，例如替换为`广东话`）。<br>      <br>    - 示例：“`请用广东话表达。`”<br>      <br>    - 支持的方言：广东话、东北话、甘肃话、贵州话、河南话、湖北话、江西话、闽南话、宁夏话、山西话、陕西话、山东话、上海话、四川话、天津话、云南话。<br>  - 指定情感<br>    <br>    - 适用音色<br>      <br>      - 复刻音色<br>        <br>      - [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色<br>    - 格式：<br>      <br>      - 复刻音色：<br>        <br>        <br>        <br>        点击查看复刻音色指令格式<br>        <br>        <br>        <br>        <br>        <br>        <br>        - `请尽可能非常大声地说一句话。`<br>          <br>        - `请用尽可能慢地语速说一句话。`<br>          <br>        - `请用尽可能快地语速说一句话。`<br>          <br>        - `请非常轻声地说一句话。`<br>          <br>        - `你可以慢一点说吗`<br>          <br>        - `你可以非常快一点说吗`<br>          <br>        - `你可以非常慢一点说吗`<br>          <br>        - `你可以快一点说吗`<br>          <br>        - `请非常生气地说一句话。`<br>          <br>        - `请非常开心地说一句话。`<br>          <br>        - `请非常恐惧地说一句话。`<br>          <br>        - `请非常伤心地说一句话。`<br>          <br>        - `请非常惊讶地说一句话。`<br>          <br>        - `请尽可能表现出坚定的感觉。`<br>          <br>        - `请尽可能表现出愤怒的感觉。`<br>          <br>        - `请尝试一下亲和的语调。`<br>          <br>        - `请用冷酷的语调讲话。`<br>          <br>        - `请用威严的语调讲话。`<br>          <br>        - `我想体验一下自然的语气。`<br>          <br>        - `我想看看你如何表达威胁。`<br>          <br>        - `我想看看你怎么表现智慧。`<br>          <br>        - `我想看看你怎么表现诱惑。`<br>          <br>        - `我想听听用活泼的方式说话。`<br>          <br>        - `我想听听你用激昂的感觉说话。`<br>          <br>        - `我想听听用沉稳的方式说话的样子。`<br>          <br>        - `我想听听你用自信的感觉说话。`<br>          <br>        - `你能用兴奋的感觉和我交流吗？`<br>          <br>        - `你能否展示狂傲的情绪表达？`<br>          <br>        - `你能展现一下优雅的情绪吗？`<br>          <br>        - `你可以用幸福的方式回答问题吗？`<br>          <br>        - `你可以做一个温柔的情感演示吗？`<br>          <br>        - `能用冷静的语调和我谈谈吗？`<br>          <br>        - `能用深沉的方法回答我吗？`<br>          <br>        - `能用粗犷的情绪态度和我对话吗？`<br>          <br>        - `用阴森的声音告诉我这个答案。`<br>          <br>        - `用坚韧的声音告诉我这个答案。`<br>          <br>        - `用自然亲切的闲聊风格叙述。`<br>          <br>        - `用广播剧博客主的语气讲话。`<br>          <br>      - 系统音色：系统音色和复刻音色的情感指令格式不同，详情请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")<br>  - 指定场景、角色或身份等<br>    <br>    - 适用音色： [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色<br>      <br>    - 格式：请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") |
| enable\_aigc\_tag | `boolean` | 否 | 是否在生成的音频中添加AIGC隐性标识。设置为true时，会将隐性标识嵌入到支持格式（wav/mp3/opus）的音频中。<br>默认值：false。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。 |
| aigc\_propagator | `String` | 否 | 设置AIGC隐性标识中的 `ContentPropagator` 字段，用于标识内容的传播者。仅在 `enable_aigc_tag` 为 `true` 时生效。<br>默认值：阿里云UID。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。 |
| aigc\_propagate\_id | `String` | 否 | 设置AIGC隐性标识中的 `PropagateID` 字段，用于唯一标识一次具体的传播行为。仅在 `enable_aigc_tag` 为 `true` 时生效。<br>默认值：本次语音合成请求Request ID。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。 |


## **关键接口**

### **NativeNui**

#### **startStreamInputTts**

启动双向流式语音合成，建立与服务端的连接，并注册回调以接收事件和音频数据。

此接口可能会引起阻塞，应在非UI线程调用。

- **方法签名**















```java
public synchronized int startStreamInputTts(INativeStreamInputTtsCallback callback,
                                              String ticket,
                                              String parameters,
                                              String session_id,
                                              int log_level,
                                              boolean save_log)
```

- **参数说明**




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `callback` | `INativeStreamInputTtsCallback` | 事件和数据回调接口的实现。 |
| `ticket` | `String` | JSON字符串，包含鉴权、连接和调试参数。参见 [连接与控制参数](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#57acf5ecc1w8j "")。 |
| `parameters` | `String` | JSON字符串，包含语音合成的具体效果参数。参见 [语音合成效果参数](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#d20cce9518kla "")。 |
| `session_id` | `String` | 客户端指定的会话ID。若不传入，服务端将自动生成。 |
| `log_level` | `int` | 控制SDK自身日志的打印级别。<br>取值范围：<br>  - 0：LOG\_LEVEL\_VERBOSE<br>    <br>  - 1：LOG\_LEVEL\_DEBUG<br>    <br>  - 2：LOG\_LEVEL\_INFO<br>    <br>  - 3：LOG\_LEVEL\_WARNING<br>    <br>  - 4：LOG\_LEVEL\_ERROR<br>    <br>  - 5：LOG\_LEVEL\_NONE（表示关闭此功能） |
| `save_log` | `boolean` | 是否保存本地日志。若为true，须在 [连接与控制参数](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#57acf5ecc1w8j "") 中通过`debug_path`指定路径，并可通过`max_log_file_size`设置文件大小。 |

- **返回值说明**

返回错误码，参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。


#### sendStreamInputTts

发送待合成的文本，与 startStreamInputTts 搭配使用。

在调用 startStreamInputTts 后，使用此接口持续发送文本。

所有文本发送完毕后，需调用stopStreamInputTts或asyncStopStreamInputTts来结束发送。

- **方法签名**















```java
public synchronized int sendStreamInputTts(String text)
```

- **参数说明**




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `text` | `String` | 待合成文本。不支持 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "")。如果传入的文本包含SSML标签，这些标签将被当作普通文本读出，不会被解析。 |

- **返回值说明**

返回错误码，参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。


#### stopStreamInputTts

同步接口，通知服务端文本已全部发送，并阻塞等待所有音频数据合成并收到 STREAM\_INPUT\_TTS\_EVENT\_SYNTHESIS\_COMPLETE。

阻塞等待的超时时间由参数 complete\_waiting\_ms 控制。

- **方法签名**















```java
public synchronized int stopStreamInputTts()
```

- **返回值说明**

返回错误码，参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。


#### asyncStopStreamInputTts

异步接口，通知服务端文本已全部发送。调用后立即返回，合成在后台继续进行。

通过 STREAM\_INPUT\_TTS\_EVENT\_SYNTHESIS\_COMPLETE 事件判断合成是否完成。

- **方法签名**















```java
public synchronized int asyncStopStreamInputTts()
```

- **返回值说明**

返回错误码，参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。


#### cancelStreamInputTts

立即中断与服务端的连接并终止当前合成任务。调用后不会再收到任何音频数据回调。

- **方法签名**















```java
public synchronized int cancelStreamInputTts()
```

- **返回值说明**

返回错误码，参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。


#### playStreamInputTts

同步执行的一次性合成接口。该接口会发送文本、阻塞并等待接收所有音频数据，直到合成完成后才返回。无需再调用stop接口。

该接口默认启用SSML。如果在 [语音合成效果参数](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#d20cce9518kla "") 中显式设置enable\_ssml，则以用户设置为准。

此接口应在非UI线程调用。

- **方法签名**















```java
public synchronized int playStreamInputTts(INativeStreamInputTtsCallback callback,
                                             String ticket,
                                             String parameters,
                                             String text,
                                             String session_id,
                                             int log_level,
                                             boolean save_log)
```

- **参数说明**


callback、ticket等参数与 [startStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#05eab5125e2pm "") 接口中的定义相同。






| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `text` | `String` | 待合成文本。支持 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "")。 |

- **返回值说明**

返回错误码，参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。


#### asyncPlayStreamInputTts

异步执行的一次性合成接口。调用后立即返回，合成任务在后台进行，结果通过回调返回。无需再调用stop接口。

该接口默认启用SSML。如果在 [语音合成效果参数](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#d20cce9518kla "") 中显式设置enable\_ssml，则以用户设置为准。

- **方法签名**















```java
public synchronized int asyncPlayStreamInputTts(INativeStreamInputTtsCallback callback,
                                             String ticket,
                                             String parameters,
                                             String text,
                                             String session_id,
                                             int log_level,
                                             boolean save_log)
```

- **参数说明**


callback、ticket等参数与 [startStreamInputTts](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#05eab5125e2pm "") 接口中的定义相同。






| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `text` | `String` | 待合成文本。支持 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "")。 |

- **返回值说明**

返回错误码，参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。


### **INativeStreamInputTtsCallback：监听回调**

#### **onStreamInputTtsEventCallback：监听事件**

- **方法签名**















```java
void onStreamInputTtsEventCallback(StreamInputTtsEvent event,
                                     String task_id,
                                     String session_id,
                                     int ret_code,
                                     String error_msg,
                                     String timestamp,
                                     String all_response);
```

- **参数说明**




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `event` | `StreamInputTtsEvent` | 回调事件。 |
| `task_id` | `String` | 语音合成任务ID。 |
| `session_id` | `String` | 会话ID。客户端传入则原样返回；未传入时由服务端生成。 |
| `ret_code` | `int` | 错误码，仅在事件 STREAM\_INPUT\_TTS\_EVENT\_TASK\_FAILED 中有效。参见 [错误码查询](https://help.aliyun.com/zh/isi/support/error-codes "")。 |
| `error_msg` | `String` | 错误信息，仅在事件 STREAM\_INPUT\_TTS\_EVENT\_TASK\_FAILED 中有效。 |
| `timestamp` | `String` | 合成结果的时间戳信息。 |
| `all_response` | `String` | 完整的 JSON 字符串响应。可解析以获取所需数据。 |


#### onStreamInputTtsDataCallback **：监听音频数据**

合成过程中，SDK 会连续触发此回调，需在回调中获取音频数据。

- **方法签名**















```java
void onStreamInputTtsDataCallback(byte[] data);
```

- **参数说明**




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `data` | `byte[]` | 返回当前片段的音频数据，可用于：<br>  - 合成完整的音频文件并播放。<br>    <br>  - 通过支持流式播放的播放器实时播放。<br>    <br>注意：<br>  - 对 mp3/opus 压缩格式，分段传输必须使用流式播放器，不能逐帧播放，否则可能解码失败。<br>    <br>  - 组装完整文件时需采用追加模式写入同一文件。<br>    <br>  - 对于 wav 和 mp3 格式，仅在第一次 onStreamInputTtsDataCallback 回调的数据中包含文件头，后续回调均为纯音频数据。处理时需将所有回调的 `buffer` 按顺序拼接。opus 格式的每一帧都是独立的 Ogg page，可直接拼接。 |


#### onStreamInputTtsLogTrackCallback **：监听追踪日志**

此回调用于接收 SDK 内部的详细日志，方便进行问题定位和调试。

```java
default void onStreamInputTtsLogTrackCallback(Constants.LogLevel level, String log)
```

### **StreamInputTtsEvent：事件类型**

| **事件** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **事件** | **说明** |
| STREAM\_INPUT\_TTS\_EVENT\_SYNTHESIS\_STARTED | 表示服务端已成功接收请求并开始处理。通常在此事件后，`onStreamInputTtsDataCallback` 将很快开始返回第一批音频数据。 |
| STREAM\_INPUT\_TTS\_EVENT\_SENTENCE\_SYNTHESIS | 语音合成运行过程中的信息，包括计费信息等。 |
| STREAM\_INPUT\_TTS\_EVENT\_SYNTHESIS\_COMPLETE | 表示服务端已发送完全部音频数据，此后 `onStreamInputTtsEventCallback` 将不会再被调用。收到此事件是数据流结束的明确信号。 |
| STREAM\_INPUT\_TTS\_EVENT\_TASK\_FAILED | 表示任务失败。此时可从 [INativeStreamInputTtsCallback](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#8b030fec74e01 "") 的all\_response获得task\_id、error\_code、error\_message用于判断具体错误。<br>```json<br>{<br>    "header": {<br>        "task_id": "2bf83b9a-baeb-4fda-8d9a-xxxxxxxxxxxx",<br>        "event": "task-failed",<br>        "error_code": "InvalidParameter",<br>        "error_message": "[tts:]Engine return error code: 418",<br>        "attributes": {}<br>    },<br>    "payload": {}<br>}<br>``` |

## **高级功能**

### **SSML 标记语言**

**目的**：通过在文本中嵌入 XML 标签，实现对发音、语速、停顿等细节的精确控制。

**使用限制**：

- **模型**：仅适用于 `cosyvoice-v2` 模型。

- **调用方式**：仅支持 [一次性输入待合成文本](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#f8b7cc6ae3s40 "")（`playStreamInputTts` 或 `asyncPlayStreamInputTts` 接口），不支持 [流式输入待合成文本](https://help.aliyun.com/zh/model-studio/cosyvoice-android-sdk#2e911197440yt "")（`sendStreamInputTts` 接口）。


**使用方法**：调用 `playStreamInputTts`或`asyncPlayStreamInputTts`接口时，SDK 会自动启用 SSML，此时直接在 `text` 参数中传入包含 SSML 标签的文本即可。

详细的标签用法参考 [SSML标记语言介绍](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "")。

### **数学表达式**

**目的**：使模型能够正确朗读常见的数学公式和表达式。

**使用限制**：仅适用于 `cosyvoice-v2` 模型。

**使用方法**：直接在 `text` 参数中传入包含 LaTeX 格式的数学表达式的文本即可。详情参见 [LaTeX 公式转语音](https://help.aliyun.com/zh/model-studio/latex-capability-support-description "")。