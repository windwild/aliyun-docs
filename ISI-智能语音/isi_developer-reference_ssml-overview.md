### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)SSML标记语言介绍

# SSML标记语言介绍

更新时间：2025-04-18 01:40:12

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

使用方式

标签

<speak>

<emotion>

<break>

<s>

<sub>

<w>

<vhml>

<phoneme>

<soundEvent>

<say-as>

综合示例

本文为您介绍SSML（Speech Synthesis Markup Language）标记语言的功能、标签使用及示例。

## 概述

SSML是一种基于XML的语音合成标记语言。与纯文本的合成相比，使用SSML可以充实合成的内容，为最终合成效果带来更多变化。SSML不仅控制语音合成能读什么，更能控制语音合成可以怎么读，包括控制断句分词方式、发音、速度、停顿、声调和音量等特征，甚至加入背景音乐。

**说明**

阿里巴巴语音合成服务的SSML实现基于 [W3C](https://www.w3.org/TR/speech-synthesis/) 的语音合成标记语言版本1.0。但并不支持W3C包含的所有的标记类型，而是从业务角度出发，将支持的标记类型最大程度与业务需求绑定。

## 使用方式

**说明**

- 目前仅中文及英文声音支持SSML功能，中文和英文所支持的SSML标签及内容也有略有差别，详情请参考文档下方各标签的介绍和示例。

- 所有文本需放在<speak></speak>标签之内，且每个语音合成任务只能包含一个<speak></speak>标签。长文本任务（包括实时长文本合成和异步长文本合成）可以含多个成对的<speak></speak>标签。

- 长文本语音合成请求可使用多个<speak></speak>标签，及SSML与文本结合的方式，以下示例可以将全文作为一次请求，在长文本语音合成服务中进行合成测试。















```java
<speak><say-as interpret-as="telephone">114</say-as>查询号码 <say-as interpret-as="cardinal">123</say-as>开始干。加起来为<say-as interpret-as="digits">1234</say-as>。<say-as interpret-as="name">张三</say-as>的快递。<say-as interpret-as="address">富路国际1号楼3单元304</say-as><say-as interpret-as="nick">李四6689</say-as></speak>
```

- 文本头部<speak>之前可以省略XML Header。

- 标签内的文字内容如果包含XML的特殊字符，需要做字符转义，常用的特殊字符对应关系如下。

  - "（双引号）对应：&quot;

  - ' （撇号或单引号）对应：&apos;

  - &（表示和的符号）对应：&amp;

  - <（小于号）对应：&lt;

  - \> （大于号）对应：&gt;

将带标签的文本作为text参数值，上传至语音合成服务，以Java SDK为例：

```java
SpeechSynthesizer synthesizer = new SpeechSynthesizer(client, getSynthesizerListener());
String text = "<speak>请闭上眼睛休息一下<break time=\"500ms\"/>好了，请睁开眼睛。</speak>";
synthesizer.setText(text);
```

发送给语音合成服务的请求内容如下：

```json
{
    "payload": {
        "volume": 50,
        "sample_rate": 16000,
        "format": "wav",
        "text": "<speak>请闭上眼睛休息一下<break time=\"500ms\"/>好了，请睁开眼睛。</speak>"
    },
    "context": {
        "sdk": {
            "name": "nls-sdk-java",
            "version": "2.0.4"
        }
    },
    "header": {
        "namespace": "SpeechSynthesizer",
        "name": "StartSynthesis",
        "message_id": "5fdf78c0dd574b6897f3cb204dd0****",
        "appkey": "fd4er4aa****",
        "task_id": "6e1be78ef5804c50a2c5a8b92de1****"
    }
}
```

## 标签

### <speak>

- 描述

<speak>标签是所有待支持SSML标签的根节点。一切需要调用SSML标签的文本都要包含在<speak></speak>中。

- 语法















```xml
<speak>需要调用SSML标签的文本</speak>
```

- 属性

<speak>标签支持如下属性。




| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| voice | String | 线上可调用的发音人的名称代号，为全小写的voice参数值，如"siyue"。 | 否 | 阿里巴巴语音合成特有标签。在合成时，指定发音人，优先级高于接口请求参数`voice`指定的发音人。<br>**重要**<br>通过阿里云百炼调用时，发音人名称为model参数，请参考： [模型列表](https://help.aliyun.com/zh/model-studio/developer-reference/model-list "")<br>**重要**<br>“xiaoyue”暂不支持在voice中设置。 |
| encodeType | String | PCM/WAV/MP3 | 否 | 阿里巴巴语音合成特有标签。在合成时，指定音频文件格式，优先级高于接口请求参数`format`指定的文件格式。<br>实时长文本任务在SSML标签中设置`encodeType`无效。 |
| sampleRate | String | 8000/16000/24000/48000 | 否 | 阿里巴巴语音合成特有标签。在合成时，指定音频的采样率，优先级高于接口请求参数`sample_rate`指定的音频采样率。<br>实时长文本任务在SSML标签中设置sampleRate无效。 |
| rate | String | \[-500,500\]之间的整数。默认值为0。<br>  - 大于0表示加快语速。<br>    <br>  - 小于0表示减慢语速。 | 否 | 阿里巴巴语音合成特有标签。在合成时，指定音频的语速，优先级高于接口请求参数`speech_rate`指定的语速。<br>**重要**<br>通过阿里云百炼调用时，该参数有效范围为\[0.5,2\]，与实际倍速相同，默认值为1，表示正常语速。 |
| pitch | String | \[-500,500\]之间的整数。默认值为0。<br>  - 大于0表示升高音高。<br>    <br>  - 小于0表示降低音高。 | 否 | 阿里巴巴语音合成特有标签。在合成时，指定音频的音高，优先级高于接口请求参数`pitch_rate`指定的音高。<br>**重要**<br>通过阿里云百炼调用时，该参数的有效范围为\[0.5,2\]，与实际音高相同，默认值为1，表示正常音高。 |
| volume | String | \[0,100\]之间的整数。默认值为50。<br>  - 大于50表示增大音量。<br>    <br>  - 小于50表示减小音量。 | 否 | 阿里巴巴语音合成特有标签。在合成时，指定音频的音量，优先级高于接口请求参数`volume`指定的音量。 |
| effect | String | robot/lolita/lowpass/echo/eq/lpfilter/hpfilter | 否 | 阿里巴巴语音合成特有标签。使用该标签可以使合成的语音产生不同的声音效果。<br>  - robot：机器人音效。<br>    <br>  - lolita：萝莉音效。<br>    <br>  - lowpass：低通音效。<br>    <br>  - echo：回声音效。<br>    <br>  - eq：均衡器。<br>    <br>  - lpfilter：低通滤波器。<br>    <br>  - hpfilter：高通滤波器。<br>    <br>**说明**<br>  - 其中eq、lpfilter、hpfilter是高级效果器，您可以通过`effectValue`自定义效果器的效果。<br>    <br>  - 一个SSML只支持一种音效，不可以写多个effect属性。<br>    <br>  - 选择使用音效功能会增加系统延时。 |
| effectValue | String | 当effect取值为eq/lpfilter/hpfilter时，使用该参数修改效果器的默认效果。 | 否 | - eq（均衡器）：系统默认使用8个等级。对应的频率为\[“40 Hz”,“100 Hz”, “200 Hz”, “400 Hz”, “800 Hz”, “1600 Hz”, “4000 Hz”, “12000 Hz”\]；对应的带宽为\[“1.0q”, “1.0q”, “1.0q”, “1.0q”, “1.0q”, “1.0q”, “1.0q”, “1.0q”\]。在使用过程中，需要输入8个等级对应的增益，其取值范围为\[-20 dB, 20 dB\]。例如，effectValue=”1 1 1 1 1 1 1 1”。是一个以空格分割的8个整数组成的字符串。数值为0表示不调整对应频率的增益。<br>    <br>  - lpfilter：输入低通滤波器的频率值。取值为(0, 目标采样率/2\]之间的整数。例如effectValue=”800”。<br>    <br>  - hpfilter：输入高通滤波器的频率值。取值为(0, 目标采样率/2\]之间的整数。例如effectValue=“1200”。 |
| bgm | String | 线上可调用的背景音乐的名称。参见bgm属性说明。 | 否 | 阿里巴巴语音合成特有标签。为合成的语音添加指定的背景音乐。 |
| backgroundMusicVolume | String | \[0,100\]之间的整数。默认值为50。<br>  - 大于50表示增大音量。<br>    <br>  - 小于50表示减小音量。 | 否 | 阿里巴巴语音合成特有标签。控制背景音乐的音量。 |



其中，bgm属性说明如下。




| **服务内嵌URL** | **自定义背景音URL** |
| --- | --- |



|     |     |
| --- | --- |
| **服务内嵌URL** | **自定义背景音URL** |
| 目前阿里巴巴语音合成服务内嵌如下几款背景音乐供您体验：<br>  - [背景音乐1.wav](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230110/lwro/1.wav)<br>    <br>  - [背景音乐2.wav](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230110/bdzj/2.wav)<br>    <br>  - [背景音乐3.wav](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230110/egia/3.wav) | 您可以根据需求，使用自定义的背景音。需要将背景音存放在阿里云的OSS上，并且所在的存储空间至少为公共读权限，请参见 [创建存储空间](https://help.aliyun.com/zh/oss/manage-buckets-create-buckets#task-bcz-sbz-5db "")。使用HTTP/HTTPS协议生成文件访问链接，请参见 [上传文件](https://help.aliyun.com/zh/oss/getting-started/upload-objects-16#concept-zx1-4p4-tdb "")。<br>音频要求：<br>  - 采样率16 kHz、单声道WAV格式。<br>    <br>  - 短文本语音合成不超过2.8 MB，长文本语音合成不超过7.3 MB。<br>    <br>  - 合成时长超出背景音时长时，背景音将随合成音频循环播放（如果背景音不是WAV格式，可使用ffmpeg将其转为WAV格式：`ffmpeg -i 输入音频 -acodec pcm_s16le -ac 1 -ar 16000 目标.wav`）。<br>    <br>  - 标签内的URL如果包含XML的特殊字符，需要做字符转义。<br>    <br>  - 位深度要求16位。<br>    <br>**重要**<br>您需要对上传的音频版权承担相应的法律责任。 |

- 标签关系

<speak>标签可以包含文本和以下标签：

  - <break>

  - <s>

  - <w>

  - <phoneme>

  - <say-as>

  - <vhml/>
- 示例

  - 空属性















    ```xml
    <speak>
      需要调用SSML标签的文本
    </speak>
    ```



    音频效果： [SSML-speak1.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/wibv/SSML-speak1.mp3)

  - voice属性















    ```xml
    <speak voice="xiaogang">
      我是男声。
    </speak>
    ```



    音频效果： [SSML-speak2.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/tknc/SSML-speak2new.mp3)

  - encodeType属性















    ```xml
    <speak encodeType="mp3">
      我可以生成压缩格式的音频。
    </speak>
    ```



    音频效果： [SSML-encode.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/ilsd/SSML-encode.mp3)

  - sampleRate属性















    ```xml
    <speak sampleRate="8000">
      看看我的文件大小吧，是16000采样率音频的一半。
    </speak>
    ```



    音频效果： [SSML-speak4.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/lhoj/SSML-speak4.mp3)

  - rate属性















    ```xml
    <speak rate="200">
      我的语速比正常人快。
    </speak>
    ```



    音频效果： [SSML-speak5.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/jgiv/SSML-speak5.mp3)

  - pitch属性















    ```xml
    <speak pitch="-100">
      我的音高却比别人低。
    </speak>
    ```



    音频效果： [SSML-speak6.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/fhfk/SSML-speak6.mp3)

  - volume属性















    ```xml
    <speak volume="80">
      我的音量也很大。
    </speak>
    ```



    音频效果： [SSML-speak7.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/yrhm/SSML-speak7.mp3)

  - 属性组合（空格分隔）















    ```xml
    <speak rate="200" pitch="-100" volume="80">
      所以放在一起，我的声音是这样的。
    </speak>
    ```



    音频效果： [SSML-speak8.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/ekiz/SSML-speak8.mp3)

  - effect属性















    ```xml
    <speak effect="robot">
      你喜欢机器人瓦力吗？
    </speak>
    ```



    音频效果： [SSML-speak9.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/mdea/SSML-speak9.mp3)

  - bgm属性















    ```xml
    <speak bgm="http://nls.alicdn.com/bgm/2.wav" backgroundMusicVolume="30" rate="-500" volume="40">
      <break time="2s"/>
      阴崖老木苍苍烟
      <break time="700ms"/>
      雨声犹在竹林间
      <break time="700ms"/>
      绵蕝固知裨国计
      <break time="700ms"/>
      绵州风物总堪怜
      <break time="2s"/>
    </speak>
    ```



    音频效果： [SSML-speak10.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/xyfp/SSML-speak10.mp3)

### <emotion>

- 描述

<emotion>用于多情感声音合成，该标签是可选标签，不支持多情感声音合成的发音人使用情感标签会导致合成请求报错。

- 语法















```xml
<emotion category="happy" intensity="1.0">今天天气真不错！</emotion>
```

- 属性

<emotion>标签支持如下属性。




| **属性名称** | **属性类型** | **属性值** | **是否必须** | **描述** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **属性名称** | **属性类型** | **属性值** | **是否必须** | **描述** |
| category | String | 枚举值：如neutral, happy。 | 是 | 指定说话情绪。每个发音人支持的情绪参见下表所示。 |
| intensity | String | 浮点值：数值范围 \[0.01,2.0\]。 | 否 | 指定情绪强度。默认值为1.0，表示预定义的情绪强度。最小值为0.01，导致目标情绪略有倾向。最大值为2.0，导致目标情绪强度加倍。 |



其中，多情感声音支持说明如下。




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

- 标签关系

<emotion>标签可以包含文本和以下标签：

  - <s>

  - <sub>

  - <say-as>

  - <w>

  - <phoneme>

  - <soundEvent/>

  - <break/>

  - <vhml/>
- 示例

  - 空属性















    ```xml
    <speak voice="zhitian_emo">
        <emotion category="happy" intensity="1.0">今天天气真不错！</emotion>
    </speak>
    ```



    音频效果： [SSML-emotion.wav](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/mvbs/SSML-emotion.wav)

### <break>

- 描述

用于在文本中插入停顿，该标签是可选标签。

- 语法















```xml
# 空属性
<break/>
# 带time属性
<break time="string"/>
```

- 属性



**说明**





使用无属性的<break>标签时，停顿时长为“1s”。








| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| time | String | \[number\]s/\[number\]ms | 否 | 以秒/毫秒为单位设置停顿的时长 （如“2s”、“50ms”）。<br>  - \[number\]s：以秒为单位，\[number\]取值范围为\[1, 10\]的整数。<br>    <br>  - \[number\]ms：以毫秒为单位，\[number\]取值范围为\[50, 10000\]的整数。<br>    <br>**重要**<br>连续出现多个`<break>`标签时，停顿时长为各标签停顿时长之和，若总时长超过10秒，则只生效10秒。<br>例如，在以下示例中，连续3个`<break>`标签的总停顿时长为15秒，但由于超过10秒，最终有效停顿时长为10秒。<br>```xml<br> <speak><br>   请闭上眼睛休息一下<break time="5s"/><break time="5s"/><break time="5s"/>好了，请睁开眼睛。<br> </speak><br>``` |

- 标签关系

<break>是空标签，不能包含任何标签。如果SSML结构中存在<s>标签，请把<break>写在<s>里面，表示对当前段落或句子设置停顿。

- 示例















```xml
<speak>
     请闭上眼睛休息一下<break time="500ms"/>好了，请睁开眼睛。
</speak>
```



音频效果： [SSML-break.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/aokv/SSML-break.mp3)


### <s>

- 描述

用于表示文本的句子结构，该标签是可选标签。

- 语法















```xml
<s>文本</s>
```

- 属性

无。

- 标签关系

<s>标签可以包含文本和以下标签：

  - <break>

  - <w>

  - <phoneme>

  - <say-as>

  - <vhml/>
- 示例















```xml
<speak><s>这是第一句话</s><s>这是第二句话</s></speak>
```



音频效果： [SSML-s.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/dfuu/SSML-s.mp3)


### <sub>

- 描述

使用别名替换标签内文本。

- 语法















```xml
<sub alias="string"></sub>
```

- 属性




| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| alias | String | 替换后的内容 | 是 | 用于替换标签内的文本。 |

- 标签关系

<sub>标签可以包括文本及<vhml/>。

- 示例















```javascript
<speak><sub alias="网络协议标准">W3C</sub></speak>
```



音频效果： [SSML-sub.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/cuft/SSML-sub.mp3)


### <w>

- 描述

用于表示文本的词语结构，该标签是可选标签。英文文本通常采用空格来进行分词，一般无需使用此标签。<w>标签内部必须是一个独立的词或短语，这个词或短语不允许混合使用中文和其他外语。

- 语法















```xml
<w>文本</w>
```

- 属性

无。

- 标签关系

<w>标签可以包含文本和<vhml/>

- 示例















```xml
<speak>南京市长<w>江大桥</w>今天发表了演讲。</speak>
```



音频效果： [SSML-w.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/gcaa/SSML-w.mp3)


### **<vhml>**

- 描述

虚拟人类标记语言标签，用于标记人体和面部表情的动画的标记语言，可以插入在文本中，包含一个src属性，内容是一个用户定义的字符串。<vhml>下src属性的内容会在时间戳中返回给用户，用户可以使用这个内容来驱动虚拟人面部或者肢体动画。在时间戳中，src属性的内容会出现在text中，phoneme会为null，begin\_index，end\_index, begin\_time, end\_time均为0。大多数情况<vhml>在时间戳中的顺序会依照<vhml>标签在原文本的顺序来，但是如果<vhml>出现在需要正则化的文本（比如123会正则化成一百二十三）内部或者旁边，会出现和原文本顺序不符合的情况，但是多个<vhml>标签间的顺序不会错乱。

- 语法

<vhml src="content"/>

- 属性

无。

- 标签关系

<vhml/>是一个空标签。

- 示例















```xml
<speak><vhml src="start"/>我们今天来<vhml src="t0"/>介绍一下这个新商品<vhml src="end"/></speak>
时间戳结果：
{
     "subtitles":[\
        {\
           "text":"start",\
           "phoneme":"null",\
           "begin_index":0,\
           "end_index":0,\
           "begin_time":0,\
           "end_time":0\
        },\
        {\
           "text":"我",\
           "phoneme":"null",\
           "begin_index":0,\
           "end_index":1,\
           "begin_time":0,\
           "end_time":88\
        },\
        {\
           "text":"们",\
           "phoneme":"null",\
           "begin_index":1,\
           "end_index":2,\
           "begin_time":88,\
           "end_time":238\
        },\
        {\
           "text":"今",\
           "phoneme":"null",\
           "begin_index":2,\
           "end_index":3,\
           "begin_time":238,\
           "end_time":450\
        },\
        {\
           "text":"天",\
           "phoneme":"null",\
           "begin_index":3,\
           "end_index":4,\
           "begin_time":450,\
           "end_time":650\
        },\
        {\
           "text":"来",\
           "phoneme":"null",\
           "begin_index":4,\
           "end_index":5,\
           "begin_time":650,\
           "end_time":825\
        },\
        {\
           "text":"t0",\
           "phoneme":"null",\
           "begin_index":0,\
           "end_index":0,\
           "begin_time":0,\
           "end_time":0\
        },\
        {\
           "text":"介",\
           "phoneme":"null",\
           "begin_index":5,\
           "end_index":6,\
           "begin_time":825,\
           "end_time":988\
        },\
        {\
           "text":"绍",\
           "phoneme":"null",\
           "begin_index":6,\
           "end_index":7,\
           "begin_time":988,\
           "end_time":1213\
        },\
        {\
           "text":"一",\
           "phoneme":"null",\
           "begin_index":7,\
           "end_index":8,\
           "begin_time":1213,\
           "end_time":1325\
        },\
        {\
           "text":"下",\
           "phoneme":"null",\
           "begin_index":8,\
           "end_index":9,\
           "begin_time":1325,\
           "end_time":1525\
        },\
        {\
           "text":"这",\
           "phoneme":"null",\
           "begin_index":9,\
           "end_index":10,\
           "begin_time":1525,\
           "end_time":1663\
        },\
        {\
           "text":"个",\
           "phoneme":"null",\
           "begin_index":10,\
           "end_index":11,\
           "begin_time":1663,\
           "end_time":1750\
        },\
        {\
           "text":"新",\
           "phoneme":"null",\
           "begin_index":11,\
           "end_index":12,\
           "begin_time":1750,\
           "end_time":1950\
        },\
        {\
           "text":"商",\
           "phoneme":"null",\
           "begin_index":12,\
           "end_index":13,\
           "begin_time":1950,\
           "end_time":2188\
        },\
        {\
           "text":"品",\
           "phoneme":"null",\
           "begin_index":13,\
           "end_index":14,\
           "begin_time":2188,\
           "end_time":2538\
        },\
        {\
           "text":"end",\
           "phoneme":"null",\
           "begin_index":0,\
           "end_index":0,\
           "begin_time":0,\
           "end_time":0\
        }\
     ]
}
```


### <phoneme>

- 描述

用于控制标签内文本的读音，该标签是可选标签。英文文本不支持该标签。

- 语法















```xml
<phoneme alphabet="string" ph="string">文本</phoneme>
```

- 属性




| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| alphabet | String | py | 是 | “py”表示拼音。 |
| ph | String | 标签内文本对应的拼音串 | 是 | 拼音用法的赋值规范：<br>  - 字与字的拼音用空格分隔，拼音的数目必须与字数相等。<br>    <br>  - 每个拼音由发音和音调组成，音调为1~5的数字编号，其中”5”表示轻声。 |

- 标签关系

<phoneme>标签可以包括文本和<vhml/>。

- 示例















```xml
<speak>
      去<phoneme alphabet="py" ph="dian3 dang4 hang2">典当行</phoneme>把这个玩意<phoneme alphabet="py" ph="dang4 diao4">当掉</phoneme>
</speak>
```



音频效果： [SSML-phoneme.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/fxpp/SSML-phoneme.mp3)


### <soundEvent>

- 描述

提示音标签，可以在SSML合成过程中，通过该标签在任意位置插入提示音。

- 语法















```xml
<soundEvent src="URL"/>
```

- 属性




| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| src | String | URL提示音资源路径 | 是 | 您可以根据需求，使用自定义提示音。需要将提示音存放在阿里云OSS上，并且所在的存储空间至少为公共读权限，请参见 [创建存储空间](https://help.aliyun.com/zh/oss/manage-buckets-create-buckets#task-bcz-sbz-5db "")，使用HTTP/HTTPS协议生成文件访问链接请参见 [上传文件](https://help.aliyun.com/zh/oss/getting-started/upload-objects-16#concept-zx1-4p4-tdb "")。<br>音频要求：<br>  - 采样率16 kHz、单声道WAV格式。<br>    <br>  - 不超过2 MB。<br>    <br>  - 位深度要求16位。<br>    <br>**重要**<br>您需要对上传的音频版权承担相应的法律责任。 |

- 标签关系

<soundEvent>是空标签，不可以包含任何标签。

- 示例















```xml
<speak>
     一匹马受了惊吓<soundEvent src="http://nls.alicdn.com/sound-event/horse-neigh.wav"/>人们四散躲避
</speak>
```



音频效果： [SSML-sound-event.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/ivrf/SSML-sound-event.mp3)


### <say-as>

- 描述

用于指示出标签内文本的信息类型，进而按照该类型的默认发音方式发音。

- 语法















```xml
<say-as interpret-as="string">文本</say-as>
```

- 属性




| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **属性名称** | **属性类型** | **属性值** | **是否必选** | **描述** |
| interpret-as | String | cardinal/digits/telephone/name/address/id/characters/punctuation/date/time/currency/measure | 是 | 指示出标签内文本的信息类型：<br>  - cardinal：按整数或小数发音<br>    <br>  - digits：按数字发音。<br>    <br>  - telephone：按电话号码常用方式发音。<br>    <br>  - name：按人名发音。<br>    <br>  - address：按地址发音。<br>    <br>  - id：适用于账户名、昵称等<br>    <br>  - characters：将标签内的文本按字符一一读出。<br>    <br>  - punctuation：将标签内的文本按标点符号的方式读出来。<br>    <br>  - date：按日期发音。<br>    <br>  - time：按时间发音。<br>    <br>  - currency：按金额发音。<br>    <br>  - measure：按计量单位发音。 |

- 各<say-as>类型支持范围

  - cardinal




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字串 | 145 | 一百四十五 | 整数输入范围：20位以内的正负整数，\[-99999999999999999999,99999999999999999999\]。<br>小数输入范围：对小数点后小数的位数没有特殊限制，建议不超过10位。 |
    | 负号+数字串 | -145 | 负一百四十五 |
    | 以逗号分隔3位数字串 | 10,000 | 一万 |
    | 负号+以逗号分隔3位数字串 | -10,124 | 负一万一百二十四 |
    | 数字串+小数点+2个零 | 10.00 | 十 |
    | 负号+数字串+小数点+2个零 | -110.00 | 负一百一十 |
    | 数字串+小数点+数字串 | 79.090 | 七十九点零九零 |
    | 负号+数字串+小数点+数字串 | -79.001 | 负七十九点零零一 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字串 | 145 | one hundred forty five | 整数输入范围：13位以内的正负整数，\[-999999999999,999999999999\]。<br>小数输入范围：对小数点后小数的位数没有特殊限制，建议不超过10位。 |
    | 以零开头的数字串 | 0145 | one hundred forty five |
    | 负号+数字串 | -145 | minus hundred forty five |
    | 以逗号分隔三位数字串 | 60,000 | sixty thousand |
    | 负号+以逗号分隔三位数字串 | -208,000 | minus two hundred eight thousand |
    | 数字串+小数点+零 | 12.00 | twelve |
    | 数字串+小数点+数字串 | 12.34 | twelve point three four |
    | 以逗号分隔三位数字串+小数点+数字串 | 1,000.1 | one thousand point one |
    | 负号+数字串+小数点+数字串 | -12.34 | minus twelve point three four |
    | 负号+以逗号分隔三位数字串+小数点+数字串 | -1,000.1 | minus one thousand point one |
    | （以逗号分隔三位）数字串+连词符+（以逗号分隔三位）数字 | 1-1,000 | one to one thousand |
    | 其他默认读法 | 012.34 | twelve point three four | 无 |
    | 1/2 | one half |
    | -3/4 | minus three quarters |
    | 5.1/6 | five point one over six |
    | -3 1/2 | minus three and a half |
    | 1,000.3^3 | one thousand point three to the power of three |
    | 3e9.1 | three times ten to the power of nine point one |
    | 23.10% | twenty three point one percent |

  - digits




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字串 | 129090909 | 一二九零九零九零九 | 对数字串的长度没有特殊限制，建议不超过20位。<br>当数字串超过10位时，每个数字后插入停顿。 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字串 | 12034 | one two zero three four | 对数字串的长度没有特殊限制，建议不超过20位。<br>当数字串以空格或连词符分组时，分组之间会插入逗号而产生适当停顿，支持最长5个分组。 |
    | 数字串+空格或连词符+数字串+空格或连词符+数字串+空格或连词符+数字串 | 1-23-456 7890 | one, two three, four five six, seven eight nine zero |

  - telephone




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 座机号 | 4930286 | 四九三 零二八六 | 支持7~8位座机号，支持空格和“-”作为分隔符。<br>其中，7位座机号支持“3-4”的数字分隔方式；8位座机号支持“4-4”的数字分隔方式。 |
    | 493 0286 | 四九三 零二八六 |
    | 493-0286 | 四九三 零二八六 |
    | 62552560 | 六二五五 二五六零 |
    | 6255 2560 | 六二五五 二五六零 |
    | 6255-2560 | 六二五五 二五六零 |
    | 座机号+分机号 | 4930286-109 | 四九三 零二八六 转幺零九 | 支持1~4位分机号。 |
    | 4930286转109 | 四九三 零二八六 转幺零九 |
    | 4930286分机109 | 四九三 零二八六 分机幺零九 |
    | 4930286分机号109 | 四九三 零二八六 分机号幺零九 |
    | 区号+座机号 | 01062552560 | 零幺零 六二五五 二五六零 | 支持区号：010、02x、03xx、04xx、05xx、07xx、08xx、09xx。 |
    | 010 62552560 | 零幺零 六二五五 二五六零 |
    | 010 6255 2560 | 零幺零 六二五五 二五六零 |
    | 010 6255-2560 | 零幺零 六二五五 二五六零 |
    | 010-62552560 | 零幺零 六二五五 二五六零 |
    | 010-6255-2560 | 零幺零 六二五五 二五六零 |
    | (010)62552560 | 零幺零 六二五五 二五六零 |
    | 03198907098 | 零三幺九 八九零 七零九八 |
    | 0319-8907098 | 三幺九 八九零 七零九八 |
    | 区号+座机号+分机号 | 010 62552560-109 | 零幺零 六二五五 二五六零 转幺零九 | 无 |
    | 010-62552560-109 | 零幺零 六二五五 二五六零 转幺零九 |
    | (010)62552560-109 | 零幺零 六二五五 二五六零 转幺零九 |
    | (010)62552560转109 | 零幺零 六二五五 二五六零 转幺零九 |
    | (010)62552560分机109 | 零幺零 六二五五 二五六零 分机幺零九 |
    | (010)62552560分机号109 | 零幺零 六二五五 二五六零 分机号幺零九 |
    | 国家代码+区号+座机号 | 86-010-62791627 | 八六 零幺零 六二七九 幺六二七 | 支持国家代码：86、 (86)、+86、(+86)、0086。并统一读为“八六”。 |
    | (86)10-62791627 | 八六 幺零 六二七九 幺六二七 |
    | +86-010-62791627 | 八六 零幺零 六二七九 幺六二七 |
    | 0086-10-62791627 | 八六 幺零 六二七九 幺六二七 |
    | (+86)-10-6279 1627 | 八六 幺零 六二七九 幺六二七 |
    | 国家代码+区号+座机号+分机号 | (86)21-58118818-207 | 八六 二幺 五八幺幺 八八幺八 转二零七 | 无 |
    | (86)021-5811-8818-207 | 八六 零二幺 五八幺幺 八八幺八 转二零七 |
    | (86)021-58118818转207 | 八六 零二幺 五八幺幺 八八幺八 转二零七 |
    | (86)21-5811-8818分机207 | 八六 二幺 五八幺幺 八八幺八 分机二零七 |
    | +86-021-58118818分机号207 | 八六 零二幺 五八幺幺 八八幺八分机号二零七 |
    | 手机号 | 139 0000 5678 | 幺三九 零零零零 五六七八 | 支持11位手机号，支持3-3-5、3-4-4两种数字分隔方式 |
    | 139-000-05678 | 幺三九 零零零 零五六七八 |
    | 139 000 05678 | 幺三九 零零零 零五六七八 |
    | 国家代码+手机号 | +86-13900005678 | 八六 幺三九 零零零零 五六七八 | 无 |
    | (+86)-139-0000-5678 | 八六 幺三九 零零零零 五六七八 |
    | +8613900005678 | 八六 幺三九 零零零零 五六七八 |
    | 0086-139 000 05678 | 八六 幺三九 零零零 零五六七八 |
    | 服务号 | 123 | 幺二三 | - 支持常用的服务号。<br>      <br>    - 支持以400/800开头的10位服务号，支持以“3-3-4”的数字分隔方式。<br>      <br>    - 支持以12530/17951/12593开头的16位号码。 |
    | 95678 | 九五六七八 |
    | 4008110510 | 四零零 八幺幺 零五幺零 |
    | 800-810-8888 | 八零零 八幺零 八八八八 |
    | 1253013520638377 | 幺二五三零 幺三五 二零六三 八三七七 |
    | 其他 | (86)(21)9899-80800-0909 | 八六 二幺 九八九九 八零八零零 零九零九 | 支持“数字串+分隔符（左右括号、-）”方式。 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字串 | 12034 | one two oh three four | 对数字串的长度没有特殊限制，建议不超过20位。当数字串以空格或连词符分组时，分组之间会插入逗号而产生适当停顿，支持最长5个分组。 |
    | 数字串+空格或连词符+数字串+空格或连词符+数字串 | 1-23-456 7890 | one, two three, four five six, seven eight nine oh |
    | 加号+数字串+空格或连词符+数字串 | +43-211-0567 | plus four three, two one one, oh five six seven |
    | 左括号+数字串+右括号+空格+数字串+空格或连词符+数字串 | (21) 654-3210 | (two one) six five four, three two one oh |

  - address




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 常用地址格式 | 元和镇嘉元30-9 | 元和镇嘉元三十杠九 | 支持常用地址格式。此处地址指标准的邮寄地址。 |
    | 市台路388弄1107-1108号 | 市台路三八八弄幺幺零七杠幺幺零八号 |
    | 华润二十四城六期锦云府3-1-3205 | 华润二十四城六期锦云府三杠一杠三二零五 |
    | 圣华名都大厦2幢2006室 | 圣华名都大厦二幢二零零六室 |
    | 五常街道庭院5幢4单元201 | 五常街道庭院五幢四单元二零幺 |
    | 芙蓉江路150弄19号 | 芙蓉江路幺五零弄十九号 |



    英文文本不支持该标签。

  - id




    | **格式** | **示例** | **输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **输出** | **说明** |
    | 字符串 | dell0101 | D E L L 零 一 零 一 | 大小写英文字符、阿拉伯数字0~9、下划线。<br>输出的空格表示每个字符之间插入停顿，即字符一个一个地读。 |
    | myid\_1998 | M Y I D 下划线 一 九 九 八 |
    | AiTest | A I T E S T |



    英文文本该标签功能同标签characters。

  - characters




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 字符串 | ISBN 1-001-099098-1 | I S B N 一 杠 零 零 一 杠 零 九 九 零 九 八 杠 一 | 支持中文汉字、大小写英文字符、阿拉伯数字0~9以及部分全角和半角字符。<br>输出的空格表示每个字符之间插入停顿，即字符一个一个地读。标签内的文本如果包含XML的特殊字符，需要做字符转义。 |
    | x10b2345\_u | x 一 零 b 二 三 四 五 下划线 u |
    | v1.0.1 | v 一 点 零 点 一 |
    | 版本号2.0 | 版本号二 点 零 |
    | 苏M MA000 | 苏M M A 零 零 零 |
    | 空中客车A330 | 空中客车A 三 三 零 |
    | 型号s01 s02和s03 | 型号s 零 一 s 零二 和s 零 三 |
    | 空中客车A330 | 空中客车A 三 三 零 |
    | αβγ | 阿尔法 贝塔 伽玛 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 字符串 | \*b+3$.c-0'=α | asterisk B plus three dollar dot C dash zero apostrophe equals alpha | 支持中文汉字、大小写英文字符、阿拉伯数字0~9以及部分全角和半角字符。<br>输出的空格表示每个字符之间插入停顿，即字符一个一个地读。<br>标签内的文本如果包含XML的特殊字符，需要做字符转义。 |

  - punctuation




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 标点符号 | … | 省略号 | 支持常见中英文标点。输出的空格表示每个字符之间插入停顿，即字符一个一个地读。<br>标签内的文本如果包含XML的特殊字符，需要做字符转义。 |
    | …… | 省略号 |
    | !"#$%& | 叹号 双引号 井号 dollar 百分号 and |
    | ‘()\*+ | 单引号 左括号 右括号 星号 加号 |
    | ,-./:; | 逗号 杠 点 斜杠 冒号 分号 |
    | <=>?@ | 小于 等号 大于 问号 at |
    | \[\\\]^\_ | 左方括号 反斜线 右方括号 脱字符 下划线 |



    英文文本该标签功能同标签characters。

  - date




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | xx年 | 71年 | 七一年 | 支持2位和4位年份。其中：<br>    - 2位年份支持60年~99年、00年~09年、10年~19年。<br>      <br>    - 4位年份支持1000年~1999年、2000年~2099年。 |
    | 04年 | 零四年 |
    | 19年 | 一九年 |
    | 1011年 | 一零一一年 |
    | 1998年 | 一九九八年 |
    | 2008年 | 二零零八年 |
    | xx年xx月 | 98年4月 | 九八年四月 | 当月份为1到9月时，支持开头带“0”和不带“0”两种写法。例如“1908年4月”和“1908年04月”。 |
    | 1998年04月 | 一九九八年四月 |
    | 08年8月 | 零八年八月 |
    | 2008年8月 | 二零零八年八月 |
    | xx年xx月xx日xx年xx月xx号 | 98年4月23日 | 九八年四月二十三日 | 当日期为1到9日时，支持开头带“0”和不带“0”两种写法。例如“1908年4月8日”和“1908年04月08日”。 |
    | 1998年04月23日 | 一九九八年四月二十三日 |
    | 08年8月8号 | 零八年八月八号 |
    | 2008年08月08号 | 二零零八年八月八号 |
    | xx年xx月xx日xx年xx月xx号 | 98年4月23日 | 九八年四月二十三日 | 当日期为1到9日时，支持开头带“0”和不“0”两种写法。例如“1908年4月8日”和“1908年04月08日”。 |
    | 1998年04月23日 | 一九九八年四月二十三日 |
    | 08年8月8号 | 零八年八月八号 |
    | 2008年08月08号 | 二零零八年八月八号 |
    | xx月xx号 | 3月20日 | 三月二十日 | 无 |
    | 08月07号 | 八月七号 |
    | 年月缩写 | 2018/08 | 二零一八年八月 | 支持“/”、“-”、“.”作为缩写的分隔符。 |
    | 2018-08 | 二零一八年八月 |
    | 2018.08 | 二零一八年八月 |
    | 年月日缩写 | 2018/08/08 | 二零一八年八月八日 |
    | 2018-8-8 | 二零一八年八月八日 |
    | 2018.08.08 | 二零一八年八月八日 |
    | xx年xx月xx日~xx年xx月xx日xx年xx月xx号~xx年xx月xx号 | 04年9月1日~30日 | 零四年九月一日至三十日 | 支持“~”、“-”作为“至”的缩写标志。 |
    | 2004年09月01号-2008年06月08号 | 二零零四年九月一号至二零零八年六月八号 |
    | xx年xx月xx日~xx日xx年xx月xx号~xx号 | 04年9月1日~30日 | 零四年九月一日至三十日 |
    | 2004年09月01号-2008年06月08号 | 二零零四年九月一号至二零零八年六月八号 |
    | xx年xx月~xx年xx月 | 01年04月~10年04月 | 零一年四月至一零年四月 |
    | 2001年04月~2010年04月 | 二零零一年四月至二零一零年四月 |
    | xx月xx日~xx月xx日xx月xx号~xx月xx号 | 10月1日~10月7日 | 十月一日至十月七日 |
    | 10月01号~10月07号 | 十月一号至十月七号 |
    | xx月xx日~xx日xx月xx号~xx号 | 10月1日~7日 | 十月一日至七日 |
    | 10月01号~07号 | 十月一号至七号 |
    | 年月日缩写~年月日缩写 | 2018/03/03~2019/01/01 | 二零一八年三月三日至二零一九年一月一日 | 支持“/”、“.”作为缩写的分隔符，支持“~”、“-”作为“至”的缩写标志。 |
    | 1997.9.9~1998.9.9 | 一九九七年九月九日至一九九八年九月九日 |
    | 月日缩写~月日缩写 | 10/20~10/31 | 十月二十日至十月三十一日 |
    | xx~xx月xx月~xx月 | 1~10月 | 一至十月 |
    | 1月~10月 | 一月至十月 |
    | 月日年缩写 | 10/20/2018 | 二零一八年十月二十日 | 仅支持4位的年份，仅支持“/”作为日期的分隔符，仅支持“月/日/年”的书写方式。 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 四位数字/两位数字或四位数字-两位数字 | 2000/01 | two thousand, oh one | 跨年度。 |
    | 1900-01 | nineteen hundred, oh one |
    | 2001-02 | twenty oh one, oh two |
    | 2019-20 | twenty nineteen, twenty |
    | 1998-99 | nineteen ninety eight, ninety nine |
    | 1999-00 | nineteen ninety nine, oh oh |
    | 以1或2开头的四位数字 | 2000 | two thousand | 四位数字年份。 |
    | 1900 | nineteen hundred |
    | 1905 | nineteen oh five |
    | 2021 | twenty twenty one |
    | 星期几-星期几<br>或<br>星期几~星期几<br>或<br>星期几&星期几 | mon-wed | monday to wednesday | 星期几的范围标签内的文本如果包含XML的特殊字符，需要做字符转义。 |
    | tue~fri | tuesday to friday |
    | sat&sun | saturday and sunday |
    | DD-DD MMM, YYYY<br>或<br>DD~DD MMM, YYYY<br>或<br>DD&DD MMM, YYYY | 19-20 Jan, 2000 | the nineteen to the twentieth of january two thousand | DD表示两位数字日期，MMM表示月份的三字母缩写或完整单词，YYYY表示以1或2开头的四位数字年份。 |
    | 01 ~ 10 Jul, 2020 | the first to the tenth of july twenty twenty |
    | 05&06 Apr, 2009 | the fifth and the sixth of april two thousand nine |
    | MMM DD-DD<br>或<br>MMM DD~DD<br>或<br>MMM DD&DD | Feb 01 - 03 | feburary the first to the third | MMM表示月份的三字母缩写或完整单词，DD表示两位数字日期。 |
    | Aug 10~20 | august the tenth to the twentieth |
    | Dec 11&12 | december the eleventh and the twelfth |
    | MMM-MMM<br>或<br>MMM~MMM<br>或<br>MMM&MMM | Jan-Jun | january to june | MMM表示月份的三字母缩写或完整单词。 |
    | jul ~ dec | july to december |
    | sep&oct | september and october |
    | YYYY-YYYY<br>或<br>YYYY~YYYY | 1990 - 2000 | nineteen ninety to two thousand | YYYY表示以1或2开头的四位数字年份。 |
    | 2001~2021 | two thousand one to twenty twenty one |
    | WWW DD MMM YYYY | Sun 20 Nov 2011 | sunday the twentieth of november twenty eleven | WWW表示星期几的三字母缩写或完整单词，DD表示两位数字日期，MMM表示月份的三字母缩写或完整单词，MM表示两位数字月份（或三字母缩写或完整单词），YYYY表示以1或2开头的四位数字年份。 |
    | WWW DD MMM | Sun 20 Nov | sunday the twentieth of november |
    | WWW MMM DD YYYY | Sun Nov 20 2011 | sunday november the twentieth twenty eleven |
    | WWW MMM DD | Sun Nov 20 | sunday november the twentieth |
    | WWW YYYY-MM-DD | Sat 2010-10-01 | aturday october the first twenty ten |
    | WWW YYYY/MM/DD | Sat 2010/10/01 | saturday october the first twenty ten |
    | WWW MM/DD/YYYY | Sun 11/20/2011 | sunday november the twentieth twenty eleven |
    | MM/DD/YYYY | 11/20/2011 | november the twentieth twenty eleven |
    | YYYY | 1998 | nineteen ninety eight |
    | 其他默认读法 | 10 Mar, 2001 | the tenth of march two thousand one | 无 |
    | 10 Mar | the tenth of march |
    | Mar 2001 | march two thousand one |
    | Fri. 10/Mar/2001 | friday the tenth of march two thousand one |
    | Mar 10th, 2001 | march the tenth two thousand one |
    | Mar 10 | march the tenth |
    | 2001/03/10 | march the tenth two thousand one |
    | 2001-03-10 | march the tenth two thousand one |
    | 2000s | two thousands |
    | 2010's | twenty tens |
    | 1900's | nineteen hundreds |
    | 1990s | nineteen nineties |

  - time




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 时刻 | 12:00 | 十二点 | 支持常用时间和时间范围格式。 |
    | 12:00:00点 | 十二点 |
    | 10:20分 | 十点二十分 |
    | 10:20:30 | 十点二十分三十秒 |
    | 09:18:14 | 九点十八分十四秒 |
    | 时刻~时刻 | 11:00~12:00 | 十一点到十二点 |
    | 09:00-14:00 | 九点到十四点 |
    | 11:00~11:30 | 十一点到十一点三十分 |
    | 11:00-12:18 | 十一点到十二点十八分 |
    | 10:30~11:00 | 十点三十分到十一点 |
    | 09:28-10:00 | 九点二十八分到十点 |
    | 10:20~11:20 | 十点二十分到十一点二十分 |
    | 06:00~08:00 | 六点到八点 |
    | 上午10:20~下午13:30 | 上午十点二十分到下午十三点三十分 |
    | 时间缩写 | 5:00 am | 凌晨五点整 |
    | 5:30 am | 凌晨五点半 |
    | 5:20:12 am | 凌晨五点二十分十二秒 |
    | 7:00 am | 上午七点整 |
    | 7:30 AM | 上午七点半 |
    | 7:20:12 a.m. | 上午七点二十分十二秒 |
    | 07:08:12 A.M. | 上午七点零八分十二秒 |
    | 5:00 pm | 下午五点整 |
    | 5:30 PM | 下午五点半 |
    | 5:20:12 p.m. | 下午五点二十分十二秒 |
    | 05:09:12 P.M. | 下午五点零九分十二秒 |
    | 9:00 pm | 晚上九点整 |
    | 9:30 pm | 晚上九点半 |
    | 9:20:12 PM | 晚上九点二十分十二秒 |
    | 9:02:12 P.M. | 晚上九点零二分十二秒 |
    | 12:00 pm | 中午十二点整 |
    | 12:30 p.m. | 中午十二点半 |
    | 12:20:12 PM | 中午十二点二十分十二秒 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | HH:MM AM或PM | 09:00 AM | nine A M | HH表示一或两位数字小时，MM表示两位数字分钟，AM/PM表示上/下午。 |
    | 09:03 PM | nine oh three P M |
    | 09:13 p.m. | nine thirteen p m |
    | HH:MM | 21:00 | twenty one hundred |
    | HHMM | 100 | one oclock |
    | 时刻-时刻 | 8:00 am - 05:30 pm | eight a m to five p m | 支持常见时间格式和范围。 |
    | 7:05~10:15 AM | seven oh five to ten fifteen A M |
    | 09:00-13:00 | nine oclock to thirteen hundred |

  - currency




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字+金额标识符 | 12.00 RMB | 十二人民币 | 支持AUD（澳元） 、CAD（加元）、 HKD（港币）、JPY（日元）、USD（美元）、CHF（瑞士法郎）、NOK（挪威克朗）、SEK（瑞典克朗）、GBP（英镑）、 RMB（人民币）、CNY（元）和EUR（欧元）。<br>支持的数字格式包括：整数、小数以及以逗号分隔的国际写法。 |
    | 12.50 RMB | 十二点五零人民币 |
    | 12,000,000 RMB | 一千二百万人民币 |
    | 12,000,000.00 RMB | 一千二百万人民币 |
    | 12,000.35 RMB | 一万两千点三五人民币 |
    | 金额标识符+数字 | $12 | 十二美元 | 支持 CAD（加元）、 $（美元）、Fr（法郎）、kr（丹麦克朗）、 £（英镑）、¥（元）和 €（欧元）。<br>支持的数字格式包括：整数、小数以及以逗号分隔的国际写法。 |
    | $12.00 | 十二美元 |
    | $12.12 | 二点一二美元 |
    | $12,000 | 一万两千美元 |
    | $12,000.00 | 一万两千美元 |
    | $12,000.99 | 一万两千点九九美元 |
    | 其他默认读法 | 1213 | 一千二百一十三 | 无 |
    | 1213 KML | 一千二百一十三K M L |
    | 1213.00 KML | 一千二百一十三K M L |
    | 1213.9 KML | 一千二百一十三点九K M L |
    | 1,000 KML | 一千K M L |
    | 1,000.00 KML | 一千K M L |
    | 1,000.98 KML | 一千点九八K M L |
    | 12,000 | 一万两千 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字+金额识别符 | 1.00 RMB | one yuan | 支持的数字格式：整数、小数以及以逗号分隔的国际写法。<br>支持的金额识别符：<br>CN¥ (yuan)<br>CNY (yuan)<br>RMB (yuan)<br>AUD (australian dollar)<br>CAD (canadian dollar)<br>CHF (swiss franc)<br>DKK (danish krone)<br>EUR (euro)<br>GBP (british pound)<br>HKD (Hong Kong(China) dollar)<br>JPY (japanese yen)<br>NOK (norwegian krone)<br>SEK (swedish krona)<br>SGD (singapore dollar)<br>USD (united states dollar) |
    | 2.02 CNY | two point zero two yuan |
    | 1,000.23 CN¥ | one thousand point two three yuan |
    | 1.01 SGD | one singapore dollar and one cent |
    | 2.01 CAD | two canadian dollars and one cent |
    | 3.1 HKD | three hong kong dollars and ten cents |
    | 1,000.00 EUR | one thousand euros |
    | 金额识别符+数字 | US$ 1.00 | one US dollar | 支持的数字格式：整数、小数以及以逗号分隔的国际写法。<br>支持的金额识别符：<br>US$ (US dollar)<br>CA$ (Canadian dollar)<br>AU$ (Australian dollar)<br>SG$ (Singapore dollar)<br>HK$ (Hong Kong dollar)<br>C$ (Canadian dollar)<br>A$ (Australian dollar)<br>$ (dollar)<br>£ (pound)<br>€ (euro)<br>CN¥ (yuan)<br>CNY (yuan)<br>RMB (yuan)<br>AUD (australian dollar)<br>CAD (canadian dollar)<br>CHF (swiss franc)<br>DKK (danish krone)<br>EUR (euro)<br>GBP (british pound)<br>HKD (Hong Kong(China) dollar)<br>JPY (japanese yen)<br>NOK (norwegian krone)<br>SEK (swedish krona)<br>SGD (singapore dollar)<br>USD (united states dollar) |
    | $0.01 | one cent |
    | JPY 1.01 | one japanese yen and one sen |
    | £1.1 | one pound and ten pence |
    | €2.01 | two euros and one cent |
    | USD 1,000 | one thousand united states dollars |
    | 数字+量词+金额识别符<br>或<br>金额识别符+数字+量词 | 1.23 Tn RMB | one point two three trillion yuan | 支持的量词格式包括：<br>thousand<br>million<br>billion<br>trillion<br>Mil (million)<br>mil (million)<br>Bil (billion)<br>bil (billion)<br>MM (million)<br>Bn (billion)<br>bn (billion)<br>Tn (trillion)<br>tn (trillion)<br>K(thousand)<br>k (thousand)<br>M (million)<br>m (million) |
    | $1.2 K | one point two thousand dollars |

  - measure




    | **格式** | **示例** | **中文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **中文输出** | **说明** |
    | 数字+中文单位 | 2片 | 两片 | 支持常见中文单位及单位缩写。 |
    | 120公顷 | 一百二十公顷 |
    | 100多毫克 | 一百多毫克 |
    | 100来米 | 一百来米 |
    | 100余人 | 一百余人 |
    | 1厘米20毫米 | 一厘米二十毫米 |
    | 120.00平方公里 | 一百二十平方公里 |
    | 数字+单位缩写 | 120.56 cm² | 一百二十点五六平方厘米 |
    | 120 ㎡ 56 cm² | 一百二十平方米五十六平方厘米 |
    | 100 m 12 cm 6 mm | 一百米十二厘米六毫米 |
    | 范围 | 10~15 kg | 十至十五千克 |
    | 10.24~789.82亩 | 十点二四至七百八十九点八二亩 |
    | 10米~15米 | 十米至十五米 |
    | 10.24 cm~19.08 cm | 十点二四厘米至十九点零八厘米 |
    | 数字+单位+"/"+单位 | 10元/斤 | 十元每斤 |
    | 199~299元/件 | 一百九十九至二百九十九元每件 |
    | 299.99元/g~399.99元/g | 二百九十九点九九元每克至三百九十九点九九元每克 |
    | 其他默认读法 | 12扎 | 十二扎 |
    | 30 rm | 三十r m |
    | 4万万同胞 | 四万万同胞 |
    | 12.897微克 | 十二点八九七微克 |






    | **格式** | **示例** | **英文输出** | **说明** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **示例** | **英文输出** | **说明** |
    | 数字+计量单位 | 1.0 kg | one kilogram | 支持的数字格式：整数、小数以及以逗号分隔的国际写法。<br>支持常见单位缩写。 |
    | 1,234.01 km | one thousand two hundred thirty four point zero one kilometres. |
    | 计量单位 | mm2 | square millimetre |

  - <say-as>常见符号读法如下表所示。




    | **符号** | **中文读法** | **英文读法** |
    | --- | --- | --- |



    |     |     |     |
    | --- | --- | --- |
    | **符号** | **中文读法** | **英文读法** |
    | ! | 叹号 | exclamation mark |
    | “ | 双引号 | double quote |
    | # | 井号 | pound |
    | $ | dollar | dollar |
    | % | 百分号 | percent |
    | & | and | and |
    | ‘ | 单引号 | left quote |
    | （ | 左括号 | left parenthesis |
    | ） | 右括号 | right parenthesis |
    | \* | 星 | asterisk |
    | + | 加 | plus |
    | , | 逗号 | comma |
    | - | 杠 | dash |
    | . | 点 | dot |
    | / | 斜杠 | slash |
    | ： | 零冒号 | solon |
    | ； | 分号 | semicolon |
    | < | 小于 | less than |
    | = | 等号 | equals |
    | > | 大于 | greater than |
    | ? | 问号 | question mark |
    | @ | at | at |
    | \[ | 左方括号 | left bracket |\
    | \ | 反斜线 | back slash |\
    | \] | 右方括号 | right bracket |
    | ^ | 脱字符 | caret |
    | \_ | 下划线 | underscore |
    | \` | 反引号 | back quote |
    | { | 左花括号 | left brace |
    | \| | 竖线 | vertical bar |
    | } | 右花括号 | right brace |
    | ~ | 波浪线 | tilde |
    | ！ | 叹号 | exclamation mark |
    | “ | 左双引号 | left double quote |
    | ” | 右双引号 | right double qute |
    | ‘ | 左单引号 | left quote |
    | ’ | 右单引号 | right quote |
    | （ | 左括号 | left parenthesis |
    | ） | 右括号 | right parenthesis |
    | ， | 逗号 | comma |
    | 。 | 句号 | full stop |
    | — | 杠 | em dash |
    | ： | 冒号 | colon |
    | ； | 分号 | semicolon |
    | ？ | 问号 | question mark |
    | 、 | 顿号 | enumeration comma |
    | … | 省略号 | ellipsis |
    | …… | 省略号 | ellipsis |
    | 《 | 左书名号 | left guillemet |
    | 》 | 右书名号 | right guillemet |
    | ￥ | 人民币符号 | yuan |
    | ≥ | 大于等于 | greater than or equal to |
    | ≤ | 小于等于 | less than or equal to |
    | ≠ | 不等于 | not equal |
    | ≈ | 约等于 | approximately equal |
    | ± | 加减 | plus or minus |
    | × | 乘 | times |
    | π | 派 | pi |
    | Α | 阿尔法 | alpha |
    | Β | 贝塔 | beta |
    | Γ | 伽玛 | gamma |
    | Δ | 德尔塔 | delta |
    | Ε | 艾普西龙 | epsilon |
    | Ζ | 捷塔 | zeta |
    | Θ | 西塔 | theta |
    | Ι | 艾欧塔 | iota |
    | Κ | 喀帕 | kappa |
    | ∧ | 拉姆达 | lambda |
    | Μ | 缪 | mu |
    | Ν | 拗 | nu |
    | Ξ | 克西 | ksi |
    | Ο | 欧麦克轮 | omicron |
    | ∏ | 派 | pi |
    | Ρ | 柔 | rho |
    | ∑ | 西格玛 | sigma |
    | Τ | 套 | tau |
    | Υ | 宇普西龙 | upsilon |
    | Φ | fai | phi |
    | Χ | 器 | chi |
    | Ψ | 普赛 | psi |
    | Ω | 欧米伽 | omega |
    | α | 阿尔法 | alpha |
    | β | 贝塔 | beta |
    | γ | 伽玛 | gamma |
    | δ | 德尔塔 | delta |
    | ε | 艾普西龙 | epsilon |
    | ζ | 捷塔 | zeta |
    | η | 依塔 | eta |
    | θ | 西塔 | theta |
    | ι | 艾欧塔 | iota |
    | κ | 喀帕 | kappa |
    | λ | 拉姆达 | lambda |
    | μ | 缪 | mu |
    | ν | 拗 | nu |
    | ξ | 克西 | ksi |
    | ο | 欧麦克轮 | omicron |
    | π | 派 | pi |
    | ρ | 柔 | rho |
    | σ | 西格玛 | sigma |
    | τ | 套 | tau |
    | υ | 宇普西龙 | upsilon |
    | φ | fai | phi |
    | χ | 器 | chi |
    | ψ | 普赛 | psi |
    | ω | 欧米伽 | omega |

  - <say-as>常见计量单位如下表所示。




    | **格式** | **类别** | **中文示例** | **英文示例** |
    | --- | --- | --- | --- |



    |     |     |     |     |
    | --- | --- | --- | --- |
    | **格式** | **类别** | **中文示例** | **英文示例** |
    | 缩写 | 长度 | nm（纳米）、μm（微米）、 mm（毫米）、cm（厘米）、m（米）、km（千米）、ft（英尺）、in（英寸） | nm (nanometre), μm (micrometre), mm (millimetre), cm (centimetre), m (metre), km (kilometre), ft (foot), in (inch) |
    | 面积 | cm²（平方厘米）、㎡（平方米）、km²（平方千米）、SqFt（平方英尺） | cm² (square centimetre), ㎡ (square metre), km2 (square kilometre), SqFt (square foot) |
    | 体积 | cm³（立方厘米）、m³（立方米）、km³（立方千米）、mL（毫升）、L（升）、gallon（加仑） | cm³ (cubic centimetre), m³ (cubic metre), km3 (cubic kilometre), mL (millilitre), L (millilitre), gal (gallon) |
    | 重量 | μg（微克）、mg（毫克）、g（克）、kg（千克） | μg (microgram), mg (microgram), g (gram), kg (kilogram) |
    | 时间 | min（分）、sec（秒）、ms（毫秒） | min (minute), sec (second), ms (millisecond) |
    | 电磁 | μA（微安）、mA（毫安）、Ω（欧姆）、Hz（赫兹）、kHz（千赫兹）、MHz（兆赫兹）、GHz（吉赫兹）、V（伏）、kV（千伏）、kWh（千瓦时） | μA (microamp), mA (milliamp), Hz (hertz), kHz (kilohertz), MHz (megahertz), GHz (gigahertz), V (volt), kV (kilovolt), kWh (kilowatt hour) |
    | 声音 | dB（分贝） | dB (decibel) |
    | 气压 | Pa（帕）、kPa（千帕）、Mpa（兆帕） | Pa (pascal), kPa (kilopascal), MPa (megapascal) |
    | 其他常见单位 | 支持不限于上述类别的中文单位，例如“米”、“秒”、“美元”、“毫升每瓶”等。以及中文量词，例如“架”、“场”、“头”、“部”、“盆”等。 | 支持不限于上述类别的计量单位，例如 tsp (teaspoon), rpm (round per minute), KB (kilobyte), mmHg (milimetre of mercury) 等。 |
- 标签关系

<say-as>标签可以包括文本及<vhml/>。

- 示例

  - cardinal















    ```javascript
    <speak>
      <say-as interpret-as="cardinal">12345</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_Cardinal.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/nrke/SSML-say-as_Cardinal.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="cardinal">10234</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_cardinal.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/yvvb/A_08DITpZa-5MAAAAAAAAAAAAAARQnAQ.mp3)

  - digits















    ```javascript
    <speak>
      <say-as interpret-as="digits">12345</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_digit.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/wjzm/SSML-say-as_digit.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="digits">10234</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_digits.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/jzgi/A__57jQ7S6zMYAAAAAAAAAAAAAARQnAQ.mp3)

  - telephone















    ```javascript
    <speak>
      <say-as interpret-as="telephone">12345</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_Telephone.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/ansi/SSML-say-as_Telephone.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="telephone">10234</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_telephone.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/aczd/A_oAu7RKN8y8UAAAAAAAAAAAAAARQnAQ.mp3)

  - name















    ```javascript
    <speak>
      她的曾用名是<say-as interpret-as="name">曾小凡</say-as>
    </speak>
    ```



    音频效果： [SSML-say-as\_Name.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/kcwj/SSML-say-as_Name.mp3)

  - address















    ```javascript
    <speak>
      <say-as interpret-as="address">富路国际1号楼3单元304</say-as>
    </speak>
    ```



    音频效果： [SSML-say-as\_Address.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/ewap/SSML-say-as_Address.mp3)

  - id















    ```javascript
    <speak>
      <say-as interpret-as="id">myid_1998</say-as>
    </speak>
    ```



    音频效果： [SSML-say-as\_id.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/diwd/SSML-say-as_id.mp3)

  - characters















    ```javascript
    <speak>
      <say-as interpret-as="characters">希腊字母αβ</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_characters.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/kctr/SSML-say-as_characters.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="characters">*b+3.c$=α</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_characters.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/lusf/A_uAuHS7sbP6sAAAAAAAAAAAAAARQnAQ.mp3)

  - punctuation















    ```javascript
    <speak>
      <say-as interpret-as="punctuation"> -./:;</say-as>
    </speak>
    ```



    音频效果： [SSML-say-as\_punctuation.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/jkuk/SSML-say-as_punctuation.mp3)

  - date















    ```javascript
    <speak>
      <say-as interpret-as="date">1000-10-10</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_date.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/zojv/SSML-say-as_date.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="date">10-01-2020</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_date.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/vfru/A_SIHjS4GHd74AAAAAAAAAAAAAARQnAQ.mp3)

  - time















    ```javascript
    <speak>
      <say-as interpret-as="time">5:00am</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_time.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/ioxn/SSML-say-as_time.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="time">0500</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_time.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/bijt/A_EX2VQbJofSkAAAAAAAAAAAAAARQnAQ.mp3)

  - currency















    ```javascript
    <speak>
      <say-as interpret-as="currency">13,000,000.00RMB</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_currency.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/zeir/SSML-say-as_currency.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="currency">$1,000.01</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_currency.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/sjav/A_N7taQoQPkvAAAAAAAAAAAAAAARQnAQ.mp3)

  - measure















    ```javascript
    <speak>
      <say-as interpret-as="measure">100m12cm6mm</say-as>
    </speak>
    ```



    中文音频效果： [SSML-say-as\_measure.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/oltz/SSML-say-as_measure.mp3)















    ```javascript
    <speak>
      <say-as interpret-as="measure">1,000.01kg</say-as>
    </speak>
    ```



    英文音频效果： [en-SSML-say-as\_measure.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/eoxf/A_dERvQrsiEyMAAAAAAAAAAAAAARQnAQ.mp3)

