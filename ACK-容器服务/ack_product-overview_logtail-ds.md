logtail-ds组件是由阿里云日志服务提供，用于采集Kubernetes日志的Agent。本文介绍logtail-ds组件信息、使用说明和变更记录。

## 组件介绍

logtail-ds日志组件提供高性能、低资源消耗的日志采集功能，默认安装在kube-system命名空间下。在安装logtail-ds组件过程中自动完成以下操作：

1. 创建aliyunlogconfigs CRD（Custom Resource Definition），用于向K8s系统注册CRD。
2. 部署alibaba-log-controller的Deployment，负责管理CRD。
3. 以DaemonSet模式安装Logtail，负责采集数据。

logtail-ds支持动态过滤需要采集的容器，支持标准输出、文件、Syslog等多种采集方式，支持多种日志解析方式和配置方式。关于日志采集功能的更多信息，请参见[Logtail采集概述](https://help.aliyun.com/zh/sls/use-logtail-to-collect-data/#concept-ppd-yx5-vdb "Logtail是日志服务提供的日志采集Agent，用于采集阿里云ECS、自建IDC、其他云厂商等服务器上的日志。本文介绍Logtail的功能、优势、使用限制及配置流程等信息。")。


## 使用说明

有关日志服务logtail-ds组件的使用说明，请参见[通过日志服务采集Kubernetes容器日志](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/collect-text-logs-from-ack-clusters-using-daemonset-deployed-logtail-agents#task-1797722 "阿里云容器服务Kubernetes集群集成了日志服务，您可在创建集群时启用日志服务，快速采集Kubernetes集群的容器日志，包括容器的标准输出以及容器内的文本文件。")。


## 变更记录

有关日志服务logtail-ds组件的变更记录，请参见[logtail-ds发布历史](https://help.aliyun.com/zh/sls/sls-release-notes#concept-w5w-q3q-zdb "本文档为您介绍日志服务Logtail的发布历史。")。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[日志与监控](https://help.aliyun.com/zh/ack/product-overview/logs-and-monitoring/)logtail-ds

# logtail-ds

更新时间：2021-07-15 22:29:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ack-node-problem-detector](https://help.aliyun.com/zh/ack/product-overview/ack-node-problem-detector)[下一篇：LoongCollector](https://help.aliyun.com/zh/ack/product-overview/loongcollector)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

变更记录