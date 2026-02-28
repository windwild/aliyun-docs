### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[百炼语音模型服务](https://help.aliyun.com/zh/isi/developer-reference/spirit-product-speech-model-service/)最佳实践

# 最佳实践

更新时间：2024-11-19 04:35:33

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：API详情](https://help.aliyun.com/zh/isi/developer-reference/api-details)[下一篇：热词](https://help.aliyun.com/zh/isi/developer-reference/hotwords/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

预处理视频文件以提高文件转写效率

前提条件

操作步骤

通过OSS提高文件转写效率和稳定性

## 预处理视频文件以提高文件转写效率

Paraformer语音识别API可以兼容视频文件，但由于视频文件尺寸通常较大、传输较为耗时，因此建议您对视频文件进行预处理。仅提取需要进行语音识别的音轨，并进行合理压缩，从而显著降低文件尺寸、减少API调用过程中的文件传输耗时、加快文件转写吞吐效率。

### **前提条件**

已安装 [FFmpeg](https://ffmpeg.org/)。

### **操作步骤**

使用FFmpeg提取视频文件中的第一条音轨、将采样降到16kHz、并压缩编码为OPUS文件。

一般情况下，输出的音频文件将显著小于输入的视频文件的尺寸，可向文件转写API提交该音频文件（以URL指定），获得语音识别结果。

```shell
ffmpeg -i input-video-file -ac 1 -ar 16000 -acodec libopus output-audio-file.opus
```

## 通过OSS提高文件转写效率和稳定性

由于阿里云对象存储OSS可以便捷地为文件生成URL，从而被指定为API的输入，对位于同地域OSS中的文件进行转写有助于提高转写效率和稳定性，因此推荐您使用与Paraformer语音识别API同地域的OSS进行音视频文件存储。

Paraformer语音识别文件转写API当前部署的地域有： **华北2（北京，cn-beijing）**。

**重要**

对同地域的OSS文件进行语音识别文件转写时，应指定OSS bucket的内网域名下的URL作为文件名。这将避免产生不必要的OSS网络流量费用。

更多关于对象存储OSS的信息，请参见 [OSS](https://www.aliyun.com/product/oss?spm=a2c4g.611471.0.0.1d3141bcT5RxYT)。