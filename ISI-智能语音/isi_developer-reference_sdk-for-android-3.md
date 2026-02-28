### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis/)[语音合成](https://help.aliyun.com/zh/isi/developer-reference/speech-synthesis-1/)[移动端SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-mobile-clients-2/)Android SDK（旧版）

# Android SDK（旧版）

更新时间：2022-09-08 07:16:58

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：iOS SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-ios-1)[下一篇：iOS SDK（旧版）](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-ios-4)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

关键接口

调用顺序

Proguard配置

代码示例

本文介绍了如何使用阿里云智能语音服务提供的旧版Android SDK，包括SDK的安装方法及SDK代码示例。请注意，新用户请关注新版Android SDK。

**注意**

推荐您使用新版本Android SDK，本版本后续将不再更新。详情请参见 [Android SDK](https://help.aliyun.com/zh/isi/developer-reference/nui-sdk-for-android-2#topic-2572254 "")。

## 前提条件

- 阅读接口说明，详情请参见 [接口说明](https://help.aliyun.com/zh/isi/developer-reference/overview-of-speech-synthesis#topic-2572243 "")。

- 已获取项目appkey，详情请参见 [创建项目](https://help.aliyun.com/zh/isi/create-a-project#topic-2572188 "")。

- 已获取智能语音服务访问令牌，详情请参见 [获取Token概述](https://help.aliyun.com/zh/isi/overview-of-obtaining-an-access-token#587dee8029x7r "")。


## 关键接口

- NlsClient：语音处理客户端，利用该客户端可以进行一句话识别、实时语音识别和语音合成的语音处理任务。该客户端为线程安全，建议全局仅创建一个实例。

- SpeechSynthesizer：代表一次语音合成请求。

- SpeechSynthesizerCallback：语音合成回调接口，在获得合成音频数据、发生错误等事件发生时会触发回调。您需要实现此接口，在回调方法中加入自己的处理逻辑。


## 调用顺序

1. 创建NlsClient实例。

2. 定义SpeechSynthesizerCallback实现类，按业务需求处理识别结果或错误情况。

3. 调用NlsClient.createSynthesizerRequest()方法得到SpeechSynthesizer实例。

4. 设置SpeechSynthesizer参数。

包括access Token、appkey、语音文本（text）、发音人（voice）和语速（speechRate）等。

5. 调用SpeechSynthesizer.start()方法开始与云端服务连接。

6. 在回调中获得合成的音频数据并播放，或者处理错误。

7. 调用SpeechSynthesizer.stop()方法结束语音合成。



**说明**





如果需要发起新的请求，请重复步骤3~7。

8. 调用NlsClient.release()方法释放客户端实例。


## Proguard配置

如果代码使用了混淆，请在proguard-rules.pro中配置：

```java
-keep class com.alibaba.idst.util.*{*;}
```

## 代码示例

- 创建识别请求

















```java
// 创建语音合成对象
speechSynthesizer = client.createSynthesizerRequest(callback);
speechSynthesizer.setToken("");
speechSynthesizer.setAppkey("");
// 设置语音编码，PCM编码可以直接用audioTrack播放，其他编码不行。
speechSynthesizer.setFormat(SpeechSynthesizer.FORMAT_PCM);
// 以下选项都会改变最终合成的语音效果。
// 设置语音数据采样率
speechSynthesizer.setSampleRate(SpeechSynthesizer.SAMPLE_RATE_16K);
// 设置人声
speechSynthesizer.setVoice(SpeechSynthesizer.VOICE_XIAOGANG);
// 设置语音合成方法
speechSynthesizer.setMethod(SpeechSynthesizer.METHOD_RUS);
// 设置语速
speechSynthesizer.setSpeechRate(100);
// 设置是否返回语音对应的时间戳信息
speechSynthesizer.setEnableSubtitle(true);
// 设置要转为语音的文本
speechSynthesizer.setText("欢迎使用智能语音！");
speechSynthesizer.start()
```

- 获取合成语音并播放















```java
// 获取音频数据的回调，在这里将音频写入播放器。
@Override
public void OnBinaryReceived(byte[] data, int code)
{
      Log.d(TAG, "binary received length: " + data.length);
      if (!playing) {
          playing = true;
          audioTrack.play();
      }
      audioTrack.write(data, 0, data.length);
}
```

- 返回语音时间戳信息















```java
// 调用onMetaInfo，需要设置：SpeechSynthesizer.setEnableSubtitle(true)。
@Override
public void onMetaInfo(String message, int code) {
      Log.d(TAG,"onMetaInfo " + message + ": " + String.valueOf(code));
}
```