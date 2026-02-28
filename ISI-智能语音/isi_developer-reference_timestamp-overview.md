### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)[长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/long-text-to-speech-synthesis/)[异步长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/asynchronous-long-text-to-speech-synthesis/)时间戳功能介绍

# 时间戳功能介绍

更新时间：2025-03-27 02:31:39

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：RESTful API](https://help.aliyun.com/zh/isi/developer-reference/restful-api)[下一篇：SSML标记语言介绍](https://help.aliyun.com/zh/isi/developer-reference/ssml-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

参数设置

服务端响应

示例

长文本语音异步合成服务在输出音频流的同时，可输出每次传入文本中各单句（在句号、问号、叹号等位置切分）在音频中的时间位置，即句级别时间戳。该时间信息可用于视频配音字幕或有声书播报文字高亮等场景。本文为您介绍时间戳功能。

## 使用限制

针对长文本语音合成，目前只支持长文本RESTful接口句级时间戳。

## 参数设置

在客户端将请求参数enable\_subtitle设置为true，开启时间戳功能。以RESTful接口为例、其设置方式如下：

```java
// 长文本TTS RESTful接口支持句级时间戳，默认为false，不开启。
tts.put("enable_subtitle", true);
```

## 服务端响应

服务端返回的带字幕信息的响应`sentences`字段。

| 参数 | 类型 | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数 | 类型 | 说明 |
| sentences | List | 时间戳信息 |

其中`sentences`字段格式如下：

| 参数 | 类型 | 说明 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 参数 | 类型 | 说明 |
| begin\_time | String | ⽂本对应TTS语⾳开始时间戳，单位ms。 |
| end\_time | String | ⽂本对应TTS语⾳结束时间戳，单位ms。 |

## 示例

请求示例：

```json
{
    "payload":{
        "tts_request":{
            "voice":"Aifan",
            "sample_rate":16000,
            "format":"mp3",
            "enable_subtitle":true,
            "text":"我家的后面有一个很大的园，相传叫作百草园。现在是早已并屋子一起卖给朱文公的子孙了，连那最末次的相见也已经隔了七八年，其中似乎确凿只有一些野草；但那时却是我的乐园。"
        },
        "notify_url":"http://123****.com",
        "enable_notify":false
    },
    "context":{
        "device_id":"my_device_id"
    },
    "header":{
        "appkey":"1iMxP16qgjP****",
        "token":"16aea272b48d4bb188664611837f****"
    }
}
```

返回示例：

```json
{
    "status":200,
    "data":{
        "sentences":[\
            {\
                "text":"我家的后面有一个很大的园，相传叫作百草园",\
                "begin_time":"0",\
                "end_time":"4247"\
            },\
            {\
                "text":"现在是早已并屋子一起卖给朱文公的子孙了，连那最末次的相见也已经隔了七八年，其中似乎确凿只有一些野草；但那时却是我的乐园",\
                "begin_time":"4247",\
                "end_time":"16060"\
            }\
        ],
        "task_id":"9628f978abab4628b1bcfd5a9da3749f",
        "audio_address":"http://nls-cloud-cn-shanghai.oss-cn-shanghai.aliyuncs.com/jupiter-flow/tmp/9628f978abab4628b1bcfd5a9da3749f.mp3?Expires=1621305670&OSSAccessKeyId=LTAI****************&Signature=OYHTJMQXMpiAx*****",
        "notify_custom":""
    },
    "error_code":20000000,
    "error_message":"SUCCESS",
    "request_id":"7e70c414c31a41ae86b4a5f4241a6f3c"
}
```