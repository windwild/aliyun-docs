### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)[长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/long-text-to-speech-synthesis/)[实时长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/real-time-long-text-to-speech-synthesis/)C++ SDK

# C++ SDK

更新时间：2025-07-29 01:51:07

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java-1-1)[下一篇：接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

SDK下载

SDK包文件说明

编译运行

关键接口

C++ SDK错误码

服务端响应状态码

代码示例

常见问题

C++ SDK（3.0及以后版本）使用语音合成和语音识别功能，可以提高GCC5.0以上的编译版本吗？

为什么链接不到framework？

C++ SDK ASR请求有DNS解析失败的情况导致异常，报错ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): GetInetAddressByHostname:252 DNS: resolved timeout.ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): start:76 start failed: DNS: resolved timeout..unimrcpserver\_current.log: \[ERROR\] \[\[./ali/AliRecogChannel.cpp:772,onTaskFailed\]\]Ali Task start failed Msg :DNS: resolved timeout., start finised."如何解决？

C++ SDK（新）集成到其他项目中时，将CMakeLists.txt中的add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=0) 修改为add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=1)后编译不通过该如何解决？

C++ SDK旧版NlsSdkCpp2.0和新版NlsSdkCpp3.X的区别是什么？

C++版的SDK不支持实现C11规范吗？ 现在导致项目无法链接SDK该如何解决？

C++ SDK测试Demo成功，集成项目报错，DNS解析失败，报错nls-gateway-cn-shanghai.aliyuncs.com dns failed: nodename nor servname provided, or not known如何解决？

C++ SDK测试Demo可以成功，集成项目报错，网络链接失败，报错\[dnsEventCallback:465\]Node:0x7f087c001030 ai\_canonname: nls-gateway-cn-shanghai.aliyuncs.com.gds.alibabadns.com\[dnsEventCallback:477\]Node:0x7f087c001030 IpV4:106.15.XX.XX\[connectProcess:1329\]Node:0x7f087c001030 sockFd:41\[connectProcess:1347\]Node:0x7f087c001030 new Socket ip:106.15.XX.XX port:443 Fd:41.\[socketConnect:1458\]Node:0x7f087c001030 Connect failed:Network is unreachable. retry...如何解决？

C++ SDK语音合成时传入的文本没有采用UTF-8编码会有什么错误信息？

SDK报错“DNS resolved timeout”是什么问题？

本文介绍如何使用阿里云智能语音服务提供的C++ SDK，包括SDK的安装方法及SDK代码示例。

## SDK下载

**说明**

- 当前最新版本：3.2.1b，支持Linux平台。发布日期：2024年12月25日。

- 使用SDK前，请先阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-1#topic-2605518 "")。

- 该版本C++ SDK API 3.1和上一版本API 2.0（已下线）定义有区别，本文以当前版本为例进行介绍。


您可通过以下两种方法获取SDK。

- 方法一：从GitHub获取最新源码，详细编译和运行方式可见下文，或查看源码中的readme.md。















```javascript
git clone --depth 1 https://github.com/aliyun/alibabacloud-nls-cpp-sdk
```

- 方法二：直接从下文表中选取需要的SDK包进行下载。其中SDK源码包为SDK原始代码，需要通过下文编译方法生成集成所需的库文件。其他对应平台的SDK包内含相关库文件、头文件，无需编译。




| **最新SDK包** | **平台** | **MD5** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **最新SDK包** | **平台** | **MD5** |
| [alibabacloud-nls-cpp-sdk3.3.0b-master\_cbcac53.zip](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250728/uhudak/alibabacloud-nls-cpp-sdk3.3.0b-master_cbcac53.zip) | SDK源码 | 7257c0998654e611cf2e8ca9867670ef |
| [NlsCppSdk\_Linux-x86\_64\_3.3.0b\_cbcac53.tar.gz](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250728/ehavmg/NlsCppSdk_Linux-x86_64_3.3.0b_cbcac53.tar.gz) | Linux x86\_64 | 9a93df607f26f1558bc1043a425af6d1 |
| [NlsCppSdk\_Linux-aarch64\_3.1.15\_fa30fba.tar.gz](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230911/ziaf/NlsCppSdk_Linux-aarch64_3.1.15_fa30fba.tar.gz) | Linux aarch64 | 76c34a3ab397d7285963a139b9270ff4 |



其中：

  - alibabacloud-nls-cpp-sdk<version>-master\_<github commit id>.zip为SDK源码包。

  - NlsCppSdk\_<平台>\_<版本号>\_<github commit id>.tar.gz为对应平台下开发需要的SDK包，详见内部readme.md。

## **SDK包文件说明**

- scripts/build\_linux.sh：SDK源码中，以Linux平台为例的示例编译脚本。

- CMakeLists.txt：SDK源码中，以Linux平台为例的示例代码工程CMakeList文件。

- demo目录：SDK包中，集成示例代码，以Linux平台为例，如下表所示。




| **文件名** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **文件名** | **描述** |
| speechRecognizerDemo.cpp | 一句话识别示例。 |
| speechSynthesizerDemo.cpp | 语音合成示例。 |
| speechTranscriberDemo.cpp | 实时语音识别示例。 |
| fileTransferDemo.cpp | 录音文件识别示例。 |

- resource目录：SDK源码中，语音服务范例音频，可用于功能测试，如下表所示。




| **文件名** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **文件名** | **描述** |
| - test0.wav<br>    <br>  - test1.wav<br>    <br>  - test2.wav<br>    <br>  - test3.wav | 测试音频（16k采样频率、16bit采样位数的音频文件）。 |

- include：SDK源码中，SDK头文件，如下表所示。




| **文件名** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **文件名** | **描述** |
| nlsClient.h | SDK实例。 |
| nlsEvent.h | 回调事件说明。 |
| nlsGlobal.h | SDK全局头文件。 |
| nlsToken.h | SDK Access Token实例。 |
| iNlsRequest.h | NLS请求基础头文件。 |
| speechRecognizerRequest.h | 一句话识别。 |
| speechSynthesizerRequest.h | 语音合成、长文本语音合成。 |
| speechTranscriberRequest.h | 实时音频流识别。 |
| FileTrans.h | 录音文件识别。 |

- lib：SDK库文件。

- readme.md：SDK说明。

- release.log：版本更新说明。

- version：版本号。


## **编译运行**

