### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[了解计费](https://help.aliyun.com/zh/oss/understanding-billing/)[计费项](https://help.aliyun.com/zh/oss/billable-items/)[增值计费项](https://help.aliyun.com/zh/oss/value-added-billing-item/)AI内容感知费用

# AI内容感知费用

更新时间：2026-02-09 04:58:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费单价

计费项

当您在数据索引-向量检索模式中开启 AI 增值服务-AI 内容感知后，会产生 AI 内容感知费用。AI 内容感知可以智能感知和理解 OSS 中多媒体文件的内容，生成详细内容描述和精简描述摘要，用以增强语义检索效果。

## **计费单价**

本文仅说明相关计费项及付费方式。有关计费项的定价详情，请参见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)。

## 计费项

| **计费项** | **计费条件** | **计费规则** | **计费周期** | **付费方式** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **计费项** | **计费条件** | **计费规则** | **计费周期** | **付费方式** |
| 图片内容感知<br>（ImageContentAware） | 在数据索引-向量检索模式中开启图片内容感知时收取 | 按处理的图片数量（张）进行计费 | 按小时计费（账单出账时间通常在当前计费周期结束后，具体出账时间以系统为准） | 按量付费： 图片内容感知费用=处理的图片张数×图片内容感知单价 |
| 视频内容感知<br>（VideoContentAware） | 在数据索引-向量检索模式中开启视频内容感知时收取 | 按处理的视频时长进行计费 | 按小时计费（账单出账时间通常在当前计费周期结束后，具体出账时间以系统为准） | 按量付费： 视频内容感知费用=处理的视频时长×视频内容感知单价 |