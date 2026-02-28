### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/) [开发参考](https://help.aliyun.com/zh/isi/developer-reference/) [语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/) [离线语音合成](https://help.aliyun.com/zh/isi/developer-reference/offline-speech-synthesis/) 接口说明

# 接口说明

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：开通授权](https://help.aliyun.com/zh/isi/developer-reference/enable-authorization)[下一篇：Android SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-android)

该文章对您有帮助吗？

反馈

离线语音合成是指在弱网或无网状态下，通过设备本地的语音合成模型，将文本转换成自然流畅的语音。

## 功能介绍

离线语音合成主要包括以下功能，暂不支持多实例调用。

- 提供语速调节、语调调节、音量调节功能。

- 适用于车载导航、智能硬件、文学有声阅读和无障碍播报等场景。

- 以SDK的方式集成，支持多种不同硬件平台。

- 按照设备激活数量收费，收费更加灵活可控。

- 提供多种音色选择。


## 前提条件

已激活SDK，具体请参见 [开通授权](https://help.aliyun.com/zh/isi/developer-reference/enable-authorization#task-2083188 "")。

## 语音包列表

|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 名称 | voice参数值 | 类型 | 适用场景 | 支持语言 | 支持采样率（Hz） | 备注 | 下载链接 |
| 艾佳 | aijia | 标准女声 | 通用场景 | 支持中文及中英文混合场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/a9f6fd18-cf0c-45a0-83b0-718ccfa36212.zip) |
| 艾诚 | aicheng | 温暖男声 | 通用场景 | 支持中文及中英文混合场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/15b64d3f-ee9b-409a-bac6-e319596dfe91.zip) |
| 艾琪 | aiqi | 温柔女声 | 通用场景 | 支持中文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/b7b1152b-0174-44e9-88a8-2525695eb45c.zip) |
| 艾达 | aida | 标准男声 | 通用场景 | 支持中文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/5b44533f-0d00-43f6-8bbc-f8752afec4df.zip) |
| 艾浩 | aihao | 资讯男声 | 文学场景 | 支持中文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/d95c5709-8a2f-4473-959d-08a8a1f0019c.zip) |
| 艾硕 | aishuo | 自然男声 | 客服场景 | 支持中文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/1b4b3829-b95c-411c-b960-21f0cef77fc9.zip) |
| 艾颖 | aiying | 软萌童声 | 文学场景 | 支持中文及中英文混合场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/ce7b0092-51e3-41f6-9119-0f0511355f80.zip) |
| 艾彤 | aitong | 儿童音 | 童声场景 | 仅支持纯中文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/5637b419-1515-46f5-b9bf-52b381e0a3a8.zip) |
| Abby | abby | 美语女声 | 英文场景 | 仅支持英文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/de45872e-f2a4-4c75-8c9c-6cb1570cf39e.zip) |
| Andy | andy | 美语男声 | 英文场景 | 仅支持英文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/3798c839-c5e6-4ff1-b69e-004bbf51be64.zip) |
| Annie | annie | 美语女声 | 英文场景 | 仅支持英文场景 | 24K | 精品版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/96affc9e-9a20-4dee-8ae7-a0aa8953493c.zip) |
| 小云 | xiaoyun | 标准女声 | 通用场景 | 支持中文及中英文混合场景 | 16K | 标准版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/43a0c626-c40d-4762-92b0-2c0e1fa8ef79.zip) |
| 小达 | xiaoda | 标准男声 | 通用场景 | 中文及中英文混合场景 | 16K | 标准版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/60d0b806-6518-4cb1-91b4-6807fd8d3d49.zip) |
| 小刚 | xiaogang | 温暖男声 | 通用场景 | 中文及中英文混合场景 | 16K | 标准版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/329c607b-3235-4fd0-8bc2-c87ada55bb36.zip) |
| 小琪 | xiaoqi | 温柔女声 | 通用场景 | 中文及中英文混合场景 | 16K | 标准版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/591aab02-82e2-4774-b76b-91c80e41813d.zip) |
| 小夏 | xiaoxia | 自然女声 | 客服场景 | 中文及中英文混合场景 | 16K | 标准版 | [下载语音包](https://gw.alipayobjects.com/os/bmw-prod/a346db66-357a-4708-8ad6-c7f1e6a9691d.zip) |

## 时序图

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2402912771/CAEQShiBgIDQmKX22BgiIGU2NjhiZGY0NTNhMjQyY2FiODlkNmNkOTk2YTBjZmVl4024928_20231008170233.737.svg)

