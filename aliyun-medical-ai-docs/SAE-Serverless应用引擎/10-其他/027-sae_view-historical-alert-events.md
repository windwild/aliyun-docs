### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[告警管理](https://help.aliyun.com/zh/sae/alert-management-overview2-0/)查看告警事件历史

# 查看告警事件历史

更新时间：2025-02-24 03:00:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查看告警发送历史](https://help.aliyun.com/zh/sae/view-alarm-sending-history)[下一篇：管理联系人](https://help.aliyun.com/zh/sae/contact)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

相关文档

告警规则被触发后会产生告警事件，但只有满足通知策略匹配规则的事件才会生成告警并被发送给指定联系人。您可以通过SAE查看所有产生的告警事件。本文介绍如何在SAE控制台查看告警事件详情并管理告警。

## 前提条件

已创建并启用告警规则。具体操作，请参见 [应用监控告警规则](https://help.aliyun.com/zh/sae/apply-monitoring-alarm-rules-new "")。

## 操作步骤

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在左侧导航栏，选择**通知告警** \> **告警事件历史**。

3. 在 **事件列表** 页面，按需筛选字段，然后单击 **搜索**，查看对应的告警事件历史。






| **字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **字段** | **说明** |
| **事件名称** | 创建的告警规则的名称。 |
| **集成名称** | 告警事件对应的集成名称。 |
| **事件状态** | 告警事件的状态。<br>   - **未恢复**：告警事件持续被触发。<br>     <br>   - **静默**：在设置的自动恢复告警事件的时间内，和第一条告警事件名称和等级相同的告警事件的状态为静默。<br>     <br>   - **已恢复**：在设置的时间内，告警事件不再触发。 |
| **事件对象** | 监控任务名称或集群名称。 |
| **对象类型** | 事件对象类型。默认值为 **app**。 |
| **集成类型** | 告警事件对应的集成类型。 |





   - 单击事件名称，查看目标事件的详细信息，包括基本信息、监控数据和扩展字段等。

   - 单击 **发送测试事件**，在弹出的对话框中设置 **集成名称** 和 **事件内容**，可以发送一次告警事件测试到指定集成中。


## 相关文档

- [应用监控告警规则](https://help.aliyun.com/zh/sae/apply-monitoring-alarm-rules-new "")

- [查看告警发送历史](https://help.aliyun.com/zh/sae/view-alarm-sending-history "")