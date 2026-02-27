### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-多模态交互开发套件](https://help.aliyun.com/zh/model-studio/multimodal-products/)[最佳实践](https://help.aliyun.com/zh/model-studio/multimodal-best-practices/)[接入听悟智能纪要Agent](https://help.aliyun.com/zh/model-studio/fast-integrate-tingwu-meeting-agent/)录音纪要Agent使用教程

# 录音纪要Agent使用教程

更新时间：2026-02-11 02:10:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：三方RTC接入视频通话](https://help.aliyun.com/zh/model-studio/third-party-rtc-invoke-liveai)[下一篇：离线转写能力集成](https://help.aliyun.com/zh/model-studio/fast-integrate-offline-tingwu-meeting-agent)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能入口

开通服务

应用配置

实时录音总结设置

录音文件总结设置

对话体验

开始实时转写

退出实时转写

## **功能入口**

新建多模态应用后，在「多模态交互控制台-Agent-推荐应用」中勾选「录音纪要」点击确认即可添加。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4413777671/p1041701.png)

## **开通服务**

首次使用录音纪要Agent，需要开通通义听悟服务，请前往 [通义听悟-智能纪要](https://bailian.console.aliyun.com/?tab=app#/app/app-market/tingwu/tingwu-meeting-summary) 进行开通并发布应用。

![截屏2026-01-07 14](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4413777671/p1042451.png)

1. 在通义听悟-智能纪要应用中点击右上角「立即开通」。


![截屏2026-01-07 14](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1042460.png)

![截屏2026-01-07 14](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1042474.png)

![截屏2026-01-07 14](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1042476.png)

2. 完成开通操作后，点击通义听悟-智能纪要控制台右上角「创建应用」，进行应用配置并发布。


![截屏2026-01-07 14](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1042357.png)

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1041614.png)

## **应用配置**

在通义听悟-智能纪要控制台创建应用并发布后，您需要在多模态交互控制台页面中选择对应的通义听悟应用。（如需调整应用能力，可以前往通义听悟-智能纪要控制台进行调整 [去配置](https://bailian.console.aliyun.com/?tab=app#/app/app-market/tingwu/tingwu-meeting-summary)）

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1041615.png)

### **实时录音总结设置**

您可以在右侧配置中设置实时录音总结的启动指令、退出/暂停唤醒词、恢复指令。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4413777671/p1041612.png)

指令参考：

|     |     |     |     |
| --- | --- | --- | --- |
| 启动指令 | 暂停指令（自定义唤醒词） | 恢复指令 | 退出指令（自定义唤醒词） |
| “开始/打开/启动实时转写”<br>“开始实时转写”<br>“开始实时转写并翻译”<br>“开始实时转写会议内容”<br>“打开实时转写，记录这段对话”<br>“现在启动实时转写”<br>“开始实时转写并记录讨论”<br>“打开实时转写功能，记录课堂内容”<br>“开始实时转写客户咨询”<br>“启动实时转写，记录小组讨论”<br>“现在实时转写这段谈话” | “小云，暂停一下”<br>“小云，暂停转写”<br>“小云，暂停实时转写”<br>“小云，等一下再实时转写”<br>“小云，先停转一下”<br>“小云，转写暂停” | “继续录音”<br>“继续实时转写”<br>“继续转写”<br>“可以继续转了”<br>“恢复转写”<br>“接着转吧” | “小云，停止转写”<br>“小云，结束转写”<br>“小云，停止实时转写”<br>“小云，结束实时转写”<br>“小云，结束转写，帮我整理一下内容”<br>“小云，停止转写，总结这段讨论”<br>“小云，停止实时转写，总结当前对话” |

### **录音文件总结设置**

您还可以设置录音文件总结的启动指令、退出指令、暂停指令以及恢复指令。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1041699.png)

指令参考：

|     |     |     |     |
| --- | --- | --- | --- |
| 启动指令 | 退出指令 | 暂停指令 | 恢复指令 |
| “开始/打开/启动录音总结”<br>“开始录制并总结”<br>“录音并总结这个会议”<br>“现在开始录音并总结”<br>“开始录音并总结课程内容”<br>“录音并总结接下来的访谈”<br>“录音总结这段讨论”<br>“打开录音，总结当前对话”<br>“录音总结当前会议内容”<br>“录下并总结这个客户咨询”<br>“录音总结小组讨论”<br>“启动录音并总结这段谈话”<br>“录下课堂内容并总结” | “停止录音”<br>“结束录音”<br>“结束录制，帮我总结一下吧，顺便翻译成英语”<br>“结束录音，整理一下这段讨论”<br>“停止录音，总结今天的课程”<br>“结束会议录音，并翻译成英文” | “等一下再录”<br>“暂停录制”<br>“先停录一下”<br>“录音暂停” | “继续录音”<br>“继续录制”<br>“可以继续录了”<br>“恢复录制”<br>“接着录吧” |

## **对话体验**

完成各项配置后，您可以在多模态交互控制台体验通义听悟的录音和纪要能力。

### **开始实时转写**

使用之前配置的启动指令开启录音总结，如“开启实时转写”，即可开始转写，同时您也可以查看双语字幕。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1041613.png)

### **退出实时转写**

使用之前已配置的 **唤醒词加上退出指令** 即可退出实时转写，如“小云，退出实时转写”。点击「查看分析结果」可前往通义听悟查看智能纪要。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1041617.png)

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3413777671/p1041616.png)