### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[语音合成](https://help.aliyun.com/zh/model-studio/speech-synthesis-api-reference/)[实时语音合成（Qwen-TTS-Realtime）](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime-api-reference/)声音设计（Qwen）

# 千问声音设计API参考

更新时间：2026-02-11 02:27:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：声音复刻（Qwen）](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-cloning)[下一篇：语音合成（Qwen-TTS）](https://help.aliyun.com/zh/model-studio/qwen-tts-api)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

语言支持说明

如何编写高质量的声音描述？

要求与限制

核心原则

描述维度参考

示例对比

快速开始：从声音设计到语音合成

1\. 工作流程

2\. 模型配置与准备工作

3\. 示例代码

API参考

创建音色

查询音色列表

查询特定音色

删除音色

语音合成

音色配额与自动清理规则

计费说明

错误信息

声音设计通过文本描述生成定制化音色，支持多语言和多维度音色特征定义，适用于广告配音、角色塑造、有声内容创作等多种应用。声音设计与语音合成是前后关联的两个步骤。本文档聚焦于介绍声音设计的参数和接口细节，语音合成请参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "") 或 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")。

**用户指南**：关于模型介绍和选型建议请参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "") 或 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")。

## **语言支持说明**

声音设计服务支持多语言音色创建和语音合成，覆盖如下语言：中文（zh）、英文（en）、德语（de）、意大利语（it）、葡萄牙语（pt）、西班牙语（es）、日语（ja）、韩语（ko）、法语（fr）、俄语（ru）。

## **如何编写高质量的声音描述？**

### **要求与限制**

在编写声音描述（`voice_prompt`）时，请务必遵循以下技术约束：

- 长度限制：`voice_prompt` 的内容长度不得超过 2048 个字符。

- 支持语言：描述文本仅支持中文和英文。


### **核心原则**

高质量的声音描述（`voice_prompt`）是成功创建理想音色的关键。它如同声音设计的“蓝图”，直接指导模型生成具有特定特征的声音。

请遵循以下核心原则对声音进行描述：

1. 具体而非模糊：使用能够描绘具体声音特质的词语，如“低沉”、“清脆”、“语速偏快”。避免使用“好听”、“普通”等主观且缺乏信息量的词汇。

2. 多维而非单一：优秀的描述通常结合多个维度（如下文所述的性别、年龄、情感等）。单一维度的描述（如仅“女声”）过于宽泛，难以生成特色鲜明的音色。

3. 客观而非主观：专注于声音本身的物理和感知特征，而不是个人的喜好。例如，用“音调偏高，带有活力”代替“我最喜欢的声音”。

4. 原创而非模仿：请描述声音的特质，而不是要求模仿特定人物（如名人、演员）。此类请求涉及版权风险且模型不支持直接模仿。

5. 简洁而非冗余：确保每个词都有其意义。避免重复使用同义词或无意义的强调词（如“非常非常棒的声音”）。


### **描述维度参考**

| **维度** | **描述示例** |
| --- | --- |

|     |     |
| --- | --- |
| **维度** | **描述示例** |
| 性别 | 男性、女性、中性 |
| 年龄 | 儿童 (5-12岁)、青少年 (13-18岁)、青年 (19-35岁)、中年 (36-55岁)、老年 (55岁以上) |
| 音调 | 高音、中音、低音、偏高、偏低 |
| 语速 | 快速、中速、缓慢、偏快、偏慢 |
| 情感 | 开朗、沉稳、温柔、严肃、活泼、冷静、治愈 |
| 特点 | 有磁性、清脆、沙哑、圆润、甜美、浑厚、有力 |
| 用途 | 新闻播报、广告配音、有声书、动画角色、语音助手、纪录片解说 |

### 示例对比

#### ✅ 推荐示例

- “年轻活泼的女性声音，语速较快，带有明显的上扬语调，适合介绍时尚产品。”

_分析：结合了年龄、性格、语速和语调，并指明了适用场景，形象立体。_

- “沉稳的中年男性，语速缓慢，音色低沉有磁性，适合朗读新闻或纪录片解说。”

_分析：清晰定义了性别、年龄段、语速、音色特点和应用领域。_

- “可爱的儿童声音，大约8岁女孩，说话略带稚气，适合动画角色配音。”

_分析：精确到具体年龄和声音特质（稚气），目标明确。_

- “温柔知性的女性，30岁左右，语调平和，适合有声书朗读。”

_分析：通过“知性”、“平和”等词汇，有效传递了声音的情感和风格。_


#### ❌ 不推荐示例与改进建议

| **不推荐示例** | **主要问题** | **改进建议** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **不推荐示例** | **主要问题** | **改进建议** |
| 好听的声音 | 过于模糊，主观性强，缺乏可执行的特征。 | 添加具体维度，如：“声线清澈的青年女声，语调温柔”。 |
| 像某明星的声音 | 涉及版权风险，模型无法直接模仿。 | 提取其声音特质进行描述，如：“声音成熟、富有磁性、语速沉稳的男声”。 |
| 非常非常非常好听的女声 | 信息冗余，重复词汇无助于定义音色。 | 移除重复词，并增加有效描述，如：“一个20~24岁，语气轻快、音调活泼、音色甜美的女声”。 |
| 123456 | 无效输入，无法解析为声音特征。 | 请提供有意义的文本描述，参考上方的推荐示例。 |

## 快速开始：从声音设计到语音合成

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7484970771/CAEQZhiBgIDSoqeC2RkiIGVmNDNmZGJhYzhiNzQ1NmI4ZmJiMmMyMmU2ZDUzZWRj5899512_20251120114927.389.svg)

### 1\. 工作流程

声音设计与语音合成是紧密关联的两个独立步骤，遵循“先创建，后使用”的流程：

