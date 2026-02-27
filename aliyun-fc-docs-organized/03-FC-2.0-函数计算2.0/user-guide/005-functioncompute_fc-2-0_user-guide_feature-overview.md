### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/programming-languages/)[编程模型扩展](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/programming-model-extensions/)功能简介

# 功能简介

更新时间：2025-12-07 22:24:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：函数实例生命周期回调](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/lifecycle-hooks-for-function-instances-7)[下一篇：管理服务](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-services)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

常驻应用与FaaS运行环境

编程模型扩展

计费说明

本文介绍函数计算基于传统常驻应用所拓展的运行时扩展功能，帮助您消除闲置成本。

## 常驻应用与FaaS运行环境

传统常驻的虚拟机或者托管容器类服务通常从实例启动到结束作为计费区间，即使该时间段没有业务请求仍然需要付费。函数计算提供1 ms计费粒度，且只在有实际请求的区间内计费，在请求以外的时间段内实例会被冷冻。这样基本消除了完全事件驱动的计费模型的闲置成本，然而冷冻机制也会打破一些传统架构下long-running进程的假设，加大应用迁移的难度。例如常用的开源分布式链路追踪Tracing Analysis库或者是第三方APM解决方案由于函数计算特殊的运行环境无法正确上报数据。

下列痛点都阻碍传统应用平滑迁移至Serverless架构：

- 异步背景指标数据延迟或丢失：如果在请求期间没有发送成功，则可能被延迟至下一次请求，或者数据点被丢弃。

- 同步发送指标增加延迟：如果在每个请求结束后都调用类似Flush接口，不仅增加了每个请求的延迟，对于后端服务也产生了不必要的压力。

- 函数优雅下线：实例关闭时应用有清理连接，关闭进程，上报状态等需求。在函数计算中实例下线时机开发者无法掌握，也缺少Webhook通知函数实例下线事件。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2924615671/CAEQYRiBgMCz456v3hgiIGJjOTFhMzBmM2NmMTQ2OTM4MjBkODA3Y2NmMmQ5ZDg23963382_20230830144006.372.svg)

## 编程模型扩展

函数计算针对上述痛点发布了运行时扩展（runtime extensions）功能。该功能在现有的HTTP服务编程模型上扩展，在已有的HTTP服务器的模型中增加了PreFreeze和PreStop webhooks。扩展开发者实现HTTP handler，监听函数实例生命周期事件。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2924615671/CAEQNBiBgIDJ_5eZ4xgiIDA2OTM2MDg4ZjEyYzRlMGU5YzIxZDBjZjgyMzRlMjc13963382_20230830144006.372.svg)

- PreFreeze：在每次函数计算服务决定冷冻当前函数实例前，函数计算服务会调用HTTP GET /pre-freeze路径，扩展开发者负责实现相应逻辑以确保完成实例冷冻前的必要操作，例如等待指标发送成功等。函数调用InvokeFunction的时间不包括PreFreeze hook的执行时间。
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2924615671/CAEQYRiBgMDYybGm3hgiIDAyZDljMzg1ZDJiMzRmZmE5NzNlZmM0OTQ3NzUyZWQw3963382_20230830144006.372.svg)
- PreStop：在每次函数计算决定停止当前函数实例前，函数计算服务会调用HTTP GET /pre-stop路径，扩展开发者负责实现相应逻辑以确保完成实例释放前的必要操作，如关闭数据库链接，以及上报、更新状态等。
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2924615671/CAEQNBiBgIDzlpmZ4xgiIGM5YjBkMTdjNDcxMjQyYzRhOWMwZjcwOGJlYTE5N2Qy3963382_20230830144006.372.svg)

## 计费说明

唤起PreFreeze或PreStop中产生的同InvokeFunction计费方式一致。扩展HTTP hooks请求数不做计费。扩展在单实例多并发的场景下依然适用，假设同时有多个Invoke请求在相同实例执行，在所有请求都结束后即将冷冻实例之前会调用一次PreFreeze hook。以下图为例，函数规格为1 GB，从t1 PreFreeze开始到t6请求2结束的时间段（假设为1秒），则实例执行时间为t6-t1，消耗1s \* 1 GB=1 CU。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2924615671/CAEQNBiBgIDli5qZ4xgiIGMzNWEwOTAzZDY3MjQ5YTc5YjBhYWY1MzA4MmY3OWQ53963382_20230830144006.372.svg)