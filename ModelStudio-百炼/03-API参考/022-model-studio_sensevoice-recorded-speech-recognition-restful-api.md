### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音识别](https://help.aliyun.com/zh/model-studio/speech-recognition-api-reference/)[录音文件识别（SenseVoice）- 即将下线](https://help.aliyun.com/zh/model-studio/sensevoice-speech-recognition/)RESTful API

# SenseVoice录音语音识别RESTful API

更新时间：2026-02-11 02:30:17

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

模型列表

约束

提交任务接口

基本信息

请求参数

响应参数

查询任务接口

基本信息

请求参数

响应参数

识别结果说明

完整示例

错误码

更多示例

常见问题

语言列表

**警告**

**SenseVoice 服务即将下线**：SenseVoice 录音文件识别服务即将下线，为避免影响业务，请尽快迁移至其他语音识别服务（ [录音文件识别-Paraformer/Fun-ASR](https://help.aliyun.com/zh/model-studio/recording-file-recognition "")、 [录音文件识别-千问](https://help.aliyun.com/zh/model-studio/qwen-speech-recognition "")）。

本文介绍SenseVoice录音文件识别RESTful API的使用。

**用户指南：** 关于模型介绍和选型建议请参见 [录音文件识别-Fun-ASR/Paraformer/SenseVoice](https://help.aliyun.com/zh/model-studio/recording-file-recognition "")。

目前提供了 [提交任务接口](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#418f2ac8ecxm4 "") 和 [查询任务接口](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#480630e0582sb "")，通常情况下，您可以先调用提交任务接口开启任务，然后循环调用查询任务接口，直至任务完成。

## **前提条件**

已开通服务并 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。请 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")，而非硬编码在代码中，防范因代码泄露导致的安全风险。

## **模型列表**

| **模型名** | **模型简介** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名** | **模型简介** |
| sensevoice-v1 | 语音识别大模型，支持50多种语言的识别，具备情感分析和音频事件检测功能，并默认提供标点符号预测及逆文本正则化（ITN）能力。 |

## **约束**

服务不支持本地音/视频文件直传，输入源需为可通过公网访问的文件URL（支持HTTP/HTTPS协议，示例：`https://your-domain.com/file.mp3`）。URL通过`file_urls`参数指定，单次请求最多支持100个URL。

使用SDK时，若录音文件存储在 [阿里云OSS](https://help.aliyun.com/zh/oss/user-guide/simple-upload#a632b50f190j8 "")，不支持使用以 `oss://`为前缀的临时 URL。

使用RESTful API时，若录音文件存储在 [阿里云OSS](https://help.aliyun.com/zh/oss/user-guide/simple-upload#a632b50f190j8 "")，支持使用以 `oss://`为前缀的临时 URL：

**重要**

- 临时 URL 有效期48小时，过期后无法使用， **请勿用于生产环境。**

- 文件上传凭证接口限流为 100 QPS 且不支持扩容， **请勿用于生产环境、高并发及压测场景。**

- 生产环境建议使用 [阿里云OSS](https://help.aliyun.com/zh/oss/user-guide/what-is-oss "") 等稳定存储，确保文件长期可用并规避限流问题。


- **音频格式**

`aac`、`amr`、`avi`、`flac`、`flv`、`m4a`、`mkv`、`mov`、`mp3`、`mp4`、`mpeg`、`ogg`、`opus`、`wav`、`webm`、`wma`、`wmv`



**重要**





由于音/视频格式及其变种众多，技术上无法穷尽测试，API不能保证所有格式均能够被正确识别。请通过测试验证您所提供的文件能够获得正常的语音识别结果。

- **音频文件大小和时长**

音频文件不超过2GB；无时长限制。

如果希望处理的文件超过了上述限制，可尝试对文件进行预处理以降低文件尺寸。有关文件预处理的最佳实践可以查阅 [预处理视频文件以提高文件转写效率（针对录音文件识别场景）](https://help.aliyun.com/zh/model-studio/paraformer-best-practices#c5dda0a0cf2x9 "")。

- **批处理音频数目**

单次请求最多支持100个文件URL。


- **可识别语言**

详情请参见 [语言列表](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#66ac0678d6b4w "")。



**重要**





SenseVoice每次只支持识别一种语言，请勿在`language_hints`参数中指定多个语言代码。

- **接口调用方式限制**

不支持前端直接调用API，需通过后端中转。


## **提交任务接口**

### **基本信息**

|     |     |
| --- | --- |
| **接口描述** | 提交语音识别任务。 |
| **URL** | ```http<br>https://dashscope.aliyuncs.com/api/v1/services/audio/asr/transcription<br>``` |
| **请求方法** | POST |
| **请求头** | ```http<br>Authorization: Bearer {api-key} // 需替换为您自己的API Key<br>Content-Type: application/json<br>X-DashScope-Async: enable<br>``` |
| **消息体** | 包含所有 [请求参数](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#493b0f8f2ap0y "") 的消息体如下，对于可选字段，在实际业务中可根据需求省略：<br>```json<br>{<br>    "model":"sensevoice-v1", //模型名固定为sensevoice-v1<br>    "input":{<br>        "file_urls":[<br>            "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/sensevoice/rich_text_example_1.wav"<br>        ] //待识别文件，必选<br>    },<br>    "parameters":{<br>        "channel_id":[<br>            0<br>        ], //音轨索引，可选<br>        "disfluency_removal_enabled":false, //过滤语气词开关，可选<br>        "language_hints":["en"] //指定识别语音中语言代码。SenseVoice只支持配置一个语种。<br>    }<br>}<br>``` |

### **请求参数**

**点击查看请求示例**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/services/audio/asr/transcription' \
     --header "Authorization: Bearer $DASHSCOPE_API_KEY" \
     --header "Content-Type: application/json" \
     --header "X-DashScope-Async: enable" \
     --data '{"model":"sensevoice-v1","input":{"file_urls":["https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/sensevoice/rich_text_example_1.wav"]},"parameters":{"language_hints":["en"]}}'
```

| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| model | string | - | 是 | 指定模型名。固定为`sensevoice-v1` **。** |
| file\_urls | array\[string\] | - | 是 | 待识别音/视频文件的URL列表，支持HTTP / HTTPS协议，单次请求最多支持100个URL。<br>若录音文件存储在阿里云OSS，使用RESTful API方式支持使用以 oss://为前缀的临时 URL。<br>**重要**<br>- 临时 URL 有效期48小时，过期后无法使用， **请勿用于生产环境。**<br>  <br>- 文件上传凭证接口限流为 100 QPS 且不支持扩容， **请勿用于生产环境、高并发及压测场景。**<br>  <br>- 生产环境建议使用 [阿里云OSS](https://help.aliyun.com/zh/oss/user-guide/what-is-oss "") 等稳定存储，确保文件长期可用并规避限流问题。 |
| channel\_id | array\[int\] | \[0\] | 否 | 指定在多音轨文件中需要进行语音识别的音轨索引，以List的形式给出，例如`[0]`表示仅识别第一条音轨，`[0, 1]`表示同时识别前两条音轨。 |
| disfluency\_removal\_enabled | boolean | false | 否 | 过滤语气词，默认关闭。 |
| language\_hints | array\[string\] | \["auto"\] | 否 | 指定识别语音中语言代码。SenseVoice只支持配置一个语种。默认使用“auto”自动检测语种。支持的语言代码请参见 [语言列表](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#66ac0678d6b4w "")。 |

### **响应参数**

**点击查看响应示例**

```json
{
  "output": {
    "task_status": "PENDING",
    "task_id": "c2e5d63b-96e1-4607-bb91-************"
  },
  "request_id": "77ae55ae-be17-97b8-9942--************"
}
```

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| task\_status | string | 任务状态。 |
| task\_id | string | 任务ID。 |

## **查询任务接口**

### **基本信息**

|     |     |
| --- | --- |
| **接口描述** | 查询语音识别任务执行情况和结果。 |
| **URL** | ```http<br>https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}<br>``` |
| **请求方法** | POST |
| **请求头** | ```http<br>Authorization: Bearer {api-key} // 需替换为您自己的API Key<br>``` |
| **消息体** | 无。 |

### **请求参数**

**点击查看请求示例**

```curl
curl --location 'https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}' --header "Authorization: Bearer $DASHSCOPE_API_KEY"
```

| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| task\_id | string | - | 是 | 查询任务需指定其ID，该ID为 [提交任务接口](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#418f2ac8ecxm4 "") 被调用后返回的`task_id`。 |

### **响应参数**

**点击查看响应示例**

当任务包含多个子任务时，只要存在任一子任务成功，整个任务状态将标记为`SUCCEEDED`，需通过`subtask_status`字段判断具体子任务结果。

正常示例

异常示例

```json
{
  "request_id": "f9e1afad-94d3-997e-a83b-************",
  "output": {
    "task_id": "f86ec806-4d73-485f-a24f-************",
    "task_status": "SUCCEEDED",
    "submit_time": "2024-09-12 15:11:40.041",
    "scheduled_time": "2024-09-12 15:11:40.071",
    "end_time": "2024-09-12 15:11:40.903",
    "results": [\
      {\
        "file_url":"https://xxx1.wav",\
        "transcription_url":"https://xxx1.json",\
        "subtask_status":"SUCCEEDED"\
      },\
      {\
        "file_url":"https://xxx2.wav",\
        "transcription_url":"https://xxx2.json",\
        "subtask_status":"SUCCEEDED"\
      }\
    ],
    "task_metrics": {
      "TOTAL": 2,
      "SUCCEEDED": 2,
      "FAILED": 0
    }
  },
  "usage": {
    "duration": 9
  }
}
```

“`code`”为错误码，“`message`”为错误信息，只有异常情况才有这两个字段，您可以通过这两个字段，对照 [错误码](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#1c165039e53bj "") 排查问题。

```json
{
    "task_id": "7bac899c-06ec-4a79-8875-xxxxxxxxxxxx",
    "task_status": "SUCCEEDED",
    "submit_time": "2024-12-16 16:30:59.170",
    "scheduled_time": "2024-12-16 16:30:59.204",
    "end_time": "2024-12-16 16:31:02.375",
    "results": [\
        {\
            "file_url":"https://xxx1.wav",\
            "transcription_url":"https://xxx1.json",\
            "subtask_status":"SUCCEEDED"\
        },\
        {\
            "file_url":"https://xxx1.wav",\
            "code": "InvalidFile.DownloadFailed",\
            "message": "The audio file cannot be downloaded.",\
            "subtask_status": "FAILED"\
        }\
    ],
    "task_metrics": {
        "TOTAL": 2,
        "SUCCEEDED": 1,
        "FAILED": 1
    }
}
```

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| task\_id | string | 被查询任务的ID。 |
| task\_status | string | 被查询任务的状态。<br>**说明**<br>当任务包含多个子任务时，只要存在任一子任务成功，整个任务状态将标记为`SUCCEEDED`，需通过`subtask_status`字段判断具体子任务结果。 |
| subtask\_status | string | 子任务状态。 |
| file\_url | string | 语音识别任务中所处理的文件URL。 |
| transcription\_url | string | 获取识别结果对应的链接。该链接有效期为24小时，超时后无法查询任务或通过先前查询结果中的URL下载结果。<br>识别结果保存为JSON文件，您可以通过上述链接下载该文件或直接通过HTTP请求读取该文件中的内容。<br>JSON数据中各字段含义请参见 [识别结果说明](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api#a9021178ccl7s "")。 |

### 识别结果说明

识别结果保存为JSON文件。

点击查看识别结果示例

```json
{
  "file_url": "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/sensevoice/rich_text_example_1.wav",
  "properties": {
    "audio_format": "pcm_s16le",
    "channels": [\
      0\
    ],
    "original_sampling_rate": 16000,
    "original_duration_in_milliseconds": 17645
  },
  "transcripts": [\
    {\
      "channel_id": 0,\
      "content_duration_in_milliseconds": 13240,\
      "text": "\u003c|Speech|\u003e Senior staff, principal doris jackson, wakefield faculty, and of course, my fellow classmates. \u003c|/Speech|\u003e \u003c|NEUTRAL|\u003e\u003c|Applause|\u003e \u003c|Speech|\u003e I am honored \u003c|/Applause|\u003e to have been chosen to speak before my classmates, as well as the students across America today. \u003c|/Speech|\u003e",\
      "sentences": [\
        {\
          "begin_time": 0,\
          "end_time": 7480,\
          "text": "\u003c|Speech|\u003e Senior staff, principal doris jackson, wakefield faculty, and of course, my fellow classmates. \u003c|/Speech|\u003e \u003c|NEUTRAL|\u003e"\
        },\
        {\
          "begin_time": 11880,\
          "end_time": 17640,\
          "text": "\u003c|Applause|\u003e \u003c|Speech|\u003e I am honored \u003c|/Applause|\u003e to have been chosen to speak before my classmates, as well as the students across America today. \u003c|/Speech|\u003e"\
        }\
      ]\
    }\
  ]
}
```

需要关注的参数如下：

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| audio\_format | string | 源文件中音频的格式。 |
| channels | array\[integer\] | 源文件中音频的音轨索引信息，对单轨音频返回\[0\]，对双轨音频返回\[0, 1\]，以此类推。 |
| original\_sampling\_rate | integer | 源文件中音频的采样率（Hz）。 |
| original\_duration\_in\_milliseconds | integer | 源文件中的原始音频时长（ms）。 |
| channel\_id | integer | 识别结果的音轨索引，以0为起始。 |
| content\_duration\_in\_milliseconds | integer | 音轨中被判定为语音内容的时长（ms）。<br>**重要**<br>SenseVoice服务根据音频中AI识别出的有效语音时长计费，非语音段落（如静默、背景音）不计费。由于技术限制，系统判定的语音时段可能与实际存在细微差异，计费结果以服务端数据为准。 |
| transcript | string | 段落级别的语音识别结果。 |
| sentences | array | 句子级别的语音识别结果。 |
| begin\_time | integer | 开始时间戳（ms）。 |
| end\_time | integer | 结束时间戳（ms）。 |
| text | string | 语音识别结果。<br>**说明**<br>- **支持4种情绪的情感识别**：生气（ANGRY）、高兴（HAPPY）、伤心（SAD）和中性（NEUTRAL）。<br>  <br>若识别结果中未出现上述情感，或返回结果中包含“`|SPECIAL_TOKEN_1|`”，代表该语音中未检测到特定情绪。<br>  <br>情感一般出现在识别结果最末端，例如：“`今天天气好棒啊！|HAPPY|`”。<br>  <br>- **音频事件检测**：支持4种常见音频事件识别，包括掌声（Applause）、背景音乐（BGM）、笑声（Laughter）和人声（Speech）。<br>  <br>音频事件通过起始符（格式为“`|事件类型|`”，例如“`|Applause|`”）和结束符（格式为“`|/事件类型|`”，例如“`|/Applause|`”）标记。例如：“`|Applause|今天|/Applause|天气好棒啊！`”表示在说“今天”这两个字的时候有掌声存在。 |

## **完整示例**

您可以使用编程语言自带的HTTP类库，来实现提交和查询任务的请求：先调用提交任务接口开启任务，然后循环调用查询任务接口，直至任务完成。

以Python为例，代码如下：

```python
import requests
import json
import os
import time

# 若没有配置环境变量，请将下行替换为：api_key="your-api-key"。your-api-key为您实际的API Key
api_key = os.getenv("DASHSCOPE_API_KEY")
file_urls = [\
    "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/sensevoice/rich_text_example_1.wav"\
]
language_hints = ["en"]

# 提交语音识别任务，包含待识别文件url列表
def submit_task(api_key, file_urls) -> str:

    headers = {
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json",
        "X-DashScope-Async": "enable",
    }

    data = {
        "model": "sensevoice-v1",
        "input": {"file_urls": file_urls},
        "parameters": {
            "channel_id": [0],
            "language_hints": language_hints,
        },
    }
    # 录音文件识别服务url
    service_url = (
        "https://dashscope.aliyuncs.com/api/v1/services/audio/asr/transcription"
    )
    response = requests.post(
        service_url, headers=headers, data=json.dumps(data)
    )

    # 打印响应内容
    if response.status_code == 200:
        return response.json()["output"]["task_id"]
    else:
        print("task failed!")
        print(response.json())
        return None

# 循环查询任务状态直到成功
def wait_for_complete(task_id):
    headers = {
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json",
        "X-DashScope-Async": "enable",
    }

    pending = True
    while pending:
        # 查询任务状态服务url
        service_url = f"https://dashscope.aliyuncs.com/api/v1/tasks/{task_id}"
        response = requests.post(
            service_url, headers=headers
        )
        if response.status_code == 200:
            status = response.json()['output']['task_status']
            if status == 'SUCCEEDED':
                print("task succeeded!")
                pending = False
                return response.json()['output']['results']
            elif status == 'RUNNING' or status == 'PENDING':
                pass
            else:
                print("task failed!")
                pending = False
        else:
            print("query failed!")
            pending = False
        print(response.json())
        time.sleep(0.1)

task_id = submit_task(api_key=api_key, file_urls=file_urls)
print("task_id: ", task_id)
result = wait_for_complete(task_id)
print("transcription result: ", result)
```

## **错误码**

| **错误代码 Code** | **错误信息Message（具体信息内容可能跟随场景有所变化）** | **含义说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误代码 Code** | **错误信息Message（具体信息内容可能跟随场景有所变化）** | **含义说明** |
| InvalidFile.DecodeFailed | The audio file cannot be decoded. | 无法解码文件。请检查文件编码是否正确，并确认文件为正确的音频格式。 |

更多阿里云百炼平台相关错误码请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "")。

## **更多示例**

更多示例，请参见 [GitHub](https://github.com/aliyun/alibabacloud-bailian-speech-demo)。

## **常见问题**

请参见GitHub [QA](https://github.com/aliyun/alibabacloud-bailian-speech-demo/tree/master/docs/QA)。

## **语言列表**

Sensevoice支持如下50多种语言，其中top10为重点支持语言。可通过查询下表获取语言代码并配置`language_hints`参数以获得更佳的效果，默认支持中文和英文。

| **语言** | **语言代码** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **语言** | **语言代码** |
| **重点语言** | **中文（Chinese）** | **zh** |
| **英文（English）** | **en** |
| **粤语（Cantonese）** | **yue** |
| **日语（Japanese）** | **ja** |
| **韩语（Korean）** | **ko** |
| **俄语（Russian）** | **ru** |
| **法语（French）** | **fr** |
| **意大利语（Italian）** | **it** |
| **德语（German）** | **de** |
| **西班牙语（Spanish）** | **es** |
| 更多语言 | 加泰罗尼亚语（Catalan） | ca |
| 印度尼西亚语（Indonesian） | id |
| 泰语（Thai） | th |
| 荷兰语（Dutch） | nl |
| 葡萄牙语（Portuguese） | pt |
| 捷克语（Czech） | cs |
| 波兰语（Polish） | pl |
| 希腊语（Greek） | el |
| 马来语（Malay） | ms |
| 塔加洛语（Tagalog） | tl |
| 保加利亚语（Bulgarian） | bg |
| 克罗地亚语（Croatian） | hr |
| 丹麦语（Danish） | da |
| 土耳其语（Turkish） | tr |
| 越南语（Vietnamese） | vi |
| 希伯来语（Hebrew ） | he |
| 匈牙利语（Hungarian） | hu |
| 乌克兰语（Ukrainian） | uk |
| 爪哇语（Javanese） | jw |
| 乌兹别克语（Uzbek） | uz |
| 挪威（Norwegian） | no |
| 罗马尼亚（Romanian） | ro |
| 瑞典语（Swedish） | sv |
| 波斯语（Persian） | fa |
| 泰米尔语（Tamil） | ta |
| 阿塞拜疆语（Azerbaijani） | az |
| 孟加拉语（Bengali） | bn |
| 缅甸语（Myanmar） | my |
| 高棉语（Khmer ） | km |
| 印地语（Hindi） | hi |
| 卡纳达语（Kannada ） | kn |
| 老挝语（Lao） | lo |
| 马拉雅拉姆语（Malayalam） | ml |
| 马拉地语（Marathi） | mr |
| 蒙古语（Mongolian） | mn |
| 尼泊尔语（Nepali） | ne |
| 旁遮普语（Punjabi ） | pa |
| 僧伽罗语（Sinhala） | si |
| 斯瓦希里语（Swahili） | sw |
| 泰卢固语（Telugu） | te |
| 乌尔都语（Urdu） | ur |
| 豪萨语（Hausa） | ha |