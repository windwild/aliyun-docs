### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[日志与监控](https://help.aliyun.com/zh/ack/product-overview/logs-and-monitoring/)LoongCollector

# LoongCollector组件介绍与发布记录（灰度中）

更新时间：2025-03-17 07:09:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：logtail-ds](https://help.aliyun.com/zh/ack/product-overview/logtail-ds)[下一篇：logtail-windows](https://help.aliyun.com/zh/ack/product-overview/logtail-windows)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

变更记录

LoongCollector是由阿里云日志服务SLS提供的可用于采集Kubernetes日志的Agent。LoongCollector在继承Logtail组件日志采集与处理能力的基础上，进一步进行了功能扩展。

## **组件介绍**

**说明**

组件处于灰度发布中。

LoongCollector组件直接通过Kubernetes原生接口获取集群数据，提供无侵入式的集群日志采集方案。详细介绍及使用限制，请参见 [LoongCollector采集](https://help.aliyun.com/zh/sls/loongcollector-collection/ "")。

## **使用说明**

关于如何基于LoongCollector组件实现集群日志采集，请参见 [LoongCollector采集](https://help.aliyun.com/zh/sls/loongcollector-collection/ "")。

## **变更记录**

关于LoongCollector组件的变更记录，请参见 [LoongCollector发布历史](https://help.aliyun.com/zh/sls/loongcollector-release-history "")。