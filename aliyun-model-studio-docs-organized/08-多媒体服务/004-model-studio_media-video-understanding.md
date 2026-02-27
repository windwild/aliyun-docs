### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-全妙轻应用系列](https://help.aliyun.com/zh/model-studio/quanmiao-light-application-series/)[使用指南](https://help.aliyun.com/zh/model-studio/light-application-guidelines-for-use/)影视传媒视频理解

# 影视传媒视频理解

更新时间：2026-02-12 02:59:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：影视互娱剧本创作](https://help.aliyun.com/zh/model-studio/film-and-television-script-creation)[下一篇：车机网络热点信息互动问答](https://help.aliyun.com/zh/model-studio/car-machine-content-platform-news-hot-list-interaction)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能概述

功能入口

功能介绍

应用详情

效果调试

查看API示例

相关文档

常见问题

1、支持处理哪些视频？

2、如果有大量视频需要处理，怎样提高视频处理效率？

3、视频处理中哪些步骤会消耗Token？怎样操作可以减少Token的消耗？

4、离线调用怎么增加并发配额？

5、需要处理大量视频时，有什么方式可以降低费用？

影视传媒视频理解轻应用支持借助视频处理、视频理解、大语言模型的串联能力，实现对视频里指定要点的理解和提取，并按要求生成指定类型的文案、提取标签、洞察分析等。

**重要**

- 影视传媒视频理解应用按实际调用模型对应的输入、输出Token以后付费方式来计费。具体请参见 [影视传媒视频理解计费](https://help.aliyun.com/zh/model-studio/film-and-television-media-video-understanding-billing "")。

- 关于Token的计算方法和模型的计费详情，请参见 [计费项](https://help.aliyun.com/zh/model-studio/billing-for-model-studio "")。

- 您可点击 [链接](https://common-buy.aliyun.com/?spm=a2c4g.11186623.0.0.6ebb69f3CQubdx&commodityCode=sfm_videoanalysis_public_cn) 开通影视传媒视频理解。


## 功能概述

影视传媒视频理解轻应用通过整合视频处理、自动语音识别（ASR）、视觉语言模型（VLM）和大语言模型（LLM）等算法能力，构建了一套通用的视频理解方案。该方案支持视频描述、结构解析、标签分类、问答场景、内容挖掘、视频检索、分析场景、营销应用场景、学习示例以及游戏赛事场景等十大常见应用，并内置多个对应的子任务模板。用户可以参照这些模板进行修改和调试，以适配或自定义其业务场景。总体而言，基于基础模型，系统支持更细粒度的理解和更复杂的任务；在功能上，支持一次VL视觉理解即可复用并完成多个下游子任务。

## **功能入口**

访问 [**应用实践**](https://bailian.console.aliyun.com/?tab=app#/app-market/lightApplication) 页面，单击 **全妙-影视传媒视频理解** 卡片区域的 **立即查看**，即可进入该轻应用控制台。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9152752571/p982654.png)

## 功能介绍

### **应用详情**

在 **影视传媒视频理解** 应用的 **应用详情** 页签，您可以查看功能描述、目标客群、最佳实践、使用步骤、计费规则、全妙相关应用推荐、视频理解相关解决方案七部分内容。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9317637371/p907546.png)

### **效果调试**

单击 **效果调试** 页签，您可以参考以下步骤设置配置项。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9317637371/p907592.png)

1. 设置 **视频处理** 配置项。


1. 上传视频文件：单击或拖拽本地视频文件至虚线框内。


      > 支持中英文视频，以及`.flv`、`.ts`、`.avi`、`.wmv`、`.mpg`、`.mkv`、`.mov`、`.mp4`格式，视频大小需小于120 MB，分辨率小于1080P，时长不超过10分钟。



      如果视频超过10分钟，您可以调用异步API实现。功能相同，但目前不支持页面上预览结果。



      请在API页面查看调用方式详情：



      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9152752571/p982657.png)

2. **可选**：输入视频相关的补充文字资料，辅助大模型理解。![F9BC4C8A-42D0-4e57-B3B5-FCCE8E6CB320](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7731207671/p1038462.png)


2. 设置 **视觉语言分析（VL分析）** 配置项。通过多模态大模型分析视频各个片段里的详细信息，例如角色、动作、画面内容等。生成的内容是一个中间结果，主要服务于第3步的进一步加工处理，输出结果较长，可不做重点关注。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9317637371/p907631.png)



1. 选择VL大模型：目前支持通 **义千问VL-Max-Latest**、 **千问VL-Max**、 **千问VL-Plus-Latest**、 **千问VL-Plus**。

2. 输入VL大模型的指令（Prompt）：按照模板填写输入给到VL大模型的指令。


3. **可选**：设置 **文本加工** 配置项。结合您的具体目标，在下方输入相应Prompt，包括但不限于视频内容摘要、标签抽取、视频分类。


1. 选择大语言模型，目前支持 **千问-Max-Latest**、 **千问-Max**、 **千问-Plus-Latest**、 **千问-Plus、DeepSeek-R1、通义干问2.5-7B-1M、Qwen3-235B-A22B（思考模式及非思考模式）**。

2. 输入大语言模型的指令（Prompt）：可选用 **参考示例** 中的场景应用，支持内容描述、结构解析、标签分类、问答场景、内容挖掘、视频检索、分析场景和营销场景等10大常见应用，并内置了多个对应子任务模板。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4567697471/p949828.png)


      > 您可以点击 **增加文本模型任务**，最多支持添加3个。


      **视频理解支持的功能如下：**

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2257440371/p867124.png)


