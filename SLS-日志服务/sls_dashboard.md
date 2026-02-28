### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据监控](https://help.aliyun.com/zh/sls/data-monitoring/)[可视化](https://help.aliyun.com/zh/sls/visualization-2/)仪表盘

# 仪表盘

更新时间：2024-12-17 22:41:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：可视化概述](https://help.aliyun.com/zh/sls/overview-of-visualization)[下一篇：快速创建仪表盘](https://help.aliyun.com/zh/sls/dashboard-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

什么是仪表盘

使用场景

实时监控和可视化

快速发现异常指标

定位异常根因

免密分享和集成仪表盘

仪表盘是日志服务提供的数据可视化工具，通常包含多个统计图表，汇总并呈现关键性能指标、重要数据和分析结果。当您打开或刷新仪表盘时，统计图表自动执行一次查询分析操作。本文介绍仪表盘的概念和使用场景。

## 什么是仪表盘

仪表盘以柱状图、折线图、饼图等形式展示日志的查询分析结果，每个仪表盘由多个统计图表组成，每个图表实际是一个或多个查询分析语句。当您打开或刷新仪表盘时，统计图表自动执行一次查询分析操作。

通过仪表盘您可以实时监控可观测关键指标、快速发现指标的异常并定位异常的根因，同时您可以通过免密分享将仪表盘分享给他人，这有助于提高团队间的沟通效率，协同解决问题。

## 使用场景

### **实时监控和可视化**

通过仪表盘，您可以将复杂的日志、事件数据以及其他监控数据转化为直观的图表和图形，实时监控系统状态、业务运行情况和安全事件等。

### 快速发现异常指标

通过设置阈值和告警，仪表盘可用于检测关键指标的异常行为，例如成功率降低或资源不足，同时结合历史对比和多维度分析，用户能快速发现和定位异常指标，提高系统和业务的稳定性和响应速度。

|     |
| --- |
| ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7993306271/p846651.png)![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7993306271/p846662.png)![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7993306271/p846657.png) |

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7993306271/p846734.png)

### 定位异常根因

在仪表盘发现异常时，通过交互事件将图表与日志服务集成的多种数据进行关联，如（日志、指标和追踪），帮助用户深入分析异常的原因。

![2024-09-12_15-24-27 (1)](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0075026271/p848290.gif)

### 免密分享和集成仪表盘

仪表盘免密分享功能使得用户可以将仪表盘共享给其他人，或集成到第三方系统中，而无需登录权限。