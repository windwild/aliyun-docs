### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis-1/)接口说明

# 接口说明

更新时间：2025-05-27 22:49:49

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Latex能力支持说明](https://help.aliyun.com/zh/isi/developer-reference/cosyvoice-support-for-latex)[下一篇：RESTful API](https://help.aliyun.com/zh/isi/developer-reference/restful-api-3)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费和并发限制

功能介绍

就近地域智能接入

服务地址

交互流程

音色列表

多情感声音支持说明

服务状态码

通用错误码

语音合成/长文本语音合成错误码

语音合成为您提供将输入文本合成为语音二进制数据的功能。本文档介绍了当前目录下各SDK文档的通用信息。

[←返回语音合成产品详情页](https://ai.aliyun.com/nls/tts)

## **计费和并发限制**

- 语音合成提供试用版和商用版两种计费模式，详情请参见 [试用版和商用版](https://help.aliyun.com/zh/isi/product-overview/pricing#40ba8a7127hw1 "")。如果您需要将试用版升级为商用版，请参见 [试用版升级为商用版](https://help.aliyun.com/zh/isi/product-overview/billing-10#41bb3ea20c3v4 "")。

- 计费方式详情请参见 [计费方式](https://help.aliyun.com/zh/isi/product-overview/billing-10 "")。

- 并发限制请参见 [并发和QPS说明](https://help.aliyun.com/zh/isi/product-overview/faq-about-concurrency-and-monitoring "")。


## 功能介绍

- 支持输出PCM、WAV和MP3编码格式数据。

- 支持设置语速、语调和音量。

- 支持设置不同场景及风格的声音。参见 [音色列表](https://help.aliyun.com/zh/isi/developer-reference/overview-of-speech-synthesis#5186fe1abb7ag "")。

- 支持一次性合成300字符以内的文字，其中1个汉字、1个英文字母、1个标点或1个句子中间空格均算作1个字符，超过300个字符的内容将会截断。

- 仅支持采用UTF-8编码的文本输入。

- 支持 [多情感声音](https://help.aliyun.com/zh/isi/developer-reference/overview-of-speech-synthesis#section-ain-atc-dko "") 调用，具体请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview#sectiondiv-g6w-isw-rmw "") 中的<emotion>标签。标签不算作字符。


**说明**

- 字级别音素边界接口：语音合成服务在输出音频的同时，可输出每个汉字/英文单词在音频中的时间位置，即时间戳。该时间信息可用于驱动虚拟人口型、做视频配音字幕等。详情请参见 [语音合成时间戳功能介绍](https://help.aliyun.com/zh/isi/developer-reference/timestamp-feature#topic-2572251 "")。

- 文学场景相关发音人信息，请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-1#topic-2637955 "")。

- 如需使用Android或iOS SDK，请参见 [移动端接口说明](https://help.aliyun.com/zh/isi/developer-reference/overview-5#topic-1917954 "")。


## 就近地域智能接入

语音合成支持就近地域智能接入，域名为`nls-gateway.aliyuncs.com`。

推荐终端用户使用就近地域接入。根据调用接口时客户端所在的地理位置，系统会自动解析到最近的某个具体地域的服务器。例如在北京地域发起请求，系统会自动解析到北京地域的服务器，与指定域名`nls-gateway-cn-beijing.aliyuncs.com`的实现效果一致。

## 服务地址

| **访问类型** | **说明** | **URL** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **访问类型** | **说明** | **URL** |
| 外网访问（默认上海地域） | 所有服务器均可使用外网访问URL（SDK中默认设置了外网访问URL）。 | - 上海：`wss://nls-gateway-cn-shanghai.aliyuncs.com/ws/v1`<br>  <br>- 北京：`wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1`<br>  <br>- 深圳：`wss://nls-gateway-cn-shenzhen.aliyuncs.com/ws/v1` |
| ECS内网访问 | 使用阿里云上海、北京、深圳ECS（即ECS地域为华东2（上海）、华北2（北京）、华南1（深圳）），可使用内网访问URL。 ECS的经典网络不能访问AnyTunnel，即不能在内网访问语音服务；如果希望使用AnyTunnel，需要创建专有网络在其内部访问。<br>**说明**<br>- 使用内网访问方式，将不产生ECS实例的公网流量费用。<br>  <br>- 关于ECS的网络类型请参见 [网络类型](https://help.aliyun.com/zh/ecs/user-guide/network-types#concept-nfj-dz2-5db "")。 | - 上海：`ws://nls-gateway-cn-shanghai-internal.aliyuncs.com:80/ws/v1`<br>  <br>- 北京：`ws://nls-gateway-cn-beijing-internal.aliyuncs.com:80/ws/v1`<br>  <br>- 深圳：`ws://nls-gateway-cn-shenzhen-internal.aliyuncs.com:80/ws/v1` |

## 交互流程

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7850048471/CAEQQRiBgICP8cew9hgiIDhhNTAwMGVlZTljNjQxNjU4NzBmYTBkOTE4YjMxYzk04024928_20231008170233.737.svg)

**说明**

- 上图描述的是WebSocket的交互流程，关于RESTful API的交互流程图请参见 [RESTful API](https://help.aliyun.com/zh/isi/developer-reference/restful-api-3#topic-2572249 "")。

- 服务端的响应除了音频流之外，都会在返回信息的header包含本次识别任务的task\_id参数，是本次请求的唯一标识。

- 如果您希望实时播放服务端返回的音频流，请使用支持流式播放的音频播放器。支持流式播放的播放器包括：ffmpeg、pyaudio（Python）、AudioFormat（Java）和MediaSource（JavaScript）等。


1. 鉴权

客户端在与服务端建立WebSocket连接时，使用Token进行鉴权。关于Token获取请参见 [获取Token概述](https://help.aliyun.com/zh/isi/overview-of-obtaining-an-access-token#587dee8029x7r "")。

2. 开始合成

客户端发起语音合成请求，在请求消息中进行参数设置，各参数含义如下表所示。




| **参数** | **类型** | **是否必需** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必需** | **说明** |
| appkey | String | 是 | [管控台](https://nls-portal.console.aliyun.com/applist) 创建的项目Appkey。 |
| text | String | 是 | 待合成文本，文本内容必须采用UTF-8编码，长度不超过300个字符（英文字母之间需要添加空格）。<br>**说明**<br>调用某音色的多情感内容，需要在text中加上ssml-emotion标签，详情请参见 [<emotion>](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview#title-i3w-j10-5yw "")。<br>只有支持多情感的音色，才能使用<emotion>标签，否则会报错：Illegal ssml text。 |
| voice | String | 否 | 发音人，默认是`xiaoyun`。 |
| format | String | 否 | 音频编码格式，支持.pcm、.wav和.mp3格式。默认值：`pcm`。 |
| sample\_rate | Integer | 否 | 音频采样率，默认值：16000 Hz。 |
| volume | Integer | 否 | 音量，取值范围：0～100。默认值：50。 |
| speech\_rate | Integer | 否 | 语速，取值范围：-500～500，默认值：0。<br>\[-500, 0, 500\] 对应的语速倍速区间为 \[0.5, 1.0, 2.0\]。<br>   1. -500表示默认语速的0.5倍速。<br>      <br>   2. 0表示默认语速的1倍速。1倍速是指模型默认输出的合成语速，语速会依据每一个发音人略有不同，大概每秒钟4个字左右。<br>      <br>   3. 500表示默认语速的2倍速。<br>      <br>计算方法如下：<br>   1. 0.8倍速（1-1/0.8）/0.002 = -125<br>      <br>   2. 1.2倍速（1-1/1.2）/0.001 = 166<br>      <br>**说明**<br>1. 小于1倍速时，使用0.002系数。<br>      <br>2. 大于1倍速时，使用0.001系数。<br>      <br>实际算法结果取近似值。 |
| pitch\_rate | Integer | 否 | 语调，取值范围：-500～500，默认值：0。 |
| enable\_subtitle | Boolean | 否 | 开启字级别时间戳。更多使用方法，请参见 [语音合成时间戳功能介绍](https://help.aliyun.com/zh/isi/developer-reference/timestamp-feature "")。 |

3. 接收合成数据

服务端返回合成的语音二进制数据，SDK接收并处理二进制数据。

4. 结束合成

语音合成完毕，服务端发送合成完毕事件通知，举例如下。















```json
{
       "header": {
           "message_id": "05450bf69c53413f8d88aed1ee60****",
           "task_id": "640bc797bb684bd6960185651307****",
           "namespace": "SpeechSynthesizer",
           "name": "SynthesisCompleted",
           "status": 20000000,
           "status_message": "GATEWAY|SUCCESS|Success."
       }
}
```





**说明**





文档示例将合成的音频保存在文件中，如果您需要播放音频且对实时性要求较高，建议使用流式播放，即边接收语音数据边播放，减少延时。

5. 合成失败处理

当因为参数或其他原因导致合成任务失败时，会收到任务失败（TaskFailed）通知，举例如下。收到任务失败通知后，对应底层连接将断开。















```json
{
      "header":{
         "namespace":"Default",
         "name":"TaskFailed",
         "status":41020001,
         "message_id":"62c126f7d9b340deb82b5b7eaca0****",
         "task_id":"4552df26d1f547aab9a2c4a94678****",
         "status_text":"TTS:TtsClientError:[tts]Engine return error code: 418"
      }
}
```


## **音色列表**

| **名称** | **voice参数值** | **类型** | **适用场景** | **支持语言** | **支持采样率（Hz）** | **支持字/句级别时间戳** | **支持儿化音** | **声音品质** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **名称** | **voice参数值** | **类型** | **适用场景** | **支持语言** | **支持采样率（Hz）** | **支持字/句级别时间戳** | **支持儿化音** | **声音品质** |
| 阿斌 | abin | 广东普通话 | 对话数字人 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 否 | 否 | 标准版 |
| 知小白 | zhixiaobai | 普通话女声 | 对话数字人 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 否 | 是 | 标准版 |
| 知小夏 | zhixiaoxia | 普通话女声 | 对话数字人 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 否 | 是 | 标准版 |
| 知小妹 | zhixiaomei | 普通话女声 | 直播数字人 | 支持中文及中英文混合场景 | 8K/16K/24K | 是 | 是 | 标准版 |
| 知柜 | zhigui | 普通话女声 | 直播数字人 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 知硕 | zhishuo | 普通话男声 | 客服数字人 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 艾夏 | aixia | 普通话女声 | 客服数字人 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| Cally | cally | 美式英文女声 | 英语口语对话数字人 | 仅支持纯英文场景 | 8K/16K | 是 | 是 | 标准版 |
| 知锋\_多情感 | zhifeng\_emo | 多种情感男声 | 通用场景 | 中文及中英文混合场景 | 8K/16K/24K | 是 | 是 | 标准版 |
| 知冰\_多情感 | zhibing\_emo | 多种情感男声 | 通用场景 | 纯中文场景 | 8K/16K/24K | 是 | 是 | 标准版 |
| 知妙\_多情感 | zhimiao\_emo | 多种情感女声 | 中英场景 | 中文及英文场景 | 8K/16K | 是 | 是 | 标准版 |
| 知米\_多情感 | zhimi\_emo | 多种情感女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 知燕\_多情感 | zhiyan\_emo | 多种情感女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 知贝\_多情感 | zhibei\_emo | 多种情感童声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 知甜\_多情感 | zhitian\_emo | 多种情感女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 小云 | xiaoyun | 标准女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 否 | 否 | lite版 |
| 小刚 | xiaogang | 标准男声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 否 | 否 | lite版 |
| 若兮 | ruoxi | 温柔女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 思琪 | siqi | 温柔女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K/24K | 是 | 否 | 标准版 |
| 思佳 | sijia | 标准女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 思诚 | sicheng | 标准男声 | 通用场景 | 中文及中英文混合场景 | 8K/16K/24K | 是 | 否 | 标准版 |
| 艾琪 | aiqi | 温柔女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾佳 | aijia | 标准女声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾诚 | aicheng | 标准男声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾达 | aida | 标准男声 | 通用场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 宁儿 | ninger | 标准女声 | 通用场景 | 纯中文场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 瑞琳 | ruilin | 标准女声 | 通用场景 | 纯中文场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 思悦 | siyue | 温柔女声 | 客服场景 | 中文及中英文混合场景 | 8K/16K/24K | 是 | 否 | 标准版 |
| 艾雅 | aiya | 严厉女声 | 客服场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾美 | aimei | 甜美女声 | 客服场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾雨 | aiyu | 自然女声 | 客服场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾悦 | aiyue | 温柔女声 | 客服场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾婧 | aijing | 严厉女声 | 客服场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 小美 | xiaomei | 甜美女声 | 客服场景 | 中文及中英文混合场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 艾娜 | aina | 浙普女声 | 客服场景 | 纯中文场景 | 8K/16K | 是 | 否 | 标准版 |
| 伊娜 | yina | 浙普女声 | 客服场景 | 纯中文场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 思婧 | sijing | 严厉女声 | 客服场景 | 纯中文场景 | 8K/16K/24K | 是 | 否 | 标准版 |
| 思彤 | sitong | 儿童音 | 童声场景 | 纯中文场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 小北 | xiaobei | 萝莉女声 | 童声场景 | 纯中文场景 | 8K/16K/24K | 是 | 否 | 标准版 |
| 艾彤 | aitong | 儿童音 | 童声场景 | 纯中文场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾薇 | aiwei | 萝莉女声 | 童声场景 | 纯中文场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾宝 | aibao | 萝莉女声 | 童声场景 | 纯中文场景 | 8K/16K | 是 | 否 | 标准版 |
| Harry | harry | 英音男声 | 英文场景 | 英文场景 | 8K/16K | 否 | 否 | 标准版 |
| Abby | abby | 美音女声 | 英文场景 | 英文场景 | 8K/16K | 是 | 否 | 标准版 |
| Andy | andy | 美音男声 | 英文场景 | 英文场景 | 8K/16K | 是 | 否 | 标准版 |
| Eric | eric | 英音男声 | 英文场景 | 英文场景 | 8K/16K | 是 | 否 | 标准版 |
| Emily | emily | 英音女声 | 英文场景 | 英文场景 | 8K/16K | 是 | 否 | 标准版 |
| Luna | luna | 英音女声 | 英文场景 | 英文场景 | 8K/16K | 是 | 否 | 标准版 |
| Luca | luca | 英音男声 | 英文场景 | 英文场景 | 8K/16K | 是 | 否 | 标准版 |
| Wendy | wendy | 英音女声 | 英文场景 | 英文场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| William | william | 英音男声 | 英文场景 | 英文场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| Olivia | olivia | 英音女声 | 英文场景 | 英文场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 姗姗 | shanshan | 粤语女声 | 方言场景 | 标准粤文（简体）及粤英文混合场景 | 8K/16K/24K | 否 | 否 | 标准版 |
| 艾媛 | aiyuan | 知心姐姐 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾颖 | aiying | 软萌童声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾祥 | aixiang | 磁性男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾墨 | aimo | 情感男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾晔 | aiye | 青年男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾婷 | aiting | 电台女声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾凡 | aifan | 情感女声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| Lydia | lydia | 英中双语女声 | 英文场景 | 英文及英中文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 小玥 | chuangirl | 四川话女声 | 方言场景 | 中文及中英文混合场景 | 8K/16K | 否 | 否 | 标准版 |
| 艾硕 | aishuo | 自然男声 | 客服场景 | 中文及中英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 青青 | qingqing | 中国台湾话女声 | 方言场景 | 纯中文场景 | 8K/16K | 否 | 否 | 标准版 |
| 翠姐 | cuijie | 东北话女声 | 方言场景 | 纯中文场景 | 8K/16K | 是 | 是 | 标准版 |
| 小泽 | xiaoze | 湖南重口音男声 | 方言场景 | 纯中文场景 | 8K/16K | 否 | 否 | 标准版 |
| 艾楠 | ainan | 广告男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾浩 | aihao | 资讯男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾茗 | aiming | 诙谐男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾笑 | aixiao | 资讯女声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾厨 | aichu | 舌尖男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾倩 | aiqian | 资讯女声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 智香 | tomoka | 日语女声 | 多语种场景 | 纯日文场景 | 8K/16K | 是 | 否 | 标准版 |
| 智也 | tomoya | 日语男声 | 多语种场景 | 纯日文场景 | 8K/16K | 是 | 否 | 标准版 |
| Annie | annie | 美语女声 | 英文场景 | 纯英文场景 | 8K/16K | 是 | 否 | 标准版 |
| 艾树 | aishu | 资讯男声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 艾茹 | airu | 新闻女声 | 文学场景 | 中文及中英文混合场景 | 8K/16K | 是 | 是 | 精品版 |
| 佳佳 | jiajia | 粤语女声 | 方言场景 | 标准粤文（简体）及粤英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| Indah | indah | 印尼语女声 | 多语种场景 | 纯印尼语场景 | 8K/16K | 否 | 否 | 标准版 |
| 桃子 | taozi | 粤语女声 | 方言场景 | 支持标准粤文（简体）及粤英文混合场景 | 8K/16K | 是 | 否 | 标准版 |
| 柜姐 | guijie | 亲切女声 | 通用场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| Stella | stella | 知性女声 | 通用场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| Stanley | stanley | 沉稳男声 | 通用场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| Kenny | kenny | 沉稳男声 | 通用场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| Rosa | rosa | 自然女声 | 通用场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| Farah | farah | 马来语女声 | 多语种场景 | 仅支持纯马来语场景 | 8K/16K | 否 | 否 | 标准版 |
| 马树 | mashu | 儿童剧男声 | 通用场景 | 通用场景 | 8K/16K | 是 | 否 | 标准版 |
| 知琪 | zhiqi | 温柔女声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 知厨 | zhichu | 舌尖男声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 是 | 精品版 |
| 小仙 | xiaoxian | 亲切女声 | 直播场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 悦儿 | yuer | 儿童剧女声 | 通用场景 | 仅支持纯中文场景 | 8K/16K | 是 | 否 | 标准版 |
| 猫小美 | maoxiaomei | 活力女声 | 直播场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 知祥 | zhixiang | 磁性男声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 知佳 | zhijia | 标准女声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 知楠 | zhinan | 广告男声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 知倩 | zhiqian | 资讯女声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 知茹 | zhiru | 新闻女声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 知德 | zhide | 新闻男声 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 知飞 | zhifei | 激昂解说 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 否 | 精品版 |
| 艾飞 | aifei | 激昂解说 | 直播场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 亚群 | yaqun | 卖场广播 | 直播场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 巧薇 | qiaowei | 卖场广播 | 直播场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 大虎 | dahu | 东北话男声 | 方言场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| ava | ava | 美语女生 | 英文场景 | 仅支持纯英文场景 | 8K/16K | 是 | 否 | 标准版 |
| 知伦 | zhilun | 悬疑解说 | 超高清场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 否 | 精品版 |
| 艾伦 | ailun | 悬疑解说 | 直播场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 是 | 标准版 |
| 杰力豆 | jielidou | 治愈童声 | 童声场景 | 仅支持纯中文场景 | 8K/16K | 是 | 是 | 标准版 |
| 知薇 | zhiwei | 萝莉女声 | 超高清场景 | 仅支持纯中文场景 | 8K/16K/24K/48K | 是 | 否 | 精品版 |
| 老铁 | laotie | 东北老铁 | 直播场景 | 仅支持纯中文场景 | 8K/16K | 是 | 是 | 标准版 |
| 老妹 | laomei | 吆喝女声 | 直播场景 | 仅支持纯中文场景 | 8K/16K | 是 | 是 | 标准版 |
| 艾侃 | aikan | 天津话男声 | 方言场景 | 仅支持纯中文场景 | 8K/16K | 是 | 是 | 标准版 |
| Tala | tala | 菲律宾语女声 | 多语种场景 | 仅支持菲律宾语场景 | 8K/16K | 否 | 否 | 标准版 |
| 知甜 | zhitian | 甜美女声 | 通用场景 | 支持中文及中英文混合场景 | 8K/16K | 是 | 否 | 精品版 |
| 知青 | zhiqing | 中国台湾话女生 | 方言场景 | 仅支持纯中文场景 | 8K/16K | 是 | 否 | 精品版 |
| Tien | tien | 越南语女声 | 多语种场景 | 仅支持越南语场景 | 8K/16K | 否 | 否 | 标准版 |
| Becca | becca | 美语客服女声 | 美式英文 | 仅支持纯英语场景 | 8K/16K | 否 | 否 | 标准版 |
| Kyong | Kyong | 韩语女声 | 韩语场景 | 韩语 | 8K/16K | 否 | 否 | 标准版 |
| masha | masha | 俄语女声 | 俄语场景 | 俄语 | 8K/16K | 否 | 否 | 标准版 |
| camila | camila | 西班牙语女声 | 西班牙语场景 | 西班牙语 | 8k/16k | 否 | 否 | 标准版 |
| perla | perla | 意大利语女声 | 意大利语场景 | 意大利语 | 8k/16k | 否 | 否 | 标准版 |
| 知猫 | zhimao | 普通话女声 | 直播 | 中文 | 8k/16k | 是 | 否 | 标准版 |
| 知媛 | zhiyuan | 普通话女声 | 通用场景 | 中文 | 8k/16k | 是 | 否 | 标准版 |
| 知雅 | zhiya | 普通话女声 | 客服 | 中文 | 8k/16k | 是 | 否 | 标准版 |
| 知悦 | zhiyue | 普通话女声 | 通用场景 | 中文 | 8k/16k | 是 | 否 | 标准版 |
| 知达 | zhida | 普通话男声 | 通用场景 | 中文及中英文混合场景 | 8k/16k | 是 | 否 | 标准版 |
| 知莎 | zhistella | 普通话女声 | 通用场景 | 中文 | 8k/16k | 是 | 否 | 标准版 |
| Kelly | kelly | 香港粤语女声 | 方言场景 | 香港粤语 | 8k/16k | 是 | 否 | 标准版 |
| clara | clara | 法语女声 | 通用场景 | 法语 | 8k/16k | 否 | 否 | 标准版 |
| hanna | hanna | 德语女声 | 通用场景 | 德语 | 8k/16k | 否 | 否 | 标准版 |
| waan | waan | 泰语女声 | 通用场景 | 泰语 | 8k/16k | 否 | 否 | 标准版 |
| betty | betty | 美式英文女声 | 通用场景 | 美式英文 | 8k/16k | 是 | 否 | 标准版 |
| beth | beth | 美式英文女声 | 通用场景 | 美式英文 | 8k/16k | 是 | 否 | 标准版 |
| cindy | cindy | 美式英文女声 | 通用场景 | 美式英文 | 8k/16k | 是 | 否 | 标准版 |
| donna | donna | 美式英文女声 | 通用场景 | 美式英文 | 8k/16k | 是 | 否 | 标准版 |
| eva | eva | 美式英文女声 | 通用场景 | 美式英文 | 8k/16k | 是 | 否 | 标准版 |
| brian | brian | 美式英文男声 | 通用场景 | 美式英文 | 8k/16k | 是 | 否 | 标准版 |
| david | david | 美式英文男声 | 通用场景 | 美式英文 | 8k/16k/24k | 是 | 否 | 标准版 |
| abby\_ecmix | abby\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| annie\_ecmix | annie\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| andy\_ecmix | andy\_ecmix | 美式英文男声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| ava\_ecmix | ava\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| betty\_ecmix | betty\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| beth\_ecmix | beth\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| brian\_ecmix | brian\_ecmix | 美式英文男声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| cindy\_ecmix | cindy\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| cally\_ecmix | cally\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| donna\_ecmix | donna\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| david\_ecmix | david\_ecmix | 美式英文男声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |
| eva\_ecmix | eva\_ecmix | 美式英文女声 | 通用场景 | 英文及英中文混合场景 | 8k/16k/24k | 是 | 否 | 标准版 |

## 多情感声音支持说明

只有多情感发音人模型才可以支持多情感选择。多情感声音支持的情感如下表所示，每个音色支持的情感分类不完全相同，主要包括：neutral（中性）、happy（开心）、angry（生气）、sad（悲伤）、fear（害怕）、hate（憎恨）、surprise（惊讶）、arousal（激动）、serious（严肃）、disgust（厌恶）、jealousy（嫉妒）、embarrassed（尴尬）、frustrated（沮丧）、affectionate（深情）、gentle（温柔）、newscast（播报）、customer-service（客服）、story（小说）、living（直播）。

| **音色名** | **voice参数值** | **情感分类（emotion category）** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **音色名** | **voice参数值** | **情感分类（emotion category）** |
| 知锋\_多情感 | zhifeng\_emo | angry，fear，happy，neutral，sad，surprise |
| 知冰\_多情感 | zhibing\_emo | angry，fear，happy，neutral，sad，surprise |
| 知妙\_多情感 | zhimiao\_emo | serious，sad，disgust，jealousy，embarrassed，happy，fear，surprise，neutral，frustrated，affectionate，gentle，angry，newscast，customer-service，story，living |
| 知米\_多情感 | zhimi\_emo | angry，fear，happy，hate，neutral，sad，surprise |
| 知燕\_多情感 | zhiyan\_emo | neutral，happy，angry，sad，fear，hate，surprise，arousal |
| 知贝\_多情感 | zhibei\_emo | neutral，happy，angry，sad，fear，hate，surprise |
| 知甜\_多情感 | zhitian\_emo | neutral，happy，angry，sad，fear，hate，surprise |

## 服务状态码

服务的每一次响应都包含status字段，即服务状态码，各状态码含义如下。

### **通用错误码**

| **状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

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

| **状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 40000001 | Gateway:ACCESS\_DENIED:No privilege to this voice! | 设置了错误的发音人名称。 | 请参考官网文档，设置正确的发音人。 |
| 40000004 | Gateway:IDLE\_TIMEOUT:Websocket session is idle for too long time,the last directive is 'StartSynthesis'! | 请求建立链接后，长时间没有发送任何数据，超过10s后服务端会返回此错误信息。 | 请求处理完成后请及时关闭链接，此外，当服务端瞬时压力过大不能及时返回数据时也可能出现此错误，此时可以重试恢复。 |
| 40010003 | Gateway:DIRECTIVE\_INVALID:No text specified! | 没有设置有效的待合成文本文字。 | 请参考官网文档示例代码设置待合成的文本。 |
| 41020001 | 语音合成调用客户端错误 | 可能有多个错误消息，需根据对应的错误消息调整。 | - 如果提示`Engine return error code: 424.`表示传递的背景音乐或拼接录音不符合格式，请参考文档说明设置正确的背景音。<br>  <br>- 如果提示`Engine return error code:418`表示传递了不支持的发音人名称。<br>  <br>- 如果提示`Engine return error code: 413`表示使用的SSML格式错误。<br>  <br>- 如果提示`Request json illegal,failed to parse request.`表示传递的JSON格式非法。<br>  <br>- 如果提示`SSML text length should be less than 300.`表示传递的合成文本过长，建议使用长文本语音合成接口。 |
| 51020001 | TTS:TtsServerError | 受机器负载或网络等因素导致的异常，通常为偶发出现。 | 一般重试调用即可恢复。 |