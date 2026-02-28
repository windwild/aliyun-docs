### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)[产品计费](https://help.aliyun.com/zh/model-studio/test-1/)新人免费额度

# 新人免费额度

更新时间：2026-02-11 01:55:18

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：选择部署模式](https://help.aliyun.com/zh/model-studio/regions/)[下一篇：模型调用计费](https://help.aliyun.com/zh/model-studio/model-pricing)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

规则说明

有效期

适用范围

注意事项

获取免费额度

查看剩余额度

使用免费额度

免费额度用完即停

常见问题

免费额度用完是否有通知？

免费额度用完会有什么影响？

免费额度用完后该如何充值？

为什么产生了费用？

如何查看产生费用的模型？

如何查看模型调用记录？

如何避免扣费？

还有剩余额度，为何调用失败？

为什么看不到免费额度与有效期？

当您首次开通阿里云百炼时，平台会自动为您发放各模型的新人专属免费额度。

**说明**

仅 **中国大陆版** 模型享有免费额度，其他地域无免费额度。

## **规则说明**

### **有效期**

新人免费额度有效期通常是30~90天，从开通阿里云百炼或模型申请通过之日起计算。超过有效期或免费额度消耗完后，继续使用模型推理服务将产生 [计费](https://help.aliyun.com/zh/model-studio/billing-for-model-studio "")。

**重要**

自**2025年9月8日11点**起，首次开通阿里云百炼的用户，获赠的新人免费额度有效期调整为 90 天，在此之前已开通的用户不受影响，详情参考 [阿里云百炼新人免费额度有效期调整通知](https://help.aliyun.com/zh/model-studio/new-free-quota-validity-adjustment "")。

### **适用范围**

新人免费额度仅支持抵扣模型实时推理（调用）产生的费用。不支持抵扣 [Batch调用](https://help.aliyun.com/zh/model-studio/batch-interfaces-compatible-with-openai/ "")、 [上下文缓存](https://help.aliyun.com/zh/model-studio/context-cache "")、 [模型调优](https://help.aliyun.com/zh/model-studio/model-training-overview "")、 [模型部署简介](https://help.aliyun.com/zh/model-studio/model-deployment-introduction "")、自定义模型（调优后模型、已部署模型）产生的费用。

### **注意事项**

阿里云主账号与其RAM子账号共享免费额度。

> 例如：qwen-max的总免费额度为100万Token。主账号消耗了10万Token，RAM子账号消耗了20万Token，qwen-max的剩余免费额度为70万Token。

## 获取免费额度

访问[阿里云百炼-中国大陆版](https://bailian.console.aliyun.com/#/model-market)，阅读并同意协议后，系统将自动开通阿里云百炼并发放 **免费推理额度**。

> 如果未弹出服务协议，表示您已经开通过阿里云百炼且获得免费额度。

**如何查询百炼的首次开通时间**

在 **[我的订单](https://usercenter2.aliyun.com/order/list)** 页面，搜索商品 **阿里云百炼** 或 **模型服务灵积**，再 **删除** 时间范围，单击 **搜索**。

查询结果中，支付/开通时间 **最早的** 订单即为阿里云百炼的首次开通时间。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1571291471/p928567.png)

## 查看剩余额度

可通过以下两种方式查看模型的免费额度。

#### **方式一：通过模型用量查看**

在控制台的 **[模型用量](https://bailian.console.aliyun.com/?tab=model#/model-usage/free-quota)** 页面，点击 **免费额度** 页签，查看所有模型的免费额度余量及过期时间。

#### **方式二：通过模型广场查看**

1. 在控制台的 **[模型广场](https://bailian.console.aliyun.com/?tab=model#/model-market/all)** 页面，找到目标模型系列并单击进入详情页。

![11](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9935068571/p1010357.webp)

2. 在 **模型Code** 选择模型的版本，在 **免费额度** 区域进行查看。若无免费额度，则可能免费额度已到期，具体有效期参见 [模型列表](https://help.aliyun.com/zh/model-studio/models "")。

如下图所示， **362,917/1,000,000** 表示剩余362,917个Token，总共1,000,000个Token。


> 控制台显示的免费额度每小时更新，非实时数据。


![12](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9935068571/p1010358.webp)


## **使用免费额度**

实时调用大模型将自动扣除免费额度，请参考 [开始使用阿里云百炼](https://help.aliyun.com/zh/model-studio/what-is-model-studio#1b7e9bceeb486 "")。

### **免费额度用完即停**

默认状态下，免费额度消耗完后继续使用会扣费。启用免费额度用完即停功能后，免费额度耗尽将无法继续调用（返回错误 code：AllocationQuota.FreeTierOnly），避免产生额外费用。

#### **如何开启**

##### **方式一：在模型用量页面开启**

**为单个模型开启:**

1. 在控制台的 **[模型用量](https://bailian.console.aliyun.com/?tab=model#/model-usage/free-quota)** 页面，点击 **免费额度** 页签。

2. 在页面列表中找到目标模型，在其右侧操作列中打开 **免费额度用完即停** 开关（若该模型没有免费额度，则无法开启）。


**批量开启**：

1. 在控制台的 **[模型用量](https://bailian.console.aliyun.com/?tab=model#/model-usage/free-quota)** 页面，点击 **免费额度** 页签。

2. 点击 **批量操作免费额度用完即停**，在下拉菜单中选择 **批量开启**。

3. 勾选目标模型，点击 **批量开启**。若需为所有支持且未开启的模型启用此功能，可点击 **一键开启所有模型**。

4. 在确认弹窗中，点击 **开启免费额度用完即停**。

![2026-01-12_15-51-25](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4644028671/p1044022.jpg)


##### **方式二：在模型广场页面开启**

以 Qwen3-Coder-Plus 为例。前往[Qwen3-Coder-Plus 模型详情页](https://bailian.console.aliyun.com/?tab=model#/model-market/detail/group-qwen3-coder-plus?modelGroup=group-qwen3-coder-plus)并开启 **免费额度用完即停** 开关。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5847454571/p994732.png)

若模型没有显示开关，说明该模型免费额度已耗尽或过期，或模型本身没有提供免费额度。

#### **如何关闭**

该功能默认为关闭状态。若已启用 **免费额度用完即停** 功能，需在控制台显示的 **免费额度用完后** 才可以关闭。

> 控制台显示的免费额度每小时更新，非实时数据。

## **常见问题**

### **免费额度用完是否有通知？**

目前没有通知机制。

### **免费额度用完会有什么影响？**

若没有开启 [免费额度用完即停](https://help.aliyun.com/zh/model-studio/new-free-quota#d1cb80ac11i92 "") 功能，已开始的模型调用会继续完成，不会因为免费额度用完而中断。超出免费额度的Token将按 [模型列表](https://help.aliyun.com/zh/model-studio/models "") 中的输入/输出成本计费，产生的费用会以按量后付费的方式自动从阿里云账户中扣除。这可能会导致账户出现欠费情况。

如果账户欠费，其他模型即使仍有免费额度也无法进行调用。

建议您在调用模型前查询该模型的免费额度并进行 [预算管理](https://help.aliyun.com/zh/user-center/how-to-manage-a-budget "") 或 [设置账号余额预警](https://help.aliyun.com/zh/user-center/monitor-account-balances "")，以减少不必要的费用支出。同时，请确保您的账户中有充足的 [余额](https://usercenter2.aliyun.com/home)，避免因欠费影响您的业务，未使用的余额支持 [余额提现](https://help.aliyun.com/zh/user-center/balance-withdrawal "")。

### **免费额度用完后该如何充值？**

阿里云支持支付宝、银联在线支付、网银等多种充值方式，实际可用方式请以账号 [充值界面](https://billing-cost.console.aliyun.com/fortune/fund-management/recharge) 展示为准。更多信息请参考 [充值方式介绍](https://help.aliyun.com/zh/user-center/use-alipay-online-banking-to-recharge-online#8e4f4cdcf42rl "")。

充值完成后，账户余额可能存在一定时间的更新延迟，请您等待几分钟后，再前往[费用与成本](https://usercenter2.aliyun.com/home)查看可用余额。充值已到账且没有欠费时即可调用模型。

### **为什么产生了费用？**

**可能有以下原因：**

- 您使用了没有免费额度的模型（例如：qwen-max和qwen-max-latest两个模型的免费额度不共享）。

- 免费额度不支持抵扣 [OpenAI兼容-Batch](https://help.aliyun.com/zh/model-studio/batch-interfaces-compatible-with-openai/ "") 调用产生的费用。

- 控制台显示的免费额度数据每小时更新。因此，控制台显示模型还有免费额度，实际上免费额度可能已经被消耗完，导致产生了调用费用。建议您稍后再次查看最新的免费额度情况。


您可以通过 [如何查看产生费用的模型？](https://help.aliyun.com/zh/model-studio/new-free-quota#3bfa8283d0tc2 "") 及 [如何查看模型调用记录？](https://help.aliyun.com/zh/model-studio/new-free-quota#ab6ba5c538rn3 "") 确认费用详情。

### **如何查看产生费用的模型？**

模型调用完 **一小时后**，在[账单详情](https://usercenter2.aliyun.com/finance/expense-report/expense-detail)页面，选择账单月份，再选择**商品名称** 为 **阿里云百炼大模型推理**，单击 **搜索**。在资产/资源实例ID列查看产生费用的模型。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2927326371/p898881.png)

### **如何查看模型调用记录？**

模型调用完 **一小时后**，在模型监控（ [北京](https://bailian.console.aliyun.com/?tab=model#/model-telemetry) 或 [新加坡](https://modelstudio.console.aliyun.com/?tab=model#/model-telemetry)）页面设置查询条件（例如，选择时间范围、业务空间等），再在 **模型列表** 区域找到目标模型并单击 **操作** 列的 **监控**，即可查看该模型的调用统计结果。具体请参见 [模型监控](https://help.aliyun.com/zh/model-studio/model-telemetry/ "") 文档。

> 数据按小时更新，高峰期可能有小时级延迟，请您耐心等待。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6923304571/p992753.png)

### **如何避免扣费？**

超出免费额度后，会自动从阿里云账号余额扣费。您可以通过以下方式管理扣费风险：

- 进入阿里云百炼的[API-Key（北京）](https://bailian.console.aliyun.com/?apiKey=1&tab=globalset#/efm/api_key) 或 [API-Key（新加坡）](https://modelstudio.console.aliyun.com/?tab=globalset#/efm/api_key)页面删除已创建的 API-Key。删除API Key后，您将无法通过API调用百炼上的模型，因此也不会再产生模型调用费用。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4293235471/p943678.png)

- 设置 [高额消费预警](https://usercenter2.aliyun.com/home/alarm-threshold)。当设置的预警产品日账单大于预警阈值时，每天短信提醒一次。（统计截止昨日24点的账单费用）

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9403157371/p902681.png)


### **还有剩余额度，为何调用失败？**

您可以查看[阿里云账户](https://usercenter2.aliyun.com/home?spm=a2c4g.11186623.nav-v2-dropdown-my-aliyun.9.f6683048dWvpGu)是否欠费。如果欠费，即使模型有免费额度也无法调用。

### **为什么看不到免费额度与有效期？**

当免费额度列显示 **无免费额度** 或不显示 **免费额度** 区域，说明账号下该模型的免费额度已到期。