1. 准备声音设计所需的声音描述与试听文本。

   - 声音描述（voice\_prompt）：定义目标音色的特征（关于如何编写请参见“ [如何编写高质量的声音描述？](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-design#e827c8d365gwc "")”）。

   - 试听文本（preview\_text）：目标音色生成的预览音频朗读的内容（如“大家好，欢迎收听”）。
2. 调用 [创建音色](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-design#1eaa57d82did9 "") 接口，创建一个专属音色，获取音色名和预览音频。

**此步骤必须指定**`target_model` **，声明创建的音色将由哪个语音合成模型驱动**

试听获取预览音频来判断是否符合预期；若符合要求，继续下一步，否则，重新设计。

若已有创建好的音色（调用 [查询音色列表](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-design#401d33226330i "") 接口查看），可跳过这一步直接进行下一步。

3. 使用音色进行语音合成。

调用语音合成接口，传入上一步获得的音色。 **此步骤指定的语音合成模型必须和上一步的**`target_model` **一致。**


### 2\. 模型配置与准备工作

选择合适的模型并完成准备工作。

#### 模型配置

声音设计时需要指定以下两个模型：

- 声音设计模型：qwen-voice-design

- 驱动音色的语音合成模型（两类）：

  - **千问3-TTS-VD-Realtime**（参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "")）：

    - qwen3-tts-vd-realtime-2026-01-15

    - qwen3-tts-vd-realtime-2025-12-16
  - **千问3-TTS-VD**（参见 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")）：

    - qwen3-tts-vd-2026-01-26

#### 准备工作

1. **获取API Key**： [获取API Key](https://help.aliyun.com/zh/model-studio/get-api-key "")，为安全起见，推荐将API Key配置到环境变量。

2. **安装SDK**：确保已 [安装最新版DashScope SDK](https://help.aliyun.com/zh/model-studio/install-sdk "")。


### 3\. 示例代码

双向流式合成

非流式/单向流式合成

适用于千问3-TTS-VC-Realtime系列模型，更多说明请参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "")。

1. 生成专属音色并试听效果，若对效果满意，进行下一步；否则重新生成。






Python



Java

































```python
import requests
import base64
import os

def create_voice_and_play():
       # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
       # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key = "sk-xxx"
       api_key = os.getenv("DASHSCOPE_API_KEY")

       if not api_key:
           print("错误: 未找到DASHSCOPE_API_KEY环境变量，请先设置API Key")
           return None, None, None

       # 准备请求数据
       headers = {
           "Authorization": f"Bearer {api_key}",
           "Content-Type": "application/json"
       }

       data = {
           "model": "qwen-voice-design",
           "input": {
               "action": "create",
               "target_model": "qwen3-tts-vd-realtime-2026-01-15",
               "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。",
               "preview_text": "各位听众朋友，大家好，欢迎收听晚间新闻。",
               "preferred_name": "announcer",
               "language": "zh"
           },
           "parameters": {
               "sample_rate": 24000,
               "response_format": "wav"
           }
       }

       # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
       url = "https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization"

       try:
           # 发送请求
           response = requests.post(
               url,
               headers=headers,
               json=data,
               timeout=60  # 添加超时设置
           )

           if response.status_code == 200:
               result = response.json()

               # 获取音色名称
               voice_name = result["output"]["voice"]
               print(f"音色名称: {voice_name}")

               # 获取预览音频数据
               base64_audio = result["output"]["preview_audio"]["data"]

               # 解码Base64音频数据
               audio_bytes = base64.b64decode(base64_audio)

               # 保存音频文件到本地
               filename = f"{voice_name}_preview.wav"

               # 将音频数据写入本地文件
               with open(filename, 'wb') as f:
                   f.write(audio_bytes)

               print(f"音频已保存到本地文件: {filename}")
               print(f"文件路径: {os.path.abspath(filename)}")

               return voice_name, audio_bytes, filename
           else:
               print(f"请求失败，状态码: {response.status_code}")
               print(f"响应内容: {response.text}")
               return None, None, None

       except requests.exceptions.RequestException as e:
           print(f"网络请求发生错误: {e}")
           return None, None, None
       except KeyError as e:
           print(f"响应数据格式错误，缺少必要的字段: {e}")
           print(f"响应内容: {response.text if 'response' in locals() else 'No response'}")
           return None, None, None
       except Exception as e:
           print(f"发生未知错误: {e}")
           return None, None, None

if __name__ == "__main__":
       print("开始创建语音...")
       voice_name, audio_data, saved_filename = create_voice_and_play()

       if voice_name:
           print(f"\n成功创建音色 '{voice_name}'")
           print(f"音频文件已保存: '{saved_filename}'")
           print(f"文件大小: {os.path.getsize(saved_filename)} 字节")
       else:
           print("\n音色创建失败")
```





需要导入Gson依赖，若是使用Maven或者Gradle，添加依赖方式如下：







Maven



Gradle



















在`pom.xml`中添加如下内容：

















```xml
<!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
<dependency>
       <groupId>com.google.code.gson</groupId>
       <artifactId>gson</artifactId>
       <version>2.13.1</version>
</dependency>
```





在`build.gradle`中添加如下内容：

















```gradle
// https://mvnrepository.com/artifact/com.google.code.gson/gson
implementation("com.google.code.gson:gson:2.13.1")
```



















```java
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Base64;

public class Main {
       public static void main(String[] args) {
           Main example = new Main();
           example.createVoice();
       }

       public void createVoice() {
           // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
           // 若没有配置环境变量，请用百炼API Key将下行替换为：String apiKey = "sk-xxx"
           String apiKey = System.getenv("DASHSCOPE_API_KEY");

           // 创建JSON请求体字符串
           String jsonBody = "{\n" +
                   "    \"model\": \"qwen-voice-design\",\n" +
                   "    \"input\": {\n" +
                   "        \"action\": \"create\",\n" +
                   "        \"target_model\": \"qwen3-tts-vd-realtime-2026-01-15\",\n" +
                   "        \"voice_prompt\": \"沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。\",\n" +
                   "        \"preview_text\": \"各位听众朋友，大家好，欢迎收听晚间新闻。\",\n" +
                   "        \"preferred_name\": \"announcer\",\n" +
                   "        \"language\": \"zh\"\n" +
                   "    },\n" +
                   "    \"parameters\": {\n" +
                   "        \"sample_rate\": 24000,\n" +
                   "        \"response_format\": \"wav\"\n" +
                   "    }\n" +
                   "}";

           HttpURLConnection connection = null;
           try {
               // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
               URL url = new URL("https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization");
               connection = (HttpURLConnection) url.openConnection();

               // 设置请求方法和头部
               connection.setRequestMethod("POST");
               connection.setRequestProperty("Authorization", "Bearer " + apiKey);
               connection.setRequestProperty("Content-Type", "application/json");
               connection.setDoOutput(true);
               connection.setDoInput(true);

               // 发送请求体
               try (OutputStream os = connection.getOutputStream()) {
                   byte[] input = jsonBody.getBytes("UTF-8");
                   os.write(input, 0, input.length);
                   os.flush();
               }

               // 获取响应
               int responseCode = connection.getResponseCode();
               if (responseCode == HttpURLConnection.HTTP_OK) {
                   // 读取响应内容
                   StringBuilder response = new StringBuilder();
                   try (BufferedReader br = new BufferedReader(
                           new InputStreamReader(connection.getInputStream(), "UTF-8"))) {
                       String responseLine;
                       while ((responseLine = br.readLine()) != null) {
                           response.append(responseLine.trim());
                       }
                   }

                   // 解析JSON响应
                   JsonObject jsonResponse = JsonParser.parseString(response.toString()).getAsJsonObject();
                   JsonObject outputObj = jsonResponse.getAsJsonObject("output");
                   JsonObject previewAudioObj = outputObj.getAsJsonObject("preview_audio");

                   // 获取音色名称
                   String voiceName = outputObj.get("voice").getAsString();
                   System.out.println("音色名称: " + voiceName);

                   // 获取Base64编码的音频数据
                   String base64Audio = previewAudioObj.get("data").getAsString();

                   // 解码Base64音频数据
                   byte[] audioBytes = Base64.getDecoder().decode(base64Audio);

                   // 保存音频到本地文件
                   String filename = voiceName + "_preview.wav";
                   saveAudioToFile(audioBytes, filename);

                   System.out.println("音频已保存到本地文件: " + filename);

               } else {
                   // 读取错误响应
                   StringBuilder errorResponse = new StringBuilder();
                   try (BufferedReader br = new BufferedReader(
                           new InputStreamReader(connection.getErrorStream(), "UTF-8"))) {
                       String responseLine;
                       while ((responseLine = br.readLine()) != null) {
                           errorResponse.append(responseLine.trim());
                       }
                   }

                   System.out.println("请求失败，状态码: " + responseCode);
                   System.out.println("错误响应: " + errorResponse.toString());
               }

           } catch (Exception e) {
               System.err.println("请求发生错误: " + e.getMessage());
               e.printStackTrace();
           } finally {
               if (connection != null) {
                   connection.disconnect();
               }
           }
       }

       private void saveAudioToFile(byte[] audioBytes, String filename) {
           try {
               File file = new File(filename);
               try (FileOutputStream fos = new FileOutputStream(file)) {
                   fos.write(audioBytes);
               }
               System.out.println("音频已保存到: " + file.getAbsolutePath());
           } catch (IOException e) {
               System.err.println("保存音频文件时发生错误: " + e.getMessage());
               e.printStackTrace();
           }
       }
}
```

2. 使用上一步生成的专属音色进行语音合成。

这里参考了使用系统音色进行语音合成DashScope SDK的“server commit模式”示例代码，将`voice`参数替换为声音设计生成的专属音色进行语音合成。

**关键原则**：声音设计时使用的模型 (`target_model`) 必须与后续进行语音合成时使用的模型 (`model`) 保持一致，否则会导致合成失败。






Python



Java

































```python
# coding=utf-8
# Installation instructions for pyaudio:
# APPLE Mac OS X
#   brew install portaudio
#   pip install pyaudio
# Debian/Ubuntu
#   sudo apt-get install python-pyaudio python3-pyaudio
#   or
#   pip install pyaudio
# CentOS
#   sudo yum install -y portaudio portaudio-devel && pip install pyaudio
# Microsoft Windows
#   python -m pip install pyaudio

import pyaudio
import os
import base64
import threading
import time
import dashscope  # DashScope Python SDK 版本需要不低于1.23.9
from dashscope.audio.qwen_tts_realtime import QwenTtsRealtime, QwenTtsRealtimeCallback, AudioFormat

# ======= 常量配置 =======
TEXT_TO_SYNTHESIZE = [\
       '对吧~我就特别喜欢这种超市，',\
       '尤其是过年的时候',\
       '去逛超市',\
       '就会觉得',\
       '超级超级开心！',\
       '想买好多好多的东西呢！'\
]

def init_dashscope_api_key():
       """
       初始化 dashscope SDK 的 API key
       """
       # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
       # 若没有配置环境变量，请用百炼API Key将下行替换为：dashscope.api_key = "sk-xxx"
       dashscope.api_key = os.getenv("DASHSCOPE_API_KEY")

# ======= 回调类 =======
class MyCallback(QwenTtsRealtimeCallback):
       """
       自定义 TTS 流式回调
       """
       def __init__(self):
           self.complete_event = threading.Event()
           self._player = pyaudio.PyAudio()
           self._stream = self._player.open(
               format=pyaudio.paInt16, channels=1, rate=24000, output=True
           )

       def on_open(self) -> None:
           print('[TTS] 连接已建立')

       def on_close(self, close_status_code, close_msg) -> None:
           self._stream.stop_stream()
           self._stream.close()
           self._player.terminate()
           print(f'[TTS] 连接关闭 code={close_status_code}, msg={close_msg}')

       def on_event(self, response: dict) -> None:
           try:
               event_type = response.get('type', '')
               if event_type == 'session.created':
                   print(f'[TTS] 会话开始: {response["session"]["id"]}')
               elif event_type == 'response.audio.delta':
                   audio_data = base64.b64decode(response['delta'])
                   self._stream.write(audio_data)
               elif event_type == 'response.done':
                   print(f'[TTS] 响应完成, Response ID: {qwen_tts_realtime.get_last_response_id()}')
               elif event_type == 'session.finished':
                   print('[TTS] 会话结束')
                   self.complete_event.set()
           except Exception as e:
               print(f'[Error] 处理回调事件异常: {e}')

       def wait_for_finished(self):
           self.complete_event.wait()

# ======= 主执行逻辑 =======
if __name__ == '__main__':
       init_dashscope_api_key()
       print('[系统] 初始化 Qwen TTS Realtime ...')

       callback = MyCallback()
       qwen_tts_realtime = QwenTtsRealtime(
           # 声音设计、语音合成要使用相同的模型
           model="qwen3-tts-vd-realtime-2026-01-15",
           callback=callback,
           # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/realtime
           url='wss://dashscope.aliyuncs.com/api-ws/v1/realtime'
       )
       qwen_tts_realtime.connect()

       qwen_tts_realtime.update_session(
           voice="myvoice", # 将voice参数替换为声音设计生成的专属音色
           response_format=AudioFormat.PCM_24000HZ_MONO_16BIT,
           mode='server_commit'
       )

       for text_chunk in TEXT_TO_SYNTHESIZE:
           print(f'[发送文本]: {text_chunk}')
           qwen_tts_realtime.append_text(text_chunk)
           time.sleep(0.1)

       qwen_tts_realtime.finish()
       callback.wait_for_finished()

       print(f'[Metric] session_id={qwen_tts_realtime.get_session_id()}, '
             f'first_audio_delay={qwen_tts_realtime.get_first_audio_delay()}s')
```



















```java
import com.alibaba.dashscope.audio.qwen_tts_realtime.*;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.google.gson.JsonObject;

import javax.sound.sampled.*;
import java.io.*;
import java.util.Base64;
import java.util.Queue;
import java.util.concurrent.CountDownLatch;
import java.util.concurrent.atomic.AtomicReference;
import java.util.concurrent.ConcurrentLinkedQueue;
import java.util.concurrent.atomic.AtomicBoolean;

public class Main {
       // ===== 常量定义 =====
       private static String[] textToSynthesize = {
               "对吧~我就特别喜欢这种超市",
               "尤其是过年的时候",
               "去逛超市",
               "就会觉得",
               "超级超级开心！",
               "想买好多好多的东西呢！"
       };

       // 实时音频播放器类
       public static class RealtimePcmPlayer {
           private int sampleRate;
           private SourceDataLine line;
           private AudioFormat audioFormat;
           private Thread decoderThread;
           private Thread playerThread;
           private AtomicBoolean stopped = new AtomicBoolean(false);
           private Queue<String> b64AudioBuffer = new ConcurrentLinkedQueue<>();
           private Queue<byte[]> RawAudioBuffer = new ConcurrentLinkedQueue<>();

           // 构造函数初始化音频格式和音频线路
           public RealtimePcmPlayer(int sampleRate) throws LineUnavailableException {
               this.sampleRate = sampleRate;
               this.audioFormat = new AudioFormat(this.sampleRate, 16, 1, true, false);
               DataLine.Info info = new DataLine.Info(SourceDataLine.class, audioFormat);
               line = (SourceDataLine) AudioSystem.getLine(info);
               line.open(audioFormat);
               line.start();
               decoderThread = new Thread(new Runnable() {
                   @Override
                   public void run() {
                       while (!stopped.get()) {
                           String b64Audio = b64AudioBuffer.poll();
                           if (b64Audio != null) {
                               byte[] rawAudio = Base64.getDecoder().decode(b64Audio);
                               RawAudioBuffer.add(rawAudio);
                           } else {
                               try {
                                   Thread.sleep(100);
                               } catch (InterruptedException e) {
                                   throw new RuntimeException(e);
                               }
                           }
                       }
                   }
               });
               playerThread = new Thread(new Runnable() {
                   @Override
                   public void run() {
                       while (!stopped.get()) {
                           byte[] rawAudio = RawAudioBuffer.poll();
                           if (rawAudio != null) {
                               try {
                                   playChunk(rawAudio);
                               } catch (IOException e) {
                                   throw new RuntimeException(e);
                               } catch (InterruptedException e) {
                                   throw new RuntimeException(e);
                               }
                           } else {
                               try {
                                   Thread.sleep(100);
                               } catch (InterruptedException e) {
                                   throw new RuntimeException(e);
                               }
                           }
                       }
                   }
               });
               decoderThread.start();
               playerThread.start();
           }

           // 播放一个音频块并阻塞直到播放完成
           private void playChunk(byte[] chunk) throws IOException, InterruptedException {
               if (chunk == null || chunk.length == 0) return;

               int bytesWritten = 0;
               while (bytesWritten < chunk.length) {
                   bytesWritten += line.write(chunk, bytesWritten, chunk.length - bytesWritten);
               }
               int audioLength = chunk.length / (this.sampleRate*2/1000);
               // 等待缓冲区中的音频播放完成
               Thread.sleep(audioLength - 10);
           }

           public void write(String b64Audio) {
               b64AudioBuffer.add(b64Audio);
           }

           public void cancel() {
               b64AudioBuffer.clear();
               RawAudioBuffer.clear();
           }

           public void waitForComplete() throws InterruptedException {
               while (!b64AudioBuffer.isEmpty() || !RawAudioBuffer.isEmpty()) {
                   Thread.sleep(100);
               }
               line.drain();
           }

           public void shutdown() throws InterruptedException {
               stopped.set(true);
               decoderThread.join();
               playerThread.join();
               if (line != null && line.isRunning()) {
                   line.drain();
                   line.close();
               }
           }
       }

       public static void main(String[] args) throws Exception {
           QwenTtsRealtimeParam param = QwenTtsRealtimeParam.builder()
                   // 声音设计、语音合成要使用相同的模型
                   .model("qwen3-tts-vd-realtime-2026-01-15")
                   // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：wss://dashscope-intl.aliyuncs.com/api-ws/v1/realtime
                   .url("wss://dashscope.aliyuncs.com/api-ws/v1/realtime")
                   // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                   // 若没有配置环境变量，请用百炼API Key将下行替换为：.apikey("sk-xxx")
                   .apikey(System.getenv("DASHSCOPE_API_KEY"))
                   .build();
           AtomicReference<CountDownLatch> completeLatch = new AtomicReference<>(new CountDownLatch(1));
           final AtomicReference<QwenTtsRealtime> qwenTtsRef = new AtomicReference<>(null);

           // 创建实时音频播放器实例
           RealtimePcmPlayer audioPlayer = new RealtimePcmPlayer(24000);

           QwenTtsRealtime qwenTtsRealtime = new QwenTtsRealtime(param, new QwenTtsRealtimeCallback() {
               @Override
               public void onOpen() {
                   // 连接建立时的处理
               }
               @Override
               public void onEvent(JsonObject message) {
                   String type = message.get("type").getAsString();
                   switch(type) {
                       case "session.created":
                           // 会话创建时的处理
                           break;
                       case "response.audio.delta":
                           String recvAudioB64 = message.get("delta").getAsString();
                           // 实时播放音频
                           audioPlayer.write(recvAudioB64);
                           break;
                       case "response.done":
                           // 响应完成时的处理
                           break;
                       case "session.finished":
                           // 会话结束时的处理
                           completeLatch.get().countDown();
                       default:
                           break;
                   }
               }
               @Override
               public void onClose(int code, String reason) {
                   // 连接关闭时的处理
               }
           });
           qwenTtsRef.set(qwenTtsRealtime);
           try {
               qwenTtsRealtime.connect();
           } catch (NoApiKeyException e) {
               throw new RuntimeException(e);
           }
           QwenTtsRealtimeConfig config = QwenTtsRealtimeConfig.builder()
                   .voice("myvoice") // 将voice参数替换为声音设计生成的专属音色
                   .responseFormat(QwenTtsRealtimeAudioFormat.PCM_24000HZ_MONO_16BIT)
                   .mode("server_commit")
                   .build();
           qwenTtsRealtime.updateSession(config);
           for (String text:textToSynthesize) {
               qwenTtsRealtime.appendText(text);
               Thread.sleep(100);
           }
           qwenTtsRealtime.finish();
           completeLatch.get().await();

           // 等待音频播放完成并关闭播放器
           audioPlayer.waitForComplete();
           audioPlayer.shutdown();
           System.exit(0);
       }
}
```


适用于千问3-TTS-VC系列模型，更多说明请参见 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")。

1. 生成专属音色并试听效果，若对效果满意，进行下一步；否则重新生成。






Python



Java

































```python
import requests
import base64
import os

def create_voice_and_play():
       # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
       # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key = "sk-xxx"
       api_key = os.getenv("DASHSCOPE_API_KEY")

       if not api_key:
           print("错误: 未找到DASHSCOPE_API_KEY环境变量，请先设置API Key")
           return None, None, None

       # 准备请求数据
       headers = {
           "Authorization": f"Bearer {api_key}",
           "Content-Type": "application/json"
       }

       data = {
           "model": "qwen-voice-design",
           "input": {
               "action": "create",
               "target_model": "qwen3-tts-vd-2026-01-26",
               "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。",
               "preview_text": "各位听众朋友，大家好，欢迎收听晚间新闻。",
               "preferred_name": "announcer",
               "language": "zh"
           },
           "parameters": {
               "sample_rate": 24000,
               "response_format": "wav"
           }
       }

       # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
       url = "https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization"

       try:
           # 发送请求
           response = requests.post(
               url,
               headers=headers,
               json=data,
               timeout=60  # 添加超时设置
           )

           if response.status_code == 200:
               result = response.json()

               # 获取音色名称
               voice_name = result["output"]["voice"]
               print(f"音色名称: {voice_name}")

               # 获取预览音频数据
               base64_audio = result["output"]["preview_audio"]["data"]

               # 解码Base64音频数据
               audio_bytes = base64.b64decode(base64_audio)

               # 保存音频文件到本地
               filename = f"{voice_name}_preview.wav"

               # 将音频数据写入本地文件
               with open(filename, 'wb') as f:
                   f.write(audio_bytes)

               print(f"音频已保存到本地文件: {filename}")
               print(f"文件路径: {os.path.abspath(filename)}")

               return voice_name, audio_bytes, filename
           else:
               print(f"请求失败，状态码: {response.status_code}")
               print(f"响应内容: {response.text}")
               return None, None, None

       except requests.exceptions.RequestException as e:
           print(f"网络请求发生错误: {e}")
           return None, None, None
       except KeyError as e:
           print(f"响应数据格式错误，缺少必要的字段: {e}")
           print(f"响应内容: {response.text if 'response' in locals() else 'No response'}")
           return None, None, None
       except Exception as e:
           print(f"发生未知错误: {e}")
           return None, None, None

if __name__ == "__main__":
       print("开始创建语音...")
       voice_name, audio_data, saved_filename = create_voice_and_play()

       if voice_name:
           print(f"\n成功创建音色 '{voice_name}'")
           print(f"音频文件已保存: '{saved_filename}'")
           print(f"文件大小: {os.path.getsize(saved_filename)} 字节")
       else:
           print("\n音色创建失败")
```





需要导入Gson依赖，若是使用Maven或者Gradle，添加依赖方式如下：







Maven



Gradle



















在`pom.xml`中添加如下内容：

















```xml
<!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
<dependency>
       <groupId>com.google.code.gson</groupId>
       <artifactId>gson</artifactId>
       <version>2.13.1</version>
</dependency>
```





在`build.gradle`中添加如下内容：

















```gradle
// https://mvnrepository.com/artifact/com.google.code.gson/gson
implementation("com.google.code.gson:gson:2.13.1")
```







**重要**





使用声音设计生成的专属音色进行语音合成时，必须按照如下方式设置音色：

















```java
MultiModalConversationParam param = MultiModalConversationParam.builder()
                   .parameter("voice", "your_voice") // 将voice参数替换为声音设计生成的专属音色
                   .build();
```























```java
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Base64;

public class Main {
       public static void main(String[] args) {
           Main example = new Main();
           example.createVoice();
       }

       public void createVoice() {
           // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
           // 若没有配置环境变量，请用百炼API Key将下行替换为：String apiKey = "sk-xxx"
           String apiKey = System.getenv("DASHSCOPE_API_KEY");

           // 创建JSON请求体字符串
           String jsonBody = "{\n" +
                   "    \"model\": \"qwen-voice-design\",\n" +
                   "    \"input\": {\n" +
                   "        \"action\": \"create\",\n" +
                   "        \"target_model\": \"qwen3-tts-vd-2026-01-26\",\n" +
                   "        \"voice_prompt\": \"沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。\",\n" +
                   "        \"preview_text\": \"各位听众朋友，大家好，欢迎收听晚间新闻。\",\n" +
                   "        \"preferred_name\": \"announcer\",\n" +
                   "        \"language\": \"zh\"\n" +
                   "    },\n" +
                   "    \"parameters\": {\n" +
                   "        \"sample_rate\": 24000,\n" +
                   "        \"response_format\": \"wav\"\n" +
                   "    }\n" +
                   "}";

           HttpURLConnection connection = null;
           try {
               // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
               URL url = new URL("https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization");
               connection = (HttpURLConnection) url.openConnection();

               // 设置请求方法和头部
               connection.setRequestMethod("POST");
               connection.setRequestProperty("Authorization", "Bearer " + apiKey);
               connection.setRequestProperty("Content-Type", "application/json");
               connection.setDoOutput(true);
               connection.setDoInput(true);

               // 发送请求体
               try (OutputStream os = connection.getOutputStream()) {
                   byte[] input = jsonBody.getBytes("UTF-8");
                   os.write(input, 0, input.length);
                   os.flush();
               }

               // 获取响应
               int responseCode = connection.getResponseCode();
               if (responseCode == HttpURLConnection.HTTP_OK) {
                   // 读取响应内容
                   StringBuilder response = new StringBuilder();
                   try (BufferedReader br = new BufferedReader(
                           new InputStreamReader(connection.getInputStream(), "UTF-8"))) {
                       String responseLine;
                       while ((responseLine = br.readLine()) != null) {
                           response.append(responseLine.trim());
                       }
                   }

                   // 解析JSON响应
                   JsonObject jsonResponse = JsonParser.parseString(response.toString()).getAsJsonObject();
                   JsonObject outputObj = jsonResponse.getAsJsonObject("output");
                   JsonObject previewAudioObj = outputObj.getAsJsonObject("preview_audio");

                   // 获取音色名称
                   String voiceName = outputObj.get("voice").getAsString();
                   System.out.println("音色名称: " + voiceName);

                   // 获取Base64编码的音频数据
                   String base64Audio = previewAudioObj.get("data").getAsString();

                   // 解码Base64音频数据
                   byte[] audioBytes = Base64.getDecoder().decode(base64Audio);

                   // 保存音频到本地文件
                   String filename = voiceName + "_preview.wav";
                   saveAudioToFile(audioBytes, filename);

                   System.out.println("音频已保存到本地文件: " + filename);

               } else {
                   // 读取错误响应
                   StringBuilder errorResponse = new StringBuilder();
                   try (BufferedReader br = new BufferedReader(
                           new InputStreamReader(connection.getErrorStream(), "UTF-8"))) {
                       String responseLine;
                       while ((responseLine = br.readLine()) != null) {
                           errorResponse.append(responseLine.trim());
                       }
                   }

                   System.out.println("请求失败，状态码: " + responseCode);
                   System.out.println("错误响应: " + errorResponse.toString());
               }

           } catch (Exception e) {
               System.err.println("请求发生错误: " + e.getMessage());
               e.printStackTrace();
           } finally {
               if (connection != null) {
                   connection.disconnect();
               }
           }
       }

       private void saveAudioToFile(byte[] audioBytes, String filename) {
           try {
               File file = new File(filename);
               try (FileOutputStream fos = new FileOutputStream(file)) {
                   fos.write(audioBytes);
               }
               System.out.println("音频已保存到: " + file.getAbsolutePath());
           } catch (IOException e) {
               System.err.println("保存音频文件时发生错误: " + e.getMessage());
               e.printStackTrace();
           }
       }
}
```

2. 使用上一步生成的专属音色进行语音合成（非流式合成）。

这里参考了使用系统音色进行语音合成DashScope SDK的“非流式输出”示例代码，将`voice`参数替换为声音设计生成的专属音色进行语音合成。单向流式合成请参见 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts#c204937c02gsb "")。

**关键原则**：声音设计时使用的模型 (`target_model`) 必须与后续进行语音合成时使用的模型 (`model`) 保持一致，否则会导致合成失败。






Python



Java

































```python
import os
import dashscope


if __name__ == '__main__':
       # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
       dashscope.base_http_api_url = 'https://dashscope.aliyuncs.com/api/v1'

       text = "今天天气怎么样？"
       # SpeechSynthesizer接口使用方法：dashscope.audio.qwen_tts.SpeechSynthesizer.call(...)
       response = dashscope.MultiModalConversation.call(
           model="qwen3-tts-vd-2026-01-26",
           # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
           # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key = "sk-xxx"
           api_key=os.getenv("DASHSCOPE_API_KEY"),
           text=text,
           voice="myvoice", # 将voice参数替换为声音设计生成的专属音色
           stream=False
       )
       print(response)
```



















```java
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversation;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationParam;
import com.alibaba.dashscope.aigc.multimodalconversation.MultiModalConversationResult;
import com.alibaba.dashscope.exception.ApiException;
import com.alibaba.dashscope.exception.NoApiKeyException;
import com.alibaba.dashscope.exception.UploadFileException;

import com.alibaba.dashscope.utils.Constants;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.URL;

public class Main {
       private static final String MODEL = "qwen3-tts-vd-2026-01-26";
       public static void call() throws ApiException, NoApiKeyException, UploadFileException {
           MultiModalConversation conv = new MultiModalConversation();
           MultiModalConversationParam param = MultiModalConversationParam.builder()
                   // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
                   // 若没有配置环境变量，请用百炼API Key将下行替换为：.apiKey("sk-xxx")
                   .apiKey(System.getenv("DASHSCOPE_API_KEY"))
                   .model(MODEL)
                   .text("Today is a wonderful day to build something people love!")
                   .parameter("voice", "myvoice") // 将voice参数替换为声音设计生成的专属音色
                   .build();
           MultiModalConversationResult result = conv.call(param);
           String audioUrl = result.getOutput().getAudio().getUrl();
           System.out.print(audioUrl);

           // 下载音频文件到本地
           try (InputStream in = new URL(audioUrl).openStream();
                FileOutputStream out = new FileOutputStream("downloaded_audio.wav")) {
               byte[] buffer = new byte[1024];
               int bytesRead;
               while ((bytesRead = in.read(buffer)) != -1) {
                   out.write(buffer, 0, bytesRead);
               }
               System.out.println("\n音频文件已下载到本地: downloaded_audio.wav");
           } catch (Exception e) {
               System.out.println("\n下载音频文件时出错: " + e.getMessage());
           }
       }
       public static void main(String[] args) {
           try {
               // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1
               Constants.baseHttpApiUrl = "https://dashscope.aliyuncs.com/api/v1";
               call();
           } catch (ApiException | NoApiKeyException | UploadFileException e) {
               System.out.println(e.getMessage());
           }
           System.exit(0);
       }
}
```


## **API参考**

使用不同 API 时，请确保使用同一账号进行操作。

### **创建音色**

输入声音描述和试听文本，创建自定义音色。

- **URL**

中国内地：















```http
POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization
```



国际：















```http
POST https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
```

- **请求头**




| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| Authorization | string | 支持 | 鉴权令牌，格式为`Bearer <your_api_key>`，使用时，将“`<your_api_key>`”替换为实际的API Key。 |
| Content-Type | string | 支持 | 请求体中传输的数据的媒体类型。固定为`application/json`。 |

- **消息体**

包含所有请求参数的消息体如下，对于可选字段，在实际业务中可根据需求省略。



**重要**





注意区分如下参数：



  - `model`：声音设计模型，固定为qwen-voice-design

  - `target_model`：驱动音色的语音合成模型，须和后续调用语音合成接口时使用的语音合成模型一致，否则合成会失败


```json
{
    "model": "qwen-voice-design",
    "input": {
        "action": "create",
        "target_model": "qwen3-tts-vd-realtime-2026-01-15",
        "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。",
        "preview_text": "各位听众朋友，大家好，欢迎收听晚间新闻。",
        "preferred_name": "announcer",
        "language": "zh"
    },
    "parameters": {
        "sample_rate": 24000,
        "response_format": "wav"
    }
}
```

- **请求参数**




| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| model | string | - | 支持 | 声音设计模型，固定为`qwen-voice-design`。 |
| action | string | - | 支持 | 操作类型，固定为`create`。 |
| target\_model | string | - | 支持 | 驱动音色的语音合成模型，支持的模型有（两类）：<br>  - **千问3-TTS-VD-Realtime**（参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "")）：<br>    <br>    - qwen3-tts-vd-realtime-2026-01-15<br>      <br>    - qwen3-tts-vd-realtime-2025-12-16<br>  - **千问3-TTS-VD**（参见 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")）：<br>    <br>    - qwen3-tts-vd-2026-01-26<br>必须与后续调用语音合成接口时使用的语音合成模型一致，否则合成会失败。 |
| voice\_prompt | string | - | 支持 | 声音描述。最大长度 2048 字符。<br>只支持中文和英文。<br>关于如何编写声音描述，请参见“ [如何编写高质量的声音描述？](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-design#e827c8d365gwc "")”。 |
| preview\_text | string | - | 支持 | 预览音频对应的文本。最大长度 1024 字符。<br>支持中文（zh）、英文（en）、德语（de）、意大利语（it）、葡萄牙语（pt）、西班牙语（es）、日语（ja）、韩语（ko）、法语（fr）、俄语（ru）。 |
| preferred\_name | string | - | 支持 | 为音色指定一个便于识别的名称（仅允许数字、英文字母和下划线，不超过16个字符）。建议选用与角色、场景相关的标识。<br>> 该关键字会在设计的音色名中出现，例如关键字为“announcer”，最终音色名为“qwen-tts-vd-announcer-voice-20251201102800-a1b2” |
| language | string | zh | 不支持 | 语言代码，指定声音设计生成音色的语言倾向。该参数影响生成音色的语言特征和发音倾向，建议根据实际使用场景选择对应语言代码。<br>若使用该参数，设置的语种要和`preview_text`的语种一致。<br>取值范围：`zh`（中文）、`en`（英文）、`de`（德语）、`it`（意大利语）、`pt`（葡萄牙语）、`es`（西班牙语）、`ja`（日语）、`ko`（韩语）、`fr`（法语）、`ru`（俄语）。 |
| sample\_rate | int | 24000 | 不支持 | 声音设计生成的预览音频采样率（单位：Hz）。<br>取值范围：<br>  - 8000<br>    <br>  - 16000<br>    <br>  - 24000<br>    <br>  - 48000 |
| response\_format | string | wav | 不支持 | 声音设计生成的预览音频格式。<br>取值范围：<br>  - pcm<br>    <br>  - wav<br>    <br>  - mp3<br>    <br>  - opus |

- **响应参数**



**点击查看响应示例**




















```json
{
      "output": {
          "preview_audio": {
              "data": "{base64_encoded_audio}",
              "sample_rate": 24000,
              "response_format": "wav"
          },
          "target_model": "qwen3-tts-vd-realtime-2026-01-15",
          "voice": "yourVoice"
      },
      "usage": {
          "count": 1
      },
      "request_id": "yourRequestId"
}
```






需关注的参数如下：




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| voice | string | 音色名称，可直接用于语音合成接口的`voice`参数。 |
| data | string | 声音设计生成的预览音频数据，以 Base64 编码字符串形式返回。 |
| sample\_rate | int | 声音设计生成的预览音频采样率（单位：Hz），与音色创建时的采样率一致，未指定则默认为 24000 Hz。 |
| response\_format | string | 声音设计生成的预览音频格式，与音色创建时的音频格式一致，未指定则默认为wav。 |
| target\_model | string | 驱动音色的语音合成模型，支持的模型有（两类）：<br>  - **千问3-TTS-VD-Realtime**（参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "")）：<br>    <br>    - qwen3-tts-vd-realtime-2026-01-15<br>      <br>    - qwen3-tts-vd-realtime-2025-12-16<br>  - **千问3-TTS-VD**（参见 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")）：<br>    <br>    - qwen3-tts-vd-2026-01-26<br>必须与后续调用语音合成接口时使用的语音合成模型一致，否则合成会失败。 |
| request\_id | string | Request ID。 |
| count | integer | 本次请求实际计入费用的“创建音色”次数，本次请求的费用为count×0.2元。<br> <br>创建音色时，count恒为1。 |

- **示例代码**



**重要**





注意区分如下参数：



  - `model`：声音设计模型，固定为qwen-voice-design

  - `target_model`：驱动音色的语音合成模型，须和后续调用语音合成接口时使用的语音合成模型一致，否则合成会失败


cURL

Python

Java

若未将API Key配置到环境变量，需将示例中的`$DASHSCOPE_API_KEY`替换为实际的API Key。

```curl
# ======= 重要提示 =======
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
# 新加坡地域和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# === 执行时请删除该注释 ===

curl -X POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization \
-H "Authorization: Bearer $DASHSCOPE_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "model": "qwen-voice-design",
    "input": {
        "action": "create",
        "target_model": "qwen3-tts-vd-realtime-2026-01-15",
        "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。",
        "preview_text": "各位听众朋友，大家好，欢迎收听晚间新闻。",
        "preferred_name": "announcer",
        "language": "zh"
    },
    "parameters": {
        "sample_rate": 24000,
        "response_format": "wav"
    }
}'
```

```python
import requests
import base64
import os

def create_voice_and_play():
    # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key = "sk-xxx"
    api_key = os.getenv("DASHSCOPE_API_KEY")

    if not api_key:
        print("错误: 未找到DASHSCOPE_API_KEY环境变量，请先设置API Key")
        return None, None, None

    # 准备请求数据
    headers = {
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json"
    }

    data = {
        "model": "qwen-voice-design",
        "input": {
            "action": "create",
            "target_model": "qwen3-tts-vd-realtime-2026-01-15",
            "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。",
            "preview_text": "各位听众朋友，大家好，欢迎收听晚间新闻。",
            "preferred_name": "announcer",
            "language": "zh"
        },
        "parameters": {
            "sample_rate": 24000,
            "response_format": "wav"
        }
    }

    # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
    url = "https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization"

    try:
        # 发送请求
        response = requests.post(
            url,
            headers=headers,
            json=data,
            timeout=60  # 添加超时设置
        )

        if response.status_code == 200:
            result = response.json()

            # 获取音色名称
            voice_name = result["output"]["voice"]
            print(f"音色名称: {voice_name}")

            # 获取预览音频数据
            base64_audio = result["output"]["preview_audio"]["data"]

            # 解码Base64音频数据
            audio_bytes = base64.b64decode(base64_audio)

            # 保存音频文件到本地
            filename = f"{voice_name}_preview.wav"

            # 将音频数据写入本地文件
            with open(filename, 'wb') as f:
                f.write(audio_bytes)

            print(f"音频已保存到本地文件: {filename}")
            print(f"文件路径: {os.path.abspath(filename)}")

            return voice_name, audio_bytes, filename
        else:
            print(f"请求失败，状态码: {response.status_code}")
            print(f"响应内容: {response.text}")
            return None, None, None

    except requests.exceptions.RequestException as e:
        print(f"网络请求发生错误: {e}")
        return None, None, None
    except KeyError as e:
        print(f"响应数据格式错误，缺少必要的字段: {e}")
        print(f"响应内容: {response.text if 'response' in locals() else 'No response'}")
        return None, None, None
    except Exception as e:
        print(f"发生未知错误: {e}")
        return None, None, None

if __name__ == "__main__":
    print("开始创建语音...")
    voice_name, audio_data, saved_filename = create_voice_and_play()

    if voice_name:
        print(f"\n成功创建音色 '{voice_name}'")
        print(f"音频文件已保存: '{saved_filename}'")
        print(f"文件大小: {os.path.getsize(saved_filename)} 字节")
    else:
        print("\n音色创建失败")
```

```java
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Base64;

public class Main {
    public static void main(String[] args) {
        Main example = new Main();
        example.createVoice();
    }

    public void createVoice() {
        // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
        // 若没有配置环境变量，请用百炼API Key将下行替换为：String apiKey = "sk-xxx"
        String apiKey = System.getenv("DASHSCOPE_API_KEY");

        // 创建JSON请求体字符串
        String jsonBody = "{\n" +
                "    \"model\": \"qwen-voice-design\",\n" +
                "    \"input\": {\n" +
                "        \"action\": \"create\",\n" +
                "        \"target_model\": \"qwen3-tts-vd-realtime-2026-01-15\",\n" +
                "        \"voice_prompt\": \"沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。\",\n" +
                "        \"preview_text\": \"各位听众朋友，大家好，欢迎收听晚间新闻。\",\n" +
                "        \"preferred_name\": \"announcer\",\n" +
                "        \"language\": \"zh\"\n" +
                "    },\n" +
                "    \"parameters\": {\n" +
                "        \"sample_rate\": 24000,\n" +
                "        \"response_format\": \"wav\"\n" +
                "    }\n" +
                "}";

        HttpURLConnection connection = null;
        try {
            // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
            URL url = new URL("https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization");
            connection = (HttpURLConnection) url.openConnection();

            // 设置请求方法和头部
            connection.setRequestMethod("POST");
            connection.setRequestProperty("Authorization", "Bearer " + apiKey);
            connection.setRequestProperty("Content-Type", "application/json");
            connection.setDoOutput(true);
            connection.setDoInput(true);

            // 发送请求体
            try (OutputStream os = connection.getOutputStream()) {
                byte[] input = jsonBody.getBytes("UTF-8");
                os.write(input, 0, input.length);
                os.flush();
            }

            // 获取响应
            int responseCode = connection.getResponseCode();
            if (responseCode == HttpURLConnection.HTTP_OK) {
                // 读取响应内容
                StringBuilder response = new StringBuilder();
                try (BufferedReader br = new BufferedReader(
                        new InputStreamReader(connection.getInputStream(), "UTF-8"))) {
                    String responseLine;
                    while ((responseLine = br.readLine()) != null) {
                        response.append(responseLine.trim());
                    }
                }

                // 解析JSON响应
                JsonObject jsonResponse = JsonParser.parseString(response.toString()).getAsJsonObject();
                JsonObject outputObj = jsonResponse.getAsJsonObject("output");
                JsonObject previewAudioObj = outputObj.getAsJsonObject("preview_audio");

                // 获取音色名称
                String voiceName = outputObj.get("voice").getAsString();
                System.out.println("音色名称: " + voiceName);

                // 获取Base64编码的音频数据
                String base64Audio = previewAudioObj.get("data").getAsString();

                // 解码Base64音频数据
                byte[] audioBytes = Base64.getDecoder().decode(base64Audio);

                // 保存音频到本地文件
                String filename = voiceName + "_preview.wav";
                saveAudioToFile(audioBytes, filename);

                System.out.println("音频已保存到本地文件: " + filename);

            } else {
                // 读取错误响应
                StringBuilder errorResponse = new StringBuilder();
                try (BufferedReader br = new BufferedReader(
                        new InputStreamReader(connection.getErrorStream(), "UTF-8"))) {
                    String responseLine;
                    while ((responseLine = br.readLine()) != null) {
                        errorResponse.append(responseLine.trim());
                    }
                }

                System.out.println("请求失败，状态码: " + responseCode);
                System.out.println("错误响应: " + errorResponse.toString());
            }

        } catch (Exception e) {
            System.err.println("请求发生错误: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (connection != null) {
                connection.disconnect();
            }
        }
    }

    private void saveAudioToFile(byte[] audioBytes, String filename) {
        try {
            File file = new File(filename);
            try (FileOutputStream fos = new FileOutputStream(file)) {
                fos.write(audioBytes);
            }
            System.out.println("音频已保存到: " + file.getAbsolutePath());
        } catch (IOException e) {
            System.err.println("保存音频文件时发生错误: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### **查询音色列表**

分页查询已创建的音色列表。

- **URL**

中国内地：















```http
POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization
```



国际：















```http
POST https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
```

- **请求头**




| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| Authorization | string | 支持 | 鉴权令牌，格式为`Bearer <your_api_key>`，使用时，将“`<your_api_key>`”替换为实际的API Key。 |
| Content-Type | string | 支持 | 请求体中传输的数据的媒体类型。固定为`application/json`。 |

- **消息体**

包含所有请求参数的消息体如下，对于可选字段，在实际业务中可根据需求省略。



**重要**





`model`：声音设计模型，固定为`qwen-voice-design`，请勿修改。



















```json
{
      "model": "qwen-voice-design",
      "input": {
          "action": "list",
          "page_size": 10,
          "page_index": 0
      }
}
```

- **请求参数**




| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| model | string | - | 支持 | 声音设计模型，固定为`qwen-voice-design`。 |
| action | string | - | 支持 | 操作类型，固定为`list`。 |
| page\_index | integer | 0 | 不支持 | 页码索引。取值范围：\[0, 200\]。 |
| page\_size | integer | 10 | 不支持 | 每页包含数据条数。取值范围：大于0即可。 |

- **响应参数**



**点击查看响应示例**




















```json
{
      "output": {
          "page_index": 0,
          "page_size": 2,
          "total_count": 26,
          "voice_list": [\
              {\
                  "gmt_create": "2025-12-10 17:04:54",\
                  "gmt_modified": "2025-12-10 17:04:54",\
                  "language": "zh",\
                  "preview_text": "各位听众朋友们，大家好，欢迎收听今天的节目。",\
                  "target_model": "qwen3-tts-vd-realtime-2026-01-15",\
                  "voice": "yourVoice1",\
                  "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。，低沉有磁性，语速平稳"\
              },\
              {\
                  "gmt_create": "2025-12-10 15:31:35",\
                  "gmt_modified": "2025-12-10 15:31:35",\
                  "language": "zh",\
                  "preview_text": "各位听众朋友们，大家好",\
                  "target_model": "qwen3-tts-vd-realtime-2026-01-15",\
                  "voice": "yourVoice2",\
                  "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。"\
              }\
          ]
      },
      "usage": {},
      "request_id": "yourRequestId"
}
```






需关注的参数如下：




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| voice | string | 音色名称，可直接用于语音合成接口的`voice`参数。 |
| target\_model | string | 驱动音色的语音合成模型，支持的模型有（两类）：<br>  - **千问3-TTS-VD-Realtime**（参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "")）：<br>    <br>    - qwen3-tts-vd-realtime-2026-01-15<br>      <br>    - qwen3-tts-vd-realtime-2025-12-16<br>  - **千问3-TTS-VD**（参见 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")）：<br>    <br>    - qwen3-tts-vd-2026-01-26<br>必须与后续调用语音合成接口时使用的语音合成模型一致，否则合成会失败。 |
| language | string | 语言代码。<br>取值范围：`zh`（中文）、`en`（英文）、`de`（德语）、`it`（意大利语）、`pt`（葡萄牙语）、`es`（西班牙语）、`ja`（日语）、`ko`（韩语）、`fr`（法语）、`ru`（俄语）。 |
| voice\_prompt | string | 声音描述。 |
| preview\_text | string | 试听文本。 |
| gmt\_create | string | 创建音色的时间。 |
| gmt\_modified | string | 修改音色的时间。 |
| page\_index | integer | 页码索引。 |
| page\_size | integer | 每页包含数据条数。 |
| total\_count | integer | 查询得到的数据总条数。 |
| request\_id | string | Request ID。 |

- **示例代码**



**重要**





`model`：声音设计模型，固定为`qwen-voice-design`，请勿修改。










cURL



Python



Java



















若未将API Key配置到环境变量，需将示例中的`$DASHSCOPE_API_KEY`替换为实际的API Key。

















```curl
# ======= 重要提示 =======
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
# 新加坡地域和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# === 执行时请删除该注释 ===

curl -X POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization \
  -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "model": "qwen-voice-design",
      "input": {
          "action": "list",
          "page_size": 10,
          "page_index": 0
      }
}'
```



















```python
import os
import requests

# 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# 若没有配置环境变量，请用百炼API Key将下行替换为：api_key = "sk-xxx"
api_key = os.getenv("DASHSCOPE_API_KEY")
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
url = "https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization"

payload = {
      "model": "qwen-voice-design", # 不要修改该值
      "input": {
          "action": "list",
          "page_size": 10,
          "page_index": 0
      }
}

headers = {
      "Authorization": f"Bearer {api_key}",
      "Content-Type": "application/json"
}

response = requests.post(url, json=payload, headers=headers)

print("HTTP 状态码:", response.status_code)

if response.status_code == 200:
      data = response.json()
      voice_list = data["output"]["voice_list"]

      print("查询到的音色列表：")
      for item in voice_list:
          print(f"- 音色: {item['voice']}  创建时间: {item['gmt_create']}  模型: {item['target_model']}")
else:
      print("请求失败:", response.text)
```



















```java
import com.google.gson.Gson;
import com.google.gson.JsonArray;
import com.google.gson.JsonObject;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
      public static void main(String[] args) {
          // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
          // 若没有配置环境变量，请用百炼API Key将下行替换为：String apiKey = "sk-xxx"
          String apiKey = System.getenv("DASHSCOPE_API_KEY");
          // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
          String apiUrl = "https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization";

          // JSON 请求体（旧版本 Java 无 """ 多行字符串）
          String jsonPayload =
                  "{"
                          + "\"model\": \"qwen-voice-design\"," // 不要修改该值
                          + "\"input\": {"
                          +     "\"action\": \"list\","
                          +     "\"page_size\": 10,"
                          +     "\"page_index\": 0"
                          + "}"
                          + "}";

          try {
              HttpURLConnection con = (HttpURLConnection) new URL(apiUrl).openConnection();
              con.setRequestMethod("POST");
              con.setRequestProperty("Authorization", "Bearer " + apiKey);
              con.setRequestProperty("Content-Type", "application/json");
              con.setDoOutput(true);

              try (OutputStream os = con.getOutputStream()) {
                  os.write(jsonPayload.getBytes("UTF-8"));
              }

              int status = con.getResponseCode();
              BufferedReader br = new BufferedReader(new InputStreamReader(
                      status >= 200 && status < 300 ? con.getInputStream() : con.getErrorStream(), "UTF-8"));

              StringBuilder response = new StringBuilder();
              String line;
              while ((line = br.readLine()) != null) {
                  response.append(line);
              }
              br.close();

              System.out.println("HTTP 状态码: " + status);
              System.out.println("返回 JSON: " + response.toString());

              if (status == 200) {
                  Gson gson = new Gson();
                  JsonObject jsonObj = gson.fromJson(response.toString(), JsonObject.class);
                  JsonArray voiceList = jsonObj.getAsJsonObject("output").getAsJsonArray("voice_list");

                  System.out.println("\n 查询到的音色列表：");
                  for (int i = 0; i < voiceList.size(); i++) {
                      JsonObject voiceItem = voiceList.get(i).getAsJsonObject();
                      String voice = voiceItem.get("voice").getAsString();
                      String gmtCreate = voiceItem.get("gmt_create").getAsString();
                      String targetModel = voiceItem.get("target_model").getAsString();

                      System.out.printf("- 音色: %s  创建时间: %s  模型: %s\n",
                              voice, gmtCreate, targetModel);
                  }
              }

          } catch (Exception e) {
              e.printStackTrace();
          }
      }
}
```


### **查询特定音色**

通过音色名称获取特定音色的详细信息。

- **URL**

中国内地：















```http
POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization
```



国际：















```http
POST https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
```

- **请求头**




| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| Authorization | string | 支持 | 鉴权令牌，格式为`Bearer <your_api_key>`，使用时，将“`<your_api_key>`”替换为实际的API Key。 |
| Content-Type | string | 支持 | 请求体中传输的数据的媒体类型。固定为`application/json`。 |

- **消息体**

包含所有请求参数的消息体如下，对于可选字段，在实际业务中可根据需求省略。



**重要**





`model`：声音设计模型，固定为`qwen-voice-design`，请勿修改。



















```json
{
      "model": "qwen-voice-design",
      "input": {
          "action": "query",
          "voice": "voiceName"
      }
}
```

- **请求参数**




| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| model | string | - | 支持 | 声音设计模型，固定为`qwen-voice-design`。 |
| action | string | - | 支持 | 操作类型，固定为`query`。 |
| voice | string | - | 支持 | 待查询的音色名称。 |

- **响应参数**



**点击查看响应示例**










查到数据



未查到数据

































```json
{
      "output": {
          "gmt_create": "2025-12-10 14:54:09",
          "gmt_modified": "2025-12-10 17:47:48",
          "language": "zh",
          "preview_text": "各位听众朋友们，大家好",
          "target_model": "qwen3-tts-vd-realtime-2026-01-15",
          "voice": "yourVoice",
          "voice_prompt": "沉稳的中年男性播音员，音色低沉浑厚，富有磁性，语速平稳，吐字清晰，适合用于新闻播报或纪录片解说。"
      },
      "usage": {},
      "request_id": "yourRequestId"
}
```





当查询的音色不存在时，API返回HTTP 400状态码，响应体包含VoiceNotFound错误码。

















```json
{
      "request_id":"yourRequestId",
      "code":"VoiceNotFound",
      "message":"Voice not found: qwen-tts-vd-announcer-voice-xxxx"
}
```






需关注的参数如下：




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| voice | string | 音色名称，可直接用于语音合成接口的`voice`参数。 |
| target\_model | string | 驱动音色的语音合成模型，支持的模型有（两类）：<br>  - **千问3-TTS-VD-Realtime**（参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime "")）：<br>    <br>    - qwen3-tts-vd-realtime-2026-01-15<br>      <br>    - qwen3-tts-vd-realtime-2025-12-16<br>  - **千问3-TTS-VD**（参见 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")）：<br>    <br>    - qwen3-tts-vd-2026-01-26<br>必须与后续调用语音合成接口时使用的语音合成模型一致，否则合成会失败。 |
| language | string | 语言代码。<br>取值范围：`zh`（中文）、`en`（英文）、`de`（德语）、`it`（意大利语）、`pt`（葡萄牙语）、`es`（西班牙语）、`ja`（日语）、`ko`（韩语）、`fr`（法语）、`ru`（俄语）。 |
| voice\_prompt | string | 声音描述。 |
| preview\_text | string | 试听文本。 |
| gmt\_create | string | 创建音色的时间。 |
| gmt\_modified | string | 修改音色的时间。 |
| request\_id | string | Request ID。 |

- **示例代码**



**重要**





`model`：声音设计模型，固定为`qwen-voice-design`，请勿修改。










cURL



Python



Java



















若未将API Key配置到环境变量，需将示例中的`$DASHSCOPE_API_KEY`替换为实际的API Key。

















```curl
# ======= 重要提示 =======
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
# 新加坡地域和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# === 执行时请删除该注释 ===

