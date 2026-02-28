开启听视频功能后，CDN节点会将视频文件中的音频分离，并返回给客户端，实现听视频的同时降低带宽的使用，有效节省流量。通过本文您可以了解开启音视频分离的操作方法。

## 背景信息

当客户端请求访问视频文件时，向服务器端发送URL请求，例如：`http://www.aliyun.com/test.flv?ali_audio_only=1`，CDN服务器端仅向客户端发送纯音频数据。客户端必须支持`Transfer-Encoding:chunked`传输方式。


**说明**

- 听视频功能不支持Range请求，但是播放视频时许多客户端都会发起Range请求（包括但不限于Safari、iOS设备上的浏览器），建议您使用自研的客户端对接该功能。
- 听视频过程中如果需要拖动进度条播放，需同时配置拖拽功能。进行拖拽时，会先读取原音视频文件的meta信息获取播放时长，将播放时长作为播放进度来实现播放进度的拖拽具体操作。更多信息，请参见 [配置拖拽播放](https://help.aliyun.com/zh/cdn/user-guide/video-seeking#task-187634 "当您播放视音频时，需要随意拖拽播放进度，而不影响视音频的播放效果，可以开启拖拽播放功能。通过本文您可以了解配置拖拽播放功能的操作方法。")。

- 目前听视频功能不支持mp4 box header size等于16的场景（64位），仅支持mp4 box header size等于8的场景。

## 操作步骤

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。
2. 在左侧导航栏，单击域名管理。
3. 在域名管理页面，单击目标域名对应的管理。
4. 在指定域名的左侧导航栏，单击视频相关。
5. 在听视频区域，打开听视频开关。


开启听视频功能后，需要配合请求参数`ali_audio_only`使用。支持的文件格式如下表所示。





| 文件格式 | meta信息 | ali\_audio\_only参数 | 举例 |
| --- | --- | --- | --- |




| 文件格式 | meta信息 | ali\_audio\_only参数 | 举例 |
| --- | --- | --- | --- |
| MP4 | 源站视频的meta信息必须在文件头部，不支持meta信息在尾部的视频。 | `ali_audio_only`参数表示该请求为音视频分离请求，服务端只返回meta信息和音频信息，视频信息会被过滤掉。如果不带该参数或参数值非1，则该功能失效。 | 请求`http://domain/video.mp4?ali_audio_only=1`。 |
| FLV | 无要求。 | `ali_audio_only`参数表示该请求为音视频分离请求，服务端只返回meta信息和音频信息，视频信息会被过滤掉。如果不带该参数或参数值非1，则该功能失效。 | 请求`http://domain/video.flv?ali_audio_only=1`。 |


## 相关文档

- [批量配置域名](https://help.aliyun.com/zh/cdn/api-batchsetcdndomainconfig#doc-api-Cdn-BatchSetCdnDomainConfig "调用BatchSetCdnDomainConfig进行域名批量配置。")

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[视频相关](https://help.aliyun.com/zh/cdn/user-guide/video-related-settings/)配置听视频

# 配置听视频

更新时间：2022-06-30 22:18:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置拖拽播放](https://help.aliyun.com/zh/cdn/user-guide/video-seeking)[下一篇：配置音视频试看](https://help.aliyun.com/zh/cdn/user-guide/audio-and-video-preview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

操作步骤

相关文档