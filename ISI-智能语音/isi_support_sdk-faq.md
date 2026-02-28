### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[服务支持](https://help.aliyun.com/zh/isi/support/)[常见问题](https://help.aliyun.com/zh/isi/support/faq/)SDK FAQ

# SDK FAQ

更新时间：2024-04-01 22:26:50

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：语音合成FAQ](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis)[下一篇：计费定价FAQ](https://help.aliyun.com/zh/isi/support/faq-about-billing-and-pricing)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

公共类

如何使用SDK设置泛热词？

SDK报错“DNS resolved timeout”是什么问题？

如何使用SDK设置自学习模型？

是否有Android和iOS的SDK，能否用在专有云下？

Token如何使用？

Token重新获取会不会导致已获取的Token失效？

是否可以提供服务的IP白名单？

如何进行log控制与音频保存?

调用上有什么限制？

为什么链接不到framework？

SDK错误事件如何定位原因？

Java SDK类

一句话识别、实时语音识别SDK中，send接口参数含义及使用方式？

如何结合SDK日志，分析延迟问题？

Java SDK找不到com.alibaba的JAR包，如何安装Alibaba Cloud SDK for Java？

使用Java SDK调用SpeechRecognizer.stop方法时出现连接超时，提示timeout after 10 seconds waiting for complete confirmation. state:STATE\_STOP\_SENT如何解决？

录音文件转写接口Java SDK Demo运行报错如何排查？

实时语音识别使用Java SDK，SpeechRecognizer recognizer如何调用stop()实现通知服务端语音数据发送完毕？

实时流识别模式，Java SDK中如何触发回调onTranscriptionComplete？

调用Java SDK时报错，提示java.lang.IllegalStateException: complete already: DefaultChannelPromise@75822ea8(failure: java.lang.Exception: WebSocket Client failed to connect,status:403 Forbidden,reason:Meta:ACCESS\_DENIED:The token '\*\*\*' is invalid!)"如何解决？

在生成synthesizer = new SpeechSynthesizer时一直失败，提示java.nio.channels.ClosedChannelException如何解决？

在测试实时语音识别和语音合成功能时，对应JAR包在哪里？

Java SDK实时识别NlsClient类去连接server报错， 提示ERROR NlsClient:102 - failed to connect to server after 3 tries,error msg is :hostname can't be null如何解决？

Java SDK语音合成报错，提示java.nio.channels.ClosedChannelException at io.netty.channel.AbstractChannel$AbstractUnsafe.ensureOpen(...)如何解决？

Java SDK通过传入阿里云账号的AccessKey ID和AccessKey Secret，调用阿里云Java SDK得到client提示错误org.json.JSONArray.iterator()Ljava/util/Iterator如何解决？

Java版SDK可以直接提供上传音频文件的方式进行识别吗？

使用Java Demo识别录音文件没有识别结果，使用文档中的语音文件识别可以正常识别，该如何解决？

C++ SDK类

C++ SDK语音合成时传入的文本没有采用UTF-8编码会有什么错误信息？

C++ SDK如何获取Token？

C++ SDK调用智能实时语音解析接口失败，提示 {"TaskFailed":"connect failed."} {"channeclClosed": "nls request finished."}如何解决？

C++ SDK进行语音合成时，报错未设置appkey，但是代码已经设置该如何解决？OnSynthesisTaskFailed: status code=10000002 task id=\*\*\*error message={TaskFailed":"{"task\_id":"00000000000000000000000000000000","result":"","status":40000003,"message":"Gateway:PARAMETER\_INVALID:appkey not set"}"}"

C++ SDK（3.0及以后版本）使用语音合成和语音识别功能，可以提高GCC5.0以上的编译版本吗？

C++ SDK中的speechRecognizerDemo.cpp中的g\_akid和g\_akSecret在哪里获取？

C++ SDK实时语音识别报错，提示status\_text:Gateway:IDLE\_TIMEOUT:Websocket session is idle for too long time, the last directive is 'StartTranscription'!如何解决？

C++ SDK获取Token，当系统的时间不是标准时间时会获取失败，在C++ SDK中，可以自己设置timestamp，而不是获取系统的时间吗？

C++ SDK ASR请求有DNS解析失败的情况导致异常，报错ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): GetInetAddressByHostname:252 DNS: resolved timeout.ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): start:76 start failed: DNS: resolved timeout..unimrcpserver\_current.log: \[ERROR\] \[\[./ali/AliRecogChannel.cpp:772,onTaskFailed\]\]Ali Task start failed Msg :DNS: resolved timeout., start finised."如何解决？

C++ SDK调用实时语音识别，集成在mrcp里面使用，部分情况下创建多个识别通道时会返回10000002如何解决？

C++ SDK（新）集成到其他项目中时，将CMakeLists.txt中的add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=0) 修改为add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=1)后编译不通过该如何解决？

C++ SDK在Windows上使用，报错缺少nlsCommonSdk.dll如何解决？

C++ SDK旧版NlsSdkCpp2.0和新版NlsSdkCpp3.X的区别是什么？

C++版的SDK不支持实现C11规范吗？ 现在导致项目无法链接SDK该如何解决？

C++ 版SDK集成语音识别报错，提示Meta:ACCESS\_DENIED:The token '' is invalid!, start finised.start() failed.CbParam: 1 exg.onTaskFailed: status code: 10000011, error message: Stop invoke error. Please check the order of execution or whether the data sent is valid.如何解决？

C++ 版SDK集成语音识别一句话报错，提示transcriber process start...alispeech-DEBUG start:60 starting transcriber...alispeech-WARNING \_on\_error:123 retry start: \[SSL: CERTIFICATE\_VERIFY\_FAILED\] certificate verify failed (\_ssl.c:852)alispeech-DEBUG \_on\_close:110 callback on\_channel\_closedMyCallback.OnRecognitionChannelClosed如何解决？

C++ SDK一句话识别调用stop后返回错误回调状态码40000004该如何解决？{"header":{"namespace":"Default","name":"TaskFailed","status":40000004,"message\_id":"xxxxxxxxxxxxxxxxxxxxxxxxx","task\_id":"xxxxxxxxxxxxxxxxxxxxxxxxx","status\_text":"Gateway:IDLE\_TIMEOUT:Websocket session is idle for too long time, the last directive is 'StopRecognition'!"}}

