### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) Android SDK

# Android SDK

更新时间：2026-02-26 21:01:58

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

下载安装

接口说明

SDK错误码

时序图说明

duplex

push2talk

tap2talk

常见问题

语音对话支持哪些LLM？

是否支持RAG？

本文介绍了如何使用阿里云智能语音服务提供的Android NUI SDK，包括SDK下载安装、关键接口及代码示例。

## 前提条件

- 已 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#2572188 "") 并获取项目Appkey。

语音对话的项目类型选择 **语音识别 \+ 语音合成 \+ 语音分析**，然后在 **服务管理与开通** 页面将其升级为商用版。

- 已 [获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token-in-the-console "")。


## **下载安装**

[下载SDK和示例代码](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241024/drwsvu/V0.4.11-02A-20241024_Android.tar.gz)。

**说明**

请下载后在样例初始化代码中替换您的阿里云账号信息、Appkey和Token才可运行。

| **类别** | **兼容范围** |
| --- | --- |

|     |     |
| --- | --- |
| **类别** | **兼容范围** |
| 系统 | 支持Android 4.0以上版本，API LEVEL 14。 |
| 架构 | armeabi-v7a，arm64-v8a，x86，x86\_64。 |

## **接口说明**

- **createConversation**：创建交互，设置回调。对应销毁接口为 **destroyConversation**。















```java
/**
* 初始化SDK，SDK为单例，请先释放后再次进行初始化。请勿在UI线程调用，可能会引起阻塞。
* @param callback：事件监听回调，参见下文具体回调。
* @param parameters：json string形式的初始化参数，参见下方说明或接口说明：
* @return：参见错误码
*/
public synchronized int createConversation(final INativeConvCallback callback);
```



