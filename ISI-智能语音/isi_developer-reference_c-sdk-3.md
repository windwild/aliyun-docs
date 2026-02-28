### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/developer-reference/cosvoice-large-model-for-speech-synthesis/)[流式文本语音合成](https://help.aliyun.com/zh/isi/developer-reference/siso-text-to-speech-synthesis-for-cosyvoice/)C++ SDK

# C++ SDK

更新时间：2025-05-27 01:57:59

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

下载安装

SDK下载

SDK包文件说明

编译运行（Linux平台编译）

关键接口

基础接口

流式文本合成接口

代码示例

状态码

C++ SDK状态码

其他状态码

服务端响应状态码

本文介绍如何使用阿里云智能语音服务提供的C++ SDK，包括SDK的安装方法及SDK代码示例。

## 前提条件

- 阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/interface-description "")。

- 已获取项目Appkey，详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#2572188 "")。

- 已获取Access Token，详情请参见 [获取Token概述](https://help.aliyun.com/zh/isi/overview-of-obtaining-an-access-token#587dee8029x7r "")。


## 下载安装

### **SDK下载**

您可通过以下两种方法获取SDK。

- 方法一：从GitHub获取最新源码，详细编译和运行方式可见下文，或查看源码中的`readme.md`。















```shell
git clone --depth 1 https://github.com/aliyun/alibabacloud-nls-cpp-sdk
```

- 方法二：直接从下文表中选取需要的SDK包进行下载。其中SDK源码包为SDK原始代码，需要通过下文编译方法生成集成所需的库文件。其他对应平台的SDK包内含相关库文件、头文件，无需编译。




| **最新SDK包** | **平台** | **MD5** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **最新SDK包** | **平台** | **MD5** |
| [alibabacloud-nls-cpp-sdk3.2.1b-master\_1e2e874.zip](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241225/kpejrx/alibabacloud-nls-cpp-sdk3.2.1b-master_1e2e874.zip) | SDK源码 | e1d4f71f3db2e24fccd43f103573bea0 |
| [NlsCppSdk\_Linux-x86\_64\_3.2.1b\_1e2e874.tar.gz](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241225/txtfhu/NlsCppSdk_Linux-x86_64_3.2.1b_1e2e874.tar.gz) | Linux x86\_64 | 31f118233bd5b0fa2908989746aad284 |





**说明**





以上Linux-x86\_64版本使用gcc8.4.0 \_GLIBCXX\_USE\_CXX11\_ABI=0编译。可用源码包根据readme.md说明重新编译。



其中：



  - `alibabacloud-nls-cpp-sdk<version>-master_<github commit id>.zip`为SDK源码包。

  - `NlsCppSdk_<平台>_<版本号>_<github commit id>.tar.gz`为对应平台下开发需要的SDK包，详见内部readme.md。


### **SDK包文件说明**

- `scripts/build_linux.sh`：SDK源码中，以Linux平台为例的示例编译脚本。

- `CMakeLists.txt`：SDK源码中，以Linux/Android平台为例的示例代码工程`CMakeList`文件。

- demo目录：SDK包中，集成示例代码，以Linux平台为例，如下表所示。




| **文件名** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **文件名** | **描述** |
| speechRecognizerDemo.cpp | 一句话识别示例。 |
| speechSynthesizerDemo.cpp | 语音合成示例。 |
| speechTranscriberDemo.cpp | 实时语音识别示例。 |
| flowingSynthesizerDemo.cpp | 流式文本语音合成示例。 |
| fileTransferDemo.cpp | 录音文件识别示例。 |

- resource目录：SDK源码中，语音服务范例音频，可用于功能测试，如下表所示。




| **文件名** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **文件名** | **描述** |
| - test0.wav<br>    <br>  - test1.wav<br>    <br>  - test2.wav<br>    <br>  - test3.wav | 测试音频（16k采样频率、16bit采样位数的音频文件）。 |

- `include`：SDK源码中，SDK头文件，如下表所示。




| **文件名** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **文件名** | **描述** |
| nlsClient.h | SDK实例。 |
| nlsEvent.h | 回调事件说明。 |
| nlsGlobal.h | SDK全局头文件。 |
| nlsToken.h | SDK Access Token实例。 |
| iNlsRequest.h | NLS请求基础头文件。 |
| speechRecognizerRequest.h | 一句话识别。 |
| speechSynthesizerRequest.h | 语音合成、长文本语音合成。 |
| speechTranscriberRequest.h | 实时音频流识别。 |
| flowingSynthesizerRequest.h | 流式文本语音合成。 |
| FileTrans.h | 录音文件识别。 |

- `lib`：SDK库文件。

- `readme.md`：SDK说明。

- `release.log`：版本更新说明。

- `version`：版本号。


## 编译运行（Linux平台编译）

1. 安装工具的最低版本要求如下：

   - CMake 3.0

   - Glibc 2.5

   - Gcc 4.8.5
2. 在Linux终端运行如下脚本。

1. 进入SDK源码的根目录。

2. 生成SDK库文件和可执行程序： **srDemo**（一句话识别）、 **stDemo**（实时语音识别）、 **syDemo**（语音合成）、 **daDemo**（语音对话）、 **fsDemo**（流式文本语音合成）。















      ```shell
      ./scripts/build_linux.sh
      ```

3. 查看范例使用方式。















      ```shell
      cd build/demo
      ./fsDemo
      ```

## **关键接口**

### **基础接口**

- NlsClient：语音处理客户端，利用该客户端可以进行一句话识别、实时语音识别和语音合成的语音处理任务。该客户端为线程安全，建议全局仅创建一个实例。




| **接口名** | **启用版本** | **功能描述** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **接口名** | **启用版本** | **功能描述** |
| getInstance | 2.x | 获取（创建）`NlsClient`实例。 |
| setLogConfig | 2.x | 设置日志文件与存储路径。 |
| setDirectHost | 3.x | 跳过`DNS`域名解析直接设置服务器`IPV4`地址，若调用则需要在`startWorkThread`之前。 |
| setAddrInFamily | 3.1.12 | 设置套接口地址结构的类型，默认为`AF_INET`仅返回`IPV4`相关的地址信息，需要在`startWorkThread`之前调用。 |
| setUseSysGetAddrInfo | 3.1.13 | 若`libevent`的`DNS`无法满足，无法完成`DNS`，可调用此接口切换成系统的接口，需要在`startWorkThread`之前调用。 |
| calculateUtf8Chars | 3.1.14 | 统计文本内容字符数，需要传入`UTF-8`编码的文本内容，其中1个汉字、1个英文字母或1个标点均算作1个字符。 |
| setSyncCallTimeout | 3.1.17 | 设置同步调用模式的超时时间（ms）， 0则为关闭同步模式，默认0。此模式`start()`后收到服务端结果再return出去，`stop()`后收到`close()`回调再`return`出去。 |
| startWorkThread | 3.x | 启动工作线程数，默认1即启动一个线程，若-1则启动CPU核数的线程数。在高并发的情况下建议选择-1。可以理解NlsClient实例初始化，必须调用。 |
| getVersion | 3.x | 获取SDK版本号。 |
| releaseInstance | 2.x | 销毁`NlsClient`对象实例。 |
| createFlowingSynthesizerRequest | 3.2 | 创建流式文本语音合成对象，线程安全，支持高并发请求。 |
| releaseFlowingSynthesizerRequest | 3.2 | 销毁流式文本语音合成对象，需要在当前请求的closed事件后调用。 |

- NlsToken：创建Token对象，用于申请获取Token ID。申请新Token时需要先获取有效时间戳，若超过有效时间则再申请。若在有效时间内多次申请Token会导致Token ID错误而无法使用。




| **接口名** | **功能描述** |
| --- | --- |



|     |     |
| --- | --- |
| **接口名** | **功能描述** |
| setAccessKeyId | 设置阿里云账号AccessKey ID。 |
| setKeySecret | 设置阿里云账号AccessKey Secret。 |
| setDomain | 设置域名，非必填。 |
| setServerVersion | 设置API版本，非必填。 |
| setServerResourcePath | 设置服务路径，非必填。 |
| setRegionId | 设置服务的确ID，非必填。 |
| setAction | 设置功能，非必填。 |
| applyNlsToken | 申请获取Token ID。 |
| getToken | 获取Token ID。 |
| getExpireTime | 获取Token有效期时间戳（秒）。 |
| getErrorMsg | 获得错误信息 |

- NlsEvent：事件对象，您可以从中获取Request状态码、云端返回结果、失败信息等。




| **接口名** | **功能描述** |
| --- | --- |



|     |     |
| --- | --- |
| **接口名** | **功能描述** |
| getStatusCode | 获取状态码，正常情况为0或者20000000，失败时对应失败的错误码。 |
| getErrorMessage | 在`TaskFailed`回调中，获取`NlsRequest`操作过程中出现失败时的错误信息。 |
| getTaskId | 获取任务的`TaskId`。 |
| getBinaryData | 获取云端返回的二进制数据。 |
| getAllResponse | 获取云端返回的结果。 |


### **流式文本合成接口**

接口说明以`flowingSynthesizerRequest.h`内容为准。

| **接口名** | **启用版本** | **功能描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **接口名** | **启用版本** | **功能描述** |
| setOnSynthesisStarted | 3.2 | 设置流式文本语音合成启动回调函数。 |
| setOnSynthesisCompleted | 3.2 | 设置语音合成结束回调函数。 |
| setOnChannelClosed | 2.x | 设置通道关闭回调函数。 |
| setOnTaskFailed | 2.x | 设置错误回调函数。 |
| setOnSentenceBegin | 3.2 | 服务端检测到了一句话的开始的回调函数。 |
| setOnSentenceEnd | 3.2 | 服务端检测到了一句话的结束，返回该句的全量时间戳的回调函数。 |
| setOnBinaryDataReceived | 2.x | 设置语音合成二进制音频数据接收回调函数。 |
| setOnSentenceSynthesis | 3.2 | 增量返回语音合成的结果，包含最新的音频和时间戳、句内全量、句间增量的回调函数。 |
| setOnMessage | 3.1.16 | 设置服务端`response message`回调函数，所有回调从此回调输出由用户自行解析。非必填。设置后需`setEnableOnMessage`启动。 |
| setAppKey | 2.x | 设置AppKey。 |
| setToken | 2.x | 口令认证。所有的请求都必须通过`SetToken`方法认证通过，才可以使用。 |
| setUrl | 2.x | 设置服务URL地址。非必填。 |
| sendText | 3.2 | 在同一个流式TTS会话中，单次合成不超过5000字，总计不超过10万字，其中1个汉字、1个英文字母、1个标点或1个句子中间空格均算作1个字符。 |
| setVoice | 2.x | 发音人voice设置。 |
| setVolume | 2.x | 音量volume设置。 |
| setFormat | 2.x | 设置音频数据编码格式（默认是PCM，支持的格式：PCM、WAV、MP3）。 |
| setSampleRate | 2.x | 音频采样率设置。 |
| setSpeechRate | 2.x | 语速设置。 |
| setPitchRate | 2.x | 语调设置。 |
| setEnableSubtitle | 2.x | 是否开启字幕功能。 |
| setPayloadParam | 2.x | 参数设置，入参为JSON格式字符串。 |
| setTimeout | 2.x | 设置链接超时时间，默认5000ms。 |
| setContextParam | 2.x | 设置用户自定义参数，入参为JSON格式字符串。 |
| AppendHttpHeaderParam | 2.x | 设置用户自定义ws阶段`HTTP header`参数。 |
| setSendTimeout | 3.1.14 | 设置发送超时时间，默认5000ms。 |
| setEnableOnMessage | 3.1.16 | 设置开启服务器返回消息回调。 |
| getTaskId | 3.1.17 | 获得当前请求的`task_id`。 |
| start | 2.x | 启动`FlowingSynthesizerRequest`。 |
| stop | 3.2 | 结束合成任务，后续需要等待合成完毕。 |
| cancel | 2.x | 不会与服务端确认关闭，直接关闭语音合成过程。 |

## 代码示例

**说明**

- 示例中将合成的音频保存在文件中，如果您需要播放音频且对实时性要求较高，建议使用流式播放，即边接收语音数据边播放，减少延时，而无需等待合成结束后再处理语音流。

- 完整示例，参见SDK压缩包中demo目录的 **flowingSynthesizerRequest.cpp** 文件。

- 调用接口前，需配置环境变量，通过环境变量读取访问凭证。智能语音交互的`AccessKey ID`、`AccessKey Secret`和`AppKey`的环境变量名：`NLS_AK_ENV`、`NLS_SK_ENV`、`NLS_APPKEY_ENV` **。**


**代码示例**

```c
#include <errno.h>
#include <pthread.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/time.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <ctime>
#include <fstream>
#include <iostream>
#include <string>
#include <vector>

#include "nlsClient.h"
#include "nlsEvent.h"
#include "nlsToken.h"
#include "flowingSynthesizerRequest.h"

#define SAMPLE_RATE_16K 16000
#define DEFAULT_STRING_LEN 512
#define AUDIO_TEXT_LENGTH 2048

/**
 * 全局维护一个服务鉴权token和其对应的有效期时间戳，
 * 每次调用服务之前，首先判断token是否已经过期，
 * 如果已经过期，则根据AccessKey ID和AccessKey
 * Secret重新生成一个token，并更新这个全局的token和其有效期时间戳。
 *
 * 注意：不要每次调用服务之前都重新生成新token，只需在token即将过期时重新生成即可。所有的服务并发可共用一个token。
 */
// 自定义线程参数
struct ParamStruct {
  char text[AUDIO_TEXT_LENGTH];
  char token[DEFAULT_STRING_LEN];
  char appkey[DEFAULT_STRING_LEN];
  char url[DEFAULT_STRING_LEN];

  pthread_mutex_t mtx;
};

// 自定义事件回调参数
struct ParamCallBack {
 public:
  explicit ParamCallBack(ParamStruct* param) {
    tParam = param;
    pthread_mutex_init(&mtxWord, NULL);
    pthread_cond_init(&cvWord, NULL);
  };
  ~ParamCallBack() {
    tParam = NULL;
    pthread_mutex_destroy(&mtxWord);
    pthread_cond_destroy(&cvWord);
  };

  pthread_mutex_t mtxWord;
  pthread_cond_t cvWord;

  ParamStruct* tParam;
};

std::string g_appkey = "";
std::string g_akId = "";
std::string g_akSecret = "";
std::string g_token = "";
std::string g_url = "";
std::string g_voice = "xiaoyun";
int g_threads = 1;
bool g_save_audio = true;
std::string g_text = "";
std::string g_format = "wav";
long g_expireTime = -1;
static int sample_rate = SAMPLE_RATE_16K;
static bool enableSubtitle = false;

std::vector<std::string> splitString(
    const std::string& str, const std::vector<std::string>& delimiters) {
  std::vector<std::string> result;
  size_t startPos = 0;

  // 查找字符串中的每个分隔符
  while (startPos < str.length()) {
    size_t minPos = std::string::npos;
    size_t delimiterLength = 0;

    for (std::vector<std::string>::const_iterator it = delimiters.begin();
         it != delimiters.end(); ++it) {
      std::size_t position = str.find(*it, startPos);
      // 查找最近的分隔符
      if (position != std::string::npos &&
          (minPos == std::string::npos || position < minPos)) {
        minPos = position;
        delimiterLength = it->size();
      }
    }

    // 如果找到分隔符，则提取前面的字符串
    if (minPos != std::string::npos) {
      result.push_back(str.substr(startPos, minPos - startPos));
      startPos = minPos + delimiterLength;
    } else {
      // 没有更多分隔符，剩下的全部是一个部分
      result.push_back(str.substr(startPos));
      break;
    }
  }

  return result;
}

/**
 * 根据AccessKey ID和AccessKey Secret重新生成一个token，并获取其有效期时间戳
 */
int generateToken(std::string akId, std::string akSecret, std::string* token,
                  long* expireTime) {
  AlibabaNlsCommon::NlsToken nlsTokenRequest;
  nlsTokenRequest.setAccessKeyId(akId);
  nlsTokenRequest.setKeySecret(akSecret);

  int retCode = nlsTokenRequest.applyNlsToken();
  /*获取失败原因*/
  if (retCode < 0) {
    std::cout << "Failed error code: " << retCode
              << "  error msg: " << nlsTokenRequest.getErrorMsg() << std::endl;
    return retCode;
  }

  *token = nlsTokenRequest.getToken();
  *expireTime = nlsTokenRequest.getExpireTime();

  return 0;
}

void OnSynthesisStarted(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  std::cout << "OnSynthesisStarted:"
            << "  status code: " << cbEvent->getStatusCode()
            << "  task id: " << cbEvent->getTaskId()
            << "  all response:" << cbEvent->getAllResponse() << std::endl;
}

/**
 * @brief sdk在接收到云端返回合成结束消息时, sdk内部线程上报Completed事件
 * @note 上报Completed事件之后，SDK内部会关闭识别连接通道.
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void OnSynthesisCompleted(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  std::cout
      << "OnSynthesisCompleted: "
      << ", status code: "
      << cbEvent
             ->getStatusCode()  // 获取消息的状态码，成功为0或者20000000，失败时对应失败的错误码
      << ", task id: "
      << cbEvent->getTaskId()  // 当前任务的task id，方便定位问题，建议输出
      << std::endl;
  std::cout << "OnSynthesisCompleted: All response:"
            << cbEvent->getAllResponse()
            << std::endl;  // 获取服务端返回的全部信息
}

/**
 * @brief 合成过程发生异常时, sdk内部线程上报TaskFailed事件
 * @note 上报TaskFailed事件之后，SDK内部会关闭识别连接通道.
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void OnSynthesisTaskFailed(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  FILE* failed_stream = fopen("synthesisTaskFailed.log", "a+");
  if (failed_stream) {
    char outbuf[1024] = {0};
    snprintf(outbuf, sizeof(outbuf),
             "OnSynthesisTaskFailed status code:%d task id:%s error mesg:%s\n",
             cbEvent->getStatusCode(), cbEvent->getTaskId(),
             cbEvent->getErrorMessage());
    std::cout << outbuf << std::endl;
    fwrite(outbuf, strlen(outbuf), 1, failed_stream);
    fclose(failed_stream);
  }
}

/**
 * @brief 识别结束或发生异常时，会关闭连接通道,
 * sdk内部线程上报ChannelCloseed事件
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void OnSynthesisChannelClosed(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  ParamCallBack* tmpParam = static_cast<ParamCallBack*>(cbParam);
  if (tmpParam) {
    std::cout << "OnSynthesisChannelClosed: "
              << ", All response: " << cbEvent->getAllResponse()
              << std::endl;  // 获取服务端返回的全部信息
  }
}

/**
 * @brief 文本上报服务端之后, 收到服务端返回的二进制音频数据,
 * SDK内部线程通过BinaryDataRecved事件上报给用户
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 * @notice 此处切记不可做block操作,只可做音频数据转存. 若在此回调中做过多操作,
 *         会阻塞后续的数据回调和completed事件回调.
 */
void OnBinaryDataRecved(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  std::vector<unsigned char> data =
      cbEvent->getBinaryData();  // getBinaryData() 获取文本合成的二进制音频数据
  std::cout
      << "  OnBinaryDataRecved: status code: "
      << cbEvent
             ->getStatusCode()  // 获取消息的状态码，成功为0或者20000000，失败时对应失败的错误码
      << ", taskId: "
      << cbEvent->getTaskId()  // 当前任务的task id，方便定位问题，建议输出
      << ", data size: " << data.size()  // 数据的大小
      << std::endl;

  if (g_save_audio && data.size() > 0) {
    // 以追加形式将二进制音频数据写入文件
    std::string dir = "./tts_audio";
    if (access(dir.c_str(), 0) == -1) {
      mkdir(dir.c_str(), S_IRWXU);
    }
    char file_name[256] = {0};
    snprintf(file_name, 256, "%s/%s.%s", dir.c_str(), cbEvent->getTaskId(),
             g_format.c_str());
    FILE* tts_stream = fopen(file_name, "a+");
    if (tts_stream) {
      fwrite((char*)&data[0], data.size(), 1, tts_stream);
      fclose(tts_stream);
    }
  }
}

void OnSentenceBegin(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  std::cout
      << "OnSentenceBegin "
      << "Response: "
      << cbEvent
             ->getAllResponse()  // 获取消息的状态码，成功为0或者20000000，失败时对应失败的错误码
      << std::endl;
}

void OnSentenceEnd(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  std::cout
      << "OnSentenceEnd "
      << "Response: "
      << cbEvent
             ->getAllResponse()  // 获取消息的状态码，成功为0或者20000000，失败时对应失败的错误码
      << std::endl;
}

/**
 * @brief 返回 tts 文本对应的日志信息，增量返回对应的字幕信息
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void OnSentenceSynthesis(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  std::cout
      << "OnSentenceSynthesis "
      << "Response: "
      << cbEvent
             ->getAllResponse()  // 获取消息的状态码，成功为0或者20000000，失败时对应失败的错误码
      << std::endl;
}

/**
 * @brief 服务端返回的所有信息会通过此回调反馈,
 * @param cbEvent 回调事件结构, 详见nlsEvent.h
 * @param cbParam 回调自定义参数，默认为NULL, 可以根据需求自定义参数
 * @return
 */
void onMessage(AlibabaNls::NlsEvent* cbEvent, void* cbParam) {
  std::cout << "onMessage: All response:" << cbEvent->getAllResponse()
            << std::endl;
}

/**
 * @brief 短链接模式下工作线程
 *        以 createFlowingSynthesizerRequest   <----|
 *                   |                              |
 *           request->start()                       |
 *                   |                              |
 *           request->sendText()                    |
 *                   |                              |
 *           request->stop()                        |
 *                   |                              |
 *           收到OnSynthesisChannelClosed回调        |
 *                   |                              |
 *      releaseFlowingSynthesizerRequest(request) --|
 *        进行循环。
 */
void* pthreadFunc(void* arg) {
  int testCount = 0;  // 运行次数计数，用于超过设置的loop次数后退出
  bool timedwait_flag = false;

  // 从自定义线程参数中获取token, 配置文件等参数.
  ParamStruct* tst = static_cast<ParamStruct*>(arg);
  if (tst == NULL) {
    std::cout << "arg is not valid." << std::endl;
    return NULL;
  }

  pthread_mutex_init(&(tst->mtx), NULL);

  // 初始化自定义回调参数
  ParamCallBack cbParam(tst);

  /*
   * 1. 创建流式文本语音合成FlowingSynthesizerRequest对象.
   *
   * 流式文本语音合成文档详见:
   * https://help.aliyun.com/zh/isi/developer-reference/streaming-text-to-speech-synthesis/
   */

  AlibabaNls::FlowingSynthesizerRequest* request =
      AlibabaNls::NlsClient::getInstance()->createFlowingSynthesizerRequest();
  if (request == NULL) {
    std::cout << "createFlowingSynthesizerRequest failed." << std::endl;
    return NULL;
  }

  /*
   * 2. 设置用于接收结果的回调
   */
  // 设置音频合成可以开始的回调函数
  request->setOnSynthesisStarted(OnSynthesisStarted, &cbParam);
  // 设置音频合成结束回调函数
  request->setOnSynthesisCompleted(OnSynthesisCompleted, &cbParam);
  // 设置音频合成通道关闭回调函数
  request->setOnChannelClosed(OnSynthesisChannelClosed, &cbParam);
  // 设置异常失败回调函数
  request->setOnTaskFailed(OnSynthesisTaskFailed, &cbParam);
  // 设置文本音频数据接收回调函数
  request->setOnBinaryDataReceived(OnBinaryDataRecved, &cbParam);
  // 设置字幕信息
  request->setOnSentenceSynthesis(OnSentenceSynthesis, &cbParam);
  // 一句话开始
  request->setOnSentenceBegin(OnSentenceBegin, &cbParam);
  // 一句话结束
  request->setOnSentenceEnd(OnSentenceEnd, &cbParam);
  // 设置所有服务端返回信息回调函数
  // request->setOnMessage(onMessage, &cbParam);
  // 开启所有服务端返回信息回调函数, 其他回调(除了OnBinaryDataRecved)失效
  // request->setEnableOnMessage(true);

  /*
   * 3. 设置request的相关参数
   */
  // 发音人, 包含"xiaoyun", "ruoxi", "xiaogang"等. 可选参数, 默认是xiaoyun
  request->setVoice(g_voice.c_str());
  // 音量, 范围是0~100, 可选参数, 默认50
  request->setVolume(50);
  // 音频编码格式, 可选参数, 默认是wav. 支持的格式pcm, wav, mp3
  request->setFormat("wav");
  // 音频采样率, 包含8000, 16000. 可选参数, 默认是16000
  request->setSampleRate(sample_rate);
  // 语速, 范围是-500~500, 可选参数, 默认是0
  request->setSpeechRate(0);
  // 语调, 范围是-500~500, 可选参数, 默认是0
  request->setPitchRate(0);
  // 开启字幕
  request->setEnableSubtitle(enableSubtitle);

  // 设置AppKey, 必填参数, 请参照官网申请
  if (strlen(tst->appkey) > 0) {
    request->setAppKey(tst->appkey);
  }
  // 设置账号校验token, 必填参数
  if (strlen(tst->token) > 0) {
    request->setToken(tst->token);
  }

  if (strlen(tst->url) > 0) {
    request->setUrl(tst->url);
  }

  // 设置链接超时500ms
  // request->setTimeout(500);
  // 获取返回文本的编码格式
  // const char* output_format = request->getOutputFormat();
  // std::cout << "text format: " << output_format << std::endl;

  /*
   * 4.
   * start()为异步操作。成功则开始返回BinaryRecv事件。失败返回TaskFailed事件。
   */
  std::cout << "start -> pid " << pthread_self() << std::endl;
  struct timespec outtime;
  struct timeval now;
  int ret = request->start();
  testCount++;
  if (ret < 0) {
    std::cout << "start failed. pid:" << pthread_self() << std::endl;
    const char* request_info = request->dumpAllInfo();
    if (request_info) {
      std::cout << "  all info: " << request_info << std::endl;
    }
    AlibabaNls::NlsClient::getInstance()->releaseFlowingSynthesizerRequest(
        request);  // start()失败，释放request对象
    return NULL;
  } else {
    std::cout << "start success. pid " << pthread_self() << std::endl;
    /*
     * 等待started事件返回表示start()成功, 然后再发送音频数据。
     * 语音服务器存在来不及处理当前请求的情况, 10s内不返回任何回调的问题,
     * 然后在10s后返回一个TaskFailed回调, 所以需要设置一个超时机制。
     */
    std::cout << "wait started callback." << std::endl;
    gettimeofday(&now, NULL);
    outtime.tv_sec = now.tv_sec + 10;
    outtime.tv_nsec = now.tv_usec * 1000;
    pthread_mutex_lock(&(cbParam.mtxWord));
    if (ETIMEDOUT == pthread_cond_timedwait(&(cbParam.cvWord),
                                            &(cbParam.mtxWord), &outtime)) {
      std::cout << "start timeout" << std::endl;
      timedwait_flag = true;
      pthread_mutex_unlock(&(cbParam.mtxWord));
      // start()调用超时，cancel()取消当次请求。
      request->cancel();
      return NULL;
    }
    pthread_mutex_unlock(&(cbParam.mtxWord));
  }

  /*
   * 5. 模拟大模型流式返回文本结果，进行逐个语音合成
   */
  std::string text_str(tst->text);
  if (!text_str.empty()) {
    const char* delims[] = {"。", "！", "；", "？", "\n"};
    std::vector<std::string> delimiters(
        delims, delims + sizeof(delims) / sizeof(delims[0]));
    std::vector<std::string> sentences = splitString(text_str, delimiters);
    for (std::vector<std::string>::const_iterator it = sentences.begin();
         it != sentences.end(); ++it) {
      std::cout << "sendText: " << *it << std::endl;
      ret = request->sendText(it->c_str());
      if (ret < 0) {
        break;
      }
      usleep(500 * 1000);
    }  // for
    if (ret < 0) {
      std::cout << "sendText failed. pid:" << pthread_self() << std::endl;
      const char* request_info = request->dumpAllInfo();
      if (request_info) {
        std::cout << "  all info: " << request_info << std::endl;
      }
      AlibabaNls::NlsClient::getInstance()->releaseFlowingSynthesizerRequest(
          request);  // start()失败，释放request对象
      return NULL;
    }
  }

  /*
   * 6. start成功，开始等待接收完所有合成数据。
   *    stop()为无意义接口，调用与否都会跑完全程.
   *    cancel()立即停止工作, 且不会有回调返回, 失败返回TaskFailed事件。
   */
  //    ret = request->cancel();
  ret = request->stop();

  /*
   * 开始等待接收完所有合成数据。
   */
  if (ret == 0) {
    /*
     * 等待started事件返回表示start()成功, 然后再发送音频数据。
     * 语音服务器存在来不及处理当前请求的情况, 10s内不返回任何回调的问题,
     * 然后在10s后返回一个TaskFailed回调, 所以需要设置一个超时机制。
     */
    // 等待closed事件后再进行释放, 否则会出现崩溃
    std::cout << "wait closed callback." << std::endl;
    /*
     * 语音服务器存在来不及处理当前请求, 10s内不返回任何回调的问题,
     * 然后在10s后返回一个TaskFailed回调, 错误信息为:
     * "Gateway:IDLE_TIMEOUT:Websocket session is idle for too long time,
     * the last directive is 'XXXX'!" 所以需要设置一个超时机制.
     */
    gettimeofday(&now, NULL);
    outtime.tv_sec = now.tv_sec + 30;
    outtime.tv_nsec = now.tv_usec * 1000;
    // 等待closed事件后再进行释放, 否则会出现崩溃
    pthread_mutex_lock(&(cbParam.mtxWord));
    if (ETIMEDOUT == pthread_cond_timedwait(&(cbParam.cvWord),
                                            &(cbParam.mtxWord), &outtime)) {
      std::cout << "stop timeout" << std::endl;
      pthread_mutex_unlock(&(cbParam.mtxWord));
      return NULL;
    }
    pthread_mutex_unlock(&(cbParam.mtxWord));
  } else {
    std::cout << "ret is " << ret << ", pid " << pthread_self() << std::endl;
  }
  gettimeofday(&now, NULL);
  std::cout << "current request task_id:" << request->getTaskId() << std::endl;
  std::cout << "stop finished. pid " << pthread_self() << " tv: " << now.tv_sec
            << std::endl;

  /*
   * 7. 完成所有工作后释放当前请求。
   *    请在closed事件(确定完成所有工作)后再释放, 否则容易破坏内部状态机,
   * 会强制卸载正在运行的请求。
   */
  const char* request_info = request->dumpAllInfo();
  if (request_info) {
    std::cout << "  all info: " << request_info << std::endl;
  }
  AlibabaNls::NlsClient::getInstance()->releaseFlowingSynthesizerRequest(
      request);
  std::cout << "release Synthesizer success. pid " << pthread_self()
            << std::endl;

  pthread_mutex_destroy(&(tst->mtx));

  return NULL;
}

/**
 * 合成多个文本数据;
 * sdk多线程指一个文本数据对应一个线程, 非一个文本数据对应多个线程.
 * 示例代码为同时开启4个线程合成4个文件;
 * 免费用户并发连接不能超过2个;
 */
#define AUDIO_TEXT_NUMS 4
#define AUDIO_FILE_NAME_LENGTH 32
int flowingSynthesizerMultFile(const char* appkey, int threads) {
  /**
   * 获取当前系统时间戳，判断token是否过期
   */
  std::time_t curTime = std::time(0);
  if (g_token.empty()) {
    if (g_expireTime - curTime < 10) {
      std::cout << "the token will be expired, please generate new token by "
                   "AccessKey-ID and AccessKey-Secret."
                << std::endl;
      int ret = generateToken(g_akId, g_akSecret, &g_token, &g_expireTime);
      if (ret < 0) {
        std::cout << "generate token failed" << std::endl;
        return -1;
      } else {
        if (g_token.empty() || g_expireTime < 0) {
          std::cout << "generate empty token" << std::endl;
          return -2;
        }
        std::cout << "token: " << g_token << std::endl;
      }
    }
  }

  /* 不要超过AUDIO_TEXT_LENGTH */
  const char texts[AUDIO_TEXT_LENGTH] = {
      "唧唧复唧唧，木兰当户织。不闻机杼声，唯闻女叹息。问女何所思，问女何所忆。"
      "女亦无所思，女亦无所忆。昨夜见军帖，可汗大点兵。军书十二卷，卷卷有爷名。"
      "阿爷无大儿，木兰无长兄。愿为市鞍马，从此替爷征。东市买骏马，西市买鞍鞯，"
      "南市买辔头，北市买长鞭。旦辞爷娘去，暮宿黄河边。不闻爷娘唤女声，但闻黄河"
      "流水鸣溅溅。旦辞黄河去，暮至黑山头。不闻爷娘唤女声，但闻燕山胡骑鸣啾啾。"
      " 万里赴戎机，关山度若飞。朔气传金柝，寒光照铁衣。将军百战死，壮士十年归"
      "。 "
      "归来见天子，天子坐明堂。策勋十二转，赏赐百千强。可汗问所欲，木兰不用尚书"
      "郎，愿驰千里足，送儿还故乡。 "
      "爷娘闻女来，出郭相扶将；阿姊闻妹来，当户理红妆；小弟闻姊来，磨刀霍霍向猪"
      "羊。开我东阁门，坐我西阁床。脱我战时袍，著我旧时裳。当窗理云鬓，对镜帖花"
      "黄。出门看火伴，火伴皆惊忙：同行十二年，不知木兰是女郎。 "
      "雄兔脚扑朔，雌兔眼迷离；双兔傍地走，安能辨我是雄雌？"};

  ParamStruct pa[threads];

  for (int i = 0; i < threads; i++) {
    memset(pa[i].token, 0, DEFAULT_STRING_LEN);
    memcpy(pa[i].token, g_token.c_str(), g_token.length());

    memset(pa[i].appkey, 0, DEFAULT_STRING_LEN);
    memcpy(pa[i].appkey, appkey, strlen(appkey));

    memset(pa[i].text, 0, AUDIO_TEXT_LENGTH);
    if (g_text.empty()) {
      memcpy(pa[i].text, texts, strlen(texts));
    } else {
      memcpy(pa[i].text, g_text.data(), strlen(g_text.data()));
    }

    memset(pa[i].url, 0, DEFAULT_STRING_LEN);
    if (!g_url.empty()) {
      memcpy(pa[i].url, g_url.c_str(), g_url.length());
    }
  }

  std::vector<pthread_t> pthreadId(threads);
  // 启动四个工作线程, 同时识别四个音频文件
  for (int j = 0; j < threads; j++) {
    pthread_create(&pthreadId[j], NULL, &pthreadFunc, (void*)&(pa[j]));
  }

  std::cout << "start pthread_join..." << std::endl;

  for (int j = 0; j < threads; j++) {
    pthread_join(pthreadId[j], NULL);
  }

  std::cout << "flowingSynthesizerMultFile exit..." << std::endl;
  return 0;
}

int main(int argc, char* argv[]) {
  std::string g_appkey = getenv("NLS_APPKEY_ENV");
  g_akId = getenv("NLS_AK_ENV");
  g_akSecret = getenv("NLS_SK_ENV");

  std::cout << " appKey: " << g_appkey << std::endl;
  std::cout << " akId: " << g_akId << std::endl;
  std::cout << " akSecret: " << g_akSecret << std::endl;
  std::cout << " voice: " << g_voice << std::endl;
  std::cout << "\n" << std::endl;

  int ret = AlibabaNls::NlsClient::getInstance()->setLogConfig(
      "log-flowingSynthesizer", AlibabaNls::LogDebug, 400, 50, NULL);
  if (ret < 0) {
    std::cout << "set log failed." << std::endl;
    return -1;
  }

  // 设置运行环境需要的套接口地址类型, 默认为AF_INET
  // 必须在startWorkThread()前调用
  // AlibabaNls::NlsClient::getInstance()->setAddrInFamily("AF_INET");

  // 私有云部署的情况下进行直连IP的设置
  // 必须在startWorkThread()前调用
  // AlibabaNls::NlsClient::getInstance()->setDirectHost("xxx.xxx.xxx.xxx");

  std::cout << "startWorkThread begin... " << std::endl;

  // 启动工作线程, 在创建请求和启动前必须调用此函数
  // 入参为负时, 启动当前系统中可用的核数
  // 高并发的情况下推荐4, 单请求的情况推荐为1
  // 若高并发CPU占用率较高, 则可填-1启用所有CPU核
  AlibabaNls::NlsClient::getInstance()->startWorkThread(1);

  std::cout << "startWorkThread finish" << std::endl;

  // 合成多个文本
  ret = flowingSynthesizerMultFile(g_appkey.c_str(), g_threads);
  if (ret) {
    std::cout << "flowingSynthesizerMultFile failed." << std::endl;
    AlibabaNls::NlsClient::releaseInstance();
    return -2;
  }

  // 所有工作完成，进程退出前，释放nlsClient.
  // 请注意, releaseInstance()非线程安全.
  std::cout << "releaseInstance -> " << std::endl;
  AlibabaNls::NlsClient::releaseInstance();
  std::cout << "releaseInstance done." << std::endl;

  return 0;
}
```

## **状态码**

### **C++ SDK** 状态码

| **状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 0 | Success | 成功 | 无 |
| -10 | DefaultError | 默认错误。 | 暂未使用。 |
| -11 | JsonParseFailed | 错误的JSON格式。 | 请检查传入的 JSON 字符串是否符合 JSON 格式。 |
| -12 | JsonObjectError | 错误的JSON对象。 | 建议重新尝试。 |
| -13 | MallocFailed | Malloc失败。 | 请检查内存是否充足。 |
| -14 | ReallocFailed | Realloc失败。 | 请检查内存是否充足。 |
| -15 | InvalidInputParam | 传入无效的参数。 | 暂未使用。 |
| -50 | InvalidLogLevel | 无效日志级别。 | 请检查设置的Log级别。 |
| -51 | InvalidLogFileSize | 无效日志文件大小。 | 请检查设置的Log文件大小参数。 |
| -52 | InvalidLogFileNum | 无效日志文件数量。 | 请检查设置的Log文件数量参数。 |
| -100 | EncoderExistent | NLS的编码器已存在。 | 建议重新尝试。 |
| -101 | EncoderInexistent | NLS的编码器不存在。 | 建议重新初始化。 |
| -102 | OpusEncoderCreateFailed | Opus编码器创建失败。 | 建议重新初始化。 |
| -103 | OggOpusEncoderCreateFailed | OggOpus编码器创建失败。 | 建议重新初始化。 |
| -104 | InvalidEncoderType | encoder类型无效。 | 编译时可能关闭OPUS但是又使用，或请检查`ENCODER_TYPE`。 |
| -150 | EventClientEmpty | 主工作线程空指针， 已释放。 | 建议重新初始化，即`startWorkThread()`。 |
| -151 | SelectThreadFailed | 工作线程选择失败， 未初始化。 | 建议重新初始化，即`startWorkThread()`。 |
| -160 | StartCommandFailed | 发送start命令失败。 | 建议重新尝试 |
| -161 | InvokeStartFailed | 请求状态机不对， 导致start失败。 | 请检查当前请求是否未创建或者已经完成。 |
| -162 | InvokeSendAudioFailed | 请求状态机不对， 导致sendAudio失败。 | 请检查当前请求是否已经启动（即收到started事件回调）或者已经完成。 |
| -163 | InvalidOpusFrameSize | opus帧长无效， 默认为640字节。 | OPU编码模式下，`sendAudio`一帧只接收640字节数据。 |
| -164 | InvokeStopFailed | 请求状态机不对， 导致stop失败。 | 请检查当前请求是否未启动（即收到started事件回调）或者已经完成。 |
| -165 | InvokeCancelFailed | 请求状态机不对， 导致stop失败。 | 请检查当前请求是否未启动（即收到started事件回调）或者已经完成。 |
| -166 | InvokeStControlFailed | 请求状态机不对， 导致stControl失败。 | 请检查当前请求是否未启动（即收到started事件回调）或者已经完成。 |
| -200 | NlsEventEmpty | NLS事件为空。 | SDK内部使用， NlsEvent帧丢失。 |
| -201 | NewNlsEventFailed | 创建NlsEvent失败。 | SDK内部使用， NlsEvent帧创建失败。 |
| -202 | NlsEventMsgEmpty | NLS事件中消息为空。 | `parseJsonMsg()`进行解析时发现消息字符串为空。 |
| -203 | InvalidNlsEventMsgType | 无效的NLS事件中消息类型。 | SDK内部使用， NlsEvent帧的事件类型不合法。 |
| -204 | InvalidNlsEventMsgStatusCode | 无效的NLS事件中消息状态码。 | SDK内部使用， NlsEvent帧的事件消息状态不合法。 |
| -205 | InvalidNlsEventMsgHeader | 无效的NLS事件中消息头。 | SDK内部使用， NlsEvent帧的事件消息头不合法。 |
| -250 | CancelledExitStatus | 已调用Cancel。 | 暂未使用。 |
| -251 | InvalidWorkStatus | 无效的工作状态。 | SDK内部使用， 当前请求内部状态不合法。 |
| -252 | InvalidNodeQueue | WorkThread中NodeQueue无效。 | SDK内部使用， 当前待运行的请求不合法，建议释放当前请求重新尝试。 |
| -300 | InvalidRequestParams | 请求的入参无效。 | SendAudio传入的数据为空。 |
| -301 | RequestEmpty | 请求是空指针。 | SDK内部使用， 当前请求已经释放，建议释放当前请求重新尝试。 |
| -302 | InvalidRequest | 无效的请求。 | SDK内部使用， 当前请求已经释放，建议释放当前请求重新尝试。 |
| -303 | SetParamsEmpty | 设置传入的参数为空。 | 请检查传入的参数是否为空。 |
| -350 | GetHttpHeaderFailed | 获得http头失败。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -351 | HttpGotBadStatus | http错误的状态。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -352 | WsResponsePackageFailed | 解析WebSocket返回包失败。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -353 | WsResponsePackageEmpty | 解析WebSocket返回包为空。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -354 | WsRequestPackageEmpty | WebSocket请求包为空。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -355 | UnknownWsFrameHeadType | 未知WebSocket帧头类型。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -356 | InvalidWsFrameHeaderSize | 无效的WebSocket帧头大小。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -357 | InvalidWsFrameHeaderBody | 无效的WebSocket帧头本体。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -358 | InvalidWsFrameBody | 无效的WebSocket帧本体。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -359 | WsFrameBodyEmpty | 帧数据为空， 常见为收到了脏数据。 | SDK内部使用， 根据日志中反馈信息详细定位。 |
| -400 | NodeEmpty | Node为空指针。 | 建议释放当前请求重新尝试。 |
| -401 | InvaildNodeStatus | Node所处状态无效。 | SDK内部使用， 建议释放当前请求重新尝试。 |
| -402 | GetAddrinfoFailed | 通过DNS解析地址识别。 | SDK内部使用， 请检查当前环境的DNS是否可用。 |
| -403 | ConnectFailed | 联网失败。 | 请检查当前网络环境是否可用。 |
| -404 | InvalidDnsSource | 当前设备无DNS。 | SDK内部使用， 请检查当前环境的DNS是否可用。 |
| -405 | ParseUrlFailed | 无效URl。 | 请检查设置的URL是否有效。 |
| -406 | SslHandshakeFailed | SSL握手失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -407 | SslCtxEmpty | SSL\_CTX未空。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -408 | SslNewFailed | SSL\_new失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -409 | SslSetFailed | SSL设置参数失败. | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -410 | SslConnectFailed | SSL\_connect失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -411 | SslWriteFailed | SSL发送数据失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -412 | SslReadSysError | SSL接收数据收到SYSCALL错误。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -413 | SslReadFailed | SSL接收数据失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -414 | SocketFailed | 创建Socket失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -415 | SetSocketoptFailed | 设置Socket参数失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -416 | SocketConnectFailed | 进行Socket链接失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -417 | SocketWriteFailed | Socket发送数据失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -418 | SocketReadFailed | Socket接收数据失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -430 | NlsReceiveFailed | NLS接收帧数据失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -431 | NlsReceiveEmpty | NLS接收帧数据为空。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -432 | ReadFailed | 接收数据失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -433 | NlsSendFailed | NLS发送数据失败。 | SDK内部使用， 请检查当前网络环境是否可用，并再次尝试。 |
| -434 | NewOutputBufferFailed | 创建buffer失败。 | SDK内部使用， 请检查内存是否充足。 |
| -435 | NlsEncodingFailed | 音频编码失败。 | SDK内部使用， 建议释放当前请求重新尝试。 |
| -436 | EventEmpty | event为空。 | SDK内部使用， 建议释放当前请求重新尝试。 |
| -437 | EvbufferTooMuch | evbuffer中数据太多。 | SDK内部使用， 发送数据缓存已满（16K音频最大缓存320000，8K音频最大缓存160000），请检查是否发送音频数据过频或一次发送过多数据。 |
| -438 | EvutilSocketFalied | evutil设置参数失败。 | SDK内部使用， 建议释放当前请求重新尝试。 |
| -439 | InvalidExitStatus | 无效的退出状态。 | 请检查是否已经cancel了当前请求。 |
| -450 | InvalidAkId | 阿里云账号AK ID无效。 | 请检查阿里云账号AK ID是否为空。 |
| -451 | InvalidAkSecret | 阿里云账号AK Secret无效。 | 请检查阿里云账号AK Secret是否为空。 |
| -452 | InvalidAppKey | 项目appKey无效。 | 请检查阿里云项目appKey是否为空。 |
| -453 | InvalidDomain | domain无效。 | 请检查输入的domain是否为空。 |
| -454 | InvalidAction | action无效。 | 请检查输入的action是否为空。 |
| -455 | InvalidServerVersion | ServerVersion无效 | 请检查输入的ServerVersion是否为空。 |
| -456 | InvalidServerResource | ServerResource无效。 | 请检查输入的ServerResource是否为空。 |
| -457 | InvalidRegionId | RegionId无效。 | 请检查输入的Region Id是否为空。 |
| -500 | InvalidFileLink | 无效的录音文件链接 | 录音文件转写文件链接为空。 |
| -501 | ErrorStatusCode | 错误的状态码。 | 录音文件转写返回错误，详见错误码。 |
| -502 | IconvOpenFailed | 申请转换描述失败。 | UTF8与GBK转换失败。 |
| -503 | IconvFailed | 编码转换失败。 | UTF8与GBK转换失败。 |
| -504 | ClientRequestFaild | 账号客户端请求失败。 | 录音文件转写返回失败。 |
| -999 | NlsMaxErrorCode | 无 | 无 |

### **其他状态码**

| **状态码** | **状态消息** | **原因** | **解决方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **状态码** | **状态消息** | **原因** | **解决方案** |
| 10000001 | `NewSslCtxFailed` | `SSL: couldn't create a context!` | 建议重新初始化。 |
| 10000002 | `DefaultErrorCode` | `return of SSL_read: error:00000000:lib(0):func(0):reason(0)` | 建议重新尝试。 |
| `return of SSL_read: error:140E0197:SSL routines:SSL_shutdown:shutdown while in init` |
| 10000003 | `SysErrorCode` | 系统错误 | 根据系统反馈的错误信息进行处理。 |
| 10000004 | `EmptyUrl` | `URL: The url is empty.` | 传入的URL为空， 请重新填写正确URL。 |
| 10000005 | `InvalidWsUrl` | `Could not parse WebSocket url:` | 传入的URL格式错误， 请重新填写正确URL。 |
| 10000007 | `JsonStringParseFailed` | `JSON: Json parse failed.` | JSON格式异常， 请通过日志查看具体的错误点。 |
| 10000008 | `UnknownWsHeadType` | `WEBSOCKET: unkown head type.` | 联网失败，请检查本机DNS解析和URL是否有效。 |
| 10000009 | `HttpConnectFailed` | `HTTP: connect failed.` | 与云端连接失败，请检查网络后，重试。 |
| 10000010 | `MemNotEnough` | 内存不足 | 请检查内存是否充足。 |
| 10000015 | `SysConnectFailed` | `connect failed.` | 联网失败，请检查本机DNS解析和URL是否有效。 |
| 10000100 | `HttpGotBadStatusWith403` | `Got bad status host=xxxxx line=HTTP/1.1 403 Forbidden` | 链接被拒，请检查账号特别是token是否过期。 |
| 10000101 | `EvSendTimeout` | `Send timeout. socket error:` | libevent发送event超时，请检查回调中是否有耗时任务，或并发过大导致无法及>时处理事件。 |
| 10000102 | `EvRecvTimeout` | `Recv timeout. socket error:` | libevent接收event超时，请检查回调中是否有耗时任务，或并发过大导致无法及>时处理事件。 |
| 10000103 | `EvUnknownEvent` | `Unknown event:` | 未知的libevent事件，建议重新尝试。 |
| 10000104 | `OpNowInProgress` | `Operation now in progress` | 链接正在进行中，建议重新尝试。 |
| 10000105 | `BrokenPipe` | `Broken pipe` | pipe处理不过来，建议重新尝试。 |
| 10000110 | `TokenHasExpired` | `Gateway:ACCESS_DENIED:The token 'xxx' has expired!` | 请更新Token。 |
| 10000111 | `TokenIsInvalid` | `Meta:ACCESS_DENIED:The token 'xxx' is invalid!` | 请检查Token的有效性。 |
| 10000112 | `NoPrivilegeToVoice` | `Gateway:ACCESS_DENIED:No privilege to this voice! (voice: zhinan， privilege: 0)` | 此发音人无权使用。 |
| 10000113 | `MissAuthHeader` | `Gateway:ACCESS_DENIED:Missing authorization header!` | 请检查账号是否有权限，或并发是否在限度内。 |
| 10000120 | `Utf8ConvertError` | `utf8ToGbk failed` | UTF-8转码失败，常为系统问题，建议重新尝试。 |
| 20000000 | `SuccessStatusCode` | 成功 |  |

### **服务端响应状态码**

关于服务状态码，请参见 [服务状态码](https://help.aliyun.com/zh/isi/developer-reference/api-reference-1#section-n3d-5n8-ycb "")。