C++ SDK测试Demo成功，集成项目报错，DNS解析失败，报错nls-gateway-cn-shanghai.aliyuncs.com dns failed: nodename nor servname provided, or not known如何解决？

C++ SDK测试Demo可以成功，集成项目报错，网络链接失败，报错\[dnsEventCallback:465\]Node:0x7f087c001030 ai\_canonname: nls-gateway-cn-shanghai.aliyuncs.com.gds.alibabadns.com\[dnsEventCallback:477\]Node:0x7f087c001030 IpV4:106.15.XX.XX\[connectProcess:1329\]Node:0x7f087c001030 sockFd:41\[connectProcess:1347\]Node:0x7f087c001030 new Socket ip:106.15.XX.XX port:443 Fd:41.\[socketConnect:1458\]Node:0x7f087c001030 Connect failed:Network is unreachable. retry...如何解决？

C++ 语音合成Demo，NlsCommonSdk版本20211018基于vc16.0，NlsSdkCpp3.X版本20210629基于vc14.0，Demo程序只执行到OnSynthesisTaskFailed，返回20000000，在win10 X64 vs2015中得不到WAV的可能原因？log信息如下ERROR alibabaNlsLog: \[ID:15284\]\[AlibabaNls::ConnectNode::parseFrame:1014\]Node:000001D733079F20 Result conversion failed.

Android SDK类

Android SDK是否可以上传opus音频数据，实现实时语音转文字？

Android SDK中使用onNuiNeedAudioData录音数据回调，并在该回调过程中填充录音数据ret = audioRecord.read(buffer, 0, len)。在实时录音转写过程中，突然断网后再连网，录音SDK会自动连接并继续转写吗？

智能语音交互SDK，最低支持Android的哪个版本？

Android SDK录音文件识别极速版，是否支持通过任务ID查询任务状态？

Android SDK调用文件上传转写极速版，调用int startFileTranscriber(String params, byte\[\] task\_id)后无法收到回调，报错提示“EventE/iDST::NativeNui: no java instance, maybe already released”。

使用实时语音识别Android SDK，管控台模型选择为8K，但是实际测试中为何将采样率设置成16K才能识别正确？

int ret = nui\_instance.initialize(this, genInitParams(assets\_path,debug\_path), Constants.LogLevel.LOG\_LEVEL\_VERBOSE, true)。在该段代码中，录音权限是打开的，但代码仍然报错240021。

使用离线语音合成Android SDK，语音播报时出现不合理断句，该如何处理？

使用语音合成Android SDK，在调用cancel时候出现一次anr，该如何处理？

实时音频识别对Android版本有要求吗？

调用Android SDK时，手机报错提示“audio recoder not init”。

在模拟器上运行下载的Android程序，程序出现闪退现象，是什么原因？

使用语音识别Android SDK回调onNuiNeedAudioData，但在onNuiEventCallback中回调延迟，并显示错误码50000000。

使用语音合成Android SDK TTS时，报错提示“tts event:TTS\_EVENT\_ERROR ret 140002”。

不能正常使用语音合成Android SDK。

iOS SDK类

是否支持后台处理？

下载语音交互iOS SDK至本地库，测试代码时，在模拟器可以正常运行，真机却无法运行，报错提示“Reason: no suitable image found. Did find:xxx”。

使用智能语音服务集成iOS SDK，接入NuiSdk运行报错MIC。

使用智能语音服务集成iOS SDK，接入nuisdk.framework后，导入头文件项目失败。

使用iOS SDK接入nuisdk.framework后，报错提示“/Users/admin/FlashTranscription\_iOS/Fc\_ASR.xcodeproj Building for iOS, but the linked and embedded framework 'nuisdk.framework' was built for iOS + iOS Simulator”。

使用集成语音服务iOS SDK，在接入nuisdk.framework后报错，需要修改Legacy Build system，才可以运行，是什么原因？

使用一句话识别iOS SDK，配置nuisdk.framework为Embed & Sign后，提示“nuisdk.framework/Headers/NeoNui.h”。

使用App集成iOS SDK，提交到App store失败，提示“Unsupported Architectures. The executable for AliYunSmart.app/Frameworks/nuisdk.framework contains unsupported architectures '\[x86\_ \_64, i386\]'. With error code”。

TRTC实时音视频和语音识别结合，当同时调用麦克风时可能会发生冲突，导致有一方没有声音，如何解决？

使用智能语音交互iOS SDK，App是否能在后台模式和终止应用的情况下进行语音播报？

使用语音合成iOS SDK，onNuiTtsUserdataCallback不返回时间戳信息，如何解决？

使用语音合成iOS SDK，如何保存为文件，保存格式是什么？

使用语音合成iOS SDK，连续点击播放按钮，高频率触发播放出现页面终止情况，该如何解决？

使用集成语音服务iOS SDK，flutter\_plugin集成时，报错提示“Undefined symbols for architecture arm64: "std::\_\_1::mutex::~mutex()", referenced from: \_\_\_cxx\_global\_var\_init in libflutter\_tts.a(ringBuf.o)”。

使用在线合成语音iOS SDK，写入文件播放声音是杂音，是什情况？

WebSocket

实时语音识别接口WebSocket，发送语音体的指令是什么？一次可以发送多少Bytes?

使用实时语音识别接口WebSocket，设置了32位随机message\_id，报错提示Status:40000002 Gateway:MESSAGE\_INVALID:Invalid message id ''!。

使用WebSocket协议连接阿里云的地址，发送二进制语音数据时，建立的连接被服务器主动断开且没有错误提示，是什么原因？

使用实时语音识别WebSocket，在基于Web的JavaScript WebSocket连接成功后，如何获得message\_id和task\_id？

使用WebSocket调用实时语音识别时，WebSocket经常自动终止服务，不能实现实时语音识别，需要手动发送PCM或WAV音频文件，是什么原因？

