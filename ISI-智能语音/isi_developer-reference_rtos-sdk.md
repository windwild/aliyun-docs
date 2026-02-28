### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/)

# RTOS SDK

更新时间：

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

本文介绍如何使用智能语音交互语音对话的RTOS SDK，包括SDK的安装方法及SDK代码示例等。

## 前提条件

- 已 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#2572188 "") 并获取项目Appkey。

语音对话的项目类型选择 **语音识别 \+ 语音合成 \+ 语音分析**，然后在 **服务管理与开通** 页面将其升级为商用版。

- 已 [获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token-in-the-console "")。


## **下载安装**

[下载SDK和示例代码](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241015/hsbkca/voicechat-rtos-master-57cc95ec8cbd4e52b5d3a96e1b0b74002ef8fa75+%281%29.zip)。

## **平台依赖**

### **支持平台**

Linux、YOC、FreeRTOS

### **依赖库**

mbedtls、cjson、lwip

### **最小化配置参考**

```c
#ifndef MBEDTLS_CONFIG_H
#define MBEDTLS_CONFIG_H

#define MBEDTLS_PLATFORM_C
#define MBEDTLS_PLATFORM_MEMORY

/* mbed TLS feature support */
#define MBEDTLS_CIPHER_MODE_CBC
#define MBEDTLS_CIPHER_MODE_CFB
#define MBEDTLS_PKCS1_V15
#define MBEDTLS_KEY_EXCHANGE_RSA_ENABLED
#define MBEDTLS_SSL_PROTO_TLS1_2

#ifdef MBEDTLS_RSA_ALT
#define MBEDTLS_RSA_NO_CRT
#endif

/* mbed TLS modules */
#define MBEDTLS_AES_C
#define MBEDTLS_ASN1_PARSE_C
#define MBEDTLS_BIGNUM_C
#define MBEDTLS_CIPHER_C
#define MBEDTLS_CIPHER_MODE_CTR
#define MBEDTLS_CTR_DRBG_C
#define MBEDTLS_ENTROPY_C

#define MBEDTLS_MD_C
#define MBEDTLS_MD5_C

#define MBEDTLS_NET_C_ALT
#define MBEDTLS_OID_C
#define MBEDTLS_SHA1_C
#define MBEDTLS_SHA256_C
#define MBEDTLS_SHA512_C
#define MBEDTLS_PK_C
#define MBEDTLS_PK_PARSE_C
#define MBEDTLS_RSA_C
#define MBEDTLS_SSL_CLI_C

#define MBEDTLS_SSL_TLS_C
#define MBEDTLS_X509_CRT_PARSE_C
#define MBEDTLS_X509_USE_C
#define MBEDTLS_BASE64_C
#define MBEDTLS_CERTS_C
#define MBEDTLS_PEM_PARSE_C

#define MBEDTLS_SSL_SERVER_NAME_INDICATION

/* Save some RAM by adjusting to your exact needs */
#define MBEDTLS_PSK_MAX_LEN    16 /* 128-bits keys are generally enough */

#define MBEDTLS_SSL_CIPHERSUITES  \
        MBEDTLS_TLS_RSA_WITH_AES_128_CBC_SHA

/*
 * Save RAM at the expense of interoperability: do this only if you control
 * both ends of the connection!  (See comments in "mbedtls/ssl.h".)
 * The optimal size here depends on the typical size of records.
 */

#if !defined (MBEDTLS_DEBUG_C)
/*reduce readonly date size*/
#define CK_REMOVE_UNUSED_FUNCTION_AND_DATA
#endif

#ifdef CK_SAVE_MEM_L2

#error "comment this line and set CK_FLASH_BLOCK_START,CK_FLAHS_BLOCK_NUM"

#define ck_alloc(a)      ck_cert_flash_alloc(a)
#define ck_memcpy(d,s,l) ck_cert_flash_copy((uint32_t)d,s,l)

#endif

#ifdef MBEDTLS_SSL_PROTO_DTLS
#define CK_SAVE_MEM_L4   /*alicoap can open*/
#endif

#endif /* MBEDTLS_CONFIG_H */
```