curl -X POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization \
  -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "model": "qwen-voice-design",
      "input": {
          "action": "query",
          "voice": "voiceName"
      }
}'
```



















```python
import requests
import os

def query_voice(voice_name):
      """
      查询指定音色信息
      :param voice_name: 音色名称
      :return: 音色信息字典，如果找不到则返回None
      """
      # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
      # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key = "sk-xxx"
      api_key = os.getenv("DASHSCOPE_API_KEY")

      # 准备请求数据
      headers = {
          "Authorization": f"Bearer {api_key}",
          "Content-Type": "application/json"
      }

      data = {
          "model": "qwen-voice-design",
          "input": {
              "action": "query",
              "voice": voice_name
          }
      }

      # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
      url = "https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization"
      # 发送请求
      response = requests.post(
          url,
          headers=headers,
          json=data
      )

      if response.status_code == 200:
          result = response.json()

          # 检查是否包含错误信息
          if "code" in result and result["code"] == "VoiceNotFound":
              print(f"找不到音色: {voice_name}")
              print(f"错误信息: {result.get('message', 'Voice not found')}")
              return None

          # 获取音色信息
          voice_info = result["output"]
          print(f"成功查询到音色信息:")
          print(f"  音色名称: {voice_info.get('voice')}")
          print(f"  创建时间: {voice_info.get('gmt_create')}")
          print(f"  修改时间: {voice_info.get('gmt_modified')}")
          print(f"  语言: {voice_info.get('language')}")
          print(f"  预览文本: {voice_info.get('preview_text')}")
          print(f"  模型: {voice_info.get('target_model')}")
          print(f"  音色描述: {voice_info.get('voice_prompt')}")

          return voice_info
      else:
          print(f"请求失败，状态码: {response.status_code}")
          print(f"响应内容: {response.text}")
          return None

