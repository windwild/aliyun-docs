### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音合成](https://help.aliyun.com/zh/model-studio/speech-synthesis-api-reference/)[实时语音合成（CosyVoice）](https://help.aliyun.com/zh/model-studio/cosyvoice-large-model-for-speech-synthesis/)Java SDK

# 语音合成CosyVoice Java SDK

更新时间：2026-02-10 08:56:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：实时多模态交互流程](https://help.aliyun.com/zh/model-studio/omni-realtime-interaction-process)[下一篇：Python SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk)

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

通过Flowable调用

高并发调用

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

本文介绍语音合成CosyVoice Java SDK的参数和接口细节。

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

- [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#82d9324616ifx "")、 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#cc2a504f344s2 "") 或Flowable单向流式调用：单次发送文本长度不得超过 20000 字符。

- [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "") 或Flowable双向流式调用：单次发送文本长度不得超过 20000 字符，且累计发送文本总长度不得超过 20 万字符。


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

- 使用 [DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "") 2.20.3 或更高版本

- 仅支持 [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#82d9324616ifx "") 和 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#cc2a504f344s2 "")（即 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`call`方法），不支持 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "")（即 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`streamingCall`方法）和 [Flowable调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#b0f81fef83ojo "")。

- 使用方法与普通语音合成一致：将包含SSML的文本传入 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`call`方法即可


## **快速开始**

[SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 提供了语音合成的关键接口，支持以下几种调用方式：

- 非流式调用：阻塞式，一次性发送完整文本，直接返回完整音频。适合短文本语音合成场景。

- 单向流式调用：非阻塞式，一次性发送完整文本，通过回调函数接收音频数据（可能分片）。适用于对实时性要求高的短文本语音合成场景。

- 双向流式调用：非阻塞式，可分多次发送文本片段，通过回调函数实时接收增量合成的音频流。适合实时性要求高的长文本语音合成场景。


### **非流式调用**

同步提交语音合成任务，直接获取完整结果。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6771370771/CAEQURiBgIDHpsn4phkiIDQ0ZGE2OTk3NmY5NTRhNDVhZDQwNWE3ZGZiMzk4Yjk54709861_20241015153444.149.svg)

实例化 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 绑定 [请求参数](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#a96bfa6340jdd "")，调用`call`方法进行合成并获取二进制音频数据。

发送的文本长度不得超过20000字符（详情请参见 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`call`方法）。

**重要**

每次调用`call`方法前，需要重新初始化`SpeechSynthesizer`实例。

**点击查看完整示例**

```java
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.utils.Constants;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;

public class Main {
    // 模型
    private static String model = "cosyvoice-v3-flash";
    // 音色
    private static String voice = "longanyang";

    public static void streamAudioDataToSpeaker() {
        // 请求参数
        SpeechSynthesisParam param =
                SpeechSynthesisParam.builder()
                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                        .model(model) // 模型
                        .voice(voice) // 音色
                        .build();

        // 同步模式：禁用回调（第二个参数为null）
        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, null);
        ByteBuffer audio = null;
        try {
            // 阻塞直至音频返回
            audio = synthesizer.call("今天天气怎么样？");
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            // 任务结束关闭websocket连接
            synthesizer.getDuplexApi().close(1000, "bye");
        }
        if (audio != null) {
            // 将音频数据保存到本地文件“output.mp3”中
            File file = new File("output.mp3");
            // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
            System.out.println(
                    "[Metric] requestId为："
                            + synthesizer.getLastRequestId()
                            + "首包延迟（毫秒）为："
                            + synthesizer.getFirstPackageDelay());
            try (FileOutputStream fos = new FileOutputStream(file)) {
                fos.write(audio.array());
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }

    public static void main(String[] args) {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        streamAudioDataToSpeaker();
        System.exit(0);
    }
}
```

### **单向流式调用**

异步提交语音合成任务，通过注册`ResultCallback`回调，逐帧接收实时语音分段数据。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6771370771/CAEQVRiBgMCfo..hrBkiIGEyMjNkZjVlMWZiYzRhZDU4ZjEyZjdjMmMzYjM1YzMz4709861_20241015153444.149.svg)

实例化 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 绑定 [请求参数](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#a96bfa6340jdd "") 和 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "")，调用`call`方法进行合成并通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "") 的`onEvent`方法实时获取合成结果。

发送的文本长度不得超过20000字符（详情请参见 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`call`方法）。

**重要**

每次调用`call`方法前，需要重新初始化`SpeechSynthesizer`实例。

**点击查看完整示例**

```java
import com.alibaba.dashscope.audio.tts.SpeechSynthesisResult;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.common.ResultCallback;
import com.alibaba.dashscope.utils.Constants;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.concurrent.CountDownLatch;

class TimeUtils {
    private static final DateTimeFormatter formatter =
            DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss.SSS");

    public static String getTimestamp() {
        return LocalDateTime.now().format(formatter);
    }
}

public class Main {
    // 模型
    private static String model = "cosyvoice-v3-flash";
    // 音色
    private static String voice = "longanyang";

    public static void streamAudioDataToSpeaker() {
        CountDownLatch latch = new CountDownLatch(1);

        // 实现回调接口ResultCallback
        ResultCallback<SpeechSynthesisResult> callback = new ResultCallback<SpeechSynthesisResult>() {
            @Override
            public void onEvent(SpeechSynthesisResult result) {
                // System.out.println("收到消息: " + result);
                if (result.getAudioFrame() != null) {
                    // 此处实现保存音频数据到本地的逻辑
                    System.out.println(TimeUtils.getTimestamp() + " 收到音频");
                }
            }

            @Override
            public void onComplete() {
                System.out.println(TimeUtils.getTimestamp() + " 收到Complete，语音合成结束");
                latch.countDown();
            }

            @Override
            public void onError(Exception e) {
                System.out.println("出现异常：" + e.toString());
                latch.countDown();
            }
        };

        // 请求参数
        SpeechSynthesisParam param =
                SpeechSynthesisParam.builder()
                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                        .model(model) // 模型
                        .voice(voice) // 音色
                        .build();
        // 第二个参数“callback”传入回调即启用异步模式
        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, callback);
        // 非阻塞调用，立即返回null（实际结果通过回调接口异步传递），在回调接口的onEvent方法中实时获取二进制音频
        try {
            synthesizer.call("今天天气怎么样？");
            // 等待合成完成
            latch.await();
            // 等待播放线程全部播放完
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            // 任务结束后关闭websocket连接
            synthesizer.getDuplexApi().close(1000, "bye");
        }
        // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        System.out.println(
                "[Metric] requestId为："
                        + synthesizer.getLastRequestId()
                        + "，首包延迟（毫秒）为："
                        + synthesizer.getFirstPackageDelay());
    }

    public static void main(String[] args) {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        streamAudioDataToSpeaker();
        System.exit(0);
    }
}
```

### 双向流式调用

分多次提交文本，通过注册`ResultCallback`回调，逐帧接收实时语音分段数据。

**说明**

- 流式输入时可多次调用`streamingCall`按顺序提交文本片段。服务端接收文本片段后自动进行分句：


  - 完整语句立即合成

  - 不完整语句缓存至完整后合成


调用 `streamingComplete` 时，服务端会强制合成所有已接收但未处理的文本片段（包括未完成的句子）。

- 发送文本片段的间隔不得超过23秒，否则触发“request timeout after 23 seconds”异常。

若无待发送文本，需及时调用 `streamingComplete`结束任务。


> 服务端强制设定23秒超时机制，客户端无法修改该配置。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6771370771/CAEQVRiBgICHxPGhrBkiIGE3ZTVmMzY0YzI3NzQxYTFiYWE2MmU2NTBhMDgzZGM14709861_20241015153444.149.svg)

1. 实例化SpeechSynthesizer类

实例化 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 绑定 [请求参数](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#a96bfa6340jdd "") 和 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "")。

2. 流式传输

多次调用 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`streamingCall`方法分片提交待合成文本，将待合成文本分段发送至服务端。

在发送文本的过程中，服务端会通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "") 的`onEvent`方法，将合成结果实时返回给客户端。

每次调用`streamingCall`方法发送的文本片段（即`text`）长度不得超过20000字符，累计发送的文本总长度不得超过20万字符。

3. 结束处理

调用 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`streamingComplete`方法结束语音合成。

该方法会阻塞当前线程，直到 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "") 的`onComplete`或者`onError`回调触发后才会释放线程阻塞。

请务必确保调用该方法，否则可能会导致结尾部分的文本无法成功转换为语音。


**点击查看完整示例**

```java
import com.alibaba.dashscope.audio.tts.SpeechSynthesisResult;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisAudioFormat;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.common.ResultCallback;
import com.alibaba.dashscope.utils.Constants;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

class TimeUtils {
    private static final DateTimeFormatter formatter =
            DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss.SSS");

    public static String getTimestamp() {
        return LocalDateTime.now().format(formatter);
    }
}

public class Main {
    private static String[] textArray = {"流式文本语音合成SDK，",
            "可以将输入的文本", "合成为语音二进制数据，", "相比于非流式语音合成，",
            "流式合成的优势在于实时性", "更强。用户在输入文本的同时",
            "可以听到接近同步的语音输出，", "极大地提升了交互体验，",
            "减少了用户等待时间。", "适用于调用大规模", "语言模型（LLM），以",
            "流式输入文本的方式", "进行语音合成的场景。"};
    private static String model = "cosyvoice-v3-flash"; // 模型
    private static String voice = "longanyang"; // 音色

    public static void streamAudioDataToSpeaker() {
        // 配置回调函数
        ResultCallback<SpeechSynthesisResult> callback = new ResultCallback<SpeechSynthesisResult>() {
            @Override
            public void onEvent(SpeechSynthesisResult result) {
                // System.out.println("收到消息: " + result);
                if (result.getAudioFrame() != null) {
                    // 此处实现处理音频数据的逻辑
                    System.out.println(TimeUtils.getTimestamp() + " 收到音频");
                }
            }

            @Override
            public void onComplete() {
                System.out.println(TimeUtils.getTimestamp() + " 收到Complete，语音合成结束");
            }

            @Override
            public void onError(Exception e) {
                System.out.println("出现异常：" + e.toString());
            }
        };

        // 请求参数
        SpeechSynthesisParam param =
                SpeechSynthesisParam.builder()
                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                        .model(model)
                        .voice(voice)
                        .format(SpeechSynthesisAudioFormat
                                .PCM_22050HZ_MONO_16BIT) // 流式合成使用PCM或者MP3
                        .build();
        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, callback);
        // 带Callback的call方法将不会阻塞当前线程
        try {
            for (String text : textArray) {
                // 发送文本片段，在回调接口的onEvent方法中实时获取二进制音频
                synthesizer.streamingCall(text);
            }
            // 等待结束流式语音合成
            synthesizer.streamingComplete();
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            // 任务结束关闭websocket连接
            synthesizer.getDuplexApi().close(1000, "bye");
        }

        // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        System.out.println(
                "[Metric] requestId为："
                        + synthesizer.getLastRequestId()
                        + "，首包延迟（毫秒）为："
                        + synthesizer.getFirstPackageDelay());
    }

    public static void main(String[] args) {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        streamAudioDataToSpeaker();
        System.exit(0);
    }
}
```

### **通过Flowable调用**

Flowable是一个用于工作流和业务流程管理的开源框架，它基于Apache 2.0许可证发布。关于Flowable的使用，请参见 [Flowable API详情](http://reactivex.io/RxJava/2.x/javadoc/)。

使用Flowable前需确保已集成RxJava库，并了解响应式编程基础概念。

单向流式调用

双向流式调用

以下示例展示了通过Flowable对象的`blockingForEach`接口，阻塞式地获取每次流式返回的`SpeechSynthesisResult`类型数据。

您也可以在Flowable的所有流式数据返回完成后，通过 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`getAudioData`来获取完整的合成结果。

**点击查看完整示例**

```java
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

class TimeUtils {
    private static final DateTimeFormatter formatter =
            DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss.SSS");

    public static String getTimestamp() {
        return LocalDateTime.now().format(formatter);
    }
}

public class Main {
    private static String model = "cosyvoice-v3-flash"; // 模型
    private static String voice = "longanyang"; // 音色

    public static void streamAudioDataToSpeaker() throws NoApiKeyException {
        // 请求参数
        SpeechSynthesisParam param =
                SpeechSynthesisParam.builder()
                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                        .model(model) // 模型
                        .voice(voice) // 音色
                        .build();
        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, null);
        synthesizer.callAsFlowable("今天天气怎么样?").blockingForEach(result -> {
            // System.out.println("收到消息: " + result);
            if (result.getAudioFrame() != null) {
                // 此处实现处理音频数据的逻辑
                System.out.println(TimeUtils.getTimestamp() + " 收到音频");
            }
        });
        // 任务结束关闭 WebSocket 连接
        synthesizer.getDuplexApi().close(1000, "bye");
        // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        System.out.println(
                "[Metric] requestId为："
                        + synthesizer.getLastRequestId()
                        + "首包延迟（毫秒）为："
                        + synthesizer.getFirstPackageDelay());
    }

    public static void main(String[] args) throws NoApiKeyException {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        streamAudioDataToSpeaker();
        System.exit(0);
    }
}
```

以下示例展示了通过Flowable对象作为输入参数，输入文本流。并通过Flowable对象作为返回值，利用的`blockingForEach`接口，阻塞式地获取每次流式返回的`SpeechSynthesisResult`类型数据。

您也可以在Flowable的所有流式数据返回完成后，通过 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`getAudioData`来获取完整的合成结果。

**点击查看完整示例**

```java
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.utils.Constants;
import io.reactivex.BackpressureStrategy;
import io.reactivex.Flowable;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

class TimeUtils {
    private static final DateTimeFormatter formatter =
            DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss.SSS");

    public static String getTimestamp() {
        return LocalDateTime.now().format(formatter);
    }
}

public class Main {
    private static String[] textArray = {"流式文本语音合成SDK，",
            "可以将输入的文本", "合成为语音二进制数据，", "相比于非流式语音合成，",
            "流式合成的优势在于实时性", "更强。用户在输入文本的同时",
            "可以听到接近同步的语音输出，", "极大地提升了交互体验，",
            "减少了用户等待时间。", "适用于调用大规模", "语言模型（LLM），以",
            "流式输入文本的方式", "进行语音合成的场景。"};
    private static String model = "cosyvoice-v3-flash";
    private static String voice = "longanyang";

    public static void streamAudioDataToSpeaker() throws NoApiKeyException {
        // 模拟流式输入
        Flowable<String> textSource = Flowable.create(emitter -> {
            new Thread(() -> {
                for (int i = 0; i < textArray.length; i++) {
                    emitter.onNext(textArray[i]);
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        throw new RuntimeException(e);
                    }
                }
                emitter.onComplete();
            }).start();
        }, BackpressureStrategy.BUFFER);

        // 请求参数
        SpeechSynthesisParam param =
                SpeechSynthesisParam.builder()
                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                        .model(model) // 模型
                        .voice(voice) // 音色
                        .build();
        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, null);
        synthesizer.streamingCallAsFlowable(textSource).blockingForEach(result -> {
            if (result.getAudioFrame() != null) {
                // 此处实现播放音频的逻辑
                System.out.println(
                        TimeUtils.getTimestamp() +
                                " 二进制音频大小为：" + result.getAudioFrame().capacity());
            }
        });
        synthesizer.getDuplexApi().close(1000, "bye");
        // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        System.out.println(
                "[Metric] requestId为："
                        + synthesizer.getLastRequestId()
                        + "，首包延迟（毫秒）为："
                        + synthesizer.getFirstPackageDelay());
    }

    public static void main(String[] args) throws NoApiKeyException {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        streamAudioDataToSpeaker();
        System.exit(0);
    }
}
```

### **高并发调用**

在DashScope Java SDK中，采用了OkHttp3的连接池技术，以减少重复建立连接的开销。详情请参见 [高并发场景](https://help.aliyun.com/zh/model-studio/high-concurrency-scenarios "")。

## **请求参数**

通过SpeechSynthesisParam的链式方法配置模型、音色等参数。配置完成的参数对象传入 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的构造函数中使用。

**点击查看示例**

```java
SpeechSynthesisParam param = SpeechSynthesisParam.builder()
    .model("cosyvoice-v3-flash") // 模型
    .voice("longanyang") // 音色
    .format(SpeechSynthesisAudioFormat.WAV_8000HZ_MONO_16BIT) // 音频编码格式、采样率
    .volume(50) // 音量，取值范围：[0, 100]
    .speechRate(1.0f) // 语速，取值范围：[0.5, 2]
    .pitchRate(1.0f) // 语调，取值范围：[0.5, 2]
    .build();
```

| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| model | String | 是 | 语音合成[模型](https://help.aliyun.com/zh/model-studio/models#7a960cc042zwt "")。<br>不同模型版本需要使用对应版本的音色：<br>- cosyvoice-v3-flash/cosyvoice-v3-plus：使用longanyang等音色。<br>  <br>- cosyvoice-v2：使用longxiaochun\_v2等音色。<br>  <br>- cosyvoice-v1：使用longwan等音色。<br>  <br>- 完整音色列表请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")。 |
| voice | String | 是 | 语音合成所使用的音色。<br>支持系统音色和复刻音色：<br>- **系统音色**：参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")。<br>  <br>- **复刻音色**：通过 [声音复刻](https://help.aliyun.com/zh/model-studio/voice-replica-1/ "") 功能定制。使用复刻音色时，请确保声音复刻与语音合成使用同一账号。详细操作步骤请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api#da30eeebc4uwk "")。<br>  <br>  使用声音复刻生成的复刻音色时，本请求的`model`参数值，必须与创建该音色时所用的模型版本（即`target_model`参数）完全一致。 |
| format | enum | 否 | 音频编码格式及采样率。<br>若未指定`format`，则合成音频采样率为22.05kHz，格式为mp3。<br>**说明**<br>默认采样率代表当前音色的最佳采样率，缺省条件下默认按照该采样率输出，同时支持降采样或升采样。<br>可指定的音频编码格式及采样率如下：<br>- 所有模型均支持的音频编码格式及采样率：<br>  <br>  - SpeechSynthesisAudioFormat.WAV\_8000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为8kHz<br>    <br>  - SpeechSynthesisAudioFormat.WAV\_16000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为16kHz<br>    <br>  - SpeechSynthesisAudioFormat.WAV\_22050HZ\_MONO\_16BIT，代表音频格式为wav，采样率为22.05kHz<br>    <br>  - SpeechSynthesisAudioFormat.WAV\_24000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为24kHz<br>    <br>  - SpeechSynthesisAudioFormat.WAV\_44100HZ\_MONO\_16BIT，代表音频格式为wav，采样率为44.1kHz<br>    <br>  - SpeechSynthesisAudioFormat.WAV\_48000HZ\_MONO\_16BIT，代表音频格式为wav，采样率为48kHz<br>    <br>  - SpeechSynthesisAudioFormat.MP3\_8000HZ\_MONO\_128KBPS，代表音频格式为mp3，采样率为8kHz<br>    <br>  - SpeechSynthesisAudioFormat.MP3\_16000HZ\_MONO\_128KBPS，代表音频格式为mp3，采样率为16kHz<br>    <br>  - SpeechSynthesisAudioFormat.MP3\_22050HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为22.05kHz<br>    <br>  - SpeechSynthesisAudioFormat.MP3\_24000HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为24kHz<br>    <br>  - SpeechSynthesisAudioFormat.MP3\_44100HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为44.1kHz<br>    <br>  - SpeechSynthesisAudioFormat.MP3\_48000HZ\_MONO\_256KBPS，代表音频格式为mp3，采样率为48kHz<br>    <br>  - SpeechSynthesisAudioFormat.PCM\_8000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为8kHz<br>    <br>  - SpeechSynthesisAudioFormat.PCM\_16000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为16kHz<br>    <br>  - SpeechSynthesisAudioFormat.PCM\_22050HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为22.05kHz<br>    <br>  - SpeechSynthesisAudioFormat.PCM\_24000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为24kHz<br>    <br>  - SpeechSynthesisAudioFormat.PCM\_44100HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为44.1kHz<br>    <br>  - SpeechSynthesisAudioFormat.PCM\_48000HZ\_MONO\_16BIT，代表音频格式为pcm，采样率为48kHz<br>- 除`cosyvoice-v1`外，其他模型支持的音频编码格式及采样率：<br>  <br>  音频格式为opus时，支持通过`bit_rate`参数调整码率。仅对2.21.0及之后版本的DashScope适用。<br>  <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_8KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为8kHz，码率为32kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_16KHZ\_MONO\_16KBPS，代表音频格式为opus，采样率为16kHz，码率为16kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_16KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为16kHz，码率为32kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_16KHZ\_MONO\_64KBPS，代表音频格式为opus，采样率为16kHz，码率为64kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_24KHZ\_MONO\_16KBPS，代表音频格式为opus，采样率为24kHz，码率为16kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_24KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为24kHz，码率为32kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_24KHZ\_MONO\_64KBPS，代表音频格式为opus，采样率为24kHz，码率为64kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_48KHZ\_MONO\_16KBPS，代表音频格式为opus，采样率为48kHz，码率为16kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_48KHZ\_MONO\_32KBPS，代表音频格式为opus，采样率为48kHz，码率为32kbps<br>    <br>  - SpeechSynthesisAudioFormat.OGG\_OPUS\_48KHZ\_MONO\_64KBPS，代表音频格式为opus，采样率为48kHz，码率为64kbps |
| volume | int | 否 | 音量。<br>默认值：50。<br>取值范围：\[0, 100\]。50代表标准音量。音量大小与该值呈线性关系，0为静音，100为最大音量。 |
| speechRate | float | 否 | 语速。<br>默认值：1.0。<br>取值范围：\[0.5, 2.0\]。1.0为标准语速，小于1.0则减慢，大于1.0则加快。 |
| pitchRate | float | 否 | 音高。该值作为音高调节的乘数，但其与听感上的音高变化并非严格的线性或对数关系，建议通过测试选择合适的值。<br>默认值：1.0。<br>取值范围：\[0.5, 2.0\]。1.0为音色自然音高。大于1.0则音高变高，小于1.0则音高变低。 |
| bit\_rate | int | 否 | 音频码率（单位kbps）。音频格式为opus时，支持通过`bit_rate`参数调整码率。<br>默认值：32。<br>取值范围：\[6, 510\]。<br>`cosyvoice-v1`模型不支持该参数。<br>**说明**<br>`bit_rate`需要通过`SpeechSynthesisParam`实例的`parameter`方法或者`parameters`方法进行设置：<br>通过parameter设置<br>通过parameters设置<br>```java<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameter("bit_rate", 32)<br>    .build();<br>```<br>```java<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameters(Collections.singletonMap("bit_rate", 32))<br>    .build();<br>``` |
| enableWordTimestamp | boolean | 否 | 是否开启字级别时间戳。<br>默认值：false。<br>- true：开启。<br>  <br>- false：关闭。<br>  <br>该功能仅适用于cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持的系统音色。<br>> 时间戳结果仅能通过回调接口获取 |
| seed | int | 否 | 生成时使用的随机数种子，使合成的效果产生变化。在模型版本、文本、音色及其他参数均相同的前提下，使用相同的seed可复现相同的合成结果。<br>默认值0。<br>取值范围：\[0, 65535\]。<br>cosyvoice-v1不支持该功能。 |
| languageHints | List | 否 | 指定语音合成的目标语言，提升合成效果。cosyvoice-v1不支持该功能。<br>当数字、缩写、符号等朗读方式或者小语种合成效果不符合预期时使用，例如：<br>- 数字朗读方式不符合预期，“hello, this is 110”读成“hello, this is one one zero”而非“hello, this is 幺幺零”<br>  <br>- 符号朗读不准确，“@”读成“艾特”而非“at”<br>  <br>- 小语种合成效果差，合成不自然<br>  <br>取值范围：<br>- zh：中文<br>  <br>- en：英文<br>  <br>- fr：法语<br>  <br>- de：德语<br>  <br>- ja：日语<br>  <br>- ko：韩语<br>  <br>- ru：俄语<br>  <br>**注意**：此参数为数组，但当前版本仅处理第一个元素，因此建议只传入一个值。<br>**重要**<br>此参数用于指定语音合成的目标语言，该设置与声音复刻时的样本音频的语种无关。如果您需要设置复刻任务的源语言，请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/model-studio/cosyvoice-clone-api "")。 |
| instruction | String | 否 | 设置指令，用于控制方言、情感或角色等合成效果。该功能仅适用于cosyvoice-v3-flash模型的复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色。<br>**使用要求**：<br>- 指令必须使用固定格式和内容（见下方说明）<br>  <br>- 不设置时不生效（无默认值）<br>  <br>**支持的功能**：<br>- 指定方言<br>  <br>  - 适用音色：仅复刻音色<br>    <br>  - 格式：“`请用<方言>表达。`”（注意，结尾一定不要遗漏句号，使用时将“`<方言>`”替换为具体的`方言`，例如替换为`广东话`）。<br>    <br>  - 示例：“`请用广东话表达。`”<br>    <br>  - 支持的方言：广东话、东北话、甘肃话、贵州话、河南话、湖北话、江西话、闽南话、宁夏话、山西话、陕西话、山东话、上海话、四川话、天津话、云南话。<br>- 指定情感<br>  <br>  - 适用音色<br>    <br>    - 复刻音色<br>      <br>    - [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色<br>  - 格式：<br>    <br>    - 复刻音色：<br>      <br>      <br>      <br>      点击查看复刻音色指令格式<br>      <br>      <br>      <br>      <br>      <br>      <br>      - `请尽可能非常大声地说一句话。`<br>        <br>      - `请用尽可能慢地语速说一句话。`<br>        <br>      - `请用尽可能快地语速说一句话。`<br>        <br>      - `请非常轻声地说一句话。`<br>        <br>      - `你可以慢一点说吗`<br>        <br>      - `你可以非常快一点说吗`<br>        <br>      - `你可以非常慢一点说吗`<br>        <br>      - `你可以快一点说吗`<br>        <br>      - `请非常生气地说一句话。`<br>        <br>      - `请非常开心地说一句话。`<br>        <br>      - `请非常恐惧地说一句话。`<br>        <br>      - `请非常伤心地说一句话。`<br>        <br>      - `请非常惊讶地说一句话。`<br>        <br>      - `请尽可能表现出坚定的感觉。`<br>        <br>      - `请尽可能表现出愤怒的感觉。`<br>        <br>      - `请尝试一下亲和的语调。`<br>        <br>      - `请用冷酷的语调讲话。`<br>        <br>      - `请用威严的语调讲话。`<br>        <br>      - `我想体验一下自然的语气。`<br>        <br>      - `我想看看你如何表达威胁。`<br>        <br>      - `我想看看你怎么表现智慧。`<br>        <br>      - `我想看看你怎么表现诱惑。`<br>        <br>      - `我想听听用活泼的方式说话。`<br>        <br>      - `我想听听你用激昂的感觉说话。`<br>        <br>      - `我想听听用沉稳的方式说话的样子。`<br>        <br>      - `我想听听你用自信的感觉说话。`<br>        <br>      - `你能用兴奋的感觉和我交流吗？`<br>        <br>      - `你能否展示狂傲的情绪表达？`<br>        <br>      - `你能展现一下优雅的情绪吗？`<br>        <br>      - `你可以用幸福的方式回答问题吗？`<br>        <br>      - `你可以做一个温柔的情感演示吗？`<br>        <br>      - `能用冷静的语调和我谈谈吗？`<br>        <br>      - `能用深沉的方法回答我吗？`<br>        <br>      - `能用粗犷的情绪态度和我对话吗？`<br>        <br>      - `用阴森的声音告诉我这个答案。`<br>        <br>      - `用坚韧的声音告诉我这个答案。`<br>        <br>      - `用自然亲切的闲聊风格叙述。`<br>        <br>      - `用广播剧博客主的语气讲话。`<br>        <br>    - 系统音色：系统音色和复刻音色的情感指令格式不同，详情请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "")<br>- 指定场景、角色或身份等<br>  <br>  - 适用音色： [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持Instruct的系统音色<br>    <br>  - 格式：请参见 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") |
| enable\_aigc\_tag | boolean | 否 | 是否在生成的音频中添加AIGC隐性标识。设置为true时，会将隐性标识嵌入到支持格式（wav/mp3/opus）的音频中。<br>默认值：false。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。<br>**说明**<br>`enable_aigc_tag`需要通过`SpeechSynthesisParam`实例的`parameter`方法或者`parameters`方法进行设置：<br>通过parameter设置<br>通过parameters设置<br>```java<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameter("enable_aigc_tag", true)<br>    .build();<br>```<br>```java<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameters(Collections.singletonMap("enable_aigc_tag", true))<br>    .build();<br>``` |
| aigc\_propagator | String | 否 | 设置AIGC隐性标识中的 `ContentPropagator` 字段，用于标识内容的传播者。仅在 `enable_aigc_tag` 为 `true` 时生效。<br>默认值：阿里云UID。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。<br>**说明**<br>`aigc_propagator`需要通过`SpeechSynthesisParam`实例的`parameter`方法或者`parameters`方法进行设置：<br>通过parameter设置<br>通过parameters设置<br>```java<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameter("enable_aigc_tag", true)<br>    .parameter("aigc_propagator", "xxxx")<br>    .build();<br>```<br>```java<br>Map<String, Object> map = new HashMap();<br>map.put("enable_aigc_tag", true);<br>map.put("aigc_propagator", "xxxx");<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameters(map)<br>    .build();<br>``` |
| aigc\_propagate\_id | String | 否 | 设置AIGC隐性标识中的 `PropagateID` 字段，用于唯一标识一次具体的传播行为。仅在 `enable_aigc_tag` 为 `true` 时生效。<br>默认值：本次语音合成请求Request ID。<br>仅cosyvoice-v3-flash、cosyvoice-v3-plus、cosyvoice-v2支持该功能。<br>**说明**<br>`aigc_propagate_id`需要通过`SpeechSynthesisParam`实例的`parameter`方法或者`parameters`方法进行设置：<br>通过parameter设置<br>通过parameters设置<br>```java<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameter("enable_aigc_tag", true)<br>    .parameter("aigc_propagate_id", "xxxx")<br>    .build();<br>```<br>```java<br>Map<String, Object> map = new HashMap();<br>map.put("enable_aigc_tag", true);<br>map.put("aigc_propagate_id", "xxxx");<br>SpeechSynthesisParam param = SpeechSynthesisParam.builder()<br>    .model("cosyvoice-v3-flash") // 模型<br>    .voice("longanyang") // 音色<br>    .parameters(map)<br>    .build();<br>``` |

## **关键接口**

### `SpeechSynthesizer`类

`SpeechSynthesizer`通过“`import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;`”方式引入，提供语音合成的关键接口。

| **接口/方法** | **参数** | **返回值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **接口/方法** | **参数** | **返回值** | **描述** |
| ```java<br>public SpeechSynthesizer(SpeechSynthesisParam param, ResultCallback<SpeechSynthesisResult> callback)<br>``` | - `param`： [请求参数](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#a96bfa6340jdd "")<br>  <br>- `callback`：<br>  <br>  - [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "")：单向/双向流式调用<br>    <br>  - `null`：非流式调用 | `SpeechSynthesizer`实例 | 构造函数。<br>- 当您使用 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#cc2a504f344s2 "") 或 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "") 时，请将callback参数设置为 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "")。<br>  <br>- 当您使用 [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#82d9324616ifx "") 或 [通过Flowable调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#b0f81fef83ojo "") 时，请将callback参数设为null。 |
| ```java<br>public ByteBuffer call(String text)<br>``` | `text`：待合成文本（UTF-8） | `ByteBuffer`或`null` | 将整段文本（无论是纯文本还是包含 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") 的文本）转换为语音。<br>在创建`SpeechSynthesizer`实例时，存在以下两种情况：<br>- 没有指定`ResultCallback`：`call`方法会阻塞当前线程直到语音合成完成。使用方法请参见 [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#82d9324616ifx "")。<br>  <br>- 指定了`ResultCallback`：`call`方法会立刻返回null。合成结果通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "") 的`onEvent`方法获取。使用方法请参见 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#cc2a504f344s2 "")。<br>  <br>**重要**<br>每次调用`call`方法前，需要重新初始化`SpeechSynthesizer`实例。 |
| ```java<br>public void streamingCall(String text)<br>``` | `text`：待合成文本（UTF-8） | 无 | 流式发送待合成文本（不支持包含SSML的文本）。<br>您可以多次调用该接口，将待合成文本分多次发送给服务端。合成结果通过 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "") 的`onEvent`方法获取。<br>详细调用流程和参考示例请参见 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "")。 |
| ```java<br>public void streamingComplete() throws RuntimeException<br>``` | 无 | 无 | 结束流式语音合成。<br>该方法阻塞调用线程直至发生以下条件之一：<br>- 服务端完成最终音频合成（成功）<br>  <br>- 流式会话异常中断（失败）<br>  <br>- 达到10分钟超时阈值（自动解除阻塞）<br>  <br>详细的调用流程和参考示例请参见 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "")。<br>**重要**<br>[双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "") 时，请确保调用该方法，以免导致合成语音缺失。 |
| ```java<br>public Flowable<SpeechSynthesisResult> callAsFlowable(String text)<br>``` | `text`：待合成文本，须为UTF-8格式 | 合成结果，封装在` Flowable<SpeechSynthesisResult>`中 | 非流式文本（不支持包含SSML的文本）输入实时转换为流式语音输出，合成结果在flowable中流式返回。<br>详细的调用流程和参考示例请参见 [通过Flowable调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#b0f81fef83ojo "")。 |
| ```java<br>boolean getDuplexApi().close(int code, String reason)<br>``` | code: WebSocket关闭码（Close Code）<br>reason：关闭原因<br>这两个参数可参考 [The WebSocket Protocol](https://datatracker.ietf.org/doc/html/rfc6455#section-7.1.5) 文档进行配置 | true | 在任务结束后，无论是否出现异常都需要关闭WebSocket连接，避免造成连接泄漏。关于如何复用连接提升效率请参考 [高并发场景](https://help.aliyun.com/zh/model-studio/high-concurrency-scenarios "")。 |
| ```java<br>public Flowable<SpeechSynthesisResult> streamingCallAsFlowable(Flowable<String> textStream)<br>``` | `textStream`：封装了待合成文本的`Flowable`实例 | 合成结果，封装在` Flowable<SpeechSynthesisResult>`中 | 流式文本（不支持包含SSML的文本）输入实时转换为流式语音输出，合成结果在flowable中流式返回。<br>详细的调用流程和参考示例请参见 [通过Flowable调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#b0f81fef83ojo "")。 |
| ```java<br>public String getLastRequestId()<br>``` | 无 | 上一个任务的Request ID | 获取上一个任务的Request ID，在调用`call`、`streamingCall`、`callAsFlowable`、`streamingCallAsFlowable`开始新任务之后可以使用。 |
| ```java<br>public long getFirstPackageDelay()<br>``` | 无 | 当前任务首包延迟 | 获取当前任务的首包延迟，任务结束后使用。首包延迟是开始发送文本和接收第一个音频包之间的时间，单位为毫秒。<br>**影响首包延迟的因素：**<br>- WebSocket连接建立耗时（首次调用）<br>  <br>- 音色加载时间（不同音色加载时间不同）<br>  <br>- 服务承载量（高峰期可能出现排队等待）<br>  <br>- 网络延迟<br>  <br>**典型延迟范围：**<br>- 复用连接且音色已加载：500ms左右<br>  <br>- 首次连接或切换音色：可能达到1500~2000ms<br>  <br>若首包延迟持续过高（>2000ms），建议：<br>1. 使用高并发场景下的连接池功能提前建立连接<br>   <br>2. 检查网络连接质量<br>   <br>3. 避免在高峰时段调用 |

### **回调接口（**`ResultCallback`）

在 [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#cc2a504f344s2 "") 或 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "") 时，通过回调接口`ResultCallback`获取合成结果。通过“`import com.alibaba.dashscope.common.ResultCallback;`”方式引入。

**点击查看示例**

```java
ResultCallback<SpeechSynthesisResult> callback = new ResultCallback<SpeechSynthesisResult>() {
    @Override
    public void onEvent(SpeechSynthesisResult result) {
        System.out.println("RequestId为：" + result.getRequestId());
        // 实时处理音频分片（如播放/写入缓冲）
    }

    @Override
    public void onComplete() {
        System.out.println("任务完成");
        // 处理合成结束逻辑（如释放播放器）
    }

    @Override
    public void onError(Exception e) {
        System.out.println("任务失败：" + e.getMessage());
        // 处理异常（网络错误/服务端错误码）
    }
};
```

| **接口/方法** | **参数** | **返回值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **接口/方法** | **参数** | **返回值** | **描述** |
| ```java<br>public void onEvent(SpeechSynthesisResult result)<br>``` | `result`：SpeechSynthesisResult实例 | 无 | 当服务端推送语音合成数据时被异步回调。<br>调用 [SpeechSynthesisResult](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#eec5791d0e7qg "") 的`getAudioFrame`方法能够获得二进制音频数据。<br>调用 [SpeechSynthesisResult](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#eec5791d0e7qg "") 的`getUsage`方法能够获得截止当前，本次请求中计费的有效字符数。 |
| ```java<br>public void onComplete()<br>``` | 无 | 无 | 当所有合成数据全部返回（语音合成完成）后被异步回调。 |
| ```java<br>public void onError(Exception e)<br>``` | `e`：异常信息 | 无 | 发生异常时该接口被异步回调。<br>建议在`onError`方法中实现完整的异常日志记录和资源清理逻辑。 |

## **响应结果**

服务器返回二进制音频数据：

- [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#82d9324616ifx "")：对 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`call`方法返回的二进制音频数据进行处理。

- [单向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#cc2a504f344s2 "") 或 [双向流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#ba023aacfbr84 "")：对 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "") 的`onEvent`方法的参数（`SpeechSynthesisResult`类型）进行处理。

`SpeechSynthesisResult`的关键接口如下：




| **接口/方法** | **参数** | **返回值** | **描述** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **接口/方法** | **参数** | **返回值** | **描述** |
| ```java<br>public ByteBuffer getAudioFrame()<br>``` | 无 | 二进制音频数据 | 返回当前流式合成片段的二进制音频数据，可能为空（当无新数据到达时）。<br>您可以将二进制音频数据合成为一个完整的音频文件后使用播放器播放，也可以通过支持流式播放的播放器实时播放。<br>**重要**<br>  - 流式语音合成中，对于mp3/opus等压缩格式，音频分段传输需使用流式播放器，不可逐帧播放，避免解码失败。<br>    <br>    <br>    > 支持流式播放的播放器：ffmpeg、pyaudio (Python)、AudioFormat (Java)、MediaSource (Javascript)等。<br>    <br>  - 将音频数据合成完整的音频文件时，应以追加模式写入同一文件。<br>    <br>  - 流式语音合成的wav/mp3 格式音频仅首帧包含头信息，后续帧为纯音频数据。 |
| ```java<br>public String getRequestId()<br>``` | 无 | 任务的Request ID | 获取任务的Request ID。当调用`getAudioFrame`获取到二进制音频数据时，`getRequestId`方法的返回值为`null`。 |
| ```java<br>public SpeechSynthesisUsage getUsage()<br>``` | 无 | `SpeechSynthesisUsage`：截止当前，本次请求中计费的有效字符数 | 返回`SpeechSynthesisUsage`或`null`。<br>通过`SpeechSynthesisUsage`的`getCharacters`方法，可获取截止当前，本次请求中计费的有效字符数，请以最后一次收到的`SpeechSynthesisUsage`为准。 |
| ```java<br>public Sentence getTimestamp()<br>``` | 无 | `Sentence`：截止当前，本次请求中计费的句子<br>> 需要开启`enableWordTimestamp`字级别时间戳 | 返回`Sentence`或`null`。<br>`Sentence`的方法：<br>  - `getIndex`：可获取句子编号，从0开始。<br>    <br>  - `getWords`：可获取组成句子的字符数组`List<Word>`，请以最后一次收到的`Sentence`为准。<br>    <br>`Word`方法：<br>  - `getText`：获取字的文本。<br>    <br>  - `getBeginIndex`：获取字在句子中的开始位置索引，从 0 开始。<br>    <br>  - `getEndIndex`：获取字在句子中的结束位置索引，从 1 开始。<br>    <br>  - `getBeginTime`：获取字对应音频的开始时间戳，单位为毫秒。<br>    <br>  - `getEndTime`：获取字对应音频的结束时间戳，单位为毫秒。 |


## **错误码**

如遇报错问题，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行排查。

## **更多示例**

更多示例，请参见 [GitHub](https://github.com/aliyun/alibabacloud-bailian-speech-demo)。

## **常见问题**

### **功能特性/计量计费/限流**

#### **Q：当遇到发音不准的情况时，有什么解决方案可以尝试？**

通过 [SSML](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language "") 可以对语音合成效果进行个性化定制。

#### **Q：** 语音合成是按文本字符数计费的，要如何查看或获取每次合成的文本长度？

- [非流式调用](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#82d9324616ifx "")：需要按照 [字符计算规则](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#37d964dceaz3i "") 自行计算。

- 其他调用方式：通过 [响应结果SpeechSynthesisResult](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#dd391b62b6prp "") 的`getUsage`方法获取。请以收到的最后一个响应结果为准。


### **故障排查**

如遇代码报错问题，请根据 [错误码](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#75df3e20f46ro "") 中的信息进行排查。

#### **Q：如何获取** Request ID **？**

通过以下两种方式可以获取：

- 在 [回调接口（ResultCallback）](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#3639e1cb40mxi "") 的`onEvent`方法中调用 [SpeechSynthesisResult](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#eec5791d0e7qg "") 的`getRequestId`方法。

`getRequestId`方法返回值可能为null，详情请参见 [SpeechSynthesisResult](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#eec5791d0e7qg "") 中关于`getRequestId`方法的描述。

- 调用 [SpeechSynthesizer](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`getLastRequestId`方法。


#### **Q：使用SSML功能失败是什么原因？**

请按以下步骤排查：

1. 确保 [限制与约束](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#923300b3e9a3z "") 正确

2. [安装最新版本 DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")

3. 确保使用正确的接口：只有 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`call`方法支持SSML

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

请检查是否遗漏了调用 [SpeechSynthesizer类](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#adcb5e9bddbyq "") 的`streamingComplete`方法。在语音合成过程中，服务端会在缓存足够文本后才开始合成。如果未调用`streamingComplete`方法，可能会导致缓存中的结尾部分文本未能被合成为语音。

### **权限与认证**

#### **Q：** 我希望我的 API Key 仅用于 CosyVoice 语音合成服务，而不被百炼其他模型使用（权限隔离），我该如何做 **？**

可以通过新建业务空间并只授权特定模型来限制API Key的使用范围。详情请参见 [业务空间管理](https://help.aliyun.com/zh/model-studio/use-workspace "")。

#### **Q：使用子业务空间的API Key是否可以调用CosyVoice模型？**

对于默认业务空间，模型均可调用。

对于子业务空间：需要为API Key对应的子业务空间进行 [模型授权](https://help.aliyun.com/zh/model-studio/model-authentication-instructions "")，详情请参见 [子业务空间的模型调用](https://help.aliyun.com/zh/model-studio/model-calling-in-sub-workspace "")。

### **更多问题**

请参见GitHub [QA](https://github.com/aliyun/alibabacloud-bailian-speech-demo/blob/master/docs/QA/cosyvoice.md)。