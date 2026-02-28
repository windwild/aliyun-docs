### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音识别](https://help.aliyun.com/zh/model-studio/speech-recognition-api-reference/)[录音文件识别（SenseVoice）- 即将下线](https://help.aliyun.com/zh/model-studio/sensevoice-speech-recognition/)Python SDK

# SenseVoice录音语音识别Python SDK

更新时间：2026-02-11 02:30:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Java SDK](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-java-sdk)[下一篇：RESTful API](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-restful-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

模型列表

约束

调用模式

异步提交任务+同步等待任务结束

异步提交任务+异步查询任务执行结果

请求参数

响应结果

TranscriptionResponse

TranscriptionOutput

识别结果说明

关键接口

核心类（Transcription）

错误码

更多示例

常见问题

语言列表

**警告**

**SenseVoice 服务即将下线**：SenseVoice 录音文件识别服务即将下线，为避免影响业务，请尽快迁移至其他语音识别服务（ [录音文件识别-Paraformer/Fun-ASR](https://help.aliyun.com/zh/model-studio/recording-file-recognition "")、 [录音文件识别-千问](https://help.aliyun.com/zh/model-studio/qwen-speech-recognition "")）。

本文介绍SenseVoice录音文件识别Python SDK的使用。

**用户指南：** 关于模型介绍和选型建议请参见 [录音文件识别-Fun-ASR/Paraformer/SenseVoice](https://help.aliyun.com/zh/model-studio/recording-file-recognition "")。

## **前提条件**

- 已开通服务并 [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")。请 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")，而非硬编码在代码中，防范因代码泄露导致的安全风险。

- [安装最新版DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


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

详情请参见 [语言列表](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#66ac0678d6b4w "")。



**重要**





SenseVoice每次只支持识别一种语言，请勿在`language_hints`参数中指定多个语言代码。


## **调用模式**

[核心类（Transcription）](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#adcb5e9bddbyq "") 提供了异步提交任务、同步等待任务结束和异步查询任务执行结果的接口。可通过如下两种调用模式进行录音文件识别：

- 异步提交任务+同步等待任务结束：提交任务后，阻塞当前线程直到任务结束并获取识别结果。

- 异步提交任务+异步查询任务执行结果：提交任务后，在需要的时候通过调用查询任务接口获取任务的执行结果。


### **异步提交任务+同步等待任务结束**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3105970771/CAEQURiBgMCvo5zjpxkiIDQyNzUwZjVjMWM3MjQ5Nzg4ODBjNDRjNzE1ZGFiOGFj4709861_20241015153444.149.svg)

1. 调用 [核心类（Transcription）](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#adcb5e9bddbyq "") 的`async_call`方法并设置 [请求参数](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#b7aea1f7fdsq4 "")。



**说明**





   - 语音识别服务对通过API提交的任务采取尽力服务原则进行处理。任务提交后将进入排队（`PENDING`）状态，排队时间取决于队列长度和文件时长，无法明确给出，通常在数分钟内。任务开始处理后，语音识别将以数百倍加速完成。

   - 每一个任务完成后，识别结果和URL下载链接有效期为24小时，超时后无法获取任务状态或通过原有URL下载结果。


2. 调用 [核心类（Transcription）](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#adcb5e9bddbyq "") 的`wait`方法同步等待任务结束。

任务的状态包括`PENDING`、`RUNNING`、`SUCCEEDED`和`FAILED`。当任务处于`PENDING`或`RUNNING`状态时，`wait`方法将被阻塞。当任务处于`SUCCEEDED`或`FAILED`状态时，`wait`方法不再阻塞并返回任务的执行结果。

`wait`方法返回 [TranscriptionResponse](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#c4fe4e43ee4n6 "")。


点击查看完整示例

```python
# For prerequisites running the following sample, visit https://help.aliyun.com/document_detail/611472.html

from http import HTTPStatus
import dashscope
import json

# 若未配置环境变量，取消下一行的注释并将your-api-key替换成您自己的API Key
# dashscope.api_key = 'your-api-key'

task_response = dashscope.audio.asr.Transcription.async_call(
    model='sensevoice-v1',
    file_urls=['https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/sensevoice/rich_text_example_1.wav'],
    language_hints=['en'],
)

transcribe_response = dashscope.audio.asr.Transcription.wait(task=task_response.output.task_id)
if transcribe_response.status_code == HTTPStatus.OK:
    print(json.dumps(transcribe_response.output, indent=4, ensure_ascii=False))
    print('transcription done!')
```

### **异步提交任务+异步查询任务执行结果**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3105970771/CAEQURiBgMCN3qzkpxkiIGE0YmU4YTdjMWNiNzRmYjJhMjFlMWZkZmFmOWQ1NmEx4709861_20241015153444.149.svg)

1. 调用 [核心类（Transcription）](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#adcb5e9bddbyq "") 的`async_call`方法并设置 [请求参数](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#b7aea1f7fdsq4 "")。



**说明**





   - 语音识别服务对通过API提交的任务采取尽力服务原则进行处理。任务提交后将进入排队（`PENDING`）状态，排队时间取决于队列长度和文件时长，无法明确给出，通常在数分钟内。任务开始处理后，语音识别将以数百倍加速完成。

   - 每一个任务完成后，识别结果和URL下载链接有效期为24小时，超时后无法获取任务状态或通过原有URL下载结果。


2. 循环调用 [核心类（Transcription）](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#adcb5e9bddbyq "") 的`fetch`方法同步等待任务结束。

当任务状态为`SUCCEEDED`或`FAILED`时，停止轮询并处理结果。

`fetch`方法返回 [TranscriptionResponse](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#c4fe4e43ee4n6 "")。


点击查看完整示例

```python
# For prerequisites running the following sample, visit https://help.aliyun.com/document_detail/611472.html

from http import HTTPStatus
from dashscope.audio.asr import Transcription
import json

# 若未配置环境变量，取消下一行的注释并将your-api-key替换成您自己的API Key
# import dashscope
# dashscope.api_key = 'your-api-key'

transcribe_response = Transcription.async_call(
    model='sensevoice-v1',
    file_urls=['https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/sensevoice/rich_text_example_1.wav'],
    language_hints=['en'],
)

while True:
    if transcribe_response.output.task_status == 'SUCCEEDED' or transcribe_response.output.task_status == 'FAILED':
        break
    transcribe_response = Transcription.fetch(task=transcribe_response.output.task_id)

if transcribe_response.status_code == HTTPStatus.OK:
    print(json.dumps(transcribe_response.output, indent=4, ensure_ascii=False))
    print('transcription done!')
```

## **请求参数**

请求参数通过 [核心类（Transcription）](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#adcb5e9bddbyq "") 的`async_call`方法进行设置。

| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| model | str | - | 是 | 指定模型名。固定为`sensevoice-v1` **。** |
| file\_urls | list\[str\] | - | 是 | 待识别音/视频文件的URL列表，支持HTTP / HTTPS协议，单次请求最多支持100个URL。<br>若录音文件存储在阿里云OSS，使用SDK方式不支持使用以 oss://为前缀的临时 URL。 |
| channel\_id | list\[int\] | \[0\] | 否 | 指定在多音轨文件中需要进行语音识别的音轨索引，以List的形式给出，例如`[0]`表示仅识别第一条音轨，`[0, 1]`表示同时识别前两条音轨。 |
| disfluency\_removal\_enabled | bool | False | 否 | 过滤语气词，默认关闭。 |
| language\_hints | list\[str\] | \["auto"\] | 否 | 指定识别语音中语言代码。SenseVoice只支持配置一个语种。默认使用“auto”自动检测语种。支持的语言代码请参见 [语言列表](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#66ac0678d6b4w "")。 |

## **响应结果**

### `TranscriptionResponse`

`TranscriptionResponse`封装了任务的基本信息（`task_id`和`task_status`）和执行结果（`output`属性对应的内容，参见 [TranscriptionOutput](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#3c2916848c07k "")）。

点击查看`TranscriptionResponse`结构示例

PENDING状态

RUNNING状态

SUCCEEDED状态

FAILED状态

```json
{
    "status_code":200,
    "request_id":"251aceab-a6aa-9fc4-b7f7-0cc6d3e2a9f3",
    "code":null,
    "message":"",
    "output":{
        "task_id":"7d0a58a3-1dbe-4de9-8cff-5f48213128b0",
        "task_status":"PENDING",
        "submit_time":"2025-02-13 16:55:08.573",
        "scheduled_time":"2025-02-13 16:55:08.592",
        "task_metrics":{
            "TOTAL":2,
            "SUCCEEDED":0,
            "FAILED":0
        }
    },
    "usage":null
}
```

```json
{
    "status_code":200,
    "request_id":"d9d530f1-853c-9848-a5f1-f5de59086ff7",
    "code":null,
    "message":"",
    "output":{
        "task_id":"6351feef-9694-45d2-9d32-63454f2ffb8d",
        "task_status":"RUNNING",
        "submit_time":"2025-02-13 17:31:20.681",
        "scheduled_time":"2025-02-13 17:31:20.703",
        "task_metrics":{
            "TOTAL":2,
            "SUCCEEDED":1,
            "FAILED":0
        }
    },
    "usage":null
}
```

```json
{
    "status_code":200,
    "request_id":"16668704-6702-9e03-8ab7-a32a5d7bb095",
    "code":null,
    "message":"",
    "output":{
        "task_id":"6351feef-9694-45d2-9d32-63454f2ffb8d",
        "task_status":"SUCCEEDED",
        "submit_time":"2025-02-13 17:31:20.681",
        "scheduled_time":"2025-02-13 17:31:20.703",
        "end_time":"2025-02-13 17:31:21.867",
        "results":[\
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
        "task_metrics":{
            "TOTAL":2,
            "SUCCEEDED":2,
            "FAILED":0
        }
    },
    "usage":{
        "duration":9
    }
}
```

```json
{
    "status_code":200,
    "request_id":"16668704-6702-9e03-8ab7-a32a5d7bb095",
    "code":null,
    "message":"",
    "output":{
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
                "file_url":"https://xxx2.wav",\
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
    },
    "usage":{
        "duration":9
    }
}
```

需要关注的参数如下：

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| status\_code | HTTP请求状态码。 |
| code | - 最外层的`code`无需关注。<br>  <br>- `output.results`下面的`code`，代表错误码。可以结合`message`字段，对照 [错误码](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#1c165039e53bj "") 排查问题。 |
| message | - 最外层的`message`无需关注。<br>  <br>- `output.results`下面的`message`，代表错误信息。可以结合`code`字段，对照 [错误码](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#1c165039e53bj "") 排查问题。 |
| task\_id | 任务ID。 |
| task\_status | 任务状态。<br>有`PENDING`、`RUNNING`、`SUCCEEDED`和`FAILED`这四种状态。<br>当任务包含多个子任务时，只要存在任一子任务成功，整个任务状态将标记为`SUCCEEDED`，需通过`subtask_status`字段判断具体子任务结果。 |
| results | 子任务识别结果。 |
| subtask\_status | 子任务状态。<br>有`PENDING`、`RUNNING`、`SUCCEEDED`和`FAILED`这四种状态。 |
| file\_url | 被识别音频的URL。 |
| transcription\_url | 音频识别结果对应的URL。<br>识别结果保存为JSON文件，您可以通过`transcription_url`对应的链接下载文件或直接通过HTTP请求读取该文件中的内容。JSON文件的内容请参见 [识别结果说明](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#a9021178ccl7s "")。 |

### `TranscriptionOutput`

`TranscriptionOutput`对应 [TranscriptionResponse](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#c4fe4e43ee4n6 "") 的`output`属性，代表当前任务执行结果。

点击查看`TranscriptionOutput`结构示例

PENDING状态

RUNNING状态

SUCCEEDED状态

FAILED状态

```json
{
    "task_id":"f2f7c2fa-0cd9-4bb2-a283-27b26ee4bb67",
    "task_status":"PENDING",
    "submit_time":"2025-02-13 17:59:27.754",
    "scheduled_time":"2025-02-13 17:59:27.789",
    "task_metrics":{
        "TOTAL":2,
        "SUCCEEDED":0,
        "FAILED":0
    }
}
```

```json
{
    "task_id":"f2f7c2fa-0cd9-4bb2-a283-27b26ee4bb67",
    "task_status":"RUNNING",
    "submit_time":"2025-02-13 17:59:27.754",
    "scheduled_time":"2025-02-13 17:59:27.789",
    "task_metrics":{
        "TOTAL":2,
        "SUCCEEDED":0,
        "FAILED":0
    }
}
```

```json
{
    "task_id":"f2f7c2fa-0cd9-4bb2-a283-27b26ee4bb67",
    "task_status":"SUCCEEDED",
    "submit_time":"2025-02-13 17:59:27.754",
    "scheduled_time":"2025-02-13 17:59:27.789",
    "end_time":"2025-02-13 17:59:28.828",
    "results":[\
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
    "task_metrics":{
        "TOTAL":2,
        "SUCCEEDED":2,
        "FAILED":0
    }
}
```

“`code`”为错误码，“`message`”为错误信息，只有异常情况才有这两个字段，您可以通过这两个字段，对照 [错误码](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#1c165039e53bj "") 排查问题。

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
            "file_url": "https://xxx2.wav",\
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

需要关注的参数如下：

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| code | 代表错误码。可以结合`message`字段，对照 [错误码](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#1c165039e53bj "") 排查问题。 |
| message | 代表错误信息。可以结合`code`字段，对照 [错误码](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#1c165039e53bj "") 排查问题。 |
| task\_id | 任务ID。 |
| task\_status | 任务状态。<br>有`PENDING`、`RUNNING`、`SUCCEEDED`和`FAILED`这四种状态。<br>当任务包含多个子任务时，只要存在任一子任务成功，整个任务状态将标记为`SUCCEEDED`，需通过`subtask_status`字段判断具体子任务结果。 |
| results | 子任务识别结果。 |
| subtask\_status | 子任务状态。<br>有`PENDING`、`RUNNING`、`SUCCEEDED`和`FAILED`这四种状态。 |
| file\_url | 被识别音频的URL。 |
| transcription\_url | 音频识别结果对应的URL。<br>识别结果保存为JSON文件，您可以通过`transcription_url`对应的链接下载文件或直接通过HTTP请求读取该文件中的内容。JSON文件的内容请参见 [识别结果说明](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#a9021178ccl7s "")。 |

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

## **关键接口**

### 核心类（`Transcription`）

`Transcription`可以通过“`from dashscope.audio.asr import Transcription`”方式引入。

| **成员方法** | **方法签名** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **成员方法** | **方法签名** | **说明** |
| async\_call | ```python<br>@classmethod<br>def async_call(cls,<br>               model: str,<br>               file_urls: List[str],<br>               phrase_id: str = None,<br>               api_key: str = None,<br>               workspace: str = None,<br>               **kwargs) -> TranscriptionResponse<br>``` | 异步提交语音识别任务。 |
| wait | ```python<br>@classmethod<br>def wait(cls,<br>         task: Union[str, TranscriptionResponse],<br>         api_key: str = None,<br>         workspace: str = None,<br>         **kwargs) -> TranscriptionResponse<br>``` | 阻塞当前线程直到异步任务结束（任务状态为`SUCCEEDED`或`FAILED`）。<br>该方法返回 [TranscriptionResponse](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#c4fe4e43ee4n6 "")。 |
| fetch | ```python<br>@classmethod<br>def fetch(cls,<br>          task: Union[str, TranscriptionResponse],<br>          api_key: str = None,<br>          workspace: str = None,<br>          **kwargs) -> TranscriptionResponse<br>``` | 异步查询当前任务执行结果。<br>该方法返回 [TranscriptionResponse](https://help.aliyun.com/zh/model-studio/sensevoice-recorded-speech-recognition-python-sdk#c4fe4e43ee4n6 "")。 |

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