### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[一句话识别](https://help.aliyun.com/zh/isi/developer-reference/short-sentence-recognition/)[移动端SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-mobile-clients/)iOS SDK

# iOS SDK

更新时间：2025-11-06 01:20:58

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Android SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-android)[下一篇：HarmonyOS Next SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-harmonyosnext)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

下载安装

SDK关键接口

调用步骤

代码示例

NUI SDK初始化

参数设置

开始识别

回调处理

结束识别

常见问题

iOS SDK使用一句话识别功能，集成nuisdk.framework，按照文档在工程Build Phases的Link Binary With Libraries中添加nuisdk.framework，在编译配置的General > Frameworks, Libraries, and Embedded Content中配置nuisdk.framework为Embed & Sign，但.m中仍提示找不到 nuisdk.framework/Headers/NeoNui.h如何解决？

是否有Android和iOS的SDK，能否用在专有云环境下？

iOS是否支持后台处理？

下载语音交互iOS SDK至本地静态库，运行Demo程序测试代码时，模拟器可以正常运行，真机无法运行，报错“Reason: no suitable image found. Did find:xxx”如何解决？

iOS端集成nuisdk运行报mic错误如何处理？

使用智能语音服务集成iOS SDK，接入nuisdk.framework后，导入头文件#import "nuisdk.framework/Headers/NeoNui.h"后项目报错如何解决？

按照文档使用SDK接入后报错“/Users/admin/FlashTranscription\_iOS/Fc\_ASR.xcodeproj Building for iOS, but the linked and embedded framework 'nuisdk.framework' was built for iOS + iOS Simulator."”如何解决？

使用集成语音服务iOS SDK，集成flutter\_plugin时报错“Undefined symbols for architecture arm64: "std::\_\_1::mutex::~mutex()", referenced from: \_\_\_cxx\_global\_var\_init in libflutter\_tts.a(ringBuf.o)”如何解决？

TRTC实时音视频和语音识别结合，当同时调用麦克风时可能会发生冲突，导致有一方没有声音如何解决？

使用App集成iOS SDK，提交到App store失败，提示“Unsupported Architectures. The executable for AliYunSmart.app/Frameworks/nuisdk.framework contains unsupported architectures '\[x86\_ \_64, i386\]'. With error code”如何解决？

使用集成语音服务iOS SDK，接入nuisdk.framework后报错，要修改Legacy Build system才可以运行，如何解决？

本文介绍如何使用阿里云智能语音服务提供的iOS NUI SDK，包括SDK下载安装、关键接口及代码示例。

## 前提条件

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/overview-3#topic-2572215 "")。

- 准备好项目Appkey，详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#topic-2572188 "")。

