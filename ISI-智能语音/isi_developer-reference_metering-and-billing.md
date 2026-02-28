### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音识别](https://help.aliyun.com/zh/isi/developer-reference/speech-recognition/)[百炼语音模型服务](https://help.aliyun.com/zh/isi/developer-reference/spirit-product-speech-model-service/)计量计费

# 计量计费

更新时间：2024-11-19 04:34:58

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：快速开始](https://help.aliyun.com/zh/isi/developer-reference/quick-start)[下一篇：API详情](https://help.aliyun.com/zh/isi/developer-reference/api-details)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费方式

免费额度

查看账单

本文为您介绍Paraformer语音识别的计费详细说明。

## **计费方式**

| **模型服务** | **模型名** | **计费单元** | **计费单价** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **模型服务** | **模型名** | **计费单元** | **计费单价** |
| Paraformer语音识别 | paraformer-1 | 秒（不足1秒四舍五入） | 0.00008元/秒 |
| paraformer-8k-1 |
| paraformer-mtl-1 |

**重要**

- Paraformer语音识别模型服务仅对音轨中被判定为语音内容的时长进行语音转写，并据此进行计量计费，非语音内容不计量、不计费。通常情况下语音内容时长会短于原始音频时长。由于对是否存在语音内容的判定是由AI模型给出的，可能与实际情况存在一定误差。

- 对于多轨音频文件，默认参数配置下仅转写首轨音频，并仅对其进行计量计费。如开发者指定对多个音轨进行转写，将对各音轨根据其语音内容时长分别进行计量计费。每次请求的实际计费单元数量可通过返回结果中的 **content\_duration** 字段获得，详情请参见 [返回参数说明](https://help.aliyun.com/zh/dashscope/api-reference-1)。


## **免费额度**

| **模型服务** | **免费额度** |
| --- | --- |

|     |     |
| --- | --- |
| **模型服务** | **免费额度** |
| paraformer-1 | 每主账号每月36,000秒（10小时）<br>**说明**<br>免费额度于每月1日0点生效。 |
| paraformer-8k-1 |
| paraformer-mtl-1 |

## 查看账单

- 有关DashScope的账单时效信息，请参见 [产品计费](https://help.aliyun.com/zh/dashscope/product-overview/billing-rules)。

- 更多账单明细信息，请前往阿里云费用与成本查看 [账单详情](https://usercenter2.aliyun.com/finance/expense-report/expense-detail)。