### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/)[专业版应用监控](https://help.aliyun.com/zh/sae/monitoring-on-application-professional-edition/)[应用配置](https://help.aliyun.com/zh/sae/application-settings-new/)监控方法自定义

# 监控方法自定义

更新时间：2025-05-20 05:22:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：探针管理](https://help.aliyun.com/zh/sae/agent-management)[下一篇：业务参数提取规则](https://help.aliyun.com/zh/sae/business-parameter-extraction-rules)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

自定义监控方法

除了被ARMS探针自动发现的所有方法和接口外，如果您需要监控应用中的其他方法和接口，则可在应用监控中自定义监控方法。

## **自定义监控方法**

1. 在 **应用监控** 页面，选择**应用配置** \> **监控方法自定义**，单击 **添加方法**，即可自定义监控方式。

2. 在**添加自定义方法**对话框中，设置以下参数，并单击**确认**。




| **参数** | **描述** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **描述** |
| **方法全名** | 需要监控的方法的名称，具有唯一性。 |
| **开启此功能** | 开启此功能，即可监控此方法，并且可在本地方法栈中展示此方法，更多信息，请参见 [调用链分析](https://help.aliyun.com/zh/sae/trace-explorer "")。默认为开启状态。<br>**说明**<br>ARMS支持动态开启或关闭此功能，并且无需重启应用。 |
| **设为业务调用入口** | 设置为业务调用入口后，则可通过调用链对其进行业务查询，并且可在**提供服务**模块中展示对应接口，更多信息，请参见 [提供服务](https://help.aliyun.com/zh/sae/provision-of-services "")。默认为关闭状态。<br>**说明**<br>如果调用栈中的多个自定义方法同时被设置为业务调用入口，那么只会统计到最后一个方法的监控信息（如A函数调用B函数，如果同时对A与B函数做自定义埋点，则只能统计到B函数的信息）。 |