- 已获取Access Token，详情请参见 [获取Token概述](https://help.aliyun.com/zh/isi/overview-of-obtaining-an-access-token#587dee8029x7r "")。


## 下载安装

1. [移动端SDK选择与下载](https://help.aliyun.com/zh/isi/sdk-selection-and-download "")。



**重要**





请下载后在样例初始化代码中替换您的阿里云账号信息、Appkey和Token才可运行。



为方便集成，2.5.14版本后iOS接口使用纯Object-C接口，不再使用C++混合接口。

2. 解压ZIP包，将zip包中的nuisdk.framework添加到您的工程中，并在工程Build Phases的Link Binary With Libraries中添加nuisdk.framework。

3. 使用Xcode打开此工程，工程中提供了参考代码以及一些直接可使用的工具类，例如音频播放录制和文件操作，您可以直接复制源码到您的实际工程进行使用。其中一句话识别示例代码为SpeechRecognizerViewController。替换Appkey和Token后可直接运行。


## SDK关键接口

- **nui\_initialize**：初始化SDK。















```javascript
/**
* 初始化SDK，SDK为单例，请先释放后再次进行初始化。请勿在UI线程调用，可能引起阻塞。
* @param parameters: 初始化参数，参见接口说明文档:https://help.aliyun.com/zh/isi/developer-reference/overview-3
* @param level: log打印级别，值越小打印越多
* @param save_log: 是否保存log为文件，存储目录为parameter中的debug_path字段值。注意，log文件无上限，请注意持续存储导致磁盘存满。
* @return 参见错误码
*/
  -(NuiResultCode) nui_initialize:(const char *)parameters
                         logLevel:(NuiSdkLogLevel)level
                          saveLog:(BOOL)save_log;
```

- **nui\_set\_params**：以JSON格式设置SDK参数。















```cpp
/**
* 以JSON格式设置参数
* @param params: 参数信息请参见接口说明文档:https://help.aliyun.com/zh/isi/developer-reference/overview-3
* @return 参见错误码
*/
  -(NuiResultCode) nui_set_params:(const char *)params;
```

- **nui\_dialog\_start**：开始识别。















```cpp
/**
* 开始识别
* @param vad_mode: 多种模式，对于识别场景，请使用P2T
* @param dialog_params: 设置识别参数，可不设置
* @return 参见错误码
*/
  -(NuiResultCode) nui_dialog_start:(NuiVadMode)vad_mode
                        dialogParam:(const char *)dialog_params;
```

- **nui\_dialog\_cancel**：结束识别。















```cpp
/**
* 结束识别，调用该接口后，服务端将返回最终识别结果并结束任务
* @param force: 是否强制结束而忽略最终结果，false或NO表示停止但是等待完整结果返回
* @return 参见错误码
*/
  -(NuiResultCode) nui_dialog_cancel:(BOOL)force;
```

- **nui\_release**：释放SDK。















```cpp
/**
* 释放SDK资源
* @return 参见错误码
*/
  -(NuiResultCode) nui_release;
```

- **nui\_get\_version**：获得当前SDK版本信息。















```
/**
* 获得当前SDK版本信息
* @return 字符串形式的SDK版本信息
*/
  -(const char*) nui_get_version;
```

- **nui\_get\_all\_response**：获得当前事件回调的完整信息。















```
/**
* 获得当前事件回调的完整信息
* @return json字符串形式的完整事件信息
*/
  -(const char*) nui_get_all_response;
```

- **NeoNuiSdkDelegate：** 事件代理

onNuiEventCallback：SDK事件回调。















```cpp
/**
* SDK主要事件回调
* @param event: 回调事件，参见如下事件列表
* @param dialog: 会话编号（暂不支持）
* @param wuw: 语音唤醒功能使用（暂不支持）
* @param asr_result: 语音识别结果
* @param finish: 本轮识别是否结束标志
* @param resultCode: 参见错误码，在出现EVENT_ASR_ERROR事件时有效
*/
  -(void) onNuiEventCallback:(NuiCallbackEvent)nuiEvent
                      dialog:(long)dialog
                   kwsResult:(const char *)wuw
                   asrResult:(const char *)asr_result
                    ifFinish:(BOOL)finish
                     retCode:(int)code;
```



NuiCallbackEvent事件列表：




| **名称** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **名称** | **说明** |
| EVENT\_VAD\_START | 检测到人声起点。 |
| EVENT\_VAD\_END | 检测到人声尾点。 |
| EVENT\_ASR\_PARTIAL\_RESULT | 语音识别中间结果。 |
| EVENT\_ASR\_RESULT | 语音识别最终结果。 |
| EVENT\_ASR\_ERROR | 根据错误码信息判断出错原因。 |
| EVENT\_MIC\_EEROR | 录音错误，表示SDK连续2秒未收到任何音频，可检查录音系统是否正常。 |



onNuiNeedAudioData：获取音频















```cpp
/**
* 开始识别时，此回调被连续调用，App需要在回调中进行语音数据填充
* @param audioData:  填充语音的存储区
* @param len: 需要填充语音的字节数
* @return 实际填充的字节数
*/
  -(int) onNuiNeedAudioData:(char *)audioData length:(int)len;
```



onNuiAudioStateChanged：根据音频状态进行录音功能的开关。















```cpp
/**
* 当start/stop/cancel等接口调用时，SDK通过此回调通知App进行录音的开关操作
* @param state：录音需要的状态（打开/关闭）
*/
  -(void) onNuiAudioStateChanged:(NuiAudioState)state;
```



onNuiRmsChanged：音频能量事件。















```cpp
/**
* SDK主要事件回调
* @param rms: 语音能量值，范围为-160至0
*/
  -(void) onNuiRmsChanged:(float) rms;
```


## 调用步骤

1. 初始化SDK、录音实例。

2. 根据业务需求配置参数。

3. 调用nui\_dialog\_start开始识别。

4. 根据音频状态回调onNuiAudioStateChanged，打开录音机。

5. 在onNuiNeedAudioData回调中提供录音数据。

6. 在EVENT\_ASR\_PARTIAL\_RESULT事件回调中获取识别结果。

7. 调用nui\_dialog\_cancel结束识别。

8. 结束调用，使用release接口释放SDK资源。


## 代码示例

**说明**

接口默认采用get\_instance方式获得单例，您如果有多例需求，也可以直接alloc对象进行使用。

### **NUI SDK初始化**

```cpp
BOOL save_log = NO;
NSString * initParam = [self genInitParams];
[_nui nui_initialize:[initParam UTF8String] logLevel:LOG_LEVEL_VERBOSE saveLog:save_log];
```

其中，genInitParams生成为String JSON字符串，包含资源目录和用户信息。其中用户信息包含如下字段，获取方式请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/overview-3 "")。

```cpp
-(NSString*) genInitParams {
    NSString *strResourcesBundle = [[NSBundle mainBundle] pathForResource:@"Resources" ofType:@"bundle"];
    NSString *bundlePath = [[NSBundle bundleWithPath:strResourcesBundle] resourcePath];
    NSString *debug_path = [_utils createDir];

    NSMutableDictionary *ticketJsonDict = [NSMutableDictionary dictionary];

    //获取账号访问凭证：
    //  getTicket为示例工程中提供了多种可能的方式，请选择适合自身业务的安全方式
    //
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
    [_utils getTicket:ticketJsonDict Type:get_token_from_server_for_online_features];
    if ([ticketJsonDict objectForKey:@"token"] != nil) {
        NSString *tokenValue = [ticketJsonDict objectForKey:@"token"];
        if ([tokenValue length] == 0) {
            TLog(@"The 'token' key exists but the value is empty.");
        }
    } else {
        TLog(@"The 'token' key does not exist.");
    }

    [ticketJsonDict setObject:@"wss://nls-gateway.cn-shanghai.aliyuncs.com:443/ws/v1" forKey:@"url"]; // 默认

    //工作目录路径，SDK从该路径读取配置文件
    [ticketJsonDict setObject:bundlePath forKey:@"workspace"]; // 必填
    //当初始化SDK时的save_log参数取值为true时，该参数生效。表示是否保存音频debug，该数据保存在debug目录中，需要确保debug_path有效可写
    [ticketJsonDict setObject:save_wav ? @"true" : @"false" forKey:@"save_wav"];
    //debug目录，当初始化SDK时的save_log参数取值为true时，该目录用于保存中间音频文件
    [ticketJsonDict setObject:debug_path forKey:@"debug_path"];

    //AsrCloud = 4  // 在线一句话识别可以选这个
    [ticketJsonDict setObject:@"4" forKey:@"service_mode"]; // 必填

    NSString *id_string = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
    TLog(@"id: %s", [id_string UTF8String]);
    [ticketJsonDict setObject:id_string forKey:@"device_id"]; // 必填, 推荐填入具有唯一性的id, 方便定位问题

    NSData *data = [NSJSONSerialization dataWithJSONObject:ticketJsonDict options:NSJSONWritingPrettyPrinted error:nil];
    NSString * jsonStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
    return jsonStr;
}
```

### **参数设置**

以JSON字符串形式进行设置。

```cpp
-(NSString*) genParams {
    NSMutableDictionary *nls_config = [NSMutableDictionary dictionary];
    [nls_config setValue:@YES forKey:@"enable_intermediate_result"]; // 必填
    //参数可根据实际业务进行配置
    //接口说明可见: https://help.aliyun.com/document_detail/173298.html
    //查看 2.开始识别

    //由于对外的SDK(01B版本)不带有本地VAD模块(仅带有唤醒功能(029版本)的SDK具有VAD模块)，
    //若要使用VAD模式，则需要设置nls_config参数启动在线VAD模式(见genParams())
    //
    //模式说明：
    //若使用P2T模式，即按下开始说话，放开结束说话的模式，则不启动enable_voice_detection。
    //若使用VAD模式，即自动判断用户说完一句话，则启动enable_voice_detection。
    //[nls_config setValue:@YES forKey:@"enable_voice_detection"];
    //[nls_config setValue:@10000 forKey:@"max_start_silence"];
    //[nls_config setValue:@800 forKey:@"max_end_silence"];

    //[nls_config setValue:@"<更新token>" forKey:@"token"];
    //[nls_config setValue:@YES forKey:@"enable_punctuation_prediction"];
    //[nls_config setValue:@YES forKey:@"enable_inverse_text_normalization"];
    //[nls_config setValue:@16000 forKey:@"sample_rate"];
    //[nls_config setValue:@"opus" forKey:@"sr_format"];

    NSMutableDictionary *dictM = [NSMutableDictionary dictionary];
    [dictM setObject:nls_config forKey:@"nls_config"];
    [dictM setValue:@(SERVICE_TYPE_ASR) forKey:@"service_type"]; // 必填

    //如果有HttpDns则可进行设置
    //[dictM setObject:[_utils getDirectIp] forKey:@"direct_ip"];

    /*若文档中不包含某些参数，但是此功能支持这个参数，可以用如下万能接口设置参数*/
    //NSMutableDictionary *extend_config = [NSMutableDictionary dictionary];
    //[extend_config setValue:@YES forKey:@"custom_test"];
    //[dictM setObject:extend_config forKey:@"extend_config"];

    NSData *data = [NSJSONSerialization dataWithJSONObject:dictM options:NSJSONWritingPrettyPrinted error:nil];
    NSString * jsonStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
    return jsonStr;
}

NSString * parameters = [self genParams];
[_nui nui_set_params:[parameters UTF8String]];
```

### **开始识别**

通过nui\_dialog\_start接口开启监听。

```cpp
-(NSString*) genDialogParams {
    NSMutableDictionary *dialog_params = [NSMutableDictionary dictionary];
    // 运行过程中可以在nui_dialog_start时更新临时参数，尤其是更新过期token
    // 注意: 若下一轮对话不再设置参数，则继续使用初始化时传入的参数
//    [dialog_params setValue:@"" forKey:@"app_key"];
//    [dialog_params setValue:@"" forKey:@"token"];

    NSData *data = [NSJSONSerialization dataWithJSONObject:dialog_params options:NSJSONWritingPrettyPrinted error:nil];
    NSString * jsonStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
    return jsonStr;
}

//若需要修改token等参数, 可详见genDialogParams()
NSString * parameters = [self genDialogParams];
//若要使用VAD模式，则需要设置nls_config参数启动在线VAD模式(见genParams())
[_nui nui_dialog_start:MODE_P2T dialogParam:[parameters UTF8String]];
```

### **回调处理**

- **onNuiAudioStateChanged**：录音状态回调，SDK内部维护录音状态，调用时根据该状态的回调进行录音机的开关操作。















```cpp
  -(void)onNuiAudioStateChanged:(NuiAudioState)state{
      TLog(@"onNuiAudioStateChanged state=%u", state);
      if (state == STATE_CLOSE || state == STATE_PAUSE) {
          // 旧版本示例工程提供的录音模块，仅做参考，可根据自身业务重写录音模块。
          // [_voiceRecorder stop:YES];

          // 新版本示例工程提供了新的录音模块，仅做参考，可根据自身业务重写录音模块。
          [_audioController stopRecorder:NO];
      } else if (state == STATE_OPEN){
          self.recordedVoiceData = [NSMutableData data];
          // 旧版本示例工程提供的录音模块，仅做参考，可根据自身业务重写录音模块。
          // [_voiceRecorder start];

          // 新版本示例工程提供了新的录音模块，仅做参考，可根据自身业务重写录音模块。
          [_audioController startRecorder];
      }
}
```

- **onNuiNeedAudioData**：录音数据回调，在该回调中填充录音数据。















```cpp
  -(int)onNuiNeedAudioData:(char *)audioData length:(int)len {
      static int emptyCount = 0;
      @autoreleasepool {
          @synchronized(_recordedVoiceData){
              if (_recordedVoiceData.length > 0) {
                  int recorder_len = 0;
                  if (_recordedVoiceData.length > len)
                      recorder_len = len;
                  else
                      recorder_len = _recordedVoiceData.length;
                  NSData *tempData = [_recordedVoiceData subdataWithRange:NSMakeRange(0, recorder_len)];
                  [tempData getBytes:audioData length:recorder_len];
                  tempData = nil;
                  NSInteger remainLength = _recordedVoiceData.length - recorder_len;
                  NSRange range = NSMakeRange(recorder_len, remainLength);
                  [_recordedVoiceData setData:[_recordedVoiceData subdataWithRange:range]];
                  emptyCount = 0;
                  return recorder_len;
              } else {
                  if (emptyCount++ >= 50) {
                      TLog(@"_recordedVoiceData length = %lu! empty 50times.", (unsigned long)_recordedVoiceData.length);
                      emptyCount = 0;
                  }
                  return 0;
              }
          }
      }
      return 0;
}
```

- **onNuiEventCallback**：NUI SDK事件回调，请勿在事件回调中调用SDK的接口，可能引起死锁。















```cpp
  -(void)onNuiEventCallback:(NuiCallbackEvent)nuiEvent
                     dialog:(long)dialog
                  kwsResult:(const char *)wuw
                  asrResult:(const char *)asr_result
                   ifFinish:(bool)finish
                    retCode:(int)code {
      TLog(@"onNuiEventCallback event %d finish %d", nuiEvent, finish);
      if (nuiEvent == EVENT_ASR_PARTIAL_RESULT || nuiEvent == EVENT_ASR_RESULT) {
          // asr_result在此包含task_id，task_id有助于排查问题，请用户进行记录保存。
          TLog(@"ASR RESULT %s finish %d", asr_result, finish);
          NSString *result = [NSString stringWithUTF8String:asr_result];
      } else if (nuiEvent == EVENT_ASR_ERROR) {
          // asr_result在EVENT_ASR_ERROR中为错误信息，搭配错误码code和其中的task_id更易排查问题，请用户进行记录保存。
          TLog(@"EVENT_ASR_ERROR error[%d], error mesg[%s]", code, asr_result);

          // 可通过nui_get_all_response获得完整的信息
          const char *response = [_nui nui_get_all_response];
          if (response != NULL) {
              TLog(@"GET ALL RESPONSE: %s", response);
          }
      } else if (nuiEvent == EVENT_MIC_ERROR) {
          TLog(@"MIC ERROR");
          // 旧版本示例工程提供的录音模块，仅做参考，可根据自身业务重写录音模块。
          // [_voiceRecorder stop:YES];
          // [_voiceRecorder start];

          // 新版本示例工程提供了新的录音模块，仅做参考，可根据自身业务重写录音模块。
          [_audioController stopRecorder:NO];
          [_audioController startRecorder];
      }

      //finish 为真（可能是发生错误，也可能是完成识别）表示一次任务生命周期结束，可以开始新的识别
      if (finish) {
      }

      return;
}
```


### **结束识别**

```cpp
[_nui nui_dialog_cancel:NO];
```

## 常见问题

### iOS SDK使用一句话识别功能，集成nuisdk.framework，按照文档在工程Build Phases的Link Binary With Libraries中添加nuisdk.framework，在编译配置的General > Frameworks, Libraries, and Embedded Content中配置nuisdk.framework为Embed & Sign，但.m中仍提示找不到 nuisdk.framework/Headers/NeoNui.h如何解决？

请检查头文件#import <nuisdk/NeoNui.h>是否按照文档正常导入。

### 是否有Android和iOS的SDK，能否用在专有云环境下？

有SDK，在专有云安装包里默认不提供，可以通过阿里云帮助中心对应的服务文档中下载，如实时语音识别的 [Android SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-android-1#topic-1917930 "") 和 [iOS SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-ios#topic-1917931 "")。移动端SDK可以调用公共云ASR、TTS服务，也可以用在专有云环境下。

### iOS是否支持后台处理？

SDK本身不限制前后台，iOS SDK的样例工程默认仅支持前台处理，如果您需要支持后台处理，可以做如下修改：

1. 在工程Info.list中添加 **Required background modes** 配置，并在该配置下添加 **Item**，Value设置为 **App plays audio or streams audio/video using AirPlay**。![配置1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1356988061/p206201.png)

2. 在录音模块中进入后台时，不停止录音。亦即NLSVoiceRecorder.m中\_appResignActive接口中不做停止录音调用。![配置2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1356988061/p206203.png)


### 下载语音交互iOS SDK至本地静态库，运行Demo程序测试代码时，模拟器可以正常运行，真机无法运行，报错“Reason: no suitable image found. Did find:xxx”如何解决？

建议您删除手机上对应的APP后，执行`xcode clean`，并重新尝试运行。除此以外，还需检查签名的正确性，如果签名不正确，需撤销原来的inHouse证书，重新制作新的证书和provisioning profile，并将代码重新签名，再次打包。

### iOS端集成nuisdk运行报mic错误如何处理？

请检查当前录音设备是否被占用。

### 使用智能语音服务集成iOS SDK，接入nuisdk.framework后，导入头文件\#import "nuisdk.framework/Headers/NeoNui.h"后项目报错如何解决？

一般情况下是SDK导入有问题导致，请您确认下图参数是否已勾选，如果已勾选，建议您将头文件导入方式换为`#import <nuisdk/NeoNui.h>`。![ios导入头部文件失败](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4271970661/p478647.png)

### 按照文档使用SDK接入后报错“/Users/admin/FlashTranscription\_iOS/Fc\_ASR.xcodeproj Building for iOS, but the linked and embedded framework 'nuisdk.framework' was built for iOS + iOS Simulator."”如何解决？

可能因为版本过高导致，建议您修改项目配置 **Validate Workspace** 为 **Yes** 后，重新编译。![按照文档使用SDK接入后报错](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4271970661/p478653.png)

### 使用集成语音服务iOS SDK，集成flutter\_plugin时报错“Undefined symbols for architecture arm64: "std::\_\_1::mutex::~mutex()", referenced from: \_\_\_cxx\_global\_var\_init in libflutter\_tts.a(ringBuf.o)”如何解决？

您可以打开iOS工程下的Podfile文件，修改`post_install do |installer|`部分的代码，再次执行构建即可成功。

![集成语音服务报错](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0157780661/p478665.png)

### TRTC实时音视频和语音识别结合，当同时调用麦克风时可能会发生冲突，导致有一方没有声音如何解决？

建议尝试TRTC的音视频流，使用`localStream.getAudioTrack`获取`MediaStreamTrack`对象，并转换为符合ASR标准的音频流，然后通过语音识别SDK发起请求。

### 使用App集成iOS SDK，提交到App store失败，提示“Unsupported Architectures. The executable for AliYunSmart.app/Frameworks/nuisdk.framework contains unsupported architectures '\[x86\_ \_64, i386\]'. With error code”如何解决？

可能是模拟器架构影响，您可以参考如下方法查看framework版本并移除framework模拟器架构。

1. 进入framework目录。

2. 输入命令`lipo -info xxxFramework`，查看framework的架构版本，如果含有模拟器打包需要把模拟器架构移除。


### 使用集成语音服务iOS SDK，接入nuisdk.framework后报错，要修改Legacy Build system才可以运行，如何解决？

建议您修改项目配置 **Validate Workspace** 为 **Yes** 后，重新编译。![按照文档使用SDK接入后报错](<Base64-Image-Removed>)