### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[服务支持](https://help.aliyun.com/zh/isi/support/)[常见问题](https://help.aliyun.com/zh/isi/support/faq/)语音识别FAQ

# 语音识别FAQ

更新时间：2025-07-29 01:48:10

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：产品公共FAQ](https://help.aliyun.com/zh/isi/support/common-faq-about-services)[下一篇：语音识别输入格式FAQ](https://help.aliyun.com/zh/isi/support/faq-about-input-formats-for-speech-recognition)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能类

实时转写说话有停顿，但是语音识别不断句怎么办？

语音识别能自动断开多句话吗？

语音识别服务支持离线功能吗？

语音识别支持哪些模型？

语音识别是否可以混合识别极少量英文单词和字母？

开启ITN（逆文本规整）后，中文数字混合时为什么并不是全部转为阿拉伯数字？

录音文件识别的enable\_sample\_rate\_adaptive和极速版本里的sample\_rate，这两个接口是一样的吗？

录音转文本能区分坐席和客户吗？

智能语音交互的一句话识别，标点符号是根据什么来判断逗号和句号的？

离线文件转写如何区分左右声道？

语音识别可以支持多个词表吗？

设置录音文件识别服务的版本，"4.0"和"2.0"两个版本有什么区别？

在电话端支持哪些国家的语音识别？

在语音识别的服务中，有没有请求参数是音频文件地址，返回参数是转写文本？

实时语音转写能和录音文件识别一样加入音轨ID吗？

录音文件识别可以生成SRT字幕文件吗？

语音识别服务支持哪些编码格式的音频？

语音识别服务支持哪些采样率？

怎么查看音频文件的采样率？

语音识别服务支持的方言模型和语种都有哪些？

语音识别能否自动断开多句话？

实时识别和录音文件转写分别支持哪些语音格式？

性能类

语音识别的识别准确率怎么计算？

语音识别模型的字准率能达到多少？

录音文件识别极速版延迟是多少？

8k模型可以识别16k的音频吗？

录音文件识别极速版调用频率有限制吗？

粤语的识别准确率是多少？

15秒左右的录音文件识别大概需要多久能转换成文本呢？

语音转文本有没有优先级？比如现在正在转写任务，突然有紧急的转写任务，能调整处理优先级吗？

针对两个用户打电话场景，哪个模型效果比较好？

服务请求时长限制？

“流式”模式和“非流式”模式识别的区别？

什么是ASR尾点延迟？

实时语音识别慢怎么办？

效果类

对于识别不准的词该如何进行优化？

单字识别不出来是什么原因？

热词效果如果不佳是否可以自主调节权重？

录音文件识别时间戳不准，如何解决？

语音识别太灵敏、无效声音（噪音等）被识别出了文字怎么办？

远场识别为什么会经常丢字？如何提高远场识别效果？

ASR识别很离谱，不准确怎么办？

有些词汇总是识别不准怎么办？

如何提高标点断句的效果？

实时场景中，已经开启了标点断句，为什么效果还是不理想？

录音文件识别存在一次请求后返回两次相同的结果的情况吗？

实时语音识别遇到识别慢、超时问题，如何排查？

为什么语音识别准确率很低，有时只识别出几个字？

确认调用方式和采样率都没问题，识别还是不准确怎么办？

SDK使用类

一句话识别录入的demo是使用Websocket进行识别展示的吗？

实时语音识别服务有Python SDK吗？

语音识别的返回结果JSON中endtime=-1是什么意思？

移动端鸿蒙Next SDK中如何修改识别语音采样率为8000HZ或者16000HZ?

计费类

录音文件识别极速版不支持试用吗？

本文汇总了您在使用语音识别服务时的常见问题。

语音识别类常见问题主要分为以下几类：

- 功能类

  - [实时转写说话有停顿，但是语音识别不断句怎么办？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-6kv-vfh-axp "")

  - [语音识别能自动断开多句话吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-i2c-90n-9li "")

  - [语音识别服务支持离线功能吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-44v-bn1-3zl "")

  - [语音识别支持哪些模型？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-cq2-8wo-3zp "")

  - [语音识别是否可以混合识别极少量英文单词和字母？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-r9o-rqw-x1y "")

  - [开启ITN（逆文本规整）后，中文数字混合时为什么并不是全部转为阿拉伯数字？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-8ds-7z9-o3m "")

  - [录音文件识别的enable\_sample\_rate\_adaptive和极速版本里的sample\_rate，这两个接口是一样的吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-pyu-8gm-dg2 "")

  - [录音转文本能区分坐席和客户吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-ug4-u38-vzz "")

  - [智能语音交互的一句话识别，标点符号是根据什么来判断逗号和句号的？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-7il-slx-o4q "")

  - [离线文件转写如何区分左右声道？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-xhy-iil-6fc "")

  - [语音识别可以支持多个词表吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-uce-9l7-7pb "")

  - [设置录音文件识别服务的版本，"4.0"和"2.0"两个版本有什么区别？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-l8m-pjv-505 "")

  - [在电话端支持哪些国家的语音识别？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-o6n-ch9-jtn "")

  - [在语音识别的服务中，有没有请求参数是音频文件地址，返回参数是转写文本？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-1yp-oa5-e6b "")

  - [实时语音转写能和录音文件识别一样加入音轨ID吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-47a-p0a-1tz "")

  - [录音文件识别可以生成SRT字幕文件吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-hk5-hgy-w83 "")

  - [语音识别服务支持哪些编码格式的音频？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-lah-mz2-45y "")

  - [语音识别服务支持哪些采样率？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-mkp-gvr-5h2 "")

  - [怎么查看音频文件的采样率？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-4n8-hsc-q5a "")

  - [语音识别服务支持的方言模型和语种都有哪些？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-ozo-fn1-tjc "")

  - [语音识别能否自动断开多句话？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-m9i-zpn-psb "")

  - [实时识别和录音文件转写分别支持哪些语音格式？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-6zq-bg5-ro9 "")
- 性能类

  - [语音识别的识别准确率怎么计算？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-rd9-bfw-70y "")

  - [语音识别模型的字准率能达到多少？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-1nl-m1e-61t "")

  - [录音文件识别极速版延迟是多少？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-fv4-6f9-aqs "")

  - [8k模型可以识别16k的音频吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-rv7-bet-e7d "")

  - [录音文件识别极速版调用频率有限制吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-44i-swc-8o7 "")

  - [粤语的识别准确率是多少？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-t62-2ij-p89 "")

  - [15秒左右的录音文件识别大概需要多久能转换成文本呢？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-1k0-7h0-nts "")

  - [语音转文本有没有优先级？比如现在正在转写任务，突然有紧急的转写任务，能调整处理优先级吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-cq7-q0h-c0j "")

  - [针对两个用户打电话场景，哪个模型效果比较好？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-jmh-lwy-mfi "")

  - [服务请求时长限制？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-jz5-qil-fvn "")

  - [“流式”模式和“非流式”模式识别的区别？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-sxv-qm8-aaz "")

  - [什么是ASR尾点延迟？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-mvt-ek2-ne2 "")

  - [实时语音识别慢怎么办？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#1dd0b1c992cgy "")
- 效果类

  - [对于识别不准的词该如何进行优化？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-eft-te4-6yk "")

  - [单字识别不出来是什么原因？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-zt1-r1h-9xm "")

  - [热词效果如果不佳是否可以自主调节权重？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-2gi-46b-qbr "")

  - [录音文件识别时间戳不准，如何解决？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-54e-evb-1id "")

  - [语音识别太灵敏、无效声音（噪音等）被识别出了文字怎么办？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-3br-y1r-3bp "")

  - [如何提高标点断句的效果？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-un5-g9q-n3b "")

  - [实时场景中，已经开启了标点断句，为什么效果还是不理想？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-65k-1eq-90w "")

  - [录音文件识别存在一次请求后返回两次相同的结果的情况吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-e0s-08d-b3i "")

  - [实时语音识别遇到识别慢、超时问题，如何排查？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-z0h-h2d-xcb "")

  - [为什么语音识别准确率很低，有时只识别出几个字？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-efw-9lt-a7q "")

  - [确认调用方式和采样率都没问题，识别还是不准确怎么办？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-w3u-ati-f8p "")
- SDK使用类

  - [一句话识别录入的demo是使用Websocket进行识别展示的吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-e9h-tl4-3tf "")

  - [实时语音识别服务有Python SDK吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-qi4-kqx-c2v "")

  - [语音识别的返回结果JSON中endtime=-1是什么意思？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-4xd-m0o-tzq "")

  - [移动端鸿蒙Next SDK中如何修改识别语音采样率为8000HZ或者16000HZ?](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#9ed21fdd886x0 "")
- 计费类

  - [录音文件识别极速版不支持试用吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-recognition#sectiondiv-s7u-dqo-5vo "")

## 功能类

### 实时转写说话有停顿，但是语音识别不断句怎么办？

1. 如果是vad断句情况下，实时转写的vad断句依赖对音频中静音数据的判断，如果上游不发送静音音频，服务端则无法识别用户说话是否有停顿。如果确认是上游没有发送静音音频，则系统通过对实时转写服务的时间戳和实际音频的时间戳对比。如果发现服务端的判断音频时长比实际音频时长短，说明静音时服务端没有收到用户发的静音数据。

2. 在开启语义断句情况下，有可能是后处理模型的效果问题。


解决方案：在用户停顿时持续地向服务端发送静音数据。

### 语音识别能自动断开多句话吗？

实时语音识别服务可以断开多句话。一句话识别服务的每个请求只对应一句话，无法断开。

### 语音识别服务支持离线功能吗？

目前不支持本地离线的语音识别，必须把音频数据发送到服务端做识别。

### 语音识别支持哪些模型？

可以在 [智能语音交互控制台](https://nls-portal.console.aliyun.com/overview) 中项目功能配置里查看具体的模型种类，目前有8k和16k两种采样率的模型，每个采样率下面又有多个领域模型，可以按需选择。

### 语音识别是否可以混合识别极少量英文单词和字母？

可以的，中文普通话模型支持对中英文混杂的音频进行识别。

### 开启ITN（逆文本规整）后，中文数字混合时为什么并不是全部转为阿拉伯数字？

是否要转成阿拉伯数字，系统是用模型来判断的，并不是所有数字都需要转成阿拉伯数字，模型的判断主要准则是一般书面文本中常用的形态。

### 录音文件识别的enable\_sample\_rate\_adaptive和极速版本里的sample\_rate，这两个接口是一样的吗？

不是。极速版的sample\_rate就是采样率，enable\_sample\_rate\_adaptive是个开关，极速版默认采样率16k，不需要这个开关。

### 录音转文本能区分坐席和客户吗？

语音识别引擎只能区分出说话的不同角色，角色对应的身份引擎是无法识别的，需要用户从业务的角度自行判断。建议您在存储录音时按照角色分类存储。

### 智能语音交互的一句话识别，标点符号是根据什么来判断逗号和句号的？

结合音频的声学特征和对识别结果文本做语音分析后做标点处理。

### 离线文件转写如何区分左右声道？

语音识别引擎无法区分左右声道，当多声道音频送入语音识别服务进行识别时，返回结果会用channel\_id字段来标记多个音轨。如果采集顺序固定，可以根据channel\_id区分对应声道。具体可参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-2#topic-1917932 "")。

### 语音识别可以支持多个词表吗？

一次可使用一个词表，每次只能传一个vocabulary\_id，如果觉得不够可以使用定制模型。具体可参见 [使用POP API创建业务专属热词](https://help.aliyun.com/zh/isi/developer-reference/call-the-pop-api-to-manage-business-specific-hotwords#topic-1917965 "")。

### 设置录音文件识别服务的版本，"4.0"和"2.0"两个版本有什么区别？

由于历史原因，早期发布的录音文件识别服务（默认为2.0版本）的回调方式和轮询方式的识别结果在JSON字符串的风格和字段上均有不同。录音文件识别服务在4.0版本对回调方式做了优化，使得回调方式的识别结果与轮询方式的识别结果保持一致，均为驼峰风格的JSON格式字符串。具体可参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-2#topic-1917932 "")。

### 在电话端支持哪些国家的语音识别？

电话8k语音目前支持的外语语种为英语，非电话16k语音支持更多外语语种。语种模型支持列表详见 [功能特性](https://help.aliyun.com/zh/isi/product-overview/features#topic-2047420 "")。

### 在语音识别的服务中，有没有请求参数是音频文件地址，返回参数是转写文本？

可使用录音文件识别功能，具体请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-2#topic-1917932 "")。

### 实时语音转写能和录音文件识别一样加入音轨ID吗？

不能，音轨ID是录音文件专用的。实时转写只有单通道语音，不需要channel区分。

### 录音文件识别可以生成SRT字幕文件吗？

目前没有。需要根据返回结果中的时间信息自己进行拼接。

### 语音识别服务支持哪些编码格式的音频？

每种服务支持的格式不尽相同，请参见各服务中的说明。您可以使用常见音频编辑软件如Audacity，查看音频文件的编码格式。

### 语音识别服务支持哪些采样率？

一般支持8000 Hz、16000 Hz的采样率。 电话客服场景通常是8000采样率，如果是手机App、PC端工具、网页H5类场景，通常是16000 Hz采样率（可能会有32、44k采样率，但开发时需要调用方将采样率调整为16k）。其他采样率的录音数据需要预先自行转码。

录音文件转写可以支持其他采样率，例如32k、44k等等。

### 怎么查看音频文件的采样率？

可以使用常见音频编辑软件如Audacity查看音频文件的采样率，也可以使用开源命令行工具 [FFmpeg](https://www.ffmpeg.org/) 查看。

### 语音识别服务支持的方言模型和语种都有哪些？

语音识别目前支持的语种和方言模型如下：

- 语种






|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 语言 | 模型名称 | 采样率 | 标点 | ITN | 顺滑 | 语义断句 | 声音和文本对齐 |
| 英语 | 通用-英文，教育直播-英文，教育内容分析-英文 | 16k | 支持 | 支持 | 支持 | 不支持 | 支持 |
| 电话客服（通用） | 8k | 支持 | 支持 | 支持 | 不支持 | 不支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 日语 | 通用-日语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 支持 |
| 西班牙语 | 通用-西班牙语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 通用-西班牙客服通用 | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 阿拉伯语 | 通用-阿拉伯语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 哈萨克语 | 通用-哈萨克语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 韩语 | 通用-韩语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 泰语 | 通用-泰语 | 16k | 不支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 通用-泰语客服通用 | 8k | 不支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 印尼语 | 通用-印尼语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 电话客服（通用） | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 俄语 | 通用-俄语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 越南语 | 通用-越南语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 通用-越南语客服通用 | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 法语 | 通用-法语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 德语 | 通用-德语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 意大利语 | 通用-意大利语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 印地语 | 通用-印地语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 马来语 | 通用-马来语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 通用-马来语客服通用 | 8k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 菲律宾语 | 通用-菲律宾语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 电话客服（通用） | 8k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 泰米尔语 | 通用-泰米尔语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 葡萄牙语 | 通用-葡萄牙语 | 16k | 支持 | 支持 | 不支持 | 不支持 | 不支持 |
| 土耳其语 | 通用-土耳其语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 波兰语 | 通用-波兰语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 乌克兰语 | 通用-乌克兰语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 罗马尼亚语 | 通用-罗马尼亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 荷兰语 | 通用-荷兰语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 希腊语 | 通用-希腊语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 匈牙利语 | 通用-匈牙利语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 爪哇语 | 通用-爪哇语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 孟加拉语 | 通用-孟加拉语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 缅甸语 | 通用-缅甸语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 老挝语 | 通用-老挝语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 斯瓦希里语 | 通用-斯瓦希里语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 阿塞拜疆语 | 通用-阿塞拜疆语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 波斯语 | 通用-波斯语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 僧伽罗语 | 通用-僧伽罗语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 加泰罗尼亚语 | 通用-加泰罗尼亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 高棉语 | 通用-高棉语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 希伯来语 | 通用-希伯来语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 克罗地亚语 | 通用-克罗地亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 豪萨语 | 通用-豪萨语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 马拉地语 | 通用-马拉地语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 泰卢固语 | 通用-泰卢固语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 旁遮普语 | 通用-旁遮普语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 瑞典语 | 通用-瑞典语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 保加利亚语 | 通用-保加利亚语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 丹麦语 | 通用-丹麦语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 挪威语 | 通用-挪威语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 坎纳达语 | 通用-坎纳达语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 马拉雅拉姆语 | 通用-马拉雅拉姆语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 捷克语 | 通用-捷克语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 乌尔都语 | 通用-乌尔都语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 尼泊尔语 | 通用-尼泊尔语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 蒙古语（外蒙） | 通用-蒙古语（外蒙） | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 乌兹别克语 | 通用-乌兹别克语 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |

- 方言






|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 语言 | 模型名称 | 采样率 | 标点 | ITN | 顺滑 | 语义断句 | 声音和文本对齐 |
| 粤语 | 通用-粤语 | 16k | 支持 | 支持 | 支持 | 不支持 | 支持 |
| 电话客服（通用） | 8k | 支持 | 支持 | 支持 | 不支持 | 支持 |
| 粤中自由说 | 8k | 支持 | 支持 | 支持 | 不支持 | 不支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 粤语（繁体） | 通用-粤语（繁体） | 8k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 通用-粤语（繁体） | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 四川话 | 通用-四川话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 电话客服（通用） | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 湖北话 | 通用-湖北话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 通用-湖北话 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 上海话 | 通用-上海话 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
| 湖南话 | 通用-湖南话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 河南话 | 通用-河南话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 通用-河南话 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 浙江话 | 通用-浙江话 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
| 东北话 | 通用-东北话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 山东话 | 通用-山东话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 天津话 | 通用-天津话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 陕西话 | 通用-陕西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 山西话 | 通用-山西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 贵州话 | 通用-贵州话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 云南话 | 通用-云南话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 甘肃话 | 通用-甘肃话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 维吾尔语 | 通用-维吾尔语 | 16k | 不支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 通用-维吾尔语 | 8k | 不支持 | 不支持 | 不支持 | 不支持 | 不支持 |
| 苏州话 | 通用-苏州话 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
| 闽南语 | 通用-闽南语 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
| 江西话 | 通用-江西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 宁夏话 | 通用-宁夏话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 广西话 | 通用-广西话 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 通用-广西话 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 中文普通话 | 识音石 V1 - 端到端模型，教育内容分析，医疗内容分析，新闻媒体内容分析，娱乐视频内容分析，音视频离线转写（升级版），新零售领域识别模型，出行领域识别模型，汽车领域 | 16k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 中英自由说 | 16k | 支持 | 支持 | 支持 | 支持 | 不支持 |
| 识音石 V1 - 端到端模型 | 8k | 支持 | 支持 | 支持 | 支持 | 支持 |
| 东南亚多语言 | 16k | 支持 | 不支持 | 不支持 | 不支持 | 不支持 |


最新的模型支持情况可以登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/applist)，在项目配置中查看。![图片 1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6924473261/p283621.png)![图片2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6924473261/p283622.png)![图片 3](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6924473261/p283624.png)

### 语音识别能否自动断开多句话？

实时语音识别服务可以断开多句话；一句话识别服务的每个请求只对应一句话，无法断开。

### 实时识别和录音文件转写分别支持哪些语音格式？

![p283628](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6006367261/p300212.png)

## 性能类

### 语音识别的识别准确率怎么计算？

行业通常使用错误率来统计识别效果，中文常用CER（字错误率），英文常用WER（词错误率）。计算方式：（插入错误字数ins+删除错误字数del+替换错误字数sub）/总字数。以下图为例：![错误率](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4483161361/p324651.png)这批数据的准确率=（14365-74-385-1706）/14365=84.93%。快速计算方式为：100-15.07=84.93。

### 语音识别模型的字准率能达到多少？

关于达摩院智能语音交互语音识别准确度的数字，我们通过了CNAS（国家软件测试中心）的评测，国家软件中心对语音识别算法准确度测试中，在60分贝以下的降噪环境中，用普通话在距离耳麦1厘米的位置，以240字/分钟的匀速朗读样本量1207字的测试下，我们经过5轮测试的结果，识别准确率均大于98%。该准确度经过国家软件测试中心的标准认证。

而在现实的使用过程当中，可能会受到耳麦质量、背景杂音、口音差异等原因导致准确度有一定的偏差，对于数据格式为8k、16bit、双通道分轨（用户或客服双轨）的pcm或者wav格式，信噪比在20dB以上的语音，绝大部分商用场景下我们能保障85%的准确度，确保您有效使用。

### 录音文件识别极速版延迟是多少？

录音文件识别极速版服务承诺10秒内完成30分钟的音频识别，指的是从收到全部音频到完成识别的时间，音频上传的速度和客户端带宽等因素相关，时长可能会有不同。在服务端返回的识别结果中包含latency字段，记录了服务端处理时长。

### 8k模型可以识别16k的音频吗？

不可以。8K模型和16K模型只支持识别对应采样率的音频。

### 录音文件识别极速版调用频率有限制吗？

没有。但对并发有限制，并发数在控制台上查看。

### 粤语的识别准确率是多少？

粤语8k、16k识别准确率在80~95%之间，实际结果受语料数据与发音标准程度影响。使用不同服务准确率会有略微区别（相对5%），准确率排名整体为：录音文件识别＞一句话识别＞实时语音识别。

### 15秒左右的录音文件识别大概需要多久能转换成文本呢？

录音文件识别是离线API。对于免费用户的识别任务在24小时内完成并返回识别文本；付费用户的识别任务在3小时内完成并返回识别文本。60秒以内的短音频建议客户使用一句话识别，时效更好。

### 语音转文本有没有优先级？比如现在正在转写任务，突然有紧急的转写任务，能调整处理优先级吗？

暂不支持这个操作，文件转写目前的时效性还是比较快的。

### 针对两个用户打电话场景，哪个模型效果比较好？

目前建议都使用新一代端到端“识音石”识别模型，综合效果性能比较好。

### 服务请求时长限制？

- 一句话识别支持60秒以内的实时语音。

- 实时语音识别不限制时长。


### “流式”模式和“非流式”模式识别的区别？

“非流式”模式也称为普通模式，普通模式下，服务判断用户整句话说完后才返回一次识别结果；而“流式”模式下用户一边说话一边返回识别结果，在句子结束的识别结果前会有很多中间结果。

### 什么是ASR尾点延迟？

尾点延迟的定义是调用端发送音频结束到完成识别的时间。

目前语音实时识别，如一句话识别、实时转写接口的延迟在300毫秒左右，视模型、音频差异而略有不同。

一句话识别RESTful接口因为批量接收音频，识别时长和音频时长相关。不考虑网络开销，一句话识别RESTful接口处理时长和音频时长近似线性关系，简单计算可以认为：接口处理时长=音频时长\*0.2。例如，1分钟音频处理时长约为12秒。实际线上性能会随模型的不同和服务器负载略有差异。

### 实时语音识别慢怎么办？

请检查是否将参数`enable_semantic_sentence_detection`设为了`true`。

上述参数设为`true`会开启语义断句，虽可提升识别准确率，但会小幅增加延迟。如对时延要求较高，可将其设为`false`。

## 效果类

### 对于识别不准的词该如何进行优化？

1. 首先考虑无标注优化：

1. 使用业务相关语料进行定制语言模型优化。业务语料包括业务关键词、业务相关的句子和篇章等。训练语料中要尽可能的对词进行泛化。（比如把“银税e贷是什么”、“如何办理银税e贷”等等相关话术加入到训练语料中）

2. 针对依然识别不好的业务关键词，再以复制多行或者提高模型权重的方式进行定制语言模型加强。

3. 个别解决不好的业务关键词，使用泛热词进行优化。
2. 其次考虑有标注优化：

1. 如果主要是因为口音等问题导致的整体识别效果不好，并且无标注优化方式无法解决到满意程度，可以开始声学模型优化。

2. 声学模型优化需要标注数据，标注本身也可以加入业务相关语料中进行语言模型优化。

### 单字识别不出来是什么原因？

因为单字发音单元短，且没有上下文语义，所以单字的识别是难点，添加热词效果不一定好，建议采用定制化模型优化。

### 热词效果如果不佳是否可以自主调节权重？

人名和地名类热词不支持设置权重，业务专属热词支持权重。目前在控制台上创建业务专属热词时不支持设置权重，如果需要调整权重您可以通过API进行维护。

### 录音文件识别时间戳不准，如何解决？

可通过设置时间戳校准功能参数 **enable\_timestamp\_alignment** 为 **true** 来调准。详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/api-reference-2#topic-1917932 "")。

### 语音识别太灵敏、无效声音（噪音等）被识别出了文字怎么办？

可以通过设定参数`speech_noise_threshold`的值来修改VAD噪声阈值。

`speech_noise_threshold`参数区间是\[-1，1\]，取值越小越灵敏，可能会有更多噪音被当成语音被误识别；取值越大，可能更多语音段会被当成噪音而没有被识别。例如设为0.6，如果仍觉得太灵敏，可以继续尝试设置为0.7。如果发现有丢字、漏识别，需要将该值调小，例如0.5、0.2甚至是-0.2等。

代码示例：

- Java















```java
transcriber.addCustomedParam("speech_noise_threshold", -0.1);
```

- C++















```c
request->setPayloadParam("speech_noise_threshold",-0.1);
```


### 远场识别为什么会经常丢字？如何提高远场识别效果？

这是因为远、近场的VAD阈值不一样，建议调节参数`speech_noise_threshold`。`speech_noise_threshold`参数区间是\[-1，1\]，取值越小越灵敏，可能会有更多噪音被当成语音被误识别；取值越大，可能更多语音段会被当成噪音而没有被识别。例如设为-0.2，如果丢字现象仍然比较严重，可以继续调小至如-0.3、-0.4；如果发现较多噪声被误识别了，也可以适当调大，例如-0.1、0等。

### ASR识别很离谱，不准确怎么办？

一般来说，ASR模型识别率均有一定的保证。如果在所有情况下语音识别都不准确，或者识别率很低，往往需要整体考虑是否有什么地方配置错误，例如实际语音的采样率（在线识别场景ASR只支持8k 16bit或者16k 16bit)、调用时设置的采样率参数（8000或者16000）、ASR服务端模型（8k或者16k），这三者需要保持一致。

**重要**

如果是公共云ASR调用，需要确认阿里云控制台上该appkey所选择的模型采样率；如果是专有云ASR环境，则需要确认service/resource/asr/default/models/readme.txt 文件中所定义的采样率。

### 有些词汇总是识别不准怎么办？

在某些情况下，确实存在某些词汇识别不准的情况，如特定名词。针对此现象（下面以词汇“银税e贷”为例），我们建议有：

- 通过自学习平台的定制语言模型训练优化，例如把“银税e贷是什么”、“如何办理银税e贷”等等相关话术加入到文本语料中进行训练。

- 通过自学习平台的热词优化，例如把“银税e贷”作为热词进行训练，设置相应权重。

- 专有云可通过ASR的白名单优化，例如“银税e贷”更容易为误识别为“银税一袋”，则可以在service/resource/asr/default/models/nn\_itn/correct.list中按预定格式进行设置，第一列是误识别的文本，第二列是正确文本，注意该操作要求重启ASR生效。


### 如何提高标点断句的效果？

默认VAD断句，可以添加参数`enable_semantic_sentence_detection`使用语义断句。如果是实时识别，请确认中间结果（参数`enable_intermediate_result`）也是开启的。

### 实时场景中，已经开启了标点断句，为什么效果还是不理想？

可以确认下是否开启中间结果，实时场景的语义断句需要配合中间结果使用。

### 录音文件识别存在一次请求后返回两次相同的结果的情况吗？

此类现象大部分是由于用户提交的语音文件是双声道，且两个声道语音内容相同造成的。如果是这种情况，属正常现象，设置参数first\_channel\_only为true，只识别首个声道即可解决。

### 实时语音识别遇到识别慢、超时问题，如何排查？

排查方式：

- 运行阿里云提供的示例，和您的服务对比运行状态，记录并提供日志信息。

- 记录请求对应的taskid，方便排查问题。

- 客户端使用TCPDump（Linux）/Wireshark（Windows）等抓包工具，确定网络状况。


### 为什么语音识别准确率很低，有时只识别出几个字？

请检查音频数据的采样率与管控台应用的模型是否一致，以及音频是否是单通道录音。

**重要**

只有录音文件识别支持双通道的录音。

### 确认调用方式和采样率都没问题，识别还是不准确怎么办？

您可以通过如下两种方式提高识别准确率：

- 使用自定义热词功能，快速、实时提高准确率，详情请参见 [热词概述](https://help.aliyun.com/zh/isi/developer-reference/overview-1#topic-2572262 "")。

- 开通自学习模型训练，通过模型定制的方式提高大量文本的识别率，详情请参见 [语言模型定制概述](https://help.aliyun.com/zh/isi/developer-reference/overview-2#topic-2572270 "")。


## SDK使用类

### 一句话识别录入的demo是使用Websocket进行识别展示的吗？

是Websocket。SDK就是采用的Websocket协议，RESTful API接口是HTTP协议。SDK接口详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-9#topic-1964088 "")。

### 实时语音识别服务有Python SDK吗？

暂不支持。

### 语音识别的返回结果JSON中endtime=-1是什么意思？

表示当前句子未结束。当语音识别模式为“流式”时，才会存在中间结果。

### 移动端鸿蒙Next SDK中 **如何修改识别语音采样率为8000HZ或者16000HZ?**

demo代码中，使用的是16000Hz采样率录音、识别。 如果想要修改为8000Hz录音、识别，则需要同时修改录音接口采样率参数和SDK配置采样率参数两个地方，以16000Hz修改为8000Hz为例：

1. 修改`AudioCapture.ets`文件中的`samplingRate:audio.AudioSamplingRate.SAMPLE_RATE_16000`为`samplingRate:audio.AudioSamplingRate.SAMPLE_RATE_8000`。

2. 修改对应识别demo文件（.ets文件）中的初始化参数，`genInitParams()`中增加对 **sample\_rate** 的设置，即 `object.set("sample_rate", "8000")`，其他地方无需修改。


## 计费类

### 录音文件识别极速版不支持试用吗？

对，录音文件极速版暂不支持试用，需要付费才可以。