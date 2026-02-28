### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/)

# iOS SDK

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

本文为您介绍如何使用阿里云智能语音服务提供的iOS NUI SDK，包括SDK下载安装、关键接口及代码示例。

## 前提条件

- 使用SDK前，首先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/sdk-reference-12 "")。

- 已准备项目账号等信息，详情请参见 [开通授权](https://help.aliyun.com/zh/isi/enable-authorization-1 "")。


## 下载安装

1. [移动端SDK选择与下载](https://help.aliyun.com/zh/isi/sdk-selection-and-download "")。







**说明**

请下载后在样例初始化代码中替换您的阿里云账号信息、Appkey和Token才可运行。为方便集成，2.5.14版本后iOS接口使用纯Object-C接口，不再使用C++混合接口。

2. 解压ZIP包，将zip包中的nuisdk.framework添加到您到工程中，并在工程Build Phases的Link Binary With Libraries中添加nuisdk.framework。

3. 使用Xcode打开此工程，工程中提供了参考代码以及一些直接可使用的工具类，例如音频播放录制和文件操作，您可以直接复制源码到您的实际工程进行使用。

其中，唤醒后进行一句话识别即唤醒识别的场景示例代码可参考WakeupAndSpeechRecognizerViewController.mm文件，单纯唤醒的场景示例代码可参考OnlyWakeupViewController.mm（2.6.4版本新增）。


## SDK关键接口

- **nui\_initialize**：初始化SDK。


```objectc
    /**
     * 初始化SDK，SDK为单例，请先释放后再次进行初始化。请勿在UI线程调用，可能引起阻塞。
     * @param parameters: 初始化参数，参见接口说明文档https://help.aliyun.com/zh/isi/sdk-reference-12
     * @param level: log打印级别，值越小打印越多
     * @param save_log: 是否保存log为文件，存储目录为parameter中的debug_path字段值，log日志最大上限详见max_log_file_size【V2.6.4新增】。
     * @return 参考错误码:https://help.aliyun.com/document_detail/459864.html
     */
  -(NuiResultCode) nui_initialize:(const char *)parameters
                         logLevel:(NuiSdkLogLevel)level
                          saveLog:(BOOL)save_log;
```

- **nui\_set\_params**：以JSON格式设置SDK参数。


```objectc
/**
* 以JSON格式设置参数
* @param params: 参数信息请参见接口说明文档https://help.aliyun.com/zh/isi/sdk-reference-12
* @return 参考错误码:https://help.aliyun.com/document_detail/459864.html
*/
  -(NuiResultCode) nui_set_params:(const char *)params;
```

- **nui\_dialog\_start**：开始识别。


```objectc
/**
* 开始识别
* @param vad_mode: 多种模式，对于唤醒后识别的场景，则用MODE_KWS；若只使用唤醒功能，则用MODE_ONLY_KWS
* @param dialog_params: 设置识别参数，可不设置
* @return 参考错误码:https://help.aliyun.com/document_detail/459864.html
*/
  -(NuiResultCode) nui_dialog_start:(NuiVadMode)vad_mode
                        dialogParam:(const char *)dialog_params;
```

- **nui\_dialog\_cancel**：结束识别。


```objectc
/**
* 结束识别，调用该接口后，服务端将返回最终识别结果并结束任务
* @param force: 是否强制结束而忽略最终结果，NO表示停止但是等待完整结果返回
* @return 参考错误码:https://help.aliyun.com/document_detail/459864.html
*/
  -(NuiResultCode) nui_dialog_cancel:(BOOL)force;
```

- **nui\_get\_version**：获得SDK版本信息。


```objectc
/**
* 获得SDK版本号
*/
  -(const char*) nui_get_version;
```

- **nui\_get\_all\_response**：获得事件返回的完整信息（2.6.0版本新增）。


```objectc
/**
* onNuiEventCallback触发时可通过此接口获得完整的返回信息，便于定位问题
*/
  -(const char*) nui_get_all_response;
```

- **nui\_release**：释放SDK。


```objectc
/**
* 释放SDK资源
* @return 参考错误码:https://help.aliyun.com/document_detail/459864.html
*/
  -(NuiResultCode) nui_release;
```

- **NeoNuiSdkDelegate**：事件代理。

  - onNuiEventCallback：SDK事件回调。


    ```java
    /**
     * SDK主要事件回调
     * @param event: 回调事件，参见如下事件列表
     * @param dialog: 会话编号，暂不使用
     * @param wuw: 语音唤醒功能使用
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

  - onNuiNeedAudioData：获取音频。


    ```objectc
    /**
     * 开始识别时，此回调被连续调用，App需要在回调中进行语音数据填充
     * @param buffer:  填充语音的存储区
     * @param len: 需要填充语音的字节数
     * @return 实际填充的字节数
     */
    -(int) onNuiNeedAudioData:(char *)audioData length:(int)len;
    ```

  - onNuiAudioStateChanged：根据音频状态进行录音功能的开关。


    ```objectc
    /**
     * 当start/stop/cancel等接口调用时，SDK通过此回调通知App进行录音的开关操作
     * @param user_data: 初始化listener的user_data值
     * @param state：录音需要的状态（打开/关闭）
     */
    -(void) onNuiAudioStateChanged:(NuiAudioState)state;
    ```

  - onNuiRmsChanged：音频能量事件。


    ```objectc
    /**
     * SDK主要事件回调
     * @param rms: 语音能量值，范围为-160至0
     */
    -(void) onNuiRmsChanged:(float) rms;
    ```

  - onNuiLogTrackCallback：SDK内部日志回调（2.6.4版本新增）。


    ```objectc
    /**
     * SDK内部日志回调。
     * @param level: 大于此日志级别的SDK内部日志将通过此回调送出
     * @param log: 具体的日志内容
     */
    -(void) onNuiLogTrackCallback:(NuiSdkLogLevel)level
                       logMessage:(const char *)log;
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


## 代码示例

**NUI SDK初始化**

```objectc
//请注意此处的参数配置，其中账号相关需要按照genInitParams的说明填入后才可访问服务
NSString * initParam = [self genInitParams];
[_nui nui_initialize:[initParam UTF8String] logLevel:LOG_LEVEL_VERBOSE saveLog:save_log];
```

其中，genInitParams生成为String JSON字符串，包含资源目录和用户信息。主要包含如下字段：

```java
-(NSString*) genInitParams {
    NSString *strResourcesBundle = [[NSBundle mainBundle] pathForResource:@"Resources" ofType:@"bundle"];
    NSString *bundlePath = [[NSBundle bundleWithPath:strResourcesBundle] resourcePath];
    NSString *debug_path = [_utils createDir];
    NSMutableDictionary *dictM = [NSMutableDictionary dictionary];

    //账号和项目创建
    // 需要特别注意：ak_id/ak_secret/app_key/sdk_code/device_id等参数必须传入SDK
    // 离线语音合成sdk_code取值：精品版为software_nls_tts_offline， 标准版为software_nls_tts_offline_standard
    // 离线语音合成账户的sdk_code也可用于唤醒
    // 鉴权信息获取参：https://help.aliyun.com/document_detail/69835.htm?spm=a2c4g.11186623.2.28.10b33069T2ydLk#topic-1917889

    //获取账号访问凭证：
    // 注意！此.mm是唤醒+一句话识别的功能演示，包含离线唤醒功能和在线识别功能，
    // 所以账号方案需要mixed方案，或者创建两个Appkey分别用户唤醒功能和在线功能。
    [_utils getTicket:dictM Type:get_sts_access_from_server_for_mixed_features];

    //请参照阿里云官网获取鉴权信息获取配额
    //  https://help.aliyun.com/document_detail/251488.html?spm=a2c4g.11186623.6.638.1f0d530eut95Jn
    //  如果配额已耗尽，请联系客户扩大配额
    //  如果合成失败，通常是由于鉴权失败，可以参照阿里云官网Q&A部分
    //  https://help.aliyun.com/document_detail/204191.html?spm=a2c4g.11186623.6.657.3cde7340qMll1h ，根据错误日志判别导致鉴权失败的原因

    [dictM setObject:@"wss://nls-gateway.cn-shanghai.aliyuncs.com:443/ws/v1" forKey:@"url"];

    [dictM setObject:bundlePath forKey:@"workspace"];
    [dictM setObject:debug_path forKey:@"debug_path"];
    [dictM setObject:save_wav ? @"true" : @"false" forKey:@"save_wav"];

    //过滤SDK内部日志通过回调送回到用户层
    [dictM setObject:[NSString stringWithFormat:@"%d", NUI_LOG_LEVEL_INFO] forKey:@"log_track_level"];
    //设置本地存储日志文件的最大字节数, 最大将会在本地存储2个设置字节大小的日志文件
    [dictM setObject:@(50 * 1024 * 1024) forKey:@"max_log_file_size"];

    // 特别说明: 鉴权所用的id是由以下device_id，与手机内部的一些唯一码进行组合加密生成的。
    //   更换手机或者更换device_id都会导致重新鉴权计费。
    //   此外, 以下device_id请设置有意义且具有唯一性的id, 比如用户账号(手机号、IMEI等),
    //   传入相同或随机变换的device_id会导致鉴权失败或重复收费。
    //   NSString *id_string = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString]; 并不能保证生成不变的device_id，请不要使用
    [dictM setObject:@"empty_device_id" forKey:@"device_id"]; // 必填

    //如果使用外部唤醒资源，在此设置模型文件路径参数
    // 举例1：模型文件pack_kws.bin可以放在thirdparty
//    NSString *file = [[NSBundle mainBundle] pathForResource:@"thirdparty/pack_kws" ofType:@"bin"];
//    [dictM setObject:file forKey:@"upgrade_file"];

    NSData *data = [NSJSONSerialization dataWithJSONObject:dictM options:NSJSONWritingPrettyPrinted error:nil];
    NSString * jsonStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
    return jsonStr;
}
```

**参数设置**

以JSON字符串形式进行设置。

```objectc
-(NSString*) genParams {
    NSMutableDictionary *nls_config = [NSMutableDictionary dictionary];
    [nls_config setValue:@YES forKey:@"enable_intermediate_result"];
//    参数可根据实际业务进行配置
//    [nls_config setValue:@YES forKey:@"enable_punctuation_prediction"];
//    [nls_config setValue:@YES forKey:@"enable_inverse_text_normalization"];
//    [nls_config setValue:@YES forKey:@"enable_voice_detection"];
//    [nls_config setValue:@10000 forKey:@"max_start_silence"];
//    [nls_config setValue:@800 forKey:@"max_end_silence"];
//    [nls_config setValue:@16000 forKey:@"sample_rate"];
//    [nls_config setValue:@"opus" forKey:@"sr_format"];
    NSMutableDictionary *dictM = [NSMutableDictionary dictionary];
    [dictM setObject:nls_config forKey:@"nls_config"];
    [dictM setValue:@(SERVICE_TYPE_ASR) forKey:@"service_type"];

    /*若文档中不包含某些参数，但是此功能支持这个参数，可以用如下万能接口设置参数*/
//    NSMutableDictionary *extend_config = [NSMutableDictionary dictionary];
//    [extend_config setValue:@YES forKey:@"custom_test"];
//    [dictM setObject:extend_config forKey:@"extend_config"];

//    可以通过以下方式设置自定义唤醒词进行体验，如果需要更好的唤醒效果请进行唤醒词定制
//    注意：动态唤醒词只有在设置了唤醒模型的前提下才可以使用
    NSMutableDictionary *dictWuw = [NSMutableDictionary dictionary];
    [dictWuw setObject:@"小白小白" forKey:@"name"];
    [dictWuw setObject:@"main" forKey:@"type"];
    NSMutableArray *wuwArray = [[NSMutableArray alloc] init];
    [wuwArray addObject:dictWuw];
    [dictM setObject:wuwArray forKey:@"wuw"];

//    如果有HttpDns则可进行设置
//    [dictM setObject:[_utils getDirectIp] forKey:@"direct_ip"];

    NSData *data = [NSJSONSerialization dataWithJSONObject:dictM options:NSJSONWritingPrettyPrinted error:nil];
    NSString * jsonStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
    return jsonStr;
}

NSString * parameters = [self genParams];
[_nui nui_set_params:[parameters UTF8String]];
```

**开始识别**

通过startDialog接口开启监听。

```objectc
// 唤醒后立即一句话识别，选择MODE_KWS
// 只用唤醒功能，选择MODE_ONLY_KWS
[_nui nui_dialog_start:MODE_KWS dialogParam:[param_string UTF8String]];
```

**回调处理**

- onNuiAudioStateChanged：录音状态回调，SDK内部维护录音状态，调用时根据该状态的回调进行录音机的开关操作。


```objectc
  -(void)onNuiAudioStateChanged:(NuiAudioState)state{
      TLog(@"onNuiAudioStateChanged state=%u", state);
      if (state == STATE_CLOSE || state == STATE_PAUSE) {
          if (_audioController != nil) {
              [_audioController stopRecorder:NO];
          }
      } else if (state == STATE_OPEN){
          self.recordedVoiceData = [NSMutableData data];
          if (_audioController != nil) {
              [_audioController startRecorder];
          }
      }
}
```

- onNuiNeedAudioData：录音数据回调，在该回调中填充录音数据。


```java
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

- onNuiEventCallback：NUI SDK事件回调，请勿在事件回调中调用SDK的接口，可能引起死锁。


```objectc
  -(void)onNuiEventCallback:(NuiCallbackEvent)nuiEvent
                     dialog:(long)dialog
                  kwsResult:(const char *)wuw
                  asrResult:(const char *)asr_result
                   ifFinish:(BOOL)finish
                    retCode:(int)code {
      TLog(@"onNuiEventCallback event %d finish %d", nuiEvent, finish);
      if (nuiEvent == EVENT_WUW_TRUSTED) {
          NSString *result = [NSString stringWithUTF8String:wuw];
          TLog(@"EVENT_WUW %s", wuw);
          [myself showKwsResult:result];
      } else if (nuiEvent == EVENT_ASR_PARTIAL_RESULT || nuiEvent == EVENT_ASR_RESULT) {
          TLog(@"ASR RESULT %s finish %d", asr_result, finish);
          NSString *result = [NSString stringWithUTF8String:asr_result];
          [myself showAsrResult:result];
      } else if (nuiEvent == EVENT_ASR_ERROR) {
          TLog(@"EVENT_ASR_ERROR error[%d]", code);
      } else if (nuiEvent == EVENT_MIC_ERROR) {
          TLog(@"MIC ERROR");
          if (_audioController != nil) {
              [_audioController stopRecorder:NO];
              [_audioController startRecorder];
          }
      }

      if (finish) {
          dispatch_async(dispatch_get_main_queue(), ^{
              // UI更新代码
              [myself->StartButton setEnabled:YES];
              [myself->StartButton setAlpha:1.0];
              [myself->StopButton setEnabled:NO];
              [myself->StopButton setAlpha:0.4];
          });
      }

      return;
}
```


**停止识别**

```objectc
[_nui nui_dialog_cancel:NO];
```

**取消识别**

```objectc
[_nui nui_dialog_cancel:YES];
```