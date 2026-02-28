### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[应用广场](https://help.aliyun.com/zh/model-studio/application-gallery/)[官方应用-通义拍照解题辅导](https://help.aliyun.com/zh/model-studio/edu-tutor/)产品简介

# 通义拍照解题辅导产品介绍

更新时间：2025-10-15 02:24:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：UI应用数据](https://help.aliyun.com/zh/model-studio/ui-application-data)[下一篇：API概览](https://help.aliyun.com/zh/model-studio/api-edututor-2025-07-07-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

产品概述

功能介绍

试卷切题

解题辅导

应用场景

使用入口

百炼应用体验页面

API调用

计量计费规则

## **产品概述**

拍照解题辅导应用，利用通义大模型多模态识别及推理能力,对用户上传的题目试卷图片进行切题识别、推理判解，输出对题目的考点分析、方法思路、解析过程。

## **功能介绍**

### **试卷切题**

- 将练习册、试卷或教辅的整页图片，按照题目维度进行自动切题，并进行结构化识别文字内容和坐标位置。

- 支持扫描版本及实拍场景的题目图片，涵盖jgp/png/bmp/heic等多种图片格式。

- 支持精细化题目结构的返回，包含题目类型、题干、子题、选项、插图、答案等内容。


## **解题辅导**

- 针对单个题目（含图片或文本），支持输出对题目的详细解析过程（考点、思路、解题过程）及最终答案。

- 题目类型涵盖K12阶段各学科、大学教育、成人考试等各类题型。

- 支持多轮交互，方便用户更好与大模型进行知识互动，真正了解题目背后的知识点。


## **应用场景**

- 学生自学：遇到难题？拍照上传，立刻获取分步详解和思路分析，快速定位疑难点，实时交互获取知识详解。

- 家长辅导：孩子的题目不会讲？大模型提供清晰的知识点分析和讲解思路，从“直接给答案”转变为“科学教方法”。


## **使用入口**

### **百炼应用体验页面**

登录【阿里云百炼】->点击顶部导航【应用】->选择【应用实践】->找到【通义拍照解题辅导】，开通服务后进入效果调试页面，上传本地试卷图片进行体验。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9176325571/p994784.png)

### **API调用**

根据API示例或者查看接口文档，进行接口调用。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9176325571/p994783.png)

## **计量计费规则**

- 拍照解题辅导如果仅开通服务，不会产生费用，当前应用属于公测阶段免费使用。

- 试卷切题、解题辅导接口免费调用，限制单个账号每个接口每天1000次调用。

- 调用限制：对于每个开通账号，限流为5QPS（每秒不超过5次请求）。