1. 安装工具的最低版本要求如下：

   - CMake 3.0

   - Glibc 2.5

   - Gcc 4.8.5
2. 在Linux终端运行如下脚本。

1. 进入SDK源码的根目录。

2. 生成SDK库文件和可执行程序： **srDemo**（一句话识别）、 **stDemo**（实时语音识别）、 **syDemo**（语音合成）、 **daDemo**（语音对话）。















      ```shell
      ./scripts/build_linux.sh
      ```

3. 查看范例使用方式。















      ```shell
      cd build/demo
      ./syDemo
      ```

## **关键接口**

- 基础接口

  - NlsClient：语音处理客户端，利用该客户端可以进行一句话识别、实时语音识别和语音合成的语音处理任务。该客户端为线程安全，建议全局仅创建一个实例。




    | **接口名** | **启用版本** | **功能描述** |
    | --- | --- | --- |



    |     |     |     |
    | --- | --- | --- |
    | **接口名** | **启用版本** | **功能描述** |
    | getInstance | 2.x | 获取（创建）NlsClient实例。 |
    | setLogConfig | 2.x | 设置日志文件与存储路径。 |
    | setDirectHost | 3.x | 跳过DNS域名解析直接设置服务器IPv4地址，若调用则需要在startWorkThread之前。 |
    | setAddrInFamily | 3.1.12 | 设置套接口地址结构的类型，默认为AF\_INET仅返回IPv4相关的地址信息，需要在startWorkThread之前调用。 |
    | setUseSysGetAddrInfo | 3.1.13 | 若libevent的DNS无法满足，无法完成DNS，可调用此接口切换成系统的接口，需要在startWorkThread之前调用。 |
    | calculateUtf8Chars | 3.1.14 | 统计文本内容字符数，需要传入UTF-8编码的文本内容，其中1个汉字、1个英文字母或1个标点均算作1个字符。 |
    | setSyncCallTimeout | 3.1.17 | 设置同步调用模式的超时时间（ms）。默认值为0（即关闭同步模式）。<br>使用同步调用模式时：<br>    - start()阻塞直至接收服务端结果<br>      <br>    - stop()阻塞直至触发close()回调 |
    | setPreconnectedPool | 3.3.0 | 设置每个域名URL的预连接池。<br>    - 作用：<br>      <br>      为域名URL建立持久连接池，请求结束后自动复用连接<br>      <br>      - 降低每次发起请求前的连接时间<br>        <br>      - 大幅降低首包延迟<br>    - 与长链接模式冲突，会关闭已设置的长链接模式。<br>      <br>    - 禁用场景：听悟场景<br>      <br>    - 调用约束：需要在`startWorkThread`之前调用 |
    | startWorkThread | 3.x | 启动工作线程数，默认1即启动一个线程，若-1则启动CPU核数的线程数。在高并发的情况下建议选择-1。可以理解NlsClient实例初始化，必须调用。 |
    | getVersion | 3.x | 获取SDK版本号。 |
    | releaseInstance | 2.x | 销毁NlsClient对象实例。 |
    | CreateSynthesizerRequest | 2.x | 创建语音合成对象，线程安全，支持高并发请求。创建此对象时即可通过入参确定是长文本语音合成还是短文本语音合成。300字以内可用短文本语音合成，300字以上可考虑使用长文本语音合成。字符计算可调用接口calculateUtf8Chars。 |
    | releaseSynthesizerRequest | 2.x | 销毁语音合成对象，需要在当前请求的closed事件后调用。 |

  - NlsToken：创建Token对象，用于申请获取TokenId。申请新Token时需要先获取有效时间戳，若超过有效时间则再申请。若在有效时间内多次申请Token会导致TokenId错误而无法使用。




    | **接口名** | **功能描述** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **接口名** | **功能描述** |
    | setAccessKeyId | 设置阿里云账号AccessKey ID。 |
    | setKeySecret | 设置阿里云账号AccessKey Secret。 |
    | setDomain | 设置域名，非必填。 |
    | setServerVersion | 设置API版本，非必填。 |
    | setServerResourcePath | 设置服务路径，非必填。 |
    | setRegionId | 设置服务的地区ID，非必填。 |
    | setAction | 设置功能，非必填。 |
    | applyNlsToken | 申请获取Token ID。 |
    | getToken | 获取Token ID。 |
    | getExpireTime | 获取Token有效期时间戳（秒）。 |
    | getErrorMsg | 获得错误信息。 |

  - NlsEvent：事件对象，您可以从中获取Request状态码、云端返回结果、失败信息等。




    | **接口名** | **功能描述** |
    | --- | --- |



    |     |     |
    | --- | --- |
    | **接口名** | **功能描述** |
    | getStatusCode | 获取状态码，正常情况为0或者20000000，失败时对应失败的错误码。 |
    | getErrorMessage | 在TaskFailed回调中，获取NlsRequest操作过程中出现失败时的错误信息。 |
    | getTaskId | 获取任务的TaskId。 |
    | getBinaryData | 获取云端返回的二进制数据。 |
    | getAllResponse | 获取云端返回的识别结果。 |
- 识别接口

SpeechSynthesizerRequest：语音合成请求对象，用于语音合成及长文本语音合成。接口说明以speechSynthesizerRequest.h内容为准。