## **交互模式**

RTOS SDK和Demo目前支持按键开始/结束交互的模式。

## **使用Demo测试**

1. 编辑入口类，修改如下参数。


|     |     |
| --- | --- |
| **参数** | **说明** |
| ws\_url | 域名地址。生产环境网关URL：<br>`wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1` |
| appkey | 语音对话服务接入的key。详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#2572188 "")。 |
| token | 访问系统的令牌。具体获取操作，请参见 [通过控制台获取Token](https://help.aliyun.com/zh/isi/getting-started/obtain-an-access-token-in-the-console "")。 |

2. 代码示例如下。


```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <time.h>
#include <pthread.h>

#include "nui_things.h"
#include "log_new.h"
#include "my_fifo.h"

#define TAG "voice_chat_api_test"

static int global_state_ = -1;
static int first_frame = 1;
my_fifo_t *asr_fifo_ = NULL;
my_fifo_t *tts_fifo_ = NULL;
FILE *fp_asr_ = NULL;
FILE *fp_tts_ = NULL;
char *g_appkey = NULL;
char *g_token = NULL;
char *g_dialog_id = NULL;
char *g_in_file = NULL;
char *g_url = NULL;

static long long current_milliseconds() {
       struct timespec ts;
       clock_gettime(CLOCK_REALTIME, &ts);
       return (long long)(ts.tv_sec) * 1000 + (ts.tv_nsec / 1000000);
}
static int event_cb(void *user_data, NuiThingsEvent event, int dialog_finish)
{
       int ret = 0;
       switch (event) {
       case kNuiThingsEventStarted:
           KLOGW(TAG, "============================Started:\n%s\n", (char *)user_data);
           //设备端可记录dialog_id，下次会话初始化时可选择添入dialog_id以继续上一次会话
           break;
       case kNuiThingsEventListening:
           global_state_ = kNuiThingsEventListening;
           first_frame = 1;
           KLOGW(TAG, "============================Listening");
           break;
       case kNuiThingsEventThinking:
           global_state_ = kNuiThingsEventListening;
           KLOGW(TAG, "============================Thinking");
           break;
       case kNuiThingsEventResponding:
           global_state_ = kNuiThingsEventResponding;
           KLOGW(TAG, "============================Responding");
           break;
       case kNuiThingsEventSpeechContent:
           KLOGW(TAG, "============================SpeechContent:\n%s\n", (char *)user_data);
           break;
       case kNuiThingsEventSpeechEnded:
           KLOGW(TAG, "============================SpeechEnded:\n%s\n", (char *)user_data);
           break;
       case kNuiThingsEventRespondingContent:
           KLOGW(TAG, "============================RespondingContent:\n%s\n", (char *)user_data);
           break;
       default:
           break;
       }

       return ret;
}
static int provide_asr_data_cb(void *user_data, char *buffer, int len)
{
       int ret = 0;
       if (get_fifo_count(asr_fifo_) > 0) {
           ret = my_fifo_get(asr_fifo_, buffer, len);
       }
       return ret;
}
static int tts_data_cb(void *user_data, NuiThingsEvent event, const char *event_response, const int event_length) {
       int ret = 0;
       char file_name[64];
       memset(file_name, 0, sizeof(file_name));
       switch(event) {
           case kNuiThingsEventTTSStart:
               KLOGW(TAG, "============================TTSStart");
               if (fp_tts_ == NULL) {
                   my_fifo_clear(tts_fifo_);
                   sprintf(file_name, "tts_%lld.pcm", current_milliseconds());
                   fp_tts_ = fopen(file_name, "wb");
               }
               break;
           case kNuiThingsEventTTSEnd:
               KLOGW(TAG, "============================TTSEnd");
               if (fp_tts_ != NULL) {
                   fclose(fp_tts_);
                   fp_tts_ = NULL;
               }
               global_state_ = kNuiThingsEventTTSEnd;
               break;
           case kNuiThingsEventTTSData:
               ret = my_fifo_put(tts_fifo_, (void *)event_response, event_length);
               break;
       }
       return ret;
}
void *flow_handler(void * arg) {
       while (1) {
           usleep(20*1000);
           if (global_state_ == kNuiThingsEventTTSEnd) {
               nui_things_set_action(kVoiceChatActionLocalRespondingEnded);
               if(fp_asr_ == NULL) {
                   my_fifo_clear(asr_fifo_);
                   fp_asr_ = fopen(g_in_file, "rb");
               }
               global_state_ = kNuiThingsEventNone;
           }
       }
       return NULL;
}
int invalied_argv(int index, int argc) {
     if (index >= argc) {
       printf("invalid params...\n");
       return -1;
     }
     return 0;
}
int parse_argv(int argc, char *argv[]) {
       int index = 1;
       while (index < argc) {
           if (!strcmp(argv[index], "--appkey")) {
               index++;
               if (invalied_argv(index, argc)) return -1;
               g_appkey = argv[index];
           } else if (!strcmp(argv[index], "--token")) {
               index++;
               if (invalied_argv(index, argc)) return -1;
               g_token = argv[index];
           } else if (!strcmp(argv[index], "--dialog_id")) {
               index++;
               if (invalied_argv(index, argc)) return -1;
               g_dialog_id = argv[index];
           } else if (!strcmp(argv[index], "--in_file")) {
               index++;
               if (invalied_argv(index, argc)) return -1;
               g_in_file = argv[index];
           } else if (!strcmp(argv[index], "--url")) {
               index++;
               if (invalied_argv(index, argc)) return -1;
               g_url = argv[index];
           }
           index++;
       }
       if (g_in_file == NULL || g_appkey == NULL || g_token == NULL) {
           return -1;
       }
       return 0;
}
int main(int argc, char *argv[]) {
       if (parse_argv(argc, argv)) {
           printf(
               "params is not valid.\n"
               "Usage:\n"
               "  --url <url of server>\n"
               "  --appkey < >\n"
               "  --token < >\n"
               "  --in_file < >\n"
               "eg:\n"
               "./out/linux/bin/VoiceChatApiTest --appkey xxx --token xxx --url wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1 --in_file 16k_16bit_mono.pcm\n");
           return -1;
       }
       char asr_buffer[16*2*320];
       char tts_buffer[24*2*100];
       int count = sizeof(asr_buffer)/2;
       int read_size = 0;
       pthread_t flow_thread;

       /* mit sdk struct */
       NuiThingsListener   mit_listener;
       NuiThingsInitConfig mit_init_config; //sdk init config
       NuiThingsConfig     mit_dialog_config; //nls dialog config

       memset(&mit_init_config, 0, sizeof(mit_init_config));
       memset(&mit_dialog_config, 0, sizeof(mit_dialog_config));


       //init sdk config
       mit_listener.on_event_callback       = event_cb;
       mit_listener.need_data_callback      = provide_asr_data_cb;
       mit_listener.tts_data_callback       = tts_data_cb;
       mit_listener.user_data               = NULL;
       mit_init_config.mode                 = kNuiThingsModeNls;
       mit_init_config.listener             = &mit_listener;
       mit_init_config.log_link_enable      = 0;
       mit_init_config.log_level            = Warning;

       //init nls dialog config
       mit_dialog_config.mode                      = "push2talk";
       mit_dialog_config.device_uuid               = "1234567890";
       if (g_url != NULL) {
           mit_dialog_config.url                   = g_url;
       } else {
           mit_dialog_config.url                   = "wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1";
       }
       mit_dialog_config.app_key                   = g_appkey;
       mit_dialog_config.token                     = g_token;
       mit_dialog_config.model_id                  = "qwen-plus";
       mit_dialog_config.prompt                    = "\u4f60\u662f\u4e2a\u6709\u7528\u7684\u52a9\u624b";//你是个有用的助手
       mit_dialog_config.voice                     = "loongstella";
       mit_dialog_config.inbound_format            = "pcm";
       mit_dialog_config.outbound_format           = "pcm";
       mit_dialog_config.outbound_sample_rate      = 24000;
       if (g_dialog_id != NULL) {
           //上轮对话的dialog_id，不设置默认从服务端返回
           mit_dialog_config.dialog_id             = g_dialog_id;
       }
       mit_dialog_config.context_depth             = "all";
       mit_dialog_config.enable_search             = "false";
       mit_dialog_config.debug                     = "false";

       //init fifo
       asr_fifo_ = my_fifo_alloc(16*2*1000*9);
       tts_fifo_ = my_fifo_alloc(24*2*1000*9);

       //init
       nui_things_init(&mit_init_config);

       //start Connect->Start->Listening
       nui_things_start(&mit_dialog_config);

       if (fp_asr_ = fopen(g_in_file, "rb")) {
           KLOGW(TAG, "open file success.");
           fread(asr_buffer, 1, sizeof(asr_buffer), fp_asr_);
           my_fifo_put(asr_fifo_, asr_buffer, sizeof(asr_buffer));
       } else {
           KLOGE(TAG, "open file failed.");
           nui_things_stop(1);
           return -1;
       }
       pthread_create(&flow_thread, NULL, flow_handler, NULL);

       while (1) {
           if (global_state_ == kNuiThingsEventListening) {
               //KLOGW(TAG, "Listening");
               if (first_frame) {
                   nui_things_set_action(kVoiceChatActionSendSpeech);
                   first_frame = 0;
               }
               read_size = 0;
               if (fp_asr_) {
                   if ((read_size = fread(asr_buffer, 1, count, fp_asr_)) < count) {
                       my_fifo_put(asr_fifo_, asr_buffer, read_size);
                       nui_things_set_action(kVoiceChatActionStopSpeech);
                       fclose(fp_asr_);
                       fp_asr_ = NULL;
                   } else {
                       my_fifo_put(asr_fifo_, asr_buffer, count);
                   }
               }
           } else if (global_state_ == kNuiThingsEventResponding) {
               if (get_fifo_count(tts_fifo_) > 0) {
                   if (fp_tts_) {
                       read_size = my_fifo_get(tts_fifo_, tts_buffer, sizeof(tts_buffer));
                       fwrite(tts_buffer, 1, read_size, fp_tts_);
                   }
               }
           }
           usleep(20*1000);
       }
}
```


## **接口说明**

```c
/**
 * 初始化VoiceChat实例
 */
int nui_things_init(NuiThingsInitConfig * config);
/**
 * 销毁VoiceChat实例，释放资源
 */
int nui_things_uninit();
/**
 * 启动VoiceChat实例，连接服务
 */
int nui_things_start(NuiThingsConfig *config);
/**
 * 发送请求
 */
int nui_things_set_action(VoiceChatActionType action);
/**
 * 在Listening状态时，通知服务端与用户主动交互
 * type : "transcript" 表示直接把文本转语音，"prompt" 表示把文本送大模型回答
 * text : 请求文本，如"您好，我是您的智能语音助手，期待为您服务。"
 */
int nui_things_request_to_respond(const char *type, const char *text);
/**
 * 停止VoiceChat实例
 * cancel : 0 等待当前交互完成后停止， 1 立即停止
 */
int nui_things_stop(int cancel);
```

### DialogState：对话状态说明

语音对话服务包括以下三种状态：

|     |     |
| --- | --- |
| **状态** | **说明** |
| LISTENING | 表示机器人正在监听用户输入。用户可以发送音频。 |
| THINKING | 表示机器人正在思考。 |
| RESPONDING | 表示机器人正在生成语音或语音回复中。 |

## **时序图**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2951319271/CAEQUBiBgICMyK3PlBkiIDk5OGRlZTdmN2QwMTQ1YzBiMjA4MmRjMmU3OWZmNTRm4705034_20241012144303.065.svg)

## **状态机**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2951319271/CAEQUBiBgMCe2La9lBkiIDNiNDIwZTg5NmZiYzRhNTU4MDdhZjk0NGNhY2FlYjg54705044_20241015162332.916.svg)

## **移植适配流程**

### **根据平台选择对应的配置文件**

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5751319271/p859604.png)

