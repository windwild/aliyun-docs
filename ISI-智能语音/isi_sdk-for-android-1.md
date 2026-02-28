### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) Android SDK

# Android SDK

更新时间：2025-11-03 04:03:30

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是智能语音交互](https://help.aliyun.com/zh/isi/product-overview/what-is-intelligent-speech-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

下载安装

SDK关键接口

调用步骤

Proguard配置

代码示例

本文为您介绍如何使用阿里云智能语音服务提供的Android NUI SDK，包括SDK下载安装、关键接口及代码示例。

## **前提条件**

- 使用SDK前，首先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/sdk-reference-12 "")。

- 已准备项目账号等信息，详情请参见 [开通授权](https://help.aliyun.com/zh/isi/enable-authorization-1 "")。


## **下载安装**

1. [移动端SDK选择与下载](https://help.aliyun.com/zh/isi/sdk-selection-and-download "")。



**说明**





请下载后在样例初始化代码中替换您的阿里云账号信息和Appkey才可运行。

2. 解压ZIP包，在`app/libs`目录下获取AAR格式的SDK包。

3. 使用Android Studio打开此工程。

其中，唤醒后进行一句话识别即唤醒识别的场景示例代码请参考WakeupAndSpeechRecognizerActivity.java文件，单纯唤醒的场景示例代码请参考OnlyWakeupActivity.java（2.6.4版本新增）。


## **SDK关键接口**

- **initialize**：初始化SDK。















```java
/**
* 初始化SDK，SDK为单例，请先释放后再次进行初始化。请勿在UI线程调用，可能会引起阻塞。
* @param callback: 事件监听回调，参见下文回调说明。
* @param parameters: 初始化参数，参见接口说明。
* @param level: log打印级别，值越小打印越多。
* @param save_log: 是否保存log为文件，存储目录为parameter中的debug_path字段值，log日志最大上限详见max_log_file_size。
* @return：参见错误码：https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int initialize(final INativeNuiCallback callback,
                                     String parameters,
                                     final Constants.LogLevel level,
                                     final boolean save_log)
```



其中，INativeNuiCallback类型包含如下回调。

  - **onNuiAudioStateChanged**：根据音频状态进行录音功能的开关。















    ```java
    /**
     * 当start/stop/cancel等接口调用时，SDK通过此回调通知App进行录音的开关操作
     * @param state：录音需要的状态（打开/关闭）
     */
    void onNuiAudioStateChanged(Constants.AudioState state);
    ```

  - **onNuiNeedAudioData**：在回调中提供音频数据。















    ```java
    /**
     * 开始识别时，此回调被连续调用，App需要在回调中进行语音数据填充
     * @param buffer: 填充语音的存储区
     * @param len: 需要填充语音的字节数
     * @return 实际填充的字节数
     */
    int onNuiNeedAudioData(byte[] buffer, int len);
    ```

  - **onNuiEventCallback**：SDK事件回调。















    ```java
    /**
     * SDK主要事件回调
     * @param event: 回调事件，参见如下事件列表
     * @param resultCode: 参见错误码，在出现EVENT_ASR_ERROR事件时有效
     * @param arg2: 保留参数
     * @param kwsResult: 语音唤醒功能
     * @param asrResult: 语音识别结果
     */
    void onNuiEventCallback(NuiEvent event, final int resultCode, final int arg2, KwsResult kwsResult, AsrResult asrResult);
    ```



    事件列表：




    | **名称** | **说明** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **名称** | **说明** |
    | EVENT\_WUW\_TRUST | 检测到唤醒词。 |
    | EVENT\_VAD\_START | 检测到人声起点。 |
    | EVENT\_VAD\_END | 检测到人声尾点。 |
    | EVENT\_ASR\_PARTIAL\_RESULT | 语音识别中间结果。 |
    | EVENT\_ASR\_RESULT | 语音识别最终结果。 |
    | EVENT\_ASR\_ERROR | 根据错误码信息判断出错原因。 |
    | EVENT\_MIC\_EEROR | 录音错误。 |

  - **onNuiAudioRMSChanged**：音频能量值回调。















    ```java
    /**
     * 音频能量值回调
     * @param val: 音频数据能量值回调，范围-160至0，一般用于UI展示语音动效
     */
    public void onNuiAudioRMSChanged(float val);
    ```

  - **onNuiLogTrackCallback**：SDK内部日志回调（2.6.4版本新增）。















    ```java
    /**
     * SDK内部日志回调。若Override此回调，则SDK内部符合日志级别的日志将通过此回调送出。若多实例都Override此回调，则所有回调都会接收到SDK的日志信息。
     * @param level: 大于此日志级别的SDK内部日志将通过此回调送出
     * @param log: 具体的日志内容
     */
    public void onNuiLogTrackCallback(Constants.LogLevel level, String log);
    ```
- **set\_params**：以JSON格式设置SDK参数。















```java
/**
* 以JSON格式设置参数
* @param params：参见接口说明 https://help.aliyun.com/zh/isi/sdk-reference-12
* @return：参见错误码：https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int setParams(String params)
```

- **startDialog**：开始唤醒识别。















```java
/**
* 开始识别
* @param vad_mode: 多种模式，对于唤醒后识别的场景，则用TYPE_KWS；若只使用唤醒功能，则用TYPE_ONLY_KWS
* @return：参见错误码：https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int startDialog(VadMode vad_mode, String dialog_params);
```

- **stopDialog**：结束识别。















```java
/**
* 结束识别，调用该接口后，服务端将返回最终识别结果并结束任务
* @return：参见错误码：https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int stopDailog();
```

- **cancelDialog**：立即结束识别。















```java
/**
* 结束识别，调用该接口后，将不等待服务端将返回最终识别结果而立即结束任务
* @return：参见错误码：https://help.aliyun.com/document_detail/459864.html。
*/
public synchronized int cancelDialog();
```

- **release**：释放SDK。















```java
/**
* 释放SDK资源
* @return 参见错误码
*/
public synchronized int release()
```


## **调用步骤**

1. 初始化SDK、录音实例。

2. 根据业务需求设置参数。

3. 调用startDialog开始识别。

4. 根据音频状态回调onNuiAudioStateChanged，打开录音机。

5. 在onNuiNeedAudioData回调中提供录音数据。

6. 在EVENT\_WUW\_TRUST事件中进行用户提示。

7. 在EVENT\_ASR\_PARTIAL\_RESULT事件回调中获取识别结果。

8. 在EVENT\_ASR\_RESULT事件中获取最终识别结果。

9. 结束调用，使用release接口释放SDK资源。


## **Proguard配置**

如果代码使用了混淆，请在proguard-rules.pro中配置：

```java
-keep class com.alibaba.idst.nui.*{*;}
```

## 代码示例

**NUI SDK初始化**

```java
//创建NUI实例
NativeNui nui_instance = new NativeNui();

//拷贝资源
CommonUtils.copyAssetsData(this);

//这里获得当前nuisdk.aar中assets路径
String asset_path = CommonUtils.getModelPath(this);

// 创建调试目录，用于存储运行日志
String debug_path = getExternalCacheDir().getAbsolutePath() + "/debug";
Utils.createDir(debug_path);

//SDK初始化
//由于唤醒功能为本地功能, 涉及鉴权, 故genInitParams中需要填写ak_id、ak_secret
int ret = nui_instance.initialize(this, genInitParams(asset_path, debug_path), Constants.LogLevel.LOG_LEVEL_VERBOSE, true);
```

其中，genInitParams生成为String JSON字符串，包含资源目录和用户信息。其中用户信息包含如下字段：

```java
private String genInitParams(String workpath, String debugpath) {
    String str = "";
    try {
        // 需要特别注意：ak_id/ak_secret/app_key/sdk_code/device_id等参数必须传入SDK
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户的sdk_code也可用于唤醒
        // 鉴权信息获取参：https://help.aliyun.com/document_detail/69835.htm

        //获取账号访问凭证：
        Auth.GetTicketMethod method = Auth.GetTicketMethod.GET_STS_ACCESS_FROM_SERVER_FOR_OFFLINE_FEATURES;
        if (!g_appkey.isEmpty()) {
            Auth.setAppKey(g_appkey);
        }
        if (!g_token.isEmpty()) {
            Auth.setToken(g_token);
        }
        if (!g_ak.isEmpty()) {
            Auth.setAccessKey(g_ak);
        }
        if (!g_sk.isEmpty()) {
            Auth.setAccessKeySecret(g_sk);
        }
        Auth.setStsToken(g_sts_token);
        Auth.setSdkCode(g_sdk_code);
        // 此处展示将用户传入账号信息进行交互，实际产品不可以将任何账号信息存储在端侧
        if (!g_appkey.isEmpty()) {
            if (!g_ak.isEmpty() && !g_sk.isEmpty()) {
                if (g_sts_token.isEmpty()) {
                    method = Auth.GetTicketMethod.GET_ACCESS_IN_CLIENT_FOR_OFFLINE_FEATURES;
                } else {
                    method = Auth.GetTicketMethod.GET_STS_ACCESS_IN_CLIENT_FOR_OFFLINE_FEATURES;
                }
            }
        }
        Log.i(TAG, "Use method:" + method);
        JSONObject object = Auth.getTicket(method);

        object.put("url", "wss://nls-gateway.cn-shanghai.aliyuncs.com:443/ws/v1");
        //工作目录路径，SDK从该路径读取配置文件
        object.put("workspace", workpath); // 必填
        object.put("debug_path", debugpath);

        //过滤SDK内部日志通过回调送回到用户层
        object.put("log_track_level", String.valueOf(Constants.LogLevel.toInt(Constants.LogLevel.LOG_LEVEL_INFO)));

        // ModeFullMix = 0   // 选用此模式开启本地功能并需要进行鉴权注册，TYPE_KWS模式选这个
        // ModeFullCloud = 1
        // ModeFullLocal = 2 // 选用此模式开启本地功能并需要进行鉴权注册，YPE_ONLY_KWS模式选这个
        // ModeAsrMix = 3    // 选用此模式开启本地功能并需要进行鉴权注册
        // ModeAsrCloud = 4
        // ModeAsrLocal = 5  // 选用此模式开启本地功能并需要进行鉴权注册
        object.put("service_mode", Constants.ModeFullMix); // 必填

        //如果使用外置唤醒资源，可以进行设置文件路径。通过upgrade_file参数传入唤醒模型文件的绝对路径。

        // 举例1：模型文件kws.bin可以放在assets，这里需要主动拷贝到App的data目录，并获得绝对路径。
        String kws_bin_name = "kws.bin";
        String kws_bin_dest_name = CommonUtils.getModelPath(this) + "/" + kws_bin_name;
        CommonUtils.copyAsset(this, kws_bin_name, kws_bin_dest_name);

        // 举例2：模型文件kws.bin放在/sdcard/目录，请确认读写权限
//            kws_bin_name = "kws.bin";
//            String kws_bin_dest_name = "/sdcard/" + kws_bin_name;

        object.put("upgrade_file", kws_bin_dest_name);
        str = object.toString();
    } catch (JSONException e) {
        e.printStackTrace();
    }

    // 注意! str中包含ak_id ak_secret token app_key等敏感信息, 实际产品中请勿在Log中输出这类信息！
    Log.i(TAG, "InsideUserContext:" + str);
    return str;
}

// 将鉴权信息打包成json格式
public static JSONObject getTicket(GetTicketMethod method) {
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

    JSONObject object = new JSONObject();

    cur_method = method;

    //项目创建
    //  创建appkey请查看：https://help.aliyun.com/zh/isi/getting-started/start-here
    String APPKEY = "<您申请创建的app_key>";
    if (!cur_appkey.isEmpty()) {
        APPKEY = cur_appkey;
    }
    object.put("app_key", APPKEY); // 必填
    cur_appkey = APPKEY;

    if (method == GetTicketMethod.GET_STS_ACCESS_FROM_SERVER_FOR_ONLINE_FEATURES) {
        //方法一，仅适合在线语音交互服务(强烈推荐):
        //  客户远端服务端使用STS服务获得STS临时凭证，然后下发给移动端侧，详情请查看：
        //    https://help.aliyun.com/document_detail/466615.html 使用其中方案二使用STS获取临时账号。
        //  然后在移动端侧通过AccessToken()获得Token和有效期，用于在线语音交互服务。
        String STS_AK_ID = "STS.<服务器生成的具有时效性的临时凭证>";
        String STS_AK_SECRET = "<服务器生成的具有时效性的临时凭证>";
        String STS_TOKEN = "<服务器生成的具有时效性的临时凭证>";
        String TOKEN = "<由STS生成的临时访问令牌>";
        final AccessToken token = new AccessToken(STS_AK_ID, STS_AK_SECRET, STS_TOKEN);
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_token = TOKEN;
            cur_ak = STS_AK_ID;
            cur_sk = STS_AK_SECRET;
            cur_sts_token = STS_TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
            cur_sts_token = "";
        }
    } else if (method == GetTicketMethod.GET_STS_ACCESS_FROM_SERVER_FOR_OFFLINE_FEATURES) {
        //方法二，仅适合离线语音交互服务(强烈推荐):
        //  客户远端服务端使用STS服务获得STS临时凭证，然后下发给移动端侧，详情请查看：
        //    https://help.aliyun.com/document_detail/466615.html 使用其中方案二使用STS获取临时账号。
        String STS_AK_ID = "STS.<服务器生成的具有时效性的临时凭证>";
        String STS_AK_SECRET = "<服务器生成的具有时效性的临时凭证>";
        String STS_TOKEN = "<服务器生成的具有时效性的临时凭证>";
        object.put("ak_id", STS_AK_ID); // 必填
        object.put("ak_secret", STS_AK_SECRET); // 必填
        object.put("sts_token", STS_TOKEN); // 必填
        cur_ak = STS_AK_ID;
        cur_sk = STS_AK_SECRET;
        cur_sts_token = STS_TOKEN;
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    } else if (method == GetTicketMethod.GET_STS_ACCESS_FROM_SERVER_FOR_MIXED_FEATURES) {
        //方法三，适合离在线语音交互服务(强烈推荐):
        //  客户远端服务端使用STS服务获得STS临时凭证，然后下发给移动端侧，详情请查看：
        //    https://help.aliyun.com/document_detail/466615.html 使用其中方案二使用STS获取临时账号。
        //  然后在移动端侧通过AccessToken()获得Token和有效期，用于在线语音交互服务。
        //注意！此处介绍同一个Appkey用于在线和离线功能，用户可创建两个Appkey分别用于在线和离线功能。
        String STS_AK_ID = "STS.<服务器生成的具有时效性的临时凭证>";
        String STS_AK_SECRET = "<服务器生成的具有时效性的临时凭证>";
        String STS_TOKEN = "<服务器生成的具有时效性的临时凭证>";
        String TOKEN = "<由STS生成的临时访问令牌>";
        final AccessToken token = new AccessToken(STS_AK_ID, STS_AK_SECRET, STS_TOKEN);
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();

        object.put("ak_id", STS_AK_ID); // 必填
        object.put("ak_secret", STS_AK_SECRET); // 必填
        object.put("sts_token", STS_TOKEN); // 必填
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_token = TOKEN;
            cur_ak = STS_AK_ID;
            cur_sk = STS_AK_SECRET;
            cur_sts_token = STS_TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
            cur_sts_token = "";
        }
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    } else if (method == GetTicketMethod.GET_TOKEN_FROM_SERVER_FOR_ONLINE_FEATURES) {
        //方法四，仅适合在线语音交互服务(推荐):
        //  客户远端服务端使用Token服务获得Token临时令牌，然后下发给移动端侧，详情请查看：
        //    https://help.aliyun.com/document_detail/466615.html 使用其中方案一获取临时令牌Token
        //  获得Token方法：
        //    https://help.aliyun.com/zh/isi/getting-started/overview-of-obtaining-an-access-token
        String TOKEN = "<服务器生成的具有时效性的临时凭证>";
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
        } else {
            cur_token = "";
        }
    } else if (method == GetTicketMethod.GET_ACCESS_FROM_SERVER_FOR_OFFLINE_FEATURES) {
        //方法五，仅适合离线语音交互服务(不推荐):
        //  客户远端服务端将账号信息ak_id和ak_secret(请加密)下发给移动端侧。
        //注意！账号信息出现在移动端侧，存在泄露风险。
        String AK_ID = "<一定不可代码中存储和本地明文存储>";
        String AK_SECRET = "<一定不可代码中存储和本地明文存储>";
        object.put("ak_id", AK_ID); // 必填
        object.put("ak_secret", AK_SECRET); // 必填
        cur_ak = AK_ID;
        cur_sk = AK_SECRET;
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    } else if (method == GetTicketMethod.GET_ACCESS_FROM_SERVER_FOR_MIXED_FEATURES) {
        //方法六，适合离在线语音交互服务(不推荐):
        //  客户远端服务端将账号信息ak_id和ak_secret(请加密)下发给移动端侧。
        //  然后在移动端侧通过AccessToken()获得Token和有效期，用于在线语音交互服务。
        //注意！账号信息出现在移动端侧，存在泄露风险。
        String AK_ID = "<一定不可代码中存储和本地明文存储>";
        String AK_SECRET = "<一定不可代码中存储和本地明文存储>";
        String TOKEN = "<生成的临时访问令牌>";
        final AccessToken token = new AccessToken(AK_ID, AK_SECRET, "");
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();

        object.put("ak_id", AK_ID); // 必填
        object.put("ak_secret", AK_SECRET); // 必填
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
        }
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    } else if (method == GetTicketMethod.GET_TOKEN_IN_CLIENT_FOR_ONLINE_FEATURES) {
        //方法七，仅适合在线语音交互服务(强烈不推荐):
        //  仅仅用于开发和调试
        //注意！账号信息出现在移动端侧，存在泄露风险。
        String TOKEN = "<移动端写死的访问令牌，仅用于调试>";
        if (!cur_token.isEmpty()) {
            TOKEN = cur_token;
        }
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
        } else {
            cur_token = "";
        }
    } else if (method == GetTicketMethod.GET_ACCESS_IN_CLIENT_FOR_OFFLINE_FEATURES) {
        //方法八，仅适合离线语音交互服务(强烈不推荐):
        //  仅仅用于开发和调试
        //注意！账号信息出现在移动端侧，存在泄露风险。
        String AK_ID = "<移动端写死的账号信息，仅用于调试>";
        String AK_SECRET = "<移动端写死的账号信息，仅用于调试>";
        if (!cur_ak.isEmpty()) {
            AK_ID = cur_ak;
        }
        if (!cur_sk.isEmpty()) {
            AK_SECRET = cur_sk;
        }

        object.put("ak_id", AK_ID); // 必填
        object.put("ak_secret", AK_SECRET); // 必填
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    } else if (method == GetTicketMethod.GET_ACCESS_IN_CLIENT_FOR_MIXED_FEATURES) {
        //方法九，适合离在线语音交互服务(强烈不推荐):
        //  仅仅用于开发和调试
        //注意！账号信息出现在移动端侧，存在泄露风险。
        String AK_ID = "<移动端写死的账号信息，仅用于调试>";
        String AK_SECRET = "<移动端写死的账号信息，仅用于调试>";
        String TOKEN = "<生成的临时访问令牌>";
        if (!cur_ak.isEmpty()) {
            AK_ID = cur_ak;
        }
        if (!cur_sk.isEmpty()) {
            AK_SECRET = cur_sk;
        }
        final AccessToken token = new AccessToken(AK_ID, AK_SECRET, "");
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();

        object.put("ak_id", AK_ID); // 必填
        object.put("ak_secret", AK_SECRET); // 必填
        cur_ak = AK_ID;
        cur_sk = AK_SECRET;
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
        }
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    } else if (method == GetTicketMethod.GET_ACCESS_IN_CLIENT_FOR_ONLINE_FEATURES) {
        //方法十，适合在线语音交互服务(强烈不推荐):
        //  仅仅用于开发和调试
        //注意！账号信息出现在移动端侧，存在泄露风险。
        String AK_ID = "<移动端写死的账号信息，仅用于调试>";
        String AK_SECRET = "<移动端写死的账号信息，仅用于调试>";
        String TOKEN = "<生成的临时访问令牌>";
        if (!cur_ak.isEmpty()) {
            AK_ID = cur_ak;
        }
        if (!cur_sk.isEmpty()) {
            AK_SECRET = cur_sk;
        }
        final AccessToken token = new AccessToken(AK_ID, AK_SECRET, "");
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();

        object.put("ak_id", AK_ID); // 必填
        object.put("ak_secret", AK_SECRET); // 必填
        cur_ak = AK_ID;
        cur_sk = AK_SECRET;
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
        }
    } else if (method == GetTicketMethod.GET_STS_ACCESS_IN_CLIENT_FOR_ONLINE_FEATURES) {
        //方法十一，适合在线语音交互服务(强烈不推荐):
        //  仅仅用于开发和调试
        String STS_AK_ID = "STS.<移动端写死的账号信息，仅用于调试>";
        String STS_AK_SECRET = "<移动端写死的账号信息，仅用于调试>";
        String STS_TOKEN = "<移动端写死的账号信息，仅用于调试>";
        if (!cur_ak.isEmpty()) {
            STS_AK_ID = cur_ak;
        }
        if (!cur_sk.isEmpty()) {
            STS_AK_SECRET = cur_sk;
        }
        if (!cur_sts_token.isEmpty()) {
            STS_TOKEN = cur_sts_token;
        }
        String TOKEN = "<由STS生成的临时访问令牌>";
        final AccessToken token = new AccessToken(STS_AK_ID, STS_AK_SECRET, STS_TOKEN);
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();

        object.put("ak_id", STS_AK_ID); // 必填
        object.put("ak_secret", STS_AK_SECRET); // 必填
        object.put("sts_token", STS_TOKEN); // 必填
        cur_ak = STS_AK_ID;
        cur_sk = STS_AK_SECRET;
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
            cur_sts_token = STS_TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
            cur_sts_token = "";
        }
    } else if (method == GetTicketMethod.GET_STS_ACCESS_IN_CLIENT_FOR_OFFLINE_FEATURES) {
        //方法十二，适合离线语音交互服务(强烈不推荐):
        //  仅仅用于开发和调试
        String STS_AK_ID = "STS.<移动端写死的账号信息，仅用于调试>";
        String STS_AK_SECRET = "<移动端写死的账号信息，仅用于调试>";
        String STS_TOKEN = "<移动端写死的账号信息，仅用于调试>";
        if (!cur_ak.isEmpty()) {
            STS_AK_ID = cur_ak;
        }
        if (!cur_sk.isEmpty()) {
            STS_AK_SECRET = cur_sk;
        }
        if (!cur_sts_token.isEmpty()) {
            STS_TOKEN = cur_sts_token;
        }
        String TOKEN = "<由STS生成的临时访问令牌>";
        final AccessToken token = new AccessToken(STS_AK_ID, STS_AK_SECRET, STS_TOKEN);
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();

        object.put("ak_id", STS_AK_ID); // 必填
        object.put("ak_secret", STS_AK_SECRET); // 必填
        object.put("sts_token", STS_TOKEN); // 必填
        cur_ak = STS_AK_ID;
        cur_sk = STS_AK_SECRET;
        cur_sts_token = STS_TOKEN;
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
            cur_sts_token = "";
        }
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    } else if (method == GetTicketMethod.GET_STS_ACCESS_IN_CLIENT_FOR_MIXED_FEATURES) {
        //方法十三，适合离在线语音交互服务(强烈不推荐):
        //  仅仅用于开发和调试
        String STS_AK_ID = "STS.<移动端写死的账号信息，仅用于调试>";
        String STS_AK_SECRET = "<移动端写死的账号信息，仅用于调试>";
        String STS_TOKEN = "<移动端写死的账号信息，仅用于调试>";
        if (!cur_ak.isEmpty()) {
            STS_AK_ID = cur_ak;
        }
        if (!cur_sk.isEmpty()) {
            STS_AK_SECRET = cur_sk;
        }
        if (!cur_sts_token.isEmpty()) {
            STS_TOKEN = cur_sts_token;
        }
        String TOKEN = "<由STS生成的临时访问令牌>";
        final AccessToken token = new AccessToken(STS_AK_ID, STS_AK_SECRET, STS_TOKEN);
        Thread th = new Thread() {
            @Override
            public void run() {
                try {
                    token.apply();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        th.start();
        try {
            th.join(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        TOKEN = token.getToken();

        object.put("ak_id", STS_AK_ID); // 必填
        object.put("ak_secret", STS_AK_SECRET); // 必填
        object.put("sts_token", STS_TOKEN); // 必填
        cur_ak = STS_AK_ID;
        cur_sk = STS_AK_SECRET;
        cur_sts_token = STS_TOKEN;
        if (TOKEN != null && !TOKEN.isEmpty()) {
            object.put("token", TOKEN);  // 必填
            cur_appkey = APPKEY;
            cur_token = TOKEN;
            // token生命周期超过expired_time, 则需要重新token = new AccessToken()
            cur_token_expired_time = token.getExpireTime();
        } else {
            cur_token = "";
            cur_sts_token = "";
        }
        // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
        // 离线语音合成账户和sdk_code可用于唤醒
        // 由创建Appkey时设置
        object.put("sdk_code", cur_sdk_code); // 必填
    }

    return object;
}
```

**参数设置**

以JSON字符串形式进行设置。需要在startDialog()之前通过setParams()进行设置并生效。

```java
private String genParams() {
  String params = "";
  try {
    JSONObject nls_config = new JSONObject();

    // 是否返回中间识别结果，默认值：False。
    nls_config.put("enable_intermediate_result", true);
    // 是否在后处理中添加标点，默认值：False。
    nls_config.put("enable_punctuation_prediction", true);

    //参数可根据实际业务进行配置
    // nls_config.put("enable_inverse_text_normalization", true);
    // nls_config.put("enable_voice_detection", true);
    // nls_config.put("customization_id", "test_id");
    // nls_config.put("vocabulary_id", "test_id");
    // nls_config.put("max_start_silence", 10000);
    // nls_config.put("max_end_silence", 800);
    // nls_config.put("sample_rate", 16000);
    // nls_config.put("sr_format", "opus");

    /*若文档中不包含某些参数，但是此功能支持这个参数，可以用如下万能接口设置参数*/
   // JSONObject extend_config = new JSONObject();
   // extend_config.put("custom_test", true);
   // nls_config.put("extend_config", extend_config);

    JSONObject parameters = new JSONObject();
    parameters.put("nls_config", nls_config);
    //选择一句话识别服务
    parameters.put("service_type", Constants.kServiceTypeASR);

    //可以通过以下方式设置自定义唤醒词进行体验，如果需要更好的唤醒效果请进行唤醒词定制
    //注意：动态唤醒词只有在设置了唤醒模型的前提下才可以使用
    JSONArray dynamic_wuw = new JSONArray();
    JSONObject wuw = new JSONObject();
    wuw.put("name", "小白小白");
    wuw.put("type", "main");
    dynamic_wuw.add(wuw);
    parameters.put("wuw", dynamic_wuw);

    params = parameters.toString();
  } catch (JSONException e) {
    e.printStackTrace();
  }
  return params;
}

//设置相关识别参数，具体参考API文档
nui_instance.setParams(genParams());
```

**开始识别**

通过startDialog接口开启监听。

```java
// 唤醒后立即一句话识别，选择TYPE_KWS
// 只用唤醒功能，选择TYPE_ONLY_KWS
nui_instance.startDialog(Constants.VadMode.TYPE_KWS, genDialogParams());

private String genDialogParams() {
    String params = "";
    try {
        JSONObject dialog_param = new JSONObject();
        // 需要更新参数可再次设置，比如刷新token
        params = dialog_param.toString();
    } catch (JSONException e) {
        e.printStackTrace();
    }

    Log.i(TAG, "dialog params: " + params);
    return params;
}
```

**回调处理**

- onNuiAudioStateChanged：录音状态回调，SDK内部维护录音状态，调用时根据该状态的回调进行录音机的开关操作。















```java
//当录音状态发送变化的时候调用
@Override
public void onNuiAudioStateChanged(Constants.AudioState state) {
      Log.i(TAG, "onNuiAudioStateChanged");
      if (state == Constants.AudioState.STATE_OPEN) {
          Log.i(TAG, "audio recorder start");
          appendText(detailView, "RECORDER STATE_OPEN");
          if (mAudioRecorder != null) {
              mAudioRecorder.startRecording();
          }
          Log.i(TAG, "audio recorder start done");
      } else if (state == Constants.AudioState.STATE_CLOSE) {
          Log.i(TAG, "audio recorder close");
          appendText(detailView, "RECORDER STATE_CLOSE");
          if (mAudioRecorder != null) {
              mAudioRecorder.release();
          }
      } else if (state == Constants.AudioState.STATE_PAUSE) {
          Log.i(TAG, "audio recorder pause");
          appendText(detailView, "RECORDER STATE_PAUSE");
          if (mAudioRecorder != null) {
              mAudioRecorder.stop();
          }
      }
}
```

- onNuiNeedAudioData：录音数据回调，在该回调中填充录音数据。















```java
//当调用NativeNui的start后，会一定时间反复回调该接口，底层会提供buffer并告知这次需要数据的长度
//返回值告知底层读了多少数据，应该尽量保证return的长度等于需要的长度，如果返回<=0，则表示出错
@Override
public int onNuiNeedAudioData(byte[] buffer, int len) {
      if (mAudioRecorder == null) {
          return -1;
      }
      if (mAudioRecorder.getState() != AudioRecord.STATE_INITIALIZED) {
          Log.e(TAG, "audio recorder not init");
          return -1;
      }

      // 送入SDK
      int audio_size = mAudioRecorder.read(buffer, 0, len);

      // 音频存储到缓存
      if (mSaveAudioSwitch.isChecked() && audio_size > 0) {
          tmpAudioQueue.offer(buffer);
      }

      return audio_size;
}
```

- onNuiEventCallback：NUI SDK事件回调，请勿在事件回调中调用SDK的接口，可能引起死锁。















```java
//当回调事件发生时调用
@Override
public void onNuiEventCallback(Constants.NuiEvent event, final int resultCode,
                                 final int arg2, KwsResult kwsResult,
                                 AsrResult asrResult) {
      Log.i(TAG, "event=" + event);
      if (event == Constants.NuiEvent.EVENT_WUW_TRUST) {
          JSONObject jsonObject = JSON.parseObject(kwsResult.kws);
          String result = jsonObject.getString("word");
      } else if (event == Constants.NuiEvent.EVENT_ASR_RESULT) {
          JSONObject jsonObject = JSON.parseObject(asrResult.allResponse);
          JSONObject payload = jsonObject.getJSONObject("payload");
          String result = payload.getString("result");
      } else if (event == Constants.NuiEvent.EVENT_ASR_PARTIAL_RESULT) {
          JSONObject jsonObject = JSON.parseObject(asrResult.allResponse);
          JSONObject payload = jsonObject.getJSONObject("payload");
          String result = payload.getString("result");
      } else if (event == Constants.NuiEvent.EVENT_ASR_ERROR) {
          final String msg_text = Utils.getMsgWithErrorCode(resultCode, "start");
      } else if (event == Constants.NuiEvent.EVENT_MIC_ERROR) {
          final String msg_text = Utils.getMsgWithErrorCode(resultCode, "start");
          // EVENT_MIC_ERROR表示2s未传入音频数据，请检查录音相关代码、权限或录音模块是否被其他应用占用。
          // 此处也可重新启动录音模块
      }
}
```

- onNuiLogTrackCallback：SDK内部日志回调（2.6.4版本新增）。















```java
// SDK内部日志回调。若Override此回调，则SDK内部符合日志级别的日志将通过此回调送出。
// 若多实例都Override此回调，则所有回调都会接收到SDK的日志信息。
@Override
public void onNuiLogTrackCallback(Constants.LogLevel level, String log) {
      Log.i(TAG, "onNuiLogTrackCallback log level:" + level + ", message -> " + log);
}
```


**取消识别**

```java
nui_instance.cancelDialog();
```

**停止识别**

```java
nui_instance.stopDialog();
```