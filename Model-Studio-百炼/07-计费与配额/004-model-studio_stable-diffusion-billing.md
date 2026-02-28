### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[图像生成](https://help.aliyun.com/zh/model-studio/image-generation/)[文生图StableDiffusion](https://help.aliyun.com/zh/model-studio/stable-diffusion-quick-start/)计量计费

# 计量计费

更新时间：2026-02-11 02:23:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：StableDiffusion3.5 API详情](https://help.aliyun.com/zh/model-studio/stable-diffusion-3-5-apis)[下一篇：文生图FLUX](https://help.aliyun.com/zh/model-studio/flux-api-reference/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

StableDiffusion文生图模型

计费单元

计费单价

免费额度

基础限流

查看账单

**重要**

本文档仅适用于“中国内地（北京）”地域。

## StableDiffusion文生图模型

### **计费单元**

| **模型服务** | **计费单元** |
| --- | --- |

|     |     |
| --- | --- |
| **模型服务** | **计费单元** |
| StableDiffusion文生图模型 | 张 |

### **计费单价**

| **模型名称** | **计费单价** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **计费单价** |
| stable-diffusion-xl | 目前仅供免费体验。<br>> 免费额度用完后不可调用，推荐参考 [文本生成图像](https://help.aliyun.com/zh/model-studio/text-to-image "") 获取替代方案 |
| stable-diffusion-v1.5 |
| stable-diffusion-3.5-large |
| stable-diffusion-3.5-large-turbo |

### **免费额度**

| **模型名称** | **免费额度** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **免费额度** |
| stable-diffusion-xl | [申请](https://bailian.console.aliyun.com/?accounttraceid=494cccbc11014cf1a6f54cba1bc77e68dsju#/model-market) 通过后，提供500张免费使用额度，有效期90天。 |
| stable-diffusion-v1.5 |
| stable-diffusion-3.5-large |
| stable-diffusion-3.5-large-turbo |

**说明**

您可以参阅 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 确认您是否具备享有免费额度的资格，并查询免费总额度、剩余额度及到期时间。

### **基础限流**

为了保证用户调用模型的公平性，默认对于普通用户设置了基础限流。如果超出限流指定的调用限制，用户的API请求将会因为限流控制而失败，用户需要等待一段时间待满足限流条件后方能再次调用。

**说明**

限流是基于模型维度的，并且和调用用户的阿里云主账号相关联，按照该账号下所有API-KEY调用该模型的总和计算限流。

| **模型名称** | **基础限流** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **基础限流** |
| stable-diffusion-xl | - 作业提交接口 ≤ 2 QPS，每秒钟处理不超过2个完整的作业提交请求；<br>  <br>- 同一时间并发运行作业数：1 个作业，在同一时刻，只有1个作业实际处于运行状态，其他队列中的作业处于排队状态。 |
| stable-diffusion-v1.5 |
| stable-diffusion-3.5-large |
| stable-diffusion-3.5-large-turbo |

## **查看账单**

有关阿里云百炼大模型服务平台的账单时效信息请参阅 [计费项](https://help.aliyun.com/zh/model-studio/billing-for-model-studio "")。