### **根据平台创建相应的目录**

## YOC平台

1. 将package.yaml文件和voicechat-rtos目录放到componets/mind\_nuithings目录下，根据目录结构修改package.yaml目录中source\_file:的相对路径，例如将nui\_things替换为源码目录voicechat-rtos。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5751319271/p859605.png)

2. 在工程目录solutions/smart\_speaker\_demo/package.yaml文件中增加mind\_nuithings组件。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5751319271/p859606.png)

![image.png](<Base64-Image-Removed>)

3. 在solutions/smart\_speaker\_demo目录下编译即可生成静态库libmind\_nuithings.a。


## FreeRTOS平台

本文以XR872为例进行说明。

1. 将voicechat-rtos工程拷贝至src目录中。

![image](<Base64-Image-Removed>)

2. 将demo目录下的Makefile文件拷贝至voicechat-rtos根目录下。

![image.png](<Base64-Image-Removed>)

3. 修改xradio-skylark-sdk/src目录下的Makefile文件，增加voicechat-rtos模块。


```diff
diff --git a/src/Makefile b/src/Makefile
index b3996e6..20f5943 100755
   --- a/src/Makefile
+++ b/src/Makefile
@@ -68,6 +68,7 @@ SUBDIRS += $(AT_SUBDIRS)
    SUBDIRS += cjson
    SUBDIRS += util
    SUBDIRS += jpeg
+SUBDIRS += voicechat-rtos
    endif

    # ----------------------------------------------------------------------------
```

