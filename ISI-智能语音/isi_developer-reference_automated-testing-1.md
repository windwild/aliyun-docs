### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[自学习平台](https://help.aliyun.com/zh/isi/developer-reference/customization-platform/)自动化测试

# 自动化测试

更新时间：2024-12-18 03:22:10

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用SDK 2.0设置自学习模型](https://help.aliyun.com/zh/isi/developer-reference/use-sdk-2-0-to-set-a-self-learning-model)[下一篇：语音识别问题排查](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition-troubleshooting)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

创建自动化测试任务

测试结果分析

示例结果

专业词汇及其缩写说明：

管理自动化测试任务

您可以通过自动化测试建立测试任务，从而对模型的识别准确率形成量化衡量。尤其对于语言定制模型而言，当测试集不变的情况下，通过自动化测试可以看到每次自学习模型训练对于准确率的提升或者降低。

## **前提条件**

已开通智能语音交互服务，详情请参见 [准备账号](https://help.aliyun.com/zh/isi/activate-intelligent-speech-interaction-1#topic-2572187 "")。

## 创建自动化测试任务

1. 登录 [智能语音交互控制台](https://nls-portal.console.aliyun.com/)。

2. 在左侧导航栏单击 **自动化测试**，在 **自动化测试** 页面单击 **创建任务**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0018601761/p535611.png)

3. 在 **创建任务** 面板中，填写任务名称，注意不能与现有的任务名称重复。

![图片 2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9174578261/p303722.png)

4. 选择或者上传测试集。

目前支持 **上传标注测试集**、 **仅上传文本** 和 **选择已有测试集** 三种方式。



**重要**





当测试数据集有异常时，数据集解析及测试任务都会失败，因此请仔细阅读文件要求。





   - **上传标注测试集**

     适用于有音频数据，也有标注结果。按照下列格式上传，系统会自动检测采样率，当采样率非标准采样率（非16K或8K采样率）时，系统会自动调整为适合的采样率。

     ![数据目录结构](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9478598951/p147872.png)

     要求如下：


     - 路径中不允许有中文。

     - 每个WAV文件名必须是唯一的。

     - WAV文件（.wav后缀）和标注TXT（.txt后缀）文件必须分别放置在两个目录，且后缀必须为英文小写。

     - WAV文件要求：单通道，8KHz或16KHz采样率，16bit采样位数的PCM编码WAV文件（可使用Sox工具通过Channels、Sample Rate和Sample Encoding进行判断）。


标注文本

![图片 1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9174578261/p303712.png)

要求如下：

     - 标注文件格式：UTF-8无BOM编码，各字段间用tab键分隔。

     - trans目录中可以包含多个TXT文件，每个TXT文件中指定多个WAV文件对应的标注文本。

     - 标注文件第一列音频文件名需要和wav目录的音频文件名对应（注意文件名带.wav后缀）。

     - 标注文本应该是归一化后的（按照实际读音转写成汉字，“5256”对应”五千二百五十六”，”2004”对应“二零零四”或“两千零四”，“19%”对应”百分之十九”等） ，WAV文件名不需要带目录，因为文件名唯一。
   - **仅上传文本**

     文本测试集适用于没有音频数据，只有文本语料数据的场景，我们会通过语音合成帮您合成相应的音频数据构造标注好的测试集。要求如下：

     - 请上传1个文本文件，仅支持TXT格式（UTF-8无BOM编码）。

     - 请不要携带标点符号，每行不超过300字。
   - **选择已有测试集**

     您也可以先创建测试集，在创建任务时，选择相应测试集进行测试。采样率相同的测试集可以选择多个一起进行测试。
5. 选择测试模型（可选择创建的语言定制模型），单击 **下一步**。

![图片 3](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9174578261/p303743.png)

6. 选择需对比的模型（非必选，最多可选一个），完成后单击 **确定**。

7. 单击目标任务右侧的 **开始任务**，系统开始自动化测试任务。


## **测试结果分析**

在测试结果中，您需要关注后缀为 `compareResult.txt` 的文件。

在`compareResult.txt`文件中，会显示测试数据集中每句音频的识别统计结果，并在文本最后给出该测试集整体的识别率。其中：ref表示人工标注结果，res表示asr识别结果。

### **示例结果**

![image](<Base64-Image-Removed>)

### **专业词汇及其缩写说明：**

- nwords：总字数，以人工标注结果为准。

- cor (corrections): 正确识别的字数。


- ins (insertions): 插入错误，识别结果比人工标注多出的字数。

- del (deletions): 删除错误，识别结果比人工标注缺少的字数。

- sub (substitutions): 替换错误，识别结果中错误替换的字数。

- corr (correction rate): 识别正确率。

  - 计算公式：corr=nwordsnwords−sub−del​=nwordscor​
- cer (character error rate): 字错误率。

  - 计算公式：cer=nwordssub+del+ins​=nwordsnwords−cor+ins​
- wer (word error rate): 词错误率。同字错误率，常用于英文文本。

- ser (sentence error rate): 句错误率，在整个测试数据集中识别出错的句子所占比率。


## **管理自动化测试任务**

当任务 **当前状态** 为 **测试完成** 时，可在操作列 **查看结果**、 **下载结果**、 **开始任务**，或执行 **编辑** 或 **删除** 操作。

![image](<Base64-Image-Removed>)