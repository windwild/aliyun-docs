### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 完美日记

# 完美日记

更新时间：2024-03-27 06:31:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：【产品公告】关于停止维护Nginx Ingress Controller组件的公告](https://help.aliyun.com/zh/ack/product-overview/product-announcement-announcement-on-end-of-maintenance-for-nginx-ingress-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

客户介绍

业务痛点

阿里云的解决方案

使用的阿里云产品

业务价值

依托于阿里云容器服务ACK，完美日记走上容器化改造之路，通过ACK完成大规模应用部署及运维，让整个业务系统变得更加“轻松”。切换到Kubernetes正式环境后，容器服务扩容时间只需要约90秒，同时完美日记IT系统可以根据运营节奏进行扩容，服务器扩容成本可降低70%~90%。同时，应用的部署效率得到大幅提升，可按照模板创建服务，应用部署时间减少90%。

## **客户介绍**

完美日记成立于2016年，是广州逸仙电子商务有限公司旗下品牌。该品牌致力于探索欧美时尚趋势，同时结合亚洲女性面部和肌肤特点，研发一系列“高品质、精设计”的欧美时尚彩妆产品。

## **业务痛点**

- **自行维护服务器成本过高：** 早期互联网公司通常直接购买服务器，并在IDC机房租用机架进行部署，将应用程序直接运行在物理机上。如需扩展，就必须购买新的服务器。IDC机房可能频繁出现各种故障，导致业务稳定性大大降低。同时，如果IDC需要迁移，迁移的时间往往夜晚业务低峰时段且需要耗费大量人力。在资源成本、服务稳定性和工作效率等方面都会带来巨大的消耗。

- **人工发版繁琐易错：** 2019年双11大促前夕，完美日记小程序刚刚上线，采用传统的部署方式。某些应用需要在SLB上配置OpenResty Web平台，运维人员需要在SLB上手动依次勾选服务器，发布版本的时间长达半个小时以上。如果发版中出现问题，通常还需要延长一个小时以上的时间来完成故障排查。

- **大规模应用的研发与运维挑战：** 对于大规模应用的研发和运维人员来说，都需要考虑是否拥有足够的技术和能力来应对挑战，产品架构设计是否可以满足未来的企业需求，组织架构和文化是否已经适应企业的新战略发展。


## **阿里云的解决方案**

- **全栈容器化简化服务器运维：** 自2019年起，完美日记便开始筹备容器化改造，包括改造方案的设计和对阿里云Kubernetes服务的选择。经过仔细的测试和结合公司情况和人员配备情况，最终选择了阿里云容器服务ACK托管版集群来完成大规模应用部署，一次性将所有应用迁移至ACK，并以标准的Kubernetes方式进行运维部署。

- **全链路可观测和流量防护提升业务稳定性：** 基于容器服务ACK，完美日记将IT系统接入阿里云应用实时监控服务ARMS，跟踪复杂的服务调用，支持对异常服务进行快速定位和修复。可观测监控Prometheus版对ACK容器资源进行统一监控。同时，完美日记使用性能测试服务PTS进行压力测试，利用秒级流量和真实地理位置流量等特性进行测试。通过收集压测数据并分析系统的强依赖和关键瓶颈点，对关键业务接口、关键第三方调用、数据库慢调用等进行限流保护，提升业务稳定性。

- **简单稳定且低成本的容器镜像仓库服务：** 完美日记选用阿里云容器镜像服务企业版（ACR EE），相较于自建Harbor更为稳定、成本更低。自建Harbor需要考虑计算、数据库和磁盘成本，在项目很多或镜像较多场景下，磁盘成本会升高。而使用ACR EE无需考虑维护成本。此外，自建Harbor容易出现镜像拉取失败问题，而ACR EE可以实现高并发。

- **容器弹性灵活应对流量洪峰：** 利用ACK的快速弹性能力，完美日记可以从容应对大促资源快速扩容。同时，在大促前，完美日记使用阿里云云数据库RDS、阿里云安全等产品进行扩容、链路梳理、缓存、连接池预热、后端资源保障等，以确保大促活动的平稳进行。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2645351171/CAEQOxiBgMCMq4HK8BgiIDc4ZGY0NDAzZDlkZDQ3YjFiMDUwZmE2NWY3MDVkMmYy3963382_20230830144006.372.svg)

## **使用的阿里云产品**

- [阿里云容器服务ACK（Alibaba Cloud Container Service for Kubernetes）](https://www.aliyun.com/product/kubernetes)

- [阿里云容器镜像服务ACR（Alibaba Cloud Container Registry](https://www.aliyun.com/product/acr)

- [阿里云监控服务 Prometheus（Aliyun Cloud Monitor Prometheus）](https://www.aliyun.com/product/developerservices/prometheus)

- [阿里云实时监控服务（ARMS）](https://www.aliyun.com/product/arms)

- [阿里云性能测试PTS（Performance Testing Service）](https://www.aliyun.com/product/pts)

- [阿里云微服务引擎 MSE（Alibaba Cloud Microservice Engine，MSE）](https://www.aliyun.com/product/aliware/mse)

- [应用高可用服务 AHAS（Application High Availability Service）](https://www.aliyun.com/product/ahas)


## **业务价值**

- **极大提升运维效率，降低人力成本：** 容器化改造之后，完美日记的整个系统变得更加“轻松”。在切换到Kubernetes正式环境后，扩容时间只需约90秒，可以灵活配合产品运营节奏进行扩容，服务器扩容成本降低70%~90%。同时，应用部署效率大幅提升，只需要按照文件模板即可创建一个服务，部署时间可减少90%。

- **提升资源利用率，降低资源和管理成本：** 服务器资源可以自动计算并部署到服务器上，利用隔离技术可以部署多个项目服务器，提升约50%的服务器利用率。服务模块的自动负载均衡无需人工干预，人力工作量降低约90%。服务模块的伸缩容无需编写脚本，只需点击伸缩按钮即可实现弹性伸缩，大大减少人工错误率，工作量降低约70%。服务模块不可用时，ACK将自动剔除并自动重启服务模块。服务器宕机时，运行在服务器上的服务模块将自动转移至可用服务器上，无需人工干预，工作量显著降低。