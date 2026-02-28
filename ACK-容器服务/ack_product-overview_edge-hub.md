### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[边缘](https://help.aliyun.com/zh/ack/product-overview/edge/)edge-hub

# edge-hub

更新时间：2024-12-19 04:13:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：terway-edge](https://help.aliyun.com/zh/ack/product-overview/terway-edge)[下一篇：edge-tunnel](https://help.aliyun.com/zh/ack/product-overview/edge-tunnel)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

变更记录

2024年12月

2023年11月

2023年08月

2022年12月

2022年01月

2021年11月

2021年10月

2021年09月

2021年07月

edge-hub组件是节点维度的SideCar，以Static Pod形态运行在每个节点上。v0.12.0以及之后的版本组件中，边缘节点池内edge-hub以systemd service形态运行，云端节点池内cloud-hub以DaemonSet形态运行在每个节点上。本文介绍edge-hub的组件介绍、使用说明和变更记录。

## 组件介绍

edge-hub组件是节点上其他组件（如kubelet、kube-proxy、Flannel和CoreDNS等）和云端kube-apiserver之间的流量代理，有边缘（Edge）和云端（Cloud）两种运行模式。其中边缘的edge-hub会缓存云端返回的数据，edge-hub组件在云端命名为cloud-hub。

该组件的主要功能如下：

- 提供数据缓存能力。即使云端断网时，业务Pod重启时可以从edge-hub中获取到本地缓存数据，避免业务中断。

- 支持kube-apiserver访问链路自适应，支持使用InClusterConfig的Pod通过edge-hub代理访问kube-apiserver。

- 支持服务拓扑的路由选择，通过无感知过滤EndpointSlice资源以支持服务拓扑能力，使集群内的Service访问流量仅转发到同一节点池内的后端Pod实例。

- 支持系统组件的镜像仓库自动适配，在专线或公网连接场景下，系统组件会自动切换为使用私网镜像或公网镜像。


![手动开启edge-hub的数据缓存能力](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4977931071/p338541.png)

## 使用说明

关于如何使用edge-hub组件，请参见 [设置边缘节点自治](https://help.aliyun.com/zh/ack/ack-edge/user-guide/configure-node-autonomy#task-2481912 "")、 [在边缘场景无缝运行使用InClusterConfig的业务Pod](https://help.aliyun.com/zh/ack/ack-edge/user-guide/run-application-pods-that-use-inclusterconfig-at-the-edge-without-making-pod-facing-changes#task-2121245 "")。

## 变更记录

### 2024年12月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.12.3 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.12.3 | - 配套v1.26.3-aliyun.1、1.28.9-aliyun.1、1.30.7-aliyun.1版本的ACK Edge集群。<br>  <br>- 支持terway-edge组件的本地缓存能力。 | 2024年12月19日 | 此次升级不会对业务造成影响。 |

### 2023年11月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.12.0 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.12.0 | - 配套v1.26.3-aliyun.1版本的ACK Edge集群。<br>  <br>- 调整组件的部署形态。<br>  <br>  - 将边缘节点池内的edge-hub调整为systemd service形态部署。<br>    <br>  - 云端节点池内的cloud-hub调整为DaemonSet形态部署。 | 2023年11月28日 | 此次升级不会对业务造成影响。 |

### 2023年08月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.11.0 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.11.0 | 配套v1.24.6-aliyunedge.1版本的ACK Edge集群。 | 2023年08月03日 | 此次升级不会对业务造成影响。 |

### 2022年12月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.10.3 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.10.3 | 配套v1.22-aliyunedge.1版本的ACK Edge集群。 | 2022年12月07日 | 此次升级不会对业务造成影响。 |

### 2022年01月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.10.0 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.10.0 | v1.20.11-aliyunedge.1集群的首个edge-hub版本。<br>- 健康检查增强：解决了kubelet停止后 **edge-hub** 仍一直上报心跳的问题。<br>  <br>- 节点证书管理增强： **edge-hub** 证书残留状态下，节点接入其他集群时自动更新 **edge-hub** 证书。<br>  <br>- 完善云边流量统计：在边缘节点上提供请求粒度的流量统计数据（ **edge-hub endpoint**: http://127.0.0.1:10267/metrics）。<br>  <br>- 稳定性增强：解决边缘请求高并发状态下触发数据竞争问题。 | 2022年01月27日 | 此次升级不会对业务造成影响。 |

### 2021年11月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.9.5 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.9.5 | 修复边缘请求不带Accept Header被拒绝的问题。 | 2021年11月15日 | 此次升级不会对业务造成影响。 |
| v0.9.4 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.9.4 | 修复HTTPS Server证书usage在各语言识别不一致的问题。 | 2021年11月01日 | 此次升级不会对业务造成影响。 |

### 2021年10月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.9.3 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.9.3 | - 修复数据过滤框架中数据过长被截断的问题。<br>  <br>- 支持LB Service忽略边缘过滤。 | 2021年10月27日 | 此次升级不会对业务造成影响。 |
| v0.9.2 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.9.2 | - 支持HTTPS Server能力，增加10268端口。<br>  <br>- 支持边缘数据过滤框架。 | 2021年10月12日 | 此次升级对存量业务无影响。如果存量业务需要使用新增功能，需要重新创建Pod。 |

### 2021年09月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.9.1 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.9.1 | 支持Windows系统的边缘节点。 | 2021年09月23日 | 此次升级不会对业务造成影响。 |

### 2021年07月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v0.9.0 | registry.cn-hangzhou.aliyuncs.com/acs/edge-hub:v0.9.0 | v1.18.8-aliyunedge.1集群的首个edge-hub版本。 | 2021年07月12日 | 此次升级不会对业务造成影响。 |