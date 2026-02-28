### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[分布式云容器平台ACK One](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/)[操作指南](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/)[注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/registered-clusters/)[Knative](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/knative/)Knative概述

# Knative概述

更新时间：2025-02-14 04:33:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用Fluid加速OSS文件访问](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-fluid-to-accelerate-access-to-oss-objects)[下一篇：注册集群FAQ](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/faq-about-registered-clusters)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

文档使用指引

Knative是基于Kubernetes的Serverless框架，旨在制定云原生、跨平台的Serverless编排标准。它整合容器构建、工作负载管理和事件模型，帮助您部署和管理Serverless工作负载，打造企业级Serverless平台。

## 组件介绍

阿里云容器服务Knative完全兼容开源Knative，并与容器服务ACK、消息、存储、网络等云产品进行了全方位的融合，提供生产级别的Knative能力。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2476074071/p755609.png)

作为一个通用的Serverless框架，Knative由以下核心组件组成：

- Serving：管理Serverless工作负载以对外提供服务，提供自动扩缩容和灰度发布功能，在没有服务需要处理时，可缩容至零个实例。

- Eventing：针对Serverless事件驱动模式提供了事件的接入、注册、订阅、过滤和触发等一系列完整的事件管理能力。事件模型有效解耦了生产者和消费者，允许生产者在消费者启动前产生事件，消费者在生产者启动前监听事件。

- Function: 简化了创建、构建和部署Knative服务的流程，让您无需深入了解底层技术栈（如Kubernetes、容器和Knative），即可将无状态、事件驱动的函数作为Knative服务部署到Kubernetes集群中。


## 使用说明

注册集群支持使用Knative功能，使用时，您需要满足以下条件：

- 已创建注册集群，并将自建Kubernetes集群（当前仅支持Kubernetes 1.18版本）接入注册集群。具体操作，请参见 [创建注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-ack-one-registered-clusters#task-skz-qwk-qfb "")。

- 已通过kubectl连接注册集群。具体操作，请参见 [获取集群KubeConfig并通过kubectl工具连接集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/obtain-the-kubeconfig-file-of-a-cluster-and-use-kubectl-to-connect-to-the-cluster "")。

- 仅支持线下集群的Calico路由反射器模式或Cilium BGP路由模式。


## 文档使用指引

| **功能** | **相关文档** |
| --- | --- |

|     |     |
| --- | --- |
| **功能** | **相关文档** |
| Knative版本发布说明 | [Knative版本发布说明](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/knative-version-release-notes1 "") |
| 阿里云Knative和开源Knative对比 | [阿里云Knative和开源Knative对比](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/comparison-between-alibaba-cloud-knative-and-open-source-knative "") |
| Knative组件管理 | - [部署与管理Knative组件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-knative "")<br>  <br>- [管理Knative组件](https://help.aliyun.com/zh/ack/deploy-a-knative-component "") |
| Knative服务管理 | - [快速部署一个Knative服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-knative-to-deploy-serverless-applications "")<br>  <br>- [为Knative选择网关](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-between-kourier-and-alb-ingresses/ "")<br>  <br>- [创建修订版本](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-revision "")<br>  <br>- [配置HTTPS证书访问](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-access-over-https "")<br>  <br>- [使用自定义域名](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/set-a-custom-domain-name-for-knative-serving "")<br>  <br>- [基于流量灰度发布服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-a-canary-release-for-a-knative-service-1 "")<br>  <br>- [在Knative中部署gRPC服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-grpc-service-in-knative "")<br>  <br>- [基于AHPA实现定时自动扩缩容](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/knative-combined-with-ahpa-to-realize-timing-elasticity-based-on "") |
| Knative事件驱动 | - [部署Knative Eventing](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-knative-eventing-1693822907541 "")<br>  <br>- [在Knative中使用EventBridge事件驱动](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-eventbridge-to-trigger-knative-services-to-consume-events "") |
| Knative函数部署 | [部署Knative Functions](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/creating-knative-based-functions-with-knative-functions "") |
| KServe | - [部署KServe组件](https://help.aliyun.com/zh/ack/knative-support-kserve "")<br>  <br>- [基于KServe快速部署一个推理服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/quickly-deploy-the-first-inference-service-based-on-kserve "") |
| Knative最佳实践 | - [使用ECI资源](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-elastic-container-instances-in-knative "")<br>  <br>- [基于流量请求数实现服务自动扩缩容](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-automatic-scaling-for-pods-based-on-the-number-of-requests "")<br>  <br>- [在Knative中使用HPA](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-hpa-in-knative "")<br>  <br>- [查看Knative服务监控大盘](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/view-the-knative-dashboard-in-prometheus-service-1 "")<br>  <br>- [通过云效实现Knative服务持续交付](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-apsara-devops-to-implement-continuous-knative-service-delivery "")<br>  <br>- [基于Knative部署生产级别的Stable Diffusion服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/knative-based-stable-diffusion-service-best-practices "") |