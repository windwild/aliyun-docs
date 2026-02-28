### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/)[专业版应用监控](https://help.aliyun.com/zh/sae/monitoring-on-application-professional-edition/)[应用诊断](https://help.aliyun.com/zh/sae/application-diagnosis/)线程分析

# 线程分析

更新时间：2025-05-18 23:06:58

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：智能洞察](https://help.aliyun.com/zh/sae/intelligent-insights)[下一篇：Arthas诊断](https://help.aliyun.com/zh/sae/arthas-diagnosis)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能入口

进行线程分析

线程分析功能提供线程粒度的CPU耗时和每类线程数量的统计，并且每5分钟记录一次线程的方法栈并聚合，可真实还原代码执行过程，帮助您快速定位线程问题。当发现集群的CPU使用率过高，或者出现大量慢方法时，可以通过线程分析功能找到消耗CPU最多的线程或方法。

**说明**

该功能目前仅支持Java应用。

## **功能入口**

在 **应用监控** 页面，单击**应用诊断** \> **线程分析**。

## **进行线程分析**

**线程分析** 页面的左侧列表展示了应用的全部线程，您可以根据 **CPU耗时** 统计快速发现异常线程。选中某一异常线程后，再根据右侧的 **CPU耗时** 和 **线程数** 曲线图分析CPU耗时与线程数变化，例如分析每分钟的线程总数是否过多。

![pyXrpg5S5j](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7104267471/p951896.png)

您还可以单击异常线程的 **方法栈**，查看指定时间内的真实运行方法栈，例如查看处于BLOCKED状态的线程对应的方法，从而优化指定代码段，以便降低CPU使用率。

![pg_am_method_stack](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4395559361/p84725.png)

如果您的探针版本为2.7.3.5或以上版本，ARMS通过持续剖析能力提供了数据更准确的线程CPU使用方法栈信息，效果如下图所示，更多信息，请参见 [持续性能剖析](https://help.aliyun.com/zh/sae/continuous-performance-profiling "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5999074071/p755120.png)

**说明**

如果单击 **方法栈** 后，显示无数据，排查方法如下：

- 如果探针版本为2.7.3.5以下，则在**应用配置** \> **自定义配置**页签的 **线程设置** 区域查看 **线程分析方法栈** 开关是否开启。如未开启，则无法记录方法栈信息；如已开启，则每5分钟采集一次方法栈信息。

- 如果探针版本为2.7.3.5及以上，则在**应用配置** \> **自定义配置**页签的 **持续剖析** 区域查看 **总开关** 和 **CPU热点** 开关是否开启。如未开启，则无法记录方法栈信息。