4. 修改xradio-skylark-sdk目录下的gcc.mk文件，增加头文件路径（此处请根据具体的voicechat-rtos目录设置）。


```diff
diff --git a/gcc.mk b/gcc.mk
index 91a120b..b55514d 100755
   --- a/gcc.mk
+++ b/gcc.mk
@@ -80,7 +80,7 @@ endif

    CC_FLAGS = $(CPU) -c $(DBG_FLAG) -fno-common -fmessage-length=0 \
           -fno-exceptions -ffunction-sections -fdata-sections -fomit-frame-pointer \
   -       -Wall -Werror -Wpointer-arith -Wno-error=unused-function \
+       -Wall -Wpointer-arith -Wno-error=unused-function \
           -MMD -MP $(OPTIMIZE_FLAG)

    LD_FLAGS = $(CPU) -Wl,--gc-sections --specs=nano.specs \
@@ -181,6 +181,11 @@ endif
    INCLUDE_PATHS += -I$(INCLUDE_ROOT_PATH)/net
    INCLUDE_PATHS += -I$(INCLUDE_ROOT_PATH)/net/$(LWIP_DIR)
    INCLUDE_PATHS += -I$(INCLUDE_ROOT_PATH)/net/$(MBEDTLS_DIR)
+INCLUDE_PATHS += -I$(ROOT_PATH)/src/voicechat-rtos/include
+INCLUDE_PATHS += -I$(ROOT_PATH)/src/voicechat-rtos/hal/include
+INCLUDE_PATHS += -I$(ROOT_PATH)/src/voicechat-rtos/src/util
+INCLUDE_PATHS += -I$(ROOT_PATH)/src/voicechat-rtos/src/nls_nui_things/include
+INCLUDE_PATHS += -I$(ROOT_PATH)/src/voicechat-rtos/src/nls_nui_things/nls_sdk/include
    ifeq ($(__CONFIG_LWIP_V1), y)
      INCLUDE_PATHS += -I$(INCLUDE_ROOT_PATH)/net/$(LWIP_DIR)/ipv4
    endif
```

5. 在project/demo/audio\_demo/gcc目录中，编译即可生成libvoicechat.a。


```shell
make lib -j4
```


## Linux平台编译测试

本文以Ubuntu主机为例进行说明。

```shell
sudo apt install libmbedtls-dev
sh build_linux.sh
# 一次会话，进行多轮交互
./out/linux/bin/VoiceChatApiTest --appkey xxx --token xxx --url wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1 --in_file 16k_16bit_mono.pcm
# 继续上一次会话，进行多轮交互
./out/linux/bin/VoiceChatApiTest --appkey xxx --token xxx --url wss://nls-gateway-cn-beijing.aliyuncs.com/ws/v1 --in_file context_test.pcm --dialog_id xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```