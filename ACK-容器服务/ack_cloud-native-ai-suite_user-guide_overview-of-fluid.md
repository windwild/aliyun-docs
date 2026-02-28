### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[云原生AI套件](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/)[操作指南](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/)弹性数据集

# 数据加速Fluid概述

更新时间：2025-11-17 01:28:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置NAS共享存储](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/configure-a-shared-nas-volume)[下一篇：升级ack-fluid组件](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/install-and-update-ack-fluid)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

视频介绍

Fluid功能介绍

Fluid重要概念

相关文档

Fluid是一个开源的Kubernetes原生的分布式数据集编排和加速引擎，主要服务于云原生场景下的数据密集型应用，例如大数据应用、AI应用等。本文介绍数据加速的核心功能和重要概念。

## **视频介绍**

弹性数据集

## Fluid功能介绍

Fluid通过定义数据集（Dataset）和数据运行时引擎（Runtime）资源，实现如下图所示的功能。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7880633671/CAEQQRiBgICPhqOL9RgiIDNhZWQ1OGVhNTk5NDRhZDA4NjdhNmUxM2QzMjczZjI53963382_20230830144006.372.svg)

- 数据集抽象原生支持：将数据密集型应用所需基础支撑能力功能化，实现数据高效访问并降低多维管理成本。

- 可扩展的数据引擎插件：提供统一的访问接口，方便接入第三方存储，通过不同的Runtime实现数据操作。

- 自动化的数据操作：提供多种操作模式，与自动化运维体系相结合。

- 数据弹性与调度：将数据缓存技术和弹性扩缩容、数据亲和性调度能力相结合，提高数据访问性能。

- 运行时平台无关：支持原生、边缘、Serverless Kubernetes集群、Kubernetes多集群等多样化环境，适用于混合云场景。


## Fluid重要概念

- Dataset：数据集是逻辑上相关的一组数据的集合，会被运算引擎使用。例如，大数据场景的Spark和AI场景的TensorFlow。而这些数据智能的应用会创造工业界的核心价值。Dataset的管理实际上也有多个维度，例如安全性、版本管理和数据加速。

- Runtime：实现数据集安全性、版本管理和数据加速等能力的执行引擎，定义了一系列生命周期的接口。可以通过实现这些接口，支持数据集的管理和加速。

- AlluxioRuntime：来源于 [Alluxio](https://www.alluxio.org/) 社区，是支撑Dataset数据管理和缓存的执行引擎实现，支持PVC，Ceph，CPFS加速，有效支持混合云场景。

- JuiceFSRuntime: 基于JuiceFS的分布式缓存加速引擎，支持场景化的数据缓存和加速能力。关于JuiceFS的更多信息，请参见 [JuiceFS简介](https://juicefs.com/docs/zh/community/introduction/)。关于如何在Fluid中使用JuiceFS，请参见 [在Fluid中使用JuiceFS](https://juicefs.com/docs/zh/cloud/kubernetes/fluid/)。

- JindoRuntime：来源于阿里云EMR团队 [JindoFS](https://help.aliyun.com/zh/emr/emr-on-ecs/user-guide/jindodata-available-only-for-existing-users/#concept-2217192 "")，是基于C++实现的支撑Dataset数据管理和缓存的执行引擎，可支持OSS对象存储、 [OSS-HDFS](https://help.aliyun.com/zh/emr/emr-on-ecs/user-guide/overview-36#concept-2278620 "") 以及HDFS的数据访问加速。

- ThinRuntime：可扩展的通用存储系统实现，允许用户以低代码方式接入各类存储系统，复用Fluid提供的数据编排管理、运行时平台访问接入核心能力。


**重要**

通过ack-fluid使用的分布式缓存加速引擎AlluxioRuntime、JuiceFSRuntime均为第三方开源社区/商业公司提供的免费开源组件。您可以按需选用并安装相应的服务端组件和客户端组件，以此获得分布式缓存服务。

但阿里云不承担第三方组件相关的稳定性、服务限制与安全合规等责任。您应及时关注对应第三方开源社区或商业公司的官网、代码托管平台的版本更新动态并仔细阅读及遵守相应的开源协议，自行承担因第三方组件导致的应用侧程序开发、维护、故障与安全等潜在风险。

| **特性** | **Alluxio** | **JuiceFS** | **Jindo** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **特性** | **Alluxio** | **JuiceFS** | **Jindo** |
| 底层存储类型 | PVC、Ceph、HDFS、CPFS、NFS和OSS等 | JuiceFS | OSS、OSS-HDFS、PVC |
| 支持方式 | 开源社区 | 开源社区 | 阿里云产品 |

## 相关文档

- [JindoFS加速OSS文件访问](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/use-jindofs-to-accelerate-access-to-oss#task-2057532 "")

- [Serverless数据访问加速](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/overview-of-data-access-in-serverless-cloud-computing/#concept-2233020 "")

- [开启Fluid组件监控](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/enable-monitoring-for-the-fluid-components#task-2321185 "")