def main():
      # 示例：查询音色
      voice_name = "myvoice"  # 替换为您要查询的实际音色名称

      print(f"正在查询音色: {voice_name}")
      voice_info = query_voice(voice_name)

      if voice_info:
          print("\n音色查询成功！")
      else:
          print("\n音色查询失败或音色不存在。")

if __name__ == "__main__":
      main()
```



















```java
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {

      public static void main(String[] args) {
          Main example = new Main();
          // 示例：查询音色
          String voiceName = "myvoice"; // 替换为您要查询的实际音色名称
          System.out.println("正在查询音色: " + voiceName);
          example.queryVoice(voiceName);
      }

      public void queryVoice(String voiceName) {
          // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
          // 若没有配置环境变量，请用百炼API Key将下行替换为：String apiKey = "sk-xxx"
          String apiKey = System.getenv("DASHSCOPE_API_KEY");

          // 创建JSON请求体字符串
          String jsonBody = "{\n" +
                  "    \"model\": \"qwen-voice-design\",\n" +
                  "    \"input\": {\n" +
                  "        \"action\": \"query\",\n" +
                  "        \"voice\": \"" + voiceName + "\"\n" +
                  "    }\n" +
                  "}";

          HttpURLConnection connection = null;
          try {
              // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
              URL url = new URL("https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization");
              connection = (HttpURLConnection) url.openConnection();

              // 设置请求方法和头部
              connection.setRequestMethod("POST");
              connection.setRequestProperty("Authorization", "Bearer " + apiKey);
              connection.setRequestProperty("Content-Type", "application/json");
              connection.setDoOutput(true);
              connection.setDoInput(true);

              // 发送请求体
              try (OutputStream os = connection.getOutputStream()) {
                  byte[] input = jsonBody.getBytes("UTF-8");
                  os.write(input, 0, input.length);
                  os.flush();
              }

              // 获取响应
              int responseCode = connection.getResponseCode();
              if (responseCode == HttpURLConnection.HTTP_OK) {
                  // 读取响应内容
                  StringBuilder response = new StringBuilder();
                  try (BufferedReader br = new BufferedReader(
                          new InputStreamReader(connection.getInputStream(), "UTF-8"))) {
                      String responseLine;
                      while ((responseLine = br.readLine()) != null) {
                          response.append(responseLine.trim());
                      }
                  }

                  // 解析JSON响应
                  JsonObject jsonResponse = JsonParser.parseString(response.toString()).getAsJsonObject();

                  // 检查是否包含错误信息
                  if (jsonResponse.has("code") && "VoiceNotFound".equals(jsonResponse.get("code").getAsString())) {
                      String errorMessage = jsonResponse.has("message") ?
                              jsonResponse.get("message").getAsString() : "Voice not found";
                      System.out.println("找不到音色: " + voiceName);
                      System.out.println("错误信息: " + errorMessage);
                      return;
                  }

                  // 获取音色信息
                  JsonObject outputObj = jsonResponse.getAsJsonObject("output");

                  System.out.println("成功查询到音色信息:");
                  System.out.println("  音色名称: " + outputObj.get("voice").getAsString());
                  System.out.println("  创建时间: " + outputObj.get("gmt_create").getAsString());
                  System.out.println("  修改时间: " + outputObj.get("gmt_modified").getAsString());
                  System.out.println("  语言: " + outputObj.get("language").getAsString());
                  System.out.println("  预览文本: " + outputObj.get("preview_text").getAsString());
                  System.out.println("  模型: " + outputObj.get("target_model").getAsString());
                  System.out.println("  音色描述: " + outputObj.get("voice_prompt").getAsString());

              } else {
                  // 读取错误响应
                  StringBuilder errorResponse = new StringBuilder();
                  try (BufferedReader br = new BufferedReader(
                          new InputStreamReader(connection.getErrorStream(), "UTF-8"))) {
                      String responseLine;
                      while ((responseLine = br.readLine()) != null) {
                          errorResponse.append(responseLine.trim());
                      }
                  }

                  System.out.println("请求失败，状态码: " + responseCode);
                  System.out.println("错误响应: " + errorResponse.toString());
              }

          } catch (Exception e) {
              System.err.println("请求发生错误: " + e.getMessage());
              e.printStackTrace();
          } finally {
              if (connection != null) {
                  connection.disconnect();
              }
          }
      }
}
```


### **删除音色**

删除指定音色，释放对应额度。

- **URL**

中国内地：















```http
POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization
```



国际：















```http
POST https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
```

- **请求头**




| **参数** | **类型** | **是否必须** | **说明** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必须** | **说明** |
| Authorization | string | 支持 | 鉴权令牌，格式为`Bearer <your_api_key>`，使用时，将“`<your_api_key>`”替换为实际的API Key。 |
| Content-Type | string | 支持 | 请求体中传输的数据的媒体类型。固定为`application/json`。 |

- **消息体**

包含所有请求参数的消息体如下，对于可选字段，在实际业务中可根据需求省略：



**重要**





`model`：声音设计模型，固定为`qwen-voice-design`，请勿修改。



















```json
{
      "model": "qwen-voice-design",
      "input": {
          "action": "delete",
          "voice": "yourVoice"
      }
}
```

- **请求参数**




| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| --- | --- | --- | --- | --- |



|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **默认值** | **是否必须** | **说明** |
| model | string | - | 支持 | 声音设计模型，固定为`qwen-voice-design`。 |
| action | string | - | 支持 | 操作类型，固定为`delete`。 |
| voice | string | - | 支持 | 待删除的音色。 |

- **响应参数**



**点击查看响应示例**




















```json
{
      "output": {
          "voice": "yourVoice"
      },
      "usage": {},
      "request_id": "yourRequestId"
}
```






需关注的参数如下：




| **参数** | **类型** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| request\_id | string | Request ID。 |
| voice | string | 被删除的音色。 |

- **示例代码**



**重要**





`model`：声音设计模型，固定为`qwen-voice-design`，请勿修改。










cURL



Python



Java



















若未将API Key配置到环境变量，需将示例中的`$DASHSCOPE_API_KEY`替换为实际的API Key。

















```curl
# ======= 重要提示 =======
# 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
# 新加坡地域和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
# === 执行时请删除该注释 ===

