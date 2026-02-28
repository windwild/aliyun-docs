### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/developer-reference/cosvoice-large-model-for-speech-synthesis/)[CosyVoice声音复刻服务](https://help.aliyun.com/zh/isi/developer-reference/cosyvoice-voice-voice-replica-service/)简介与SDK代码示例

# 简介与SDK代码示例

更新时间：2026-02-26 21:01:55

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：WebSocket协议说明](https://help.aliyun.com/zh/isi/developer-reference/websocket-protocol-description)[下一篇：通过OpenAPI复刻](https://help.aliyun.com/zh/isi/developer-reference/use-http-or-https-to-clone-cosyvoice)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

应用场景

产品优势

重要说明

计费说明

前提条件

使用示例

Python 使用示例

Java 使用示例

服务状态码

相关文档

CosyVoice声音复刻服务依托先进的大模型技术进行特征提取，从而完成声音的复刻，且无需训练过程。仅需提供时长较短的音频，即可迅速生成高度相似且听感自然的定制声音。本文将详细介绍CosyVoice声音复刻服务的使用方法和操作流程，帮助您快速实现声音复刻。

**重要**

声音复刻服务已于2025年4月14日升级至CosyVoice2.0 版本。在此之后复刻的音色默认使用CosyVoice2.0，相比于1.0具有更好的复刻效果。

在此之前使用 CosyVoice1.0 复刻的音色可以正常使用，您也可以使用原始音频重新复刻，以获得更好的复刻效果。

## **应用场景**

- **陪伴场景：** 利用复刻的家人声音提供个性化陪伴，用于智能助手和车载导航语音，以及家庭娱乐项目，如为家人朗读绘本、控制家用电器或提供教育辅导。

- **教育场景：** 使用复刻老师的声音，加强师生互动，丰富教学视频和课件的内容，打造更亲切、更生动的学习体验。

- **音视频产业：** 通过复刻主播的声音，方便后期补录、配音等应用场景，提高音视频的制作效率。

- **智能客服：** 借助复刻的客户经理声音，提供语音服务，包括但不限于客户回访和市场营销电话，以赋予服务更加个性化、人性化的特点。


## **产品优势**

- **低样本音频要求：** 仅需短短10~20秒的录音便能完成声音复刻，显著降低了录制成本，提升了效率。

- **高度拟真：** 利用阿里千问语音实验室自研的CosyVoice生成式神经网络语音大模型算法，结合前沿的零样本学习技术，能够在语调、韵律以及情感表达上高度还原真人声音，很难与真实录音相辨。

- **即时合成：** 秒级还原真实音色，提供高效、实时的声音复刻服务。

- **支持SSML**：在长文本语音合成中使用复刻音色支持通过SSML添加背景音、停顿并修正读音。SSML用法参考文档 [SSML标记语言介绍](https://help.aliyun.com/zh/isi/developer-reference/introduction-to-cosyvoice-ssml-markup-language "")。


## **重要说明**

- **声音复刻数量限制：** 每个UID最多可复刻1000个音色（v1和v2共用此额度）。若您需求超过此限额，请提前与我们的售前团队联系沟通。超过1年未使用的声音将下线处理。目前暂不支持删除已复刻的音色。

- **版权与合法性：** 您需对所提供声音的所有权及合法使用权负责，请注意阅读开通智能语音交互- **流式文本语音合成** 的 [服务协议](https://terms.alicdn.com/legal-agreement/terms/b_platform_service_agreement/20240229113512917/20240229113512917.html)。

- **复刻后语音的使用：** 使用复刻产生的语音（VoiceName）的用法和 [语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/streaming-speech-synthesis-tts-documentation/ "") 中的预设音色（例如：longxiaoxia）的用法一致。



**重要**





CosyVoice声音复刻产生的语音，只能在 [语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/streaming-speech-synthesis-tts-documentation/ "") 中使用，请勿在其它语音合成中使用，否则会合成失败。

- **服务调用方式：** 声音复刻服务当前仅支持通过调用API方式使用。


## 计费说明

声音复刻为免费服务，复刻成功后，使用文字转语音服务时会产生“语音合成CosyVoice大模型”相关的接口使用费用，当前价格为2元/万字符，详情请参见 [计费说明-后付费方式](https://help.aliyun.com/zh/isi/product-overview/billing-10#p-i8d-pi2-t1o "")。

## **前提条件**

- 了解相关条款并开通智能语音交互- **流式文本语音合成** 服务 **商用** 版。开通地址，请参见 [智能语音交互](https://common-buy.aliyun.com/?&commodityCode=nlsService)。

- 已准备公网可访问的音频URL，推荐将音频上传至OSS。具体操作，请参见 [简单上传至OSS](https://help.aliyun.com/zh/oss/user-guide/simple-upload#a632b50f190j8 "")。音频格式要求：
  - 声道数：单/双声道

  - 采样位数：16 bit

  - 采样率：大于16000 Hz

  - 格式：WAV、MP3、M4A

  - 文件大小：10M以内

  - 音频时长：10～20秒，不建议超过60秒。在朗读时请保持连贯，至少包含一段超过5秒的连续语音。

## **使用示例**

本文以阿里云Python SDK和Java SDK举例说明，其他语言SDK，请参见 [阿里云SDK开发参考](https://help.aliyun.com/zh/sdk/developer-reference/)。

### **Python 使用示例**

#### **步骤一：安装阿里云SDK**

执行以下命令，安装最新版本的阿里云Python SDK。

```bash
pip install aliyun-python-sdk-core
```

#### **步骤二：功能实现**

声音复刻接口调用的代码示例如下：

```python
import os
import json
import time

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.request import CommonRequest

# 通过环境变量获取阿里云Ak ID以及Ak Secret, 避免使用明文造成泄露风险
# 如您未配置环境变量，请将下行代码中的os.environ.get('ALIYUN_AK_ID')替换为AK ID，将os.environ.get('ALIYUN_AK_SECRET')替换为AK Secret
client = AcsClient(os.environ.get('ALIYUN_AK_ID'), os.environ.get('ALIYUN_AK_SECRET'))
domain = 'nls-slp.cn-shanghai.aliyuncs.com'
version = '2019-08-19'

def build_request(api_name, method):
    request = CommonRequest()
    request.set_domain(domain)
    request.set_version(version)
    request.set_action_name(api_name)
    request.set_method(method)
    request.set_protocol_type('https')
    return request

def cosy_clone(voice_prefix, url):
    clone_request = build_request('CosyVoiceClone', 'POST')
    clone_request.add_body_params('Url', url)
    clone_request.add_body_params('VoicePrefix', voice_prefix)
    # 设定等待超时时间为15s
    clone_request.set_read_timeout(15)
    begin = int(round(time.time() * 1000))
    clone_response = client.do_action_with_exception(clone_request)
    end = int(round(time.time() * 1000))
    print(json.loads(clone_response))
    print('cost: {}'.format(end - begin))

def cosy_list(voice_prefix, page_index=1, page_size=10):
    list_request = build_request('ListCosyVoice', 'POST')
    list_request.add_body_params('VoicePrefix', voice_prefix)
    list_request.add_body_params('PageIndex', page_index)
    list_request.add_body_params('PageSize', page_size)
    list_response = client.do_action_with_exception(list_request)
    print(json.loads(list_response))

if __name__ == '__main__':
    # 1. 调用CosyVoiceClone接口复刻声音
    audio_url = 'https://your-url'
    prefix = 'tongyi'  # 要求英文字母或数字
    cosy_clone(prefix, audio_url)
    # 调用成功后接口会同步返回VoiceName, 格式为 cosyvoice-${voice_prefix}-${7位随机字符}

    # 2. 调用ListCosyVoice接口可以查询您某个前缀所有声音的状态
    cosy_list(prefix)
```

更多关于CosyVoice声音复刻API信息，请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/isi/developer-reference/cosyvoice-sound-replica-api "")。

#### **步骤三：使用复刻音色**

复刻音色的使用方法和Cosyvoice成品音色相同，您在调用CosyVoice大模型时，将voice字段替换为复刻的VoiceName即可。CosyVoice大模型使用方法请参见 [语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/streaming-speech-synthesis-tts-documentation/ "")。

### Java 使用示例

#### **步骤一：安装阿里云SDK**

从Maven服务器下载最新版本的SDK。

```xml
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>4.6.4</version>
</dependency>
```

#### **步骤二：功能实现**

声音复刻接口调用的代码示例如下：

```java
package org.example;

import com.aliyuncs.CommonRequest;
import com.aliyuncs.CommonResponse;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.http.MethodType;
import com.aliyuncs.http.ProtocolType;
import com.aliyuncs.profile.DefaultProfile;

public class CosyVoiceDemo {
    //域名
    private static final String DOMAIN = "nls-slp.cn-shanghai.aliyuncs.com";
    // API版本
    private static final String API_VERSION = "2019-08-19";

    private static final IAcsClient client;

    static {
        // 创建DefaultAcsClient实例并初始化
        DefaultProfile profile = DefaultProfile.getProfile(
                "cn-shanghai",
                // 通过环境变量获取阿里云Ak ID，避免使用明文造成泄露风险
                // 如您未配置环境变量，请将下行代码中的System.getenv("AK_ID")替换为AK ID
                System.getenv("AK_ID"),
                // 通过环境变量获取阿里云Ak Secret, 避免使用明文造成泄露风险
                // 如您未配置环境变量，请将下行代码中的System.getenv("AK_SECRET"))替换为AK Secret
                System.getenv("AK_SECRET"));
        client = new DefaultAcsClient(profile);
    }

    public static void main(String[] args) throws InterruptedException {
        String voicePrefix = "your-voice-prefix";
        String url = "your-file-url";
        cosyClone(voicePrefix, url);
        cosyList(voicePrefix);
    }

    private static void cosyList(String voicePrefix) {
        CommonRequest request = buildRequest("ListCosyVoice");
        request.putBodyParameter("VoicePrefix", voicePrefix);
        String response = sendRequest(request);
        System.out.println(response);
    }

    private static void cosyClone(String voicePrefix, String url) {
        CommonRequest cloneRequest = buildRequest("CosyVoiceClone");
        cloneRequest.putBodyParameter("VoicePrefix", voicePrefix);
        cloneRequest.putBodyParameter("Url", url);
        // 设定等待超时时间为15s
        cloneRequest.setSysReadTimeout(15000);
        long startTime = System.currentTimeMillis();
        String response = sendRequest(cloneRequest);
        long endTime = System.currentTimeMillis();
        System.out.println(response);
        System.out.println("cost: "+ (endTime - startTime) + " 毫秒");
    }

    private static CommonRequest buildRequest(String popApiName) {
        CommonRequest request = new CommonRequest();
        request.setMethod(MethodType.POST);
        request.setDomain(DOMAIN);
        request.setVersion(API_VERSION);
        request.setAction(popApiName);
        request.setProtocol(ProtocolType.HTTPS);
        return request;
    }

    private static String sendRequest(CommonRequest request) {
        try {
            CommonResponse response = client.getCommonResponse(request);
            return response.getData();
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

更多关于CosyVoice声音复刻API信息，请参见 [CosyVoice声音复刻API](https://help.aliyun.com/zh/isi/developer-reference/cosyvoice-sound-replica-api "")。

#### 步骤三：使用复刻音色

复刻音色的使用方法和Cosyvoice成品音色相同，您在调用CosyVoice大模型时，将voice字段替换为复刻的VoiceName即可。CosyVoice大模型使用方法请参见 [语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/streaming-speech-synthesis-tts-documentation/ "")。

## **服务状态码**

| **状态码** | **状态消息** | **原因和处理方法** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **状态码** | **状态消息** | **原因和处理方法** |
| 40001000 | QUOTA\_ERROR | 检查是否开通服务。 |
| 40001001 | VOICE\_LIMIT\_ERROR | 音色克隆数量超限，目前默认1000个。 |
| 40001002 | VOICE\_PREFIX\_ERROR | 音色名前缀不满足规则：<br>- 不为空<br>  <br>- 不超过10个字符<br>  <br>- 仅包含数字和字母 |
| 40002000 | AUDIO\_URL\_ERROR | 音频URL地址无效。 |
| 40002001 | AUDIO\_DOWNLOAD\_FAIL | 下载音频失败。 |
| 40002002 | FILE\_SIZE\_EXCEED | 音频文件超过10 MB。 |
| 40002003 | AUDIO\_SAMPLE\_RATE\_ERROR | 音频采样率小于16 kHz。 |
| 40002004 | AUDIO\_FORMAT\_ERROR | 音频格式错误，解码失败，目前支持`wav`，`mp3`，`m4a`，`aac`。 |
| 40003000 | SILENT\_AUDIO\_ERROR | 音频内无足够的有效语音。 |
| 40003001 | AUDIO\_SNR\_ERROR | 音频信噪比太低。 |
| 50000000 | SERVER\_ERROR | 服务错误，一般可通过重试解决。<br>> 在使用CosyVoice声音复刻功能时，如果出现该错误，通常是因为录音质量不合格。请按照 [录音操作指南](https://help.aliyun.com/zh/isi/developer-reference/recording-operation-guide "") 中的指引重新录制声音并进行声音复刻。请注意尽量保证录制的声音无杂音，并避免频繁的不必要的停顿，确保至少有5秒以上的连续声音。 |
| - | ACCESS\_DENIED : Permission denied! | 没有权限。<br>在声音复刻时，若使用RAM子账号但未授予其 **AliyunNLSFullAccess** 权限，则会出现此错误。请 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")。 |

## **相关文档**

- [CosyVoice声音复刻API](https://help.aliyun.com/zh/isi/developer-reference/cosyvoice-sound-replica-api "")

- [语音合成CosyVoice大模型](https://help.aliyun.com/zh/isi/streaming-speech-synthesis-tts-documentation/ "")