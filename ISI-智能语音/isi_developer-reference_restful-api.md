### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)[长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/long-text-to-speech-synthesis/)[异步长文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/asynchronous-long-text-to-speech-synthesis/)RESTful API

# RESTful API

更新时间：2025-01-16 03:54:25

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：接口说明](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-1)[下一篇：时间戳功能介绍](https://help.aliyun.com/zh/isi/developer-reference/timestamp-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能介绍

前提条件

服务地址

POST方法上传文本

请求响应

获取合成结果

服务状态码

Java示例

Python示例

Python 3.x

Python 2.x

PHP示例

Node.js示例

GO示例

长文本语音合成RESTful API支持HTTPS POST方式请求，将待合成的文本通过HTTPS POST上传到服务端，服务端返回文本的语音合成结果。

## 功能介绍

支持如下设置：

- 合成音频的格式：.pcm、.wav、.mp3。

- 合成音频的采样率：8000 Hz、16000 Hz。

- 多种发音人。

- 可设置语速、语调、音量。

- 数据获取方式：轮询方式、回调方式。


**重要**

- **建议使用流式合成机制**：随着TTS合成效果不断提升，算法的复杂度也越来越高，对您而言，可能会遇到合成耗时变长的情况，使用流式合成可以提供更快的响应速度。本文档及SDK示例中有相关流式处理示例代码可供参考。

- **不支持纯JavaScript直接调用RESTful接口**：使用纯JavaScript直接访问RESTful接口可能会遇到跨域问题（Cross-Origin Resource Sharing, CORS），并且存在泄露App Key的风险。


## 前提条件

- 已获取项目Appkey，详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#topic-2572188 "")。

- 已获取Access Token，详情请参见 [获取Token概述](https://help.aliyun.com/zh/isi/overview-of-obtaining-an-access-token#587dee8029x7r "")。


## 服务地址

| 访问类型 | 说明 | URL | Host |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| 访问类型 | 说明 | URL | Host |
| 外网访问 | 所有服务器均可使用外网访问URL。 | https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async | nls-gateway-cn-shanghai.aliyuncs.com |
| 内网访问 | 使用阿里云上海ECS（即ECS地域为华东2（上海）），可使用内网访问URL。 | http://nls-gateway-cn-shanghai-internal.aliyuncs.com/rest/v1/tts/async | nls-gateway-cn-shanghai-internal.aliyuncs.com |

**重要**

- 支持的协议类型：

  - 外网访问：支持HTTP和HTTPS协议。

  - ECS内网访问：只支持HTTP协议。
- 本文的示例使用的是外网访问的方式。在实际业务场景中，请根据实际情况适配URL。


## POST方法上传文本

一个完整的语音合成RESTful API POST请求包含以下要素：

- URL




| 协议 | URL | 方法 |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| 协议 | URL | 方法 |
| HTTPS | https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async | POST |

- HTTPS POST请求体

请求体是请求参数组成的JSON格式字符串，因此在POST请求头部中的`Content-Type`必须设置为”application/json”，示例如下。















```json
{
      "payload":{
          "tts_request":{
              "voice":"xiaoyun",
              "sample_rate":16000,
              "format":"wav",
              "text":"今天天气好晴朗",
              "enable_subtitle": true
          },
          "enable_notify":false
      },
      "context":{
          "device_id":"my_device_id"
      },
      "header":{
          "appkey":"yourAppkey",
          "token":"yourToken"
      }
}
```


## 请求响应

发送请求后，不论是调用成功还是失败，服务端的响应消息都会通过HTTP的消息体返回给客户端。使用HTTPS GET方法和使用HTTPS POST方法请求的响应是相同的，响应的结果都包含在HTTPS的Body中。响应结果的成功或失败通过HTTPS Header的`Content-Type`字段来区分：

- 成功响应

  - Body以JSON格式字符串表示，`status`字段为200，表示请求成功。

  - Body的`data`字段包含task\_id。
- 失败响应

  - HTTPS Header没有`Content-Type`字段，或者`Content-Type`字段内容为`application/json`，表示合成失败，错误信息在Body中。

  - HTTPS Header的`X-NLS-RequestId`字段内容为请求任务的`task_id`。

  - Body内容为错误信息，以JSON格式的字符串表示。

    错误信息字段如下表所示。




    | 名称 | 类型 | 描述 |
    | --- | --- | --- |



    |     |     |     |
    | --- | --- | --- |
    | 名称 | 类型 | 描述 |
    | task\_id | String | 32位请求任务ID，请记录该值，用于排查错误。 |
    | error\_code | Integer | 服务状态码。 |
    | error\_message | String | 服务状态描述。 |
- 发起请求后的成功响应















```javascript
{
    "status":200,
    "error_code":20000000,
    "error_message":"SUCCESS",
    "request_id":"f0a9e2c49e9049e78730a3bf0b32****",
    "data":{
        "task_id":"35d9f813e00b11e9a2ce9ba0d6a2****"
    }
}
```

- 发起请求后的失败响应















```javascript
{
    "error_message":"Meta:ACCESS_DENIED:The token 'fdf' is invalid!",
    "error_code":40000001,
    "request_id":"0d8c0eea55824aada9a374aec650****",
    "url":"/rest/v1/tts/async",
    "status":400
}
```


## **获取合成结果**

根据上一步请求成功响应后返回的task\_id，再次发送GET请求或者轮询获取，获取合成文件并下载。

| 参数 | 示例 |
| --- | --- |

|     |     |
| --- | --- |
| 参数 | 示例 |
| URL | https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async |
| appkey | 您的Appkey。 |
| token | 您的Token。 |
| task\_id | 上一步请求成功响应后返回的task\_id。 |

获取合成结果GET请求示例如下：

```json
https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async?appkey={Appkey}&task_id={task_id}&token={Token}
```

命令执行成功或者轮询服务端合成状态的成功响应返回示例如下，其中`audio_address`为合成后语音的下载链接。

**说明**

`audio_address`字段对应的HTTP下载地址有期限最多只有7天。

```json
/// 轮询时服务端返回的中间状态。
{
    "status":200,
    "error_code":20000000,
    "error_message":"RUNNING",
    "request_id":"a3370c49a29148e78b39978f98ba****",
    "data":{
        "task_id":"35d9f813e00b11e9a2ce9ba0d6a2****",
        "audio_address":null,
        "notify_custom":null
    }
}
/// 获取到最终合成结果。
{
    "status":200,
    "error_code":20000000,
    "error_message":"SUCCESS",
    "request_id":"c541eae489af48d69dae2d2e203a****",
    "data":{
        "sentences":[\
            {\
                "text":"长文本语音合成接口",\
                "begin_time":"0",\
                "end_time":"2239"\
            },\
            {\
                "text":"一次返回所有文本对应的音频.现在需要增加句级别的时间戳信息",\
                "begin_time":"2239",\
                "end_time":"8499"\
            },\
            {\
                "text":"客户可利用该信息，实现播放控制功能",\
                "begin_time":"8499",\
                "end_time":"12058"\
            }\
        ],
        "task_id":"f4e9bf53cb1611eab327b15f61b4****",
        "audio_address":"此处为生成的URL地址",
        "notify_custom":""
    }
}
```

如果开启enable\_notify/notify\_url，回调识别结果为：

```json
 {
"data": {
"audio_address": "http://nls-cloud-cn-shanghai.oss-cn-shanghai.aliyuncs.com/******.wav",
"task_id": "e3a06366d**************e1257693b"
},
"request_id": "edc6b5ab4***********223c8ace71",
"status": 20000000,
"error_code": 20000000,
"error_message": "SUCCESS"
}
```

## 服务状态码

| 服务状态码 | 服务状态描述 | 解决办法 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 服务状态码 | 服务状态描述 | 解决办法 |
| 20000000 | 请求成功 | 无。 |
| 40000000 | 默认的客户端错误码 | 检查对应的错误消息。 |
| 40000001 | 身份认证失败 | 检查使用的令牌是否正确，是否过期。 |
| 40000002 | 无效的消息 | 检查发送的消息是否符合要求。 |
| 40000003 | 无效的参数 | 检查参数值设置是否合理。 |
| 40000004 | 空闲超时 | 确认是否长时间没有发送数据到服务端。 |
| 40000005 | 请求数量过多 | 检查是否超过了并发连接数或者每秒钟请求数。 |
| 40000010 | 试用期已结束，并且未开通商用版、或账号欠费。 | 请登录控制台确认服务开通状态以及账户余额。 |
| 50000000 | 默认的服务端错误 | 内部服务错误，需要客户端进行重试。 |
| 50000001 | 内部GRPC调用错误 | 内部服务错误，需要客户端进行重试。 |

## Java示例

**说明**

更多的Java示例可以 [下载nls-restful-java-demo](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20220929/egtn/nls-restful-java-demo.zip) 查看。

依赖文件内容如下：

```java
<dependency>
    <groupId>com.squareup.okhttp3</groupId>
    <artifactId>okhttp</artifactId>
    <version>3.9.1</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.83</version>
</dependency>
```

示例代码如下：

```java
package com.alibaba.nls.client;
import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONObject;
import okhttp3.MediaType;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
/**
 * 此示例演示了长文本语音合成的使用方式。
 */
public class SpeechLongSynthesizerRestfulDemo {
    private static Logger logger = LoggerFactory.getLogger(SpeechLongSynthesizerRestfulDemo.class);
    private String accessToken;
    private String appkey;
    public SpeechLongSynthesizerRestfulDemo(String appkey, String token) {
        this.appkey = appkey;
        this.accessToken = token;
    }
    public void processPOSTRequest(String text, String format, int sampleRate, String voice) {
        String url = "https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async";
        // 拼接HTTP Post请求的消息体内容。
        JSONObject context = new JSONObject();
        // device_id设置，可以设置为自定义字符串或者设备信息id。
        context.put("device_id", "my_device_id");
        JSONObject header = new JSONObject();
        // 设置你的appkey。获取Appkey请前往控制台：https://nls-portal.console.aliyun.com/applist
        header.put("appkey", appkey);
        // 设置你的Token。获取Token具体操作，请参见：https://help.aliyun.com/document_detail/450514.html
        header.put("token", accessToken);
        // voice 发音人，可选，默认是xiaoyun。
        // volume 音量，范围是0~100，可选，默认50。
        // speech_rate 语速，范围是-500~500，可选，默认是0。
        // pitch_rate 语调，范围是-500~500，可选，默认是0。
        JSONObject tts = new JSONObject();
        tts.put("text", text);
        // 设置发音人。
        tts.put("voice", voice);
        // 设置编码格式。
        tts.put("format", format);
        // 设置采样率。
        tts.put("sample_rate", sampleRate);
        // 设置声音大小，可选。
        //tts.put("volume", 100);
        // 设置语速，可选。
        //tts.put("speech_rate", 200);
        // 长文本tts restful接口支持句级时间戳，默认为false。
        tts.put("enable_subtitle", true);
        JSONObject payload = new JSONObject();
        // 可选，是否设置回调。如果设置，则服务端在完成长文本语音合成之后回调用户此处设置的回调接口，将请求状态推送给用户侧。
        payload.put("enable_notify", false);
        payload.put("notify_url", "http://123.com");
        payload.put("tts_request", tts);
        JSONObject json = new JSONObject();
        json.put("context", context);
        json.put("header", header);
        json.put("payload", payload);
        String bodyContent = json.toJSONString();
        logger.info("POST Body Content: " + bodyContent);
        // 发起请求
        RequestBody reqBody = RequestBody.create(MediaType.parse("application/json"), bodyContent);
        Request request = new Request.Builder()
            .url(url)
            .header("Content-Type", "application/json")
            .post(reqBody)
            .build();
        try {
            OkHttpClient client = new OkHttpClient();
            Response response = client.newCall(request).execute();
            String contentType = response.header("Content-Type");
            System.out.println("contentType = " + contentType);
            // 获取结果，并根据返回进一步进行处理。
            String result = response.body().string();
            response.close();
            System.out.println("result = " + result);
            JSONObject resultJson = JSON.parseObject(result);
            if(resultJson.containsKey("error_code") && resultJson.getIntValue("error_code") == 20000000) {
                logger.info("Request Success! task_id = " + resultJson.getJSONObject("data").getString("task_id"));
                String task_id = resultJson.getJSONObject("data").getString("task_id");
                String request_id = resultJson.getString("request_id");
                /// 可选：轮询检查服务端的合成状态，该轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
                waitLoop4Complete(url, appkey, accessToken, task_id, request_id);
            }else {
                logger.error("Request Error: status=" + resultJson.getIntValue("status")
                    + ", error_code=" + resultJson.getIntValue("error_code")
                    + ", error_message=" + resultJson.getString("error_message"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    /// 根据特定信息轮询检查某个请求在服务端的合成状态，轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
    private void waitLoop4Complete(String url, String appkey, String token, String task_id, String request_id) {
        String fullUrl = url + "?appkey=" + appkey + "&task_id=" + task_id + "&token=" + token + "&request_id=" + request_id;
        System.out.println("query url = " + fullUrl);
        while(true) {
            Request request = new Request.Builder().url(fullUrl).get().build();
            try {
                OkHttpClient client = new OkHttpClient();
                Response response = client.newCall(request).execute();
                String result = response.body().string();
                response.close();
                System.out.println("waitLoop4Complete = " + result);
                JSONObject resultJson = JSON.parseObject(result);
                if(resultJson.containsKey("error_code")
                    && resultJson.getIntValue("error_code") == 20000000
                    && resultJson.containsKey("data")
                    && resultJson.getJSONObject("data").getString("audio_address") != null) {
                    logger.info("Tts Finished! task_id = " + resultJson.getJSONObject("data").getString("task_id"));
                    logger.info("Tts Finished! audio_address = " + resultJson.getJSONObject("data").getString("audio_address"));
                    break;
                }else {
                    logger.info("Tts Queuing...");
                }
                // 每隔10秒钟轮询一次状态。
                Thread.sleep(10000);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
    public static void main(String[] args) {
        if (args.length < 2) {
            System.err.println("SpeechLongSynthesizerRestfulDemo need params: <token> <app-key>");
            System.exit(-1);
        }
        String token = args[0];
        String appkey = args[1];
        SpeechLongSynthesizerRestfulDemo demo = new SpeechLongSynthesizerRestfulDemo(appkey, token);
        String text = "我家的后面有一个很大的园，相传叫作百草园。现在是早已并屋子一起卖给朱文公的子孙了，连那最末次的相见也已经隔了七八年，其中似乎确凿只有一些野草；但那时却是我的乐园。";
        String format = "wav";
        int sampleRate = 16000;
        String voice = "siyue";
        demo.processPOSTRequest(text, format, sampleRate, voice);
    }
}
```

## Python示例

**说明**

- Python 2.x请使用httplib模块；Python 3.x请使用http.client模块。

- 创建HTTP/HTTPS连接时，Python 2.x使用httplib模块，Python 3.x使用http.client模块：






Python 2.x



Python 3.x























创建HTTP连接



创建HTTPS连接

































```python
import httplib

host = 'nls-gateway-cn-shanghai.aliyuncs.com'
conn = httplib.HTTPConnection(host)
```



















```python
import httplib

host = 'nls-gateway-cn-shanghai.aliyuncs.com'
conn = httplib.HTTPSConnection(host)
```









创建HTTP连接



创建HTTPS连接

































```python
import http.client

host = 'nls-gateway-cn-shanghai.aliyuncs.com'
conn = http.client.HTTPConnection(host)
```



















```python
import http.client

host = 'nls-gateway-cn-shanghai.aliyuncs.com'
conn = http.client.HTTPSConnection(host)
```

- 采用RFC 3986规范进行urlencode编码，Python 2.x请使用urllib模块的urllib.quote，Python 3.x请使用urllib.parse模块的urllib.parse.quote\_plus。


### Python 3.x

```python
import http.client
import urllib.request
import json
import time

class TtsHeader:
    def __init__(self, appkey, token):
        self.appkey = appKey
        self.token = token

    def tojson(self, e):
        return {'appkey': e.appkey, 'token': e.token}

class TtsContext:
    def __init__(self, device_id):
        self.device_id = device_id
    # 将序列化函数定义到类中。

    def tojson(self, e):
        return {'device_id': e.device_id}

class TtsRequest:
    def __init__(self, voice, sample_rate, format, enable_subtitle, text):
        self.voice = voice
        self.sample_rate = sample_rate
        self.format = format
        self.enable_subtitle = enable_subtitle
        self.text = text

    def tojson(self, e):
        return {'voice': e.voice, 'sample_rate': e.sample_rate, 'format': e.format, 'enable_subtitle': e.enable_subtitle, 'text': e.text}

class TtsPayload:
    def __init__(self, enable_notify, notify_url, tts_request):
        self.enable_notify = enable_notify
        self.notify_url = notify_url
        self.tts_request = tts_request

    def tojson(self, e):
        return {'enable_notify': e.enable_notify, 'notify_url': e.notify_url, 'tts_request': e.tts_request.tojson(e.tts_request)}

class TtsBody:
    def __init__(self, tts_header, tts_context, tts_payload):
        self.tts_header = tts_header
        self.tts_context = tts_context
        self.tts_payload = tts_payload

    def tojson(self, e):
        return {'header': e.tts_header.tojson(e.tts_header), 'context': e.tts_context.tojson(e.tts_context), 'payload': e.tts_payload.tojson(e.tts_payload)}
# 根据特定信息轮询检查某个请求在服务端的合成状态，每隔10秒钟轮询一次状态.轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。

def waitLoop4Complete(url, appkey, token, task_id, request_id):
    # fullUrl = url + "?appkey=" + appkey + "&task_id=" + task_id + "&token=" + token + "&request_id=" + request_id

    fullUrl = url + "?appkey=" + appkey + "&task_id=" + \
        task_id + "&token=" + token + "&request_id=" + request_id

    print("fullUrl=", fullUrl)
    host = {"Host": "nls-gateway-cn-shanghai.aliyuncs.com", "Accept": "*/*",
            "Connection": "keep-alive", 'Content-Type': 'application/json'}
    while True:
        result = urllib.request.urlopen(fullUrl).read()
        print("query result = ", result)
        jsonData = json.loads(result)

        # jsonData["data"]["audio_address"] is None表示还在未合成完成的状态...每隔10秒钟轮询一次状态
        if (jsonData["data"]["audio_address"] is None):
            print(" Tts Queuing...please wait...")
            time.sleep(10)
        elif "error_code" in jsonData and jsonData["error_code"] == 20000000 and "data" in jsonData and (jsonData["data"]["audio_address"] != ""):
            print("Tts Finished! task_id = " + jsonData["data"]["task_id"])
            print("Tts Finished! audio_address = " +
                  jsonData["data"]["audio_address"])
            break

        else:
            print("Tts Running...")
            time.sleep(10)
# 长文本语音合成restful接口，支持post调用，不支持get请求。发出请求后，可以轮询状态或者等待服务端合成后自动回调（如果设置了回调参数）。

def requestLongTts4Post(tts_body, appkey, token):
    host = 'nls-gateway.cn-shanghai.aliyuncs.com'
    url = 'https://' + host + '/rest/v1/tts/async'
    # 设置HTTP Headers
    http_headers = {'Content-Type': 'application/json'}
    print('The POST request body content: ' + tts_body)
    conn = http.client.HTTPSConnection(host)
    #conn = httplib.HTTPConnection(host)
    conn.request(method='POST', url=url, body=tts_body, headers=http_headers)
    response = conn.getresponse()
    print('Response status and response reason:')
    print(response.status, response.reason)
    contentType = response.getheader('Content-Type')
    print(contentType)
    body = response.read()
    if response.status == 200:
        jsonData = json.loads(body)
        print('The request succeed : ', jsonData)
        print('error_code = ', jsonData['error_code'])
        task_id = jsonData['data']['task_id']
        request_id = jsonData['request_id']
        print('task_id = ', task_id)
        print('request_id = ', request_id)
        # 说明：轮询检查服务端的合成状态，轮询操作非必须。如果设置了回调url，则服务端会在合成完成后主动回调。
        waitLoop4Complete(url, appkey, token, task_id, request_id)
    else:
        print('The request failed: ' + str(body))

appKey = 'yourAppkey'
token = 'yourToken'

text = '今天是周一，天气挺好的。'

# 拼接HTTP Post请求的消息体内容。
th = TtsHeader(appKey, token)
tc = TtsContext("mydevice")
# TtsRequest对象内容为：发音人、采样率、语音格式、待合成文本内容。
tr = TtsRequest("xiaoyun", 16000, "wav", False, text)
# 是否设置回调url，回调url地址，TtsRequest对象。
tp = TtsPayload(True, "http://134.com", tr)
tb = TtsBody(th, tc, tp)
body = json.dumps(tb, default=tb.tojson)
requestLongTts4Post(str(body), appKey, token)
```

### Python 2.x

```python
# -*- coding: UTF-8 -*-
# Python 2.x
import httplib
import urllib
import urllib2
import json
import time

class TtsHeader:
    def __init__(self, appkey, token):
        self.appkey = appKey
        self.token = token
    def tojson(self, e):
        return {'appkey': e.appkey, 'token': e.token}
class TtsContext:
    def __init__(self, device_id):
        self.device_id = device_id
    #将序列化函数定义到类中。
    def tojson(self, e):
        return {'device_id': e.device_id}
class TtsRequest:
    def __init__(self, voice, sample_rate, format, enable_subtitle, text):
        self.voice = voice
        self.sample_rate = sample_rate
        self.format = format
        self.enable_subtitle = enable_subtitle
        self.text = text
    def tojson(self, e):
        return {'voice': e.voice, 'sample_rate': e.sample_rate, 'format': e.format, 'enable_subtitle': e.enable_subtitle, 'text': e.text}
class TtsPayload:
    def __init__(self, enable_notify, notify_url, tts_request):
        self.enable_notify = enable_notify
        self.notify_url = notify_url
        self.tts_request = tts_request
    def tojson(self, e):
        return {'enable_notify': e.enable_notify, 'notify_url': e.notify_url, 'tts_request': e.tts_request.tojson(e.tts_request)}
class TtsBody:
    def __init__(self, tts_header, tts_context, tts_payload):
        self.tts_header = tts_header
        self.tts_context = tts_context
        self.tts_payload = tts_payload
    def tojson(self, e):
        return {'header': e.tts_header.tojson(e.tts_header), 'context': e.tts_context.tojson(e.tts_context), 'payload': e.tts_payload.tojson(e.tts_payload)}
# 根据特定信息轮询检查某个请求在服务端的合成状态，每隔10秒钟轮询一次状态.轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
def waitLoop4Complete(url, appkey, token, task_id, request_id):
    # fullUrl = url + "?appkey=" + appkey + "&task_id=" + task_id + "&token=" + token + "&request_id=" + request_id

    fullUrl = url + "?appkey=" + appkey + "&task_id=" + task_id + "&token=" + token + "&request_id=" + request_id

    print("fullUrl=", fullUrl)
    host = {"Host":"nls-gateway.cn-shanghai.aliyuncs.com", "Accept":"*/*", "Connection":"keep-alive",'Content-Type': 'application/json'}
    while True:
        req = urllib2.Request(url=fullUrl)
        result = urllib2.urlopen(req).read()
        print("query result = ", result)
        jsonData = json.loads(result)

        # jsonData["data"]["audio_address"] is None表示还在未合成完成的状态...每隔10秒钟轮询一次状态
        if (jsonData["data"]["audio_address"] is None):
            print(" Tts Queuing...please wait...")
            time.sleep(10)
        elif jsonData.has_key("error_code") and jsonData["error_code"] == 20000000 and jsonData.has_key("data") and (jsonData["data"]["audio_address"] != ""):
            print("Tts Finished! task_id = " + jsonData["data"]["task_id"])
            print("Tts Finished! audio_address = " + jsonData["data"]["audio_address"])
            break

        else:
            print("Tts Running...")
            time.sleep(10)
# 长文本语音合成restful接口，支持post调用，不支持get请求。发出请求后，可以轮询状态或者等待服务端合成后自动回调（如果设置了回调参数）。
def requestLongTts4Post(tts_body, appkey, token):
    host = 'nls-gateway.cn-shanghai.aliyuncs.com'
    url = 'https://' + host + '/rest/v1/tts/async'
    # 设置HTTP Headers
    http_headers = {'Content-Type': 'application/json'}
    print('The POST request body content: ' + tts_body)
    conn = httplib.HTTPSConnection(host)
    #conn = httplib.HTTPConnection(host)
    conn.request(method='POST', url=url, body=tts_body, headers=http_headers)
    response = conn.getresponse()
    print('Response status and response reason:')
    print(response.status ,response.reason)
    contentType = response.getheader('Content-Type')
    print(contentType)
    body = response.read()
    if response.status == 200:
        jsonData = json.loads(body)
        print('The request succeed : ', jsonData)
        print('error_code = ', jsonData['error_code'])
        task_id = jsonData['data']['task_id']
        request_id = jsonData['request_id']
        print('task_id = ', task_id)
        print('request_id = ', request_id)
        # 说明：轮询检查服务端的合成状态，轮询操作非必须。如果设置了回调url，则服务端会在合成完成后主动回调。
        waitLoop4Complete(url, appkey, token, task_id, request_id)
    else:
        print('The request failed: ' + str(body))

appKey = 'yourAppkey'
token = 'yourToken'

text = '今天是周一，天气挺好的。'

# 拼接HTTP Post请求的消息体内容。
th = TtsHeader(appKey, token)
tc = TtsContext("mydevice")
# TtsRequest对象内容为：发音人、采样率、语音格式、待合成文本内容。
tr = TtsRequest("xiaoyun", 16000, "wav", False, text)
# 是否设置回调url，回调url地址，TtsRequest对象。
tp = TtsPayload(True, "http://134.com", tr)
tb = TtsBody(th, tc, tp)
body = json.dumps(tb, default=tb.tojson)
requestLongTts4Post(str(body), appKey, token)
```

## PHP示例

**说明**

PHP示例中使用了cURL函数，要求PHP的版本为4.0.2以上，并且确保已安装cURL扩展。

```php
<?php
// 根据特定信息轮询检查某个请求在服务端的合成状态，每隔10秒钟轮询一次状态.轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
function waitLoop4Complete($url, $appkey, $token, $task_id, $request_id) {
    $fullUrl = $url . "?appkey=" . $appkey . "&task_id=" . $task_id . "&token=" . $token . "&request_id=" . $request_id;
    print "query url = " . $fullUrl . "\n";
    while(true) {
        $curl = curl_init();
        curl_setopt($curl, CURLOPT_RETURNTRANSFER, TRUE);
        curl_setopt($curl, CURLOPT_URL, $fullUrl);
        curl_setopt($curl, CURLOPT_HEADER, TRUE);
        curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, FALSE);
        curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, FALSE);
        $response = curl_exec($curl);
        if ($response == FALSE) {
            print "curl_exec failed!\n";
            curl_close($curl);
            return ;
        }
        // 处理服务端返回的响应。
        $headerSize = curl_getinfo($curl, CURLINFO_HEADER_SIZE);
        $headers = substr($response, 0, $headerSize);
        $bodyContent = substr($response, $headerSize);
        print $bodyContent."\n";
        $http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
        if($http_code != 200) {     // 如果请求失败，需要检查调用是否正确。
            print "tts request failure, error code = " . $http_code . "\n";
            curl_close($curl);
            return ;
        }
        curl_close($curl);
        $data = json_decode($bodyContent, true);

        //$data["data"]["audio_address"]== null时表示还在合成未完成的状态,需要等待。。。
        if(isset($data["error_code"]) && $data["error_code"] == 20000000
            && isset($data["data"]) && $data["data"]["audio_address"]== null){

            print "Tts Queuing...please wait..." . "\n";

        }
        else if(isset($data["error_code"]) && $data["error_code"] == 20000000
            && isset($data["data"]) && $data["data"]["audio_address"] != "")  {
            print "Tts Finished! task_id = " . $data["data"]["task_id"] . "\n";
            print "Tts Finished! audio_address = " . $data["data"]["audio_address"] . "\n";
            break;
        }

        // 每隔10秒钟轮询一次状态。
        sleep(10);
    }
}
// 长文本语音合成restful接口，支持post调用，不支持get请求。发出请求后，可以轮询状态或者等待服务端合成后自动回调（如果设置了回调参数）。
function requestLongTts4Post($appkey, $token, $text, $voice, $format, $sampleRate) {

    $url = "https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async";

    // 拼接HTTP Post请求的消息体内容。
    $header = array("appkey" => $appkey, "token" => $token);
    $context = array("device_id" => "my_device_id");
    $tts_request = array("text" => $text, "format" => $format, "voice" => $voice, "sample_rate" => $sampleRate, "enable_subtitle" => false);
    $payload = array("enable_notify" => true, "notify_url" => "http://123.com", "tts_request" => $tts_request);
    $tts_body = array("context" => $context, "header" => $header, "payload" => $payload);
    $body = json_encode($tts_body);
    print "The POST request body content: " . $body . "\n";
    $httpHeaders = array("Content-Type: application/json");
    $curl = curl_init();
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, TRUE);
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_POST, TRUE);
    curl_setopt($curl, CURLOPT_HTTPHEADER, $httpHeaders);
    curl_setopt($curl, CURLOPT_POSTFIELDS, $body);
    curl_setopt($curl, CURLOPT_HEADER, TRUE);
    $response = curl_exec($curl);
    if ($response == FALSE) {
        print "curl_exec failed!\n";
        curl_close($curl);
        return ;
    }
    $headerSize = curl_getinfo($curl, CURLINFO_HEADER_SIZE);
    $headers = substr($response, 0, $headerSize);
    $bodyContent = substr($response, $headerSize);
    $http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
    if($http_code != 200) {
        print "tts request failure, error code = " . $http_code . "\n";
        print "tts request failure, response = " . $bodyContent . "\n";
        return ;
    }
    curl_close($curl);
    print $bodyContent . "\n";
    $data = json_decode($bodyContent, true);
    if( isset($data["error_code"]) && $data["error_code"] == 20000000) {
        $task_id = $data["data"]["task_id"];
        $request_id = $data["request_id"];
        print "Request Success! task_id = " . $task_id . "\n";
        print "Request Success! request_id = " . $request_id . "\n";
        ///说明：轮询检查服务端的合成状态，轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
        waitLoop4Complete($url, $appkey, $token, $task_id, $request_id);
    } else {
        print "Request Error: status=" . $data["status"] . "; error_code=" . $data["error_code"] . "; error_message=" . $data["error_message"] . "\n";
    }
}

$appkey = "yourAppkey";
$token = "yourToken";

$text = "今天是周一，天气挺好的。";
$format = "wav";
$voice = "xiaogang";
$sampleRate = 16000;
requestLongTts4Post($appkey, $token, $text, $voice, $format, $sampleRate);

?>
```

## Node.js示例

首先安装request依赖，请在您的示例文件所在目录执行如下命令：

```javascript
npm install request --save
```

示例代码如下：

```javascript
const request = require('request');
const fs = require('fs');
    // 长文本语音合成restful接口，支持post调用，不支持get请求。发出请求后，可以轮询状态或者等待服务端合成后自动回调（如果设置了回调参数）。
    function requestLongTts4Post(textValue, appkeyValue, tokenValue, voiceValue, formatValue, sampleRateValue) {

        var url = "https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async"
        console.log(url);
        // 请求参数，以JSON格式字符串填入HTTPS POST请求的Body中。
        var context = {
            device_id : "device_id",
        };
        var header = {
            appkey : appkeyValue,
            token : tokenValue,
        };
        var tts_request = {
            text : textValue,
            voice : voiceValue,
            format : formatValue,
            "sample_rate" : sampleRateValue,
            "enable_subtitle" : false
        };
        var payload = {
            "enable_notify" : false,
            "notify_url": "http://123.com",
            "tts_request" : tts_request,
        };
        var tts_body = {
            "context" : context,
            "header" : header,
            "payload" : payload
        };
        var bodyContent = JSON.stringify(tts_body);
        console.log('The POST request body content: ' + bodyContent);
        // 设置HTTPS POST请求头部。
        var httpHeaders = {'Content-type' : 'application/json'};
        // 设置HTTPS POST请求。
        // encoding必须设置为null，HTTPS响应的Body为二进制Buffer类型。
        var options = {
            url: url,
            method: 'POST',
            headers: httpHeaders,
            body: bodyContent,
            encoding: null
        };
        request(options, function (error, response, body) {
            // 处理服务端的响应。
            if (error != null) {
                console.log(error);
            } else {
                if(response.statusCode != 200) {
                    console.log("Http Request Fail: " + response.statusCode + "; " + body.toString());
                    return;
                }
                console.log("response result: " + body.toString());
                var code = 0;
                var task_id = "";
                var request_id = "";
                var json = JSON.parse(body.toString());
                console.info(json);
                for(var key in json){
                    if(key=='error_code'){
                        code = json[key]
                    } else if(key=='request_id'){
                        request_id = json[key]
                    } else if(key == "data") {
                        task_id = json[key]["task_id"];
                    }
                }
                if(code == 20000000) {
                    console.info("Request Success! task_id = " + task_id);
                    console.info("Request Success! request_id = " + request_id);
                    /// 说明：轮询检查服务端的合成状态，轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
                    waitLoop4Complete(url, appkey, token, task_id, request_id);
                } else {
                    console.info("Request Error: status=" + $data["status"] + "; error_code=" + $data["error_code"] + "; error_message=" + $data["error_message"]);
                }
            }
        });

    }
    // 根据特定信息轮询检查某个请求在服务端的合成状态，每隔10秒钟轮询一次状态.轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
    function waitLoop4Complete(urlValue, appkeyValue, tokenValue, task_id_value, request_id_value) {
        var fullUrl = urlValue + "?appkey=" + appkeyValue + "&task_id=" + task_id_value + "&token=" + tokenValue + "&request_id=" + request_id_value;
        console.info("query url = " + fullUrl);
        //while(true) {
        var timer = setInterval(() => {
            var options = {
                url: fullUrl,
                method: 'GET'
            };
            console.info("query url = " + fullUrl);
            request(options, function (error, response, body) {
                // 处理服务端的响应。
                if (error != null) {
                    console.log(error);
                } else if(response.statusCode != 200) {
                    console.log("Http Request Fail: " + response.statusCode + "; " + body.toString());
                    return;
                } else {
                    console.log("query result: " + body.toString());
                    var code = 0;
                    var task_id = "";
                    var output_url = "";
                    var json = JSON.parse(body.toString());
                    console.info(json);
                    for(var key in json){
                        if(key=='error_code'){
                            code = json[key]
                        } else if(key=='request_id'){
                            request_id = json[key]
                        } else if(key == "data" && json["data"] != null) {
                            task_id = json[key]["task_id"];
                            audio_address = json[key]["audio_address"];
                        }
                    }
                    if(code == 20000000 && audio_address == null) {

                        console.info("Tts Queuing...please wait...");
                    }
                    else if(code == 20000000 && audio_address != "") {
                        console.info("Tts Finished! task_id = " + task_id);
                        console.info("Tts Finished! audio_address = " + audio_address);
                        // 退出轮询。
                        clearInterval(timer);
                    }
                }
            }
            );
        }
    , 10000);
    }

var appkey = 'yourAppkey';
var token = 'yourToken';

var text = '今天是周一，天气挺好的。';
var voice = "xiaogang";
var format = 'wav';
var sampleRate = 16000;
requestLongTts4Post(text, appkey, token, voice, format, sampleRate);
```

## GO示例

```go
package main

import (
 "bytes"
 "encoding/json"
 "fmt"
 "io/ioutil"
 "net/http"
 "strconv"
 "time"
)

// 长文本语音合成restful接口，支持post调用，不支持get请求。发出请求后，可以轮询状态或者等待服务端合成后自动回调（如果设置了回调参数）。
func requestLongTts4Post(text string, appkey string, token string) {

 var url string = "https://nls-gateway-cn-shanghai.aliyuncs.com/rest/v1/tts/async"

 // 拼接HTTP Post请求的消息体内容。
 context := make(map[string]interface{})
 context["device_id"] = "test-device"
 header := make(map[string]interface{})
 header["appkey"] = appkey
 header["token"] = token
 tts_request := make(map[string]interface{})
 tts_request["text"] = text
 tts_request["format"] = "wav"
 tts_request["voice"] = "xiaogang"
 tts_request["sample_rate"] = 16000
 tts_request["enable_subtitle"] = false
 payload := make(map[string]interface{})
 payload["enable_notify"] = false
 payload["notify_url"] = "http://123.com"
 payload["tts_request"] = tts_request
 ttsBody := make(map[string]interface{})
 ttsBody["context"] = context
 ttsBody["header"] = header
 ttsBody["payload"] = payload
 ttsBodyJson, err := json.Marshal(ttsBody)
 if err != nil {
  panic(nil)
 }
 fmt.Println(string(ttsBodyJson))
 // 发送HTTPS POST请求，处理服务端的响应。
 response, err := http.Post(url, "application/json;charset=utf-8", bytes.NewBuffer([]byte(ttsBodyJson)))
 if err != nil {
  panic(err)
 }
 defer response.Body.Close()
 contentType := response.Header.Get("Content-Type")
 body, _ := ioutil.ReadAll(response.Body)
 fmt.Println(string(contentType))
 fmt.Println(string(body))
 statusCode := response.StatusCode
 if statusCode == 200 {
  fmt.Println("The POST request succeed!")
  var f interface{}
  err := json.Unmarshal(body, &f)
  if err != nil {
   fmt.Println(err)
  }
  // 从消息体中解析出来task_id（重要）和request_id。
  var taskId string = ""
  var requestId string = ""
  m := f.(map[string]interface{})
  for k, v := range m {
   if k == "error_code" {
    fmt.Println("error_code = ", v)
   } else if k == "request_id" {
    fmt.Println("request_id = ", v)
    requestId = v.(string)

   } else if k == "data" {
    fmt.Println("data = ", v)
    data := v.(map[string]interface{})
    fmt.Println(data)
    taskId = data["task_id"].(string)

   }
  }

  // 说明：轮询检查服务端的合成状态，轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
  waitLoop4Complete(url, appkey, token, taskId, requestId)

 } else {
  fmt.Println("The POST request failed: " + string(body))
  fmt.Println("The HTTP statusCode: " + strconv.Itoa(statusCode))
 }

}

// 根据特定信息轮询检查某个请求在服务端的合成状态，每隔10秒钟轮询一次状态.轮询操作非必须，如果设置了回调url，则服务端会在合成完成后主动回调。
func waitLoop4Complete(url string, appkey string, token string, task_id string, request_id string) {
 var fullUrl string = url + "?appkey=" + appkey + "&task_id=" + task_id + "&token=" + token + "&request_id=" + request_id
 fmt.Println("fullUrl=" + fullUrl)
 for {
  response, err := http.Get(fullUrl)
  if err != nil {
   fmt.Println("The GET request failed!")
   panic(err)
  }
  defer response.Body.Close()
  body, _ := ioutil.ReadAll(response.Body)
  fmt.Println("waitLoop4Complete = ", string(body))
  var f interface{}
  json.Unmarshal(body, &f)
  if err != nil {
   fmt.Println(err)
  }
  // 从消息体中解析出来task_id（重要）和request_id。
  var code float64 = 0
  var taskId string = ""
  var audioAddress string = ""
  m := f.(map[string]interface{})
  for k, v := range m {
   if k == "error_code" {
    code = v.(float64)
   } else if k == "request_id" {
   } else if k == "data" {
    if v != nil {
     data := v.(map[string]interface{})
     taskId = data["task_id"].(string)
     if data["audio_address"] == nil {
      fmt.Println("Tts Queuing...,please wait...")

     } else {
      audioAddress = data["audio_address"].(string)
     }
    }
   }
  }
  if code == 20000000 && audioAddress != "" {
   fmt.Println("Tts Finished! task_id = " + taskId)
   fmt.Println("Tts Finished! audio_address = " + audioAddress)
   break
  } else {
   // 每隔10秒钟轮询一次状态
   time.Sleep(time.Duration(10) * time.Second)
  }
 }
}
func main() {
 var appkey string = "yourAppkey"
 var token string = "yourToken"
 var text string = "今天是周一，天气挺好的。"
 requestLongTts4Post(text, appkey, token)

}
```