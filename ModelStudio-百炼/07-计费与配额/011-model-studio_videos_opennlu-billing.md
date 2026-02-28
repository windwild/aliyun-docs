### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 计量计费

# OpenNLU开放域文本理解模型计量计费

更新时间：2026-02-11 02:35:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

查看账单

#### 计费单元

| **模型服务** | **计费单元** |
| --- | --- |

|     |     |
| --- | --- |
| **模型服务** | **计费单元** |
| OpenNLU开放域文本理解模型 | token |

**重要**

这里token数量指的是大模型使用的tokenizer分词后对应的最小分词单元的数量。在OpenNLU开放域文本理解模型中，单个token平均约对应1.5个汉字, 0.7个英文单词。OpenNLU开放域文本理解模型根据模型输出结果对应的token数量进行计量计费。每一次模型调用产生的实际token数量可以从 _response_ 中获取。

#### **计费单价**

| **模型名称** | **计费单价（币种：RMB）** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **计费单价（币种：RMB）** |
| opennlu-v1 | 0.00465元/1000 tokens |

#### **免费额度**

| **模型名称** | **免费额度** |
| --- | --- |

|     |     |
| --- | --- |
| **模型名称** | **免费额度** |
| opennlu-v1 | 开通阿里云百炼大模型服务平台即获赠总计 1,000,000 tokens限时免费使用额度，有效期180天。 |

**说明**

您可以参阅 [新人免费额度](https://help.aliyun.com/zh/model-studio/new-free-quota "") 确认您是否具备享有免费额度的资格，并查询免费总额度、剩余额度及到期时间。

### **基础限流**

为了保证用户调用模型的公平性，默认对于普通用户设置了基础限流。如果超出限流指定的调用限制，用户的API请求将会因为限流控制而失败，用户需要等待一段时间待满足限流条件后方能再次调用。

**说明**

限流是基于模型维度的，并且和调用用户的阿里云主账号相关联，按照该账号下所有API-KEY调用该模型的总和计算限流。

| **模型服务** | **模型名** | **基础限流** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **模型服务** | **模型名** | **基础限流** |
| OpenNLU开放域文本理解模型 | opennlu-v1 | 以下条件任何一个超出都会触发限流：<br>- 流量 ≤ 60 QPM，每分钟处理不超过60个完整的请求；<br>  <br>- Token消耗 ≤ 10,000 TPM，每分钟消耗的Token数目不超过10,000。 |

## **查看账单**

有关阿里云百炼大模型服务平台的账单时效信息请参阅： [计费项](https://help.aliyun.com/zh/model-studio/billing-for-model-studio "")。

有关账单详情请前往[费用与成本](https://usercenter2.aliyun.com/finance/expense-report/expense-detail)查询。