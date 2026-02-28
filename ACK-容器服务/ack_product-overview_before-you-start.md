### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)使用须知及高危风险操作说明

# 使用须知及高危风险操作说明

更新时间：2025-12-22 21:22:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：支持时区](https://help.aliyun.com/zh/ack/product-overview/supported-time-zones)[下一篇：配额与限制](https://help.aliyun.com/zh/ack/product-overview/limits)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

索引

使用须知

数据面组件相关

集群升级相关

Kubernetes原生配置相关

ACK Serverless集群相关

注册集群相关

应用目录相关

高危操作

集群相关高危操作

节点池相关高危操作

网络与负载均衡相关高危操作

存储相关高危操作

日志相关高危操作

相关文档

阿里云容器服务Kubernetes版（简称容器服务ACK）提供容器服务相关的技术架构以及核心组件的托管服务，对于非托管组件以及运行在ACK集群中的应用，不当操作可能会导致业务故障。为了更好地预估和避免相关的操作风险，在使用容器服务ACK前，请认真阅读本文中的建议与注意事项。

## **索引**

| **信息项** | **相关文档** |
| --- | --- |

|     |     |
| --- | --- |
| **信息项** | **相关文档** |
| [使用须知](https://help.aliyun.com/zh/ack/product-overview/before-you-start#section-c7y-7xe-w5u "") | - [数据面组件相关](https://help.aliyun.com/zh/ack/product-overview/before-you-start#136f5dd70f5fj "")<br>  <br>- [集群升级相关](https://help.aliyun.com/zh/ack/product-overview/before-you-start#136fabf20ffwp "")<br>  <br>- [Kubernetes原生配置相关](https://help.aliyun.com/zh/ack/product-overview/before-you-start#3 "")<br>  <br>- [ACK Serverless集群相关](https://help.aliyun.com/zh/ack/product-overview/before-you-start#4 "")<br>  <br>- [注册集群相关](https://help.aliyun.com/zh/ack/product-overview/before-you-start#c783c2c03cgcm "")<br>  <br>- [应用目录相关](https://help.aliyun.com/zh/ack/product-overview/before-you-start#5 "") |
| [高危操作](https://help.aliyun.com/zh/ack/product-overview/before-you-start#section-qyx-kxv-p4v "") | - [集群相关高危操作](https://help.aliyun.com/zh/ack/product-overview/before-you-start#6 "")<br>  <br>- [节点池相关高危操作](https://help.aliyun.com/zh/ack/product-overview/before-you-start#7 "")<br>  <br>- [网络与负载均衡相关高危操作](https://help.aliyun.com/zh/ack/product-overview/before-you-start#13710b880fjly "")<br>  <br>- [存储相关高危操作](https://help.aliyun.com/zh/ack/product-overview/before-you-start#9 "")<br>  <br>- [日志相关高危操作](https://help.aliyun.com/zh/ack/product-overview/before-you-start#10 "") |

## 使用须知

### **数据面组件相关**

数据面组件指运行在客户ECS服务器上的系统组件，例如CoreDNS、Ingress、kube-proxy、terway、kubelet等。由于数据面组件运行在客户ECS服务器上，因此数据面组件运行的稳定性需要阿里云容器服务与客户共同维护。

阿里云容器服务ACK对数据面组件提供以下支持：

- 提供组件的参数化设置管理、定期功能优化、BugFix、CVE补丁等功能，并给出相应的指导文档。

- 提供组件的监控与报警等可观测能力的建设，部分核心组件会提供组件日志，并通过SLS透出给客户。

- 提供配置最佳实践和建议，容器服务将根据集群规模大小给出组件配置建议。

- 提供组件的定期巡检能力和一定的报警通知能力，检查项包括但不限于：组件版本、组件配置、组件负载、组件部署分布拓扑、组件实例数等。


您在使用数据面组件时，请遵循以下建议：

- 使用最新的组件版本。组件经常会发布新版本以修复Bug或提供新特性。您需要在新版本的组件发布后，在保证业务稳定的前提下选择合适的时机，遵循组件升级指导文档中的说明进行升级操作。更多信息，请参见 [组件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/component-overview#task-2094293 "")。

- 请在容器服务ACK的报警中心中设置联系人的邮箱地址、手机号码，并设置相应的报警信息接收方式，阿里云将通过这些渠道推送容器服务的报警信息、产品公告等。更多信息，请参见 [容器服务报警管理](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/alert-management#task-2056339 "") 和 [如何设置消息接收？](https://help.aliyun.com/zh/account/support/message-received-management-settings#topic-2149123 "")。

- 在您收到组件稳定性风险报告后，请及时按照相关指引进行处理，消除安全隐患。

- 当您在使用数据面组件时，请通过[容器服务控制台](https://cs.console.aliyun.com/)集群管理页面**运维管理** \> **组件管理**的方式或者OpenAPI的方式配置组件的自定义参数。通过其他渠道修改组件配置可能会导致组件功能异常。更多信息，请参见 [管理组件](https://help.aliyun.com/zh/ack/manage-system-components#task-z3j-tvk-2gb "")。

- 请勿直接使用IaaS层产品的OpenAPI来变更组件的运行环境，包括但不限于使用ECS的OpenAPI更改ECS运行状态、修改Worker节点的安全组配置、更改Worker节点的网络配置以及通过负载均衡的OpenAPI修改SLB配置等，擅自改动IaaS层资源可能会导致数据面组件异常。

- 部分数据面组件受上游社区版组件影响，可能存在Bug或漏洞，请注意及时升级组件，以避免开源组件Bug或漏洞导致您的业务受损。


### **集群升级相关**

请务必通过容器服务ACK的集群升级功能升级集群的K8s版本，自行升级K8s版本可能导致ACK集群的稳定性和兼容性问题。详细操作，请参见 [升级集群和独立升级集群控制面和节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster#task-1664343 "")。

阿里云容器服务ACK对集群升级提供以下支持：

- 提供集群K8s新版本的升级功能。

- 提供K8s新版本升级的前置检查功能，确保集群当前状态支持升级。

- 提供K8s新版本的版本说明文档，包括相较于前版本的变化。

- 提示升级到K8s新版本时因资源变化可能会发生的风险。


您在使用集群升级功能时，请遵循以下建议：

- 在集群升级前运行前置检查，并根据前置检查结果逐一修复集群升级的阻塞点。

- 详细阅读K8s新版本的版本说明文档，并根据ACK所提示的升级风险确认集群和业务的状态，自行判断升级风险。详细信息，请参见 [Kubernetes版本发布概览](https://help.aliyun.com/zh/ack/overview-of-kubernetes-versions-supported-by-ack#task-1960241 "")。

- 由于集群升级不提供回滚功能，请做好充分的升级计划和预后备份。

- 根据容器服务ACK的版本支持机制，在当前版本的支持周期内及时升级集群K8s版本。更多信息，请参见 [版本说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/support-for-kubernetes-versions/#concept-186482 "")。


### Kubernetes原生配置相关

- 请勿擅自修改Kubernetes的关键配置，例如以下文件的路径、链接和内容：

  - /var/lib/kubelet

  - /var/lib/docker

  - /etc/kubernetes

  - /etc/kubeadm

  - /var/lib/containerd
- 在YAML模板中请勿使用Kubernetes集群预留的Annotation，否则会造成资源不可用、申请失败、异常等问题。以`kubernetes.io/`和`k8s.io/`开头的标签为核心组件预留标签。违规示例：`pv.kubernetes.io/bind-completed: "yes"`。


### ACK Serverless集群相关

在以下场景中，ACK Serverless集群不提供赔付：

- 为简化集群运维，ACK Serverless集群提供部分系统组件托管能力，并在集群的组件开启托管后，负责其部署和维护。由于您误删托管组件依赖的K8s对象资源等其他情况导致业务受损时，ACK Serverless不提供赔付。

- 针对 [阿里云容器服务Kubernetes版服务等级协议](https://terms.aliyun.com/legal-agreement/terms/suit_bu1_ali_cloud/suit_bu1_ali_cloud202010221416_90184.html) 下“ **除外情形**”中列举的情况和原因，ACK Serverless不提供赔付。


### 注册集群相关

- 通过[容器服务管理控制台](https://cs.console.aliyun.com/)的注册集群功能接入外部Kubernetes集群时，请确保外部集群与阿里云之间的网络稳定性。

- 容器服务ACK提供外部Kubernetes集群的注册接入，但无法管控外部集群自身的稳定性以及不当操作。因此当您通过注册集群配置外部集群节点的Label、Annotation、Tag等信息时，可能导致应用运行异常，请谨慎操作。


### 应用目录相关

为了丰富Kubernetes应用，容器服务ACK的应用市场提供了应用目录，它们是基于开源软件做了适配和二次开发的应用。ACK无法管控开源软件本身产生的缺陷，请知晓此风险。更多信息，请参见 [应用市场](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/app-marketplace#task-dby-n5y-ne0 "")。

## 高危操作

在使用容器服务ACK过程中相关功能模块存在高危操作，可能会对业务稳定性造成较大影响。在使用前请认真了解以下高危操作及其影响。

### 集群相关高危操作

| **分类** | **高危操作** | **影响** | **恢复方案** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **分类** | **高危操作** | **影响** | **恢复方案** |
| API Server | 复用API Server所使用的CLB于其他场景，例如使用LoadBalancer类型Service复用该CLB。 | 导致集群不可用，影响业务流量。 | 恢复原有配置，或请求售后服务支持。 |
| 修改API Server所使用的CLB的监听、服务器组、ACL等控制CLB转发的配置、CLB标签配置。 | 导致集群异常。 | 恢复原有配置。 |
| 删除API Server所使用的CLB。 | 导致集群不可操作。 | 不可恢复，请重新创建集群。重建集群请参见 [创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/#task-skz-qwk-qfb "")。 |
| Worker节点 | 修改集群内节点安全组。 | 可能导致节点不可用。 | 将节点重新添加到集群自动创建的节点安全组中，请参见 [为实例（主网卡）关联安全组](https://help.aliyun.com/zh/ecs/user-guide/manage-ecs-instances-in-security-groups#concept-jhw-31n-xdb "")。 |
| 节点到期或被销毁。 | 该节点不可用。 | 不可恢复。 |
| 重装操作系统。 | 节点上组件被删除。 | 节点移出再加入集群。相关操作请参见 [移除节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/remove-a-node#task-tqk-v54-dgb "")、 [添加已有节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-existing-ecs-instances-to-an-ack-cluster#task-2548777 "")。 |
| 自行升级节点组件版本。 | 可能导致节点无法使用。 | 回退到原始版本。 |
| 更改节点IP。 | 节点不可用。 | 改回原IP。 |
| 自行修改核心组件（kubelet、docker、containerd 等）参数。 | 可能导致节点不可用。 | 按照官网推荐配置参数。 |
| 修改操作系统配置。 | 可能导致节点不可用。 | 尝试还原配置项或删除节点重新购买。 |
| 修改节点时间。 | 可能导致节点上组件工作异常。 | 还原节点时间。 |
| 通过不受 ACK 支持的方式向集群中添加节点算力资源。 | ACK 提供控制台、OpenAPI、CLI等方式向集群中增加节点算力资源，请参见 [添加已有节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-existing-ecs-instances-to-an-ack-cluster "")。如果您通过其他方式向集群中添加了节点，ACK无法识别此类节点的来源，无法提供节点生命周期管理、自动化运维和技术支持等产品能力。详细风险说明，请参见 [为什么控制台显示节点所属节点池的来源为“其他节点”？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-node-management#22f153a210s4u "")。 | 建议通过节点池的方式纳管算力资源。如需继续使用，请自行确保节点与集群各组件（如 Kubernetes组件、网络、存储、安全组件等）的兼容性。 |
| Master节点（ACK专有版集群） | 修改集群内节点安全组。 | 可能导致Master节点不可用。 | 将节点重新添加到集群自动创建的节点安全组中，请参见 [为实例（主网卡）关联安全组](https://help.aliyun.com/zh/ecs/user-guide/manage-ecs-instances-in-security-groups#concept-jhw-31n-xdb "")。 |
| 节点到期或被销毁。 | 该Master节点不可用。 | 不可恢复。 |
| 重装操作系统。 | Master节点上组件被删除。 | 不可恢复。 |
| 自行升级Master或者etcd组件版本。 | 可能导致集群无法使用。 | 回退到原始版本。 |
| 删除或格式化节点/etc/kubernetes等核心目录数据。 | 该Master节点不可用。 | 不可恢复。 |
| 更改节点IP。 | 该Master节点不可用。 | 改回原IP。 |
| 自行修改核心组件（etcd、kube-apiserver、docker等）参数。 | 可能导致Master节点不可用。 | 按照官网推荐配置参数。 |
| 自行更换Master或etcd 证书 | 可能导致集群无法使用。 | 不可恢复。 |
| 自行增加或减少Master节点。 | 可能导致集群无法使用。 | 不可恢复。 |
| 修改节点时间。 | 可能导致节点上组件工作异常。 | 还原节点时间。 |
| 其他 | 通过RAM执行权限变更或修改操作。 | 集群部分资源如负载均衡可能无法创建成功。 | 恢复原先权限。 |
| **说明**<br>仅适用于1.26以下版本的集群。<br>修改或删除集群内预置的PodSecurityPolicy相关资源（包括名称为 `ack.privileged`的PodSecurityPolicy资源，名称以 `ack:podsecuritypolicy:`开头的ClusterRole、ClusterRoleBinding、Role和RoleBinding资源）。 | 可能导致集群核心组件异常、可能导致无法在集群内创建和更新Pod资源。 | 恢复相关资源。具体操作，详见 [配置或恢复ACK默认的Pod安全策略](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/use-pod-security-policies#section-sc9-zs4-6nz "")。 |

### 节点池相关高危操作

| **高危操作** | **影响** | **恢复方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **高危操作** | **影响** | **恢复方案** |
| 删除伸缩组。 | 导致节点池异常。 | 不可恢复，只能重建节点池。重建节点池请参见 [创建节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#section-eq0-lmv-4a7 "")。 |
| 通过kubectl移除节点。 | 节点池节点数显示和实际不符。 | 通过容器服务管理控制台或者节点池相关API移除指定节点（参见 [移除节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/remove-a-node#task-tqk-v54-dgb "")）或者修改节点池的期望节点数进行缩容（参见 [创建和管理节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#section-a2i-luy-mnw "")）。 |
| 直接释放ECS实例。 | 可能导致节点池详情页面显示异常。开启期望节点数的节点池为维持期望节点数，将会根据相应节点池配置自动扩容到期望节点数。 | 不可恢复。正确做法是通过容器服务管理控制台或者节点池相关API修改节点池的期望节点数进行缩容（参见 [创建和管理节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#section-a2i-luy-mnw "")）或移除指定节点（参见 [移除节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/remove-a-node#task-tqk-v54-dgb "")）。 |
| 对开启自动伸缩的节点池进行手动扩容或缩容。 | 自动伸缩组件会根据策略自动调整节点数，导致结果与期望不符。 | 不可恢复。自动伸缩节点池无需手动干预。 |
| 修改ESS伸缩组的最大或最小实例数。 | 可能导致扩缩容异常。 | - 对于未开启自动伸缩组的节点池，ESS伸缩组最大和最小实例数改为默认值2000和0。<br>  <br>- 对于开启自动伸缩的节点池，将ESS伸缩组最大和最小实例数修改为与节点池最大和最小节点数一致。 |
| 添加已有节点前不进行数据备份。 | 添加前实例上的数据丢失。 | 不可恢复。<br>- 手动添加已有节点前必须对要保留的所有数据进行提前备份。<br>  <br>- 自动添加节点时会执行系统盘替换操作，需要您提前备份保存在系统盘中的有用数据。 |
| 在节点系统盘中保存重要数据。 | 节点池的自愈操作可能通过重置节点配置的方式修复节点，因此可能导致系统盘数据丢失。 | 不可恢复。正确做法是将重要数据存放于额外的数据盘或者云盘、NAS、OSS。 |

### **网络与负载均衡相关高危操作**

| **高危操作** | **影响** | **恢复方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **高危操作** | **影响** | **恢复方案** |
| 修改内核参数`net.ipv4.ip_forward=0`。 | 网络不通。 | 修改内核参数为`net.ipv4.ip_forward=1`。 |
| 修改内核参数：<br>- `net.ipv4.conf.all.rp_filter = 1|2`<br>  <br>- `net.ipv4.conf.[ethX].rp_filter = 1|2`<br>  <br>  <br>  <br>  **说明**<br>  <br>  <br>  <br>  <br>  <br>  `ethX`代表所有以`eth`开头的网卡。 | 网络不通。 | 修改内核参数为：<br>- `net.ipv4.conf.all.rp_filter = 0`<br>  <br>- `net.ipv4.conf.[ethX].rp_filter = 0` |
| 修改内核参数`net.ipv4.tcp_tw_reuse = 1`。 | 导致Pod健康检查异常。 | 修改内核参数为`net.ipv4.tcp_tw_reuse = 0`。 |
| 修改内核参数`net.ipv4.tcp_tw_recycle = 1`。 | 导致NAT异常。 | 修改内核参数`net.ipv4.tcp_tw_recycle = 0`。 |
| 修改内核参数`net.ipv4.ip_local_port_range`。 | 导致网络偶发不通。 | 修改内核参数到默认值`net.ipv4.ip_local_port_range="32768 60999"`。 |
| 安装防火墙软件，例如Firewalld或者ufw等。 | 导致容器网络不通。 | 卸载防火墙软件并重启节点。 |
| 节点安全组配置未放通容器 CIDR的53端口UDP。 | 集群内DNS无法正常工作。 | 按照官网推荐配置放通安全组。 |
| 修改或者删除ACK添加的SLB的标签。 | 导致SLB异常。 | 恢复SLB的标签。 |
| 通过负载均衡控制台修改ACK管理的SLB的配置，包括SLB、监听及虚拟服务器组。 | 导致SLB异常。 | 恢复SLB的配置。 |
| 移除Service中复用已有SLB的Annotation，即`service.beta.kubernetes.io/alibaba-cloud-loadbalancer-id: ${YOUR_LB_ID}`。 | 导致SLB异常。 | 在Service中添加复用已有SLB的Annotation。<br>**说明**<br>复用已有SLB的Service无法直接修改为使用自动创建SLB的Service。您需要重新创建Service。 |
| 通过负载均衡控制台删除ACK创建的SLB。 | 可能导致集群网络异常。 | 通过删除Service的方式删除SLB。删除Service请参见 [删除Service](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-management/#step-trr-3n3-2uy "")。 |
| 在安装Nginx Ingress Controller组件的情况下手动删除 kube-system命名空间下的`nginx-ingress-lb` Service。 | Ingress Controller工作不正常，严重时产生崩溃。 | 使用以下YAML新建一个同名Service。<br>```yaml<br>apiVersion: v1<br>kind: Service<br>metadata:<br>  annotations:<br>  labels:<br>    app: nginx-ingress-lb<br>  name: nginx-ingress-lb<br>  namespace: kube-system<br>spec:<br>  externalTrafficPolicy: Local<br>  ports:<br>  - name: http<br>    port: 80<br>    protocol: TCP<br>    targetPort: 80<br>  - name: https<br>    port: 443<br>    protocol: TCP<br>    targetPort: 443<br>  selector:<br>    app: ingress-nginx<br>  type: LoadBalancer<br>``` |
| 新增或修改ECS节点上DNS配置文件/etc/resolv.conf中`nameserver`选项。 | 若配置的DNS服务器配置不合理，可能导致DNS无法解析，影响集群正常运行。 | 您如果想要使用自建DNS服务器作为上游服务器，建议在CoreDNS侧进行配置。具体操作，请参见 [非托管CoreDNS配置说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-coredns#task-2165721 "")。 |
| 修改、删除ACK创建的弹性网卡、灵骏弹性网卡。 | Pod网络中断。 | 不可恢复。 |
| 修改、删除网络相关 CRD。<br>```plaintext<br>podnetworkings.network.alibabacloud.com<br>podenis.network.alibabacloud.com<br>networkinterfaces.network.alibabacloud.com<br>nodes.network.alibabacloud.com<br>noderuntimes.network.alibabacloud.com<br>*.cilium.io<br>*.crd.projectcalico.org<br>``` | Terway 组件将无法工作，严重时可能导致网络中断、Pod异常。 | 不可恢复。 |
| 创建、修改、删除网络相关系统CR。<br>```plaintext<br>podenis.network.alibabacloud.com<br>networkinterfaces.network.alibabacloud.com<br>nodes.network.alibabacloud.com<br>noderuntimes.network.alibabacloud.com<br>*.cilium.io<br>*.crd.projectcalico.org<br>``` | Terway 组件将无法工作，严重时可能导致网络中断、Pod异常。 | 删除自定义CR定义，并重建关联的Pod。 |
| 修改、删除Terway网络配置中非允许修改的字段。配置参数声明 [自定义Terway配置参数](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/terway-configuration-parameters "")。 | Terway 组件将无法工作，严重时可能导致网络中断、Pod异常。 | 恢复原有配置，并重启节点。 |

### 存储相关高危操作

| **高危操作** | **影响** | **恢复方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **高危操作** | **影响** | **恢复方案** |
| 控制台手动解挂云盘。 | Pod写入报IO Error。 | 重启Pod，手动清理节点挂载残留。 |
| 节点上umount磁盘挂载路径 | Pod写入本地磁盘。 | 重启Pod。 |
| 节点上直接操作云盘。 | Pod写入本地磁盘。 | 不可恢复。 |
| 多个Pod挂载相同云盘。 | Pod写入本地磁盘或者报错IO Error。 | 确保一个云盘给一个Pod使用。<br>**重要**<br>云盘为阿里云存储团队提供的非共享存储，只能同时被一个Pod挂载。 |
| 手动删除NAS挂载目录。 | Pod写入报IO Error。 | 重启Pod。 |
| 删除正在使用的NAS盘或挂载点。 | Pod出现IO Hang。 | 重启ECS节点。重启具体操作，请参见 [重启ECS实例](https://help.aliyun.com/zh/ecs/user-guide/restart-instances#concept-yxw-dwm-xdb "")。 |

### 日志相关高危操作

| **高危操作** | **影响** | **恢复方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **高危操作** | **影响** | **恢复方案** |
| 删除宿主机/tmp/ccs-log-collector/pos目录。 | 日志重复采集。 | 不可恢复。该目录下的文件记录了日志的采集位置。 |
| 删除宿主机/tmp/ccs-log-collector/buffer目录。 | 日志丢失。 | 不可恢复。该目录是待消费的日志缓存文件。 |
| 删除aliyunlogconfig CRD资源。 | 日志采集失效。 | 重新创建删除的CRD以及对应的资源，但失效期间日志无法恢复。<br>删除CRD会关联删除对应所有的实例，即使恢复CRD后还需要手动创建被删除的实例。 |
| 删除日志组件。 | 日志采集失效。 | 重新安装日志组件并手动恢复aliyunlogconfig CRD实例，删除期间日志无法恢复。<br>删除日志组件相当于删除aliyunlogconfig CRD以及日志采集器Logtail，期间日志采集能力全部丢失。 |

## 相关文档

- [Nginx Ingress Controller使用建议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-the-nginx-ingress-controller#task-2175597 "")

- [DNS最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#task-2548861 "")