### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[产品概述](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/)[产品简介](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/product-introduction/)[客户案例](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/case-studies/)捷旅假期

# 捷旅假期

更新时间：2025-12-07 22:21:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：世纪联华](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/century-mart)[下一篇：石墨文档](https://help.aliyun.com/zh/functioncompute/fc-2-0/product-overview/shimo-docs)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

客户介绍

客户痛点

解决方案

使用效果

本文以捷旅假期为例，介绍如何通过函数计算、云消息队列 RocketMQ 版及对象存储等云服务，处理瞬时并发消息等问题。

## 客户介绍

深圳市捷旅国际旅行社有限公司（简称“深捷旅”），自2001年成立以来专注于酒店行业的客房分销业务以及酒店预订信息化水平建设，通过“捷旅假期”品牌打造了酒店B2B分销平台。深捷旅一直秉承“便捷、实惠、高效”的服务理念，围绕打造“中国B2B旅游生态圈”的目标前进。目前，全球合作的旅游分销渠道超过1万家，拥有全球超过60万家星级酒店资源，覆盖了全球300多个城市。

深捷旅与业内旅游头部OTA企业的多年深耕合作，为同程旅游、去哪儿、途牛旅游网、Expedia、Ctrip、Agoda、驴妈妈旅游网、马蜂窝旅游、国旅运通、大唐商旅等企业提供完美的酒店及票务服务。

## 客户痛点

深捷旅需要对接的酒店超过60万家，每天新增的信息超过千万条，信息并发脉冲性强且时效周期短，捷旅平台处理瞬时并发消息压力大。因此捷旅平台期望具备以下优势，缓解并发处理消息的压力。

- 并发处理能力：同时处理超过10万条的峰值消息。

- 弹缩处理能力：根据消息量的多少进行自动化毫秒级的扩缩容操作，使用成本按所需的实际资源付费。

- 支持多种触发方式：支持对象存储服务、消息存储等触发方式。

- 支持多种编程语言：支持Python、Go及Java等语言。

- 运维监控能力：支持快速部署更新及资源使用的实时监控，日志分析集成与报警能力。


## 解决方案

通过函数计算、云消息队列 RocketMQ 版及对象存储等云服务解决了捷旅平台的痛点：

- 函数计算支持监听多种数据源：

  - 监控处理业务量的变化，快速进行自适应的扩缩容操作。

  - 监控毫秒级的扩容，获得线性增长的业务处理能力。
- 函数计算支持多种编程语言，无需用户改变编程习惯。

- 函数计算支持便捷的部署、资源使用的实时监控、日志分析集成与报警能力。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2114615671/CAEQYBiBgIDD6fi53BgiIGY2NjM5MTIzOWJhZTRjOTU5NjlkMzgyMzA2NWU4Zjdl3963382_20230830144006.372.svg)

## 使用效果

- 业务稳健：函数计算可根据业务量进行扩缩容，使用函数计算后，深捷旅解决了之前按峰值配置资源方式的业务稳定性问题。

- 运维简单：运维发布有多种工具辅助进行。使用函数计算后，解决了资源扩缩容管理问题，减少了深捷旅开发运维人员的人力投入。

- 降低成本：利用函数计算的按需付费特性，在合适的规格下运行，使得整个资源得到了高效利用，不为闲置资源付费，降低了深捷旅的总体使用成本。