curl -X POST https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization \
  -H "Authorization: Bearer $DASHSCOPE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "model": "qwen-voice-design",
      "input": {
          "action": "delete",
          "voice": "yourVoice"
      }
}'
```



















```python
import requests
import os

def delete_voice(voice_name):
      """
      删除指定音色
      :param voice_name: 音色名称
      :return: True表示删除成功或音色不存在但请求成功，False表示操作失败
      """
      # 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
      # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key = "sk-xxx"
      api_key = os.getenv("DASHSCOPE_API_KEY")

      # 准备请求数据
      headers = {
          "Authorization": f"Bearer {api_key}",
          "Content-Type": "application/json"
      }

      data = {
          "model": "qwen-voice-design",
          "input": {
              "action": "delete",
              "voice": voice_name
          }
      }

      # 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
      url = "https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization"
      # 发送请求
      response = requests.post(
          url,
          headers=headers,
          json=data
      )

      if response.status_code == 200:
          result = response.json()

          # 检查是否包含错误信息
          if "code" in result and "VoiceNotFound" in result["code"]:
              print(f"音色不存在: {voice_name}")
              print(f"错误信息: {result.get('message', 'Voice not found')}")
              return True  # 音色不存在也算操作成功（因为目标已不存在）

          # 检查是否成功删除
          if "usage" in result:
              print(f"音色删除成功: {voice_name}")
              print(f"请求ID: {result.get('request_id', 'N/A')}")
              return True
          else:
              print(f"删除操作返回意外格式: {result}")
              return False
      else:
          print(f"删除音色请求失败，状态码: {response.status_code}")
          print(f"响应内容: {response.text}")
          return False

