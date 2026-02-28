### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音合成](https://help.aliyun.com/zh/model-studio/speech-synthesis-api-reference/)[实时语音合成（CosyVoice）](https://help.aliyun.com/zh/model-studio/cosyvoice-large-model-for-speech-synthesis/)SSML标记语言介绍

# SSML标记语言介绍

更新时间：2026-02-11 02:25:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：LaTeX 公式转语音](https://help.aliyun.com/zh/model-studio/latex-capability-support-description)[下一篇：音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

限制与约束

快速开始

标签

<speak>：根节点

<break>：控制停顿时间

<sub>：替换文本

<phoneme>：指定发音（拼音/音标）

<soundEvent>：插入一段外部声音（铃声、猫叫等）

<say-as>：设置文本的读法（数字、日期、电话号码等）

SSML（Speech Synthesis Markup Language） 是一种基于 XML 的语音合成标记语言。它不仅能让语音合成大模型读出更丰富的文本内容，还支持对语速、语调、停顿、音量等语音特征进行精细控制，甚至可以添加背景音乐，带来更具表现力的语音效果。本文介绍CosyVoice的SSML功能及使用。

## **限制与约束**

- **模型：** 仅cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型支持SSML功能

- **音色：** 仅复刻音色，以及 [音色列表](https://help.aliyun.com/zh/model-studio/cosyvoice-voice-list "") 中标记为支持SSML的系统音色支持SSML功能

- **接口：** 仅部分接口支持SSML功能

  - Java SDK（不低于2.20.3版本）：仅非流式调用和单向流式调用支持SSML（详情请参见： [SSML标记语言支持说明-Java SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#99f13f3817ptm "")）

  - Python SDK（不低于1.23.4版本）：仅非流式调用和单向流式调用支持SSML（详情请参见： [SSML标记语言支持说明-Python SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk#99f13f3817ptm "")）

  - WebSocket API：在发送 [run-task指令](https://help.aliyun.com/zh/model-studio/cosyvoice-websocket-api#12d8a57443dmz "") 时，必须将参数`enable_ssml`设置为`true`，且只允许发送一次 [continue-task指令](https://help.aliyun.com/zh/model-studio/cosyvoice-websocket-api#974b0beb59ob5 "")（详情请参见： [SSML标记语言支持说明-WebSocket API](https://help.aliyun.com/zh/model-studio/cosyvoice-websocket-api#99f13f3817ptm "")）。

## **快速开始**

运行代码前，请完成以下准备工作：

1. [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")

2. [安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")（如需运行Java/Python SDK示例）


Java SDK

Python SDK

WebSocket API

非流式调用

单向流式调用

```java
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.utils.Constants;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;

/**
 * SSML功能说明：
 *     1. 只有非流式调用和单向流式调用支持SSML功能
 *     2. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）
 */
public class Main {
    private static String model = "cosyvoice-v3-flash";
    private static String voice = "longanyang";

    public static void main(String[] args) {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        streamAudioDataToSpeaker();
        System.exit(0);
    }

    public static void streamAudioDataToSpeaker() {
        SpeechSynthesisParam param =
                SpeechSynthesisParam.builder()
                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                        .model(model)
                        .voice(voice)
                        .build();

        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, null);
        ByteBuffer audio = null;
        try {
            // 非流式调用，阻塞直至音频返回
            // 特殊字符需要进行转义
            audio = synthesizer.call("<speak rate=\"2\">我的语速比正常人快。</speak>");
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            // 任务结束关闭websocket连接
            synthesizer.getDuplexApi().close(1000, "bye");
        }
        if (audio != null) {
            // 将音频数据保存到本地文件“output.mp3”中
            File file = new File("output.mp3");
            try (FileOutputStream fos = new FileOutputStream(file)) {
                fos.write(audio.array());
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }

        // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        System.out.println(
                "[Metric] requestId为："
                        + synthesizer.getLastRequestId()
                        + "首包延迟（毫秒）为："
                        + synthesizer.getFirstPackageDelay());
    }
}
```

```java
import com.alibaba.dashscope.audio.tts.SpeechSynthesisResult;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisAudioFormat;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesisParam;
import com.alibaba.dashscope.audio.ttsv2.SpeechSynthesizer;
import com.alibaba.dashscope.common.ResultCallback;
import com.alibaba.dashscope.utils.Constants;

import java.io.FileOutputStream;
import java.io.IOException;
import java.util.concurrent.CountDownLatch;

/**
 * SSML功能说明：
 *     1. 只有非流式调用和单向流式调用支持SSML功能
 *     2. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）
 */
public class Main {
    private static String model = "cosyvoice-v3-flash";
    private static String voice = "longanyang";

    public static void main(String[] args) {
        // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference
        Constants.baseWebsocketApiUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference";
        streamAudioDataToSpeaker();
        System.out.println("音频已保存到 output.mp3 文件中");
        System.exit(0);
    }

    public static void streamAudioDataToSpeaker() {
        CountDownLatch latch = new CountDownLatch(1);
        final FileOutputStream[] fileOutputStream = new FileOutputStream[1];

        try {
            fileOutputStream[0] = new FileOutputStream("output.mp3");
        } catch (IOException e) {
            System.err.println("无法创建输出文件: " + e.getMessage());
            return;
        }

        // 实现回调接口ResultCallback
        ResultCallback<SpeechSynthesisResult> callback = new ResultCallback<SpeechSynthesisResult>() {
            @Override
            public void onEvent(SpeechSynthesisResult result) {
                if (result.getAudioFrame() != null) {
                    // 将音频数据写入本地文件
                    try {
                        byte[] audioData = result.getAudioFrame().array();
                        fileOutputStream[0].write(audioData);
                        fileOutputStream[0].flush();
                    } catch (IOException e) {
                        System.err.println("写入音频数据失败: " + e.getMessage());
                    }
                }
            }

            @Override
            public void onComplete() {
                System.out.println("收到Complete，语音合成结束");
                closeFileOutputStream(fileOutputStream[0]);
                latch.countDown();
            }

            @Override
            public void onError(Exception e) {
                System.out.println("出现异常：" + e.toString());
                closeFileOutputStream(fileOutputStream[0]);
                latch.countDown();
            }
        };

        SpeechSynthesisParam param =
                SpeechSynthesisParam.builder()
                        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                        // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                        .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                        .model(model)
                        .voice(voice)
                        .format(SpeechSynthesisAudioFormat.MP3_22050HZ_MONO_256KBPS)
                        .build();

        SpeechSynthesizer synthesizer = new SpeechSynthesizer(param, callback);

        try {
            // 单向流式调用，立即返回null（实际结果通过回调接口异步传递），在回调接口的onEvent方法中实时获取二进制音频
            // 特殊字符需要进行转义
            synthesizer.call("<speak rate=\"2\">我的语速比正常人快。</speak>");
            // 等待合成完成
            latch.await();
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            // 任务结束后关闭websocket连接
            try {
                synthesizer.getDuplexApi().close(1000, "bye");
            } catch (Exception e) {
                System.err.println("关闭WebSocket连接失败: " + e.getMessage());
            }

            // 确保文件流被关闭
            closeFileOutputStream(fileOutputStream[0]);
        }

        // 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        System.out.println(
                "[Metric] requestId为："
                        + synthesizer.getLastRequestId()
                        + "，首包延迟（毫秒）为："
                        + synthesizer.getFirstPackageDelay());
    }

    private static void closeFileOutputStream(FileOutputStream fileOutputStream) {
        try {
            if (fileOutputStream != null) {
                fileOutputStream.close();
            }
        } catch (IOException e) {
            System.err.println("关闭文件流失败: " + e.getMessage());
        }
    }
}
```

非流式调用

单向流式调用

```python
# coding=utf-8
# SSML功能说明：
#     1. 只有非流式调用和单向流式调用支持SSML功能
#     2. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）

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
# 非流式调用，阻塞直至音频返回
# 特殊字符需要进行转义
audio = synthesizer.call("<speak rate=\"2\">我的语速比正常人快。</speak>")

# 将音频保存至本地
with open('output.mp3', 'wb') as f:
    f.write(audio)

# 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
print('[Metric] requestId为：{}，首包延迟为：{}毫秒'.format(
    synthesizer.get_last_request_id(),
    synthesizer.get_first_package_delay()))
```

```python
# coding=utf-8
# SSML功能说明：
#     1. 只有非流式调用和单向流式调用支持SSML功能
#     2. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）

import dashscope
from dashscope.audio.tts_v2 import *
import os
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
        # 打开输出文件，准备写入音频数据
        self.file = open("output.mp3", "wb")
        print("连接建立：" + get_timestamp())

    def on_complete(self):
        print("语音合成完成，所有合成结果已被接收：" + get_timestamp())
        if hasattr(self, 'file') and self.file:
            self.file.close()
        self
        # 首次发送文本时需建立 WebSocket 连接，因此首包延迟会包含连接建立的耗时
        print('[Metric] requestId为：{}，首包延迟为：{}毫秒'.format(
            self.synthesizer.get_last_request_id(),
            self.synthesizer.get_first_package_delay()))

    def on_error(self, message: str):
        print(f"语音合成出现异常：{message}")
        if hasattr(self, 'file') and self.file:
            self.file.close()

    def on_close(self):
        print("连接关闭：" + get_timestamp())
        if hasattr(self, 'file') and self.file:
            self.file.close()

    def on_event(self, message):
        pass

    def on_data(self, data: bytes) -> None:
        print(get_timestamp() + " 二进制音频长度为：" + str(len(data)))
        # 将音频数据写入文件
        self.file.write(data)

callback = Callback()

# 实例化SpeechSynthesizer，并在构造方法中传入模型（model）、音色（voice）等请求参数
synthesizer = SpeechSynthesizer(
    model=model,
    voice=voice,
    callback=callback,
)

# 将synthesizer实例赋值给callback，以便在on_complete中使用
callback.synthesizer = synthesizer

# 单向流式调用，发送待合成文本，在回调接口的on_data方法中实时获取二进制音频
# 特殊字符需要进行转义
synthesizer.call("<speak rate=\"2\">我的语速比正常人快。</speak>")
```

Go

C#

PHP

Node.js

Java

Python

```go
// SSML功能说明：
//     1. 在发送run-task指令时，将参数enable_ssml设置为true，以开启SSML支持
//     2. 通过continue-task指令发送包含SSML的文本，且只允许发送一次continue-task指令
//     3. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）

package main

import (
    "encoding/json"
    "fmt"
    "net/http"
    "os"
    "strings"
    "time"

    "github.com/google/uuid"
    "github.com/gorilla/websocket"
)

const (
    // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference/
    wsURL      = "wss://dashscope.aliyuncs.com/api-ws/v1/inference/"
    outputFile = "output.mp3"
)

func main() {
    // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    // 若没有配置环境变量，请用百炼API Key将下行替换为：apiKey := "sk-xxx"
    apiKey := os.Getenv("DASHSCOPE_API_KEY")

    // 清空输出文件
    os.Remove(outputFile)
    os.Create(outputFile)

    // 连接WebSocket
    header := make(http.Header)
    header.Add("X-DashScope-DataInspection", "enable")
    header.Add("Authorization", fmt.Sprintf("bearer %s", apiKey))

    conn, resp, err := websocket.DefaultDialer.Dial(wsURL, header)
    if err != nil {
        if resp != nil {
            fmt.Printf("连接失败 HTTP状态码: %d\n", resp.StatusCode)
        }
        fmt.Println("连接失败:", err)
        return
    }
    defer conn.Close()

    // 生成任务ID
    taskID := uuid.New().String()
    fmt.Printf("生成任务ID: %s\n", taskID)

    // 发送run-task指令
    runTaskCmd := map[string]interface{}{
        "header": map[string]interface{}{
            "action":    "run-task",
            "task_id":   taskID,
            "streaming": "duplex",
        },
        "payload": map[string]interface{}{
            "task_group": "audio",
            "task":       "tts",
            "function":   "SpeechSynthesizer",
            "model":      "cosyvoice-v3-flash",
            "parameters": map[string]interface{}{
                "text_type":   "PlainText",
                "voice":       "longanyang",
                "format":      "mp3",
                "sample_rate": 22050,
                "volume":      50,
                "rate":        1,
                "pitch":       1,
                // 如果enable_ssml设为true，只允许发送一次continue-task指令，否则会报错“Text request limit violated, expected 1.”
                "enable_ssml": true,
            },
            "input": map[string]interface{}{},
        },
    }

    runTaskJSON, _ := json.Marshal(runTaskCmd)
    fmt.Printf("发送run-task指令: %s\n", string(runTaskJSON))

    err = conn.WriteMessage(websocket.TextMessage, runTaskJSON)
    if err != nil {
        fmt.Println("发送run-task失败:", err)
        return
    }

    textSent := false

    // 处理消息
    for {
        messageType, message, err := conn.ReadMessage()
        if err != nil {
            fmt.Println("读取消息失败:", err)
            break
        }

        // 处理二进制消息
        if messageType == websocket.BinaryMessage {
            fmt.Printf("收到二进制消息，长度: %d\n", len(message))
            file, _ := os.OpenFile(outputFile, os.O_APPEND|os.O_WRONLY|os.O_CREATE, 0644)
            file.Write(message)
            file.Close()
            continue
        }

        // 处理文本消息
        messageStr := string(message)
        fmt.Printf("收到文本消息: %s\n", strings.ReplaceAll(messageStr, "\n", ""))

        // 简单解析JSON获取event类型
        var msgMap map[string]interface{}
        if json.Unmarshal(message, &msgMap) == nil {
            if header, ok := msgMap["header"].(map[string]interface{}); ok {
                if event, ok := header["event"].(string); ok {
                    fmt.Printf("事件类型: %s\n", event)

                    switch event {
                    case "task-started":
                        fmt.Println("=== 收到task-started事件 ===")

                        if !textSent {
                            // 发送 continue-task 指令，使用SSML功能时，该指令只允许发送一次
                            continueTaskCmd := map[string]interface{}{
                                "header": map[string]interface{}{
                                    "action":    "continue-task",
                                    "task_id":   taskID,
                                    "streaming": "duplex",
                                },
                                "payload": map[string]interface{}{
                                    "input": map[string]interface{}{
                                        // 特殊字符需要进行转义
                                        "text": "<speak rate=\"2\">我的语速比正常人快。</speak>",
                                    },
                                },
                            }

                            continueTaskJSON, _ := json.Marshal(continueTaskCmd)
                            fmt.Printf("发送continue-task指令: %s\n", string(continueTaskJSON))

                            err = conn.WriteMessage(websocket.TextMessage, continueTaskJSON)
                            if err != nil {
                                fmt.Println("发送continue-task失败:", err)
                                return
                            }

                            textSent = true

                            // 延迟发送finish-task
                            time.Sleep(500 * time.Millisecond)

                            // 发送finish-task指令
                            finishTaskCmd := map[string]interface{}{
                                "header": map[string]interface{}{
                                    "action":    "finish-task",
                                    "task_id":   taskID,
                                    "streaming": "duplex",
                                },
                                "payload": map[string]interface{}{
                                    "input": map[string]interface{}{},
                                },
                            }

                            finishTaskJSON, _ := json.Marshal(finishTaskCmd)
                            fmt.Printf("发送finish-task指令: %s\n", string(finishTaskJSON))

                            err = conn.WriteMessage(websocket.TextMessage, finishTaskJSON)
                            if err != nil {
                                fmt.Println("发送finish-task失败:", err)
                                return
                            }
                        }

                    case "task-finished":
                        fmt.Println("=== 任务完成 ===")
                        return

                    case "task-failed":
                        fmt.Println("=== 任务失败 ===")
                        if header["error_message"] != nil {
                            fmt.Printf("错误信息: %s\n", header["error_message"])
                        }
                        return

                    case "result-generated":
                        fmt.Println("收到result-generated事件")
                    }
                }
            }
        }
    }
}
```

```csharp
using System.Net.WebSockets;
using System.Text;
using System.Text.Json;

// SSML功能说明：
//     1. 在发送run-task指令时，将参数enable_ssml设置为true，以开启SSML支持
//     2. 通过continue-task指令发送包含SSML的文本，且只允许发送一次continue-task指令
//     3. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）
class Program {
    // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    // 若没有配置环境变量，请用百炼API Key将下行替换为：private static readonly string ApiKey = "sk-xxx"
    private static readonly string ApiKey = Environment.GetEnvironmentVariable("DASHSCOPE_API_KEY") ?? throw new InvalidOperationException("DASHSCOPE_API_KEY environment variable is not set.");

    // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference/
    private const string WebSocketUrl = "wss://dashscope.aliyuncs.com/api-ws/v1/inference/";
    // 输出文件路径
    private const string OutputFilePath = "output.mp3";

    // WebSocket客户端
    private static ClientWebSocket _webSocket = new ClientWebSocket();
    // 取消令牌源
    private static CancellationTokenSource _cancellationTokenSource = new CancellationTokenSource();
    // 任务ID
    private static string? _taskId;
    // 任务是否已启动
    private static TaskCompletionSource<bool> _taskStartedTcs = new TaskCompletionSource<bool>();

    static async Task Main(string[] args) {
        try {
            // 清空输出文件
            ClearOutputFile(OutputFilePath);

            // 连接WebSocket服务
            await ConnectToWebSocketAsync(WebSocketUrl);

            // 启动接收消息的任务
            Task receiveTask = ReceiveMessagesAsync();

            // 发送run-task指令
            _taskId = GenerateTaskId();
            await SendRunTaskCommandAsync(_taskId);

            // 等待task-started事件
            await _taskStartedTcs.Task;

            // 发送 continue-task 指令，使用SSML功能时，该指令只允许发送一次
            // 特殊字符需要进行转义
            await SendContinueTaskCommandAsync("<speak rate=\"2\">我的语速比正常人快。</speak>");

            // 发送finish-task指令
            await SendFinishTaskCommandAsync(_taskId);

            // 等待接收任务完成
            await receiveTask;

            Console.WriteLine("任务完成，连接已关闭。");
        } catch (OperationCanceledException) {
            Console.WriteLine("任务被取消。");
        } catch (Exception ex) {
            Console.WriteLine($"发生错误：{ex.Message}");
        } finally {
            _cancellationTokenSource.Cancel();
            _webSocket.Dispose();
        }
    }

    private static void ClearOutputFile(string filePath) {
        if (File.Exists(filePath)) {
            File.WriteAllText(filePath, string.Empty);
            Console.WriteLine("输出文件已清空。");
        } else {
            Console.WriteLine("输出文件不存在，无需清空。");
        }
    }

    private static async Task ConnectToWebSocketAsync(string url) {
        var uri = new Uri(url);
        if (_webSocket.State == WebSocketState.Connecting || _webSocket.State == WebSocketState.Open) {
            return;
        }

        // 设置WebSocket连接的头部信息
        _webSocket.Options.SetRequestHeader("Authorization", $"bearer {ApiKey}");
        _webSocket.Options.SetRequestHeader("X-DashScope-DataInspection", "enable");

        try {
            await _webSocket.ConnectAsync(uri, _cancellationTokenSource.Token);
            Console.WriteLine("已成功连接到WebSocket服务。");
        } catch (OperationCanceledException) {
            Console.WriteLine("WebSocket连接被取消。");
        } catch (Exception ex) {
            Console.WriteLine($"WebSocket连接失败: {ex.Message}");
            throw;
        }
    }

    private static async Task SendRunTaskCommandAsync(string taskId) {
        var command = CreateCommand("run-task", taskId, "duplex", new {
            task_group = "audio",
            task = "tts",
            function = "SpeechSynthesizer",
            model = "cosyvoice-v3-flash",
            parameters = new
            {
                text_type = "PlainText",
                voice = "longanyang",
                format = "mp3",
                sample_rate = 22050,
                volume = 50,
                rate = 1,
                pitch = 1,
                // 如果enable_ssml设为true，只允许发送一次continue-task指令，否则会报错“Text request limit violated, expected 1.”
                enable_ssml = true
            },
            input = new { }
        });

        await SendJsonMessageAsync(command);
        Console.WriteLine("已发送run-task指令。");
    }

    private static async Task SendContinueTaskCommandAsync(string text) {
        if (_taskId == null) {
            throw new InvalidOperationException("任务ID未初始化。");
        }

        var command = CreateCommand("continue-task", _taskId, "duplex", new {
            input = new {
                text
            }
        });

        await SendJsonMessageAsync(command);
        Console.WriteLine("已发送continue-task指令。");
    }

    private static async Task SendFinishTaskCommandAsync(string taskId) {
        var command = CreateCommand("finish-task", taskId, "duplex", new {
            input = new { }
        });

        await SendJsonMessageAsync(command);
        Console.WriteLine("已发送finish-task指令。");
    }

    private static async Task SendJsonMessageAsync(string message) {
        var buffer = Encoding.UTF8.GetBytes(message);
        try {
            await _webSocket.SendAsync(new ArraySegment<byte>(buffer), WebSocketMessageType.Text, true, _cancellationTokenSource.Token);
        } catch (OperationCanceledException) {
            Console.WriteLine("消息发送被取消。");
        }
    }

    private static async Task ReceiveMessagesAsync() {
        while (_webSocket.State == WebSocketState.Open) {
            var response = await ReceiveMessageAsync();
            if (response != null) {
                var eventStr = response.RootElement.GetProperty("header").GetProperty("event").GetString();
                switch (eventStr) {
                    case "task-started":
                        Console.WriteLine("任务已启动。");
                        _taskStartedTcs.TrySetResult(true);
                        break;
                    case "task-finished":
                        Console.WriteLine("任务已完成。");
                        _cancellationTokenSource.Cancel();
                        break;
                    case "task-failed":
                        Console.WriteLine("任务失败：" + response.RootElement.GetProperty("header").GetProperty("error_message").GetString());
                        _cancellationTokenSource.Cancel();
                        break;
                    default:
                        // result-generated可在此处理
                        break;
                }
            }
        }
    }

    private static async Task<JsonDocument?> ReceiveMessageAsync() {
        var buffer = new byte[1024 * 4];
        var segment = new ArraySegment<byte>(buffer);

        try {
            WebSocketReceiveResult result = await _webSocket.ReceiveAsync(segment, _cancellationTokenSource.Token);

            if (result.MessageType == WebSocketMessageType.Close) {
                await _webSocket.CloseAsync(WebSocketCloseStatus.NormalClosure, "Closing", _cancellationTokenSource.Token);
                return null;
            }

            if (result.MessageType == WebSocketMessageType.Binary) {
                // 处理二进制数据
                Console.WriteLine("接收到二进制数据...");

                // 将二进制数据保存到文件
                using (var fileStream = new FileStream(OutputFilePath, FileMode.Append)) {
                    fileStream.Write(buffer, 0, result.Count);
                }

                return null;
            }

            string message = Encoding.UTF8.GetString(buffer, 0, result.Count);
            return JsonDocument.Parse(message);
        } catch (OperationCanceledException) {
            Console.WriteLine("消息接收被取消。");
            return null;
        }
    }

    private static string GenerateTaskId() {
        return Guid.NewGuid().ToString("N").Substring(0, 32);
    }

    private static string CreateCommand(string action, string taskId, string streaming, object payload) {
        var command = new {
            header = new {
                action,
                task_id = taskId,
                streaming
            },
            payload
        };

        return JsonSerializer.Serialize(command);
    }
}
```

示例代码目录结构为：

my-php-project/

├── composer.json

├── vendor/

└── index.php

composer.json内容如下，相关依赖的版本号请根据实际情况自行决定：

```json
{
    "require": {
        "react/event-loop": "^1.3",
        "react/socket": "^1.11",
        "react/stream": "^1.2",
        "react/http": "^1.1",
        "ratchet/pawl": "^0.4"
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

index.php内容如下：

```php
<!-- SSML功能说明： -->
<!--     1. 在发送run-task指令时，将参数enable_ssml设置为true，以开启SSML支持 -->
<!--     2. 通过continue-task指令发送包含SSML的文本，且只允许发送一次continue-task指令 -->
<!--     3. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色） -->

<?php

require __DIR__ . '/vendor/autoload.php';

use Ratchet\Client\Connector;
use React\EventLoop\Loop;
use React\Socket\Connector as SocketConnector;

// 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
// 若没有配置环境变量，请用百炼API Key将下行替换为：$api_key = "sk-xxx"
$api_key = getenv("DASHSCOPE_API_KEY");
// 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference/
$websocket_url = 'wss://dashscope.aliyuncs.com/api-ws/v1/inference/'; // WebSocket服务器地址
$output_file = 'output.mp3'; // 输出文件路径

$loop = Loop::get();

if (file_exists($output_file)) {
    // 清空文件内容
    file_put_contents($output_file, '');
}

// 创建自定义的连接器
$socketConnector = new SocketConnector($loop, [\
    'tcp' => [\
        'bindto' => '0.0.0.0:0',\
    ],\
    'tls' => [\
        'verify_peer' => false,\
        'verify_peer_name' => false,\
    ],\
]);

$connector = new Connector($loop, $socketConnector);

$headers = [\
    'Authorization' => 'bearer ' . $api_key,\
    'X-DashScope-DataInspection' => 'enable'\
];

$connector($websocket_url, [], $headers)->then(function ($conn) use ($loop, $output_file) {
    echo "连接到WebSocket服务器\n";

    // 生成任务ID
    $taskId = generateTaskId();

    // 发送 run-task 指令
    sendRunTaskMessage($conn, $taskId);

    // 定义发送 continue-task 指令的函数
    $sendContinueTask = function() use ($conn, $loop, $taskId) {
        // 发送 continue-task 指令，使用SSML功能时，该指令只允许发送一次
        $continueTaskMessage = json_encode([\
            "header" => [\
                "action" => "continue-task",\
                "task_id" => $taskId,\
                "streaming" => "duplex"\
            ],\
            "payload" => [\
                "input" => [\
                    // 特殊字符需要进行转义\
                    "text" => "<speak rate=\"2\">我的语速比正常人快。</speak>"\
                ]\
            ]\
        ]);
        $conn->send($continueTaskMessage);

        // 发送 finish-task 指令
        sendFinishTaskMessage($conn, $taskId);
    };

    // 标记是否收到 task-started 事件
    $taskStarted = false;

    // 监听消息
    $conn->on('message', function($msg) use ($conn, $sendContinueTask, $loop, &$taskStarted, $taskId, $output_file) {
        if ($msg->isBinary()) {
            // 写入二进制数据到本地文件
            file_put_contents($output_file, $msg->getPayload(), FILE_APPEND);
        } else {
            // 处理非二进制消息
            $response = json_decode($msg, true);

            if (isset($response['header']['event'])) {
                handleEvent($conn, $response, $sendContinueTask, $loop, $taskId, $taskStarted);
            } else {
                echo "未知的消息格式\n";
            }
        }
    });

    // 监听连接关闭
    $conn->on('close', function($code = null, $reason = null) {
        echo "连接已关闭\n";
        if ($code !== null) {
            echo "关闭代码: " . $code . "\n";
        }
        if ($reason !== null) {
            echo "关闭原因：" . $reason . "\n";
        }
    });
}, function ($e) {
    echo "无法连接：{$e->getMessage()}\n";
});

$loop->run();

/**
 * 生成任务ID
 * @return string
 */
function generateTaskId(): string {
    return bin2hex(random_bytes(16));
}

/**
 * 发送 run-task 指令
 * @param $conn
 * @param $taskId
 */
function sendRunTaskMessage($conn, $taskId) {
    $runTaskMessage = json_encode([\
        "header" => [\
            "action" => "run-task",\
            "task_id" => $taskId,\
            "streaming" => "duplex"\
        ],\
        "payload" => [\
            "task_group" => "audio",\
            "task" => "tts",\
            "function" => "SpeechSynthesizer",\
            "model" => "cosyvoice-v3-flash",\
            "parameters" => [\
                "text_type" => "PlainText",\
                "voice" => "longanyang",\
                "format" => "mp3",\
                "sample_rate" => 22050,\
                "volume" => 50,\
                "rate" => 1,\
                "pitch" => 1,\
                // 如果enable_ssml设为true，只允许发送一次continue-task指令，否则会报错“Text request limit violated, expected 1.”\
                "enable_ssml" => true\
            ],\
            "input" => (object) []\
        ]\
    ]);
    echo "准备发送run-task指令: " . $runTaskMessage . "\n";
    $conn->send($runTaskMessage);
    echo "run-task指令已发送\n";
}

/**
 * 读取音频文件
 * @param string $filePath
 * @return bool|string
 */
function readAudioFile(string $filePath) {
    $voiceData = file_get_contents($filePath);
    if ($voiceData === false) {
        echo "无法读取音频文件\n";
    }
    return $voiceData;
}

/**
 * 分割音频数据
 * @param string $data
 * @param int $chunkSize
 * @return array
 */
function splitAudioData(string $data, int $chunkSize): array {
    return str_split($data, $chunkSize);
}

/**
 * 发送 finish-task 指令
 * @param $conn
 * @param $taskId
 */
function sendFinishTaskMessage($conn, $taskId) {
    $finishTaskMessage = json_encode([\
        "header" => [\
            "action" => "finish-task",\
            "task_id" => $taskId,\
            "streaming" => "duplex"\
        ],\
        "payload" => [\
            "input" => (object) []\
        ]\
    ]);
    echo "准备发送finish-task指令: " . $finishTaskMessage . "\n";
    $conn->send($finishTaskMessage);
    echo "finish-task指令已发送\n";
}

/**
 * 处理事件
 * @param $conn
 * @param $response
 * @param $sendContinueTask
 * @param $loop
 * @param $taskId
 * @param $taskStarted
 */
function handleEvent($conn, $response, $sendContinueTask, $loop, $taskId, &$taskStarted) {
    switch ($response['header']['event']) {
        case 'task-started':
            echo "任务开始，发送continue-task指令...\n";
            $taskStarted = true;
            // 发送 continue-task 指令
            $sendContinueTask();
            break;
        case 'result-generated':
            // 忽略result-generated事件
            break;
        case 'task-finished':
            echo "任务完成\n";
            $conn->close();
            break;
        case 'task-failed':
            echo "任务失败\n";
            echo "错误代码：" . $response['header']['error_code'] . "\n";
            echo "错误信息：" . $response['header']['error_message'] . "\n";
            $conn->close();
            break;
        case 'error':
            echo "错误：" . $response['payload']['message'] . "\n";
            break;
        default:
            echo "未知事件：" . $response['header']['event'] . "\n";
            break;
    }

    // 如果任务已完成，关闭连接
    if ($response['header']['event'] == 'task-finished') {
        // 等待1秒以确保所有数据都已传输完毕
        $loop->addTimer(1, function() use ($conn) {
            $conn->close();
            echo "客户端关闭连接\n";
        });
    }

    // 如果没有收到 task-started 事件，关闭连接
    if (!$taskStarted && in_array($response['header']['event'], ['task-failed', 'error'])) {
        $conn->close();
    }
}
```

需安装相关依赖：

```bash
npm install ws
npm install uuid
```

示例代码如下：

```nodejs
// SSML功能说明：
//     1. 在发送run-task指令时，将参数enable_ssml设置为true，以开启SSML支持
//     2. 通过continue-task指令发送包含SSML的文本，且只允许发送一次continue-task指令
//     3. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）

import fs from 'fs';
import WebSocket from 'ws';
import { v4 as uuid } from 'uuid'; // 用于生成UUID

// 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
// 若没有配置环境变量，请用百炼API Key将下行替换为：const apiKey = "sk-xxx"
const apiKey = process.env.DASHSCOPE_API_KEY;
// 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference/
const url = 'wss://dashscope.aliyuncs.com/api-ws/v1/inference/';
// 输出文件路径
const outputFilePath = 'output.mp3';

// 清空输出文件
fs.writeFileSync(outputFilePath, '');

// 创建WebSocket客户端
const ws = new WebSocket(url, {
  headers: {
    Authorization: `bearer ${apiKey}`,
    'X-DashScope-DataInspection': 'enable'
  }
});

let taskStarted = false;
let taskId = uuid();

ws.on('open', () => {
  console.log('已连接到WebSocket服务器');

  // 发送run-task指令
  const runTaskMessage = JSON.stringify({
    header: {
      action: 'run-task',
      task_id: taskId,
      streaming: 'duplex'
    },
    payload: {
      task_group: 'audio',
      task: 'tts',
      function: 'SpeechSynthesizer',
      model: 'cosyvoice-v3-flash',
      parameters: {
        text_type: 'PlainText',
        voice: 'longanyang', // 音色
        format: 'mp3', // 音频格式
        sample_rate: 22050, // 采样率
        volume: 50, // 音量
        rate: 1, // 语速
        pitch: 1, // 音调
        enable_ssml: true // 是否开启SSML功能。如果enable_ssml设为true，只允许发送一次continue-task指令，否则会报错“Text request limit violated, expected 1.”
      },
      input: {}
    }
  });
  ws.send(runTaskMessage);
  console.log('已发送run-task消息');
});

const fileStream = fs.createWriteStream(outputFilePath, { flags: 'a' });
ws.on('message', (data, isBinary) => {
  if (isBinary) {
    // 写入二进制数据到文件
    fileStream.write(data);
  } else {
    const message = JSON.parse(data);

    switch (message.header.event) {
      case 'task-started':
        taskStarted = true;
        console.log('任务已开始');
        // 发送continue-task指令
        sendContinueTasks(ws);
        break;
      case 'task-finished':
        console.log('任务已完成');
        ws.close();
        fileStream.end(() => {
          console.log('文件流已关闭');
        });
        break;
      case 'task-failed':
        console.error('任务失败：', message.header.error_message);
        ws.close();
        fileStream.end(() => {
          console.log('文件流已关闭');
        });
        break;
      default:
        // 可以在这里处理result-generated
        break;
    }
  }
});

function sendContinueTasks(ws) {

  if (taskStarted) {
    // 发送 continue-task 指令，使用SSML功能时，该指令只允许发送一次
    const continueTaskMessage = JSON.stringify({
      header: {
        action: 'continue-task',
        task_id: taskId,
        streaming: 'duplex'
      },
      payload: {
        input: {
          // 特殊字符需要进行转义
          text: '<speak rate="2">我的语速比正常人快。</speak>'
        }
      }
    });
    ws.send(continueTaskMessage);

    // 发送finish-task指令
    const finishTaskMessage = JSON.stringify({
      header: {
        action: 'finish-task',
        task_id: taskId,
        streaming: 'duplex'
      },
      payload: {
        input: {}
      }
    });
    ws.send(finishTaskMessage);
  }
}

ws.on('close', () => {
  console.log('已断开与WebSocket服务器的连接');
});
```

如您使用Java编程语言，建议采用Java DashScope SDK进行开发，详情请参见 [Java SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk "")。

以下是Java WebSocket的调用示例。在运行示例前，请确保已导入以下依赖：

- `Java-WebSocket`

- `jackson-databind`


推荐您使用Maven或Gradle管理依赖包，其配置如下：

pom.xml

build.gradle

```xml
<dependencies>
    <!-- WebSocket Client -->
    <dependency>
        <groupId>org.java-websocket</groupId>
        <artifactId>Java-WebSocket</artifactId>
        <version>1.5.3</version>
    </dependency>

    <!-- JSON Processing -->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.13.0</version>
    </dependency>
</dependencies>
```

```gradle
// 省略其它代码
dependencies {
  // WebSocket Client
  implementation 'org.java-websocket:Java-WebSocket:1.5.3'
  // JSON Processing
  implementation 'com.fasterxml.jackson.core:jackson-databind:2.13.0'
}
// 省略其它代码
```

Java代码如下：

```java
import com.fasterxml.jackson.databind.ObjectMapper;

import org.java_websocket.client.WebSocketClient;
import org.java_websocket.handshake.ServerHandshake;

import java.io.FileOutputStream;
import java.io.IOException;
import java.net.URI;
import java.nio.ByteBuffer;
import java.util.*;

/**
 * SSML功能说明：
 *     1. 在发送run-task指令时，将参数enable_ssml设置为true，以开启SSML支持
 *     2. 通过continue-task指令发送包含SSML的文本，且只允许发送一次continue-task指令
 *     3. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）
 */
public class TTSWebSocketClient extends WebSocketClient {
    private final String taskId = UUID.randomUUID().toString();
    private final String outputFile = "output_" + System.currentTimeMillis() + ".mp3";
    private boolean taskFinished = false;

    public TTSWebSocketClient(URI serverUri, Map<String, String> headers) {
        super(serverUri, headers);
    }

    @Override
    public void onOpen(ServerHandshake serverHandshake) {
        System.out.println("连接成功");

        // 发送run-task指令
        // 如果enable_ssml设为true，只允许发送一次continue-task指令，否则会报错“Text request limit violated, expected 1.”
        String runTaskCommand = "{ \"header\": { \"action\": \"run-task\", \"task_id\": \"" + taskId + "\", \"streaming\": \"duplex\" }, \"payload\": { \"task_group\": \"audio\", \"task\": \"tts\", \"function\": \"SpeechSynthesizer\", \"model\": \"cosyvoice-v3-flash\", \"parameters\": { \"text_type\": \"PlainText\", \"voice\": \"longanyang\", \"format\": \"mp3\", \"sample_rate\": 22050, \"volume\": 50, \"rate\": 1, \"pitch\": 1, \"enable_ssml\": true }, \"input\": {} }}";
        send(runTaskCommand);
    }

    @Override
    public void onMessage(String message) {
        System.out.println("收到服务端返回的消息：" + message);
        try {
            // Parse JSON message
            Map<String, Object> messageMap = new ObjectMapper().readValue(message, Map.class);

            if (messageMap.containsKey("header")) {
                Map<String, Object> header = (Map<String, Object>) messageMap.get("header");

                if (header.containsKey("event")) {
                    String event = (String) header.get("event");

                    if ("task-started".equals(event)) {
                        System.out.println("收到服务端返回的task-started事件");

                        // 发送 continue-task 指令，使用SSML功能时，该指令只允许发送一次
                        // 特殊字符需要进行转义
                        sendContinueTask("<speak rate=\\\"2\\\">我的语速比正常人快。</speak>");

                        // 发送finish-task指令
                        sendFinishTask();
                    } else if ("task-finished".equals(event)) {
                        System.out.println("收到服务端返回的task-finished事件");
                        taskFinished = true;
                        closeConnection();
                    } else if ("task-failed".equals(event)) {
                        System.out.println("任务失败：" + message);
                        closeConnection();
                    }
                }
            }
        } catch (Exception e) {
            System.err.println("出现异常：" + e.getMessage());
        }
    }

    @Override
    public void onMessage(ByteBuffer message) {
        System.out.println("收到的二进制音频数据大小为：" + message.remaining());

        try (FileOutputStream fos = new FileOutputStream(outputFile, true)) {
            byte[] buffer = new byte[message.remaining()];
            message.get(buffer);
            fos.write(buffer);
            System.out.println("音频数据已写入本地文件" + outputFile + "中");
        } catch (IOException e) {
            System.err.println("音频数据写入本地文件失败：" + e.getMessage());
        }
    }

    @Override
    public void onClose(int code, String reason, boolean remote) {
        System.out.println("连接关闭：" + reason + " (" + code + ")");
    }

    @Override
    public void onError(Exception ex) {
        System.err.println("报错：" + ex.getMessage());
        ex.printStackTrace();
    }

    private void sendContinueTask(String text) {
        String command = "{ \"header\": { \"action\": \"continue-task\", \"task_id\": \"" + taskId + "\", \"streaming\": \"duplex\" }, \"payload\": { \"input\": { \"text\": \"" + text + "\" } }}";
        send(command);
    }

    private void sendFinishTask() {
        String command = "{ \"header\": { \"action\": \"finish-task\", \"task_id\": \"" + taskId + "\", \"streaming\": \"duplex\" }, \"payload\": { \"input\": {} }}";
        send(command);
    }

    private void closeConnection() {
        if (!isClosed()) {
            close();
        }
    }

    public static void main(String[] args) {
        try {
            // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
            // 若没有配置环境变量，请用百炼API Key将下行替换为：String apiKey = "sk-xxx"
            String apiKey = System.getenv("DASHSCOPE_API_KEY");
            if (apiKey == null || apiKey.isEmpty()) {
                System.err.println("请设置 DASHSCOPE_API_KEY 环境变量");
                return;
            }

            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "bearer " + apiKey);
            // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference/
            TTSWebSocketClient client = new TTSWebSocketClient(new URI("wss://dashscope.aliyuncs.com/api-ws/v1/inference/"), headers);

            client.connect();

            while (!client.isClosed() && !client.taskFinished) {
                Thread.sleep(1000);
            }
        } catch (Exception e) {
            System.err.println("连接WebSocket服务失败：" + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

如您使用Python编程语言，建议采用Python DashScope SDK进行开发，详情请参见 [Python SDK](https://help.aliyun.com/zh/model-studio/cosyvoice-python-sdk "")。

以下是Python WebSocket的调用示例。在运行示例前，请确保通过如下方式导入依赖：

```bash
pip uninstall websocket-client
pip uninstall websocket
pip install websocket-client
```

**重要**

请不要将运行示例代码的Python文件命名为“websocket.py”，否则会报错（AttributeError: module 'websocket' has no attribute 'WebSocketApp'. Did you mean: 'WebSocket'?）。

```python
# SSML功能说明：
#     1. 在发送run-task指令时，将参数enable_ssml设置为true，以开启SSML支持
#     2. 通过continue-task指令发送包含SSML的文本，且只允许发送一次continue-task指令
#     3. 只有cosyvoice-v3-flash、cosyvoice-v3-plus和cosyvoice-v2模型的复刻音色以及音色列表中标记为支持SSML的系统音色支持SSML功能（例如cosyvoice-v3-flash模型的longanyang音色）

import websocket
import json
import uuid
import os
import time

class TTSClient:
    def __init__(self, api_key, uri):
        """
    初始化 TTSClient 实例

    参数:
        api_key (str): 鉴权用的 API Key
        uri (str): WebSocket 服务地址
    """
        self.api_key = api_key  # 替换为你的 API Key
        self.uri = uri  # 替换为你的 WebSocket 地址
        self.task_id = str(uuid.uuid4())  # 生成唯一任务 ID
        self.output_file = f"output_{int(time.time())}.mp3"  # 输出音频文件路径
        self.ws = None  # WebSocketApp 实例
        self.task_started = False  # 是否收到 task-started
        self.task_finished = False  # 是否收到 task-finished / task-failed

    def on_open(self, ws):
        """
    WebSocket 连接建立时回调函数
    发送 run-task 指令开启语音合成任务
    """
        print("WebSocket 已连接")

        # 构造 run-task 指令
        run_task_cmd = {
            "header": {
                "action": "run-task",
                "task_id": self.task_id,
                "streaming": "duplex"
            },
            "payload": {
                "task_group": "audio",
                "task": "tts",
                "function": "SpeechSynthesizer",
                "model": "cosyvoice-v3-flash",
                "parameters": {
                    "text_type": "PlainText",
                    "voice": "longanyang",
                    "format": "mp3",
                    "sample_rate": 22050,
                    "volume": 50,
                    "rate": 1,
                    "pitch": 1,
                    # 如果enable_ssml设为True，只允许发送一次continue-task指令，否则会报错“Text request limit violated, expected 1.”
                    "enable_ssml": True
                },
                "input": {}
            }
        }

        # 发送 run-task 指令
        ws.send(json.dumps(run_task_cmd))
        print("已发送 run-task 指令")

    def on_message(self, ws, message):
        """
    接收到消息时的回调函数
    区分文本和二进制消息处理
    """
        if isinstance(message, str):
            # 处理 JSON 文本消息
            try:
                msg_json = json.loads(message)
                print(f"收到 JSON 消息: {msg_json}")

                if "header" in msg_json:
                    header = msg_json["header"]

                    if "event" in header:
                        event = header["event"]

                        if event == "task-started":
                            print("任务已启动")
                            self.task_started = True

                            # 发送 continue-task 指令，使用SSML功能时，该指令只允许发送一次
                            # 特殊字符需要进行转义
                            self.send_continue_task("<speak rate=\"2\">我的语速比正常人快。</speak>")

                            # continue-task 发送完成后发送 finish-task
                            self.send_finish_task()

                        elif event == "task-finished":
                            print("任务已完成")
                            self.task_finished = True
                            self.close(ws)

                        elif event == "task-failed":
                            error_msg = msg_json.get("error_message", "未知错误")
                            print(f"任务失败: {error_msg}")
                            self.task_finished = True
                            self.close(ws)

            except json.JSONDecodeError as e:
                print(f"JSON 解析失败: {e}")
        else:
            # 处理二进制消息（音频数据）
            print(f"收到二进制消息，大小: {len(message)} 字节")
            with open(self.output_file, "ab") as f:
                f.write(message)
            print(f"已将音频数据写入本地文件{self.output_file}中")

    def on_error(self, ws, error):
        """发生错误时的回调"""
        print(f"WebSocket 出错: {error}")

    def on_close(self, ws, close_status_code, close_msg):
        """连接关闭时的回调"""
        print(f"WebSocket 已关闭: {close_msg} ({close_status_code})")

    def send_continue_task(self, text):
        """发送 continue-task 指令，附带要合成的文本内容"""
        cmd = {
            "header": {
                "action": "continue-task",
                "task_id": self.task_id,
                "streaming": "duplex"
            },
            "payload": {
                "input": {
                    "text": text
                }
            }
        }

        self.ws.send(json.dumps(cmd))
        print(f"已发送 continue-task 指令，文本内容: {text}")

    def send_finish_task(self):
        """发送 finish-task 指令，结束语音合成任务"""
        cmd = {
            "header": {
                "action": "finish-task",
                "task_id": self.task_id,
                "streaming": "duplex"
            },
            "payload": {
                "input": {}
            }
        }

        self.ws.send(json.dumps(cmd))
        print("已发送 finish-task 指令")

    def close(self, ws):
        """主动关闭连接"""
        if ws and ws.sock and ws.sock.connected:
            ws.close()
            print("已主动关闭连接")

    def run(self):
        """启动 WebSocket 客户端"""
        # 设置请求头部（鉴权）
        header = {
            "Authorization": f"bearer {self.api_key}",
            "X-DashScope-DataInspection": "enable"
        }

        # 创建 WebSocketApp 实例
        self.ws = websocket.WebSocketApp(
            self.uri,
            header=header,
            on_open=self.on_open,
            on_message=self.on_message,
            on_error=self.on_error,
            on_close=self.on_close
        )

        print("正在监听 WebSocket 消息...")
        self.ws.run_forever()  # 启动长连接监听

# 示例使用方式
if __name__ == "__main__":
    # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    # 若没有配置环境变量，请用百炼API Key将下行替换为：API_KEY = "sk-xxx"
    API_KEY = os.environ.get("DASHSCOPE_API_KEY")
    # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/inference/
    SERVER_URI = "wss://dashscope.aliyuncs.com/api-ws/v1/inference/"

    client = TTSClient(API_KEY, SERVER_URI)
    client.run()
```

## 标签

**说明**

阿里巴巴语音合成服务在实现 SSML 时参考了 [W3C](https://www.w3.org/TR/speech-synthesis/) SSML 1.0 规范，但在设计上更注重业务适配性。因此，并未完整支持所有标准标签，而是结合实际使用场景，实现了最具实用价值的标签集合。

- 所有使用 SSML 功能的文本内容必须包含在 `<speak></speak>` 标签内。

- 支持多个 `<speak>` 标签并列使用（如：`<speak></speak><speak></speak>`），但不支持嵌套结构（如：`<speak><speak></speak></speak>`）。

- 编码时，若标签内的文本内容包含 XML 特殊字符，需进行相应的字符转义。常见特殊字符及其转义形式如下：

  - `"`（双引号） → `&quot;`

  - `'`（单引号/撇号） → `&apos;`

  - `&`（表示“和”的符号） → `&amp;`

  - `<`（小于号） → &lt;

  - `>`（大于号） → &gt;

### `<speak>` **：根节点**

- 描述

`<speak>` 标签是所有 SSML 标签的根节点，任何使用 SSML 功能的文本内容都必须包含在 `<speak></speak>` 标签之间。

- 语法















```xml
<speak>需要使用SSML功能的文本</speak>
```

- 属性




| **属性名称** | **属性类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **属性名称** | **属性类型** | **是否必选** | **描述** |
| voice | String | 否 | 指定发音人（音色）。<br>优先级高于接口请求参数`voice`指定的发音人。<br>  - 取值范围：具体的音色，详情请参见 [cosyvoice-v2音色](https://help.aliyun.com/zh/model-studio/cosyvoice-java-sdk#da9ae03e5ek7b "")。<br>    <br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak voice="longcheng_v2"><br>      我是男声。<br>    </speak><br>    ``` |
| rate | String | 否 | 指定语速。优先级高于接口请求参数`speech_rate`指定的语速。<br>  - 取值范围：\[0.5,2\]之间的小数<br>    <br>  - 默认值：1<br>    <br>    - 大于1表示加快语速<br>      <br>    - 小于1表示减慢语速<br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak rate="2"><br>      我的语速比正常人快。<br>    </speak><br>    ``` |
| pitch | String | 否 | 指定音高（语调）。优先级高于接口请求参数`pitch_rate`指定的音高（语调）。<br>  - 取值范围：\[0.5,2\]之间的小数<br>    <br>  - 默认值：1<br>    <br>    - 大于1表示升高音高<br>      <br>    - 小于1表示降低音高<br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak pitch="0.5"><br>      我的音高却比别人低。<br>    </speak><br>    ``` |
| volume | String | 否 | 指定音量。优先级高于接口请求参数`volume`指定的音量。<br>  - 取值范围：\[0,100\]之间的整数<br>    <br>  - 默认值：50<br>    <br>    - 大于50表示增大音量<br>      <br>    - 小于50表示减小音量<br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak volume="80"><br>      我的音量也很大。<br>    </speak><br>    ``` |
| effect | String | 否 | 指定音效。<br>  - 取值范围：<br>    <br>    <br>    - robot：机器人音效<br>      <br>    - lolita：萝莉音效<br>      <br>    - lowpass：低通音效<br>      <br>    - echo：回声音效<br>      <br>    - eq：均衡器（高级）<br>      <br>    - lpfilter：低通滤波器（高级）<br>      <br>    - hpfilter：高通滤波器（高级）<br>      <br>**说明**<br>    - eq、lpfilter、hpfilter是高级音效类型，您可以通过`effectValue`参数自定义其具体效果。<br>      <br>    - 每个 SSML 标签仅支持配置一种音效，不允许多个 `effect` 属性共存。<br>      <br>    - 使用音效功能会增加系统延时。<br>      <br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak effect="robot"><br>      你喜欢机器人瓦力吗？<br>    </speak><br>    ``` |
| effectValue | String | 否 | 指定音效（`effect`参数）的具体效果。<br>  - 取值范围：<br>    <br>    - `eq`（均衡器）：系统默认支持8个频率等级，对应频率如下：<br>      <br>      \[“40 Hz”,“100 Hz”, “200 Hz”, “400 Hz”, “800 Hz”, “1600 Hz”, “4000 Hz”, “12000 Hz”\]。<br>      <br>      每个频段带宽均为1.0q。<br>      <br>      使用时需通过 `effectValue` 参数指定每个频段的增益值，该参数为一个由 8 个整数组成的字符串，数值范围为 \[-20, 20\]，数字之间用空格分隔，数值为 `0` 表示不调整对应频率的增益。<br>      <br>      例如：`effectValue="1 1 1 1 1 1 1 1"`<br>      <br>    - `lpfilter`（低通滤波器）：输入低通滤波器的频率值。取值为(0, 目标采样率/2\]之间的整数。例如effectValue="800"。<br>      <br>    - `hpfilter`（高通滤波器）：输入高通滤波器的频率值。取值为(0, 目标采样率/2\]之间的整数。例如effectValue="1200"。<br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak effect="eq" effectValue="1 -20 1 1 1 1 20 1"><br>      你喜欢机器人瓦力吗？<br>    </speak><br>    <br>    <speak effect="lpfilter" effectValue="1200"><br>      你喜欢机器人瓦力吗？<br>    </speak><br>    <br>    <speak effect="hpfilter" effectValue="1200"><br>      你喜欢机器人瓦力吗？<br>    </speak><br>    ``` |
| bgm | String | 否 | 为合成的语音添加指定的背景音乐。背景音文件需存储在阿里云 OSS 上（请参见 [上传文件](https://help.aliyun.com/zh/oss/getting-started/upload-objects-16#concept-zx1-4p4-tdb "")），且所在存储空间（Bucket）应至少具有公共读权限。<br>背景音乐URL中若包含 XML 特殊字符（如 `&`, `<`, `>` 等），需进行字符转义处理。<br>  - 音频要求：<br>    <br>    音频文件大小无上限，但较大的文件可能会增加下载耗时；若合成内容的时长超过背景音时长，背景音将自动循环播放以匹配合成音频长度。<br>    <br>    - 采样率：16kHz<br>      <br>    - 声道数：单声道<br>      <br>    - 文件格式：WAV<br>      <br>      若原始音频非 WAV 格式，可使用 `ffmpeg` 工具进行转换：<br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      ```bash<br>      ffmpeg -i 输入音频 -acodec pcm_s16le -ac 1 -ar 16000 输出.wav<br>      ```<br>      <br>    - 位深度：16位<br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak bgm="http://nls.alicdn.com/bgm/2.wav" backgroundMusicVolume="30" rate="-500" volume="40"><br>      <break time="2s"/><br>      阴崖老木苍苍烟<br>      <break time="700ms"/><br>      雨声犹在竹林间<br>      <break time="700ms"/><br>      绵蕝固知裨国计<br>      <break time="700ms"/><br>      绵州风物总堪怜<br>      <break time="2s"/><br>    </speak><br>    ```<br>    <br>**重要**<br>您需要对上传的音频版权承担相应的法律责任。 |
| backgroundMusicVolume | String | 否 | 指定背景音乐的音量。和`backgroundMusicVolume`属性搭配使用。 |

- 标签关系

<speak>标签可以包含文本和其他标签：

  - [控制停顿时间](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#title-722-sn2-4x8 "")

  - [替换文本](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#title-4jk-q1t-jwz "")

  - [指定发音（拼音/音标）](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#title-m9h-7yc-48k "")

  - [插入一段外部声音（铃声、猫叫等）](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#title-al9-xs8-oer "")

  - [设置文本的读法（数字、日期、电话号码等）](https://help.aliyun.com/zh/model-studio/introduction-to-cosyvoice-ssml-markup-language#title-xt2-m52-1uk "")
- 更多示例

  - 空属性















    ```xml
    <speak>
      需要调用SSML标签的文本
    </speak>
    ```

  - 属性组合（空格分隔）















    ```xml
    <speak rate="200" pitch="-100" volume="80">
      所以放在一起，我的声音是这样的。
    </speak>
    ```

### <break>：控制停顿时间

- 描述

在语音合成过程中添加一段静默时间，模拟自然说话中的停顿效果。支持秒（s）或毫秒（ms）单位设置。该标签是可选标签。

- 语法















```xml
# 空属性
<break/>
# 带time属性
<break time="string"/>
```

- 属性



**说明**





使用无属性的<break>标签时，停顿时长为“1s”。








| **属性名称** | **属性类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **属性名称** | **属性类型** | **是否必选** | **描述** |
| time | String | 否 | 以秒/毫秒为单位设置停顿的时长 （如“2s”、“50ms”）。<br>  - 取值范围：<br>    <br>    - 以秒（s）为单位，取值范围为\[1, 10\]之间的整数<br>      <br>    - 以毫秒（ms）为单位，取值范围为\[50, 10000\]之间的整数<br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak><br>      请闭上眼睛休息一下<break time="500ms"/>好了，请睁开眼睛。<br>    </speak><br>    ```<br>    <br>**重要**<br>当连续使用多个 `<break>` 标签时，总的停顿时长为各个标签指定时间的累加。若总时长超过 10 秒，则仅生效前 10 秒。<br>如下所示，该段 SSML 中 `<break>` 标签累计时长为 15 秒，超过 10 秒限制，最终停顿时长将被截断为 10 秒：<br>```xml<br><speak><br>  请闭上眼睛休息一下<break time="5s"/><break time="5s"/><break time="5s"/>好了，请睁开眼睛。<br></speak><br>``` |

- 标签关系

<break>是空标签，不能包含任何标签。


### <sub>：替换文本

- 描述

将某段文本替换为指定的更适合朗读的文本。例如将 “W3C” 读成 “网络协议标准”。该标签是可选标签。

- 语法















```xml
<sub alias="string"></sub>
```

- 属性




| **属性名称** | **属性类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **属性名称** | **属性类型** | **是否必选** | **描述** |
| alias | String | 是 | 将某段文本替换为更适合朗读的文本。<br>示例：<br>```xml<br> <speak><br>   <sub alias="网络协议标准">W3C</sub><br> </speak><br>``` |

- 标签关系

<sub>标签仅可以包括文本。


### <phoneme>：指定发音（拼音/音标）

- 描述

控制某段文本的具体发音方式，中文可用拼音，英文可用音标（如 CMU），适用于需要精准发音的场景。该标签是可选标签。

- 语法















```xml
<phoneme alphabet="string" ph="string">文本</phoneme>
```

- 属性




| **属性名称** | **属性类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **属性名称** | **属性类型** | **是否必选** | **描述** |
| alphabet | String | 是 | 指定发音类型：拼音（对应中文）或音标（对应英文）。<br>取值范围：<br>  - "py"：拼音<br>    <br>  - "cmu"：音标，参见 [The CMU Pronouncing Dictionary](http://www.speech.cs.cmu.edu/cgi-bin/cmudict) |
| ph | String | 是 | 指定具体的拼音或音标：<br>  - 字与字的拼音用空格分隔，拼音的数目必须与字数一致。<br>    <br>  - 每个拼音由发音部分和音调组成，其中音调为 `1` 到 `5` 的整数，`5` 表示轻声。<br>    <br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak><br>      去<phoneme alphabet="py" ph="dian3 dang4 hang2">典当行</phoneme>把这个玩意<phoneme alphabet="py" ph="dang4 diao4">当掉</phoneme><br>    </speak><br>    <br>    <speak><br>      How to spell <phoneme alphabet="cmu" ph="S AY N">sin</phoneme>?<br>    </speak><br>    ``` |

- 标签关系

<phoneme>标签仅包括文本。


### <soundEvent>：插入一段外部声音（铃声、猫叫等）

- 描述

支持在语音中插入音效文件，如提示音、环境音等，增强语音表达的丰富性。该标签是可选标签。

- 语法















```xml
<soundEvent src="URL"/>
```

- 属性




| **属性名称** | **属性类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **属性名称** | **属性类型** | **是否必选** | **描述** |
| src | String | 是 | 设置外部音频URL。<br>音频文件需存储在阿里云 OSS 上（请参见 [上传文件](https://help.aliyun.com/zh/oss/getting-started/upload-objects-16#concept-zx1-4p4-tdb "")），且所在存储空间（Bucket）应至少具有公共读权限。URL中若包含 XML 特殊字符（如 `&`, `<`, `>` 等），需进行字符转义处理。<br>  - 音频要求：<br>    <br>    <br>    - 采样率：16kHz<br>      <br>    - 声道数：单声道<br>      <br>    - 文件格式：WAV<br>      <br>      若原始音频非 WAV 格式，可使用 `ffmpeg` 工具进行转换：<br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      <br>      ```bash<br>      ffmpeg -i 输入音频 -acodec pcm_s16le -ac 1 -ar 16000 输出.wav<br>      ```<br>      <br>    - 文件大小：不超过2MB<br>      <br>    - 位深度：16位<br>  - 示例：<br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    <br>    ```xml<br>    <speak><br>      一匹马受了惊吓<soundEvent src="http://nls.alicdn.com/sound-event/horse-neigh.wav"/>人们四散躲避<br>    </speak><br>    ```<br>    <br>**重要**<br>您需要对上传的音频版权承担相应的法律责任。 |

- 标签关系

<soundEvent>是空标签，不可以包含任何标签。


### <say-as>：设置文本的读法（数字、日期、电话号码等）

- 描述

告诉大模型文本是什么类型，并按该类型的常规读法进行朗读。该标签是可选标签。

- 语法















```xml
<say-as interpret-as="string">文本</say-as>
```

- 属性




| **属性名称** | **属性类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **属性名称** | **属性类型** | **是否必选** | **描述** |
| interpret-as | String | 是 | 指示出标签内文本的信息类型。<br>取值范围：<br>  - cardinal：按整数或小数的常见读法朗读<br>    <br>  - digits：按数字逐个读出（如：123 → 一二三）<br>    <br>  - telephone：按电话号码的常用方式读出<br>    <br>  - name：按人名的常规读法朗读<br>    <br>  - address：按地址的常见方式读出<br>    <br>  - id：适用于账户名、昵称等，按常规读法处理<br>    <br>  - characters：将标签内的文本按字符一一读出<br>    <br>  - punctuation：将标签内的文本按标点符号的方式读出来<br>    <br>  - date：按日期格式的常见读法朗读<br>    <br>  - time：按时间格式的常见方式读出<br>    <br>  - currency：按金额的常见读法处理<br>    <br>  - measure：按计量单位的常见方式读出 |

- 各<say-as>类型支持范围

  - cardinal




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字串 | 145 | 一百四十五 | 整数输入范围：20位以内的正负整数，\[-99999999999999999999,99999999999999999999\]。<br>小数输入范围：对小数点后小数的位数没有特殊限制，建议不超过10位。 |
    | 负号+数字串 | -145 | 负一百四十五 |
    | 以逗号分隔3位数字串 | 10,000 | 一万 |
    | 负号+以逗号分隔3位数字串 | -10,124 | 负一万一百二十四 |
    | 数字串+小数点+2个零 | 10.00 | 十 |
    | 负号+数字串+小数点+2个零 | -110.00 | 负一百一十 |
    | 数字串+小数点+数字串 | 79.090 | 七十九点零九零 |
    | 负号+数字串+小数点+数字串 | -79.001 | 负七十九点零零一 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字串 | 145 | one hundred forty five | 整数输入范围：13位以内的正负整数，\[-999999999999,999999999999\]。<br>小数输入范围：对小数点后小数的位数没有特殊限制，建议不超过10位。 |
    | 以零开头的数字串 | 0145 | one hundred forty five |
    | 负号+数字串 | -145 | minus hundred forty five |
    | 以逗号分隔三位数字串 | 60,000 | sixty thousand |
    | 负号+以逗号分隔三位数字串 | -208,000 | minus two hundred eight thousand |
    | 数字串+小数点+零 | 12.00 | twelve |
    | 数字串+小数点+数字串 | 12.34 | twelve point three four |
    | 以逗号分隔三位数字串+小数点+数字串 | 1,000.1 | one thousand point one |
    | 负号+数字串+小数点+数字串 | -12.34 | minus twelve point three four |
    | 负号+以逗号分隔三位数字串+小数点+数字串 | -1,000.1 | minus one thousand point one |
    | （以逗号分隔三位）数字串+连词符+（以逗号分隔三位）数字 | 1-1,000 | one to one thousand |
    | 其他默认读法 | 012.34 | twelve point three four | 无 |
    | 1/2 | one half |
    | -3/4 | minus three quarters |
    | 5.1/6 | five point one over six |
    | -3 1/2 | minus three and a half |
    | 1,000.3^3 | one thousand point three to the power of three |
    | 3e9.1 | three times ten to the power of nine point one |
    | 23.10% | twenty three point one percent |

  - digits




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字串 | 129090909 | 一二九零九零九零九 | 对数字串的长度没有特殊限制，建议不超过20位。<br>当数字串超过10位时，每个数字后插入停顿。 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字串 | 12034 | one two zero three four | 对数字串的长度没有特殊限制，建议不超过20位。<br>当数字串以空格或连词符分组时，分组之间会插入逗号而产生适当停顿，支持最长5个分组。 |
    | 数字串+空格或连词符+数字串+空格或连词符+数字串+空格或连词符+数字串 | 1-23-456 7890 | one, two three, four five six, seven eight nine zero |

  - telephone




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 座机号 | 4930286 | 四九三 零二八六 | 支持7~8位座机号，支持空格和“-”作为分隔符。<br>其中，7位座机号支持“3-4”的数字分隔方式；8位座机号支持“4-4”的数字分隔方式。 |
    | 493 0286 | 四九三 零二八六 |
    | 493-0286 | 四九三 零二八六 |
    | 62552560 | 六二五五 二五六零 |
    | 6255 2560 | 六二五五 二五六零 |
    | 6255-2560 | 六二五五 二五六零 |
    | 座机号+分机号 | 4930286-109 | 四九三 零二八六 转幺零九 | 支持1~4位分机号。 |
    | 4930286转109 | 四九三 零二八六 转幺零九 |
    | 4930286分机109 | 四九三 零二八六 分机幺零九 |
    | 4930286分机号109 | 四九三 零二八六 分机号幺零九 |
    | 区号+座机号 | 01062552560 | 零幺零 六二五五 二五六零 | 支持区号：010、02x、03xx、04xx、05xx、07xx、08xx、09xx。 |
    | 010 62552560 | 零幺零 六二五五 二五六零 |
    | 010 6255 2560 | 零幺零 六二五五 二五六零 |
    | 010 6255-2560 | 零幺零 六二五五 二五六零 |
    | 010-62552560 | 零幺零 六二五五 二五六零 |
    | 010-6255-2560 | 零幺零 六二五五 二五六零 |
    | (010)62552560 | 零幺零 六二五五 二五六零 |
    | 03198907098 | 零三幺九 八九零 七零九八 |
    | 0319-8907098 | 三幺九 八九零 七零九八 |
    | 区号+座机号+分机号 | 010 62552560-109 | 零幺零 六二五五 二五六零 转幺零九 | 无 |
    | 010-62552560-109 | 零幺零 六二五五 二五六零 转幺零九 |
    | (010)62552560-109 | 零幺零 六二五五 二五六零 转幺零九 |
    | (010)62552560转109 | 零幺零 六二五五 二五六零 转幺零九 |
    | (010)62552560分机109 | 零幺零 六二五五 二五六零 分机幺零九 |
    | (010)62552560分机号109 | 零幺零 六二五五 二五六零 分机号幺零九 |
    | 国家代码+区号+座机号 | 86-010-62791627 | 八六 零幺零 六二七九 幺六二七 | 支持国家代码：86、 (86)、+86、(+86)、0086。并统一读为“八六”。 |
    | (86)10-62791627 | 八六 幺零 六二七九 幺六二七 |
    | +86-010-62791627 | 八六 零幺零 六二七九 幺六二七 |
    | 0086-10-62791627 | 八六 幺零 六二七九 幺六二七 |
    | (+86)-10-6279 1627 | 八六 幺零 六二七九 幺六二七 |
    | 国家代码+区号+座机号+分机号 | (86)21-58118818-207 | 八六 二幺 五八幺幺 八八幺八 转二零七 | 无 |
    | (86)021-5811-8818-207 | 八六 零二幺 五八幺幺 八八幺八 转二零七 |
    | (86)021-58118818转207 | 八六 零二幺 五八幺幺 八八幺八 转二零七 |
    | (86)21-5811-8818分机207 | 八六 二幺 五八幺幺 八八幺八 分机二零七 |
    | +86-021-58118818分机号207 | 八六 零二幺 五八幺幺 八八幺八分机号二零七 |
    | 手机号 | 139 0000 5678 | 幺三九 零零零零 五六七八 | 支持11位手机号，支持3-3-5、3-4-4两种数字分隔方式 |
    | 139-000-05678 | 幺三九 零零零 零五六七八 |
    | 139 000 05678 | 幺三九 零零零 零五六七八 |
    | 国家代码+手机号 | +86-13900005678 | 八六 幺三九 零零零零 五六七八 | 无 |
    | (+86)-139-0000-5678 | 八六 幺三九 零零零零 五六七八 |
    | +8613900005678 | 八六 幺三九 零零零零 五六七八 |
    | 0086-139 000 05678 | 八六 幺三九 零零零 零五六七八 |
    | 服务号 | 123 | 幺二三 | - 支持常用的服务号。<br>      <br>    - 支持以400/800开头的10位服务号，支持以“3-3-4”的数字分隔方式。<br>      <br>    - 支持以12530/17951/12593开头的16位号码。 |
    | 95678 | 九五六七八 |
    | 4008110510 | 四零零 八幺幺 零五幺零 |
    | 800-810-8888 | 八零零 八幺零 八八八八 |
    | 1253013520638377 | 幺二五三零 幺三五 二零六三 八三七七 |
    | 其他 | (86)(21)9899-80800-0909 | 八六 二幺 九八九九 八零八零零 零九零九 | 支持“数字串+分隔符（左右括号、-）”方式。 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字串 | 12034 | one two oh three four | 对数字串的长度没有特殊限制，建议不超过20位。当数字串以空格或连词符分组时，分组之间会插入逗号而产生适当停顿，支持最长5个分组。 |
    | 数字串+空格或连词符+数字串+空格或连词符+数字串 | 1-23-456 7890 | one, two three, four five six, seven eight nine oh |
    | 加号+数字串+空格或连词符+数字串 | +43-211-0567 | plus four three, two one one, oh five six seven |
    | 左括号+数字串+右括号+空格+数字串+空格或连词符+数字串 | (21) 654-3210 | (two one) six five four, three two one oh |

  - address




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 常用地址格式 | 元和镇嘉元30-9 | 元和镇嘉元三十杠九 | 支持常用地址格式。此处地址指标准的邮寄地址。 |
    | 市台路388弄1107-1108号 | 市台路三八八弄幺幺零七杠幺幺零八号 |
    | 华润二十四城六期锦云府3-1-3205 | 华润二十四城六期锦云府三杠一杠三二零五 |
    | 圣华名都大厦2幢2006室 | 圣华名都大厦二幢二零零六室 |
    | 五常街道庭院5幢4单元201 | 五常街道庭院五幢四单元二零幺 |
    | 芙蓉江路150弄19号 | 芙蓉江路幺五零弄十九号 |



    英文文本不支持该标签。

  - id




    | **格式** | **示例** | **输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **输出** | **说明** |
    | 字符串 | dell0101 | D E L L 零 一 零 一 | 大小写英文字符、阿拉伯数字0~9、下划线。<br>输出的空格表示每个字符之间插入停顿，即字符一个一个地读。 |
    | myid\_1998 | M Y I D 下划线 一 九 九 八 |
    | AiTest | A I T E S T |



    英文文本该标签功能同标签characters。

  - characters




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 字符串 | ISBN 1-001-099098-1 | I S B N 一 杠 零 零 一 杠 零 九 九 零 九 八 杠 一 | 支持中文汉字、大小写英文字符、阿拉伯数字0~9以及部分全角和半角字符。<br>输出的空格表示每个字符之间插入停顿，即字符一个一个地读。标签内的文本如果包含XML的特殊字符，需要做字符转义。 |
    | x10b2345\_u | x 一 零 b 二 三 四 五 下划线 u |
    | v1.0.1 | v 一 点 零 点 一 |
    | 版本号2.0 | 版本号二 点 零 |
    | 苏M MA000 | 苏M M A 零 零 零 |
    | 空中客车A330 | 空中客车A 三 三 零 |
    | 型号s01 s02和s03 | 型号s 零 一 s 零二 和s 零 三 |
    | 空中客车A330 | 空中客车A 三 三 零 |
    | αβγ | 阿尔法 贝塔 伽玛 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 字符串 | \*b+3$.c-0'=α | asterisk B plus three dollar dot C dash zero apostrophe equals alpha | 支持中文汉字、大小写英文字符、阿拉伯数字0~9以及部分全角和半角字符。<br>输出的空格表示每个字符之间插入停顿，即字符一个一个地读。<br>标签内的文本如果包含XML的特殊字符，需要做字符转义。 |

  - punctuation




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 标点符号 | … | 省略号 | 支持常见中英文标点。输出的空格表示每个字符之间插入停顿，即字符一个一个地读。<br>标签内的文本如果包含XML的特殊字符，需要做字符转义。 |
    | …… | 省略号 |
    | !"#$%& | 叹号 双引号 井号 dollar 百分号 and |
    | ‘()\*+ | 单引号 左括号 右括号 星号 加号 |
    | ,-./:; | 逗号 杠 点 斜杠 冒号 分号 |
    | <=>?@ | 小于 等号 大于 问号 at |
    | \[\\\]^\_ | 左方括号 反斜线 右方括号 脱字符 下划线 |



    英文文本该标签功能同标签characters。

  - date




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | xx年 | 71年 | 七一年 | 支持2位和4位年份。其中：<br>    - 2位年份支持60年~99年、00年~09年、10年~19年。<br>      <br>    - 4位年份支持1000年~1999年、2000年~2099年。 |
    | 04年 | 零四年 |
    | 19年 | 一九年 |
    | 1011年 | 一零一一年 |
    | 1998年 | 一九九八年 |
    | 2008年 | 二零零八年 |
    | xx年xx月 | 98年4月 | 九八年四月 | 当月份为1到9月时，支持开头带“0”和不带“0”两种写法。例如“1908年4月”和“1908年04月”。 |
    | 1998年04月 | 一九九八年四月 |
    | 08年8月 | 零八年八月 |
    | 2008年8月 | 二零零八年八月 |
    | xx年xx月xx日xx年xx月xx号 | 98年4月23日 | 九八年四月二十三日 | 当日期为1到9日时，支持开头带“0”和不带“0”两种写法。例如“1908年4月8日”和“1908年04月08日”。 |
    | 1998年04月23日 | 一九九八年四月二十三日 |
    | 08年8月8号 | 零八年八月八号 |
    | 2008年08月08号 | 二零零八年八月八号 |
    | xx年xx月xx日xx年xx月xx号 | 98年4月23日 | 九八年四月二十三日 | 当日期为1到9日时，支持开头带“0”和不“0”两种写法。例如“1908年4月8日”和“1908年04月08日”。 |
    | 1998年04月23日 | 一九九八年四月二十三日 |
    | 08年8月8号 | 零八年八月八号 |
    | 2008年08月08号 | 二零零八年八月八号 |
    | xx月xx号 | 3月20日 | 三月二十日 | 无 |
    | 08月07号 | 八月七号 |
    | 年月缩写 | 2018/08 | 二零一八年八月 | 支持“/”、“-”、“.”作为缩写的分隔符。 |
    | 2018-08 | 二零一八年八月 |
    | 2018.08 | 二零一八年八月 |
    | 年月日缩写 | 2018/08/08 | 二零一八年八月八日 |
    | 2018-8-8 | 二零一八年八月八日 |
    | 2018.08.08 | 二零一八年八月八日 |
    | xx年xx月xx日~xx年xx月xx日xx年xx月xx号~xx年xx月xx号 | 04年9月1日~30日 | 零四年九月一日至三十日 | 支持“~”、“-”作为“至”的缩写标志。 |
    | 2004年09月01号-2008年06月08号 | 二零零四年九月一号至二零零八年六月八号 |
    | xx年xx月xx日~xx日xx年xx月xx号~xx号 | 04年9月1日~30日 | 零四年九月一日至三十日 |
    | 2004年09月01号-2008年06月08号 | 二零零四年九月一号至二零零八年六月八号 |
    | xx年xx月~xx年xx月 | 01年04月~10年04月 | 零一年四月至一零年四月 |
    | 2001年04月~2010年04月 | 二零零一年四月至二零一零年四月 |
    | xx月xx日~xx月xx日xx月xx号~xx月xx号 | 10月1日~10月7日 | 十月一日至十月七日 |
    | 10月01号~10月07号 | 十月一号至十月七号 |
    | xx月xx日~xx日xx月xx号~xx号 | 10月1日~7日 | 十月一日至七日 |
    | 10月01号~07号 | 十月一号至七号 |
    | 年月日缩写~年月日缩写 | 2018/03/03~2019/01/01 | 二零一八年三月三日至二零一九年一月一日 | 支持“/”、“.”作为缩写的分隔符，支持“~”、“-”作为“至”的缩写标志。 |
    | 1997.9.9~1998.9.9 | 一九九七年九月九日至一九九八年九月九日 |
    | 月日缩写~月日缩写 | 10/20~10/31 | 十月二十日至十月三十一日 |
    | xx~xx月xx月~xx月 | 1~10月 | 一至十月 |
    | 1月~10月 | 一月至十月 |
    | 月日年缩写 | 10/20/2018 | 二零一八年十月二十日 | 仅支持4位的年份，仅支持“/”作为日期的分隔符，仅支持“月/日/年”的书写方式。 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 四位数字/两位数字或四位数字-两位数字 | 2000/01 | two thousand, oh one | 跨年度。 |
    | 1900-01 | nineteen hundred, oh one |
    | 2001-02 | twenty oh one, oh two |
    | 2019-20 | twenty nineteen, twenty |
    | 1998-99 | nineteen ninety eight, ninety nine |
    | 1999-00 | nineteen ninety nine, oh oh |
    | 以1或2开头的四位数字 | 2000 | two thousand | 四位数字年份。 |
    | 1900 | nineteen hundred |
    | 1905 | nineteen oh five |
    | 2021 | twenty twenty one |
    | 星期几-星期几<br>或<br>星期几~星期几<br>或<br>星期几&星期几 | mon-wed | monday to wednesday | 星期几的范围标签内的文本如果包含XML的特殊字符，需要做字符转义。 |
    | tue~fri | tuesday to friday |
    | sat&sun | saturday and sunday |
    | DD-DD MMM, YYYY<br>或<br>DD~DD MMM, YYYY<br>或<br>DD&DD MMM, YYYY | 19-20 Jan, 2000 | the nineteen to the twentieth of january two thousand | DD表示两位数字日期，MMM表示月份的三字母缩写或完整单词，YYYY表示以1或2开头的四位数字年份。 |
    | 01 ~ 10 Jul, 2020 | the first to the tenth of july twenty twenty |
    | 05&06 Apr, 2009 | the fifth and the sixth of april two thousand nine |
    | MMM DD-DD<br>或<br>MMM DD~DD<br>或<br>MMM DD&DD | Feb 01 - 03 | feburary the first to the third | MMM表示月份的三字母缩写或完整单词，DD表示两位数字日期。 |
    | Aug 10~20 | august the tenth to the twentieth |
    | Dec 11&12 | december the eleventh and the twelfth |
    | MMM-MMM<br>或<br>MMM~MMM<br>或<br>MMM&MMM | Jan-Jun | january to june | MMM表示月份的三字母缩写或完整单词。 |
    | jul ~ dec | july to december |
    | sep&oct | september and october |
    | YYYY-YYYY<br>或<br>YYYY~YYYY | 1990 - 2000 | nineteen ninety to two thousand | YYYY表示以1或2开头的四位数字年份。 |
    | 2001~2021 | two thousand one to twenty twenty one |
    | WWW DD MMM YYYY | Sun 20 Nov 2011 | sunday the twentieth of november twenty eleven | WWW表示星期几的三字母缩写或完整单词，DD表示两位数字日期，MMM表示月份的三字母缩写或完整单词，MM表示两位数字月份（或三字母缩写或完整单词），YYYY表示以1或2开头的四位数字年份。 |
    | WWW DD MMM | Sun 20 Nov | sunday the twentieth of november |
    | WWW MMM DD YYYY | Sun Nov 20 2011 | sunday november the twentieth twenty eleven |
    | WWW MMM DD | Sun Nov 20 | sunday november the twentieth |
    | WWW YYYY-MM-DD | Sat 2010-10-01 | aturday october the first twenty ten |
    | WWW YYYY/MM/DD | Sat 2010/10/01 | saturday october the first twenty ten |
    | WWW MM/DD/YYYY | Sun 11/20/2011 | sunday november the twentieth twenty eleven |
    | MM/DD/YYYY | 11/20/2011 | november the twentieth twenty eleven |
    | YYYY | 1998 | nineteen ninety eight |
    | 其他默认读法 | 10 Mar, 2001 | the tenth of march two thousand one | 无 |
    | 10 Mar | the tenth of march |
    | Mar 2001 | march two thousand one |
    | Fri. 10/Mar/2001 | friday the tenth of march two thousand one |
    | Mar 10th, 2001 | march the tenth two thousand one |
    | Mar 10 | march the tenth |
    | 2001/03/10 | march the tenth two thousand one |
    | 2001-03-10 | march the tenth two thousand one |
    | 2000s | two thousands |
    | 2010's | twenty tens |
    | 1900's | nineteen hundreds |
    | 1990s | nineteen nineties |

  - time




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 时刻 | 12:00 | 十二点 | 支持常用时间和时间范围格式。 |
    | 12:00:00点 | 十二点 |
    | 10:20分 | 十点二十分 |
    | 10:20:30 | 十点二十分三十秒 |
    | 09:18:14 | 九点十八分十四秒 |
    | 时刻~时刻 | 11:00~12:00 | 十一点到十二点 |
    | 09:00-14:00 | 九点到十四点 |
    | 11:00~11:30 | 十一点到十一点三十分 |
    | 11:00-12:18 | 十一点到十二点十八分 |
    | 10:30~11:00 | 十点三十分到十一点 |
    | 09:28-10:00 | 九点二十八分到十点 |
    | 10:20~11:20 | 十点二十分到十一点二十分 |
    | 06:00~08:00 | 六点到八点 |
    | 上午10:20~下午13:30 | 上午十点二十分到下午十三点三十分 |
    | 时间缩写 | 5:00 am | 凌晨五点整 |
    | 5:30 am | 凌晨五点半 |
    | 5:20:12 am | 凌晨五点二十分十二秒 |
    | 7:00 am | 上午七点整 |
    | 7:30 AM | 上午七点半 |
    | 7:20:12 a.m. | 上午七点二十分十二秒 |
    | 07:08:12 A.M. | 上午七点零八分十二秒 |
    | 5:00 pm | 下午五点整 |
    | 5:30 PM | 下午五点半 |
    | 5:20:12 p.m. | 下午五点二十分十二秒 |
    | 05:09:12 P.M. | 下午五点零九分十二秒 |
    | 9:00 pm | 晚上九点整 |
    | 9:30 pm | 晚上九点半 |
    | 9:20:12 PM | 晚上九点二十分十二秒 |
    | 9:02:12 P.M. | 晚上九点零二分十二秒 |
    | 12:00 pm | 中午十二点整 |
    | 12:30 p.m. | 中午十二点半 |
    | 12:20:12 PM | 中午十二点二十分十二秒 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | HH:MM AM或PM | 09:00 AM | nine A M | HH表示一或两位数字小时，MM表示两位数字分钟，AM/PM表示上/下午。 |
    | 09:03 PM | nine oh three P M |
    | 09:13 p.m. | nine thirteen p m |
    | HH:MM | 21:00 | twenty one hundred |
    | HHMM | 100 | one oclock |
    | 时刻-时刻 | 8:00 am - 05:30 pm | eight a m to five p m | 支持常见时间格式和范围。 |
    | 7:05~10:15 AM | seven oh five to ten fifteen A M |
    | 09:00-13:00 | nine oclock to thirteen hundred |

  - currency




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字+金额标识符 | 12.00 RMB | 十二人民币 | 支持AUD（澳元） 、CAD（加元）、 HKD（港币）、JPY（日元）、USD（美元）、CHF（瑞士法郎）、NOK（挪威克朗）、SEK（瑞典克朗）、GBP（英镑）、 RMB（人民币）、CNY（元）和EUR（欧元）。<br>支持的数字格式包括：整数、小数以及以逗号分隔的国际写法。 |
    | 12.50 RMB | 十二点五零人民币 |
    | 12,000,000 RMB | 一千二百万人民币 |
    | 12,000,000.00 RMB | 一千二百万人民币 |
    | 12,000.35 RMB | 一万两千点三五人民币 |
    | 金额标识符+数字 | $12 | 十二美元 | 支持 CAD（加元）、 $（美元）、Fr（法郎）、kr（丹麦克朗）、 £（英镑）、¥（元）和 €（欧元）。<br>支持的数字格式包括：整数、小数以及以逗号分隔的国际写法。 |
    | $12.00 | 十二美元 |
    | $12.12 | 二点一二美元 |
    | $12,000 | 一万两千美元 |
    | $12,000.00 | 一万两千美元 |
    | $12,000.99 | 一万两千点九九美元 |
    | 其他默认读法 | 1213 | 一千二百一十三 | 无 |
    | 1213 KML | 一千二百一十三K M L |
    | 1213.00 KML | 一千二百一十三K M L |
    | 1213.9 KML | 一千二百一十三点九K M L |
    | 1,000 KML | 一千K M L |
    | 1,000.00 KML | 一千K M L |
    | 1,000.98 KML | 一千点九八K M L |
    | 12,000 | 一万两千 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字+金额识别符 | 1.00 RMB | one yuan | 支持的数字格式：整数、小数以及以逗号分隔的国际写法。<br>支持的金额识别符：<br>CN¥ (yuan)<br>CNY (yuan)<br>RMB (yuan)<br>AUD (australian dollar)<br>CAD (canadian dollar)<br>CHF (swiss franc)<br>DKK (danish krone)<br>EUR (euro)<br>GBP (british pound)<br>HKD (Hong Kong(China) dollar)<br>JPY (japanese yen)<br>NOK (norwegian krone)<br>SEK (swedish krona)<br>SGD (singapore dollar)<br>USD (united states dollar) |
    | 2.02 CNY | two point zero two yuan |
    | 1,000.23 CN¥ | one thousand point two three yuan |
    | 1.01 SGD | one singapore dollar and one cent |
    | 2.01 CAD | two canadian dollars and one cent |
    | 3.1 HKD | three hong kong dollars and ten cents |
    | 1,000.00 EUR | one thousand euros |
    | 金额识别符+数字 | US$ 1.00 | one US dollar | 支持的数字格式：整数、小数以及以逗号分隔的国际写法。<br>支持的金额识别符：<br>US$ (US dollar)<br>CA$ (Canadian dollar)<br>AU$ (Australian dollar)<br>SG$ (Singapore dollar)<br>HK$ (Hong Kong dollar)<br>C$ (Canadian dollar)<br>A$ (Australian dollar)<br>$ (dollar)<br>£ (pound)<br>€ (euro)<br>CN¥ (yuan)<br>CNY (yuan)<br>RMB (yuan)<br>AUD (australian dollar)<br>CAD (canadian dollar)<br>CHF (swiss franc)<br>DKK (danish krone)<br>EUR (euro)<br>GBP (british pound)<br>HKD (Hong Kong(China) dollar)<br>JPY (japanese yen)<br>NOK (norwegian krone)<br>SEK (swedish krona)<br>SGD (singapore dollar)<br>USD (united states dollar) |
    | $0.01 | one cent |
    | JPY 1.01 | one japanese yen and one sen |
    | £1.1 | one pound and ten pence |
    | €2.01 | two euros and one cent |
    | USD 1,000 | one thousand united states dollars |
    | 数字+量词+金额识别符<br>或<br>金额识别符+数字+量词 | 1.23 Tn RMB | one point two three trillion yuan | 支持的量词格式包括：<br>thousand<br>million<br>billion<br>trillion<br>Mil (million)<br>mil (million)<br>Bil (billion)<br>bil (billion)<br>MM (million)<br>Bn (billion)<br>bn (billion)<br>Tn (trillion)<br>tn (trillion)<br>K(thousand)<br>k (thousand)<br>M (million)<br>m (million) |
    | $1.2 K | one point two thousand dollars |

  - measure




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字+中文单位 | 2片 | 两片 | 支持常见中文单位及单位缩写。 |
    | 120公顷 | 一百二十公顷 |
    | 100多毫克 | 一百多毫克 |
    | 100来米 | 一百来米 |
    | 100余人 | 一百余人 |
    | 1厘米20毫米 | 一厘米二十毫米 |
    | 120.00平方公里 | 一百二十平方公里 |
    | 数字+单位缩写 | 120.56 cm² | 一百二十点五六平方厘米 |
    | 120 ㎡ 56 cm² | 一百二十平方米五十六平方厘米 |
    | 100 m 12 cm 6 mm | 一百米十二厘米六毫米 |
    | 范围 | 10~15 kg | 十至十五千克 |
    | 10.24~789.82亩 | 十点二四至七百八十九点八二亩 |
    | 10米~15米 | 十米至十五米 |
    | 10.24 cm~19.08 cm | 十点二四厘米至十九点零八厘米 |
    | 数字+单位+"/"+单位 | 10元/斤 | 十元每斤 |
    | 199~299元/件 | 一百九十九至二百九十九元每件 |
    | 299.99元/g~399.99元/g | 二百九十九点九九元每克至三百九十九点九九元每克 |
    | 其他默认读法 | 12扎 | 十二扎 |
    | 30 rm | 三十r m |
    | 4万万同胞 | 四万万同胞 |
    | 12.897微克 | 十二点八九七微克 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字+计量单位 | 1.0 kg | one kilogram | 支持的数字格式：整数、小数以及以逗号分隔的国际写法。<br>支持常见单位缩写。 |
    | 1,234.01 km | one thousand two hundred thirty four point zero one kilometres. |
    | 计量单位 | mm2 | square millimetre |

  - <say-as>常见符号读法如下表所示。




    | **符号** | **中文读法** | **英文读法** |
    | --- | --- | --- |



    |     |     |     |
    | --- | --- | --- |
    | **符号** | **中文读法** | **英文读法** |
    | ! | 叹号 | exclamation mark |
    | “ | 双引号 | double quote |
    | # | 井号 | pound |
    | $ | dollar | dollar |
    | % | 百分号 | percent |
    | & | and | and |
    | ‘ | 单引号 | left quote |
    | （ | 左括号 | left parenthesis |
    | ） | 右括号 | right parenthesis |
    | \* | 星 | asterisk |
    | + | 加 | plus |
    | , | 逗号 | comma |
    | - | 杠 | dash |
    | . | 点 | dot |
    | / | 斜杠 | slash |
    | ： | 零冒号 | solon |
    | ； | 分号 | semicolon |
    | < | 小于 | less than |
    | = | 等号 | equals |
    | > | 大于 | greater than |
    | ? | 问号 | question mark |
    | @ | at | at |
    | \[ | 左方括号 | left bracket |\
    | \ | 反斜线 | back slash |\
    | \] | 右方括号 | right bracket |
    | ^ | 脱字符 | caret |
    | \_ | 下划线 | underscore |
    | \` | 反引号 | back quote |
    | { | 左花括号 | left brace |
    | \| | 竖线 | vertical bar |
    | } | 右花括号 | right brace |
    | ~ | 波浪线 | tilde |
    | ！ | 叹号 | exclamation mark |
    | “ | 左双引号 | left double quote |
    | ” | 右双引号 | right double qute |
    | ‘ | 左单引号 | left quote |
    | ’ | 右单引号 | right quote |
    | （ | 左括号 | left parenthesis |
    | ） | 右括号 | right parenthesis |
    | ， | 逗号 | comma |
    | 。 | 句号 | full stop |
    | — | 杠 | em dash |
    | ： | 冒号 | colon |
    | ； | 分号 | semicolon |
    | ？ | 问号 | question mark |
    | 、 | 顿号 | enumeration comma |
    | … | 省略号 | ellipsis |
    | …… | 省略号 | ellipsis |
    | 《 | 左书名号 | left guillemet |
    | 》 | 右书名号 | right guillemet |
    | ￥ | 人民币符号 | yuan |
    | ≥ | 大于等于 | greater than or equal to |
    | ≤ | 小于等于 | less than or equal to |
    | ≠ | 不等于 | not equal |
    | ≈ | 约等于 | approximately equal |
    | ± | 加减 | plus or minus |
    | × | 乘 | times |
    | π | 派 | pi |
    | Α | 阿尔法 | alpha |
    | Β | 贝塔 | beta |
    | Γ | 伽玛 | gamma |
    | Δ | 德尔塔 | delta |
    | Ε | 艾普西龙 | epsilon |
    | Ζ | 捷塔 | zeta |
    | Θ | 西塔 | theta |
    | Ι | 艾欧塔 | iota |
    | Κ | 喀帕 | kappa |
    | ∧ | 拉姆达 | lambda |
    | Μ | 缪 | mu |
    | Ν | 拗 | nu |
    | Ξ | 克西 | ksi |
    | Ο | 欧麦克轮 | omicron |
    | ∏ | 派 | pi |
    | Ρ | 柔 | rho |
    | ∑ | 西格玛 | sigma |
    | Τ | 套 | tau |
    | Υ | 宇普西龙 | upsilon |
    | Φ | fai | phi |
    | Χ | 器 | chi |
    | Ψ | 普赛 | psi |
    | Ω | 欧米伽 | omega |
    | α | 阿尔法 | alpha |
    | β | 贝塔 | beta |
    | γ | 伽玛 | gamma |
    | δ | 德尔塔 | delta |
    | ε | 艾普西龙 | epsilon |
    | ζ | 捷塔 | zeta |
    | η | 依塔 | eta |
    | θ | 西塔 | theta |
    | ι | 艾欧塔 | iota |
    | κ | 喀帕 | kappa |
    | λ | 拉姆达 | lambda |
    | μ | 缪 | mu |
    | ν | 拗 | nu |
    | ξ | 克西 | ksi |
    | ο | 欧麦克轮 | omicron |
    | π | 派 | pi |
    | ρ | 柔 | rho |
    | σ | 西格玛 | sigma |
    | τ | 套 | tau |
    | υ | 宇普西龙 | upsilon |
    | φ | fai | phi |
    | χ | 器 | chi |
    | ψ | 普赛 | psi |
    | ω | 欧米伽 | omega |

  - <say-as>常见计量单位如下表所示。




    | **格式** | **类别** | **中文示例** | **英文示例** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **类别** | **中文示例** | **英文示例** |
    | 缩写 | 长度 | nm（纳米）、μm（微米）、 mm（毫米）、cm（厘米）、m（米）、km（千米）、ft（英尺）、in（英寸） | nm (nanometre), μm (micrometre), mm (millimetre), cm (centimetre), m (metre), km (kilometre), ft (foot), in (inch) |
    | 面积 | cm²（平方厘米）、㎡（平方米）、km²（平方千米）、SqFt（平方英尺） | cm² (square centimetre), ㎡ (square metre), km2 (square kilometre), SqFt (square foot) |
    | 体积 | cm³（立方厘米）、m³（立方米）、km³（立方千米）、mL（毫升）、L（升）、gallon（加仑） | cm³ (cubic centimetre), m³ (cubic metre), km3 (cubic kilometre), mL (millilitre), L (millilitre), gal (gallon) |
    | 重量 | μg（微克）、mg（毫克）、g（克）、kg（千克） | μg (microgram), mg (microgram), g (gram), kg (kilogram) |
    | 时间 | min（分）、sec（秒）、ms（毫秒） | min (minute), sec (second), ms (millisecond) |
    | 电磁 | μA（微安）、mA（毫安）、Ω（欧姆）、Hz（赫兹）、kHz（千赫兹）、MHz（兆赫兹）、GHz（吉赫兹）、V（伏）、kV（千伏）、kWh（千瓦时） | μA (microamp), mA (milliamp), Hz (hertz), kHz (kilohertz), MHz (megahertz), GHz (gigahertz), V (volt), kV (kilovolt), kWh (kilowatt hour) |
    | 声音 | dB（分贝） | dB (decibel) |
    | 气压 | Pa（帕）、kPa（千帕）、Mpa（兆帕） | Pa (pascal), kPa (kilopascal), MPa (megapascal) |
    | 其他常见单位 | 支持不限于上述类别的中文单位，例如“米”、“秒”、“美元”、“毫升每瓶”等。以及中文量词，例如“架”、“场”、“头”、“部”、“盆”等。 | 支持不限于上述类别的计量单位，例如 tsp (teaspoon), rpm (round per minute), KB (kilobyte), mmHg (milimetre of mercury) 等。 |
- 标签关系

<say-as>标签可以包括文本及<vhml/>。

- 示例

  - cardinal















    ```javascript
    <speak>
      <say-as interpret-as="cardinal">12345</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="cardinal">10234</say-as>
    </speak>
    ```

  - digits















    ```javascript
    <speak>
      <say-as interpret-as="digits">12345</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="digits">10234</say-as>
    </speak>
    ```

  - telephone















    ```javascript
    <speak>
      <say-as interpret-as="telephone">12345</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="telephone">10234</say-as>
    </speak>
    ```

  - name















    ```javascript
    <speak>
      她的曾用名是<say-as interpret-as="name">曾小凡</say-as>
    </speak>
    ```

  - address















    ```javascript
    <speak>
      <say-as interpret-as="address">富路国际1号楼3单元304</say-as>
    </speak>
    ```

  - id















    ```javascript
    <speak>
      <say-as interpret-as="id">myid_1998</say-as>
    </speak>
    ```

  - characters















    ```javascript
    <speak>
      <say-as interpret-as="characters">希腊字母αβ</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="characters">*b+3.c$=α</say-as>
    </speak>
    ```

  - punctuation















    ```javascript
    <speak>
      <say-as interpret-as="punctuation"> -./:;</say-as>
    </speak>
    ```

  - date















    ```javascript
    <speak>
      <say-as interpret-as="date">1000-10-10</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="date">10-01-2020</say-as>
    </speak>
    ```

  - time















    ```javascript
    <speak>
      <say-as interpret-as="time">5:00am</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="time">0500</say-as>
    </speak>
    ```

  - currency















    ```javascript
    <speak>
      <say-as interpret-as="currency">13,000,000.00RMB</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="currency">$1,000.01</say-as>
    </speak>
    ```

  - measure















    ```javascript
    <speak>
      <say-as interpret-as="measure">100m12cm6mm</say-as>
    </speak>
    ```

















    ```javascript
    <speak>
      <say-as interpret-as="measure">1,000.01kg</say-as>
    </speak>
    ```