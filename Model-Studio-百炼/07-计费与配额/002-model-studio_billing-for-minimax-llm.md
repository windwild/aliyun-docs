### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 计量计费

# MiniMax大语言模型计量计费

更新时间：2026-02-11 02:36:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

查看账单

本文介绍关于MiniMax模型计费相关内容。

#### 计费单元

| **模型服务** | **计费单元** |
| --- | --- |

|     |     |
| --- | --- |
| **模型服务** | **计费单元** |
| abab6.5s-chat | token |
| abab6.5t-chat | token |
| abab6.5g-chat | token |

**重要**

Token是模型用来表示自然语言文本的基本单位，可以直观的理解为“字”或“词”。对于中文文本来说，1个token通常对应一个汉字；对于英文文本来说，1个token通常对应3至4个字母。MiniMax大模型服务根据模型输出结果对应的token数量进行计量计费。每一次模型调用产生的实际token数量可以从 _response_ 中获取。

#### **计费单价**

| **模型名** | **计费单价（币种：RMB）** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名** | **计费单价（币种：RMB）** |
| abab6.5s-chat | 限时免费中 |
| abab6.5t-chat |
| abab6.5g-chat |

#### **免费额度**

| **模型名** | **免费额度** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名** | **免费额度** |
| abab6.5s-chat | **100万tokens**<br>**领取方式**：申请通过后发放。<br>**有效期**：180天 |
| abab6.5t-chat |
| abab6.5g-chat |

**说明**

您可以参阅 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 确认您是否具备享有免费额度的资格，并查询免费总额度、剩余额度及到期时间。

### **基础限流**

为了保证用户调用模型的公平性，所以对于普通用户设置了基础限流。限流是基于模型维度的，并且和调用用户的阿里云主账号相关联，按照该账号下所有API-KEY调用该模型的总和计算限流。如果超出调用限制，用户的API请求将会因为限流控制而失败，用户需要等待一段时间待满足限流条件后方能再次调用。

| 模型名 | **基础限流** |
| --- | --- |

|     |     |
| --- | --- |
| 模型名 | **基础限流** |
| abab6.5s-chat | 以下条件任何一个超出都会触发限流：<br>- 调用频次 ≤ 60 QPM，每分钟不超过60次API调用；<br>  <br>- Token消耗 ≤ 100,000 TPM，每分钟消耗的Token数目不超过100,000。 |
| abab6.5t-chat |
| abab6.5g-chat |

## **查看账单**

有关账单详情请前往[费用与成本](https://usercenter2.aliyun.com/finance/expense-report/expense-detail)查询。