def main():
      # 示例：删除音色
      voice_name = "myvoice"  # 替换为您要删除的实际音色名称

      print(f"正在删除音色: {voice_name}")
      success = delete_voice(voice_name)

      if success:
          print(f"\n音色 '{voice_name}' 删除操作完成！")
      else:
          print(f"\n音色 '{voice_name}' 删除操作失败！")

if __name__ == "__main__":
      main()
```



















```java
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {

      public static void main(String[] args) {
          Main example = new Main();
          // 示例：删除音色
          String voiceName = "myvoice"; // 替换为您要删除的实际音色名称
          System.out.println("正在删除音色: " + voiceName);
          example.deleteVoice(voiceName);
      }

      public void deleteVoice(String voiceName) {
          // 新加坡和北京地域的API Key不同。获取API Key：https://help.aliyun.com/zh/model-studio/get-api-key
          // 若没有配置环境变量，请用百炼API Key将下行替换为：String apiKey = "sk-xxx"
          String apiKey = System.getenv("DASHSCOPE_API_KEY");

          // 创建JSON请求体字符串
          String jsonBody = "{\n" +
                  "    \"model\": \"qwen-voice-design\",\n" +
                  "    \"input\": {\n" +
                  "        \"action\": \"delete\",\n" +
                  "        \"voice\": \"" + voiceName + "\"\n" +
                  "    }\n" +
                  "}";

          HttpURLConnection connection = null;
          try {
              // 以下为北京地域url，若使用新加坡地域的模型，需将url替换为：https://dashscope-intl.aliyuncs.com/api/v1/services/audio/tts/customization
              URL url = new URL("https://dashscope.aliyuncs.com/api/v1/services/audio/tts/customization");
              connection = (HttpURLConnection) url.openConnection();

              // 设置请求方法和头部
              connection.setRequestMethod("POST");
              connection.setRequestProperty("Authorization", "Bearer " + apiKey);
              connection.setRequestProperty("Content-Type", "application/json");
              connection.setDoOutput(true);
              connection.setDoInput(true);

              // 发送请求体
              try (OutputStream os = connection.getOutputStream()) {
                  byte[] input = jsonBody.getBytes("UTF-8");
                  os.write(input, 0, input.length);
                  os.flush();
              }

              // 获取响应
              int responseCode = connection.getResponseCode();
              if (responseCode == HttpURLConnection.HTTP_OK) {
                  // 读取响应内容
                  StringBuilder response = new StringBuilder();
                  try (BufferedReader br = new BufferedReader(
                          new InputStreamReader(connection.getInputStream(), "UTF-8"))) {
                      String responseLine;
                      while ((responseLine = br.readLine()) != null) {
                          response.append(responseLine.trim());
                      }
                  }

                  // 解析JSON响应
                  JsonObject jsonResponse = JsonParser.parseString(response.toString()).getAsJsonObject();

                  // 检查是否包含错误信息
                  if (jsonResponse.has("code") && jsonResponse.get("code").getAsString().contains("VoiceNotFound")) {
                      String errorMessage = jsonResponse.has("message") ?
                              jsonResponse.get("message").getAsString() : "Voice not found";
                      System.out.println("音色不存在: " + voiceName);
                      System.out.println("错误信息: " + errorMessage);
                      // 音色不存在也算操作成功（因为目标已不存在）
                  } else if (jsonResponse.has("usage")) {
                      // 检查是否成功删除
                      System.out.println("音色删除成功: " + voiceName);
                      String requestId = jsonResponse.has("request_id") ?
                              jsonResponse.get("request_id").getAsString() : "N/A";
                      System.out.println("请求ID: " + requestId);
                  } else {
                      System.out.println("删除操作返回意外格式: " + response.toString());
                  }

              } else {
                  // 读取错误响应
                  StringBuilder errorResponse = new StringBuilder();
                  try (BufferedReader br = new BufferedReader(
                          new InputStreamReader(connection.getErrorStream(), "UTF-8"))) {
                      String responseLine;
                      while ((responseLine = br.readLine()) != null) {
                          errorResponse.append(responseLine.trim());
                      }
                  }

                  System.out.println("删除音色请求失败，状态码: " + responseCode);
                  System.out.println("错误响应: " + errorResponse.toString());
              }

          } catch (Exception e) {
              System.err.println("请求发生错误: " + e.getMessage());
              e.printStackTrace();
          } finally {
              if (connection != null) {
                  connection.disconnect();
              }
          }
      }
}
```


### **语音合成**

如何使用声音设计生成的专属音色合成个性化的声音，请参见 [快速开始：从声音设计到语音合成](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-design#bb60d81324wsu "")。

**用于声音设计的语音合成模型（如 qwen3-tts-vd-realtime-2026-01-15）为专用模型，仅支持使用声音设计生成的音色，不支持Chelsie、Serena、Ethan、Cherry等系统音色。**

## **音色配额与自动清理规则**

- **总数限制**：1000个音色/账号


> 可通过调用 [查询音色列表](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-design#401d33226330i "") 接口查询音色数目（`total_count`）

- **自动清理**：若单个音色在过去一年内未被用于任何语音合成请求，系统将自动将其删除


## **计费说明**

声音设计和语音合成分开计费：

- 声音设计： [创建音色](https://help.aliyun.com/zh/model-studio/qwen-tts-voice-design#1eaa57d82did9 "") 按0.2 元/个计费，创建失败不计费



**说明**





免费额度说明（仅北京地域有免费额度）：



  - 阿里云百炼开通后90天内，可享10次免费音色创建机会。

  - 创建失败不占用免费次数。

  - 删除音色不会恢复免费次数。

  - 免费额度用完或超出 90 天有效期后，创建音色将按0.2 元/个的价格计费。


- 使用声音设计生成的专属音色进行语音合成：按量（文本字符数）计费，详情请参见 [实时语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime#a162110bff6c4 "") 或 [语音合成-千问](https://help.aliyun.com/zh/model-studio/qwen-tts "")


## **错误信息**

如遇报错问题，请参见 [错误信息](https://help.aliyun.com/zh/model-studio/error-code "") 进行排查。