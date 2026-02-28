### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)[长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/long-text-to-speech-synthesis/)[实时长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/real-time-long-text-to-speech-synthesis/)时间戳功能介绍

# 时间戳功能介绍

更新时间：2024-04-16 04:50:42

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-6)[下一篇：Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java-1-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能概述

参数设置

服务端响应

返回示例

字级别时间戳代码示例

实时长文本语音合成服务在输出音频流的同时，可输出每个汉字/英文单词在音频中的时间位置，即时间戳。时间戳功能又叫字级别音素边界接口，该时间信息可用于驱动虚拟人口型、做视频配音字幕等。

## **功能概述**

实时长文本语音实时合成服务的时间戳是将大段的文本切分为多个句子，以每句话为单位，与音频一起流式的输出该句子的时间戳和该句话中每个字的时间戳。时间戳以每句话为一个区块，返回句内每个字的时间戳。时间戳与合成的音频保持同步，只有当音频被合成了，时间戳才能被准确计算。

例如，“阿里巴巴。达摩院。”是一个长文本，但属于两个句子：

- 第一句：“阿里巴巴。”

- 第二句：“达摩院。”


时间戳输出示例如下（以下示例仅做举例展示，不代表每个`subtitles`元素只合成一个字的音频）：

```java
// "sentence":true表示句子时间戳，"sentence":false表示字时间戳
{"subtitles":[{"begin_index":0,"end_index":1,"begin_time":0,"end_time":0,"phoneme":"null","text":"","sentence":true},{"begin_index":0,"end_index":1,"begin_time":0,"end_time":150,"phoneme":"null","text":"阿","sentence":false}]}
{"subtitles":[{"begin_index":0,"end_index":1,"begin_time":0,"end_time":0,"phoneme":"null","text":"","sentence":true},{"begin_index":0,"end_index":1,"begin_time":0,"end_time":150,"phoneme":"null","text":"阿","sentence":false},{"begin_index":1,"end_index":2,"begin_time":150,"end_time":325,"phoneme":"null","text":"里","sentence":false}]}
{"subtitles":[{"begin_index":0,"end_index":1,"begin_time":0,"end_time":0,"phoneme":"null","text":"","sentence":true},{"begin_index":0,"end_index":1,"begin_time":0,"end_time":150,"phoneme":"null","text":"阿","sentence":false},{"begin_index":1,"end_index":2,"begin_time":150,"end_time":325,"phoneme":"null","text":"里","sentence":false},{"begin_index":2,"end_index":3,"begin_time":325,"end_time":525,"phoneme":"null","text":"巴","sentence":false}]}
// 当整句话合成后，句子时间戳被准确计算，
{"subtitles":[{"begin_index":0,"end_index":1,"begin_time":0,"end_time":850,"phoneme":"null","text":"","sentence":true},{"begin_index":0,"end_index":1,"begin_time":0,"end_time":150,"phoneme":"null","text":"阿","sentence":false},{"begin_index":1,"end_index":2,"begin_time":150,"end_time":325,"phoneme":"null","text":"里","sentence":false},{"begin_index":2,"end_index":3,"begin_time":325,"end_time":525,"phoneme":"null","text":"巴","sentence":false},{"begin_index":3,"end_index":4,"begin_time":525,"end_time":788,"phoneme":"null","text":"巴","sentence":false}]}
// 句子时间戳的begin_index与end_index与该句话的第个字时间戳相同
{"subtitles":[{"begin_index":4,"end_index":5,"begin_time":850,"end_time":850,"phoneme":"null","text":"","sentence":true},{"begin_index":4,"end_index":5,"begin_time":850,"end_time":1025,"phoneme":"null","text":"达","sentence":false}]}
{"subtitles":[{"begin_index":4,"end_index":5,"begin_time":850,"end_time":850,"phoneme":"null","text":"","sentence":true},{"begin_index":4,"end_index":5,"begin_time":850,"end_time":1025,"phoneme":"null","text":"达","sentence":false},{"begin_index":5,"end_index":6,"begin_time":1025,"end_time":1200,"phoneme":"null","text":"摩","sentence":false}]}
{"subtitles":[{"begin_index":4,"end_index":5,"begin_time":850,"end_time":1512,"phoneme":"null","text":"","sentence":true},{"begin_index":4,"end_index":5,"begin_time":850,"end_time":1025,"phoneme":"null","text":"达","sentence":false},{"begin_index":5,"end_index":6,"begin_time":1025,"end_time":1200,"phoneme":"null","text":"摩","sentence":false},{"begin_index":6,"end_index":7,"begin_time":1200,"end_time":1450,"phoneme":"null","text":"院","sentence":false}]}
```

**重要**

- 只有支持字级别音素边界接口的发音人才有此功能。

- TTS服务返回的字幕是基于发音的，所以不能直接用于上屏，需要使用您的原始文本。

- 如果用于上屏，可以基于返回的结果，定位每个句子的句首和句尾时间戳。


## **参数设置**

在客户端设置请求参数`enable_subtitle`为`true`，开启时间戳功能。

以Java SDK为例，其设置⽅式如下。

```java
// 是否开启字幕功能（返回对应文本的相应时间戳），默认不开启。
synthesizer.addCustomedParam("enable_subtitle", true);
```

## **服务端响应**

服务端返回的带字幕信息的响应MetaInfo事件。

| 参数 | 类型 | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数 | 类型 | 说明 |
| subtitles | List | 时间戳信息。 |

其中，SubtitleItem格式如下。

| 参数 | 类型 | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数 | 类型 | 说明 |
| text | String | ⽂本信息。 |
| begin\_time | Integer | ⽂本对应tts语⾳开始时间戳，单位ms。 |
| end\_time | Integer | ⽂本对应tts语⾳结束时间戳，单位ms。 |
| phoneme | String | 不支持打印该字对应的phone系列，默认输出为`"null"`。 |
| begin\_index | Integer | 该字在整句中的开始位置，从0开始。 |
| end\_index | Integer | 该字在整句中的结束位置，从0开始。 |
| sentence | Boolean | 句子时间戳控制，True表示当前时间戳为句子。 |

## 返回示例

```json
{

   "header":{

      "namespace":"SpeechLongSynthesizer",
      "name":"MetaInfo",
      "status":20000000,
      "message_id":"49818960d4ca40d88ebxxxxxxxxxxx",
      "task_id":"326f3b9d9cfa47f3a692xxxxxxxxxx",
      "status_text":"Gateway:SUCCESS:Success."
   },
   "payload":{

      "subtitles":[\
\
         {\
\
            "text":"",\
            "phoneme":"null",\
            "sentence":true,\
            "begin_index":0,\
            "end_index":1,\
            "begin_time":0,\
            "end_time":498\
         },\
         {\
\
            "text":"你",\
            "phoneme":"null",\
            "sentence":false,\
            "begin_index":0,\
            "end_index":1,\
            "begin_time":0,\
            "end_time":118\
         },\
         {\
\
            "text":"好",\
            "phoneme":"null",\
            "sentence":false,\
            "begin_index":1,\
            "end_index":2,\
            "begin_time":118,\
            "end_time":439\
         }\
      ]
   }
}
{
   "header":{
      "namespace":"SpeechLongSynthesizer",
      "name":"MetaInfo",
      "status":20000000,
      "message_id":"bb4e791f1dff464e9997xxxxxxxxxxxxxx",
      "task_id":"326f3b9d9cfa47f3a6921xxxxxxxxxxxx",
      "status_text":"Gateway:SUCCESS:Success."
   },
   "payload":{
      "subtitles":[\
         {\
            "text":"",\
            "phoneme":"null",\
            "sentence":true,\
            "begin_index":2,\
            "end_index":3,\
            "begin_time":498,\
            "end_time":1067\
         },\
         {\
            "text":"明",\
            "phoneme":"null",\
            "sentence":false,\
            "begin_index":2,\
            "end_index":3,\
            "begin_time":498,\
            "end_time":687\
         },\
         {\
            "text":"天",\
            "phoneme":"null",\
            "sentence":false,\
            "begin_index":3,\
            "end_index":4,\
            "begin_time":687,\
            "end_time":1008\
         }\
      ]
   }
}
```

## 字级别时间戳代码示例

**重要**

- 示例中使用SDK内置的默认语音合成服务的外网访问服务URL，如果您使用位于阿里云上海地域的ECS，且需要通过内网访问服务URL，则在创建NlsClient对象时，设置内网访问的URL：















```java
client = new NlsClient("ws://nls-gateway.cn-shanghai-internal.aliyuncs.com/ws/v1", accessToken);
```

- 示例中将合成的音频保存在文件中，如果您需要播放音频且对实时性要求较高，建议使用流式播放，即边接收语音数据边播放，减少延时。


```json
package com.alibaba.nls.client;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import com.alibaba.nls.client.protocol.NlsClient;
import com.alibaba.nls.client.protocol.OutputFormatEnum;
import com.alibaba.nls.client.protocol.SampleRateEnum;
import com.alibaba.nls.client.protocol.tts.SpeechSynthesizer;
import com.alibaba.nls.client.protocol.tts.SpeechSynthesizerListener;
import com.alibaba.nls.client.protocol.tts.SpeechSynthesizerResponse;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
/**
 * 此示例演示了：
 *      长文本语音合成API调用（setLongText）。
 *      流式合成TTS。
 *      首包延迟计算。
 *
 * 说明：该示例和nls-example-tts下的SpeechSynthesizerLongTextDemo不完全相同，长文本语音合成是单独的产品功能，是将一长串文本直接发送给服务端去合成，
 * 而SpeechSynthesizerLongTextDemo演示的是将一长串文本在调用方处切割然后分段调用语音合成接口。
 */
public class SpeechLongSynthesizerDemo {
    private static final Logger logger = LoggerFactory.getLogger(SpeechLongSynthesizerDemo.class);
    private static long startTime;
    private String appKey;
    NlsClient client;
    public SpeechLongSynthesizerDemo(String appKey, String token, String url) {
        this.appKey = appKey;
        //创建NlsClient实例应用全局创建一个即可。生命周期可和整个应用保持一致，默认服务地址为阿里云线上服务地址。
        if(url.isEmpty()) {
            client = new NlsClient(token);
        } else {
            client = new NlsClient(url, token);
        }
    }
    private static SpeechSynthesizerListener getSynthesizerListener() {
        SpeechSynthesizerListener listener = null;
        try {
            listener = new SpeechSynthesizerListener() {
                File f=new File("ttsForLongText.wav");
                FileOutputStream fout = new FileOutputStream(f);
                private boolean firstRecvBinary = true;
                //语音合成结束
                @Override
                public void onComplete(SpeechSynthesizerResponse response) {
                    // 调用onComplete时，表示所有TTS数据已经接收完成，因此为整个合成数据的延迟。该延迟可能较大，不一定满足实时场景。
System.out.println("name: " + response.getName() + ", status: " + response.getStatus()+", output file :"+f.getAbsolutePath());
                }
                //语音合成的语音二进制数据
                @Override
                public void onMessage(ByteBuffer message) {
                    try {
                        if(firstRecvBinary) {
                            // 此处计算首包语音流的延迟，收到第一包语音流时，即可以进行语音播放，以提升响应速度（特别是实时交互场景下）。
                            firstRecvBinary = false;
                            long now = System.currentTimeMillis();
logger.info("tts first latency : " + (now - SpeechLongSynthesizerDemo.startTime) + " ms");
                        }
                        byte[] bytesArray = new byte[message.remaining()];
                        message.get(bytesArray, 0, bytesArray.length);
//System.out.println("write array:" + bytesArray.length);
                        fout.write(bytesArray);
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }

               @Override
                public void onMetaInfo(SpeechSynthesizerResponse response) {
System.out.println("name: " + response.getName() + ", taskId: " + response.getTaskId());
                    JSONArray subtitles = (JSONArray)response.getObject("subtitles");
                    List<Map> subtitleList = subtitles.toJavaList(Map.class);
                    for (Map word : subtitleList) {
System.out.println("current subtitle: " + word);
                    }
                }

                @Override
                public void onFail(SpeechSynthesizerResponse response){
                    // task_id是调用方和服务端通信的唯一标识，当遇到问题时，需要提供此task_id以便排查。
                    System.out.println(
                        "task_id: " + response.getTaskId() +
                            //状态码
                            ", status: " + response.getStatus() +
                            //错误信息
                            ", status_text: " + response.getStatusText());
                }
            };
        } catch (Exception e) {
            e.printStackTrace();
        }
        return listener;
    }
    public void process(String text) {
        SpeechSynthesizer synthesizer = null;
        try {
            //创建实例，建立连接。
            synthesizer = new SpeechSynthesizer(client, getSynthesizerListener());
            synthesizer.setAppKey(appKey);
            //设置返回音频的编码格式。
synthesizer.setFormat(OutputFormatEnum.WAV);
            //设置返回音频的采样率。
            synthesizer.setSampleRate(SampleRateEnum.SAMPLE_RATE_16K);
            //发音人。注意Java SDK不支持调用超高清场景对应的发音人（例如"zhiqi"），如需调用请使用restfulAPI方式。
synthesizer.setVoice("siyue");
            //语调，范围是-500~500，可选，默认是0。
            synthesizer.setPitchRate(0);
            //语速，范围是-500~500，默认是0。
            synthesizer.setSpeechRate(0);
            //设置用于语音合成的文本
            // 此处调用的是setLongText接口（原语音合成接口是setText）。
            synthesizer.setLongText(text);
            //此方法将以上参数设置序列化为JSON发送给服务端，并等待服务端确认。
            long start = System.currentTimeMillis();
            synthesizer.start();
            logger.info("tts start latency " + (System.currentTimeMillis() - start) + " ms");
            SpeechLongSynthesizerDemo.startTime = System.currentTimeMillis();
            //等待语音合成结束
            synthesizer.waitForComplete();
            logger.info("tts stop latency " + (System.currentTimeMillis() - start) + " ms");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //关闭连接
            if (null != synthesizer) {
                synthesizer.close();
            }
        }
    }
    public void shutdown() {
        client.shutdown();
    }
    public static void main(String[] args) throws Exception {
        String appKey = "";
        String token = "填写你的token";
        // url取默认值
        String url = "wss://nls-gateway.cn-shanghai.aliyuncs.com/ws/v1";
        if (args.length == 2) {
            appKey= args[0];
            token    = args[1];
        } else if (args.length == 3) {
            appKey   = args[0];
            token    = args[1];
            url      = args[2];
        } else {
            System.err.println("run error, need params(url is optional): " + "<app-key> <token> [url]");
            System.exit(-1);
        }
        String ttsTextLong = "百草堂与三味书屋 鲁迅 \n" +
            "我家的后面有一个很大的园，相传叫作百草园。现在是早已并屋子一起卖给朱文公的子孙了，连那最末次的相见也已经隔了七八年，其中似乎确凿只有一些野草；但那时却是我的乐园。\n" +
            "不必说碧绿的菜畦，光滑的石井栏，高大的皂荚树，紫红的桑葚；也不必说鸣蝉在树叶里长吟，肥胖的黄蜂伏在菜花上，轻捷的叫天子（云雀）忽然从草间直窜向云霄里去了。\n" +
            "单是周围的短短的泥墙根一带，就有无限趣味。油蛉在这里低唱，蟋蟀们在这里弹琴。翻开断砖来，有时会遇见蜈蚣；还有斑蝥，倘若用手指按住它的脊梁，便会啪的一声，\n" +
            "从后窍喷出一阵烟雾。何首乌藤和木莲藤缠络着，木莲有莲房一般的果实，何首乌有臃肿的根。有人说，何首乌根是有像人形的，吃了便可以成仙，我于是常常拔它起来，牵连不断地拔起来，\n" +
            "也曾因此弄坏了泥墙，却从来没有见过有一块根像人样！ 如果不怕刺，还可以摘到覆盆子，像小珊瑚珠攒成的小球，又酸又甜，色味都比桑葚要好得远......";
        SpeechLongSynthesizerDemo demo = new SpeechLongSynthesizerDemo(appKey, token, url);
        demo.process(ttsTextLong);
        demo.shutdown();
    }
}
```