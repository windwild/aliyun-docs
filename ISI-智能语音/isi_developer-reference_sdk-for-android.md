### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)[离线语音合成](https://help.aliyun.com/zh/isi/developer-reference/offline-speech-synthesis/)Android SDK

# Android SDK

更新时间：2025-11-06 01:26:19

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-11)[下一篇：iOS SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-ios-3)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

下载安装

SDK关键接口

调用步骤

代码示例

常见问题

使用离线语音合成Android SDK，语音播报时出现不合理断句，该如何处理？

调用Android SDK时，手机报错提示“audio recorder not init”。

在模拟器上运行下载的Android程序，程序出现闪退现象，是什么原因？

int ret = nui\_instance.initialize(this, genInitParams(assets\_path,debug\_path), Constants.LogLevel.LOG\_LEVEL\_VERBOSE, true)。在该段代码中，录音权限是打开的，但代码仍然报错240021。

本文介绍了如何使用阿里云离线语音合成服务提供的Android NUI SDK，包括下载安装SDK和语音包、SDK关键接口及代码示例。

## 前提条件

- 阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-11#topic-2040874 "")。

- 已获取项目Appkey，详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#2572188 "")。

- 已获取AccessKey ID和 AccessKey Secret，详情请参见 [开通服务](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-1917889 "")。


## 下载安装

