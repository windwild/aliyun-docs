### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [操作指南](https://help.aliyun.com/zh/sae/user-guide/) [应用访问和流量管理](https://help.aliyun.com/zh/sae/sae-network-related-concepts-and-capabilities/) [微服务治理](https://help.aliyun.com/zh/sae/microservice-governance/) 接口详情

# 接口详情

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：应用概览](https://help.aliyun.com/zh/sae/serverless-app-engine-upgrade/user-guide/application-overview)[下一篇：节点详情](https://help.aliyun.com/zh/sae/node-details)

该文章对您有帮助吗？

反馈

接口详情页面主要展示该应用所有接口的QPS、异常请求、RT、并发等数据。

## **前提条件**

- 已 [部署应用](https://help.aliyun.com/zh/sae/sae-application-deployment/ "")。

- 已 [开通MSE微服务治理](https://help.aliyun.com/zh/mse/activate-microservices-governance "")。







**说明**

使用MSE时会产生单独费用。MSE的计费说明，请参见 [微服务治理计费概述](https://help.aliyun.com/zh/mse/product-overview/billing-overview "") 和 [【产品变更】SAE集成的MSE微服务治理功能商用通知](https://help.aliyun.com/zh/sae/product-overview/product-change-commercial-notice-of-non-destructive-up-and-down-line-and-gray-rule-function "")。


## **使用限制**

适用于2023年11月08日起新建的微服务应用。

## **功能入口**

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

2. 在左侧导航栏，选择**微服务治理** \> **接口详情**。


## 功能介绍

**接口详情** 页面展示该应用的所有接口的详细信息，包括统计的QPS、RT、并发等数据。单击各类型的页签可以进入各个类型的接口详情页面，包括 **WEB服务**、 **RPC服务** 和 **自定义接口** 等，各个类型页面的主要功能如下。

**说明**

监控回放仅支持回放一天内的指标数据，节点维度指标只支持回放当前在线节点。

## WEB服务

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8955760471/p792225.png)

- （图标①）可以预览 **服务端** 以及 **客户端** 的WEB接口列表，以及每个接口最近五分钟的 **请求量**、 **拒绝量**、 **RT**、 **成功率** 等信息，提供多种筛选排序能力，包含资源名称搜索、已配置防护规则的接口筛选以及请求量/拒绝量/RT/成功率排序。接口右侧![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1439143171/p792226.png)标志表示该接口配置了防护规则。







**说明**

**已配置防护规则的接口** 筛选条件会筛选出配置了防护规则的接口（忽略规则是否开启）。

- （图标②）选择当前接口的各种功能页签。



  - **接口概览**：以QPS、RT、并发各数据的统计维度展现选中的接口数据。

  - **节点详情**：分节点查看当前接口QPS、RT、并发等各项数据。

  - **接口流控**：配置选中接口的流控规则。具体操作，请参见 [配置流控规则](https://help.aliyun.com/zh/sae/flow-protection#a512802072ua8 "")。

  - **并发隔离**：配置选中接口的隔离规则。具体操作，请参见 [配置隔离规则](https://help.aliyun.com/zh/sae/flow-protection#977b1dd07254v "")。

  - **热点参数防护（HTTP 请求）**：配置选中接口的热点参数防护（HTTP请求）规则配置界面（仅对服务端接口可见）。具体操作，请参见 [配置热点参数防护（HTTP请求）规则](https://help.aliyun.com/zh/sae/flow-protection#173c3c6072kgq "")。


- （图标③）根据②中的选择展示相关的信息。

- （图标④）选择回放时间，①、③部分展示所选时间对应的指标数据。


**说明**

Java应用网关的展示页面不区分服务类型以及服务端或客户端，展示页面与WEB服务类型服务端相同，①处展示路由名。

## RPC服务

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1439143171/p791462.png)

- （图标①）可以预览 **服务端** 以及 **客户端** 的RPC服务接口列表，以及每个接口当前时间的 **请求量**、 **拒绝量**、 **RT**、 **成功率** 等信息，提供资源名搜索能力。







**说明**

RPC服务的接口列表为两层结构，第一层为RPC服务类名，第二层为方法名。

- （图标②）选择当前接口的各种功能页签。



  - **接口概览**：以QPS、RT、并发各数据的统计维度展现选中的接口数据。

  - **节点详情**：分节点查看当前接口QPS、RT、并发等各项数据。

  - **接口流控**：配置选中接口的流控规则。具体操作，请参见 [配置流控规则](https://help.aliyun.com/zh/sae/flow-protection#a512802072ua8 "")。

  - **并发隔离**：配置选中接口的隔离规则。具体操作，请参见 [配置隔离规则](https://help.aliyun.com/zh/sae/flow-protection#977b1dd07254v "")。

  - **热点参数防护（RPC）**：配置选中接口的热点参数防护（RPC请求）规则配置界面（仅对客户端接口可见）。具体操作，请参见 [配置热点参数防护（RPC）规则](https://help.aliyun.com/zh/sae/flow-protection#1598777072dlo "")。


- （图标③）根据②中的选择展示相关的信息。

- （图标④）选择回放时间，①、③部分展示所选时间对应的指标数据。


## 自定义接口

当您添加了自定义接口后，节点详情才会展示自定义接口的相关信息。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1439143171/p791450.png)

- （图标①）可以预览服务接口列表，以及每个接口当前时间的 **请求量**、 **拒绝量**、 **RT**、 **成功率** 等信息，提供多种筛选排序能力，包含资源名称搜索、已配置防护规则的接口筛选以及请求量/拒绝量/RT/成功率排序。







**说明**

**已配置防护规则的接口** 筛选条件会筛选出配置了防护规则的接口（忽略规则是否开启）。

- （图标②）选择当前接口的各种功能页签。



  - **接口概览**：以QPS、RT、并发各数据的统计维度展现选中的接口数据。

  - **节点详情**：分节点查看当前接口QPS、RT、并发等各项数据。

  - **接口流控**：配置选中接口的流控规则。具体操作，请参见 [配置流控规则](https://help.aliyun.com/zh/sae/flow-protection#a512802072ua8 "")。

  - **并发隔离**：配置选中接口的隔离规则。具体操作，请参见 [配置隔离规则](https://help.aliyun.com/zh/sae/flow-protection#977b1dd07254v "")。

  - **服务熔断**：配置选中接口的服务熔断规则配置界面（仅对客户端接口可见）。具体操作，请参见 [配置熔断规则](https://help.aliyun.com/zh/sae/flow-protection#126ab72072hfg "")。


- （图标③）根据②中的选择展示相关的信息。

- （图标④）选择回放时间，①、③部分展示所选时间对应的指标数据。