### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用开发](https://help.aliyun.com/zh/sae/sae-2-application-development/)使用Dubbo开发应用

# 使用Dubbo开发应用

更新时间：2025-01-13 01:23:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：搭建服务网关](https://help.aliyun.com/zh/sae/set-up-service-gateway)[下一篇：Dubbo开发概述](https://help.aliyun.com/zh/sae/dubbo-development-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

Dubbo的架构

相关文档

SAE支持原生Dubbo微服务框架，在该框架下开发的微服务只需添加依赖和修改配置，便可获得SAE企业级的微服务应用托管、微服务治理、监控报警和应用诊断等能力，实现零代码量应用迁移。

## Dubbo的架构

Dubbo的架构如下图所示。

![Dubbo 的架构](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3995983761/p70739.png)

1. 服务运行容器负责启动、加载、运行提供者服务。

2. 提供者在启动时，需要向注册中心进行注册。

3. 消费者在启动时，需要向注册中心订阅所需的服务。

4. 广播中心返回提供者地址列表给消费者。如果有变更，注册中心将基于长连接推送变更数据给消费者。

5. 消费者从提供者地址列表中，基于软负载均衡算法，选择某个提供者进行调用。如果调用失败，则重新调用其他提供者。

6. 消费者和提供者在内存中存储累计调用次数和调用时间，定时（每分钟）发送统计数据至监控中心。


## 相关文档

您可以参考以下示例开发Dubbo应用：

- [将Dubbo应用托管到SAE](https://help.aliyun.com/zh/sae/deploy-a-dubbo-application-on-sae "")：以包含服务提供者（本文简称Provider）和服务消费者（本文简称Consumer）的Dubbo微服务应用为例，使用XML配置的方式在本地开发Dubbo应用，并部署到SAE。

- [使用Spring Boot开发Dubbo应用](https://help.aliyun.com/zh/sae/use-spring-boot-to-develop-dubbo-applications "")：使用Spring Boot开发Dubbo应用，并使用SAE服务注册中心实现服务注册与发现。