1. [移动端SDK选择与下载](https://help.aliyun.com/zh/isi/sdk-selection-and-download "")。



**重要**





下载后在样例初始化代码中替换您的阿里云账号信息、Appkey才可运行。

2. 下载语音包，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-11#topic-2040874 "") 中的语音包列表。



**重要**





SDK和语音包是完全独立的，下载SDK后并不能直接使用，需要下载语音包，并设置语音包存放路径。

3. 解压ZIP包，在`app/libs`目录下获取AAR格式的SDK包。若需要Android CPP接入方式，则可在ZIP包的android\_libs和android\_include中获得动态库和头文件。

4. 使用Android Studio打开此工程。其中语音合成示例代码为TtsLocalActivity.java文件。


## SDK关键接口

- **tts\_initialize**：初始化SDK。















```java
/**
* 初始化SDK，离线合成暂不支持多实例，请先释放后再次进行初始化。请勿在UI线程调用，可能会引起阻塞。
* 初始化是耗时操作，不需要合成一个任务就进行该操作；在启动和退出时进行一次即可。
* @param callback：事件监听回调，参见下文具体回调。
* @param ticket：json string形式的初始化参数，参见下方说明或接口说明：https://help.aliyun.com/document_detail/204185.html。
* @param level：log打印级别，值越小打印越多。
* @param save_log：是否保存log为文件，存储目录为ticket中的debug_path字段值。注意，log文件无上限，请注意持续存储导致磁盘存满。
* @return：参见错误码：https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int tts_initialize(INativeTtsCallback callback,
                                         String ticket,
                                         final Constants.LogLevel level,
                                         boolean save_log)；
```



INativeTtsCallback类型包含如下回调：


  - onTtsEventCallback：SDK事件回调。















    ```java
    /**
     * 事件回调
     * @param event：回调事件，参见如下事件列表。
     * @param task_id：请求的任务ID。
     * @param ret_code：参见错误码，出现TTS_EVENT_ERROR事件时有效，可查阅https://help.aliyun.com/document_detail/459864.html。
     */
    void onTtsEventCallback(TtsEvent event, String task_id, int ret_code);
    ```



    事件列表：




    | 名称 | 说明 |
    | --- | --- |



    |     |     |
    | --- | --- |
    | 名称 | 说明 |
    | TTS\_EVENT\_START | 语音合成开始，准备播放。 |
    | TTS\_EVENT\_END | 语音合成结束，合成数据已全部抛出，但并不表示播放结束。 |
    | TTS\_EVENT\_CANCEL | 取消语音合成。 |
    | TTS\_EVENT\_PAUSE | 语音合成暂停。 |
    | TTS\_EVENT\_RESUME | 语音合成恢复。 |
    | TTS\_EVENT\_ERROR | 语音合成发生错误。可通过getparamTts("error\_msg")获得详细错误消息。 |

  - onTtsDataCallback：合成数据回调。















    ```java
    /**
     * @param info：使用时间戳功能时，返回JSON格式的时间戳结果。
     * @param info_len：info字段的数据长度，暂不使用。
     * @param data：合成的音频数据，写入播放器。
     */
    void onTtsDataCallback(String info, int info_len, byte[] data);
    ```

  - onTtsLogTrackCallback：SDK内部日志回调（2.6.4版本新增）。















    ```java
    /**
     * SDK内部日志回调。若Override此回调，则SDK内部符合日志级别的日志将通过此回调送出。若多实例都Override此回调，则所有回调都会接收到SDK的日志信息。
     * @param level: 大于此日志级别的SDK内部日志将通过此回调送出
     * @param log: 具体的日志内容
     */
    void onTtsLogTrackCallback(Constants.LogLevel level, String log);
    ```


其中，ticket内容参数说明、生成示例参见下方代码示例，更多参数设置请查看接口说明。

| **参数** | **类型** | **是否必选** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **说明** |
| workspace | String | 是 | 工作目录路径，SDK从该路径读取配置文件。需要有读写权限。 |
| app\_key | String | 是 | 管控台创建项目的appkey。 |
| ak\_id | String | 是 | 阿里云账号的AccessKey中的AccessKey ID，用于标识用户。或为阿里云STS（Security Token Service）的AccessKey ID。具体可见代码示例中账号鉴权相关说明。 |
| ak\_secret | String | 是 | 阿里云账号的AccessKey中的AccessKey Secret，用于验证用户的密钥。AccessKey Secret必须保密。或为阿里云STS（Security Token Service）的AccessKey Secret。具体可见代码示例中账号鉴权相关说明。 |
| token | String | 否 | 访问令牌（Access Token）。若使用阿里云账号的AccessKey，则使用此参数token。若使用阿里云STS（Security Token Service）的AccessKey，则使用sts\_token。具体可见代码示例中账号鉴权相关说明。 |
| sts\_token | String | 否 | 临时安全令牌（STS Token）。若使用阿里云STS（Security Token Service）的AccessKey，则使用此参数sts\_token。若使用阿里云账号的AccessKey，则使用token。具体可见代码示例中账号鉴权相关说明。 |
| device\_id | String | 是 | 用户层面的账户号。此为扣费依据，若device\_id重复则会被认为非法ID，导致离线语音合成无法工作。若device\_id随机变化，则会出现重复计费的情况。请保证此device\_id唯一性且不会变化。 |
| mode\_type | String | 是 | 设置成离线语音合成模式，语音合成必须设置成“0”，这个设置很重要, 遗漏会导致无法运行 |

- **setparamTts**：设置参数。















```java
/**
* 以键值对形式设置参数, 参见接口说明:https://help.aliyun.com/document_detail/204185.html
* @param param：参数名，参见接口说明。
* @param value：参数值，参见接口说明。
* @return：参见错误码:https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int setparamTts(String param, String value);
```

- **getparamTts**：获取参数。















```java
/**
* 获取参数值
* @param param：参数名，参考接口说明:https://help.aliyun.com/document_detail/204185.html。
* @return：参数值。
*/
public String getparamTts(String param);
```

- **startTts**：开始合成。















```java
/**
* 开始合成任务
* @param priority：任务优先级，请使用"1"。
* @param taskid：任务ID，可传入32个字节的uuid，或传入空内容由SDK自动生成。
* @param text：播放的文本内容。
* @return：参见错误码:https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int startTts(String priority, String taskid, String text);
```

- **cancelTts**：取消合成。















```java
/**
* 取消合成任务
* @param taskid：传入想要停止的任务ID，如果为空则取消所有任务。
* @return：参见错误码:https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int cancelTts(String taskid);
```

- **pauseTts**：暂停合成。















```java
/**
* 暂停合成任务
* @return：参见错误码:https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int pauseTts();
```

- **resumeTts**：恢复合成。















```java
/**
* 恢复暂停的任务
* @return：参见错误码:https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int resumeTts();
```

- **tts\_release**：释放SDK资源。















```java
/**
* 释放SDK
* @return：参见错误码:https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int tts_release();
```


## 调用步骤

1. 初始化SDK和播放组件。

2. 根据业务需求设置参数。

3. 调用startTts进行播放。

4. 在合成数据回调中，将数据写入播放器进行播放，建议使用流式播放。

5. 收到语音合成结束的回调。


## 代码示例

1. 语音合成初始化。















```java
//设置默认目的地路径最下级目录名字
// 比如设置当前 /data/user/0/mit.alibaba.nuidemo/files/asr_my
// 未调用此接口, 则默认为 /data/user/0/mit.alibaba.nuidemo/files/asr_my
CommonUtils.setTargetDataDir("asr_my");

//这里获得当前nuisdk.aar中assets可以搬运的默认目的地路径,
// 比如 /data/user/0/mit.alibaba.nuidemo/files/asr_my
path = CommonUtils.getModelPath(this);
Log.i(TAG, "workpath:" + path);

//这里主动调用完成SDK配置文件的拷贝目的地为CommonUtils.getModelPath(this);
// 比如当前为 /data/user/0/mit.alibaba.nuidemo/files/asr_my
if (CommonUtils.copyTtsAssetsData(this)) {
       Log.i(TAG, "copy assets data done");
} else {
       Log.e(TAG, "copy assets failed");
       ToastText("从aar的assets拷贝资源文件失败, 请检查资源文件是否存在, 详情可通过日志确认。");
       return;
}
// 注意: 比如鉴权文件为 /data/user/0/mit.alibaba.nuidemo/files/asr_my/tts/ttset.bin
// 切勿覆盖和删除asr_my内文件

//SDK初始化
NativeNui nui_tts_instance = new NativeNui(Constants.ModeType.MODE_TTS);
int ret = nui_tts_instance.tts_initialize(new INativeTtsCallback() {}, genInitParams(path), Constants.LogLevel.LOG_LEVEL_VERBOSE, true);
```



其中，genInitParams生成为String JSON字符串，包含资源目录和用户信息。其中用户信息包含如下字段。



**说明**





   - 精品版sdk\_code为software\_nls\_tts\_offline

   - 普通版sdk\_code为software\_nls\_tts\_offline\_standard


```java
/**
 * ticket生成示例，详见Demo工程中代码示例
 */
private String genInitParams(String workpath) {
    String str = "";
    try {
        //郑重提示:
        //  语音交互服务需要先准备好账号，并开通相关服务。具体步骤请查看：
        //    https://help.aliyun.com/zh/isi/getting-started/start-here
        //
        //原始账号:
        //  账号(子账号)信息主要包括AccessKey ID(后续简称为ak_id)和AccessKey Secret(后续简称为ak_secret)。
        //  此账号信息一定不可存储在app代码中或移动端侧，以防账号信息泄露造成资费损失。
        //
        //STS临时凭证:
        //  由于账号信息下发给客户端存在泄露的可能，阿里云提供的一种临时访问权限管理服务STS(Security Token Service)。
        //  STS是由账号信息ak_id和ak_secret，通过请求生成临时的sts_ak_id/sts_ak_secret/sts_token
        //  (为了区别原始账号信息和STS临时凭证, 命名前缀sts_表示STS生成的临时凭证信息)
        //什么是STS：https://help.aliyun.com/zh/ram/product-overview/what-is-sts
        //STS SDK概览：https://help.aliyun.com/zh/ram/developer-reference/sts-sdk-overview
        //STS Python SDK调用示例：https://help.aliyun.com/zh/ram/developer-reference/use-the-sts-openapi-example
        //
        //账号需求说明:
        //  若使用离线功能(离线语音合成、唤醒), 则必须app_key、ak_id和ak_secret，或app_key、sts_ak_id、sts_ak_secret和sts_token
        //  若使用在线功能(语音合成、实时转写、一句话识别、录音文件转写等), 则只需app_key和token
        JSONObject initObject = Auth.getTicket(Auth.GetTicketMethod.GET_STS_ACCESS_FROM_SERVER_FOR_OFFLINE_FEATURES);
        if (!object.containsKey("token")) {
            Log.e(TAG, "Cannot get token!!!");
        }

        object.put("url", "wss://nls-gateway.cn-shanghai.aliyuncs.com:443/ws/v1"); // 默认
        //工作目录路径，SDK从该路径读取配置文件
        object.put("workspace", workpath); // 必填, 且需要有读写权限

        initObject.put("mode_type", Constants.TtsModeTypeLocal); // 必填

        // 特别说明: 鉴权所用的id是由以下device_id，与手机内部的一些唯一码进行组合加密生成的。
        //   更换手机或者更换device_id都会导致重新鉴权计费。
        //   此外, 以下device_id请设置有意义且具有唯一性的id, 比如用户账号(手机号、IMEI等),
        //   传入相同或随机变换的device_id会导致鉴权失败或重复收费。
        object.put("device_id", "empty_device_id"); // 必填, 推荐填入具有唯一性的id, 方便定位问题

        str = object.toString();
    } catch (JSONException e) {
        e.printStackTrace();
    }
    Log.i(TAG, "UserContext:" + str);
    return str;
}
```

2. 根据需求设置参数。















```java
//设置本地发音人，如下载的aicheng语音包放在目录/sdcard/idst/目录下，那么命令为”/sdcard/idst/aicheng“
//  语音包和SDK是隔离的，需要先设置语音包
//  如果切换发音人：SDK可使用语音包与鉴权账号相关，由购买时获得的语音包使用权限决定
//  如已经购买aijia，按下边方式调用后，发音人将切为aijia
//  语音包下载地址：https://help.aliyun.com/document_detail/204185.html
//  语音包试听：https://www.aliyun.com/activity/intelligent/offline_tts
//  特别说明：离线语音合成的发音人, 并不一定也存在于在线语音合成；同理, 在线语音合成的发音人, 并不一定也存在于离线语音合成

//aar中的资源目录中自带了一个发音人aijia, /data/user/0/mit.alibaba.nuidemo/files/asr_my/tts/voices/aijia
String fullName = workspace + "/tts/voices/" + mFontName;

//切换发音人：一定要输入全路径名称
Log.i(TAG, "use extend_font_name:" + fullName);
ret = nui_tts_instance.setparamTts("extend_font_name", fullName);
if (ret != Constants.NuiResultCode.SUCCESS) {
       Log.e(TAG, "setparamTts extend_font_name " + fullName + " failed, ret:" + ret);
       String errmsg =  nui_tts_instance.getparamTts("error_msg");
       return ret;
}

//  设置发音人对应的语音合成采样率, 设置后也请设置播放器的对应采样率， 否则无法播放出正常音频。
nui_tts_instance.setparamTts("sample_rate", "16000");

// 调整语速
// nui_tts_instance.setparamTts("speed_level", "1");
// 调整音调
// nui_tts_instance.setparamTts("pitch_level", "0");
// 调整音量
// nui_tts_instance.setparamTts("volume", "1.0");
```

3. 启动语音合成。















```java
nui_tts_instance.startTts("1", "", ttsText);
```

4. 回调处理。

   - onTtsEventCallback：语音合成事件回调，根据语音合成状态控制播放器。















     ```java
     public void onTtsEventCallback(INativeTtsCallback.TtsEvent event, String task_id, int ret_code) {
         Log.i(TAG, "tts event:" + event + " task id " + task_id + " ret " + ret_code);
         if (event == INativeTtsCallback.TtsEvent.TTS_EVENT_START) {
             mAudioTrack.play();
             Log.i(TAG, "start play");
         } else if (event == INativeTtsCallback.TtsEvent.TTS_EVENT_END) {
             /*
              * 提示: TTS_EVENT_END事件表示TTS已经合成完并通过回调传回了所有音频数据, 而不是表示播放器已经播放完了所有音频数据。
              */
             Log.i(TAG, "play end");

             // 表示推送完数据, 当播放器播放结束则会有playOver回调
             mAudioTrack.isFinishSend(true);
         } else if (event == TtsEvent.TTS_EVENT_PAUSE) {
             mAudioTrack.pause();
             Log.i(TAG, "play pause");
         } else if (event == TtsEvent.TTS_EVENT_RESUME) {
             mAudioTrack.play();
         } else if (event == TtsEvent.TTS_EVENT_ERROR) {
             // 表示推送完数据, 当播放器播放结束则会有playOver回调
             mAudioTrack.isFinishSend(true);

             String error_msg =  nui_tts_instance.getparamTts("error_msg");
             Log.e(TAG, "TTS_EVENT_ERROR error_code:" + ret_code + " errmsg:" + error_msg);
             ToastText(Utils.getMsgWithErrorCode(ret_code, "error"));
             ToastText("错误码:" + ret_code + " 错误信息:" + error_msg);
         }
     }
     ```

   - onTtsDataCallback：语音合成数据回调，将回调中的合成数据写入播放器进行播放。















     ```java
     public void onTtsDataCallback(String info, int info_len, byte[] data) {
         if (info.length() > 0) {
             Log.i(TAG, "info: " + info);
         }
         if (data.length > 0) {
             mAudioTrack.setAudioData(data);
             Log.i(TAG, "write:" + data.length);
         }
     }
     ```

   - onTtsLogTrackCallback：SDK内部日志回调（2.6.4版本新增）。















     ```java
     // SDK内部日志回调。若Override此回调，则SDK内部符合日志级别的日志将通过此回调送出。
     // 若多实例都Override此回调，则所有回调都会接收到SDK的日志信息。
     @Override
     public void onTtsLogTrackCallback(Constants.LogLevel level, String log) {
         Log.i(TAG, "onTtsLogTrackCallback log level:" + level + ", message -> " + log);
     }
     ```
5. 取消语音合成。















```java
nui_tts_instance.cancelTts("");
```

6. 退出语音合成。















```java
nui_tts_instance.tts_release();
```


## 常见问题

### 使用离线语音合成Android SDK，语音播报时出现不合理断句，该如何处理？

您可以通过SSML标记语言尝试解决。

### 调用Android SDK时，手机报错提示“audio recorder not init”。

您可以通过以下方式排查：

- 检查AudioRecord是否初始化正常。

- 检查语音播放器是否有问题。

- 编写AudioRecord录音代码，测试是否正常。


### 在模拟器上运行下载的Android程序，程序出现闪退现象，是什么原因？

模拟器可能会出现未知问题，建议您使用真机测试。

### int ret = nui\_instance.initialize(this, genInitParams(assets\_path,debug\_path), Constants.LogLevel.LOG\_LEVEL\_VERBOSE, true)。在该段代码中，录音权限是打开的，但代码仍然报错240021。

表示FILE\_ACCESS\_FAIL文件访问错误。你需要检查：

- 是否有文件读写权限。

- 是否完成SDK配置文件的拷贝，检查是否拷贝完成的代码示例如下：















```java
if (CommonUtils.copyAssetsData(this)) {
Log.i(TAG, "copy assets data done");
} else {
Log.i(TAG, "copy assets failed");
return;
}
```