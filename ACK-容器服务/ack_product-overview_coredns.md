### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[网络](https://help.aliyun.com/zh/ack/product-overview/network-3/)CoreDNS

# CoreDNS

更新时间：2025-11-20 03:04:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ALB Ingress Controller](https://help.aliyun.com/zh/ack/product-overview/alb-ingress-controller)[下一篇：BlazingDNS](https://help.aliyun.com/zh/ack/product-overview/blazingdns)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

注意事项

变更记录

非托管版

托管版

CoreDNS是ACK集群和ACK Edge集群中默认采用的DNS服务发现插件，ACK Serverless集群支持选择CoreDNS组件进行服务发现。本文为您介绍CoreDNS组件信息、使用说明和变更记录。

## 组件介绍

CoreDNS是Kubernetes集群中负责DNS解析的组件，能够支持解析集群内部自定义服务域名和集群外部域名。CoreDNS项目由 [CNCF](https://cncf.io/) 托管。关于CoreDNS的更多信息，请参见 [CoreDNS: DNS and Service Discovery](https://coredns.io/)。

CoreDNS目前支持两个版本，非托管版与托管版，详细说明请参见 [服务发现DNS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-discovery-dns-1/#task-2038513 "")。

> 关于CoreDNS版本和集群版本对应关系的更多信息，请参见 [CoreDNS version in Kubernetes](https://github.com/coredns/deployment/blob/master/kubernetes/CoreDNS-k8s_version.md)。

## 注意事项

- 应用Pod中的DNS配置同样会影响DNS结果，请参见 [DNS策略配置和域名解析说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-dns-resolution#task-1985778 "")。

- 升级非托管CoreDNS前，请注意以下事项：

  - 请务必阅读CoreDNS升级的说明。更多信息，请参见 [非托管CoreDNS自动升级](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-ack-to-automatically-update-coredns#task-2093043 "")。

  - 建议备份位于kube-system命名空间下的`coredns` ConfigMap。
- CoreDNS的服务不可用会严重影响集群内的其他服务。

  - CoreDNS非托管版：请参考 [非托管CoreDNS稳定性与高性能部署建议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-coredns-for-high-availability "")，自行保证CoreDNS的可用性。

  - CoreDNS托管版：可用性由ACK保证，请参见 [CoreDNS托管版性能说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/coredns-managed-edition-performance-description "")。

## 变更记录

### **非托管版**

| **版本号** | **适用集群** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **版本号** | **适用集群** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v1.12.1.3 | 适用于1.27及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.12.1.3 | 2025年11月05日 | - 优化：<br>  <br>  - topologySpreadConstraints下增加 [matchLabelKeys](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)，避免组件升级滚动更新后可能出现的CoreDNS Pod集中在单可用区下，不符合预期的情况。更多信息，请参见 [使用调度策略实现CoreDNS高可用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-coredns-for-high-availability#ff8b04098exbi "")。 | 此次升级不会对业务造成影响。 |
| v1.12.1.2 | 适用于1.21及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.12.1.2 | 2025年10月10日 | - 优化：<br>  <br>  - 组件版本号移除`aliyun`后缀。<br>    <br>  - `cache`插件的`serve_stale`默认配置优化为`serve_stale 30s verify`。 | 此次升级不会对业务造成影响。 |
| v1.12.1.1-4035d7a99-aliyun | 适用于1.21及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.12.1.1-4035d7a99-aliyun | 2025年07月22日 | 更新到社区 [v1.12.1 版本](https://github.com/coredns/coredns/releases/tag/v1.12.1)。<br>- 新增了 [multisocket](https://coredns.io/plugins/multisocket/) 插件。<br>  <br>- 将 CNAME 查找限制从7增加到10。<br>  <br>- plugin/kubernetes：修复了因DeletionTimestamp导致的解析到已删除Pod的问题（ [#7119](https://github.com/coredns/coredns/issues/7119)）（ [#7131](https://github.com/coredns/coredns/pull/7131)）。<br>  <br>- plugin/kubernetes：恢复“仅为定义了主机名的端点创建PTR记录 ( [#6898](https://github.com/coredns/coredns/pull/6898) )”。<br>  <br>- plugin/forward：添加了选项 `failfast_all_unhealthy_upstreams` 。当所有上游服务器都关闭时，返回 `servfail`。<br>  <br>- `cache`插件默认开启`serve_stale`配置。当上游DNS Server不可用时，允许使用过期缓存进行应答（本次应答的ttl = 0)，并尝试异步获取域名的最新地址。 | 此次升级不会对业务造成影响。 |
| v1.11.3.5-5321daf49-aliyun | 适用于1.21及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.11.3.5-5321daf49-aliyun | 2025年03月19日 | - 更新base镜像，修正相关安全漏洞。<br>  <br>- 支持灵骏节点池，CoreDNS Pod不会调度到灵骏节点。 | 此次升级不会对业务造成影响。 |
| v1.11.3.2-f57ea7ed6-aliyun | 适用于1.21及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.11.3.2-f57ea7ed6-aliyun | 2024年10月21日 | - CoreDNS新增对 [Firewall](https://github.com/coredns/policy) 插件支持，并且Forward插件支持根据返回码执行下一个插件。<br>  <br>- 支持在控制台的**运维管理** \> **组件管理**页面，自定义配置CoreDNS组件部署的拓扑约束相关选项。 | 此次升级不会对业务造成影响。 |
| v1.9.3.16-4341f22f-aliyun | 仅适用于1.20.4及以上版本的ACK Serverless集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.9.3.16-4341f22f-aliyun | 2023年05月09日 | CoreDNS容器调度时默认申请的内存大小增加至4Gi，避免CoreDNS被调度至共享实例。您可以通过组件配置自定义修改内存大小。 | 升级可能会导致在创建CoreDNS时提升使用的ECI规格。 |
| v1.9.3.10-7dfca203-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.9.3.10-7dfca203-aliyun | 2023年04月03日 | - 优化可用区级的反亲和调度。<br>  <br>- 减小弹性节点场景中Pod被驱逐的可能。 | 由于调度策略调整，当集群所有可调度节点均落在单一可用区时，可能出现CoreDNS副本无法调度、组件升级失败的情况。为保证DNS可用性，建议您进行集群扩容，将可调度节点打散在多个可用区，以保证CoreDNS副本调度运行。 |
| v1.9.3.6-32932850-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.9.3.6-32932850-aliyun | 2022年08月25日 | - 支持K8s Events投递。<br>  <br>- 在ACK Serverless集群中，默认的CPU Request修改为2核。 | 此次升级不会对业务造成影响。 |
| v1.9.3.2-8850b5e7-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.9.3.2-8850b5e7-aliyun | 2022年08月03日 | 支持在日志中心一键开启CoreDNS日志采集功能。 | 此次升级不会对业务造成影响。 |
| v1.9.3.1-5e7ba42d-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.9.3.1-5e7ba42d-aliyun | 2022年07月11日 | - 若干功能特性和问题的修复，详细信息，请参见 [CoreDNS-1.9.3 Release](https://coredns.io/2022/05/27/coredns-1.9.3-release/)。<br>  <br>- 支持ACK One多集群服务。 | 此次升级不会对业务造成影响。 |
| v1.8.4.5-2ce07fd2-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.8.4.5-2ce07fd2-aliyun | 2022年04月08日 | 优化CoreDNS调度亲和性配置，允许集群所有节点为弹性伸缩节点。 | 此次升级不会对业务造成影响。 |
| v1.8.4.3-644f4735-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.8.4.3-644f4735-aliyun | 2022年02月22日 | - 关闭ServError类型的解析结果缓存。<br>  <br>- 按Hostname反亲和调度由preferred改成required，即强制按节点反亲和调度。 | 由于副本按节点强制反亲和调度，当CoreDNS副本数大于节点数时，部分CoreDNS副本会处于Pending，请于升级该版本前扩容集群节点或缩容CoreDNS副本。 |
| v1.8.4.2-7d597cff-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.8.4.2-3a376cc-aliyun | 2022年01月10日 | - 增加自定义参数支持。<br>  <br>- 默认开启解析日志。 | 此次升级不会对业务造成影响。 |
| v1.8.4.1-3a376cc-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.8.4.1-3a376cc-aliyun | 2021年10月26日 | - 支持EndpointSlices资源的监听。<br>  <br>- 支持以IPv6地址进行DNS查询。 | 此次升级不会对业务造成影响。 |
| v1.7.0.0-f59c03d-aliyun | 适用于1.14.8以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.7.0.0-f59c03d-aliyun | 2021年07月08日 | - 修改了CoreDNS默认的优雅退出的时间及CoreDNS Deployment中的容器内存限制。<br>  <br>- 更新指标（Metrics）名称。如果您的监控系统依赖于CoreDNS指标，请注意修改。更多信息，请参见 [Metric Changes](https://coredns.io/2020/06/15/coredns-1.7.0-release/#metric-changes)。<br>  <br>- 修复Forward插件只使用第一个上游DNS服务器的问题。<br>  <br>- 删除了对已弃用插件Upstream的兼容。如果Corefile配置项中包含Upstream插件，Upstream插件会在升级过程中被安全、自动地删除。 | 如果您此前修改过ECS上DNS配置文件 /etc/resolv.conf ，升级或重建CoreDNS Pod会使其采用ECS上修改过的 /etc/resolv.conf，请升级前确保配置中DNS Server均正常工作。 |
| 1.6.7.edge（停止维护） | - | registry.{{.Region}}.aliyuncs.com/acs/coredns:1.6.7.edge | 2021年04月23日 | 基于社区1.6.7版本构建。更多信息，请参见 [CoreDNS-1.6.7 Release](https://coredns.io/2020/01/28/coredns-1.6.7-release/)。 | 此次升级不会对业务造成影响。 |
| v1.7.0 | - | registry.{{.Region}}.aliyuncs.com/acs/coredns:1.7.0 | 2021年03月18日 | - 删除了对已弃用插件Upstream的兼容。如果Corefile配置项中包含Upstream插件，Upstream插件会在升级过程中被安全、自动地删除。<br>  <br>- 更新指标（Metrics）名称。如果您的监控系统依赖于CoreDNS指标，请注意修改。更多信息，请参见 [Metric Changes](https://coredns.io/2020/06/15/coredns-1.7.0-release/#metric-changes)。<br>  <br>- 修复Forward插件只使用第一个上游DNS服务器的问题。 | 如果您此前修改过ECS上DNS配置文件 /etc/resolv.conf ，升级或重建CoreDNS Pod会使其采用ECS上修改过的 /etc/resolv.conf，请升级前确保配置中DNS Server均正常工作。 |
| v1.6.7（停止维护） | - | registry.{{.Region}}.aliyuncs.com/acs/coredns:1.6.7 | 2018年11月28日 | 基于社区1.6.7版本构建。更多信息，请参见 [CoreDNS-1.6.7 Release](https://coredns.io/2020/01/28/coredns-1.6.7-release/)。 | 此次升级不会对业务造成影响。 |

### **托管版**

| **版本号** | **适用集群** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **版本号** | **适用集群** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v1.12.1.2 | 适用于1.21及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.12.1.2 | 2025年10月10日 | - 优化：<br>  <br>  - 更新到社区 [v1.12.1 版本](https://github.com/coredns/coredns/releases/tag/v1.12.1)。<br>    <br>  - 未开启IPv6双栈功能的集群中，查询AAAA类型记录将直接返回`nodata`。<br>    <br>  - 默认 [开启multisocket插件增强性能](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#708c3f86e8e7n "")。 | 此次升级不会对业务造成影响。 |
| v1.11.3.2-f57ea7ed6-aliyun | 适用于1.21及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.11.3.2-f57ea7ed6-aliyun | 2024年10月21日 | - CoreDNS新增对 [Firewall](https://github.com/coredns/policy) 插件支持，并且Forward插件支持根据返回码执行下一个插件。<br>  <br>- 支持在控制台的**运维管理** \> **组件管理**页面，自定义配置CoreDNS组件部署的拓扑约束相关选项。 | 此次升级不会对业务造成影响。 |
| v1.9.3.10-7dfca203-aliyun | 适用于1.20.4及以上版本的集群。 | registry.{{.Region}}.aliyuncs.com/acs/coredns:v1.9.3.10-7dfca203-aliyun | 2023年04月03日 | - 优化可用区级的反亲和调度。<br>  <br>- 减小弹性节点场景中Pod被驱逐的可能。 | 由于调度策略调整，当集群所有可调度节点均落在单一可用区时，可能出现CoreDNS副本无法调度、组件升级失败的情况。为保证DNS可用性，建议您进行集群扩容，将可调度节点打散在多个可用区，以保证CoreDNS副本调度运行。 |