### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/)[操作指南](https://help.aliyun.com/zh/ack/ack-edge/user-guide/)组件管理

# 组件管理

更新时间：2025-01-22 22:02:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：通过ACK Edge集群使用ACS算力](https://help.aliyun.com/zh/ack/ack-edge/user-guide/use-acs-computing-power-through-ack-edge-clusters)[下一篇：应用管理](https://help.aliyun.com/zh/ack/ack-edge/user-guide/application-management-overview/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

组件管理

组件类型

核心组件

应用管理

日志与监控

存储

网络

安全

弹性伸缩

其他

容器服务 Edge 版提供多种类型的组件，您可以根据业务需求部署、升级、卸载组件。本文从功能维度列举容器服务 Edge 版管理的集群组件。

## 前提条件

已创建ACK Edge集群。具体信息，请参见 [创建集群](https://help.aliyun.com/zh/ack/ack-edge/user-guide/create-an-ack-edge-cluster-1 "")。

## 组件管理

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**运维管理** \> **组件管理**。

3. 在 **组件管理** 页面，您可以搜索并定位目标组件，在组件卡片上按需进行安装、卸载、升级、修改控制面参数等操作。


## 组件类型

容器服务ACK管理的集群组件类型包括系统组件和可选组件：

- 系统组件：创建ACK Edge集群时，默认安装的组件。不支持卸载，新版本发布后，需要您及时进行升级。

- 可选组件：创建ACK Edge集群时，可选择性安装的组件，用于扩展集群功能。您可以按需安装、卸载或更新配置。新版本发布后，请及时进行升级。


## 核心组件

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [Kube API Server](https://help.aliyun.com/zh/ack/product-overview/kube-api-server#task-2088866 "") | 系统组件 | Kubernetes集群的总线和入口网关。 |
| [Kube Controller Manager](https://help.aliyun.com/zh/ack/product-overview/kube-controller-manager#task-2088870 "") | 系统组件 | Kubernetes集群内部资源的管理器。 |
| [kube-scheduler](https://help.aliyun.com/zh/ack/product-overview/kube-scheduler "") | 系统组件 | 负责结合节点资源使用情况和Pod的调度要求将Pod调度到集群的合适节点上。 |
| [Cloud Controller Manager](https://help.aliyun.com/zh/ack/product-overview/cloud-controller-manager#concept-wk1-grd-qfb "") | 系统组件 | 提供Kubernetes与阿里云基础产品的对接能力，例如CLB、VPC等。 |
| [edge-controller-manager](https://help.aliyun.com/zh/ack/product-overview/edge-controller-manager "") | 系统组件 | 提供边缘节点生命周期管理等功能。 |
| [edge-cloud-provider-manager](https://help.aliyun.com/zh/ack/product-overview/edge-cloud-provider-manager "") | 系统组件 | 对接阿里云边缘产品，例如ELB（ENS负载均衡）等。 |
| [yurt-app-manager](https://help.aliyun.com/zh/ack/product-overview/yurt-app-manager "") | 系统组件 | yurt-app-manager是为ACK Edge集群提供边缘单元化管理的功能组件，例如nodepool、yurtappset等。 |
| [edge-hub](https://help.aliyun.com/zh/ack/product-overview/edge-hub#concept-2181868 "") | 系统组件 | 节点上其他组件和云端kube-apiserver之间的流量代理，有边缘（Edge）和云端（Cloud）两种运行模式。 |

## 应用管理

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [OpenKruise](https://help.aliyun.com/zh/ack/product-overview/openkruise#task-2097121 "") | 可选组件 | 提供高效管理应用容器、Sidecar容器及镜像分发功能。 |
| [migrate-controller](https://help.aliyun.com/zh/ack/product-overview/migrate-controller#task-1955070 "") | 可选组件 | 基于开源项目Velero开发的一个Kubernetes应用迁移的组件。 |

## 日志与监控

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [alicloud-monitor-controller](https://help.aliyun.com/zh/ack/product-overview/alicloud-monitor-controller#concept-1918110 "") | 系统组件 | ACK提供对接云监控的系统组件。 |
| [metrics-server](https://help.aliyun.com/zh/ack/product-overview/metrics-server#concept-1918212 "") | 系统组件 | ACK基于社区开源监控组件进行改造和增强的监控采集和离线组件，并提供Metrics API进行数据消费，提供HPA的能力。 |
| [ack-node-problem-detector](https://help.aliyun.com/zh/ack/product-overview/ack-node-problem-detector#concept-1935269 "") | 可选组件 | ACK基于社区开源项目进行改造和增强的集群节点异常事件监控组件，以及对接第三方监控平台功能的组件。 |
| [logtail-ds](https://help.aliyun.com/zh/sls/sls-release-notes#concept-w5w-q3q-zdb "") | 可选组件 | 使用日志服务采集Kubernetes容器日志。 |
| [ack-onepilot](https://help.aliyun.com/zh/ack/product-overview/ack-onepilot "") | 可选组件 | 用于对接应用实时监控服务ARMS和微服务引擎MSE，可以让部署在容器服务Kubernetes中的Java或Golang应用接入ARMS、MSE。 |
| [ags-metrics-collector](https://help.aliyun.com/zh/ack/ags-metrics-collector#concept-2066985 "") | 可选组件 | 为基因计算客户使用的监控服务组件，可以通过该组件监控基因工作流中各个节点资源使用的详细信息。 |
| [ack-arms-prometheus](https://help.aliyun.com/zh/ack/product-overview/ack-arms-prometheus "") | 可选组件 | 使用阿里云Prometheus实现容器服务集群监控。 |
| [ack-arms-cmonitor](https://help.aliyun.com/zh/ack/product-overview/ack-arms-cmonitor "") | 可选组件 | ACK集群中ARMS应用监控eBPF的监控组件。 |

## 存储

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [csi-plugin](https://help.aliyun.com/zh/ack/product-overview/csi-plugin#concept-2043905 "") | 可选组件 | 支持数据卷的挂载、卸载功能。<br>创建集群时，如果选择CSI插件实现阿里云存储的接入能力的话，默认安装该组件。 |
| [csi-provisioner](https://help.aliyun.com/zh/ack/product-overview/csi-provisioner#concept-2043907 "") | 可选组件 | 支持数据卷的自动创建能力。<br>创建集群时，如果选择CSI插件实现阿里云存储的接入能力的话，默认安装该组件。 |
| [storage-operator](https://help.aliyun.com/zh/ack/product-overview/storage-operator#task-2061194 "") | 可选组件 | 用于管理存储组件的生命周期。 |
| [node-resource-manager](https://help.aliyun.com/zh/ack/product-overview/node-resource-manager#concept-2066268 "") | 可选组件 | 提供节点计算、存储资源的自动化管理能力，当前支持LVM存储资源的管理。 |
| [csi-ens-plugin](https://help.aliyun.com/zh/ack/product-overview/csi-ens-plugin "") | 可选组件 | 支持ENS云盘数据卷的挂载和卸载。 |
| [csi-ens-provisioner](https://help.aliyun.com/zh/ack/product-overview/csi-ens-provisioner "") | 可选组件 | csi-ens-provisioner支持ENS云盘数据卷的创建。 |

## 网络

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [CoreDNS](https://help.aliyun.com/zh/ack/product-overview/coredns#concept-2071838 "") | 系统组件 | ACK集群中默认采用的DNS服务发现插件，其遵循Kubernetes DNS-Based Service Discovery规范。 |
| [Flannel](https://help.aliyun.com/zh/ack/product-overview/flannel#task-2065315 "") | 系统组件 | 一种容器网络接口CNI（Container Network Interface）插件，在阿里云上使用的Flannel网络模式采用阿里云VPC模式。<br>创建集群时，如果选择Flannel网络插件实现集群内部网络互通的话，默认安装该组件。 |
| [terway-edge](https://help.aliyun.com/zh/ack/ack-edge/user-guide/terway-edge-network-plug-in-introduction "") | 系统组件 | 通过Terway Edge作为CNI插件提供Underlay容器网络通信。 |
| [ALB Ingress Controller](https://help.aliyun.com/zh/ack/product-overview/alb-ingress-controller "") | 可选组件 | 基于阿里云应用型负载均衡ALB（Application Load Balancer） ，提供更为强大的Ingress流量管理方式，兼容Nginx Ingress，具备处理复杂业务路由和证书自动发现的能力，支持HTTP、HTTPS和QUIC协议，满足在云原生应用场景下对超强弹性和大规模七层流量处理能力的需求。ACK Edge中只支持部署在云端节点池的Pod。 |

## 安全

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [aliyun-acr-credential-helper](https://help.aliyun.com/zh/ack/product-overview/aliyun-acr-credential-helper#concept-1920215 "") | 系统组件 | 一个可以在ACK集群中免密拉取ACR默认版或企业版私有镜像的组件。 |
| [gatekeeper](https://help.aliyun.com/zh/ack/product-overview/gatekeeper#task-1938542 "") | 可选组件 | 帮助您方便地管理和应用集群内的Open Policy Agent（OPA）策略，实现命名空间标签管理等功能。 |
| [security-inspector](https://help.aliyun.com/zh/ack/product-overview/security-inspector#task-2552166 "") | 可选组件 | 实现安全巡检功能的关键组件。 |
| [policy-template-controller](https://help.aliyun.com/zh/ack/product-overview/policy-template-controller#task-2185042 "") | 可选组件 | 实现策略管理功能的关键组件。 |

## 弹性伸缩

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [ack-kubernetes-cronhpa-controller](https://help.aliyun.com/zh/ack/product-overview/ack-kubernetes-cronhpa-controller "") | 可选组件 | 用于实现资源定时扩容。 |

## 其他

| **组件名称** | **组件类型** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **组件名称** | **组件类型** | **描述** |
| [ack-koordinator（ack-slo-manager）](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#task-2172306 "") | 可选组件 | ACK支持差异化SLO（Service Level Objectives）能力的核心应用，可以在保证应用服务质量的同时，充分提升资源使用效率。 |
| [aliyun-acr-acceleration-suite](https://help.aliyun.com/zh/ack/product-overview/aliyun-acr-acceleration-suite "") | 可选组件 | ACR镜像按需加载组件。 |
| [raven-agent-ds](https://help.aliyun.com/zh/ack/product-overview/raven-agent-ds "") | 可选组件 | 跨域运维通信组件。 |
| [edge-tunnel](https://help.aliyun.com/zh/ack/product-overview/edge-tunnel#concept-2181877 "") （1.26版本中用Raven代替） | 可选组件 | edge-tunnel组件本质是一个反向通道，是解决跨网络通信的一种常见方式。 |