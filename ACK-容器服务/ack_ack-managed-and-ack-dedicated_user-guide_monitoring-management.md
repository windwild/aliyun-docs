### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[可观测性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/observability-overview/)监控管理

# 监控管理

更新时间：2025-06-03 23:16:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：采集集群节点的Systemd Journal日志数据](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/collect-the-systemd-journal-log-data-of-the-node)[下一篇：【停止维护】基础资源监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/monitor-basic-resources)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

集群可观测功能

ACK兼容阿里云可观测产品，例如云监控、阿里云Prometheus等，并提供丰富的集群监控组件，帮助您全面观测集群健康状况，提前识别并响应问题。本文介绍ACK集群的全链路监控解决方案，包括基础资源、应用、集群、事件、控制面组件、网络以及内核层容器监控。

## **集群可观测功能**

下表介绍ACK集群可观测功能的各个模块及其对应监控能力。

| **功能模块** | **功能描述** | **文档链接** | **相关** **组件** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能模块** | **功能描述** | **文档链接** | **相关** **组件** |
| 基础资源监控 | 通过云监控Kubernetes监控或Prometheus监控功能，您可以查看并监控CPU、内存、网络等基础资源的使用情况及健康状态，提供报警提醒和关键指标监控，确保集群的稳定运行。 | [【停止维护】基础资源监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/monitor-basic-resources "") | [metrics-server](https://help.aliyun.com/zh/ack/product-overview/metrics-server "") |
| [使用阿里云Prometheus监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-managed-service-for-prometheus-to-monitor-an-ack-cluster "") | [ack-arms-prometheus](https://help.aliyun.com/zh/ack/product-overview/ack-arms-prometheus "") |

| [开源Prometheus监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-open-source-prometheus-to-monitor-an-ack-cluster "") | ack-prometheus-operator |
| 应用监控 | 基于阿里云 [ARMS](https://help.aliyun.com/zh/arms/product-overview/what-is-arms#concept-42781-zh "")，通过安装ack-onepilot，实现容器应用的拓扑分析、接口与事务监控、调用链追踪和性能瓶颈检测。 | [Java应用监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/monitor-application-performance "") | [ack-onepilot](https://help.aliyun.com/zh/ack/product-overview/ack-onepilot "") |
| [Python应用监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/python-application-monitoring "") |
| [Golang应用监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/golang-application-monitoring "") |
| 集群监控 | [阿里云应用监控 eBPF 版](https://help.aliyun.com/zh/arms/application-monitoring-ebpf/product-overview/what-is-alibaba-cloud-application-monitoring-ebpf-version "") 为支持无侵入方式获取容器性能数据，快速定位Pod问题，并自动关联至相关服务和控制器工作负载，缩短问题发现时间。 | [集群拓扑监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/architecture-aware-monitoring "") | [ack-arms-cmonitor](https://help.aliyun.com/zh/ack/product-overview/ack-arms-cmonitor "") |
| 事件监控 | 结合使用NPD和SLS的Kubernetes事件中心，实现实时监控和通知系统状态，诊断并转换节点异常为事件，支持闭环告警和离线通知。 | [事件监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/event-monitoring "") | [ack-node-problem-detector](https://help.aliyun.com/zh/ack/product-overview/ack-node-problem-detector "") |
| 控制面组件监控 | 通过Prometheus和Grafana实时监控关键控制面组件（如API Server、etcd、kube-scheduler、kube-controller-manager），支持优化访问和自建Prometheus配置。 | [查看集群控制面组件监控大盘](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/view-control-plane-component-dashboards-in-ack-pro-clusters "") | [API Server](https://help.aliyun.com/zh/ack/product-overview/kube-api-server "") |
| [kube-controller-manager](https://help.aliyun.com/zh/ack/product-overview/kube-controller-manager "") |
| [cloud-controller-manager](https://help.aliyun.com/zh/ack/product-overview/cloud-controller-manager "") |
| [kube-scheduler](https://help.aliyun.com/zh/ack/product-overview/kube-scheduler "") |
| etcd |
| 网络监控 | 集成Ingress日志服务，支持Ingress Dashboard与ARMS联动排查，提供CoreDNS监控和问题解析。在Terway集群中，实现网络流量和业务拓扑的可视化展示，从而实现容器网络和服务可观测性。 | [Ingress Dashboard监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ingress-dashboard#task-2005246 "") | [Nginx Ingress Controller](https://help.aliyun.com/zh/ack/product-overview/nginx-ingress-controller "") |
| [CoreDNS组件监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/coredns-monitoring "") | [CoreDNS](https://help.aliyun.com/zh/ack/product-overview/coredns "") |
| [使用ACKTerway和CiliumHubble实现网络可观测性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/implement-network-observability-by-using-ack-terway-and-cilium-hubble "") | [Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway "") |
| 内核层容器监控 | 在操作系统内核层进行容器监控的方法，为集群提供独特的内核层监控和可观测能力，助力容器化部署和迁移。 | [SysOM内核层容器监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/sysom-kernel-level-container-monitoring "") | [ack-sysom-monitor](https://help.aliyun.com/zh/ack/product-overview/ack-sysom-monitor "") |