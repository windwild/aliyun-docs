### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[Job任务](https://help.aliyun.com/zh/sae/job-task-2-0/)[任务运维](https://help.aliyun.com/zh/sae/task-o-m-2-0/)日志管理

# 日志管理

更新时间：2025-12-25 00:35:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：基础监控](https://help.aliyun.com/zh/sae/basic-monitoring-2-0)[下一篇：使用Jenkins实现Job任务的持续部署](https://help.aliyun.com/zh/sae/use-jenkins-to-create-continuous-integration-for-jobs)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

背景信息

查看实时日志

设置日志收集至SLS

在任务的运维过程中，您可以通过日志定位并诊断问题。Serverless 应用引擎 SAE（Serverless App Engine）提供实时日志和持久化日志，支持在线或下载查看。本文介绍如何通过SAE为任务模板设置日志收集规则并查看所需日志。

## 前提条件

- [创建任务模板](https://help.aliyun.com/zh/sae/job-template-management-2-0 "")

- [创建Project和Logstore](https://help.aliyun.com/zh/sls/getting-started#section-2l7-ol2-zro "")


## 背景信息

SAE提供以下日志。

- 实时日志：标准输出日志，帮助定位Pod问题。

- 持久化日志：创建或部署任务时，SAE可以自动打通日志服务SLS，将容器标准输出日志（stdout）和业务文件日志（容器内日志路径）输出到SLS，帮助您无限制行数地查看日志、自聚合分析日志。


## 查看实时日志

1. 在[SAE任务模板](https://saenext.console.aliyun.com/cn-hangzhou/job-list)中，在顶部选择目标地域和命名空间，点击目标任务模板跳转到任务模板详情页。

2. 在左侧导航栏，单击**日志管理** \> **实时日志**。

3. 在 **实时日志** 页面，在 **POD名称** 下拉列表选择目标实例，在 **实时日志刷新频率** 下拉列表中选择刷新频率。





**说明**





SAE最多显示最近的500条日志。如果您需要查看更多内容，可以使用文件日志功能查看持久化日志。具体操作，请参见 [设置日志收集至SLS](https://help.aliyun.com/zh/sae/log-management-2-0#section-011-nc2-4hd "")。


## 设置日志收集至SLS

**操作路径：**

1. 在[SAE任务模板](https://saenext.console.aliyun.com/cn-hangzhou/job-list)中，在顶部选择目标地域和命名空间，点击目标任务模板跳转到任务模板详情页。

2. 在 **任务模板详情** 页面，单击 **编辑任务模板**。

3. 展开 **日志配置** 区域， **开启SLS日志服务**。


**配置说明：**

详细配置信息，请参见 [设置日志收集至SLS](https://help.aliyun.com/zh/sae/set-log-collection-to-sls-2-0 "")。