## 综合示例

本示例将详细展示SSML的使用方法，您可以直接拷贝到管控台的项目功能配置中，测试效果。音频效果： [综合示例.mp3](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20230210/aujt/ssml-sample-wave-sound-event-update-new.mp3)。

**重要**

- 示例样音中旁白发音人使用的是定制声音，暂没有开放。体验定制声音，请参见 [语音合成声音定制](https://ai.aliyun.com/nls/customtts)。

- 语音合成每次合成请求的文本字数不能超过300字符，且只能使用一次<speak>标签，以下示例需要按照<speak>标签分多次进行合成测试。


```xml
<speak>
  相传北宋年间，
  <say-as interpret-as="date">1121-10-10</say-as>，
  <say-as interpret-as="address">开封城</say-as>
  郊外的早晨笼罩在一片
  <sub alias="双十一">11.11</sub>
  前买买买的欢乐海洋中。一支运货的骡队刚进入城门
  <soundEvent src="http://nls.alicdn.com/sound-event/bell.wav"/>
  一个肤白貌美
  <phoneme alphabet="py" ph="de5">地</phoneme>
  姑娘便拦下第一排的小哥<say-as interpret-as="name">阿发。</say-as>
</speak>

<speak voice="xiaomei">
  “亲，本店今日特惠，鞋履全场
  <say-as interpret-as="digits">199</say-as>
  减
  <say-as interpret-as="cardinal">100</say-as>，
  走过路过不要错过”。
</speak>

<speak voice="sicheng" rate="150">
  “不啦不啦，赶着上货，已经
  <say-as interpret-as="time">09:59:59</say-as>
  了，再晚就供应链断裂了”。
</speak>

<speak>
  <say-as interpret-as="name">阿发</say-as>
  擦了擦汗，带着运货队伍，径直穿过闹巷，耳边充斥着各种叫卖声：
</speak>

<speak voice="ninger" rate="200">
  最新花色现染布匹，买两尺送一尺；
</speak>

<speak voice="xiaobei">
  爆款纱帽头盔，7天无理由退货；
</speak>

<speak voice="sijia">
  专治大小方脉，调理男人妇人疑难杂症。
</speak>

<speak>
  突然，一匹马不知怎么受了惊，在路上嘶鸣狂奔
  <soundEvent src="http://nls.alicdn.com/sound-event/horse-neigh.wav"/>
  一个孩子也吓坏了，跌跌撞撞地扑向大人怀里
  <break time="50ms"/>大喊道：
</speak>

<speak voice="sitong" rate="150">
  “妈妈，妈妈！”
</speak>

<speak>
  这时，
  <say-as interpret-as="name">阿发</say-as>
  心想
</speak>

<speak effect="robot" pitch="-100">
  “吓死宝宝了！”
</speak>

<speak>
  于是他赶紧捂住了
  <phoneme alphabet="py" ph="he2 bao1">钱包</phoneme>，
  继续赶路送货。一路上，
  <say-as interpret-as="address">开封城</say-as>
  的繁荣景象给
  <say-as interpret-as="name">阿发</say-as>
  留下了深刻的印象。
</speak>

<speak bgm="http://nls.alicdn.com/bgm/2.wav" backgroundMusicVolume="30" rate="-200">
  物换星移，繁华落尽，于是他在购物狂欢之余握起画笔，勾勒出一幅长卷，并命名为《清明上河图》。
</speak>
```