### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[百炼语音模型服务](https://help.aliyun.com/zh/isi/developer-reference/spirit-product-speech-model-service/)API详情

# API详情

更新时间：2024-12-25 21:28:32

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：计量计费](https://help.aliyun.com/zh/isi/developer-reference/metering-and-billing)[下一篇：最佳实践](https://help.aliyun.com/zh/isi/developer-reference/best-practices)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

模型概览

API参考

前提条件

音视频文件转写

dashscope.audio.asr.Transcribe.async\_call()

dashscope.audio.asr.Transcribe.wait()

dashscope.audio.asr.Transcribe.fetch()

音视频文件转写结果文件

状态码说明

## **概述**

Paraformer语音识别提供的文件转写API，能够对常见的音频或音视频文件进行语音识别，并将结果返回给调用者。

常见的音频或音视频文件一般采用16kHz及以上的采样率进行录制，可选择paraformer-v1模型进行中英文语音识别，或选择paraformer-MTL-v1模型对超过20种语言及中文方言进行语音识别。当明确知道需要识别的语音是中英文时，选择paraformer-v1模型的准确率通常会比paraformer-MTL-v1模型更高。电话录音一般采用8kHz进行录制，对这类文件应选择paraformer-8k-v1模型进行语音识别以获得更佳的效果。

Paraformer语音识别返回较为丰富的结果供调用者选择使用，包括全文级文字、句子级文字、词和时间戳等。模型默认进行标点符号预测和逆文本正则化。

由于音视频文件的尺寸通常较大，文件传输和语音识别处理均需要时间，文件转写API通过异步调用方式来提交任务。开发者需要通过查询接口，在文件转写完成后获得语音识别结果。文件转写API支持批处理，用户单次可以上传最多100个文件URL，待所有URL转写完成后，用户可以一次性获取全部转写结果。

**说明**

若您有合作需求或技术咨询，请 [提交工单](https://smartservice.console.aliyun.com/service/create-ticket)。

## **模型概览**

| **模型名** | **模型简介** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名** | **模型简介** |
| [paraformer-v1](https://modelscope.cn/models/damo/speech_paraformer-large_asr_nat-zh-cn-16k-common-vocab8404-pytorch/summary) | Paraformer中语音模型服务中英文语音识别模型，支持16kHz及以上采样率的音频或视频语音识别。 |
| paraformer-8k-v1 | Paraformer中语音模型服务中文语音识别模型，支持8kHz电话语音识别。 |
| paraformer-mtl-v1 | Paraformer中语音模型服务多语言语音识别模型，支持16kHz及以上采样率的音频或视频语音识别。<br>支持的语种/方言包括：中文普通话、中文方言（粤语、吴语、闽南语、东北话、甘肃话、贵州话、河南话、湖北话、湖南话、宁夏话、山西话、陕西话、山东话、四川话、天津话）、英语、日语、韩语、西班牙语、印尼语、法语、德语、意大利语、马来语。 |

## **API参考**

### **前提条件**

- 已开通服务并获得API-KEY。具体操作，请参见[获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "") 和 [配置API Key到环境变量](https://help.aliyun.com/zh/model-studio/configure-api-key-through-environment-variables "")。

- 已安装SDK。具体操作，请参见[安装SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


### **音视频文件转写**

通过 **model** 参数指定进行语音识别的具体模型，通过 **file\_urls** 参数指定需要进行语音识别的音视频文件，支持HTTP/HTTPS协议的URL。

**说明**

需要使用您的API-KEY替换示例中的`your-dashscope-api-key`，代码才能正常运行。

```python
# For prerequisites running the following sample, visit https://help.aliyun.com/document_detail/611472.html

import dashscope
import json

dashscope.api_key='your-dashscope-api-key'

task_response=dashscope.audio.asr.Transcription.async_call(
    model='paraformer-v1',
    file_urls=['https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/paraformer/hello_world_female.wav',\
    	'https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/paraformer/hello_world_male.wav']
    )

transcribe_response=dashscope.audio.asr.Transcription.wait(task=task_response.output.task_id)
print(json.dumps(transcribe_response.output, indent=4, ensure_ascii=False))
```

文件转写API采用异步调用方式，您需要谨慎处理任务提交、状态查询、获取结果的异步逻辑。

**说明**

文件转写服务对通过API提交的任务采取尽力服务原则进行处理。具体任务的排队等待时间取决于并发的队列长度和其它任务的文件时长，因而无法提供确切等待时间。通常情况下排队等待时间应小于数分钟。一旦结束排队进入处理状态，文件将被以数百倍的加速比进行语音识别。

API支持当前主流的音视频文件格式，包括：

.aac、.amr、.avi、.flac、.flv、.m4a、.mkv、.mov、.mp3、.mp4、.mpeg、.ogg、.opus、.wav、.webm、.wma和.wmv。

**说明**

由于音视频格式及其变种众多，技术上无法穷尽测试，API不能保证所有格式均能够被正确识别。请通过测试验证您所提供的文件能够获得正常的语音识别结果。

API支持通过 **file\_urls** 参数指定最多100个文件URL进行转写，其中，文件小于等于2 GB。

如果希望处理的文件超过了上述限制，可尝试对文件进行预处理以降低文件尺寸，更多有关文件预处理的信息，请参见 [预处理视频文件以提高文件转写效率](https://help.aliyun.com/zh/dashscope/best-practices)。

### **dashscope.audio.asr.Transcribe.async\_call()**

以异步调用的方式向文件转写服务提交一个任务，返回被提交任务的信息。

- 参数配置




| **参数** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **说明** |
| model | string | - | 指定用于音视频文件转写的Paraformer模型名，可以从paraformer-v1、paraformer-8k-v1、paraformer-MTL-v1中进行选择。关于如何进行模型选择，请参见 [模型概览](https://help.aliyun.com/zh/isi/developer-reference/api-details#9da9f32009ex4 "")。 |
| file\_urls | List\[string\] | - | 音视频文件转写的URL列表，支持HTTP / HTTPS协议，最多可支持100个文件URL。 |
| channel\_id（可选） | List\[int\] | \[0\] | 指定在多音轨文件中需要进行语音识别的音轨索引，以List的形式给出，例如 \[0\] 代表对第一条音轨进行识别、 \[0, 1\] 代表对第一和第二条音轨分别进行识别等。 |

- 返回结果示例















```json
{
      "status_code": 200,
      "request_id": "8c59f00c-7723-455e-922d-ac3a31838170",
      "code": "",
      "message": "",
      "output": {
          "task_id": "bd725f8f-f699-4962-bcad-38a9fc2bcd7c",
          "task_status": "PENDING"
      },
      "usage": null
}
```

- 返回参数说明




| **返回参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **返回参数** | **类型** | **说明** |
| code | int | 状态码，更多信息，请参见 [状态码说明](https://help.aliyun.com/zh/dashscope/return-status-code-description)。 |
| task\_id | string | 提交的异步任务的ID，该ID作为任务的全局唯一标识符将用于后续对任务状态的查询、结果获取等操作。 |


### **dashscope.audio.asr.Transcribe.wait()**

以阻塞的方式等待异步任务结束（即到达SUCCEEDED或FAILED状态），返回任务的状态和文件转写结果。异步任务的状态包括PENDI _NG_、RUNNING、SUCCEEDED、FAILED。当任务处于PENDING或RUNNING状态时，wait()调用将被阻塞。当任务处于SUCCEEDED或FAILED状态时，wait()调用将返回任务的状态和结果。

- 参数配置




| **参数** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **说明** |
| task | string | - | 在调用async\_call()提交任务时所返回的task\_id。 |

- 返回结果示例















```json
{
      "status_code": 200,
      "request_id": "548c1e4b-1383-4a48-b747-ff46382ffd9d",
      "code": null,
      "message": "",
      "output": {
          "task_id": "bd725f8f-f699-4962-bcad-38a9fc2bcd7c",
          "task_status": "SUCCEEDED",
          "results": [\
              {\
                  "file_url": "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/paraformer/hello_world_male.wav",\
                  "transcription_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/0cbf0acf/20230517/14%3A30/4545b696-08f6-4330-825e-c1a0c3f67eaf-1.json?Expires=1684391431&OSSAccessKeyId=LTAI***************4G8qL&Signature=1z8zxHVQqdmUKgxr2ldipyC6lOU%3D",\
                  "subtask_status": "SUCCEEDED"\
              },\
              {\
                  "file_url": "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/paraformer/hello_world_female.wav",\
                  "transcription_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/0cbf0acf/20230517/14%3A30/9e5c4e54-3612-47c3-a824-5eeeea3059ee-1.json?Expires=1684391431&OSSAccessKeyId=LTAI***************4G8qL&Signature=WlzLbAk0zaCVJ5SkATd6xNcEQQ0%3D",\
                  "subtask_status": "SUCCEEDED"\
              }\
          ]
      },
      "usage": {
          "duration": 8
      }
}
```

- 返回参数说明




| **返回参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **返回参数** | **类型** | **说明** |
| code | int | 源文件中音频的格式。 |
| task\_id | string | 被查询任务的ID。 |
| task\_status | string | 被查询任务的状态。 |
| file\_url | string | 文件转写任务中所处理的文件URL。 |
| status | string | 所处理文件的处理状态。 |
| transcription\_url | string | 所处理文件的处理结果URL。 |


### **dashscope.audio.asr.Transcribe.fetch()**

查询异步任务，返回任务的状态和文件转写结果。异步任务的状态包括PENDING、RUNNING、SUCCEEDED、FAILED。不同于wait()，fetch()调用不会阻塞，将立即返回所查询任务的状态和结果。开发者可以编写代码，采用轮询的方式直到任务完成，再获取文件转写结果。

- 参数配置




| **参数** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **说明** |
| task | string | - | 在调用async\_call()提交任务时所返回的task\_id。 |

- 返回结果示例

  - PENDING、RUNNING状态















    ```json
        "status_code": 200,
        "request_id": "04ea046b-ccca-4765-882c-9f60bd985150",
        "code": null,
        "message": "",
        "output": {
            "task_id": "bd725f8f-f699-4962-bcad-38a9fc2bcd7c",
            "task_status": "RUNNING"
        },
        "usage": null
    }
    ```

  - SUCCEEDED状态















    ```json
    {
        "status_code": 200,
        "request_id": "548c1e4b-1383-4a48-b747-ff46382ffd9d",
        "code": null,
        "message": "",
        "output": {
            "task_id": "bd725f8f-f699-4962-bcad-38a9fc2bcd7c",
            "task_status": "SUCCEEDED",
            "results": [\
                {\
                    "file_url": "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/paraformer/hello_world_male.wav",\
                    "transcription_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/0cbf0acf/20230517/14%3A30/4545b696-08f6-4330-825e-c1a0c3f67eaf-1.json?Expires=1684391431&OSSAccessKeyId=LTAI***************4G8qL&Signature=1z8zxHVQqdmUKgxr2ldipyC6lOU%3D",\
                    "subtask_status": "SUCCEEDED"\
                },\
                {\
                    "file_url": "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/paraformer/hello_world_female.wav",\
                    "transcription_url": "https://dashscope-result-bj.oss-cn-beijing.aliyuncs.com/0cbf0acf/20230517/14%3A30/9e5c4e54-3612-47c3-a824-5eeeea3059ee-1.json?Expires=1684391431&OSSAccessKeyId=LTAI***************4G8qL&Signature=WlzLbAk0zaCVJ5SkATd6xNcEQQ0%3D",\
                    "subtask_status": "SUCCEEDED"\
                }\
            ]
        },
        "usage": {
            "duration": 8
        }
    }
    ```
- 返回参数说明




| **返回参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **返回参数** | **类型** | **说明** |
| code | int | 源文件中音频的格式。 |
| task\_id | string | 被查询任务的ID。 |
| task\_status | string | 被查询任务的状态。 |
| file\_url | string | 文件转写任务中所处理的文件URL。 |
| status | string | 所处理文件的处理状态。 |
| transcription\_url | string | 所处理文件的处理结果URL。 |


### **音视频文件转写结果文件**

当一个文件转写任务成功后，通过wait()或fetch()调用可获取文件转写的结果。这个结果同样以文件的形式保存，其链接以transcription\_url给出。开发者可以打开该URL以获取结果。

**说明**

异步任务文件转写结果文件URL的有效时间是24小时，从异步任务完成的时间开始计算。

- 返回结果示例















```json
{
      "file_url": "https://dashscope.oss-cn-beijing.aliyuncs.com/samples/audio/paraformer/hello_world_female.wav",
      "properties":
      {
          "audio_format": "pcm_s16le",
          "channels":
          [\
              0\
          ],
          "original_sampling_rate": 16000,
          "original_duration_in_milliseconds": 4087
      },
      "transcripts":
      [\
          {\
              "channel_id": 0,\
              "content_duration_in_milliseconds": 3780,\
              "text": "Hello world来自阿里巴巴达摩院语音实验室。",\
              "sentences":\
              [\
                  {\
                      "begin_time": 60,\
                      "end_time": 3840,\
                      "text": "Hello world来自阿里巴巴达摩院语音实验室。",\
                      "words":\
                      [\
                          {\
                              "begin_time": 60,\
                              "end_time": 780,\
                              "text": "Hello ",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 780,\
                              "end_time": 1320,\
                              "text": "world",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 1320,\
                              "end_time": 1500,\
                              "text": "来",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 1500,\
                              "end_time": 1720,\
                              "text": "自",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 1720,\
                              "end_time": 1860,\
                              "text": "阿",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 1860,\
                              "end_time": 2040,\
                              "text": "里",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 2040,\
                              "end_time": 2220,\
                              "text": "巴",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 2220,\
                              "end_time": 2460,\
                              "text": "巴",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 2460,\
                              "end_time": 2640,\
                              "text": "达",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 2640,\
                              "end_time": 2820,\
                              "text": "摩",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 2820,\
                              "end_time": 3000,\
                              "text": "院",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 3000,\
                              "end_time": 3220,\
                              "text": "语",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 3220,\
                              "end_time": 3400,\
                              "text": "音",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 3400,\
                              "end_time": 3580,\
                              "text": "实",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 3580,\
                              "end_time": 3720,\
                              "text": "验",\
                              "punctuation": ""\
                          },\
                          {\
                              "begin_time": 3720,\
                              "end_time": 3840,\
                              "text": "室",\
                              "punctuation": "。"\
                          }\
                      ]\
                  }\
              ]\
          }\
      ]
}
```

- 返回参数说明




| **返回参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **返回参数** | **类型** | **说明** |
| audio\_format | string | 源文件中音频的格式。 |
| channels | List\[int\] | 源文件中音频的音轨索引信息，对单轨音频返回\[0\]，对双轨音频返回\[0, 1\]，以此类推。 |
| original\_sampling\_rate | int | 源文件中音频的采样率（Hz）。 |
| original\_duration | int | 源文件中的原始音频时长（ms）。 |
| channel\_id | int | 表明转写结果的音轨索引，以0为起始。 |
| content\_duration | int | 音轨中被判定为语音内容的时长（ms）。<br>**重要**<br>Paraformer语音识别模型服务仅对音轨中被判定为语音内容的时长进行语音转写，并据此进行计量计费，非语音内容不计量、不计费。通常情况下语音内容时长会短于原始音频时长。由于对是否存在语音内容的判定是由AI模型给出的，可能与实际情况存在一定误差。 |
| transcript | string | 段落级别的语音转写结果。 |
| sentences | List\[\] | 句子级别的语音转写结果。 |
| words | List\[\] | 词级别的语音转写结果。 |
| begin\_time | int | 开始时间戳（ms）。 |
| end\_time | int | 结束时间戳（ms）。 |
| text | string | 语音转写结果。 |
| punctuation | string | 预测出的词之后的标点符号（如有）。 |


### **状态码说明**

百炼模型服务通用状态码，请参见 [错误码](https://help.aliyun.com/zh/model-studio/error-code "")。