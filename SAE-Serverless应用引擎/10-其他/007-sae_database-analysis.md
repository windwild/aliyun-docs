### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/)[专业版应用监控](https://help.aliyun.com/zh/sae/monitoring-on-application-professional-edition/)[场景化分析](https://help.aliyun.com/zh/sae/scenario-based-analysis/)数据库分析

# 数据库分析

更新时间：2025-05-18 23:13:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：日志分析](https://help.aliyun.com/zh/sae/log-analysis)[下一篇：调用链分布](https://help.aliyun.com/zh/sae/call-chain-distribution)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

查看数据库信息

专业版应用开启应用监控后，您可以在 **数据库分析** 页面了解应用下所有数据库的请求数、慢请求数、平均耗时，以及各数据库关联的SQL分析、异常分析和调用链信息。

## **查看数据库信息**

单击 **场景化分析** 页签，然后单击 **数据库分析**，即可查看数据库信息。

- 在快捷筛选区域，您可以按 **数据库类型**、 **数据库名称**、 **实例** 对数据库进行筛选过滤。

- 在趋势图区域，您可以查看数据库的请求次数、慢请求数和平均耗时的趋势图。


单击![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3245501071/p741973.png)图标，可以在弹出的对话框中查看该指标在某个时间段的统计情况或对比不同日期在同一时间段的统计情况，通过选择![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2245501071/p741972.png)图标可以切换柱状图、趋势图进行展示。

- 在数据库列表区域，您可以查看数据库名称、数据库类型、SQL/NoSQL语句、请求数、平均耗时、慢请求等信息。

在数据库列表，您可以执行以下操作：

  - 单击数据库名称或 **操作** 列的 **概览**，可以查看目标数据库的 [依赖服务](https://help.aliyun.com/zh/sae/dependent-services "")。

  - 单击 **操作** 列的 **调用链**，可以查看对应调用的链路详情。更多信息，请参见 [调用链分析](https://help.aliyun.com/zh/sae/trace-explorer "")。