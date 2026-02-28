### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[服务支持](https://help.aliyun.com/zh/sae/support/)[Web应用文档合集（文档停止维护）](https://help.aliyun.com/zh/sae/web-application-documentation/)[Web应用操作指南](https://help.aliyun.com/zh/sae/web-application-new/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-web/)日志管理（SLS）

# 日志管理（SLS）

更新时间：2024-09-02 11:43:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查看应用监控](https://help.aliyun.com/zh/sae/view-application-monitoring)[下一篇：将Web应用迁移到SAE](https://help.aliyun.com/zh/sae/migrate-applications-from-web-app-service-to-sae)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

限制条件

在SAE控制台查看日志

更多信息

在Serverless 应用引擎上成功创建应用后，阿里云提供了实时的标准输出日志，可以帮助您快速和有效的对应用产生的问题进行诊断和解决，本文主要介绍在创建成功的应用中如何查看目标版本实例的日志。

## **限制条件**

支持显示最新时间的500条版本实例的日志。如果您需要查看更多的日志，可登录Wellshell进行在线查看。

## 在SAE控制台查看日志

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击目标应用名称。

4. 在左侧导航栏，单击 **日志管理**，即可查看最新版本的实例的日志。

在 **日志管理** 页面，可以单击 **版本**。在下拉列表中选择需要查看日志的目标版本，然后单击 **实例版本**，在下拉框中选择目标版本的目标实例。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3339132271/p815743.png)


## **更多信息**

如果500行日志信息无法满足您的需求，您可以将业务日志和系统监控Metrics输出至SLS。配置成功后，您可以查看超过默认提供的500行实例日志，并持久化到SLS。同时也可以查看已销毁实例的日志。具体操作，请参见 [设置日志及监控metrics](https://help.aliyun.com/zh/sae/set-logs-and-monitor-metrics "")。