| **接口名** | **启用版本** | **功能描述** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **接口名** | **启用版本** | **功能描述** |
| setOnSynthesisCompleted | 2.x | 设置语音合成结束回调函数。 |
| setOnChannelClosed | 2.x | 设置通道关闭回调函数。 |
| setOnTaskFailed | 2.x | 设置错误回调函数。 |
| setOnBinaryDataReceived | 2.x | 设置语音合成二进制音频数据接收回调函数。 |
| setOnMetaInfo | 2.x | 设置文本对应的日志信息接收回调函数。 |
| setOnMessage | 3.1.16 | 设置服务端response message回调函数，所有回调从此回调输出由用户自行解析。非必填。设置后需setEnableOnMessage启动。 |
| setAppKey | 2.x | 设置AppKey。 |
| setToken | 2.x | 口令认证。所有的请求都必须通过SetToken方法认证通过，才可以使用。 |
| setUrl | 2.x | 设置服务URL地址。非必填。 |
| setText | 2.x | 待合成音频文本内容text设置。300字以内可用短文本语音合成，300字以上可考虑使用长文本语音合成。字符计算可调用接口calculateUtf8Chars。<br>**说明**<br>调用某音色的多情感内容，需要在text中加上ssml-emotion标签，详情请参见 [<emotion>](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview#title-i3w-j10-5yw "")。<br>只有支持多情感的音色，才能使用<emotion>标签，否则会报错：Illegal ssml text。 |
| setVoice | 2.x | 发音人voice设置。 |
| setVolume | 2.x | 音量volume设置。 |
| setFormat | 2.x | 输出音频编码格式Format设置（默认是PCM，支持的格式PCM、WAV、MP3）。 |
| setSampleRate | 2.x | 音频采样率设置。 |
| setSpeechRate | 2.x | 语速设置。 |
| setPitchRate | 2.x | 语调设置。 |
| setMethod | 2.x | 合成方法method设置，默认0。<br>  - 0：统计参数合成：基于统计参数的语音合成，优点是能适应的韵律特征的范围较宽，合成器比特率低，资源占用小，性能高，音质适中。<br>    <br>  - 1：波形拼接合成：基于高质量音库提取学习合成，资源占用相对较高，音质较好，更加贴近真实发音，但没有参数合成稳定。 |
| setEnableSubtitle | 2.x | 是否开启字幕功能。 |
| setPayloadParam | 2.x | 参数设置，入参为JSON格式字符串。 |
| setTimeout | 2.x | 设置链接超时时间，默认5000ms。 |
| setContextParam | 2.x | 设置用户自定义参数，入参为JSON格式字符串。 |
| AppendHttpHeaderParam | 2.x | 设置用户自定义ws阶段http header参数。 |
| setSendTimeout | 3.1.14 | 设置发送超时时间，默认5000ms。 |
| setEnableOnMessage | 3.1.16 | 设置开启服务器返回消息回调。 |
| getTaskId | 3.1.17 | 获得当前请求的task\_id。 |
| start | 2.x | 启动SpeechSynthesizerRequest。 |
| cancel | 2.x | 不会与服务端确认关闭，直接关闭语音合成过程。 |


## **C++ SDK错误码**

| **状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 0 | Success | 成功 |  |
| -10 | DefaultError | 默认错误 | 暂未使用。 |
| -11 | JsonParseFailed | 错误的JSON格式 | 请检查传入的JSON字符串是否符合JSON格式。 |
| -12 | JsonObjectError | 错误的JSON对象 | 建议重新尝试。 |
| -13 | MallocFailed | Malloc失败 | 请检查内存是否充足。 |
| -14 | ReallocFailed | Realloc失败 | 请检查内存是否充足。 |
| -15 | InvalidInputParam | 传入无效的参数 | 暂未使用。 |
| -50 | InvalidLogLevel | 无效日志级别 | 请检查设置的Log级别。 |
| -51 | InvalidLogFileSize | 无效日志文件大小 | 请检查设置的Log文件大小参数。 |
| -52 | InvalidLogFileNum | 无效日志文件数量 | 请检查设置的Log文件数量参数。 |
| -100 | EncoderExistent | NLS的编码器已存在 | 建议重新尝试。 |
| -101 | EncoderInexistent | NLS的编码器不存在 | 建议重新初始化。 |
| -102 | OpusEncoderCreateFailed | Opus编码器创建失败 | 建议重新初始化。 |
| -103 | OggOpusEncoderCreateFailed | OggOpus编码器创建失败 | 建议重新初始化。 |
| -104 | InvalidEncoderType | encoder类型无效 | 编译时可能关闭OPUS但是又使用，或请检查ENCODER\_TYPE。 |
| -150 | EventClientEmpty | 主工作线程空指针，已释放 | 建议重新初始化，即startWorkThread()。 |
| -151 | SelectThreadFailed | 工作线程选择失败，未初始化 | 建议重新初始化，即startWorkThread()。 |
| -160 | StartCommandFailed | 发送start命令失败 | 建议重新尝试。 |
| -161 | InvokeStartFailed | 请求状态机不对，导致start失败 | 请检查当前请求是否未创建或者已经完成。 |
| -162 | InvokeSendAudioFailed | 请求状态机不对，导致sendAudio失败 | 请检查当前请求是否已经启动（即收到started事件回调）或者已经完成。 |
| -163 | InvalidOpusFrameSize | opus帧长无效，默认为640字节 | OPU编码模式下，sendAudio一帧只接收640字节数据。 |
| -164 | InvokeStopFailed | 请求状态机不对，导致stop失败 | 请检查当前请求是否未启动（即收到started事件回调）或者已经完成。 |
| -165 | InvokeCancelFailed | 请求状态机不对，导致stop失败 | 请检查当前请求是否未启动（即收到started事件回调）或者已经完成。 |
| -166 | InvokeStControlFailed | 请求状态机不对，导致stControl失败 | 请检查当前请求是否未启动（即收到started事件回调）或者已经完成。 |
| -200 | NlsEventEmpty | NLS事件为空 | SDK内部使用，NlsEvent帧丢失。 |
| -201 | NewNlsEventFailed | 创建NlsEvent失败 | SDK内部使用，NlsEvent帧创建失败。 |
| -202 | NlsEventMsgEmpty | NLS事件中消息为空 | parseJsonMsg()进行解析时发现消息字符串为空。 |
| -203 | InvalidNlsEventMsgType | 无效的NLS事件中消息类型 | SDK内部使用，NlsEvent帧的事件类型不合法。 |
| -204 | InvalidNlsEventMsgStatusCode | 无效的NLS事件中消息状态码 | SDK内部使用，NlsEvent帧的事件消息状态不合法。 |
| -205 | InvalidNlsEventMsgHeader | 无效的NLS事件中消息头 | SDK内部使用，NlsEvent帧的事件消息头不合法。 |
| -250 | CancelledExitStatus | 已调用cancel | 暂未使用。 |
| -251 | InvalidWorkStatus | 无效的工作状态 | SDK内部使用，当前请求内部状态不合法。 |
| -252 | InvalidNodeQueue | workThread中NodeQueue无效 | SDK内部使用，当前待运行的请求不合法，建议释放当前请求重新尝试。 |
| -300 | InvalidRequestParams | 请求的入参无效 | sendAudio传入的数据为空。 |
| -301 | RequestEmpty | 请求是空指针 | SDK内部使用，当前请求已经释放，建议释放当前请求重新尝试。 |
| -302 | InvalidRequest | 无效的请求 | SDK内部使用，当前请求已经释放，建议释放当前请求重新尝试。 |
| -303 | SetParamsEmpty | 设置传入的参数为空 | 请检查传入的参数是否为空。 |
| -350 | GetHttpHeaderFailed | 获得http头失败 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -351 | HttpGotBadStatus | http错误的状态 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -352 | WsResponsePackageFailed | 解析websocket返回包失败 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -353 | WsResponsePackageEmpty | 解析websocket返回包为空 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -354 | WsRequestPackageEmpty | websocket请求包为空 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -355 | UnknownWsFrameHeadType | 未知websocket帧头类型 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -356 | InvalidWsFrameHeaderSize | 无效的websocket帧头大小 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -357 | InvalidWsFrameHeaderBody | 无效的websocket帧头本体 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -358 | InvalidWsFrameBody | 无效的websocket帧本体 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -359 | WsFrameBodyEmpty | 帧数据为空，常见为收到了脏数据 | SDK内部使用，根据日志中反馈信息详细定位。 |
| -400 | NodeEmpty | node为空指针 | 建议释放当前请求重新尝试。 |
| -401 | InvaildNodeStatus | node所处状态无效 | SDK内部使用，建议释放当前请求重新尝试。 |
| -402 | GetAddrinfoFailed | 通过DNS解析地址识别 | SDK内部使用，请检查当前环境的DNS是否可用。 |
| -403 | ConnectFailed | 联网失败 | 请检查当前网络环境是否可用。 |
| -404 | InvalidDnsSource | 当前设备无DNS | SDK内部使用，请检查当前环境的DNS是否可用。 |
| -405 | ParseUrlFailed | 无效URL | 请检查设置的URL是否有效。 |
| -406 | SslHandshakeFailed | SSL握手失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -407 | SslCtxEmpty | SSL\_CTX未空 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -408 | SslNewFailed | SSL\_new失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -409 | SslSetFailed | SSL设置参数失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -410 | SslConnectFailed | SSL\_connect失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -411 | SslWriteFailed | SSL发送数据失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -412 | SslReadSysError | SSL接收数据收到SYSCALL错误 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -413 | SslReadFailed | SSL接收数据失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -414 | SocketFailed | 创建socket失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -415 | SetSocketoptFailed | 设置socket参数失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -416 | SocketConnectFailed | 进行socket链接失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -417 | SocketWriteFailed | socket发送数据失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -418 | SocketReadFailed | socket接收数据失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -430 | NlsReceiveFailed | NLS接收帧数据失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -431 | NlsReceiveEmpty | NLS接收帧数据为空 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -432 | ReadFailed | 接收数据失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -433 | NlsSendFailed | NLS发送数据失败 | SDK内部使用，请检查当前网络环境是否可用，并再次尝试。 |
| -434 | NewOutputBufferFailed | 创建buffer失败 | SDK内部使用，请检查内存是否充足。 |
| -435 | NlsEncodingFailed | 音频编码失败 | SDK内部使用，建议释放当前请求重新尝试。 |
| -436 | EventEmpty | event为空 | SDK内部使用，建议释放当前请求重新尝试。 |
| -437 | EvbufferTooMuch | evbuffer中数据太多 | SDK内部使用，发送数据缓存已满（16K音频最大缓存320000，8K音频最大缓存160000），请检查是否发送音频数据过频或一次发送过多数据。 |
| -438 | EvutilSocketFailed | evutil设置参数失败 | SDK内部使用，建议释放当前请求重新尝试。 |
| -439 | InvalidExitStatus | 无效的退出状态 | 请检查是否已经cancel了当前请求。 |
| -450 | InvalidAkId | 阿里云账号ak id无效 | 请检查阿里云账号ak id是否为空。 |
| -451 | InvalidAkSecret | 阿里云账号ak secret无效 | 请检查阿里云账号ak secret是否为空。 |
| -452 | InvalidAppKey | 项目appKey无效 | 请检查阿里云项目appKey是否为空。 |
| -453 | InvalidDomain | domain无效 | 请检查输入的domain是否为空。 |
| -454 | InvalidAction | action无效 | 请检查输入的action是否为空。 |
| -455 | InvalidServerVersion | ServerVersion无效 | 请检查输入的ServerVersion是否为空。 |
| -456 | InvalidServerResource | ServerResource无效 | 请检查输入的ServerResource是否为空。 |
| -457 | InvalidRegionId | RegionId无效 | 请检查输入的RegionId是否为空。 |
| -500 | InvalidFileLink | 无效的录音文件链接 | 录音文件转写文件链接为空。 |
| -501 | ErrorStatusCode | 错误的状态码 | 录音文件转写返回错误，详见错误码。 |
| -502 | IconvOpenFailed | 申请转换描述失败 | UTF8与GBK转换失败。 |
| -503 | IconvFailed | 编码转换失败 | UTF8与GBK转换失败。 |
| -504 | ClientRequestFaild | 账号客户端请求失败 | 录音文件转写返回失败。 |
| -999 | NlsMaxErrorCode |  |  |

| **其他状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **其他状态码** | **状态消息** | **原因** | **解决方案** |
| 10000001 | NewSslCtxFailed | SSL: couldn't create a context! | 建议重新初始化。 |
| 10000002 | DefaultErrorCode | return of SSL\_read: error:00000000:lib(0):func(0):reason(0) | 建议重新尝试。 |
| return of SSL\_read: error:140E0197:SSL routines:SSL\_shutdown:shutdown while in init |
| 10000003 | SysErrorCode | 系统错误。 | 根据系统反馈的错误信息进行处理。 |
| 10000004 | EmptyUrl | URL: The url is empty. | 传入的URL为空，请重新填写正确URL。 |
| 10000005 | InvalidWsUrl | Could not parse WebSocket url: | 传入的URL格式错误，请重新填写正确URL。 |
| 10000007 | JsonStringParseFailed | JSON: Json parse failed. | JSON格式异常，请通过日志查看具体的错误点。 |
| 10000008 | UnknownWsHeadType | WEBSOCKET: unkown head type. | 联网失败，请检查本机DNS解析和URL是否有效。 |
| 10000009 | HttpConnectFailed | HTTP: connect failed. | 与云端连接失败，请检查网络后，重试。 |
| 10000010 | MemNotEnough | 内存不足。 | 请检查内存是否充足。 |
| 10000015 | SysConnectFailed | connect failed. | 联网失败，请检查本机DNS解析和URL是否有效。 |
| 10000100 | HttpGotBadStatusWith403 | Got bad status host=xxxxx line=HTTP/1.1 403 Forbidden | 链接被拒，请检查账号特别是token是否过期。 |
| 10000101 | EvSendTimeout | Send timeout. socket error: | libevent发送event超时，请检查回调中是否有耗时任务，或并发过大导致无法及时处理事件。 |
| 10000102 | EvRecvTimeout | Recv timeout. socket error: | libevent接收event超时，请检查回调中是否有耗时任务，或并发过大导致无法及时处理事件。 |
| 10000103 | EvUnknownEvent | Unknown event: | 未知的libevent事件，建议重新尝试。 |
| 10000104 | OpNowInProgress | Operation now in progress | 链接正在进行中，建议重新尝试。 |
| 10000105 | BrokenPipe | Broken pipe | pipe处理不过来，建议重新尝试。 |
| 10000110 | TokenHasExpired | Gateway:ACCESS\_DENIED:The token 'xxx' has expired! | 请更新Token。 |
| 10000111 | TokenIsInvalid | Meta:ACCESS\_DENIED:The token 'xxx' is invalid! | 请检查token的有效性。 |
| 10000112 | NoPrivilegeToVoice | Gateway:ACCESS\_DENIED:No privilege to this voice! (voice: zhinan, privilege: 0) | 此发音人无权使用。 |
| 10000113 | MissAuthHeader | Gateway:ACCESS\_DENIED:Missing authorization header! | 请检查账号是否有权限，或并发是否在限度内。 |
| 10000120 | Utf8ConvertError | utf8ToGbk failed | utf8转码失败，常为系统问题，建议重新尝试。 |
| 20000000 | SuccessStatusCode | 成功 |  |

## 服务端响应状态码

关于服务状态码，请参见 [服务状态码](https://help.aliyun.com/zh/isi/developer-reference/api-reference-1)。

## 代码示例

- 示例中使用了SDK内置的默认外网访问服务URL，如果您使用阿里云上海ECS且需要使用内网访问服务URL，则在创建SpeechSynthesizerRequest的对象中设置内网访问的URL：















```cpp
request->setUrl("ws://nls-gateway-cn-shanghai-internal.aliyuncs.com/ws/v1");
```

- 示例中将合成的音频保存在文件中，如果您需要播放音频且对实时性要求较高，建议使用流式播放，即边接收语音数据边播放，减少延时，而无需等待合成结束后再处理语音流。

- 完整示例请参见SDK文件中demo目录的speechSynthesizerDemo.cpp文件。

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的AccessKey ID、AccessKey Secret和AppKey的环境变量名： **NLS\_AK\_ENV**、 **NLS\_SK\_ENV**、 **NLS\_APPKEY\_ENV**。


```cpp
#include <string.h>
#include <unistd.h>
#include <pthread.h>
#include <stdlib.h>
#include <ctime>
#include <string>
#include <iostream>
#include <vector>
#include <fstream>
#include <sys/time.h>
#include <errno.h>
#include "nlsClient.h"
#include "nlsEvent.h"
#include "nlsToken.h"
#include "speechSynthesizerRequest.h"

using namespace AlibabaNlsCommon;
using AlibabaNls::NlsClient;
using AlibabaNls::NlsEvent;
using AlibabaNls::LogDebug;
using AlibabaNls::LogInfo;
using AlibabaNls::LogError;
using AlibabaNls::TtsVersion;
using AlibabaNls::SpeechSynthesizerRequest;

//自定义线程参数。
struct ParamStruct {
  std::string text;
  std::string token;
  std::string appkey;
  std::string audioFile;
};
//自定义事件回调参数。
struct ParamCallBack {
 public:
  ParamCallBack() {
    pthread_mutex_init(&mtxWord, NULL);
    pthread_cond_init(&cvWord, NULL);
  };
  ~ParamCallBack() {
    pthread_mutex_destroy(&mtxWord);
    pthread_cond_destroy(&cvWord);
  };

  std::string binAudioFile;
  std::ofstream audioFile;

  pthread_mutex_t mtxWord;
  pthread_cond_t cvWord;
};

/**
 * 全局维护一个服务鉴权token和其对应的有效期时间戳，
 * 每次调用服务之前，首先判断token是否已经过期，
 * 如果已经过期，则根据AccessKey ID和AccessKey Secret重新生成一个token，并更新这个全局的token和其有效期时间戳。
 *
 * 获取Token具体操作，请参见：https://help.aliyun.com/document_detail/450514.html
 *
 * 注意：不要每次调用服务之前都重新生成新token，只需在token即将过期时重新生成即可。所有的服务并发可共用一个token。
 */
std::string g_akId = "";
std::string g_akSecret = "";
std::string g_token = "";
long g_expireTime = -1;

/**
 * 根据AccessKey ID和AccessKey Secret重新生成一个token，并获取其有效期时间戳
 */
int generateToken(std::string akId, std::string akSecret,
                  std::string* token, long* expireTime) {
  NlsToken nlsTokenRequest;
  nlsTokenRequest.setAccessKeyId(akId);
  nlsTokenRequest.setKeySecret(akSecret);

  int ret = nlsTokenRequest.applyNlsToken();
  if (ret < 0) {
    // 获取失败原因。
    printf("generateToken Failed, error code:%d msg:%s\n",
        ret, nlsTokenRequest.getErrorMsg());
    return ret;
  }
  *token = nlsTokenRequest.getToken();
  *expireTime = nlsTokenRequest.getExpireTime();
  return 0;
}

/**
 * @brief sdk在接收到云端返回合成结束消息时, sdk内部线程上报Completed事件
 * @note 上报Completed事件之后，SDK内部会关闭识别连接通道.
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void OnSynthesisCompleted(NlsEvent* cbEvent, void* cbParam) {
  ParamCallBack* tmpParam = (ParamCallBack*)cbParam;
  // 演示如何打印/使用用户自定义参数示例。
  printf("OnSynthesisCompleted: %s\n", tmpParam->binAudioFile.c_str());
  // 获取消息的状态码，成功为0或者20000000，失败时对应失败的错误码。
  // 当前任务的task id，方便定位问题，作为和服务端交互的唯一标识建议输出。
  printf("OnSynthesisCompleted: status code=%d, task id=%s\n", cbEvent->getStatusCode(), cbEvent->getTaskId());
  // 获取服务端返回的全部信息。
  //printf("OnSynthesisCompleted: all response=%s\n", cbEvent->getAllResponse());
}

/**
 * @brief 合成过程发生异常时, sdk内部线程上报TaskFailed事件
 * @note 上报TaskFailed事件之后，SDK内部会关闭识别连接通道.
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void OnSynthesisTaskFailed(NlsEvent* cbEvent, void* cbParam) {
  ParamCallBack* tmpParam = (ParamCallBack*)cbParam;
  // 演示如何打印/使用用户自定义参数示例。
  printf("OnSynthesisTaskFailed: %s\n", tmpParam->binAudioFile.c_str());
  // 当前任务的task id。
  printf("OnSynthesisTaskFailed: status code=%d, task id=%s, error message=%s\n",
      cbEvent->getStatusCode(), cbEvent->getTaskId(), cbEvent->getErrorMessage());
}

/**
 * @brief 文本上报服务端之后, 收到服务端返回的二进制音频数据, SDK内部线程通过BinaryDataRecved事件上报给用户
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 * @notice 此处切记不可做block操作,只可做音频数据转存. 若在此回调中做过多操作,
 *         会阻塞后续的数据回调和completed事件回调.
 */
void OnBinaryDataRecved(NlsEvent* cbEvent, void* cbParam) {
  ParamCallBack* tmpParam = (ParamCallBack*)cbParam;
  // 演示如何打印/使用用户自定义参数示例。
  printf("OnBinaryDataRecved: %s\n", tmpParam->binAudioFile.c_str());

  const std::vector<unsigned char>& data = cbEvent->getBinaryData(); // getBinaryData() ：获取文本合成的二进制音频数据。
  printf("OnBinaryDataRecved: status code=%d, task id=%s, data size=%d\n",
      cbEvent->getStatusCode(), cbEvent->getTaskId(), data.size());
  // 以追加形式将二进制音频数据写入文件。
  if (data.size() > 0) {
    tmpParam->audioFile.write((char*)&data[0], data.size());
  }
}

/**
 * @brief 返回 tts 文本对应的日志信息，增量返回对应的字幕信息
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
*/
void OnMetaInfo(NlsEvent* cbEvent, void* cbParam) {
  ParamCallBack* tmpParam = (ParamCallBack*)cbParam;
  // 演示如何打印/使用用户自定义参数示例。
  printf("OnBinaryDataRecved: %s\n", tmpParam->binAudioFile.c_str());
  printf("OnMetaInfo: task id=%s, respose=%s\n", cbEvent->getTaskId(), cbEvent->getAllResponse());
}

/**
 * @brief 识别结束或发生异常时，会关闭连接通道, sdk内部线程上报ChannelCloseed事件
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void OnSynthesisChannelClosed(NlsEvent* cbEvent, void* cbParam) {
    ParamCallBack* tmpParam = (ParamCallBack*)cbParam;
    // 演示如何打印/使用用户自定义参数示例。
    printf("OnSynthesisChannelClosed: %s\n", tmpParam->binAudioFile.c_str());
    printf("OnSynthesisChannelClosed: %s\n", cbEvent->getAllResponse());

    //通知发送线程, 最终识别结果已经返回, 可以调用stop()
    pthread_mutex_lock(&(tmpParam->mtxWord));
    pthread_cond_signal(&(tmpParam->cvWord));
    pthread_mutex_unlock(&(tmpParam->mtxWord));
}

/**
 * @brief 短链接模式下工作线程
 *        以 createSynthesizerRequest          <----|
 *                   |                              |
 *           request->start()                       |
 *                   |                              |
 *           收到OnSynthesisChannelClosed回调       |
 *                   |                              |
 *           releaseSynthesizerRequest(request) ----|
 *        进行循环。
 */
void* pthreadFunc(void* arg) {

  // 0: 从自定义线程参数中获取token, 配置文件等参数.
  ParamStruct* tst = (ParamStruct*)arg;
  if (tst == NULL) {
    std::cout << "arg is not valid." << std::endl;
    return NULL;
  }

  // 1: 初始化自定义回调参数
  ParamCallBack* cbParam = new ParamCallBack();
  cbParam->binAudioFile = tst->audioFile;
  cbParam->audioFile.open(cbParam->binAudioFile.c_str(), std::ios::binary | std::ios::out);

  /*
   * 2. 创建语音识别SpeechSynthesizerRequest对象.
   *
   * 默认为实时短文本语音合成请求, 支持一次性合成300字符以内的文字,
   * 其中1个汉字、1个英文字母或1个标点均算作1个字符,
   * 超过300个字符的内容将会报错(或者截断).
   * 一次性合成超过300字符可考虑长文本语音合成功能.
   *
   * 实时短文本语音合成文档详见: https://help.aliyun.com/document_detail/84435.html
   * 长文本语音合成文档详见: https://help.aliyun.com/document_detail/130509.html
   */
  SpeechSynthesizerRequest* request =
      NlsClient::getInstance()->createSynthesizerRequest(AlibabaNls::LongTts);
  if (request == NULL) {
    printf("createSynthesizerRequest failed.\n");
    cbParam->audioFile.close();
    delete cbParam;
    return NULL;
  }

  // 设置音频合成结束回调函数
  request->setOnSynthesisCompleted(OnSynthesisCompleted, cbParam);
  // 设置音频合成通道关闭回调函数
  request->setOnChannelClosed(OnSynthesisChannelClosed, cbParam);
  // 设置异常失败回调函数
  request->setOnTaskFailed(OnSynthesisTaskFailed, cbParam);
  // 设置文本音频数据接收回调函数
  request->setOnBinaryDataReceived(OnBinaryDataRecved, cbParam);
  // 设置字幕信息
  request->setOnMetaInfo(OnMetaInfo, cbParam);

  request->setAppKey(tst->appkey.c_str());
  // 设置账号校验token, 必填参数
  request->setToken(tst->token.c_str());

  // 设置待合成文本, 必填参数. 文本内容必须为UTF-8编码
  // 一次性合成超过300字符可考虑长文本语音合成功能.
  // 长文本语音合成文档详见: https://help.aliyun.com/document_detail/130509.html
  request->setText(tst->text.c_str());
  // 发音人, 包含"xiaoyun", "ruoxi", "xiaogang"等. 可选参数, 默认是xiaoyun
  request->setVoice("siqi");
  // 访问个性化音色，访问的Voice必须是个人定制音色
  //request->setPayloadParam("{\"enable_ptts\":true}");
  // 音量, 范围是0~100, 可选参数, 默认50
  request->setVolume(50);
  // 音频编码格式, 可选参数, 默认是wav. 支持的格式pcm, wav, mp3
  request->setFormat("wav");
  // 音频采样率, 包含8000, 16000. 可选参数, 默认是16000
  request->setSampleRate(16000);
  // 语速, 范围是-500~500, 可选参数, 默认是0
  request->setSpeechRate(0);
  // 语调, 范围是-500~500, 可选参数, 默认是0
  request->setPitchRate(0);
  // 开启字幕
  request->setEnableSubtitle(true);

  // 3: start()为异步操作。成功则开始返回BinaryRecv事件。失败返回TaskFailed事件。
  int ret = request->start();
  if (ret < 0) {
    printf("start() failed. may be can not connect server. please check network or firewalld\n");
    NlsClient::getInstance()->releaseSynthesizerRequest(request); // start()失败，释放request对象
    cbParam->audioFile.close();
    delete cbParam;
    return NULL;
  }

  struct timeval now;
  struct timespec outtime;
  // 4: 通知云端数据发送结束.
  // stop()为无意义接口，调用与否都会跑完全程，均需等待closed事件回调.
  // cancel()立即停止工作, 且不会有回调返回, 失败返回TaskFailed事件。
  //ret = request->cancel();
  ret = request->stop();
  if (ret == 0) {
    printf("wait closed callback.\n");
    // 语音服务器存在来不及处理当前请求, 10s内不返回任何回调的问题,
    // 然后在10s后返回一个TaskFailed回调, 所以需要设置一个超时机制.
    gettimeofday(&now, NULL);
    outtime.tv_sec = now.tv_sec + 30;
    outtime.tv_nsec = now.tv_usec * 1000;
    // 等待closed事件后再进行释放, 否则会出现崩溃
    pthread_mutex_lock(&(cbParam->mtxWord));
    if (ETIMEDOUT == pthread_cond_timedwait(&(cbParam->cvWord), &(cbParam->mtxWord), &outtime)) {
      printf("synthesis timeout.\n");
    }
    pthread_mutex_unlock(&(cbParam->mtxWord));
  }

  NlsClient::getInstance()->releaseSynthesizerRequest(request);

  cbParam->audioFile.close();
  delete cbParam;

  return NULL;
}

// 合成单个文本数据
int speechSynthesizerFile(const char* appkey) {
  //获取当前系统时间戳，判断token是否过期。
  std::time_t curTime = std::time(0);
  if (g_expireTime - curTime < 10) {
    printf("the token will be expired, please generate new token by AccessKey-ID and AccessKey-Secret.\n");
    if (generateToken(g_akId, g_akSecret, &g_token, &g_expireTime) < 0) {
      return -1;
    }
  }

  ParamStruct pa;
  pa.token = g_token;
  pa.appkey = appkey;
  pa.text = "今天天气很棒，适合去户外旅行.";

  // 启动一个工作线程，用于单次识别。
  pthread_t pthreadId;
  pthread_create(&pthreadId, NULL, &pthreadFunc, (void *)&pa);
  pthread_join(pthreadId, NULL);
  return 0;
}

// 合成多个文本数据。
// SDK多线程指一个文本数据对应一个线程，非一个文本数据对应多个线程。
// 示例代码为同时开启2个线程合成2个文件。
// 免费用户并发连接不能超过2个。
#define AUDIO_TEXT_NUMS 2
#define AUDIO_TEXT_LENGTH 64
int speechTranscriberMultFile(const char* appkey) {
  //获取当前系统时间戳判断token是否过期。
  std::time_t curTime = std::time(0);
  if (g_expireTime - curTime < 10) {
    printf("the token will be expired, please generate new token by AccessKey-ID and AccessKey-Secret.\n");
    if (generateToken(g_akId, g_akSecret, &g_token, &g_expireTime) < 0) {
      return -1;
    }
  }

  const char texts[AUDIO_TEXT_NUMS][AUDIO_TEXT_LENGTH] =
  {
    "今日天气真不错，我想去操作踢足球.",
    "明天有大暴雨，还是宅在家里看电影吧."
  };
  ParamStruct pa[AUDIO_TEXT_NUMS];
  for (int i = 0; i < AUDIO_TEXT_NUMS; i ++) {
      pa[i].token = g_token;
      pa[i].appkey = appkey;
      pa[i].text = texts[i];
  }
  std::vector<pthread_t> pthreadId(AUDIO_TEXT_NUMS);     // 启动工作线程，同时识别音频文件。
  for (int j = 0; j < AUDIO_TEXT_NUMS; j++) {
      pthread_create(&pthreadId[j], NULL, &pthreadFunc, (void *)&(pa[j]));
  }
  for (int j = 0; j < AUDIO_TEXT_NUMS; j++) {
      pthread_join(pthreadId[j], NULL);
  }
  return 0;
}

int main(int argc, char* argv[]) {
  printf("Usage: ./demo <your appkey> <your AccessKey ID> <your AccessKey Secret>\n");

  std::string appkey = getenv("NLS_APPKEY_ENV");
  g_akId = getenv("NLS_AK_ENV");
  g_akSecret = getenv("NLS_SK_ENV");

  // 根据需要设置SDK输出日志。可选。
  // 此处表示SDK日志输出至log-synthesizer.txt。
  // LogDebug表示输出所有级别日志，支持LogDebug、LogInfo、LogWarning、LogError。
  // 400表示单个文件400MB。50表示50个日志文件循环记录。
  int ret = NlsClient::getInstance()->setLogConfig(
      "log-synthesizer", LogDebug, 400, 50);
  if (ret < 0) {
    printf("set log failed.\n");
    return -1;
  }

  // 设置运行环境需要的套接口地址类型, 默认为AF_INET
  // 必须在startWorkThread()前调用
  //AlibabaNls::NlsClient::getInstance()->setAddrInFamily("AF_INET");

  // 私有云部署的情况下可进行直连IP的设置
  // 必须在startWorkThread()前调用
  //NlsClient::getInstance()->setDirectHost("106.15.83.44");

  // 存在部分设备在设置了dns后仍然无法通过SDK的dns获取可用的IP,
  // 可调用此接口主动启用系统的getaddrinfo来解决这个问题.
  //NlsClient::getInstance()->setUseSysGetAddrInfo(true);

  // 启动工作线程, 在创建请求和启动前必须调用此函数, 可理解为对NlsClient的初始化
  // 入参为负时, 启动当前系统中可用的核数。
  // 200并发以下推荐入参为1, 更高并发入参推荐可看readme。
  NlsClient::getInstance()->startWorkThread(1);

  // 合成单个文本
  speechSynthesizerFile(appkey.c_str());
  // 合成单个文本
  //speechSynthesizerMultFile(appkey.c_str());

  // 所有工作完成，进程退出前，释放nlsClient。
  // 请注意releaseInstance()非线程安全, 需要确认所有请求都停止工作才可释放。
  NlsClient::releaseInstance();

  return 0;
}
```

## 常见问题

### C++ SDK（3.0及以后版本）使用语音合成和语音识别功能，可以提高GCC5.0以上的编译版本吗？

可以。Linux下支持GCC 4.8.5或以上版本。目前已验证且顺利编译运行的GCC版本包括4.8.5、5.5.0、8.4.0。

### 为什么链接不到framework？

framework中代码采用Objective-C和C++混合编写而成，所以需要使用.mm后缀文件进行调用，同时请确保工程的头文件路径与库文件路径设置正确。

### C++ SDK ASR请求有DNS解析失败的情况导致异常，报错ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): GetInetAddressByHostname:252 DNS: resolved timeout.ali-recog-skd.log:AliSpeech\_C++SDK(ERROR): start:76 start failed: DNS: resolved timeout..unimrcpserver\_current.log: \[ERROR\] \[\[./ali/AliRecogChannel.cpp:772,onTaskFailed\]\]Ali Task start failed Msg :DNS: resolved timeout., start finised."如何解决？

- 旧版（3.0及以前版本）：在高并发或者电脑DNS忙碌的情况下容易出现以上问题，建议您更新到3.1.X版本，或进行再次重启请求。

- 新版（3.0及以后版本）：已经对此问题进行防御，若仍然偶现此问题，则为电脑DNS忙碌，需要再次重启请求。


### C++ SDK（新）集成到其他项目中时，将CMakeLists.txt中的add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=0) 修改为add\_definitions(-D\_GLIBCXX\_USE\_CXX11\_ABI=1)后编译不通过该如何解决？

除了`CMakeLists.txt`，全工程都需要修改该参数，例如`config/linux.thirdparty.debug.cmake`和`config/linux.thirdparty.release.cmake`，请在全目录搜索`_GLIBCXX_USE_CXX11_ABI`进行修改。

### C++ SDK旧版NlsSdkCpp2.0和新版NlsSdkCpp3.X的区别是什么？

NlsSdkCpp2.0版本的SDK每一个请求为一个线程，且接口为同步接口。

NlsSdkCpp3.X版本的SDK内部由第三方库libevent统一处理事件消息，并发性能更强，且接口为异步接口。

### C++版的SDK不支持实现C11规范吗？ 现在导致项目无法链接SDK该如何解决？

工程默认为`_GLIBCXX_USE_CXX11_ABI=0`，全工程都需要修改该参数，请在全目录搜索`_GLIBCXX_USE_CXX11_ABI`进行修改。

### C++ SDK测试Demo成功，集成项目报错，DNS解析失败，报错 **nls-gateway-cn-shanghai.aliyuncs.com dns failed: nodename nor servname provided, or not known如何解决？**

1. SDK中会查看当前设备开启的所有协议族（IPv4、IPv6）进行DNS解析请求，`nls-gateway-cn-shanghai.aliyuncs.com`不支持 IPv6，返回解析错误，从而导致SDK DNS解析失败退出。可禁用当前设备的IPv6协议族，后续CppSdk产品改进对这方面进行可配置处理。

2. 建议您升级到3.1.12及以后版本。


### C++ SDK测试Demo可以成功，集成项目报错，网络链接失败，报错\[dnsEventCallback:465\]Node:0x7f087c001030 ai\_canonname: nls-gateway-cn-shanghai.aliyuncs.com.gds.alibabadns.com\[dnsEventCallback:477\]Node:0x7f087c001030 IpV4:106.15.XX.XX\[connectProcess:1329\]Node:0x7f087c001030 sockFd:41\[connectProcess:1347\]Node:0x7f087c001030 new Socket ip:106.15.XX.XX port:443 Fd:41.\[socketConnect:1458\]Node:0x7f087c001030 Connect failed:Network is unreachable. retry...如何解决？

以上现象为无法连接网络，查看日志发现DNS域名解析出来的IP链接不成功，进一步通过Ping判断网络不通。由于本地拦截DNS解析，导致SDK内部`libevent`的`evdns_getaddrinfo`获得错误的IP。

解决办法：

- 3.1.12版本以前可将`evdns_getaddrinfo()`手动替换成系统的getaddrinfo()。

- 3.1.12版本可在`CMakeLists.txt`中修改`add_definitions(-DNLS_USE_NATIVE_GETADDRINFO)`。

- 3.1.12及以后版本增加`setDirectHost()`接口，您可以在SDK外部进行DNS解析，获取正确IP后通过该接口设入。

- 3.1.13及以后版本已解决此问题，若运行时仍存在上述问题，建议调用接口`setUseSysGetAddrInfo(true)`。


### C++ SDK语音合成时传入的文本没有采用UTF-8编码会有什么错误信息？

如果传入的文本没有采用UTF-8编码，在文本中含有中文字符时，语音合成SDK调用start函数会失败，返回错误信息`Socket recv failed, errorCode: 0`。错误码为0表示服务端已经关闭了连接，此时应检查传入的文本是否采用UTF-8编码。

### SDK报错“DNS resolved timeout”是什么问题？

查看`/etc/resolv.conf`文件中nameserver的设置，建议增加并优先使用以下配置：`nameserver``114.114.114.114`。