### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[产品概述](https://help.aliyun.com/zh/sae/product-overview/)[产品简介](https://help.aliyun.com/zh/sae/product-overview/product-introduction/)应用场景

# 应用场景

更新时间：2024-10-24 01:24:23

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：开源自建对比](https://help.aliyun.com/zh/sae/product-overview/comparison-between-sae-and-open-source-services)[下一篇：使用限制](https://help.aliyun.com/zh/sae/product-overview/limits)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

应用托管

极致弹性场景

持续集成与交付

任务托管

Serverless 应用引擎 SAE（Serverless App Engine）具有广泛的应用场景，帮助您的企业极速上云、从容应对突发性流量洪流和灵活启停应用环境，降低资源成本。

## 应用托管

在企业生产环境中，通过合理拆分微服务，将每个微服务应用压缩为WAR包、JAR包、Docker镜像存储在阿里云镜像仓库。您只需基于Spring Cloud或Dubbo等框架开发规范迭代每个微服务应用，由SAE提供底层资源调度、部署、灰度发布、微服务治理和监控诊断等能力。

- 零改造：SAE能够平滑迁移应用，零改造地完成Spring Cloud或Dubbo应用快速上云。

- 免运维：SAE能够免运维底层基础设施，例如IaaS、K8s、微服务组件和APM组件等，无需自建ZooKeeper、Eureka、Consul和Skywalking等，极大降低开发运维成本。提供商业化稳定性兜底。

- 低门槛：SAE能够一站式开箱使用全套微服务能力，提供自动构建镜像能力，内置灰度发布、流量控制、环境隔离、应用监控诊断和权限管理等企业级高级特性。


![dg_microservice_application_hosting](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4901920361/p307531.png)

## 极致弹性场景

新零售、电商、在线教育、互娱等行业往往有一些不可预期的突发流量高峰，不易平衡业务SLA和资源成本，极易造成系统响应延迟、系统瘫痪等问题。为了解决这些问题，SAE提供了精准容量+弹性+限流降级一整套高可用产品化解决方案。通过该方案，SAE能够帮助应用轻松应对流量高峰，在保证业务SLA的同时也节省了资源成本。

- 保障高峰期业务SLA：基于SAE弹性+AHAS限流降级，轻松应对流量洪峰，避免系统崩溃。

- 快速诊断定位问题：SAE无缝集成的ARMS产品，具有白屏化应用监控和诊断能力，可用定位到慢SQL、慢方法、方法的调用堆栈、对于线上问题的分析、排查、预警和解决，提供强有力支持，节省大量的排查时间。

- 提升效率与降低成本：基于SAE丰富的弹性策略，无需按照峰值长期固定保有机器，提供秒级的弹性效率与实惠的硬件成本。


![dg_autoscaling_scenes](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4901920361/p307534.png)

## 持续集成与交付

SAE支持云效、Jenkins、源代码、Cloud Toolkit插件、容器镜像服务等多种部署方式，能够帮您自动完成从代码提交到应用和任务部署的DevOps完整流程，高效替代业内部署复杂、迭代缓慢的传统方式，实现了高效的持续交付流程。

- DevOps自动化：实现从代码变更到代码构建、镜像构建和应用部署的全流程自动化。

- 一键部署到云端：基于Cloud Toolkit插件部署，本地开发完应用后能一键部署到云端，方便您进行远程调试。

- CI/CD：通过SAE Job，执行完CI/CD持续集成任务后，能立即释放计算资源。


![dg_continuous_integration_and_delivery](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6982301561/p307536.png)

## 任务托管

聚焦于泛互联网、新零售、电商、文化传媒、制造、 IoT、物流、金融证券、医疗卫健和保险等行业。主要场景如下：

- 定时任务：定时拉取数据、爬虫。

- 批处理数据：数据清洗、转换、分析，对实时性要求低。

- 异步执行解耦：异步状态刷新以及离线查询。

- 开源任务框架迁移：XXL-JOB改造迁移等。

- 微服务架构：与原有的微服务架构进行调用通信、流程解耦。

- CI/CD：用SAE Job作为构建镜像的载体实现GitOps ，从而完善CI/CD的流程。


![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6885861071/p744087.png)

相比开源的分布式框架，其优点在于全托管免运维的用户体验，开箱即用的完备功能以及白屏化管控，任务运行完立即释放资源，不会浪费闲置资源成本。

SAE支持XXL-JOB零改造迁移，您无需修改任何代码和配置，即可将XXL-JOB应用部署至SAE Job，您只需为任务实际执行逻辑过程付费。在此过程中SAE Job充当了XXL-JOB的调度中心和执行器，您只需聚焦任务代码和简单配置（例如任务模板、并发重试），由SAE负责无侵入地进行任务调度和管控。