## 激活及初始化参数说明

介绍离线TTS SDK激活及初始化时需要设置的参数，主要包括鉴权信息、工作路径及日志存储路径。

**重要**

初始化参数设置并启用后，无法变更。

|     |     |     |     |
| --- | --- | --- | --- |
| 参数 | 类型 | 说明 | 是否必须 |
| ak\_id | string | AccessKey ID，获取方式请参见 [开通服务](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-1917889 "")。 | 是 |
| ak\_secret | string | AccessKey Secret，获取方式请参见 [开通服务](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-1917889 "")。 | 是 |
| app\_key | string | 项目Appkey，在项目创建完成后自动生成。可以单击控制台导航栏 **全部项目** 查看对应项目Appkey。 | 是 |
| sdk\_code | string | 产品码。<br>- 标准版sdk\_code：software\_nls\_tts\_offline\_standard<br>  <br>- 精品版sdk\_code：software\_nls\_tts\_offline | 是 |
| device\_id | string | 设备标识。<br>**说明** <br>一个Appkey中的device\_id全局唯一。 | 是 |
| workspace | string | 资源路径。 | 是 |
| mode\_type | string | 设为“0”，初始化本地引擎。 | 是 |
| debug\_path | string | 日志存储路径。<br>**说明** <br>加入该字段表明开启日志存储。<br>如果要关闭日志存储，可在动态参数设置中将 **debug\_level** 参数等级设为5。<br>日志文件以追加方式存储。 | 否 |
| enable\_et | string | 取值true或false。设为false时关闭打点，默认开启。<br>关于打点的说明，请参见 [SDK是如何进行“打点”的？](https://help.aliyun.com/zh/isi/developer-reference/faq-about-offline-speech-synthesis#section-5y4-ppf-8rp "") | 否 |
| enable\_ntp | string | 取值true或false。设为false时关闭NTP，默认开启。<br>NTP功能用于获取阿里云时间用于鉴权，请参见 [NTP的作用是什么？](https://help.aliyun.com/zh/isi/developer-reference/faq-about-offline-speech-synthesis#section-drv-r09-69j "") | 否 |
| enable\_low\_precision | string | 取值true或false。默认值取false，表示采用高精度模式；设为true时是采用低精度方式，计算量会下降，同时音质也会略下降。 | 否 |
| authspace | string | 为方便调试，将鉴权文件生成至固定目录（如“/storage/emulated/0/tts”， 请确保该目录存在，并可读写），避免卸载app重装时再次鉴权，主要用于接入时调试。不设置该参数时，鉴权文件将存在workspace目录下。 | 否 |
| extend | string | 拓展字段（JSON）。 | 否 |

## 动态参数说明

- 属性in表示可以设置给SDK的参数。in属性的参数可以通过setparamTts（以Android为例）动态设置，设置完成后下一条生效。

- 属性out表示从SDK获取的参数。out属性的参数可以通过getparamTts获取。


|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| 参数 | 类型 | 属性 | 取值 | 含义 |
| extend\_font\_name | string | in | full\_path | 发音人切换。<br>语音包资源完整路径， 如/sdcard/xiaoyun。 |
| speed\_level | string | in\|out | (0, 2\]，默认1.0 | 语速，值越大语速越快。<br>设置的值超过范围将取默认值。 |
| pitch\_level | string | in\|out | \[-500,500\]，默认0 | 声调，值越大声音越尖锐。<br>设置的值超过范围将取默认值。 |
| volume | string | in\|out | (0，2\]，默认1.0 | 音量，值越大音量越大。<br>设置的值超过范围将取默认值。<br>**重要** <br>为避免截幅引入“吱吱”噪声，建议取值限定在1.5以下。 |
| callback\_raw\_data | string | in | 0、1，默认0 | - 0：回调原始数据。<br>  <br>- 1：回调解码后数据，如原始合成数是mp3，那么将回调pcm数据。 |
| debug\_level | string | in\|out | 0、1、2、3、4、5 | 日志等级<br>- 0：verbose 无过滤<br>  <br>- 1：debug<br>  <br>- 2：info<br>  <br>- 3：warning<br>  <br>- 4：error<br>  <br>- 5：关闭日志 |
| error\_msg | string | out | 错误信息 | 在调用接口发生错误时，获取详细的错误信息。建议用户在打点时重点考虑该信息，是分析问题的有效手段。 |
| model\_sample\_rate | string | out | 16000、24000 | 音频数据采样率，通常是24000。 |
| enable\_callback\_vol | string | in | 0、1，默认0 | - 0：不回调音量<br>  <br>- 1：回调音量，会有一定的资源消耗，非必要时关闭。 |
| enable\_monopoly | string | in | 0、1，默认1 | - 0：开启非独占模式，合成速度变慢，CPU峰值下降。<br>  <br>- 1：开启独占模式，合成速度快，CPU峰值相对较高。 |

## 性能指标

**说明**

以中文发音人aicheng为例（不同发音人略有差异）。

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| 项目 | 指标 |
| CPU | 机型 | 硬件指标 | 初始化耗时 | CPU（合成态：单核） |
| 红米6A | CPU：联发Helio A22 2 GHz<br>RAM：2 GB<br>系统：Android 9.0 | 273ms | 19% |
| 华为P10 | CPU：海思麒麟960 2.4 GHz<br>RAM：4 GB<br>系统：Android 7.0 | 178ms | 12% |
| 华为P40 | CPU型号：海思麒麟9902.86 GHz<br>RAM：6 GB<br>系统：Android 10.0 | 67ms | 8.2% |
| ROM | - 参照SDK包大小<br>  <br>- 由语音包个数及大小决定 |
| RAM | 21.73 M |

## 错误码

如果语音合成发生错误，SDK将上报TTS\_EVENT\_ERROR事件，并提供错误码信息，如下表所示。

### **通用错误码**

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 40000000 | 默认的客户端错误码，对应了多个错误消息。 | 用户使用了不合理的参数或者调用逻辑。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000001 | The token 'xxx' has expired；<br>The token 'xxx' is invalid | 用户使用了不合理的参数或者调用逻辑。通用客户端错误码，通常是涉及Token相关的不正确使用，例如Token过期或者非法。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000002 | Gateway:MESSAGE\_INVALID:Can't process message in state'FAILED'! | 无效或者错误的报文消息。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000003 | PARAMETER\_INVALID;<br>Failed to decode url params | 用户传递的参数有误，一般常见于RESTful接口调用。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40000005 | Gateway:TOO\_MANY\_REQUESTS:Too many requests! | 并发请求过多。 | 如果是试用版调用，建议您升级为商用版本以增大并发。<br>如果已是商用版，可购买并发资源包，扩充您的并发额度。 |
| 40000009 | Invalid wav header! | 错误的消息头。 | 如果您发送的是WAV语音文件，且设置`format`为`wav`，请注意检查该语音文件的WAV头是否正确，否则可能会被服务端拒绝。 |
| 40000009 | Too large wav header! | 传输的语音WAV头不合法。 | 建议使用PCM、OPUS等格式发送音频流，如果是WAV，建议关注语音文件的WAV头信息是否为正确的数据长度大小。 |
| 40000010 | Gateway:FREE\_TRIAL\_EXPIRED:The free trial has expired! | 试用期已结束，并且未开通商用版、或账号欠费。 | 请登录控制台确认服务开通状态以及账户余额。 |
| 40010001 | Gateway:NAMESPACE\_NOT\_FOUND:RESTful url path illegal | 不支持的接口或参数。 | 请检查调用时传递的参数内容是否和官网文档要求的一致，并结合错误信息对比排查，设置为正确的参数。<br>比如您是否通过curl命令执行RESTful接口请求， 拼接的URL是否合法。 |
| 40010003 | Gateway:DIRECTIVE\_INVALID:\[xxx\] | 客户端侧通用错误码。 | 表示客户端传递了不正确的参数或指令，在不同的接口上有对应的详细报错信息，请参考对应文档进行正确设置。 |
| 40010004 | Gateway:CLIENT\_DISCONNECT:Client disconnected before task finished! | 在请求处理完成前客户端主动结束。 | 无，或者请在服务端响应完成后再关闭链接。 |
| 40010005 | Gateway:TASK\_STATE\_ERROR:Got stop directive while task is stopping! | 客户端发送了当前不支持的消息指令。 | 请参考官网文档示例代码进行对比测试验证。 |
| 40020105 | Meta:APPKEY\_NOT\_EXIST:Appkey not exist! | 使用了不存在的Appkey。 | 请确认是否使用了不存在的Appkey，Appkey可以通过登录控制台后查看项目配置。 |
| 40020106 | Meta:APPKEY\_UID\_MISMATCH:Appkey and user mismatch! | 调用时传递的Appkey和Token并非同一个账号UID所创建，导致不匹配。 | 请检查是否存在两个账号混用的情况，避免使用账号A名下的Appkey和账号B名下生成的Token搭配使用。 |
| 403 | Forbidden | 使用的Token无效，例如Token不存在或者已过期。 | 请设置正确的Token。Token存在有效期限制，请及时在过期前获取新的Token。 |
| 41000003 | MetaInfo doesn't have end point info | 无法获取该Appkey的路由信息。 | 请检查是否存在两个账号混用的情况，避免使用账号A名下的Appkey和账号B名下生成的Token搭配使用。 |
| 41010101 | UNSUPPORTED\_SAMPLE\_RATE | 不支持的采样率格式。 | 当前实时语音识别只支持8000 Hz和16000 Hz两种采样率格式的音频。 |
| 41040201 | Realtime:GET\_CLIENT\_DATA\_TIMEOUT:Client data does not send continuously! | 获取客户端发送的数据超时失败。 | 客户端在调用实时语音识别时请保持实时速率发送，发送完成后及时关闭链接。 |
| 50000000 | GRPC\_ERROR:Grpc error! | 受机器负载、网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |
| 50000001 | GRPC\_ERROR:Grpc error! | 受机器负载、网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |
| 52010001 | GRPC\_ERROR:Grpc error! | 受机器负载、网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |

### **语音合成/长文本语音合成错误码**

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 40000001 | Gateway:ACCESS\_DENIED:No privilege to this voice! | 设置了错误的发音人名称。 | 请参考官网文档，设置正确的发音人。 |
| 40000004 | Gateway:IDLE\_TIMEOUT:Websocket session is idle for too long time,the last directive is 'StartSynthesis'! | 请求建立链接后，长时间没有发送任何数据，超过10s后服务端会返回此错误信息。 | 请求处理完成后请及时关闭链接，此外，当服务端瞬时压力过大不能及时返回数据时也可能出现此错误，此时可以重试恢复。 |
| 40010003 | Gateway:DIRECTIVE\_INVALID:No text specified! | 没有设置有效的待合成文本文字。 | 请参考官网文档示例代码设置待合成的文本。 |
| 41020001 | 语音合成调用客户端错误 | 可能有多个错误消息，需根据对应的错误消息调整。 | - 如果提示`Engine return error code: 424.`表示传递的背景音乐或拼接录音不符合格式，请参考文档说明设置正确的背景音。<br>  <br>- 如果提示`Engine return error code:418`表示传递了不支持的发音人名称。<br>  <br>- 如果提示`Engine return error code: 413`表示使用的SSML格式错误。<br>  <br>- 如果提示`Request json illegal,failed to parse request.`表示传递的JSON格式非法。<br>  <br>- 如果提示`SSML text length should be less than 300.`表示传递的合成文本过长，建议使用长文本语音合成接口。 |
| 51020001 | TTS:TtsServerError | 受机器负载或网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |

### **语音合成/离线语音合成**

- SDK相关


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 140000 | TTS\_CREATE\_FAILED | 引擎初始化失败。 | 资源路径错误或资源文件异常，常伴随着错误码（TTS\_ASSETPATH\_INVALID），可查看日志后再确认。确保传入资源路径有效，资源文件齐全。 |
| 140001 | TTS\_ENGINE\_INVALID | 引擎没有初始化。 | 当前TTS实例未创建，请检查是否已经调用初始化接口。 |
| 140002 | TTS\_TEXT\_ERROR | 文本非法，如空等。 | 可查看SDK日志确认文件非法情况，确保传入的文本是有效的。 |
| 140003 | TTS\_MALLOC\_FAILED | 内存申请失败。 | 当前内存不足，请确保足够运行内存。 |
| 140005 | TTS\_ASSETPATH\_INVALID | 资源路径为空。 | 资源路径错误或资源文件异常，可查看日志后再确认。确保传入资源路径有效，资源文件齐全。 |
| 140006 | TTS\_HANLDE\_INVALID | 处理线程不存在。 | 可释放TTS后重新尝试。 |
| 140007 | TTS\_CREATE\_HANLDE\_FAILED | 创建处理线程失败。 | 请查看日志中错误信息进行定位。 |
| 140008 | TTS\_AUTH\_FAILED | 鉴权失败，无法继续使用SDK。 | 请检查传入的akId、akSecret和appkey的正确性。可通过查看日志中错误信息确认问题细节，可能是未开通离线鉴权、已耗尽配额等。 |
| 140011 | TTS\_OPERATE\_INVALID | 非法操作。 | 当前处理线程状态非法，可能是在未初始化情况下调用了pause接口等，请确保调用接口符合当前状态。 |
| 140012 | TTS\_OPEN\_FILE\_FAILED | 打开文件失败。 | 打开wav debug文件失败，或打开日志文件失败。详细可查看日志错误信息进行确认。 |
| 140013 | TTS\_STATE\_INVALID | 状态机校验失败。 | 当前方法调用不符合当前状态机，可能是在未初始化情况下调用了pause接口等，请确保调用接口符合当前状态。 |
| 140014 | TTS\_SYNTHESIZER\_INIT\_ERROR | 合成器初始化失败。 | 创建合成器失败，主要是因为内存不足。 |
| 140015 | TTS\_SYNTHESIZER\_RELEASE\_ERROR | 合成器释放失败。 | 合成器释放失败，需要查看日志详细定位。 |
| 140016 | TTS\_SYNTHESIZER\_FAILED | 合成失败。 | 预播放时状态错误，需查看日志详细定位。 |
| 140017 | TTS\_WAIT\_TIMEOUT | 超时退出。 | 等待某个状态超时，需查看日志详细定位。 |
| 140018 | TTS\_CLOSED | 没有编译TTS部分代码。 | 表示当前SDK中不包含TTS功能，请更换正确SDK运行。 |

- 参数配置相关


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 140100 | TTS\_PARAM\_INVALID | 参数无效。 | 初始化或设置参数时有无效入参，比如空workspace、空回调、空taskId或空文本等。需要查看日志详细定位。 |
| 140101 | TTS\_PARAM\_VALUE\_INVALID | 参数值无效。 | 设置参数时无效入参，需要查看日志详细定位。 |
| 140102 | TTS\_CFG\_OPEN\_FAILED | 配置文件打开失败。 | 资源路径错误或资源文件异常，可查看日志再确认。确保传入资源路径有效，资源文件齐全。 |

- 音频处理


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 140200 | TTS\_AM\_CREATE\_FAILED | 播放器创建失败。 | SDK内部音频管理器创建失败。 |
| 140210 | TTS\_AM\_OPEN\_FAILED | 播放器打开失败。 | SDK内部音频管理器打开失败，需要查看日志详细定位。 |
| 140210 | TTS\_DECODER\_INIT\_FAILED | 音频解码器初始化失败。 | 音频解码器（可能为MP3解码器）初始化失败，需要查看日志详细定位。 |
| 140211 | TTS\_DECODER\_MALLOC\_FAILED | 音频解码器申请内存失败。 | 当前内存不足，请确保足够运行内存。 |
| 140212 | TTS\_DECODER\_INPUT\_TOO\_MANY | 单次输入过多数据，将被丢掉。 | 查看日志确定单次输入数据上限（2000），具体问题需查看日志详细定位。 |
| 140213 | TTS\_DECODER\_OUTPUT\_TOO\_MANY | 输出过多数据，超过缓存，会丢失。 | 需查看日志详细定位。 |
| 140220 | TTS\_AP\_INIT\_FAILED | 音频处理单元打开失败（audioplayer）。 | 一般会伴随着其他AP ErrorCode返回，需要查看日志详细定位。 |
| 140221 | TTS\_AP\_START\_FAILED | ap启动出错。 | 需查看日志详细定位。 |
| 140222 | TTS\_AP\_MALLOC\_FAILED | audioplayer内存申请失败 | 当前内存不足，请确保足够运行内存。 |
| 140231 | TTS\_BGM\_DECODE\_INVALID | 解码器初始化失败 | 确认解码器是否已经初始化，可查看日志进行详细定位。 |
| 140233 | TTS\_BGM\_MALLOC\_FAILED | 内存申请失败 | 当前内存不足，请确保足够运行内存。 |
| 140237 | TTS\_BGM\_PARAM\_INVALID | 背景音乐参数设置错误 | 确认设置参数是否正确，可查看日志详细定位。重点关注日志bgm value:。 |

- cache相关


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 140300 | TTS\_CACHE\_INIT\_FAILED | 初始化cache失败。 | 通常伴随着错误码TTS\_CACHE\_PATH\_INVALID，可能是存储路径无效，可通过日志详细定位。 |
| 140302 | TTS\_CACHE\_CMD\_ERROR | 下达cache指令不合规范。 | 可查看返回的错误消息和日志详细定位。 |
| 140308 | TTS\_CACHE\_PATH\_INVALID | 无法创建缓存路径。 | 可查看返回的错误消息和日志详细定位。 |
| 140309 | TTS\_CACHE\_LIST\_CREATE\_FAILED | cache列表创建失败。 | 可查看返回的错误消息和日志详细定位。 |
| 140311 | TTS\_CACHE\_TOO\_MANY | 缓存太多。 | 可查看日志详细定位。 |
| 140312 | TTS\_CACHE\_PARAM\_INVALID | 参数错误。 | 可查看返回的错误消息和日志详细定位。 |
| 140313 | TTS\_CACHE\_RECORDING\_OPEN\_FAILED | 打开本地文件错误。 | 文件权限、路径可能存在问题，需要通过日志详细定位。 |

- font下发相关


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 140351 | TTS\_FONT\_INITLIST\_FAILED | 初始化fontlist管理器。 | 当前内存不足，请确保足够运行内存。 |
| 140352 | TTS\_FONT\_INITLIST\_INVALID | fontlist管理器未初始化。 | 当前内存不足，请确保足够运行内存。 |
| 140353 | TTS\_FONT\_CMD\_INVALID | 命令格式错误。 | 可查看返回的错误消息和日志详细定位。 |
| 140354 | TTS\_FONT\_RESPONSE\_ERROR | 服务端返回格式错误。 | 可查看返回的错误消息和日志详细定位。 |
| 140350 | TTS\_FONT\_RESPONSELIST\_ERROR | fontlist请求服务端返回格式错误。 | 可查看返回的错误消息和日志详细定位。 |
| 140356 | TTS\_FONT\_GET\_FONTLIST\_FAILED | 获取fontlist失败。 | 可查看返回的错误消息和日志详细定位。 |
| 140358 | TTS\_FONT\_LOCALMSG\_ERROR | 本地list文件解析失败。 | 可查看返回的错误消息和日志详细定位。 |
| 140359 | TTS\_FONT\_LOCALFILE\_ERROR | 本次list文件保存失败。 | 可查看返回的错误消息和日志详细定位。 |
| 140360 | TTS\_FONT\_CLOUDMSG\_ERROR | 云端list解析失败。 | 可查看返回的错误消息和日志详细定位。 |

- 本地引擎相关


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 140900 | TTS\_LOCAL\_CRE\_ENGINE\_ERROR | 本地引擎初始化失败。 | 本地引擎内部错误，需要查看日志中其他错误信息进行定位。 |
| 140901 | TTS\_LOCAL\_ENGINE\_INVALID | 本地引擎没有初始化。 | 请检查是否已经初始化了TTS，可查看返回的错误消息和日志详细定位。 |
| 140902 | TTS\_LOCAL\_ASSET\_ERROR | 本地资源校验失败。 | 本地引擎从资源路径进行校验时失败，可查看日志详细定位。 |
| 140903 | TTS\_LOCAL\_CRE\_TASK\_ERROR | 创建本地task失败。 | 可查看日志详细定位。 |
| 140905 | TTS\_LOCAL\_START\_FAILED | 本地开始合成失败。 | 可查看日志详细定位。 |
| 140906 | TTS\_LOCAL\_OPERATION\_FAILED | 本地操作失败，比如本地task不存在或默认错误。 | 可查看日志详细定位。 |
| 140907 | TTS\_LOCAL\_SWITCH\_FONT\_FAILED | 切换发音人失败。 | 可查看日志详细定位。 |
| 140908 | TTS\_LOCAL\_GET\_SAMPLERATE\_FAILED | 获取发音人的采样率失败。 | 可查看日志详细定位。 |
| 140909 | TTS\_LOCAL\_ADD\_FRONT\_END\_FAILED | 添加发音人失败。 | 可查看日志详细定位。 |
| 140910 | TTS\_LOCAL\_VOICE\_PATH\_INVALID | 本地发音人文件不存在或文件鉴权失败。 | 可查看日志详细定位。 |
| 140911 | TTS\_LOCAL\_VOICE\_MISMATCH | 本地发音人文件不匹配。 | 可查看日志详细定位。 |

- 云端引擎相关


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 141000 | TTS\_CLOUD\_CREATE\_FAILED | 云端引擎初始化失败。 | 可查看日志详细定位。 |
| 141004 | TTS\_CLOUD\_START\_FAILED | 云端请求失败。 | 一般是因为联网失，或输入的Appkey、Token、URL等存在无效参数。具体可查看日志详细定位。 |
| 141007 | TTS\_CLOUD\_NETWORK\_BROKEN | 网络比较差。 | 弱网情况，请更换网络环境运行。 |
| 141008 | TTS\_CLOUD\_SSL\_CONNECT\_FAILED | SSL链接失败，请检查发送参数是否正确。 | SSL链接失败，请检查发送参数是否正确。具体可查看日志详细定位。 |
| 141009 | TTS\_CLOUD\_HTTP\_CONNECT\_FAILED | HTTP链接失败，请检查发送参数是否正确。 | HTTP链接失败，请检查发送参数是否正确。具体可查看日志详细定位。 |
| 141010 | TTS\_CLOUD\_DNS\_FAILED | 链接失败，DNS失败。 | 链接失败，DNS失败，请检查域名解析是否正确。具体可查看日志详细定位。 |
| 141011 | TTS\_CLOUD\_URL\_INVALID | URL无效。 | URL无效，可先ping一下确认URL和port是否有效。具体可查看日志详细定位。 |
| 141012 | TTS\_CLOUD\_PROTOCOL\_ERROR | 云端协议错误。 | 云端协议错误。具体可查看日志详细定位。 |
| 141013 | TTS\_CLOUD\_PARAMETERS\_ERROR | 参数错误。 | 云端参数错误。具体可查看日志详细定位。 |
| 141014 | TTS\_CLOUD\_UNKNOWN\_WS\_HEAD\_TYPE | WebSocket使用未知头类型。 | 旧客户端已知问题，建议升级到最新版本。 |

- 服务端状态码


|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 144001 | TTS\_CLOUD\_AUTH\_FAILED | 身份认证失败。 | 检查使用的令牌是否正确，是否过期。 |
| 144002 | TTS\_CLOUD\_INVALID\_MESSAGE | 无效的消息。 | 检查发送的消息是否符合要求。 |
| 144003 | TTS\_CLOUD\_INVALID\_TOKEN | 令牌过期或无效的参数。 | 首先检查使用的令牌是否过期，然后检查参数值设置是否合理。 |
| 144004 | TTS\_CLOUD\_WAIT\_TIMEOUT | 空闲超时。 | 确认是否长时间（超过10s）没有发送数据到服务端。 |
| 144005 | TTS\_CLOUD\_EXCEED\_CONCURRENCY | 请求数量过多。 | 检查是否超过了并发连接数或者每秒钟请求数。如果超过并发数，建议从免费版升级到商用版，或者商用版扩容并发资源。 |
| 144006 | TTS\_CLOUD\_DEFAULT\_ERROR | 云端返回的未分类错误。 | 比如使用了无效的模型ID，具体可查看日志详细定位。 |
| 144100 | TTS\_CLOUD\_INVALID\_INTERFACE | 不支持的接口。 | 使用了不支持的接口。 |
| 144101 | TTS\_CLOUD\_UNSUPPORTED\_ORDER | 不支持的指令。 | 使用了不支持的指令。 |
| 144102 | TTS\_CLOUD\_INVALID\_ORDER | 无效的指令。 | 指令格式错误。 |
| 144103 | TTS\_CLOUD\_CLIENT\_DISCONNECT | 客户端提前断开连接。 | 检查是否在请求正常完成之前关闭了连接。 |
| 144200 | TTS\_CLOUD\_INVALID\_APPKEY | 应用不存在。 | 检查应用AppKey是否正确，是否与Token归属同一个账号。 |
| 144300 | TTS\_CLOUD\_INVALID\_PARAM | 参数错误。 | 检查是否传递了正确的参数。 |
| 144301 | TTS\_CLOUD\_UNSENDAUDIO | 客户端10s未发送命令。 | 检查网络问题，或者检查业务中是否存在不发数据的情况。 |
| 144302 | TTS\_CLOUD\_SENDAUDIO\_TOO\_FAST | 客户端发送数据过快，服务器资源已经耗尽。 | 检测客户端发包是否过快，是否按照1:1的实时率发包。 |
| 144303 | TTS\_CLOUD\_INVALID\_AUDIO\_FORMAT | 客户端发送音频格式不正确。 | 请将音频数据的格式转换为SDK目前支持的音频格式。 |
| 144304 | TTS\_CLOUD\_INVALID\_INVOKE | 客户端调用方法异常。 | 客户端应该先调用发送请求接口，发送请求完毕后再调用其他接口。 |
| 144305 | TTS\_CLOUD\_INVALID\_MAX\_SILENCE | 客户端设置MAXSILENCE\_PARAM方法异常。 | 参数MAXSILENCE\_PARAM的范围为200～2000。 |
| 144306 | TTS\_CLOUD\_MISMATCHED\_SAMPLERATE | 采样率不匹配。 | 检查调用时设置的采样率和管控台上Appkey绑定的ASR模型采样率是否一致。 |
| 144400 | TTS\_CLOUD\_SERVER\_ERROR | TTS服务端错误。 | 如果偶现可以忽略。 |
| 144401 | TTS\_CLOUD\_INTERNAL\_SERVER\_ERROR | 服务端内部错误。 | 未知错误。 |
| 144402 | TTS\_CLOUD\_SPEECH\_TRANSCRIBER\_SERVER\_ERROR | 实时语音识别服务不可用。 | 检查实时语音识别服务是否有任务堆积等导致任务提交失败。 |
| 144403 | TTS\_CLOUD\_SPEECH\_TRANSCRIBER\_REQUEST\_TIMEOUT | 请求实时语音识别服务超时。 | 排查实时语音识别日志。 |
| 144404 | TTS\_CLOUD\_INVOKE\_SPEECH\_TRANSCRIBER\_FAILED | 调用实时语音识别服务失败。 | 检查实时语音识别服务是否启动，端口是否正常开启。 |
| 144405 | TTS\_CLOUD\_SPEECH\_TRANSCRIBER\_BALANCE\_FAILED | 实时语音识别服务负载均衡失败，未获取到实时语音识别服务的IP地址。 | 检查VPC中的实时语音识别服务机器是否有异常。 |
| 144406 | TTS\_CLOUD\_SERVER\_AGAIN | 内部调用错误。 | 内部服务错误，需要客户端进行重试。 |