4. 设置 **其他可选输出项** 配置项（内置能力），包含 **视频时间戳+字幕**、 **视频内容总结成思维导图**、 **总结生成视频标题**。![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9317637371/p907673.png)

5. 设置 **高级功能** 配置项，包含抽帧策略配置、多语言识别、人物身份识别。


   - 抽帧策略配置：支持快速、标准和自定义抽帧方式，抽帧时间间隔越长，视频信息抓取的精细度越低，但处理一个视频耗费的Token会变少。

   - 自动语音识别（ASR）设置。

   - 多语言识别：支持五种语言形式的视频分析，包含中文、英语、法语、日语、中英文自由说。

   - 人物身份识别：支持对视频中的人物进行识别，最多支持识别3个人物，每个人物可上传1张图片。

   - 人脸相似度阈值：取值范围为0.1~1，推荐取值区间为0.45~0.65。默认值为0.5。

   - 匹配角色时，在每个视频片段抽的帧数：取值范围1~5，推荐和默认值为3。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9152752571/p982659.png)

6. 点击 **开始分析。** 按照输入的内容，大模型可以进行理解、学习生成，您可以在右侧查看第4步结果（ **视频时间戳+字幕**、 **视频内容总结成思维导图**、 **总结生成视频标题**）、 **视觉语言分析结果** 和 **文本加工结果**。


下图为视频理解示例：![e743c49f54c8da1450bceb0d53138ccf](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4567697471/p959578.png)


### 查看API示例

效果调试完成后，单击 **API** 页签，您可以查看对应生成的API示例。

**说明**

支持实时和异步两种模式：

- 实时模式：在线调用

  - 共享资源池，共享并发。

  - 最多支持1并发。

  - 支持处理的单个视频时长最多不超过30分钟，且单个视频大小小于200MB，分辨率不超过1080P。
- 异步模式：离线调用

  - 共享资源池，共享并发。

  - 每个阿里云主账号提供2个免费并发，且支持增加并发配额，最多支持扩展到10并发。

  - 任务可在24小时内处理完毕。一次任务不超过1万个视频文件，每个视频时长不超过60分钟。且单个视频大小小于450MB，分辨率小于1080P。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9317637371/p907689.png)

## **相关文档**

- 计费： [影视传媒视频理解计费](https://help.aliyun.com/zh/model-studio/film-and-television-media-video-understanding-billing "")

- 接口文档： [影视传媒视频理解](https://help.aliyun.com/zh/model-studio/api-quanmiaolightapp-2024-08-01-dir-film-and-television-media-video-understanding/ "")

- 视频理解与内容提取的解决方案： [解决方案地址](https://www.aliyun.com/solution/tech-solution-deploy/2860032)


## **常见问题**

### **1、支持处理** 哪些视频 **？**

支持中英文视频，以及`.flv`、`.ts`、`.avi`、`.wmv`、`.mpg`、`.mkv`、`.mov`、`.mp4`格式，视频大小需小于200 MB，分辨率小于1080P，时长不超过10分钟。

### **2、如果有大量视频需要处理，怎样提高视频处理效率？**

视频处理API采取SSE协议，实时的流式处理方式，如果有大量视频需要处理，可以通过并行调用API的方式提高视频的处理效率，建议并发度控制在20 QPM以内，如果您需要更高并发可以联系我们处理。

### **3、视频处理中哪些步骤会消耗Token？怎样操作可以减少Token的消耗？**

- 视频处理大致流程分为：视频ASR提取、切片、抽帧、视觉语言分析（消耗VL大模型Token），文本加工（消耗文本大模型Token）。

- 其中视频时长增长对文本加工Token消耗影响不大，视频越长、抽帧间隔越短，视觉语言分析Token消耗基本呈线性增长。

- 如果您对Token消耗有要求，可以考虑通过增加抽帧间隔（snapshotInterval\[1~10\]）来降低Token消耗。但是抽帧间隔越长，视频理解的细腻程度会有所损耗。


### **4、离线调用怎么增加并发配额？**

您可以通过 [GetVideoAnalysisConfig - 视频理解-获取配置](https://help.aliyun.com/zh/model-studio/api-quanmiaolightapp-2024-08-01-getvideoanalysisconfig "")、 [UpdateVideoAnalysisConfig - 视频理解-更新配置](https://help.aliyun.com/zh/model-studio/api-quanmiaolightapp-2024-08-01-updatevideoanalysisconfig "") 接口查看和扩缩并发。

### **5、** 需要处理大量视频时，有什么方式可以降低费用 **？**

在保证效果的前提下可尝试以下方式：

1. VL和LLM用小尺寸模型。

2. 自定义抽帧配置（调整抽帧间隔，以及图片像素，将尺寸调小）。

3. 尝试关闭ASR（如果视频有字幕可以关闭）。

4. 将并发控制在2以内（2并发不收并发费用）。