其中INativeConvCallback类型包含如下回调：
  - **onConvEventCallback**：SDK事件回调。















    ```java
    /**
     * SDK主要事件回调
     * @param event：回调事件，可通过调用其中具体方法获得事件及相关信息。具体方法见下方ConvEvent
     */
    void onConvEventCallback(ConvEvent event);
    ```


    - ConvEvent方法列表：




      | **方法名** | **说明** |
      | --- | --- |



      |     |     |
      | --- | --- |
      | **方法名** | **说明** |
      | int getStatusCode(); | 获得状态码/错误码，详情请参见 [SDK错误码](https://help.aliyun.com/zh/isi/developer-reference/android-sdk-1#c4b037ae18nhn "")。 |
      | String getErrorMessage(); | 获得错误信息。 |
      | String getDialogId(); | 获得当前dialog\_id。 |
      | Constants.ConvEventType getEventType(); | 获得当前事件类型，详情请参见下方ConvEventCode **。** |

    - ConvEventCode：




      | **SDK事件名称** | **事件说明** |
      | --- | --- |



      |     |     |
      | --- | --- |
      | **SDK事件名称** | **事件说明** |
      | EVENT\_CONVERSATION\_STARTED | AI登场。会话任务成功启动，建连成功。 |
      | EVENT\_CONVERSATION\_FAILED | 会话任务发生错误，需要查看错误码及错误信息。收到此事件后需要根据错误信息判断如何处理，也可以使用此dialog\_id重新连接，继续会话。 |
      | EVENT\_COVERSATION\_COMPLETED | AI退场。任务成功完成，执行断连操作。 |
      | EVENT\_SENTENCE\_BEGIN | HUMAN开始说话。PushToTalk模式按键则触发此事件，TapToTalk和Duplex模式是用户开始说话触发此事件。 |
      | EVENT\_SENTENCE\_END | HUMAN说话结束。PushToTalk模式按键松开则触发此事件，TapToTalk和Duplex模式是用户说话结束触发此事件。 |
      | EVENT\_DATA\_OUTPUT\_STARTED | 开始播放服务端TTS数据。 |
      | EVENT\_DATA\_OUTPUT\_COMPLETED | 服务端TTS数据合成完成。 |
      | EVENT\_INTERRUPT\_ACCEPTED | AI（服务端）接收按键请求（如打断）。 |
      | EVENT\_INTERRUPT\_DENIED | AI（服务端）拒绝按键请求（如打断）。 |
      | EVENT\_VOICE\_INTERRUPT\_ACCEPTED | AI（服务端）接收语音请求（如打断）。 |
      | EVENT\_VOICE\_INTERRUPT\_DENIED | AI（服务端）拒绝语音请求（如打断）。 |
      | EVENT\_HUMAN\_SPEAKING\_DETAIL | ASR识别结果。 |
      | EVENT\_RESPONDING\_DETAIL | 大模型返回的结果。 |
  - **onConvStateChangedCallback**：SDK状态回调。















    ```java
    /**
     * SDK状态回调
     * @param state：回调事件，可通过调用其中具体方法获得事件及相关信息。具体方法见下方DialogState
     */
    void onConvStateChangedCallback(int state);

    public enum DialogState {
        DIALOG_IDLE(0),
        DIALOG_LISTENING(1),
        DIALOG_RESPONDING(2),
        DIALOG_THINKING(3),
    }
    ```



    DialogState：AI（服务端）处于的状态。




    | **名称** | **说明** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **名称** | **说明** |
    | DIALOG\_IDLE | 当前处于空闲未工作状态。 |
    | DIALOG\_LISTENING | AI（服务端）处于听状态，接收用户输入数据（如MIC音频数据）。 |
    | DIALOG\_RESPONDING | AI（服务端）处于反馈状态，发送AI的数据（如TTS音频数据）。 |
    | DIALOG\_THINKING | AI（服务端）处于思考阶段。 |

  - **onConvDataReceivedCallback**：收到返回的结果数据。















    ```java
    /**
     * 获得返回数据(如音频)回调
     * @param buffer：返回的数据
     */
    int onConvDataReceivedCallback(byte[] buffer);
    ```

  - **onConvSoundLevelCallback**：获得的输入音频的音量级别。















    ```java
    /**
     * 计算输入音频的音量级别，从低到高0-100，以及对应的db值
     * @param level：音频的音量级别，从低到高0-100
     * @param db：音频db值，-160 - 0
     */
    void onConvSoundLevelCallback(int level, float db);
    ```

  - **onConvEventTrackCallback**：获得关键埋点信息日志。















    ```java
    /**
     * 日志埋点输出函数
     * @param level：输出日志的级别, 详见 ConvLogLevel
     * @param log：关键埋点信息日志
     */
    void onConvEventTrackCallback(int level, String log);
    ```
- **destroyConversation**：销毁交互。对应创建接口为 **createConversation**。















```java
/**
*
* @return：参见错误码
*/
public synchronized int destroyConversation();
```

- **connect**：与服务端建立链接。















```java
/**
* 初始化SDK并连接AI服务。
* @param parameters：json string形式的初始化参数，参见下方说明或接口说明：
* @return：参见错误码
*/
public synchronized int connect(String parameters);
```



参数设置：




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| appkey | String | 是 | 项目Appkey。详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#2572188 "")。 |
| token | String | 是 | 鉴权信息。 |
| url | String | 是 | 域名地址。生产环境网关URL：<br>`wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1` |
| workspace | String | 是 | 资源为resources目录下的相关文件。<br>例如以下示例工程中，通过拷贝aar包的资源文件，获得资源文件所处的路径，即为workspace。<br>```<br>ConvUtils.copyAssetsData(this);<br>ConvUtils.getModelPath(this);<br>``` |
| dialog\_id | String | 否 | 对话ID，空代表新的对话，传入则代表继续通话。格式为32位随机字符串。 |
| mode | String | 否 | 运行模式。取值如下：<br>  - duplex（默认）：在tap2talk的模式上提供语音打断能力，端侧具备移动端AEC算法处理能力。<br>    <br>  - tap2talk：语音起点由端侧VAD给出。<br>    <br>  - push2talk：按键语音交互，语音的起点和尾点由按键时间给出。 |
| user\_agent | String | 否 | 客户端userAgent，用来记录和鉴权。 |
| debug\_path | String | 否 | 日志和音频文件存储目录，不设置则在workspace下创建debug目录。 |
| save\_log | Boolean | 否 | 是否存储日志，默认false。 |
| save\_wav | Boolean | 否 | 是否存储音频，默认false。 |
| log\_level | String | 否 | 日志级别，取值范围：<br>  - verbose<br>    <br>  - debug<br>    <br>  - info（默认）<br>    <br>  - warn<br>    <br>  - warning<br>    <br>  - error |
| device\_id | String | 否 | 设备唯一标识#utdid。 |
| dialog\_attributes | JSONObject | 是 | AI角色属性。 |
| dialog\_attributes.model\_id | String | 是 | 大模型ID（枚举，给出支持的列表）。 |
| dialog\_attributes.prompt | String | 是 | 大模型prompt，最长800个字符。 |
| dialog\_attributes.voice | String | 是 | TTS音色（成品音色，比如 longxiaochun，或者客户克隆voiceName， 补充权限校验）。 |
| dialog\_attributes.voice\_detection\_enabled | Boolean | 否 | 是否开启语音检测，去掉开始和结束的静音，并且当句尾静音长度超过X（服务端控制）的时候认为指令结束。<br>默认为true，push2talk模式可设为false。 |
| advanced\_attributes | JSONObject | 否 | 高级属性。 |
| advanced\_attributes.context\_depth | String | 否 | 控制用户问题调大模型服务时附加多少历史对话，取值：<br>  - 0：表示不附加历史。<br>    <br>  - n：大于0的整数表示附加n轮问答历史，范围 \[1, 10\]。<br>    <br>  - all（默认）：表示附加本次通话中所有历史。 |
| advanced\_attributes.enable\_search | String | 否 | 是否开启LLM搜索增强，默认为false（不开启）。 |
| advanced\_attributes.xingchen | String | 否 | model\_id为xingchen-model时表示调用星辰的模型，必传此内容。JSON格式字符串，JSON内容为：<br>`"{\"character_id\":\"xxxxx\",\"user_id\":\"xxxx\"}"`<br>character\_id和user\_id是星辰的参数，必传。 |

- **disconnect**：断开链接。















```java
/**
* @param force：true则内部快速关闭websocket，false则内部进行stop再disconnect.
* @return：参见错误码
*/
public synchronized int disconnect(boolean force);
```

- **interrupt**：打断交互，使AI进入听状态。在PushToTalk模式下，在AI说和AI思考状态下打断返回空闲状态。















```java
/**
* 打断交互，使AI进入听状态。
* @return：返回打断结果，允许打断返回SUCCESS,拒绝打断返回REQUEST_DENIED
*/
public synchronized int interrupt();
```

- **sendAudioData**：推送实时采集的音频数据。















```java
/**
* @return：参见错误码
*/
public synchronized int sendAudioData(byte[] buffer, int len);
```

- **sendRefData**：推送参考音频数据，在音频数据送给播放器时推送。















```java
/**
* @return：参见错误码
*/
public synchronized int sendRefData(byte[] buffer, int len);
```

- **sendResponseData**：Listening/Idle状态下，通知服务端与用户主动交互，可以直接把上传的文本转换为语音下发，也可以上传文本调用大模型，返回的结果再转换为语音下发。















```java
/**
* @param parameters：json string形式的初始化参数，参见下方说明或接口说明：
* @return：参见错误码
*/
public synchronized int sendResponseData(String parameters);
```



参数设置：




| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| type | String | 是 | 服务应该采取的交互类型。取值如下：<br>  - transcript：表示直接把文本转语音。<br>    <br>  - prompt：表示把文本送大模型回答。 |
| text | String | 是 | 要处理的文本。 |

- **updateMessage**：更新参数（例如rtc、p2t）。















```java
/**
* 更新其他服务的参数。
* @param parameters：json string形式的初始化参数，参见下方说明或接口说明：
* @return：参见错误码
*/
public synchronized int updateMessage(String parameters);
```


  - RTC相关命令

    RTC INIT：















    ```java
    {
    	"type": "rtc",
    	"action": "INIT"
    }
    ```



    RTC设置：















    ```java
    {
    	"type": "rtc",
    	"from_state": "2",
    	"seq_id": "1",
    	"to_state": "0"
    }
    ```

  - p2t模型相关命令

    p2t按下按钮时更新agent\_chat，可填写zh、en、ja、ko。















    ```java
    {"type":"update_nls_parameters","agent_chat":{"language_type":"zh","answer_language_type":"en"}}
    # 或
    {"type":"update_nls_parameters","SendSpeech_agent_chat":{"language_type":"zh","answer_language_type":"en"}}

    # SendSpeech_agent_chat 优先级高于 agent_chat
    ```

  - 更新其它参数命令。















    ```java
    {"type":"update_nls_parameters","avatar":{}}

    {"type":"update_nls_parameters","client_info":{}}

    {"type":"update_nls_parameters","agent_chat":{}}

    {"type":"update_nls_parameters","SendSpeech_extra_info":"{\"prompt\":\"123\",\"sessionId\":\"456\"}"}
    ```

  - 更新参数万能方法

    用户自定义服务端交互参数，具体说明如下：




    | **参数字段** | **说明** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **参数字段** | **说明** |
    | `"type": "update_custom_nls_parameters"` | 表示使用用户自定义参数功能。 |
    | `nls_rule` | 规定参数在协议中添加的位置，例如：<br>    - `"payload": ["Start_custom2", "SendSpeech_custom3"]`表示在向服务端发送"Start"协议时，payload中添加参数`"custom2":{"test":2}`<br>      <br>    - `"header": ["Start_custom1"]`表示在向服务端发送"Start"协议时，header中添加参数`"custom1":{"test":1}`。 |

















    ```java
    {
    	"type": "update_custom_nls_parameters",
    	"nls_rule": {
    		"header": ["Start_custom1"],
    		"payload": ["Sart_custom2", "SendSpeech_custom3"],
    		"context": ["Stop_custom4"]
    	},
    	"nls_params": {
    		"Start_custom1": {
    			"test": 1
    		},
    		"Sart_custom2": {
    			"test": 2
    		},
           "SendHumanSpeech_custom3": {
    			"test": 3
    		},
    		"Stop_custom4": {
    			"test": 4
    		}
    	}
    }
    ```
- **setAction**：需要有一个音频（播放）开始/结束事件告知到SDK。















```java
/**
* @return：参见错误码
*/
public synchronized int setAction(ConvConstants.ConvAppAction action);

public enum ConvAppAction {
      MIC_STARTED,
      MIC_STOPPED,
      PLAYER_STARTED,
      PLAYER_STOPPED,
      ENABLE_VOICE_INTERRUPT,
      DISABLE_VOICE_INTERRUPT,
      VOICE_MUTE,
      VOICE_UNMUTE,
      START_HUMAN_SPEECH,   /* 仅在push2talk模式有效, 表示用户开始说话 */
      STOP_HUMAN_SPEECH,    /* 仅在push2talk模式有效, 表示用户说话完毕 */
      CANCEL_HUMAN_SPEECH,  /* 仅在push2talk模式有效, 表示用户说话取消 */
      PULL_OUT_HEADPHONES;
}
```


  - ConvAppAction




    | **名称** | **说明** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **名称** | **说明** |
    | MIC\_STARTED | MIC开始工作。 |
    | MIC\_STOPPED | MIC停止录音。 |
    | PLAYER\_STARTED | 开始播放。 |
    | PLAYER\_STOPPED | 播放完毕。<br>**说明**<br>需确保播放器中缓存数据全部播放完毕后给出，否则会导致自打断或播放数据进入ASR。 |
    | ENABLE\_VOICE\_INTERRUPT | 开启语音打断功能。 |
    | DISABLE\_VOICE\_INTERRUPT | 关闭语音打断功能。 |
    | VOICE\_MUTE | 语音静音。若正在AI听阶段，则主动告知AI，用户已经说完话。 |
    | VOICE\_UNMUTE | 语音静音关闭。 |
    | START\_HUMAN\_SPEECH | 仅在push2talk模式有效, 表示用户开始说话。 |
    | STOP\_HUMAN\_SPEECH | 仅在push2talk模式有效，表示用户说话完毕。 |
    | CANCEL\_HUMAN\_SPEECH | 仅在push2talk模式有效，表示用户说话取消。 |
    | PULL\_OUT\_HEADPHONES | 拔耳机时调用，用于优化耳机切换的回声消除效果。 |

  - p2t模式按下按键代码示例。















    ```java
    // 设置语种，即设置参数agent_chat
    JSONObject root_obj = new JSONObject();
    JSONObject agent_chat_obj = new JSONObject();
    agent_chat_obj.put("language_type", "zh");
    agent_chat_obj.put("answer_language_type", "en");
    root_obj.put("SendHumanSpeech_agent_chat", agent_chat_obj);
    root_obj.put("type", "update_nls_parameters");

    conv_instance.updateMessage(root_obj.toString());

    conv_instance.setAction(ConvConstants.ConvAppAction.START_HUMAN_SPEECH);
    ```

  - p2t模式松开按键代码示例。















    ```java
    conv_instance.setAction(ConvConstants.ConvAppAction.STOP_HUMAN_SPEECH);
    ```

  - p2t模式取消用户说话代码示例。















    ```java
    conv_instance.setAction(ConvConstants.ConvAppAction.CANCEL_HUMAN_SPEECH);
    ```
- **getState**：获得当前各种状态。















```java
/**
* @param param：
* @return：根据ConvStateType，返回对应事件的枚举值的int值，需要转换对应枚举
*/
public synchronized int getState(ConvConstants.ConvStateType state);

public enum ConvStateType {
      DIALOG_STATE,
      MIC_STATE,
      PLAYER_STATE;
}

/**
* 返回对应枚举
*/
public enum DialogState {
      DIALOG_IDLE(0),
      DIALOG_LISTENING(1),
      DIALOG_RESPONDING(2),
      DIALOG_THINKING(3);
}

public enum ConvAppAction {
      MIC_STARTED,
      MIC_STOPPED,
      PLAYER_STARTED,
      PLAYER_STOPPED;
}
```


  - ConvStateType




    | **名称** | **说明** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **名称** | **说明** |
    | DIALOG\_STATE | 对话（AI）当前状态，枚举值为ConvConstants.DialogState。 |
    | MIC\_STATE | MIC当前状态，枚举值为ConvConstants.ConvAppAction。 |
    | PLAYER\_STATE | PLAYER当前状态，枚举值为ConvConstants.ConvAppAction。 |

  - DialogState




    | **名称** | **说明** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **名称** | **说明** |
    | DIALOG\_IDLE | 当前处于空闲未工作状态。 |
    | DIALOG\_LISTENING | AI（服务端）处于听状态，接收用户输入数据（如MIC音频数据）。 |
    | DIALOG\_RESPONDING | AI（服务端）处于反馈状态，发送AI的数据（如TTS音频数据）。 |
    | DIALOG\_THINKING | AI（服务端）处于思考阶段。 |

  - ConvAppAction




    | **名称** | **说明** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **名称** | **说明** |
    | MIC\_STARTED | MIC开始工作。 |
    | MIC\_STOPPED | MIC停止录音。 |
    | PLAYER\_STARTED | 开始播放。 |
    | PLAYER\_STOPPED | 播放完毕。 |

## **SDK错误码**

| **状态码** | **状态消息** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **状态码** | **状态消息** | **说明** |
| 11 | MEM\_ALLOC\_ERROR | 内存分配失败。 |
| 50 | INIT\_FAILED | 初始化为不支持的模式。 |
| 51 | NOT\_CONNECTED | 链接失败，如联网超时等。 |
| 52 | ENGINE\_NULL | 交互引擎未创建，不可使用。 |
| 53 | ILLEGAL\_PARAM | 设置参数非法。 |
| 54 | ILLEGAL\_INIT\_PARAM | 初始化参数非法。 |
| 55 | INVALID\_STATE | 当前交互状态无法调用此接口。 |
| 56 | HAS\_INVOKED | 已经调用了此接口。 |
| 57 | NOT\_CREATE\_CONVERSATION | 还未创建会话即未调用createConversation就开始操作。 |
| 58 | SKIP\_SEND\_DATA | 当前交互状态忽略此次音频。 |
| 59 | SEND\_DATA\_FAILED | 发送音频失败。 |
| 60 | INVALID\_AUDIO\_DATA | 无效音频。 |
| 61 | STOP\_FAILED | stop()失败，如超时。 |
| 62 | CANCEL\_FAILED | cancel()失败，如超时。 |
| 63 | INVOKE\_TIMEOUT | 接口调用超时。 |
| 64 | REQUEST\_DENIED | 打断请求拒绝。 |
| 65 | REQUEST\_ACCEPTED | 允许打断请求。 |
| 100 | INTERNAL\_ENGINE\_INIT\_FAILED | 内部引擎初始化失败，常发生于connect()时。 |
| 101 | INTERNAL\_ENGINE\_SET\_PARAM\_FAILED | 内部引擎配置参数失败。 |
| 111 | INTERNAL\_ENGINE\_RESOURCE\_NOT\_FOUND | 内部引擎因为找不到资源文件而初始化失败，请检查资源文件是否完备，且是最新版本 |
| 112 | INTERNAL\_ENGINE\_VAD\_INVALID\_PARAM | 内部vad引擎的初始化参数非法。 |
| 113 | INTERNAL\_ENGINE\_VAD\_INVALID\_STATE | 内部vad引擎运行处于异常状态，比如vad已经释放。 |
| 114 | INTERNAL\_ENGINE\_VAD\_PROCESS\_FAILED | 内部VAD引擎在异常状态送入数据。 |
| 115 | INTERNAL\_ENGINE\_VAD\_CREATE\_FAILED | 内部vad引擎初始化失败，一般是由于资源文件缺失或者不兼容的旧版本。 |
| 200 | EMPTY\_CONV\_EVENT | 非法ConvEvent。 |
| 201 | INVALID\_CONV\_EVENT\_MSG\_TYPE | 非法的ConvEvent事件类型。 |
| 301 | SERVER\_NOT\_ACCESS | 链接服务端失败，比如服务端不可链接，DNS不可解析等。 |
| 311 | JSON\_FORMAT\_ERROR | 接收到服务端返回的消息不符合JSON格式。 |
| 312 | SSL\_ERROR | SSL失败，比如握手失败。 |
| 313 | SSL\_CONNECT\_FAILED | SSL链接失败。 |
| 351 | NLS\_INVOKE\_TIMEOUT | 向服务端发送请求操作超时。 |
| 352 | NLS\_START\_FAILED | 向服务端发送建立会话请求失败，常为网络问题。 |
| 353 | NLS\_STOP\_FAILED | 向服务端发送停止会话请求失败，常为网络问题。 |
| 354 | NLS\_CANCEL\_FAILED | 向服务端发送停止会话请求失败，常为网络问题。 |
| 355 | NLS\_START\_INBOUND\_FAILED | 向服务端发送启动对话任务请求失败，常为网络问题。 |
| 358 | NLS\_CANCEL\_BOUND\_FAILED | 向服务端发送停止对话任务请求失败，常为网络问题。 |
| 359 | NLS\_SET\_PARAMS\_FAILED | 设置请求参数错误，比如设置token无效。 |
| 360 | NLS\_SEND\_AUDIO\_FAILED | 向服务端发送音频数据失败，常为网络问题 |

## **时序图说明**

### **duplex**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7177512771/CAEQUBiBgMDe.Kr4lBkiIDY0YTg0MTcwNzg4NzRmMzA4YmZmZjExOTk3ZDBhNDhj4705034_20241012144303.065.svg)

### **push2talk**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7177512771/CAEQUBiBgMC2q634lBkiIDI5N2ZjN2Q3NTEzNjRjNDhhNzAwZjZhNjRjMjEzYTA24705034_20241012144303.065.svg)

### **tap2talk**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7177512771/CAEQUBiBgMDAp574lBkiIDY3NDRlMGMzNGE1ODQ1MjI4MzY0MzhkNjM0YTFlYzM24705034_20241012144303.065.svg)

## **常见问题**

### **语音对话支持哪些LLM？**

目前只支持千问大模型（包括Qwen\_turbo、Qwen\_plus等），不支持替换其他大模型。千问大模型支持列表，详情请参见 [千问大语言模型介绍](https://help.aliyun.com/zh/model-studio/what-is-qwen-llm "")。

### **是否支持RAG？**

支持。如果您有业务需求，请 [提交工单](https://smartservice.console.aliyun.com/service/create-ticket) 进行咨询。