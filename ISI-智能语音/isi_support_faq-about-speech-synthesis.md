### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[服务支持](https://help.aliyun.com/zh/isi/support/)[常见问题](https://help.aliyun.com/zh/isi/support/faq/)语音合成FAQ

# 语音合成FAQ

更新时间：2022-09-06 05:48:29

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：语音识别输入格式FAQ](https://help.aliyun.com/zh/isi/support/faq-about-input-formats-for-speech-recognition)[下一篇：SDK FAQ](https://help.aliyun.com/zh/isi/support/sdk-faq)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能类

为什么TTS语音合成的语音和WAV文件显示的时间长度不一致？例如语音文件显示长度是7秒钟，但实际语音只有不到5秒？

语音合成时间戳功能是什么？

语音合成时，能否控制一串数字是按数字来整体播报还是按字符来单独播报，有参数可以控制吗？

对于多音字，TTS语音合成服务发音的策略是怎么样的？

长文本语音合成有调用限制吗？

性能类

为什么TTS语音合成服务的调用有字数限制？

为什么语音合成速度慢，延迟非常大？

语音合成的读音正确率怎么样？

语音合成的发音读错怎么办？多音字如何控制发音？

为什么不同声色的语音合成音产生的延迟不一样？

语音合成的时候可以识别哪些标点符号？

语音合成支持部分文本调速吗？

本文汇总了您在使用语音合成服务时的常见问题。

语音合成类常见问题主要分为以下几类：

- 功能类

  - [为什么TTS语音合成的语音和wav文件显示的时间长度不一致？例如语音文件显示长度是7秒钟，但实际语音只有不到5秒？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-652-jur-1uu "")

  - [语音合成时间戳功能是什么？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-5sq-vam-id6 "")

  - [语音合成时，能否控制一串数字是按数字来整体播报还是按字符来单独播报，有参数可以控制吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-bef-9v5-jvz "")

  - [对于多音字，TTS语音合成服务发音的策略是怎么样的？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-4xh-1fi-rg8 "")

  - [长文本语音合成有调用限制吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-utr-dup-6gm "")
- 性能类

  - [为什么TTS语音合成服务的调用有字数限制？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-5xd-7hg-lyb "")

  - [为什么语音合成速度慢，延迟非常大？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-vhb-qzx-hok "")

  - [语音合成的读音正确率怎么样？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-rpa-z0u-vun "")

  - [语音合成的发音读错怎么办？多音字如何控制发音？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-jzv-8xh-t2t "")

  - [为什么不同声色的语音合成音产生的延迟不一样？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-512-oos-ayt "")

  - [语音合成的时候可以识别哪些标点符号？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-wj6-tgz-l8t "")

  - [语音合成支持部分文本调速吗？](https://help.aliyun.com/zh/isi/support/faq-about-speech-synthesis#sectiondiv-i6s-o9z-4yc "")

## 功能类

### 为什么TTS语音合成的语音和WAV文件显示的时间长度不一致？例如语音文件显示长度是7秒钟，但实际语音只有不到5秒？

TTS是流式合成机制，也就是边合成边返回数据，因此保存下来的WAV文件头是一个预估的值，有一定的误差。如果对于时长要求较为严格，您可以设置 **format** 为 **pcm**，在获取的完整的一句合成结果文件中自行添加WAV头信息，这样就会得到更为精确的时长。具体请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/overview-of-speech-synthesis#topic-1917944 "")。

### 语音合成时间戳功能是什么？

语音实时合成服务在输出音频流的同时，可输出每个汉字/英文单词在音频中的时间位置，即时间戳，时间戳功能又叫字级别音素边界接口。该时间信息可用于驱动虚拟人口型、做视频配音字幕等。具体请参见 [语音合成时间戳功能介绍](https://help.aliyun.com/zh/isi/developer-reference/timestamp-feature#topic-1917952 "")。

### 语音合成时，能否控制一串数字是按数字来整体播报还是按字符来单独播报，有参数可以控制吗？

您可以尝试使用SSML功能。SSML是一种基于XML的语音合成标记语言，SSML不仅可以控制语音合成能读什么，更可以控制语音合成怎么读，包括控制断句分词方式、发音、速度、停顿、声调、音量等特征，甚至加入背景音乐。具体请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview#topic-1917951 "")。

### 对于多音字，TTS语音合成服务发音的策略是怎么样的？

当遇到不是词组的多音字，TTS语音合成转换的时候会根据上下文进行多音字的预测，并给出一个发音。

### 长文本语音合成有调用限制吗？

长文本语音合成功能提供了将超长文本（如千字或者万字）合成为语音二进制数据的功能。支持输出PCM、WAV和MP3编码格式数据；支持设置语速、语调和音量；支持设置男声、女声。您可以通过实时和异步方式获取合成结果。

长文本语音合成服务和语音合成服务的差异在于：语音合成服务只能支持300字符以下的文本，而长文本语音合成是为了满足更多用户对千字或者万字文本合成需求，最多支持10万字的一次性快速合成调用。具体请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-1#topic-1917957 "")。

## 性能类

### 为什么TTS语音合成服务的调用有字数限制？

TTS语音合成服务调用有字数限制，是为了避免服务端资源浪费，一次性合成太多字最终未必会使用上。如果通过用API或SDK调用，可以分段调用后拼接；如果是MRCP协议调用，多用于客服或者呼叫中心场景，太多字数的TTS语音合成播放效果会持续播放较长时间，不符合人机交互逻辑，通常会被打断或提前结束。如果是超长文本，如果是千字或万字的新闻播放，可使用长文本语音合成接口，支持10万字的一次性快速合成调用。具体请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-1#topic-1917957 "")。

### 为什么语音合成速度慢，延迟非常大？

随着语音合成效果的不断提升，算法的复杂度也越来越高，对用户而言，可能会遇到合成耗时变长的可能，在计算量较大的高级音色上相对更明显。因此我们建议使用流式合成机制，也就是边接收服务端返回的合成数据，边保存或者播放，可以显著改善语音合成延迟问题。

首先确认统计的是否是文本全部合成的耗时，一般只需要关注首包延迟，即客户端发送完合成请求后到第一次收到服务端返回的二进制流的时间差，即为首包延迟。

### 语音合成的读音正确率怎么样？

语音合成（TTS）是概率模型，目前业界能做到的读音正确率在96%~98%之间，阿里云智能语音交互产品在通用场景下测试准确率在97%左右。这意味着不是所有读音错误都能被修复掉，建议您可以通过换字或使用SSML功能。

### 语音合成的发音读错怎么办？多音字如何控制发音？

您可以通过以下几种方式处理：

- 可以尝试将多音字替换成同音的其他汉字快速解决发音问题。

- 您可以尝试使用SSML功能。SSML是一种基于XML的语音合成标记语言，SSML不仅可以控制语音合成能读什么，更可以控制语音合成怎么读，包括控制断句分词方式、发音、速度、停顿、声调、音量等特征，甚至加入背景音乐。具体请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview#topic-1917951 "")。


### 为什么不同声色的语音合成音产生的延迟不一样？

语音合成的实时率与模型算法的复杂度有关。最快的模型1秒内可合成33秒音频，最慢的模型1秒内可合成0.7秒的音频。普通音色和精品音色的时延不同，算法效果越好的音色相对来说耗时更长。

### 语音合成的时候可以识别哪些标点符号？

特殊符号也会读出相应的发音。例如：α、β、γ、ρ、sin、cos、tan；“百分号”会读成百分之几，“冒号”和“括号”会做停顿处理，“书名号”和“破折号”目前不支持识。 对于特殊符号的处理，TTS语音合成服务和正常人说话效果是相同的，该停顿的时候会停顿。

### 语音合成支持部分文本调速吗？

支持，您可以尝试使用SSML功能。具体请参见 [SSML标记语言介绍](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview#topic-1917951 "")。