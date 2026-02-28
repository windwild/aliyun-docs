### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/) [ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/) [操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/) [网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/) 容器网络插件Terway与Flannel对比

# 容器网络插件Terway与Flannel对比

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/)[下一篇：ACK托管集群网络规划](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-cluster-network-planning)

该文章对您有帮助吗？

反馈

容器服务 Kubernetes 版支持两种容器网络插件：Terway与Flannel。本文主要对比了两种容器网络插件的功能及适用场景。

- Terway是阿里云自研的网络插件，通过ENI实现Pod的网络通信，提供了基于eBPF的网络加速、NetworkPolicy和Pod级别交换机/安全组等能力，适用于对节点规模、网络性能和安全等有较高需求的高性能计算、游戏、微服务等场景。

- Flannel是社区开源的网络插件，在ACK中采用了阿里云VPC专有网络模式，报文经过VPC路由表直接转发，适用于节点规模较小、需要简化网络配置、无需对容器网络进行自定义控制的场景。


**重要**

- 容器网络插件需要在创建集群时进行安装，且集群创建后不支持更改。

- 使用Flannel时，ALB Ingress仅支持将请求转发到NodePort与LoadBalancer类型的Service，不支持ClusterIP类型。


|     |     |     |
| --- | --- | --- |
| **对比项** | **Terway** | **Flannel** |
| 网络性能 | ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3555721571/CAEQURiBgIDRlbSMpBkiIGExZGY4NjA1ODBlMDRiMGY5YTI0NjMxYTQ5MzBjMGJh4881926_20250120094106.935.svg)<br>- Terway在TCP RR、UDP PPS、Bandwidth带宽、Latency延迟这四个方面的性能都领先于社区版Flannel。<br>  <br>  <br>  <br>  <br>  <br>  <br>  <br>  **说明** <br>  <br>  测试数据为基于ecs.ebmg5s.24xlarge实例的理论值，实际数据以您的操作环境为准。更多详细内容，请参见[阿里巴巴云原生社区](https://developer.aliyun.com/article/755848?spm=5176.26934562.main.8.5eb06560zyOukC)。<br>  <br>- Terway支持独占ENI模式：Pod独占ENI，拥有极高的网络性能，适用于高性能计算、游戏、微服务等场景。<br>  <br>- Terway支持共享ENI DataPath V2加速模式：DataPath V2是IPVLAN方案的升级版，Pod访问集群内的端点时支持通过eBPF绕过节点网络协议栈，加速网络访问。<br>  <br>**说明** <br>在DataPath V2模式下，容器网络的连接跟踪（conntrack）信息通过eBPF map进行存储。与Linux系统原生的conntrack机制类似，eBPF conntrack基于LRU（最近最少使用）算法实现，当map容量达到上限时，会自动淘汰最旧的连接记录以存储新连接，您需要根据实际业务规模合理配置相关参数，以防连接数超出限制。请参考 [优化Terway模式下conntrack配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/optimize-conntrack-configuration-in-terway-mode "")。 |
| 节点配额 | 使用Terway时节点数量上限依赖于单集群容量限制。<br>- ACK托管集群Pro版：默认支持5,000个节点，最大支持15,000个节点。<br>  <br>- ACK托管集群基础版：10个节点。 | 使用Flannel时节点数量上限依赖于VPC路由表条目数和单集群容量限制。<br>VPC路由表条目数：默认支持200个条目，申请配额后最大支持1000个条目。集群中一个节点对应一个条目，即最大支持1000个节点。<br>- ACK托管集群Pro版：默认支持200个节点，最大支持1,000个节点。<br>  <br>- ACK托管集群基础版：10个节点。 |
| 节点Pod数量 | Pod使用节点ENI，单节点Pod数量由节点的规格和指标数据（ **ENI数量**、**单网卡私有IPv4地址数**）决定。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4914167371/p904636.png)<br>以上图一个 **计算型c7**、ecs.c7.4xlarge、16 vCPU 32 GiB规格的ECS实例为例：<br>- 多IP模式（共享ENI）下最多容纳210个Pod。<br>  <br>- 独占模式下最多容纳7个Pod。<br>  <br>虽然 **计算型c6** 与 **计算型c7** 实例拥有相同的ENI数量，但是单网卡私有IPv4地址数指标上的差别使得 **计算型c6** 在多IP模式下最多能容纳140个Pod。关于详细的计算方法，请参见 [节点Pod限额计算方法](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#99aa011b071mr "")。 | 单节点Pod数量依赖于配置 **容器网段** 时设置的 **节点Pod数量** 和子网掩码位。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4914167371/p904543.png)<br>以上图为例，在ACK托管集群Pro版当前Pod网络CIDR（172.16.0.0/20）配置下，每个节点最多容纳256个Pod，集群内最多可允许部署16个节点。<br>**重要** <br>Flannel创建成功后不能修改最大节点数量。 |
| 容器网段 | - 容器网段从VPC网段中分配，因此对VPC的地址消耗较高，建议在使用前规划充足的VPC网段。<br>  <br>- 容器网段（VPC网段）、Service网段互相独立，不能重合，网段无法修改。<br>  <br>- 支持通过新增虚拟交换机（vSwitch）的方式对容器网段进行扩容。 | - 容器网段独立于VPC网段。Flannel会为集群中的每个节点从已配置的容器网段中分配一个子网网段subnet，节点内所有Pod的IP地址都将从subnet中分配。<br>  <br>- 容器网段、节点网段（VPC网段）、Service网段互相独立，不能重合，网段无法修改。<br>  <br>- 不支持容器网段扩容。 |
| 网络安全 | - 支持为Pod配置独立的虚拟交换机与安全组。<br>  <br>- 支持Kubernetes原生网络策略NetworkPolicy，可以自定义容器间的访问控制。 | - 不支持为Pod配置独立的虚拟交换机与安全组。<br>  <br>- 不支持NetworkPolicy。 |
| IPv4/IPv6双栈 | 支持双栈。 | 不支持双栈。<br>**说明** <br>ACK使用的是经过修改以适配阿里云云上环境的Flannel插件，并不与开源社区保持完全同步。ACK Flannel的更新记录，请参见 [Flannel](https://help.aliyun.com/zh/ack/product-overview/flannel "")。 |
| 固定Pod IP | 支持为Pod配置固定IP。 | 不支持为Pod配置固定IP。 |
| 会话保持 | 负载均衡后端直接对接Pod，依托会话保持能力，可以实现在后端Pod发生变化时服务无中断。 | 负载均衡后端使用NodePort连接Pod，在Pod发生变化时，流量会中断，可能导致业务上的重试。 |
| 多集群互访 | 多个集群的Pod之间只要设置安全组开放端口就可以互相通信。 | 无法支持。 |
| Pod源IP保留 | Pod访问VPC内其他端点，所使用的源IP都是Pod IP，便于审计。 | Pod访问VPC内其他端点，所使用的源IP是节点IP，Pod IP无法保留。 |

## **后续步骤**

- 在创建集群后，为Pod、Service、节点分配的网段无法修改。网段的大小决定这三种资源的数量上限，可能会对您的业务部署产生影响。规划不同的网段可以实现资源在网络逻辑上的隔离，以便于您实现访问控制、定制化路由等操作。因此推荐您在创建集群前完成网段规划，详细内容请参见 [ACK托管集群网络规划](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-cluster-network-planning "")。

- 完成网段规划后：

  - 如果您计划使用Terway，请参见 [使用Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway "") 在创建集群时安装Terway。

  - 如果您计划使用Flannel，请参见 [使用Flannel网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-flannel "") 在创建集群时安装Flannel。

## **相关文档**

- 关于集群内节点数量的限制与配额提升方式，请参见 [配额与限制](https://help.aliyun.com/zh/ack/product-overview/limits "")。

- 关于在使用容器网络时遇到的常见问题，请参见 [容器网络FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks "")。