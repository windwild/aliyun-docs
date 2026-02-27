### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[模型推理](https://help.aliyun.com/zh/model-studio/model-inference/)[语音合成](https://help.aliyun.com/zh/model-studio/speech-synthesis/)实时语音合成-CosyVoice/Sambert

# 实时语音合成-CosyVoice/Sambert

更新时间：2026-02-25 01:28:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：实时（Qwen-Omni-Realtime）](https://help.aliyun.com/zh/model-studio/realtime)[下一篇：实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

核心功能

适用范围

模型选型

快速开始

API参考

模型应用上架及备案

模型功能特性对比

支持的系统音色

常见问题

Q：语音合成的发音读错怎么办？多音字如何控制发音？

Q：使用复刻音色生成的音频无声音如何排查？

Q：声音复刻后合成效果不稳定或语音不完整如何处理？

语音合成，又称文本转语音（Text-to-Speech，TTS），是将文本转换为自然语音的技术。该技术基于机器学习算法，通过学习大量语音样本，掌握语言的韵律、语调和发音规则，从而在接收到文本输入时生成真人般自然的语音内容。

## **核心功能**

- 实时生成高保真语音，支持中英等多语种自然发声

- 提供声音复刻能力，快速定制个性化音色

- 支持流式输入输出，低延迟响应实时交互场景

- 可调节语速、语调、音量与码率，精细控制语音表现

- 兼容主流音频格式，最高支持48kHz采样率输出


## **适用范围**

**支持的模型：**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

调用以下模型时，请选择北京地域的 [API Key](https://bailian.console.aliyun.com/?tab=model#/api-key)：

- **CosyVoice：** cosyvoice-v3-plus、cosyvoice-v3-flash、cosyvoice-v2、cosyvoice-v1

- **Sambert：** sambert-zhinan-v1、sambert-zhiqi-v1、sambert-zhichu-v1、sambert-zhide-v1、sambert-zhijia-v1、sambert-zhiru-v1、sambert-zhiqian-v1、sambert-zhixiang-v1、sambert-zhiwei-v1、sambert-zhihao-v1、sambert-zhijing-v1、sambert-zhiming-v1、sambert-zhimo-v1、sambert-zhina-v1、sambert-zhishu-v1、sambert-zhistella-v1、sambert-zhiting-v1、sambert-zhixiao-v1、sambert-zhiya-v1、sambert-zhiye-v1、sambert-zhiying-v1、sambert-zhiyuan-v1、sambert-zhiyue-v1、sambert-zhigui-v1、sambert-zhishuo-v1、sambert-zhimiao-emo-v1、sambert-zhimao-v1、sambert-zhilun-v1、sambert-zhifei-v1、sambert-zhida-v1、sambert-camila-v1、sambert-perla-v1、sambert-indah-v1、sambert-clara-v1、sambert-hanna-v1、sambert-beth-v1、sambert-betty-v1、sambert-cally-v1、sambert-cindy-v1、sambert-eva-v1、sambert-donna-v1、sambert-brian-v1、sambert-waan-v1，详情请参见 [Sambert模型列表](https://help.aliyun.com/zh/model-studio/sambert-java-sdk#57d33631f7doi "")


在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

调用以下模型时，请选择新加坡地域的 [API Key](https://modelstudio.console.aliyun.com/?tab=dashboard#/api-key)：

- **CosyVoice**：cosyvoice-v3-plus、cosyvoice-v3-flash


更多信息请参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")

## **模型选型**

| **场景** | **推荐模型** | **理由** | **注意事项** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **场景** | **推荐模型** | **理由** | **注意事项** |
| **品牌形象语音定制/个性化语音克隆服务** | cosyvoice-v3-plus | 声音复刻能力最强，支持48kHz高音质输出，高音质+声音复刻，打造拟人化品牌声纹 | 成本较高（2元/万字符），建议用于核心场景 |
| **智能客服 / 语音助手** | cosyvoice-v3-flash | 成本最低（1元/万字符），支持流式交互、情感表达，响应快，性价比高 |  |
| **移动端嵌入式语音合成** | CosyVoice全系列 | SDK全覆盖，资源优化好，流式支持强，延迟可控 | cosyvoice-v1不支持 SSML |
| **方言广播系统** | cosyvoice-v3-flash、cosyvoice-v3-plus | 支持东北话、闽南语等多种方言，适合地方内容播报 | cosyvoice-v3-plus成本较高（2元/万字符） |
| **教育类应用（含公式朗读）** | cosyvoice-v2、cosyvoice-v3-flash、cosyvoice-v3-plus | 支持 [LaTeX](https://help.aliyun.com/zh/model-studio/latex-capability-support-description "") 公式转语音，适合数理化课程讲解 | cosyvoice-v2和cosyvoice-v3-plus成本较高（2元/万字符），cosyvoice-v2不支持设置情感 |
| **结构化语音播报（新闻/公告）** | cosyvoice-v3-plus、cosyvoice-v3-flash、cosyvoice-v2 | 支持 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") 控制语速、停顿、发音等，提升播报专业度 | 需额外开发 SSML 生成逻辑，不支持设置情感 |
| **语音与文本精准对齐（如字幕生成、教学回放、听写训练）** | cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2/Sambert | 支持时间戳输出，可实现合成语音与原文同步 | 需显式启用时间戳功能，默认关闭，cosyvoice-v2不支持设置情感，Sambert不支持流式输入 |
| **多语言出海产品** | cosyvoice-v3-flash、cosyvoice-v3-plus、Sambert | 支持多语种 | Sambert不支持流式输入，价格高于cosyvoice-v3-flash |

不同地域和模型的能力存在差异，请仔细阅读 [模型功能特性对比](https://help.aliyun.com/zh/model-studio/text-to-speech#6e3883d028fqq "") 后再选择使用

## **快速开始**

下面是调用API的示例代码。更多常用场景的代码示例，请参见 [GitHub](https://github.com/aliyun/alibabacloud-bailian-speech-demo)。

您需要已 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 并 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。如果通过SDK调用，还需要 [安装DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。

|     |
| --- |
| **CosyVoice**<br>将合成音频保存为文件<br>将LLM生成的文本实时转成语音并通过扬声器播放<br>Python<br>Java<br>```python<br># coding=utf-8<br>import os<br>import dashscope<br>from dashscope.audio.tts_v2 import *<br># 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key<br># 若没有配置环境变量，请用百炼API Key将下行替换为：dashscope.api_key = "sk-xxx"<br>dashscope.api_key = os.environ.get('DASHSCOPE_API_KEY')<br># 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference<br>dashscope.base_websocket_api_url='wss://dashscope.aliyuncs.com/api-ws/v1/inference'<br># 模型<br># 不同模型版本需要使用对应版本的音色：<br># cosyvoice-v3-flash/cosyvoice-v3-plus：使用longanyang等音色。<br># cosyvoice-v2：使用longxiaochun_v2等音色。<br># 每个音色支持的语言不同，合成日语、韩语等非中文语言时，需选择支持对应语言的音色。详见CosyVoice音色列表。<br>model = "cosyvoice-v3-flash"<br># 音色<br>voice = "longanyang"<br># 实例化SpeechSynthesizer，并在构造方法中传入模型（model）、音色（voice）等请求参数<br>synthesizer = SpeechSynthesizer(model=model, voice=voice)<br># 发送待合成文本，获取二进制音频<br>audio = synthesizer.call("今天天气怎么样？")<br># 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时<br>print('[Metric] requestId为：{}，首包延迟为：{}毫秒'.format(<br>    synthesizer.get_last_request_id(),<br>    synthesizer.get_first_package_delay()))<br># 将音频保存至本地<br>with open('output.mp3', 'wb') as f:<br>    f.write(audio)<br>```<br>```java<br>import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;<br>import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;<br>import com.alibaba.dashscope.utils.Constants;<br>import java.io.File;<br>import java.io.FileOutputStream;<br>import java.io.IOException;<br>import java.nio.ByteBuffer;<br>public class Main {<br>    // 模型<br>    // 不同模型版本需要使用对应版本的音色：<br>    // cosyvoice-v3-flash/cosyvoice-v3-plus：使用longanyang等音色。<br>    // cosyvoice-v2：使用longxiaochun_v2等音色。<br>    // 每个音色支持的语言不同，合成日语、韩语等非中文语言时，需选择支持对应语言的音色。详见CosyVoice音色列表。<br>    private static String model = "cosyvoice-v3-flash";<br>    // 音色<br>    private static String voice = "longanyang";<br>    public static void streamAudioDataToSpeaker() {<br>        // 请求参数<br>        SpeechSynthesisParam param =<br>                SpeechSynthesisParam.builder()<br>                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key<br>                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")<br>                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))<br>                        .model(model) // 模型<br>                        .voice(voice) // 音色<br>                        .build();<br>        // 同步模式：禁用回调（第二个参数为null）<br>        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, null);<br>        ByteBuffer audio = null;<br>        try {<br>            // 阻塞直至音频返回<br>            audio = synthesizer.call("今天天气怎么样？");<br>        } catch (Exception e) {<br>            throw new RuntimeException(e);<br>        } finally {<br>            // 任务结束关闭websocket连接<br>            synthesizer.getDuplexApi().close(1000, "bye");<br>        }<br>        if (audio != null) {<br>            // 将音频数据保存到本地文件“output.mp3”中<br>            File file = new File("output.mp3");<br>            // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时<br>            System.out.println(<br>                    "[Metric] requestId为："<br>                            + synthesizer.getLastRequestId()<br>                            + "首包延迟（毫秒）为："<br>                            + synthesizer.getFirstPackageDelay());<br>            try (FileOutputStream fos = new FileOutputStream(file)) {<br>                fos.write(audio.array());<br>            } catch (IOException e) {<br>                throw new RuntimeException(e);<br>            }<br>        }<br>    }<br>    public static void main(String[] args) {<br>        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference<br>        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";<br>        streamAudioDataToSpeaker();<br>        System.exit(0);<br>    }<br>}<br>```<br>以下代码展示通过本地设备播放千问大语言模型（qwen-turbo）实时返回的文本内容。<br>Python<br>Java<br>运行Python示例前，需要通过pip安装第三方音频播放库。<br>```python<br># coding=utf-8<br># Installation instructions for pyaudio:<br># APPLE Mac OS X<br>#   brew install portaudio<br>#   pip install pyaudio<br># Debian/Ubuntu<br>#   sudo apt-get install python-pyaudio python3-pyaudio<br>#   or<br>#   pip install pyaudio<br># CentOS<br>#   sudo yum install -y portaudio portaudio-devel && pip install pyaudio<br># Microsoft Windows<br>#   python -m pip install pyaudio<br>import os<br>import pyaudio<br>import dashscope<br>from dashscope.audio.tts_v2 import *<br>from http import HTTPStatus<br>from dashscope import Generation<br># 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key<br># 若没有配置环境变量，请用百炼API Key将下行替换为：dashscope.api_key = "sk-xxx"<br>dashscope.api_key = os.environ.get('DASHSCOPE_API_KEY')<br># 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference<br>dashscope.base_websocket_api_url='wss://dashscope.aliyuncs.com/api-ws/v1/inference'<br># 不同模型版本需要使用对应版本的音色：<br># cosyvoice-v3-flash/cosyvoice-v3-plus：使用longanyang等音色。<br># cosyvoice-v2：使用longxiaochun_v2等音色。<br># 每个音色支持的语言不同，合成日语、韩语等非中文语言时，需选择支持对应语言的音色。详见CosyVoice音色列表。<br>model = "cosyvoice-v3-flash"<br>voice = "longanyang"<br>class Callback(ResultCallback):<br>    _player = None<br>    _stream = None<br>    def on_open(self):<br>        print("websocket is open.")<br>        self._player = pyaudio.PyAudio()<br>        self._stream = self._player.open(<br>            format=pyaudio.paInt16, channels=1, rate=22050, output=True<br>        )<br>    def on_complete(self):<br>        print("speech synthesis task complete successfully.")<br>    def on_error(self, message: str):<br>        print(f"speech synthesis task failed, {message}")<br>    def on_close(self):<br>        print("websocket is closed.")<br>        # stop player<br>        self._stream.stop_stream()<br>        self._stream.close()<br>        self._player.terminate()<br>    def on_event(self, message):<br>        print(f"recv speech synthsis message {message}")<br>    def on_data(self, data: bytes) -> None:<br>        print("audio result length:", len(data))<br>        self._stream.write(data)<br>def synthesizer_with_llm():<br>    callback = Callback()<br>    synthesizer = SpeechSynthesizer(<br>        model=model,<br>        voice=voice,<br>        format=AudioFormat.PCM_22050HZ_MONO_16BIT,<br>        callback=callback,<br>    )<br>    messages = [{"role": "user", "content": "请介绍一下你自己"}]<br>    responses = Generation.call(<br>        model="qwen-turbo",<br>        messages=messages,<br>        result_format="message",  # set result format as 'message'<br>        stream=True,  # enable stream output<br>        incremental_output=True,  # enable incremental output <br>    )<br>    for response in responses:<br>        if response.status_code == HTTPStatus.OK:<br>            print(response.output.choices[0]["message"]["content"], end="")<br>            synthesizer.streaming_call(response.output.choices[0]["message"]["content"])<br>        else:<br>            print(<br>                "Request id: %s, Status code: %s, error code: %s, error message: %s"<br>                % (<br>                    response.request_id,<br>                    response.status_code,<br>                    response.code,<br>                    response.message,<br>                )<br>            )<br>    synthesizer.streaming_complete()<br>    print('requestId: ', synthesizer.get_last_request_id())<br>if __name__ == "__main__":<br>    synthesizer_with_llm()<br>```<br>```java<br>import com.alibaba.dashscope.aigc.generation.Generation;<br>import com.alibaba.dashscope.aigc.generation.GenerationParam;<br>import com.alibaba.dashscope.aigc.generation.GenerationResult;<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesisResult;<br>import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisAudioFormat;<br>import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;<br>import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;<br>import com.alibaba.dashscope.common.Message;<br>import com.alibaba.dashscope.common.ResultCallback;<br>import com.alibaba.dashscope.common.Role;<br>import com.alibaba.dashscope.exception.InputRequiredException;<br>import com.alibaba.dashscope.exception.NoApiKeyException;<br>import com.alibaba.dashscope.utils.Constants;<br>import io.reactivex.Flowable;<br>import java.nio.ByteBuffer;<br>import java.util.Arrays;<br>import java.util.concurrent.ConcurrentLinkedQueue;<br>import java.util.concurrent.atomic.AtomicBoolean;<br>import javax.sound.sampled.*;<br>public class Main {<br>    // 不同模型版本需要使用对应版本的音色：<br>    // cosyvoice-v3-flash/cosyvoice-v3-plus：使用longanyang等音色。<br>    // cosyvoice-v2：使用longxiaochun_v2等音色。<br>    // 每个音色支持的语言不同，合成日语、韩语等非中文语言时，需选择支持对应语言的音色。详见CosyVoice音色列表。<br>    private static String model = "cosyvoice-v3-flash";<br>    private static String voice = "longanyang";<br>    public static void process() throws NoApiKeyException, InputRequiredException {<br>        // Playback thread<br>        class PlaybackRunnable implements Runnable {<br>            // Set the audio format. Please configure according to your actual device,<br>            // synthesized audio parameters, and platform choice Here it is set to<br>            // 22050Hz16bit single channel. It is recommended that customers choose other<br>            // sample rates and formats based on the model sample rate and device<br>            // compatibility.<br>            private AudioFormat af = new AudioFormat(22050, 16, 1, true, false);<br>            private DataLine.Info info = new DataLine.Info(SourceDataLine.class, af);<br>            private SourceDataLine targetSource = null;<br>            private AtomicBoolean runFlag = new AtomicBoolean(true);<br>            private ConcurrentLinkedQueue<ByteBuffer> queue =<br>                    new ConcurrentLinkedQueue<>();<br>            // Prepare the player<br>            public void prepare() throws LineUnavailableException {<br>                targetSource = (SourceDataLine) AudioSystem.getLine(info);<br>                targetSource.open(af, 4096);<br>                targetSource.start();<br>            }<br>            public void put(ByteBuffer buffer) {<br>                queue.add(buffer);<br>            }<br>            // Stop playback<br>            public void stop() {<br>                runFlag.set(false);<br>            }<br>            @Override<br>            public void run() {<br>                if (targetSource == null) {<br>                    return;<br>                }<br>                while (runFlag.get()) {<br>                    if (queue.isEmpty()) {<br>                        try {<br>                            Thread.sleep(100);<br>                        } catch (InterruptedException e) {<br>                        }<br>                        continue;<br>                    }<br>                    ByteBuffer buffer = queue.poll();<br>                    if (buffer == null) {<br>                        continue;<br>                    }<br>                    byte[] data = buffer.array();<br>                    targetSource.write(data, 0, data.length);<br>                }<br>                // Play all remaining cache<br>                if (!queue.isEmpty()) {<br>                    ByteBuffer buffer = null;<br>                    while ((buffer = queue.poll()) != null) {<br>                        byte[] data = buffer.array();<br>                        targetSource.write(data, 0, data.length);<br>                    }<br>                }<br>                // Release the player<br>                targetSource.drain();<br>                targetSource.stop();<br>                targetSource.close();<br>            }<br>        }<br>        // Create a subclass inheriting from ResultCallback<SpeechSynthesisResult><br>        // to implement the callback interface<br>        class ReactCallback extends ResultCallback<SpeechSynthesisResult> {<br>            private PlaybackRunnable playbackRunnable = null;<br>            public ReactCallback(PlaybackRunnable playbackRunnable) {<br>                this.playbackRunnable = playbackRunnable;<br>            }<br>            // Callback when the service side returns the streaming synthesis result<br>            @Override<br>            public void onEvent(SpeechSynthesisResult result) {<br>                // Get the binary data of the streaming result via getAudio<br>                if (result.getAudioFrame() != null) {<br>                    // Stream the data to the player<br>                    playbackRunnable.put(result.getAudioFrame());<br>                }<br>            }<br>            // Callback when the service side completes the synthesis<br>            @Override<br>            public void onComplete() {<br>                // Notify the playback thread to end<br>                playbackRunnable.stop();<br>            }<br>            // Callback when an error occurs<br>            @Override<br>            public void onError(Exception e) {<br>                // Tell the playback thread to end<br>                System.out.println(e);<br>                playbackRunnable.stop();<br>            }<br>        }<br>        PlaybackRunnable playbackRunnable = new PlaybackRunnable();<br>        try {<br>            playbackRunnable.prepare();<br>        } catch (LineUnavailableException e) {<br>            throw new RuntimeException(e);<br>        }<br>        Thread playbackThread = new Thread(playbackRunnable);<br>        // Start the playback thread<br>        playbackThread.start();<br>        /*******  Call the Generative AI Model to get streaming text *******/<br>        // Prepare for the LLM call<br>        Generation gen = new Generation();<br>        Message userMsg = Message.builder()<br>                .role(Role.USER.getValue())<br>                .content("请介绍一下你自己")<br>                .build();<br>        GenerationParam genParam =<br>                GenerationParam.builder()<br>                        // 若没有将API Key配置到环境变量中，需将下面这行代码注释放开，并将apiKey替换为自己的API Key<br>                        // .apiKey("apikey")<br>                        .model("qwen-turbo")<br>                        .messages(Arrays.asList(userMsg))<br>                        .resultFormat(GenerationParam.ResultFormat.MESSAGE)<br>                        .topP(0.8)<br>                        .incrementalOutput(true)<br>                        .build();<br>        // Prepare the speech synthesis task<br>        SpeechSynthesisParam param =<br>                SpeechSynthesisParam.builder()<br>                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key<br>                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")<br>                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))<br>                        .model(model)<br>                        .voice(voice)<br>                        .format(SpeechSynthesisAudioFormat<br>                                .PCM_22050HZ_MONO_16BIT)<br>                        .build();<br>        SpeechSynthesizer synthesizer =<br>                new SpeechSynthesizer(param, new ReactCallback(playbackRunnable));<br>        Flowable<GenerationResult> result = gen.streamCall(genParam);<br>        result.blockingForEach(message -> {<br>            String text =<br>                    message.getOutput().getChoices().get(0).getMessage().getContent().trim();<br>            if (text != null && !text.isEmpty()) {<br>                System.out.println("LLM output：" + text);<br>                synthesizer.streamingCall(text);<br>            }<br>        });<br>        synthesizer.streamingComplete();<br>        System.out.print("requestId: " + synthesizer.getLastRequestId());<br>        try {<br>            // Wait for the playback thread to finish playing all<br>            playbackThread.join();<br>        } catch (InterruptedException e) {<br>            throw new RuntimeException(e);<br>        }<br>    }<br>    public static void main(String[] args) throws NoApiKeyException, InputRequiredException {<br>        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference<br>        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";<br>        process();<br>        System.exit(0);<br>    }<br>}<br>``` |
| **Sambert**<br>将合成音频保存为文件<br>将合成的音频通过扬声器播放<br>Python<br>Java<br>Python<br>```python<br>import dashscope<br>from dashscope.audio.tts import SpeechSynthesizer<br># 若没有将API Key配置到环境变量中，需将下面这行代码注释放开，并将apiKey替换为自己的API Key<br># dashscope.api_key = "apiKey"<br>result = SpeechSynthesizer.call(model='sambert-zhichu-v1',<br>                                # 当text内容的语种发生变化时，请确认model是否匹配。不同model支持不同的语种，详情请参见Sambert音色列表中的“语言”列。<br>                                text='今天天气怎么样',<br>                                sample_rate=48000,<br>                                format='wav')<br>print('requestId: ', result.get_response()['request_id'])<br>if result.get_audio_data() is not None:<br>    with open('output.wav', 'wb') as f:<br>        f.write(result.get_audio_data())<br>print(' get response: %s' % (result.get_response()))<br>```<br>Java<br>```java<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesizer;<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesisParam;<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesisResult;<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesisAudioFormat;<br>import com.alibaba.dashscope.common.ResultCallback;<br>import com.alibaba.dashscope.common.Status;<br>import java.io.*;<br>import java.nio.ByteBuffer;<br>public class Main {<br>    public static void SyncAudioDataToFile() {<br>        SpeechSynthesizer synthesizer = new SpeechSynthesizer();<br>        SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>          // 若没有将API Key配置到环境变量中，需将下面这行代码注释放开，并将apiKey替换为自己的API Key<br>          // .apiKey(apikey)<br>          .model("sambert-zhichu-v1")<br>          // 当text内容的语种发生变化时，请确认model是否匹配。不同model支持不同的语种，详情请参见Sambert音色列表中的“语言”列。<br>          .text("今天天气怎么样")<br>          .sampleRate(48000)<br>          .format(SpeechSynthesisAudioFormat.WAV)<br>          .build();<br>        File file = new File("output.wav");<br>        // 调用call方法，传入param参数，获取合成音频<br>        ByteBuffer audio = synthesizer.call(param);<br>        System.out.println("requestId: " + synthesizer.getLastRequestId());<br>        try (FileOutputStream fos = new FileOutputStream(file)) {<br>            fos.write(audio.array());<br>            System.out.println("synthesis done!");<br>        } catch (IOException e) {<br>            throw new RuntimeException(e);<br>        }<br>    }<br>    public static void main(String[] args) {<br>        SyncAudioDataToFile();<br>        System.exit(0);<br>    }<br>}<br>```<br>合成语音后，通过本地设备播放实时返回的音频内容。<br>运行Python示例前，需要通过pip安装第三方音频播放库。<br>Python<br>Java<br>Python<br>```python<br># coding=utf-8<br>#<br># Installation instructions for pyaudio:<br># APPLE Mac OS X<br>#   brew install portaudio<br>#   pip install pyaudio<br># Debian/Ubuntu<br>#   sudo apt-get install python-pyaudio python3-pyaudio<br>#   or<br>#   pip install pyaudio<br># CentOS<br>#   sudo yum install -y portaudio portaudio-devel && pip install pyaudio<br># Microsoft Windows<br>#   python -m pip install pyaudio<br>import dashscope<br>import sys<br>import pyaudio<br>from dashscope.api_entities.dashscope_response import SpeechSynthesisResponse<br>from dashscope.audio.tts import ResultCallback, SpeechSynthesizer, SpeechSynthesisResult<br># 若没有将API Key配置到环境变量中，需将下面这行代码注释放开，并将apiKey替换为自己的API Key<br># dashscope.api_key = "apiKey"<br>class Callback(ResultCallback):<br>    _player = None<br>    _stream = None<br>    def on_open(self):<br>        print('Speech synthesizer is opened.')<br>        self._player = pyaudio.PyAudio()<br>        self._stream = self._player.open(<br>            format=pyaudio.paInt16,<br>            channels=1,<br>            rate=48000,<br>            output=True)<br>    def on_complete(self):<br>        print('Speech synthesizer is completed.')<br>    def on_error(self, response: SpeechSynthesisResponse):<br>        print('Speech synthesizer failed, response is %s' % (str(response)))<br>    def on_close(self):<br>        print('Speech synthesizer is closed.')<br>        self._stream.stop_stream()<br>        self._stream.close()<br>        self._player.terminate()<br>    def on_event(self, result: SpeechSynthesisResult):<br>        if result.get_audio_frame() is not None:<br>            print('audio result length:', sys.getsizeof(result.get_audio_frame()))<br>            self._stream.write(result.get_audio_frame())<br>        if result.get_timestamp() is not None:<br>            print('timestamp result:', str(result.get_timestamp()))<br>callback = Callback()<br>result = SpeechSynthesizer.call(model='sambert-zhichu-v1',<br>                       text='今天天气怎么样',<br>                       sample_rate=48000,<br>                       format='pcm',<br>                       callback=callback)<br>print('requestId: ', result.get_response()['request_id'])<br>```<br>Java<br>```java<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesizer;<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesisAudioFormat;<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesisParam;<br>import com.alibaba.dashscope.audio.tts.SpeechSynthesisResult;<br>import com.alibaba.dashscope.common.ResultCallback;<br>import java.nio.ByteBuffer;<br>import java.util.concurrent.ConcurrentLinkedQueue;<br>import java.util.concurrent.CountDownLatch;<br>import java.util.concurrent.atomic.AtomicBoolean;<br>import javax.sound.sampled.*;<br>public class Main {<br>    public static void StreamAuidoDataToSpeaker() {<br>        CountDownLatch latch = new CountDownLatch(1);<br>        SpeechSynthesizer synthesizer = new SpeechSynthesizer();<br>        SpeechSynthesisParam param =<br>                SpeechSynthesisParam.builder()<br>                        // 若没有将API Key配置到环境变量中，需将下面这行代码注释放开，并将apiKey替换为自己的API Key<br>                        // .apiKey("apikey")<br>                        .text("今天天气怎么样")<br>                        .model("sambert-zhichu-v1")<br>                        .sampleRate(48000)<br>                        .format(SpeechSynthesisAudioFormat.PCM) // 流式合成使用PCM或者MP3<br>                        .build();<br>        // 播放线程<br>        class PlaybackRunnable implements Runnable {<br>            // 设置音频格式，请根据实际自身设备，合成音频参数和平台选择配置<br>            // 这里选择48k16bit单通道，建议客户根据选用的模型采样率情况和自身设备兼容性选择其他采样率和格式<br>            private AudioFormat af = new AudioFormat(48000, 16, 1, true, false);<br>            private DataLine.Info info = new DataLine.Info(SourceDataLine.class, af);<br>            private SourceDataLine targetSource = null;<br>            private AtomicBoolean runFlag = new AtomicBoolean(true);<br>            private ConcurrentLinkedQueue<ByteBuffer> queue = new ConcurrentLinkedQueue<>();<br>            // 准备播放器<br>            public void prepare() throws LineUnavailableException {<br>                targetSource = (SourceDataLine) AudioSystem.getLine(info);<br>                targetSource.open(af, 4096);<br>                targetSource.start();<br>            }<br>            public void put(ByteBuffer buffer) {<br>                queue.add(buffer);<br>            }<br>            // 停止播放<br>            public void stop() {<br>                runFlag.set(false);<br>            }<br>            @Override<br>            public void run() {<br>                if (targetSource == null) {<br>                    return;<br>                }<br>                while (runFlag.get()) {<br>                    if (queue.isEmpty()) {<br>                        try {<br>                            Thread.sleep(100);<br>                        } catch (InterruptedException e) {<br>                        }<br>                        continue;<br>                    }<br>                    ByteBuffer buffer = queue.poll();<br>                    if (buffer == null) {<br>                        continue;<br>                    }<br>                    byte[] data = buffer.array();<br>                    targetSource.write(data, 0, data.length);<br>                }<br>                // 将缓存全部播放完<br>                if (!queue.isEmpty()) {<br>                    ByteBuffer buffer = null;<br>                    while ((buffer = queue.poll()) != null) {<br>                        byte[] data = buffer.array();<br>                        targetSource.write(data, 0, data.length);<br>                    }<br>                }<br>                // 释放播放器<br>                targetSource.drain();<br>                targetSource.stop();<br>                targetSource.close();<br>            }<br>        }<br>        // 创建一个继承自ResultCallback<SpeechSynthesisResult>的子类来实现回调接口<br>        class ReactCallback extends ResultCallback<SpeechSynthesisResult> {<br>            private PlaybackRunnable playbackRunnable = null;<br>            public ReactCallback(PlaybackRunnable playbackRunnable) {<br>                this.playbackRunnable = playbackRunnable;<br>            }<br>            // 当服务侧返回流式合成结果后回调<br>            @Override<br>            public void onEvent(SpeechSynthesisResult result) {<br>                // 通过getAudio获取流式结果二进制数据<br>                if (result.getAudioFrame() != null) {<br>                    // 将数据流式推给播放器<br>                    playbackRunnable.put(result.getAudioFrame());<br>                }<br>            }<br>            // 当服务侧完成合成后回调<br>            @Override<br>            public void onComplete() {<br>                // 告知播放线程结束<br>                playbackRunnable.stop();<br>                latch.countDown();<br>            }<br>            // 当出现错误时回调<br>            @Override<br>            public void onError(Exception e) {<br>                // 告诉播放线程结束<br>                System.out.println(e);<br>                playbackRunnable.stop();<br>                latch.countDown();<br>            }<br>        }<br>        PlaybackRunnable playbackRunnable = new PlaybackRunnable();<br>        try {<br>            playbackRunnable.prepare();<br>        } catch (LineUnavailableException e) {<br>            throw new RuntimeException(e);<br>        }<br>        Thread playbackThread = new Thread(playbackRunnable);<br>        // 启动播放线程<br>        playbackThread.start();<br>        // 带Callback的call方法将不会阻塞当前线程<br>        synthesizer.call(param, new ReactCallback(playbackRunnable));<br>        System.out.println("requestId: " + synthesizer.getLastRequestId());<br>        // 等待合成完成<br>        try {<br>            latch.await();<br>            // 等待播放线程全部播放完<br>            playbackThread.join();<br>        } catch (InterruptedException e) {<br>            throw new RuntimeException(e);<br>        }<br>    }<br>    public static void main(String[] args) {<br>        StreamAuidoDataToSpeaker();<br>        System.exit(0);<br>    }<br>}<br>``` |

## **API参考**

- [语音合成-CosyVoice API参考](https://help.aliyun.com/zh/model-studio/cosyvoice-large-model-for-speech-synthesis/ "")

- [声音复刻-CosyVoice API参考](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api "")

- [语音合成-Sambert API参考](https://help.aliyun.com/zh/model-studio/sambert-speech-synthesis/ "")


## **模型应用上架及备案**

参见 [应用合规备案](https://help.aliyun.com/zh/model-studio/compliance-and-launch-filing-guide-for-ai-apps-powered-by-the-tongyi-model "")。

## **模型功能特性对比**

中国内地

国际

在 [中国内地部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **北京地域**，模型推理计算资源仅限于中国内地。

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **功能/特性** | **cosyvoice-v3-plus** | **cosyvoice-v3-flash** | **cosyvoice-v2** | **cosyvoice-v1** | **Sambert** |
| **支持语言** | [系统音色](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")（因音色而异）：中文（普通话、东北话、闽南话、陕西话）、英文、日语、韩语<br>复刻音色：中文（普通话）、英文、法语、德语、日语、韩语、俄语 | [系统音色](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")（因音色而异）：中文（普通话）、英文<br>复刻音色：中文（普通话、广东话、东北话、甘肃话、贵州话、河南话、湖北话、江西话、闽南话、宁夏话、山西话、陕西话、山东话、上海话、四川话、天津话、云南话）、英文、法语、德语、日语、韩语、俄语 | [系统音色](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")（因音色而异）：中文（普通话）、英文、韩语、日语<br>复刻音色：中文（普通话）、英文 | [系统音色](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")（因音色而异）：中文（普通话）、英文<br>复刻音色：中文（普通话）、英文 | 因 [音色](https://help.aliyun.com/zh/model-studio/sambert-python-sdk#a737f8b6f8gx0 "") 而异：中文、英文、美式英文、意大利语、西班牙语、印尼语、法语、德语、泰语 |
| **音频格式** | pcm、wav、mp3、opus | pcm、wav、mp3 |
| **音频采样率** | 8kHz、16kHz、22.05kHz、24kHz、44.1kHz、48kHz | 16kHz、48kHz |
| **声音复刻** | 支持<br>> 使用方法请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api "")<br>> 声音复刻支持的语言如下：<br>> cosyvoice-v1、cosyvoice-v2：中文（普通话）、英文<br>> cosyvoice-v3-flash：中文（普通话、广东话、东北话、甘肃话、贵州话、河南话、湖北话、江西话、闽南话、宁夏话、山西话、陕西话、山东话、上海话、四川话、天津话、云南话）、英文、法语、德语、日语、韩语、俄语<br>> cosyvoice-v3-plus：中文（普通话）、英文、法语、德语、日语、韩语、俄语 | 不支持 |
| **SSML** | 支持<br>> 该功能适用于复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中已标记为支持 SSML 的系统音色<br>> 使用方法请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") | 不支持 | 支持 |
| **LaTeX** | 支持<br>> 使用方法请参见 [LaTeX 公式转语音](https://help.aliyun.com/zh/model-studio/latex-capability-support-description "") | 不支持 |
| **音量调节** | 支持<br>> 使用方法请参见请求参数`volume` |
| **语速调节** | 支持<br>> 使用方法请参见请求参数`speech_rate`<br>> 在 Java SDK 中，该参数为`speechRate` |
| **语调（音高）调节** | 支持<br>> 使用方法请参见请求参数`pitch_rate`<br>> 在 Java SDK 中，该参数为`pitchRate` |
| **码率调节** | 支持<br>> 仅opus格式音频支持该功能<br>> 使用方法请参见请求参数`bit_rate`<br>> 在 Java SDK 中，该参数为`pitchRate` | 不支持 |
| **时间戳** | 支持默认关闭，可开启<br>> 该功能适用于复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中已标记为支持时间戳的系统音色<br>> 使用方法请参见请求参数`word_timestamp_enabled`<br>> 在 Java SDK 中，该参数为`enableWordTimestamp` | 不支持 | 支持默认关闭，可开启 |
| **指令控制（Instruct）** | 支持<br>> 该功能适用于复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中已标记为支持 Instruct 的系统音色<br>> 使用方法请参见请求参数`instruction` | 不支持 |
| **流式输入** | 支持 | 不支持 |
| **流式输出** | 支持 |
| **限流（RPS）** | 3 | 20 |
| **接入方式** | Java/Python/Android/iOS SDK、WebSocket API |
| **价格** | 2元/万字符 | 1元/万字符 | 2元/万字符 | 1元/万字符 |

在 [国际部署模式](https://help.aliyun.com/zh/model-studio/regions/#080da663a75xh "") 下，接入点与数据存储均位于 **新加坡地域**，模型推理计算资源在全球范围内动态调度（不含中国内地）。

|     |     |     |
| --- | --- | --- |
| **功能/特性** | **cosyvoice-v3-plus** | **cosyvoice-v3-flash** |
| **支持语言** | 因 [系统音色](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 而异：中文（普通话、东北话、闽南话、陕西话）、英文、日语、韩语 | 因 [系统音色](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 而异：中文（普通话）、英文 |
| **音频格式** | pcm、wav、mp3、opus |
| **音频采样率** | 8kHz、16kHz、22.05kHz、24kHz、44.1kHz、48kHz |
| **声音复刻** | 不支持 |
| **SSML** | 支持<br>> 该功能适用于复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中已标记为支持 SSML 的系统音色<br>> 使用方法请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") |
| **LaTeX** | 支持<br>> 使用方法请参见 [LaTeX 公式转语音](https://help.aliyun.com/zh/model-studio/latex-capability-support-description "") |
| **音量调节** | 支持<br>> 使用方法请参见请求参数`volume` |
| **语速调节** | 支持<br>> 使用方法请参见请求参数`speech_rate`<br>> 在 Java SDK 中，该参数为`speechRate` |
| **语调（音高）调节** | 支持<br>> 使用方法请参见请求参数`pitch_rate`<br>> 在 Java SDK 中，该参数为`pitchRate` |
| **码率调节** | 支持<br>> 仅opus格式音频支持该功能<br>> 使用方法请参见请求参数`bit_rate`<br>> 在 Java SDK 中，该参数为`pitchRate` |
| **时间戳** | 支持默认关闭，可开启<br>> 该功能适用于复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中已标记为支持时间戳的系统音色<br>> 使用方法请参见请求参数`word_timestamp_enabled`<br>> 在 Java SDK 中，该参数为`enableWordTimestamp` |
| **指令控制（Instruct）** | 支持<br>> 该功能适用于复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中已标记为支持 Instruct 的系统音色<br>> 使用方法请参见请求参数`instruction` |
| **流式输入** | 支持 |
| **流式输出** | 支持 |
| **限流（RPS）** | 3 |
| **接入方式** | Java/Python/Android/iOS SDK、WebSocket API |
| **价格** | 1.9082元/万字符 | 0.9541元/万字符 |

## **支持的系统音色**

[CosyVoice音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")

[Sambert音色列表](https://help.aliyun.com/zh/model-studio/sambert-java-sdk#57d33631f7doi "")

## **常见问题**

### Q：语音合成的发音读错怎么办？多音字如何控制发音？

- 将多音字替换成同音的其他汉字，快速解决发音问题。

- 使用SSML标记语言控制发音：Sambert和Cosyvoice都支持SSML。


### **Q：使用复刻音色生成的音频无声音如何排查？**

1. **确认音色状态**

调用 [查询指定音色](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api#e1d4d6ee81482 "") 接口，查看音色`status`是否为`OK`。

2. **检查模型版本一致性**

确保复刻音色时使用的`target_model`参数与语音合成时的`model`参数完全一致。例如：

   - 复刻时使用`cosyvoice-v3-plus`

   - 合成时也必须使用`cosyvoice-v3-plus`
3. **验证源音频质量**

检查复刻音色时使用的源音频是否符合 [音频要求](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api#%E9%9F%B3%E9%A2%91%E8%A6%81%E6%B1%82%E4%B8%8E%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5 "")：

   - 音频时长：10-20秒

   - 音质清晰

   - 无背景噪音
4. **检查请求参数**

确认语音合成时请求参数`voice`设置为复刻音色的ID。


### **Q：** 声音复刻后合成效果不稳定或语音不完整如何处理？

如果复刻音色后合成的语音出现以下问题：

- 语音播放不完整，只读出部分文字

- 合成效果不稳定，时好时坏

- 语音中包含异常停顿或静音段


可能原因：源音频质量不符合要求

解决方案：检查源音频是否符合如下要求，建议按照 [录音操作指南](https://help.aliyun.com/zh/model-studio/recording-guide "") 重新录制

- 检查音频连续性：确保源音频中语音内容连续，避免长时间停顿或静音段（超过2秒）。如果音频中存在明显的空白段，会导致模型将静音或噪声作为音色特征的一部分，影响生成效果

- 检查语音活动比例：确保有效语音占音频总时长的60%以上。如果背景噪声、非语音段过多，会干扰音色特征提取

- 验证音频质量细节：

  - 音频时长：10-20秒（推荐15秒左右）

  - 发音清晰，语速平稳

  - 无背景噪音、回音、杂音

  - 语音能量集中，无长时间静音段