本文汇总了您在使用SDK时可能遇到的常见问题。

## 公共类

### 如何使用SDK设置泛热词？

SDK中使用POP API训练的泛热词，是通过控制台配置的业务专属热词表与项目Appkey绑定的，您无需自行设置；而通过POP API训练获取的业务专属热词表，需要在SDK中设置其词表ID，且SDK设置热词的优先级更高，若与控制台一起使用，将覆盖控制台设置结果。请参考 [使用SDK设置业务专属热词](https://help.aliyun.com/zh/isi/developer-reference/use-an-sdk-to-specify-the-id-of-a-business-specific-hotword-vocabulary#topic-1917966 "")，将为您介绍在一句话识别、实时语音识别、录音文件识别中如何设置泛热词。

### SDK报错“DNS resolved timeout”是什么问题？

查看`/etc/resolv.conf`文件中nameserver的设置，建议增加并优先使用以下配置：`nameserver 114.114.114.114`。

### 如何使用SDK设置自学习模型？

如果是通过控制台创建的自学习模型，可在项目切换模型时选择该模型，发布上线后将与Appkey绑定，您无需在代码中自行设置；而通过POP API训练获取的自学习模型，需要在SDK中设置其模型ID才可以使用。请参考 [使用SDK 2.0设置自学习模型](https://help.aliyun.com/zh/isi/developer-reference/use-sdk-2-0-to-set-a-self-learning-model#topic-1917974 "")，将为您介绍在一句话识别、实时语音识别、录音文件识别中如何设置自学习模型。

### 是否有Android和iOS的SDK，能否用在专有云下？

有SDK，在专有云安装包里默认不提供，可以通过阿里云帮助中心对应的服务文档中下载，如实时语音识别的 [Android SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-android-1#topic-1917930 "") 和 [iOS SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-ios#topic-1917931 "")。移动端SDK可以调用公共云ASR、TTS服务，也可以用在专有云环境下。

### Token如何使用？

公共云Token在不同项目间、不同进程间、不同线程间都可以共用，同时一定要注意在Token过期前提前重新获取Token；出于安全考虑，建议您在服务端集成Token SDK，客户端在服务端获取Token。详情请参见 [获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token#topic-1917895 "")。

专有云Token目前默认都是default，暂时无需修改。

### Token重新获取会不会导致已获取的Token失效？

Token重新获取不会影响已获取Token的有效性，有效性只与时间有关。Token的有效期通过服务端响应消息的`ExpireTime`参数获取。更多信息，请参见 [获取Token协议说明](https://help.aliyun.com/zh/isi/getting-started/use-http-or-https-to-obtain-an-access-token#topic-1917896 "")。

### 是否可以提供服务的IP白名单？

服务器的IP比较多，且会随着扩容、机器故障置换等原因动态变化，当前的IP列表不代表后续都可以使用。建议增加以下两个域名的访问规则：nls-meta.cn-shanghai.aliyuncs.com、nls-gateway-cn-shanghai.aliyuncs.com，开通80、443端口，HTTP和websocket协议。

### 如何进行log控制与音频保存?

SDK提供多级log控制，在初始化接口中配置。

同时提供音频数据的保存方便问题定位，需要设置save\_wav和debug\_path初始化参数，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference#topic-1917922 "")。

**说明**

实时语音识别的save\_wav和debug\_path参数含义与一句话识别相同。

### 调用上有什么限制？

SDK已经对语音服务的访问做了封装，对您而言只要调用开始接口，在回调中进行适当事件处理。一般需要处理错误事件和识别结果事件。注意不能在回调中直接调用SDK的接口，可能导致死锁发生。

### 为什么链接不到framework？

framework中代码采用Objective-C和C++混合编写而成，所以需要使用.mm后缀文件进行调用，同时请确保工程的头文件路径与库文件路径设置正确。

### SDK错误事件如何定位原因？

在SDK上报错误事件时，首先根据错误码查看原因，一般能够根据错误码获得问题的初步原因。

## Java SDK类

### 一句话识别、实时语音识别SDK中，send接口参数含义及使用方式？

以Java为例。java SDK中，一句话识别和实时语音识别分别提供了三个重载的`send()`接口。如下：

```java
public void send(InputStream ins);
public void send(InputStream ins, int batchSize, int sleepInterval);
public void send(byte[] data);
```

三个接口使用时要保证持续、实时地向服务端发送语音数据。

demo是用语音文件模拟实时语音流的速度发送语音，通常一次发送间隔时间为100ms或200ms（sleepInterval）的语音数据，数据量（batchSize）和采样率有关：发送间隔过大，会导致延迟较大，容易断连；发送间隔过小，会消耗服务端和网络资源。可以适当实验调整到合适数值。

第2个接口中`ins`为模拟语音流，需要控制发送速率。ins中的数据每间隔100ms，发送3200字节（16000采样率）。调用示例：

```java
public void send(ins, 3200, 100); // 16 KHz语音
```

第3个接口中`data`为一次性发送的数据，控制循环调用的间隔，调用示例：

```java
recognizer.send(data); // 100ms语音数据
try {
 Thread.sleep(100);
} catch (InterruptedException e) {
 e.printStackTrace();
}
```

### 如何结合SDK日志，分析延迟问题？

以Java SDK日志为例。

- 一句话识别的延迟为一句话说完开始，到收到最终识别结果为止，消耗的时间。

在日志中搜索关键字`StopRecognition`以及`RecognitionCompleted`，分别找到语音发送完毕时的日志，以及一句话识别结束的日志。记录的时间差即为SDK端记录的一句话延时，如下日志延迟为：984-844=140（ms）。















```java
14:24:44.844 DEBUG [           main] [c.a.n.c.transport.netty4.NettyConnection] thread:1,send:{"header":{"namespace":"SpeechRecognizer","name":"StopRecognition","message_id":"bccac69b505f4e2897d12940e5b38953","appkey":"FWpPCaVYDRp6J1rO","task_id":"8c5c28d9a40c4a229a5345c09bc9c968"}}
14:24:44.984 DEBUG [ntLoopGroup-2-1] [  c.a.n.c.p.asr.SpeechRecognizerListener] on message:{"header":{"namespace":"SpeechRecognizer","name":"RecognitionCompleted","status":20000000,"message_id":"2869e93427b9429190206123b7a3d397","task_id":"8c5c28d9a40c4a229a5345c09bc9c968","status_text":"Gateway:SUCCESS:Success."},"payload":{"result":"北京的天气。","duration":2959}}
```

- 语音合成关注首包延迟，即从发送合成请求开始，到收到第一个语音包为止，消耗的时间。

日志中搜索关键字`send`，找到这条日志和紧随其后的一条收到语音包的日志。记录的时间差即为SDK端记录的首包延时。如下日志延时为1035-813=222（ms）。















```java
14:32:13.813 DEBUG [           main] [c.a.n.c.transport.netty4.NettyConnection] thread:1,send:{"payload":{"volume":50,"voice":"Ruoxi","sample_rate":8000,"format":"wav","text":"国家是由领土、人民、文化和政府四个要素组成的，国家也是政治地理学名词。从广义的角度，国家是指拥有共同的语言、文化、血统、领土、政府或者历史等的社会群体。从狭义的角度，国家是一定范围内的人群所形成的共同体形式。"},"context":{"sdk":{"name":"nls-sdk-java","version":"2.1.0"},"network":{"upgrade_cost":160,"connect_cost":212}},"header":{"namespace":"SpeechSynthesizer","name":"StartSynthesis","message_id":"6bf2a84444434c0299974d8242380d6c","appkey":"FWpPCaVYDRp6J1rO","task_id":"affa5c90986e4378907fbf49eddd283a"}}
14:32:14.035  INFO [ntLoopGroup-2-1] [  c.a.n.c.protocol.tts.SpeechSynthesizer] write array:6896
```

- 实时语音识别SDK日志类似一句话识别，可以从日志中计算语音末尾处延迟（关键字：`StopTranscription`和`TranscriptionCompleted`）。

- RESTful形式访问，客户端自带日志中没有体现延迟。需要用户自己编写代码，或者查看服务端日志。


### Java SDK找不到com.alibaba的JAR包，如何安装Alibaba Cloud SDK for Java？

请参见 [原版 SDK 使用指南](https://help.aliyun.com/zh/sdk/developer-reference/v1-0-java-sdk/ "") 安装Alibaba Cloud SDK for Java。

### 使用Java SDK调用SpeechRecognizer.stop方法时出现连接超时，提示timeout after 10 seconds waiting for complete confirmation. state:STATE\_STOP\_SENT如何解决？

`state:STATE_STOP_SENT`代表数据断开连接。如果10秒内系统未接到数据，请优先排查网络是否稳定，如偶发可能由于网络抖动引起。

### 录音文件转写接口Java SDK Demo运行报错如何排查？

1. 检查智能语音交互服务开通地和代码使用是否一致。![控制台开通地](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2136350661/p477445.png)![控制台开通地-代码](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2136350661/p477448.png)

2. 检查SDK的`fastjson`和`aliyun-java-sdk-core`两个库的依赖版本。阿里云Java SDK的核心库版本支持3.5.0及以上（如果版本在4.0.0及以上，需要根据错误提示补充对应的第三方依赖），详情请参见 [录音文件识别Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java-10#topic-1917933 "")。















```xml
<dependency>
       <groupId>com.aliyun</groupId>
       <artifactId>aliyun-java-sdk-core</artifactId>
       <version>3.7.1</version>
</dependency>
<dependency>
       <groupId>com.alibaba</groupId>
       <artifactId>fastjson</artifactId>
       <version>1.2.83</version>
</dependency>
```


### 实时语音识别使用Java SDK，SpeechRecognizer recognizer如何调用stop()实现通知服务端语音数据发送完毕？

1. 正常情况下自动调用，不需要单独调用stop()。如果10秒之内没有语音数据发给服务侧, 会报错41010120。如果一直实时发送语音数据给服务端，识别在服务侧是一直进行的，您可以通过设置`enable_intermediate_result=true`参数实时获取识别结果。

2. 如果您判断一句话结束，也可以主动调用stop()停止发送数据，获取最终识别结果。


### 实时流识别模式，Java SDK中如何触发回调onTranscriptionComplete？

`onTranscriptionComplete`可以通过stop触发，状态为`STATE_STOP_SENT`，回调处理完状态为`STATE_COMPLETE`。

### 调用Java SDK时报错，提示java.lang.IllegalStateException: complete already: DefaultChannelPromise@75822ea8(failure: java.lang.Exception: WebSocket Client failed to connect,status:403 Forbidden,reason:Meta:ACCESS\_DENIED:The token '\*\*\*' is invalid!)"如何解决？

报错原因是Token无效，请重新生成一个Token，具体操作方法请参见 [获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token#topic-1917895 "")。

### 在生成synthesizer = new SpeechSynthesizer时一直失败，提示java.nio.channels.ClosedChannelException如何解决？

建议您使用Java环境，并使用Demo在新的空项目中进行测试。如果测试Demo没有问题，说明不是SDK集成问题，建议您检查客户端的前端集成情况。

### 在测试实时语音识别和语音合成功能时，对应JAR包在哪里？

![在测试实时语音识别和语音合成功能时对应JAR包位置](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0757550661/p477479.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>

<parent>
<groupId>com.alibaba.nls</groupId>
<artifactId>nls-sdk-java-examples</artifactId>
<version>2.0.0</version>
<relativePath>../pom.xml</relativePath>
</parent>

<groupId>com.alibaba.nls</groupId>
<artifactId>nls-example-tts</artifactId>

<dependencies>
<dependency>
<groupId>ch.qos.logback</groupId>
<artifactId>logback-classic</artifactId>
<version>1.0.13</version>
</dependency>
<dependency>
<groupId>com.alibaba.nls</groupId>
<artifactId>nls-sdk-tts</artifactId>
<version>${sdk.version}</version>
</dependency>
</dependencies>

<build>
<plugins>
<plugin>
<artifactId>maven-assembly-plugin</artifactId>
<version>3.0.0</version>
<configuration>
<archive>
<manifest>
<mainClass>com.alibaba.nls.client.SpeechSynthesizerMultiThreadDemo</mainClass>
</manifest>
</archive>

<descriptorRefs>
<descriptorRef>jar-with-dependencies</descriptorRef>
</descriptorRefs>

</configuration>
<executions>
<execution>
<id>make-assembly</id> <!-- this is used for inheritance merges -->
<phase>package</phase> <!-- bind to the packaging phase -->
<goals>
<goal>single</goal>
</goals>
</execution>
</executions>
</plugin>
</plugins>
</build>
</project>
```

### Java SDK实时识别NlsClient类去连接server报错， 提示ERROR NlsClient:102 - failed to connect to server after 3 tries,error msg is :hostname can't be null如何解决？

如果您不再使用Demo，需要指定`hostname`，即请求阿里语音服务侧的接口。

接口详情请参见`wss://nls-gateway-cn-shanghai.aliyuncs.com/ws/v1`或 [实时语音识别Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java-8#topic-1917923 "")。

### Java SDK语音合成报错，提示java.nio.channels.ClosedChannelException at io.netty.channel.AbstractChannel$AbstractUnsafe.ensureOpen(...)如何解决？

如果未生成TaskId，说明请求未成功到达智能语音交互的服务端，一般为本地环境问题。建议您优先排查本地网络和环境，将线上Demo和本地对比检查。

### Java SDK通过传入阿里云账号的AccessKey ID和AccessKey Secret，调用阿里云Java SDK得到client提示错误org.json.JSONArray.iterator()Ljava/util/Iterator如何解决？

请确认依赖包是否完整，查找并添加如下两个依赖JAR包。

```xml
<dependency>
<groupId>org.json</groupId>
<artifactId>json</artifactId>
<version>20170516</version>
</dependency>

<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.8.2</version>
</dependency>
```

### Java版SDK可以直接提供上传音频文件的方式进行识别吗？

如下图所示，SDK示例通过调用RESTfulAPI接口，实现上传音频文件进行识别，详情请参见 [一句话识别Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java#topic-1917910 "")。![Java版SDK直接提供上传音频文件的方式进行识别](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0757550661/p477485.png)

### 使用Java Demo识别录音文件没有识别结果，使用文档中的语音文件识别可以正常识别，该如何解决？

您可以使用`file`命令查看语音格式，检查该格式是否符合产品要求。模型支持的标准8K数据格式为8 KHz采样率、16 bit采样位数、单声道WAV格式；16K语音数据标准格式为16 KHz采样率、16 bit采样位数、单声道WAV格式。如果测试使用，可以使用Sox或者ffmpeg等工具转成标准工具测试；如果线上使用，请参考相关产品说明。

下图以 [实时语音识别的接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference#topic-1917922 "") 为例。

![使用Java Demo识别录音文件没有识别结果](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0757550661/p477490.png)

## C++ SDK类

### C++ SDK语音合成时传入的文本没有采用UTF-8编码会有什么错误信息？

如果传入的文本没有采用UTF-8编码，在文本中含有中文字符时，语音合成SDK调用start函数会失败，返回错误信息`Socket recv failed, errorCode: 0`。错误码为0表示服务端已经关闭了连接，此时应检查传入的文本是否采用UTF-8编码。

### C++ SDK如何获取Token？

具体操作请参见 [获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token#topic-1917895 "")。

![C++ SDK如何获取Token](<Base64-Image-Removed>)

下载C++ Token SDK后获取到NlsCommonSDK，功能包括获取Token和录音文件识别。

NlsCppSDK（3.0.X和2.X旧版本）内部不包含NlsCommonSDK，功能包括实时识别、一句话识别、长/短语音合成，非NLS CPP SDK需要按照上图所示重新获取Token。

NlsCppSDK（3.1.X新版本）内部包含NlsCommonSDK，功能包括获取Token、录音文件识别、实时识别、一句话识别、长/短语音合成，不需要按照上图所示重新获取Token。

### C++ SDK调用智能实时语音解析接口失败，提示 {"TaskFailed":"connect failed."} {"channeclClosed": "nls request finished."}如何解决？

1. C++ SDK3.0及以前的版本有小概率出现这个问题，无需特别关注；3.1及以后版本出现这个问题可能是运行环境的网络问题导致，建议您检查本地网络环境。

2. 如果没有返回TaskId，说明在连接过程中直接断开，实时语音交互不需要重复调用接口，重复调用会有并发上限和超时时间，并发超过限制会直接返回超过限制，WebSocket连接超过10秒没有音频就会自动断开，但是会返回TaskId。

3. 这种情况一般是由于当时网络拥堵造成的，建议您使用 [抓包工具](https://help.aliyun.com/zh/ecs/user-guide/how-to-install-and-use-wireshark-in-windows "") 查看分析实际发送的包是否重传了`tcp retransmission`，可以在客户端使用`traceroute`命令或者使用MTR工具到`nls-gateway-cn-shanghai.aliyuncs.com`进行链路测试，判断从客户端到接口服务之间网络是否不稳定。


### C++ SDK进行语音合成时，报错未设置appkey，但是代码已经设置该如何解决？OnSynthesisTaskFailed: status code=10000002 task id=\*\*\*error message={TaskFailed":"{"task\_id":"00000000000000000000000000000000","result":"","status":40000003,"message":"Gateway:PARAMETER\_INVALID:appkey not set"}"}"

`status`为40000003指传入的参数有误，请重新检查传入的参数值是否正确，例如`appkey`、`voice`、`url`等 。’

### C++ SDK（3.0及以后版本）使用语音合成和语音识别功能，可以提高GCC5.0以上的编译版本吗？

可以。Linux下支持GCC 4.8.5或以上版本。目前已验证且顺利编译运行的GCC版本包括4.8.5、5.5.0、8.4.0。

### C++ SDK中的speechRecognizerDemo.cpp中的g\_akid和g\_akSecret在哪里获取？

请参见 [准备账号](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-1917889 "")。

### C++ SDK实时语音识别报错，提示status\_text:Gateway:IDLE\_TIMEOUT:Websocket session is idle for too long time, the last directive is 'StartTranscription'!如何解决？

1. 因为超过10秒没有发送数据到服务端，空闲超时自动断连。同时请检查URI是否正确，`wss://nls-gateway-cn-shanghai.aliyuncs.com/ws/v1`。如果发生这种情况，可以增加重试机制再次请求。

2. 也可能服务端瞬间收到大量请求导致单个case无法及时处理，建议重试。


### C++ SDK获取Token，当系统的时间不是标准时间时会获取失败，在C++ SDK中，可以自己设置timestamp，而不是获取系统的时间吗？

不可以。Token需要根据系统时间来生成。

### C++ SDK ASR请求有DNS解析失败的情况导致异常，报错ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): GetInetAddressByHostname:252 DNS: resolved timeout.ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): start:76 start failed: DNS: resolved timeout..unimrcpserver\_current.log: \[ERROR\] \[\[./ali/AliRecogChannel.cpp:772,onTaskFailed\]\]Ali Task start failed Msg :DNS: resolved timeout., start finised."如何解决？

- 旧版（3.0及以前版本）：在高并发或者电脑DNS忙碌的情况下容易出现以上问题，建议您更新到3.1.X版本，或进行再次重启请求。

- 新版（3.0及以后版本）：已经对此问题进行防御，若仍然偶现此问题，则为电脑DNS忙碌，需要再次重启请求。


### C++ SDK调用实时语音识别，集成在mrcp里面使用，部分情况下创建多个识别通道时会返回10000002如何解决？

错误码10000002是openssl官方错误描述，`Resource temporarily unavailable`一般是建连后未发送数据到服务端导致WebSocket超时，下一个发送的指令是`StartTranscription`。

### C++ SDK（新）集成到其他项目中时，将CMakeLists.txt中的add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=0) 修改为add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=1)后编译不通过该如何解决？

除了`CMakeLists.txt`，全工程都需要修改该参数，例如`config/linux.thirdparty.debug.cmake`和`config/linux.thirdparty.release.cmake`，请在全目录搜索`_GLIBCXX_USE_CXX11_ABI`进行修改。

### C++ SDK在Windows上使用，报错缺少nlsCommonSdk.dll如何解决？

3.1及以后版本无nlsCommonSdk.dll。

### C++ SDK旧版NlsSdkCpp2.0和新版NlsSdkCpp3.X的区别是什么？

NlsSdkCpp2.0版本的SDK每一个请求为一个线程，且接口为同步接口。

NlsSdkCpp3.X版本的SDK内部由第三方库libevent统一处理事件消息，并发性能更强，且接口为异步接口。

### C++版的SDK不支持实现C11规范吗？ 现在导致项目无法链接SDK该如何解决？

工程默认为`_GLIBCXX_USE_CXX11_ABI=0`，全工程都需要修改该参数，请在全目录搜索`_GLIBCXX_USE_CXX11_ABI`进行修改。

### C++ 版SDK集成语音识别报错，提示Meta:ACCESS\_DENIED:The token '' is invalid!, start finised.start() failed.CbParam: 1 exg.onTaskFailed: status code: 10000011, error message: Stop invoke error. Please check the order of execution or whether the data sent is valid.如何解决？

`Meta:ACCESS_DENIED:The token '' is invalid!, start finised.`指令牌无效，鉴权失败，请检查`appkey`是否错误、Token是否填入、Token是否过期。`status code: 10000011`指接口调用顺序错误（接收到Failed/complete事件时，SDK内部会关闭连接，此时再调用send方法会上报错误）。

### C++ 版SDK集成语音识别一句话报错，提示transcriber process start...alispeech-DEBUG start:60 starting transcriber...alispeech-WARNING \_on\_error:123 retry start: \[SSL: CERTIFICATE\_VERIFY\_FAILED\] certificate verify failed (\_ssl.c:852)alispeech-DEBUG \_on\_close:110 callback on\_channel\_closedMyCallback.OnRecognitionChannelClosed如何解决？

SSL证书校验失败，请检查发起调用的机器系统时间是否正确。

### C++ SDK一句话识别调用stop后返回错误回调状态码40000004该如何解决？{"header":{"namespace":"Default","name":"TaskFailed","status":40000004,"message\_id":"xxxxxxxxxxxxxxxxxxxxxxxxx","task\_id":"xxxxxxxxxxxxxxxxxxxxxxxxx","status\_text":"Gateway:IDLE\_TIMEOUT:Websocket session is idle for too long time, the last directive is 'StopRecognition'!"}}

可能是服务端瞬间收到大量请求导致的单个实例无法及时处理，建议重试。

### C++ SDK测试Demo成功，集成项目报错，DNS解析失败，报错 **nls-gateway-cn-shanghai.aliyuncs.com dns failed: nodename nor servname provided, or not known如何解决？**

1. SDK中会查看当前设备开启的所有协议族（IPv4、IPv6）进行DNS解析请求，`nls-gateway-cn-shanghai.aliyuncs.com`不支持 IPv6，返回解析错误，从而导致SDK DNS解析失败退出。可禁用当前设备的IPv6协议族，后续CppSdk产品改进对这方面进行可配置处理。

2. 建议您升级到3.1.12及以后版本。


### C++ SDK测试Demo可以成功，集成项目报错，网络链接失败，报错\[dnsEventCallback:465\]Node:0x7f087c001030 ai\_canonname: nls-gateway-cn-shanghai.aliyuncs.com.gds.alibabadns.com\[dnsEventCallback:477\]Node:0x7f087c001030 IpV4:106.15.XX.XX\[connectProcess:1329\]Node:0x7f087c001030 sockFd:41\[connectProcess:1347\]Node:0x7f087c001030 new Socket ip:106.15.XX.XX port:443 Fd:41.\[socketConnect:1458\]Node:0x7f087c001030 Connect failed:Network is unreachable. retry...如何解决？

以上现象为无法连接网络，查看日志发现DNS域名解析出来的IP链接不成功，进一步通过Ping判断网络不通。由于本地拦截DNS解析，导致SDK内部`libevent`的`evdns_getaddrinfo`获得错误的IP。

解决办法：

- 3.1.12版本以前可将evdns\_getaddrinfo()手动替换成系统的getaddrinfo()。

- 3.1.12版本可在`CMakeLists.txt`中修改`add_definitions(-DNLS_USE_NATIVE_GETADDRINFO)`。

- 3.1.12及以后版本增加setDirectHost()接口，您可以在SDK外部进行DNS解析，获取正确IP后通过该接口设入。

- 3.1.13及以后版本已解决此问题，若运行时仍存在上述问题，建议调用接口setUseSysGetAddrInfo(true)。


### C++ 语音合成Demo，NlsCommonSdk版本20211018基于vc16.0，NlsSdkCpp3.X版本20210629基于vc14.0，Demo程序只执行到OnSynthesisTaskFailed，返回20000000，在win10 X64 vs2015中得不到WAV的可能原因？ **log信息如下ERROR alibabaNlsLog: \[ID:15284\]\[AlibabaNls::ConnectNode::parseFrame:1014\]Node:000001D733079F20 Result conversion failed.**

NlsSdkCpp3.X-20210629里的Demo不适用于Windows版本程序，alibabacloud-nls-cpp-sdk（github的）里的才是Windows的Demo。

## Android SDK类

### Android SDK是否可以上传opus音频数据，实现实时语音转文字？

ASR中一句话识别和录音文件极速版支持opus数据，实时语音转文字仅支持PCM编码、16 bit采样位数、单声道（mono）。具体详情，请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-1#topic-1917909 "")。

### Android SDK中使用onNuiNeedAudioData录音数据回调，并在该回调过程中填充录音数据ret = audioRecord.read(buffer, 0, len)。在实时录音转写过程中，突然断网后再连网，录音SDK会自动连接并继续转写吗？

断网后需要重新连接录音SDK，不会自动连接，需要您增加重试机制。

### 智能语音交互SDK，最低支持Android的哪个版本？

智能语音交互SDK对于常规Android版本都支持。

### Android SDK录音文件识别极速版，是否支持通过任务ID查询任务状态？

不支持。

### Android SDK调用文件上传转写极速版，调用int startFileTranscriber(String params, byte\[\] task\_id)后无法收到回调，报错提示“EventE/iDST::NativeNui: no java instance, maybe already released”。

您需要核实：

- 资源文件是否复制成功。

- `CommonUtils.copyAssetsData`函数是否已调用。


### 使用实时语音识别Android SDK，管控台模型选择为8K，但是实际测试中为何将采样率设置成16K才能识别正确？

识别正确与否与您设置参数有关，您需要排查：

- `nls_config.put("sr_format", "pcm")`参数值是否配置为小写模式。

- 是否设置静态变量SAMPLE\_RATE为8000，即public final static int SAMPLE\_RATE = 8000。

- 模型选择是否正确选择为8K模型。


### int ret = nui\_instance.initialize(this, genInitParams(assets\_path,debug\_path), Constants.LogLevel.LOG\_LEVEL\_VERBOSE, true)。在该段代码中，录音权限是打开的，但代码仍然报错240021。

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

### 使用离线语音合成Android SDK，语音播报时出现不合理断句，该如何处理？

您可以通过SSML标记语言尝试解决，更多信息，请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview#topic-1917951 "")。

### 使用语音合成Android SDK，在调用cancel时候出现一次anr，该如何处理？

SDK接口为同步调用，建议您不要在主线程调用SDK接口。

### 实时音频识别对Android版本有要求吗？

没有要求。

### 调用Android SDK时，手机报错提示“audio recoder not init”。

您可以通过以下方式排查：

- 检查AudioRecord是否初始化正常。

- 检查语音播放器是否有问题。

- 编写AudioRecord录音代码，测试是否正常。


### 在模拟器上运行下载的Android程序，程序出现闪退现象，是什么原因？

模拟器可能会出现未知问题，建议您使用真机测试。

### 使用语音识别Android SDK回调onNuiNeedAudioData，但在onNuiEventCallback中回调延迟，并显示错误码50000000。

表示服务端内部错误，请重试。

### 使用语音合成Android SDK TTS时，报错提示“tts event:TTS\_EVENT\_ERROR ret 140002”。

建议您检查下输入文本是否合规。

### 不能正常使用语音合成Android SDK。

您需要检查以下条件是否满足：

- 是否已经满足Android SDK语音合成的前提条件，详情请参见 [前提条件](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-android-2#h2-u524Du63D0u6761u4EF611 "")。

- 是否已开通商用。


## iOS SDK类

### 是否支持后台处理？

SDK本身不限制前后台，iOS SDK的样例工程默认仅支持前台处理，如果您需要支持后台处理，可以做如下修改：

1. 在工程Info.list中添加Required background modes配置，并在该配置下添加item，Value设置为`App plays audio or streams audio/video using AirPlay`。![配置1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1356988061/p206201.png)

2. 在录音模块中进入后台时，不停止录音。亦即NLSVoiceRecorder.m中\_appResignActive接口中不做停止录音调用。![配置2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1356988061/p206203.png)


### 下载语音交互iOS SDK至本地库，测试代码时，在模拟器可以正常运行，真机却无法运行，报错提示“Reason: no suitable image found. Did find:xxx”。

建议您删除手机上对应的APP后，执行`xcode clean`，并重新尝试运行。除此以外，还需检查签名的正确性，如果签名不正确，需撤销原来的inHouse证书，重新制作新的证书和provisioning profile，并将代码重新签名，再次打包。

### 使用智能语音服务集成iOS SDK，接入NuiSdk运行报错MIC。

建议您检查下当前录音设备是否有被占用。

### 使用智能语音服务集成iOS SDK，接入nuisdk.framework后，导入头文件项目失败。

一般情况下是SDK导入有问题导致，请您确认下图参数是否已勾选，如果已勾选，建议您将头文件导入方式换为`#import <nuisdk/NeoNui.h>`。![nui](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9278870661/p478029.png)

### 使用iOS SDK接入nuisdk.framework后，报错提示“/Users/admin/FlashTranscription\_iOS/Fc\_ASR.xcodeproj Building for iOS, but the linked and embedded framework 'nuisdk.framework' was built for iOS + iOS Simulator”。

可能因为版本过高导致，建议您修改项目配置Validate Workspace为Yes后，重新编译。![Validate Workspace](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9278870661/p477878.png)

### 使用集成语音服务iOS SDK，在接入nuisdk.framework后报错，需要修改Legacy Build system，才可以运行，是什么原因？

建议您修改项目配置Validate Workspace为Yes后，重新编译。

![Validate Workspace](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9278870661/p477883.png)

### 使用一句话识别iOS SDK，配置nuisdk.framework为Embed & Sign后，提示“nuisdk.framework/Headers/NeoNui.h”。

建议检查下头文件是否按照文档正常导入，头文件导入格式为`#import <nuisdk/NeoNui.h>`。

### 使用App集成iOS SDK，提交到App store失败，提示“Unsupported Architectures. The executable for AliYunSmart.app/Frameworks/nuisdk.framework contains unsupported architectures '\[x86\_ \_64, i386\]'. With error code”。

可能是模拟器架构影响，您可以参考如下方法查看framework版本并移除framework模拟器架构。

1. 进入到framework目录。

2. 输入命令`lipo -info xxxFramework`，查看framework的架构版本，如果含有模拟器打包需要把模拟器架构移除。


### TRTC实时音视频和语音识别结合，当同时调用麦克风时可能会发生冲突，导致有一方没有声音，如何解决？

建议尝试TRTC的音视频流，然后使用`localStream.getAudioTrack`获取`MediaStreamTrack`对象，并转换为符合ASR标准的音频流，之后通过语音识别SDK发起请求。

### 使用智能语音交互iOS SDK，App是否能在后台模式和终止应用的情况下进行语音播报？

应用被终止无法进行语音播报。

### 使用语音合成iOS SDK，onNuiTtsUserdataCallback不返回时间戳信息，如何解决？

默认情况SDK不返回时间戳，如果您需要获取时间戳信息，可以通过接口setparamTts设置enable\_subtitle，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/overview-5#topic-1917954 "")。

### 使用语音合成iOS SDK，如何保存为文件，保存格式是什么？

可以在onNuiTtsUserdataCallback接口参数中将合成的数据保存成文件，合成的格式以传出参数为主，例如`[nls_config setObject:@"mp3" forKey:@"encode_type"]`。

目前支持格式为PCM、WAV、MP3，需要注意是，语音合成的文档案例中播放器不支持MP3格式音频，直接使用可能产生噪音，但存储的MP3格式文件可以用支持MP3格式的播放软件试听。如果个别音频文件出现少字的现象，可能是因为该发音人合成速度过快（如xiaoyun），部分数据没有写入文件被清除，您可以在fwrite后调用fflush保证数据完全写入文件。![code](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9278870661/p477941.png)

### 使用语音合成iOS SDK，连续点击播放按钮，高频率触发播放出现页面终止情况，该如何解决？

由于在线合成时需要连接网络，网络状况会直接影响接口响应时间，如果您的业务需要快速停止任务并开始下一条，可以根据业务需求调整网络超时时间。

### 使用集成语音服务iOS SDK，flutter\_plugin集成时，报错提示“Undefined symbols for architecture arm64: "std::\_\_1::mutex::~mutex()", referenced from: \_\_\_cxx\_global\_var\_init in libflutter\_tts.a(ringBuf.o)”。

您可以打开iOS工程下的Podfile文件，修改post\_install do \|installer\|部分的代码，再次执行构建即可成功。![code](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9278870661/p477946.png)

### 使用在线合成语音iOS SDK，写入文件播放声音是杂音，是什情况？

首先需要确认合成音频格式（PCM、WAV、MP3），如存储的音频流是MP3格式，但播放器不支持该格式音频就会出现杂音的状况，建议更换一下播放软件重试。同时也有用户出现音频只有尾部出现杂音的情况，可以用BeyondCompare查看音频流，是否有日志写入音。

## WebSocket

### 实时语音识别接口WebSocket，发送语音体的指令是什么？一次可以发送多少Bytes?

指令由Header和Payload两部分组成，其中Header为统一格式，不同指令的Payload格式不同。

服务端可支持一次发送3200 Byte或1600 Byte，单次发送数据时，需确保音频在发送的时候没有损坏。

### 使用实时语音识别接口WebSocket，设置了32位随机message\_id，报错提示Status:40000002 Gateway:MESSAGE\_INVALID:Invalid message id ''!。

WebSocket相当于您自己去构建的一个请求，message\_id就是随机生成的32位唯一ID。

您需要将message\_id改成32个hex字符，检查一下发送的消息是否符合要求。

### 使用WebSocket协议连接阿里云的地址，发送二进制语音数据时，建立的连接被服务器主动断开且没有错误提示，是什么原因？

实时语音识别WebSocket协议出现断开， 建议您：

- 检查下token是否生成正确。

- 确定客户端是否有正常发送音频流。


没有错误信息提示，建议您设置status状态码，默认值20000000。

### 使用实时语音识别WebSocket，在基于Web的JavaScript WebSocket连接成功后，如何获得message\_id和task\_id？

message\_id和task\_id是由您在调用侧自行生成的。

message\_id和task\_id可以随机生成32位唯一ID，且在一个链接的过程中，task\_id可以保持唯一不变，用以标识该链接的唯一性；message\_id建议在每次发送的消息中重新随机生成，用以标识该消息的唯一性。

### 使用WebSocket调用实时语音识别时，WebSocket经常自动终止服务，不能实现实时语音识别，需要手动发送PCM或WAV音频文件，是什么原因？

以上情况表示系统已经接收到您传递的音频，在符合协议以及传参的情况下，WSS或HTTP协议都能实现实时语音识别。如何实现不间断发送，需要您自行处理WSS，智能语音交互文档提供了Java后端代码示例，即以读取本地文件的形式模拟实时获取语音流并发送，详情请参见 [示例代码](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java-8#h2-u4EE3u7801u793Au4F8B4 "")。