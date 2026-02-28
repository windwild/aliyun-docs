### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/)[服务发现DNS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-discovery-dns-1/)DNS最佳实践

# DNS最佳实践

更新时间：2025-12-25 07:05:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DNS解析及缓存策略说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-resolution-policies-and-caching-policies)[下一篇：DNS解析异常问题排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-troubleshooting-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

本文目录

优化域名解析请求

了解容器中的DNS配置

避免IPVS缺陷导致的DNS概率性解析超时问题

使用NodeLocal DNSCache

使用合适的CoreDNS版本

监控CoreDNS运行状态

监控指标

运行日志

Kubernetes事件投递

保证CoreDNS高可用性

评估CoreDNS组件压力

调整CoreDNS Pod数量

调整CoreDNS Pod规格

调度CoreDNS Pod

优化CoreDNS配置

关闭kube-dns服务的亲和性配置

关闭Autopath插件

配置CoreDNS优雅退出

配置Forward插件与上游VPC DNS服务器的默认协议

配置Ready就绪探针插件

配置multisocket插件，增强CoreDNS解析性能

相关文档

DNS是Kubernetes集群中至关重要的基础服务之一，在客户端设置不合理、集群规模较大等情况下DNS容易出现解析超时、解析失败等现象。本文介绍Kubernetes集群中DNS的最佳实践，帮助您避免此类问题。

## **注意事项**

本文不适用于CoreDNS托管版和启用智能托管模式的ACK集群。CoreDNS托管版会按照负载自动执行弹性伸缩，无需您自行调整。

## 本文目录

DNS最佳实践包含客户端和服务端的内容：

- 在客户端，您可以通过优化域名解析请求降低解析延迟，通过使用合适的容器镜像、合适的节点操作系统 、节点DNS缓存NodeLocal DNSCache等方式来减少解析异常。

  - [优化域名解析请求](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-zzx-vw7-tu5 "")

  - [了解容器中的DNS配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-v08-zav-kf6 "")

  - [避免IPVS缺陷导致的DNS概率性解析超时问题](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-h6t-66g-7fo "")

  - [使用NodeLocal DNSCache](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-emg-1v6-a91 "")

  - [使用合适的CoreDNS版本](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-jvf-pe7-hce "")
- 在CoreDNS服务端，您可以通过监控CoreDNS运行状态识别DNS异常，快速定位异常根因，通过合理调整集群CoreDNS部署状态来提升集群CoreDNS高可用和QPS吞吐量。

  - [监控CoreDNS运行状态](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-4mf-aem-6z9 "")

    - [监控指标](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#c71f2390240ka "")

    - [运行日志](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#567a46a0226bb "")

    - [Kubernetes事件投递](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#p-yv9-fo4-8tg "")
  - [保证CoreDNS高可用性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-dua-rjx-ia7 "")

    - [评估CoreDNS组件压力](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#e22092cdcfxs6 "")

    - [调整CoreDNS Pod数量](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#767c9063b02vn "")

    - [调整CoreDNS Pod规格](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#e490dd69ceuli "")

    - [调度CoreDNS Pod](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#9629b906cddcx "")
  - [优化CoreDNS配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-7at-thy-66d "")

    - [关闭kube-dns服务的亲和性配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#17b0bfd02478a "")

    - [关闭Autopath插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#6235d0e022ucj "")

    - [配置CoreDNS优雅退出](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#76b5c570221es "")

    - [配置Forward插件与上游VPC DNS服务器的默认协议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#29c283410edkw "")

    - [配置Ready就绪探针插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#p-66k-kor-itx "")

有关CoreDNS的更多信息，请参见 [CoreDNS官方文档](https://coredns.io/)。

## 优化域名解析请求

DNS域名解析请求是Kubernetes最高频的网络行为之一，其中很多请求是可以优化和避免的。您可以通过以下方式优化域名解析请求：

- （推荐）使用连接池：当一个容器应用需要频繁请求另一服务时，推荐使用连接池。连接池可以将请求上游服务的链接缓存在内存中，避免每次访问时域名解析和TCP连接的开销。

- 使用异步或者长轮询模式来获取 DNS 域名对应的IP。

- 使用DNS缓存：

  - （推荐）当您的应用无法改造成通过连接池连接另一服务时，可以考虑在应用侧缓存DNS解析结果，具体操作，请参见 [使用NodeLocal DNSCache](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-emg-1v6-a91 "")。

  - 如果无法使用NodeLocal DNSCache，可以在容器内置NSCD（Name Service Cache Daemon）缓存。关于如何使用NSCD缓存，请参见 [在Kubernetes集群中使用NSCD](https://developer.aliyun.com/article/845769)。
- 优化resolv.conf文件：由于resolv.conf文件中ndots和search两个参数的机制作用，容器内配置域名的不同写法决定了域名解析的效率，关于ndots和search两个参数的机制详情，请参见 [DNS策略配置和域名解析说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-dns-resolution#task-1985778 "")。

- 优化域名配置：当容器内应用需要访问某域名时，该域名按以下原则配置，可以最大程度减少域名解析尝试次数，从而减少域名解析耗时。

  - Pod访问同命名空间的Service，优先使用`<service-name>`访问，其中`service-name`代指Service名称。

  - Pod跨命名空间访问Service，优先使用`<service-name>.<namespace-name>`访问，其中`namespace-name`代指Service所处的命名空间。

  - Pod访问集群外部域名时，优先使用FQDN类型域名访问，这类域名通过常见域名最后加半角句号（.）的方式来指定地址，可以避免`search`搜索域拼接带来的多次无效搜索，例如，访问www.aliyun.com时，优先使用FQDN类型域名www.aliyun.com.来访问。

    - 版本为1.33或更高的集群中，search域可配置为单个"."（相关Issue: [125883](https://github.com/kubernetes/kubernetes/issues/125883)），达到类似效果：















      ```yaml
      dnsPolicy: None
      dnsConfig:
        nameservers: ["192.168.0.10"]  ## 192.168.0.10 地址为coredns service clusterIP，实际环境需要对应修改
        searches:
  - .
  - default.svc.cluster.local  ## 注意：其中default需要修改为对应的namespace name
  - svc.cluster.local
  - cluster.local
```

使用上方配置后，Pod中的/etc/resolv.conf如下：

```plaintext
search . default.svc.cluster.local svc.cluster.local cluster.local
nameserver 192.168.0.10
```

可以看到"."为第一个搜索域，这样域名请求总是会认为请求解析的目标域名为FQDN，优先尝试解析自身，不再做无效search。

**重要**

请注意上述配置需要指定`dnsPolicy`为`None`才能达到效果。

**完整工作负载示例**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
labels:
    app: nginx
name: nginx
namespace: default
spec:
progressDeadlineSeconds: 600
replicas: 3
revisionHistoryLimit: 10
selector:
    matchLabels:
      app: nginx
strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - image: registry.openanolis.cn/openanolis/nginx:1.14.1-8.6
        imagePullPolicy: Always
        name: nginx
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: None
      dnsConfig:
        nameservers: ["192.168.0.10"]  ## 192.168.0.10 地址为coredns service clusterIP，实际环境需要对应修改
        searches:
        - .
        - default.svc.cluster.local
        - svc.cluster.local
        - cluster.local
      hostname: nginx
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      subdomain: subdomain
      terminationGracePeriodSeconds: 30
```

## 了解容器中的DNS配置

- 不同的DNS resolver 解析器会因为实现的差异有细微差别。可能会遇到dig <域名>解析正常，ping <域名>失败的情况。

- 不建议使用Alpine基础镜像，Alpine容器镜像内置的musl libc库与标准glibc的实现存在一些差异，会导致包括但不限于以下问题。您可尝试使用其他基础镜像，如Debian、CentOS等。


  - 3.18及更早版本的Alpine不支持tc回退到TCP协议。

  - 3.3及更早版本Alpine不支持search参数，不支持搜索域，无法完成服务发现。

  - 并发请求/etc/resolv.conf中配置的多个DNS服务器，导致NodeLocal DNSCache优化失效。

  - 并发使用同一Socket请求A和AAAA记录，在旧版本内核上触发Conntrack源端口冲突导致丢包问题。


关于以上问题的更多信息，请参见 [musl libc](https://wiki.musl-libc.org/functional-differences-from-glibc.html#Name_Resolver_.2F_DNS)。

- 如果是GO语言应用，请了解CGO和Pure GO不同实现下的DNS Resolver的差异。


## 避免IPVS缺陷导致的DNS概率性解析超时问题

当集群使用IPVS作为kube-proxy负载均衡模式时，您可能会在CoreDNS缩容或重启时遇到DNS概率性解析超时的问题。该问题由社区Linux内核缺陷导致，具体信息，请参见 [IPVS](https://github.com/torvalds/linux/commit/35dfb013149f74c2be1ff9c78f14e6a3cd1539d1)。

您可以通过以下任意方式降低IPVS缺陷的影响：

- 使用节点DNS缓存NodeLocal DNSCache，具体操作，请参见 [使用NodeLocal DNSCache](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#section-emg-1v6-a91 "")。

- 修改kube-proxy中IPVS UDP会话保持的超时时间，具体操作，请参见 [如何修改kube-proxy中IPVS UDP会话保持的超时时间？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-vkv-808-6wc "")。


## 使用NodeLocal DNSCache

在部分情况下，CoreDNS可能会出现下列问题：

- 小概率情况下，可能会遭遇A和AAAA并发查询导致的丢包，进而导致的DNS解析失败问题。

- 节点conntrack表满导致丢包，导致DNS解析失败。


为了提高集群DNS服务的稳定性和性能，我们推荐您安装NodeLocal DNSCache组件，它通过在集群节点上运行DNS缓存提高集群DNS性能。关于更多NodeLocal DNSCache的介绍及如何在ACK集群中部署NodeLocal DNSCache的具体步骤，请参见 [使用NodeLocal DNSCache组件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-nodelocal-dnscache#task-2008363 "")。

**重要**

安装NodeLocal DNSCache后，需将DNS缓存配置注入Pod中。执行下方的命令可以为指定namespace配置标签，在此namespace中新建的Pod会自动注入DNS缓存配置。更多注入方式请参见上方的文档。

```bash
kubectl label namespace default node-local-dns-injection=enabled
```

## 使用合适的CoreDNS版本

CoreDNS对Kubernetes版本实现了较好的向后兼容，建议您保持CoreDNS版本为较新的稳定版本。ACK组件管理中心提供了CoreDNS的安装、升级、配置能力，您可以关注组件管理中组件状态，若CoreDNS组件显示可升级，请尽快选择业务低峰期进行升级。

- 关于升级的具体操作，请参见 [非托管CoreDNS自动升级](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-ack-to-automatically-update-coredns#task-2093043 "")。

- 关于CoreDNS版本的发布记录，请参见 [CoreDNS](https://help.aliyun.com/zh/ack/product-overview/coredns#concept-2071838 "")。


CoreDNS v1.7.0以下的版本存在风险隐患，包括但不限于以下：

- CoreDNS与APIServer连通性异常（例如APIServer重启、APIServer迁移、网络抖动）时，CoreDNS会因错误日志写入失败导致容器重启。更多信息，请参见 [Set klog's logtostderr flag](https://github.com/coredns/coredns/pull/2529)。

- 启动CoreDNS时会占用额外内存，默认采用的Memory Limit在较大规模集群下可能触发OOM（OutOfMemory）问题，严重时可能导致CoreDNS Pod反复重启无法自动恢复。更多信息，请参见 [CoreDNS uses a lot memory during initialization phase](https://github.com/coredns/coredns/issues/2511)。

- CoreDNS存在若干可能影响Headless Service域名、集群外部域名解析的问题。更多信息，请参见 [plugin/kubernetes: handle tombstones in default processor](https://github.com/coredns/coredns/pull/3890) 和 [Data is not synced when CoreDNS reconnects to kubernetes api server after protracted disconnection](https://github.com/coredns/coredns/issues/3879)。

- 在集群节点异常情况下，部分旧版本CoreDNS默认采用的容忍策略，可能会导致CoreDNS Pod部署在异常节点上，且CoreDNS Pod无法被自动驱逐，继而导致域名解析异常。


不同版本的Kubernetes集群，推荐的CoreDNS最低版本有所区别。如下表：

| 集群版本 | 推荐的最低CoreDNS版本 |
| --- | --- |

|     |     |
| --- | --- |
| 集群版本 | 推荐的最低CoreDNS版本 |
| 1.14.8以下 | v1.6.2（停止维护） |
| 1.14.8及以上，1.20.4以下 | v1.7.0.0-f59c03d-aliyun |
| 1.20.4及以上，1.21.0以下 | v1.8.4.1-3a376cc-aliyun |
| 1.21.0及以上 | v1.11.3.2-f57ea7ed6-aliyun |

## 监控CoreDNS运行状态

### **监控指标**

CoreDNS通过标准的Prometheus接口暴露出解析结果等健康指标，发现CoreDNS服务端甚至上游DNS服务器的异常。

阿里云Prometheus监控默认内置了CoreDNS相关的指标监控和告警规则，您可以在[容器服务管理控制台](https://cs.console.aliyun.com/)开启Prometheus及仪表盘功能。具体操作，请参见 [CoreDNS组件监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/coredns-monitoring#task-2283377 "")。

若您是自建Prometheus监控Kubernetes集群，可以在Prometheus观测相关指标，并对重点指标设置告警。具体操作，请参见 [CoreDNS Prometheus官方文档](https://coredns.io/plugins/metrics/)。

### **运行日志**

在DNS异常发生的情况下，CoreDNS日志有助于您快速诊断异常根因。建议您开启CoreDNS域名解析日志和其SLS日志采集，具体操作，请参见 [分析和监控CoreDNS日志](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/collect-and-analyze-coredns-logs#task-2074495 "")。

### Kubernetes事件投递

在v1.9.3.6-32932850-aliyun及以上版本的CoreDNS中，您可以开启k8s\_event插件以将CoreDNS关键日志以Kubernetes事件的形式投递到事件中心。关于k8s\_event插件，请参见 [k8s\_event](https://github.com/coredns/coredns.io/blob/master/content/explugins/k8s_event.md)。

全新部署的CoreDNS会默认开启该功能。如果您是从低版本CoreDNS升级到v1.9.3.6-32932850-aliyun及以上版本的，您需要手动修改配置文件以开启该功能。

1. 执行如下命令，打开CoreDNS配置文件。

















   ```bash
   kubectl -n kube-system edit configmap/coredns
   ```

2. 新增kubeAPI和k8s\_event插件。

















   ```yaml
   apiVersion: v1
   data:
     Corefile: |
       .:53 {
           errors
           health {
               lameduck 15s
           }

           // 新增开始（请忽略其他差异）。
           kubeapi
           k8s_event {
             level info error warning // 将info、error、warning状态关键日志投递。
           }
           // 新增结束。

           kubernetes cluster.local in-addr.arpa ip6.arpa {
               pods verified
               fallthrough in-addr.arpa ip6.arpa
           }
           // 下方略。
       }
   ```

3. 检查CoreDNS Pod运行状态和运行日志，运行日志中出现`reload`字样后说明修改成功。


## 保证CoreDNS高可用性

CoreDNS是集群中的权威DNS，CoreDNS的失效会导致集群内访问Service失败，可能会造成大范围的业务不可用。您可通过下列措施保证CoreDNS的高可用性：

### **评估CoreDNS组件压力**

您可在集群中执行DNS压力测试评估组件压力。包括 [DNSPerf](https://github.com/DNS-OARC/dnsperf) 在内的许多开源工具可以帮助您完成此目标。如果您无法准确评估集群DNS压力，您可参照下方的推荐标准。

- 建议您在任何情况下设置CoreDNS Pod数应至少为2，单个Pod的资源limit不小于1核1G。

- CoreDNS所能提供的域名解析QPS与CPU消耗成正相关，使用NodeLocal DNSCache的情况下，每CPU核可以支撑10000+ QPS的域名解析请求。不同类型的业务对域名请求的QPS需求存在较大差异，您可以观察每个CoreDNS Pod的峰值CPU使用量，如果其在业务峰值期间占用CPU大于一核，建议您对CoreDNS进行副本扩容。无法确定峰值CPU使用量时，可以保守地采用Pod数和集群节点数1：8的比值来部署，即每扩容8个集群节点，增加一个CoreDNS Pod。


### **调整CoreDNS Pod数量**

CoreDNS拥有的Pod数量直接决定了CoreDNS能够使用的计算资源，您可根据评估的结果调整CoreDNS所属Pod数量。

**重要**

由于UDP报文缺少重传机制，当集群节点存在IPVS UDP缺陷导致的丢包风险时，CoreDNS Pod的缩容或重启可能会导致长达五分钟的整个集群域名解析超时或异常。关于IPVS缺陷导致解析异常的解决方案，请参见 [DNS解析异常问题排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-troubleshooting-1#section-84d-fqg-tym "")。

- 根据建议策略自动调整

  您可部署下方的`dns-autoscaler`，它会参照前方提到的推荐策略（Pod数和集群节点数1：8）实时自动调整CoreDNS的Pod数量。其中Pod数量的计算公式为replicas = max (ceil (cores × 1/coresPerReplica), ceil (nodes × 1/nodesPerReplica) )，且受到`max`、`min`限制。



  **dns-autoscaler**




















  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: dns-autoscaler
    namespace: kube-system
    labels:
      k8s-app: dns-autoscaler
  spec:
    selector:
      matchLabels:
        k8s-app: dns-autoscaler
    template:
      metadata:
        labels:
          k8s-app: dns-autoscaler
      spec:
        serviceAccountName: admin
        containers:
      - name: autoscaler
        image: registry.cn-hangzhou.aliyuncs.com/acs/cluster-proportional-autoscaler:1.8.4
        resources:
          requests:
            cpu: "200m"
            memory: "150Mi"
        command:
        - /cluster-proportional-autoscaler
        - --namespace=kube-system
        - --configmap=dns-autoscaler
        - --nodelabels=type!=virtual-kubelet
        - --target=Deployment/coredns
        - --default-params={"linear":{"coresPerReplica":64,"nodesPerReplica":8,"min":2,"max":100,"preventSinglePointFailure":true}}
        - --logtostderr=true
        - --v=9
```

- 手动调整

您可通过下方的命令手动调整CoreDNS所属的Pod数量。















```bash
kubectl scale --replicas={target} deployment/coredns -n kube-system # target替换为目标Pod数量
```

- 请勿使用工作负载自动伸缩

虽然工作负载自动伸缩，例如容器水平伸缩（HPA）、容器定时水平伸缩（CronHPA）等也可以自动调整Pod数量，但是它们会频繁执行扩缩容。由于前文所说的Pod缩容时导致的解析异常，请勿使用工作负载自动伸缩控制CoreDNS Pod数量。


### **调整CoreDNS Pod规格**

另一种调整CoreDNS资源的方式是调整Pod规格。在ACK托管集群Pro版中，CoreDNS Pod默认的内存限制为`2Gi`，CPU则未限制。推荐您将CPU Limit设置为4096m, 最小应不低于1024m。您可通过控制台对CoreDNS Pod配置进行调整。

**通过控制台修改CoreDNS配置**

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

3. 单击 **网络** 页签，找到 **CoreDNS** 卡片。单击卡片上的 **配置**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5326861471/p919974.png)

4. 修改CoreDNS配置，然后单击 **确认**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5326861471/p920399.png)


### **调度CoreDNS Pod**

**重要**

错误的调度配置可能会导致CoreDNS Pod无法部署，导致CoreDNS失效。在执行此操作前，请您确保您已经非常了解 [调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/scheduling-overview/ "") 相关知识。

建议您在部署CoreDNS Pod时，将其部署在不同可用区、不同集群节点上，避免单节点、单可用区故障。版本低于v1.8.4.3的CoreDNS组件默认配置了按节点的弱反亲和性，可能会因为节点资源不足导致部分或全部Pod部署在同一节点上，如果遇到这种情况，请删除Pod触发调度进行调整，或者升级组件版本到最新。CoreDNS 组件版本v1.8 以下版本不再维护，请尽快升级。

CoreDNS所运行的集群节点应避免CPU、内存用满的情况，否则会影响域名解析的QPS和响应延迟。当集群节点条件允许时，可以考虑使用自定义参数将CoreDNS调度至独立的集群节点上，以提供稳定的域名解析服务。

**使用自定义参数完成CoreDNS独占节点部署**

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏单击 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点**。

3. 在 **节点** 页面，单击 **标签与污点管理**。

4. 在 **标签与污点管理** 页面，选中目标节点，单击 **添加标签**。



**说明**





节点数应大于CoreDNS副本数，避免单个节点上运行多个CoreDNS副本。

5. 在 **添加** 对话框中，设置以下参数，然后单击 **确定**。

   - **名称**：node-role-type

   - **值**：coredns
6. 在集群管理页左侧导航栏中，选择**运维管理** \> **组件管理**，然后搜索 **CoreDNS**。

7. 单击 **CoreDNS** 卡片的 **配置**，在 **配置** 对话框，单击 **NodeSelector** 右侧的 **＋添加**，设置以下参数，然后单击 **确认**。


   - **Key**：node-role-type

   - **Value**：coredns


CoreDNS会重新调度至指定标签的节点上。

## 优化CoreDNS配置

容器服务ACK仅提供CoreDNS的默认配置，您应关注配置中的各个参数，优化其配置，以使CoreDNS可以为您的业务容器正常提供DNS服务。CoreDNS的配置非常灵活，具体操作，请参见 [DNS策略配置和域名解析说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-dns-resolution#task-1985778 "") 与 [CoreDNS官方文档](https://coredns.io/plugins/)。

早期版本随Kubernetes集群部署的CoreDNS默认配置可能存在一些风险，推荐您按以下方式检查和优化：

- [关闭kube-dns服务的亲和性配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#17b0bfd02478a "")

- [关闭Autopath插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#6235d0e022ucj "")

- [配置CoreDNS优雅退出](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#76b5c570221es "")

- [配置Forward插件与上游VPC DNS服务器的默认协议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#29c283410edkw "")

- [配置Ready就绪探针插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practice#p-66k-kor-itx "")


您也可以通过容器智能运维中定时巡检和故障诊断功能完成CoreDNS配置文件的检查。当容器智能运维检查结果中提示CoreDNS ConfigMap配置异常时，请逐个检查以上项目。

**说明**

CoreDNS刷新配置过程中，可能会占用额外内存。修改CoreDNS配置项后，请观察Pod运行状态，如果出现Pod内存不足的情况，请及时修改CoreDNS Deployment中容器内存限制，建议将内存调整至2 GB。

### **关闭kube-dns服务的亲和性配置**

亲和性配置可能导致CoreDNS不同副本间存在较大负载差异，建议按以下步骤关闭：

控制台操作方式

命令行方式

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**网络** \> **服务**。

3. 在kube-system命名空间下，单击服务 **kube-dns** 右侧的 **YAML编辑**。

   - 如果发现sessionAffinity字段为`None`，则无需进行以下步骤。

   - 如果发现sessionAffinity为`ClientIP`，则进行以下步骤。
4. 删除sessionAffinity、sessionAffinityConfig及所有子键，然后单击 **更新**。















```yaml
# 删除以下所有内容。
sessionAffinity: ClientIP
sessionAffinityConfig:
     clientIP:
       timeoutSeconds: 10800
```

5. 再次单击服务 **kube-dns** 右侧的 **YAML编辑**，校验sessionAffinity字段是否为`None`，为`None`则Kube-DNS服务变更成功。


1. 执行以下命令查看kube-dns服务配置信息。















```bash
kubectl -n kube-system get svc kube-dns -o yaml
```



   - 如果发现sessionAffinity字段为`None`，则无需执行以下步骤。

   - 如果发现sessionAffinity为`ClientIP`，则执行以下步骤。
2. 执行以下命令打开并编辑名为kube-dns的服务。















```bash
kubectl -n kube-system edit service kube-dns
```

3. 删除sessionAffinity相关设置（sessionAffinity、sessionAffinityConfig及所有子键），并保存退出。















```yaml
# 删除以下所有内容。
sessionAffinity: ClientIP
sessionAffinityConfig:
     clientIP:
       timeoutSeconds: 10800
```

4. 修改完成后，再次运行以下命令查看sessionAffinity字段是否为`None`，为`None`则Kube-DNS服务变更成功。















```bash
kubectl -n kube-system get svc kube-dns -o yaml
```


### **关闭Autopath插件**

部分早期版本的CoreDNS开启了Autopath插件，该插件在一些极端场景下会导致解析结果出错，请确认其是否处于开启状态，并编辑配置文件将其关闭。更多信息，请参见 [Autopath](https://github.com/coredns/coredns/issues/3765)。

**说明**

关闭Autopath插件后，客户端发起的域名解析请求QPS最高会增加3倍，解析单个域名耗时最高增加3倍，请关注CoreDNS负载和业务影响。

1. 执行`kubectl -n kube-system edit configmap coredns`命令，打开CoreDNS配置文件。

2. 删除`autopath @kubernetes`一行后保存退出。

3. 检查CoreDNS Pod运行状态和运行日志，运行日志中出现`reload`字样后说明修改成功。


### **配置CoreDNS优雅退出**

`lameduck`是 CoreDNS 中的一种机制，用于实现优雅退出（Graceful Shutdown）。它可在CoreDNS需要停止或重启时，确保正在处理的请求能够正常完成，而不会突然中断。`lameduck`的工作原理如下：

- 当CoreDNS进程将要终止时，它会进入 Lameduck 模式。

- 在`lameduck`模式下，CoreDNS会停止接收新的请求，但会继续处理已经接收到的请求，直到请求全部完成或超过`lameduck`超时时间。


控制台操作方式

命令行操作方式

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**配置管理** \> **配置项**。

3. 在kube-system命名空间下，单击配置项coredns右侧的 **YAML编辑**。

4. 参考下列的CoreDNS配置文件，保证health插件开启，并调整lameduck超时时间为`15s`，然后单击 **确定**。


```yaml
.:53 {
        errors
        # health插件在不同的CoreDNS版本中可能有不同的设置情形。
        # 情形一：默认未启用health插件。
        # 情形二：默认启用health插件，但未设置lameduck时间。
        # health
        # 情形三：默认启用health插件，设置了lameduck时间为5s。
        # health {
        #     lameduck 5s
        # }
        # 对于以上三种情形，应统一修改成以下，调整lameduck参数为15s。
        health {
            lameduck 15s
        }
        # 其它插件不需要修改，此处省略。
    }
```

如果CoreDNS Pod正常运行则说明CoreDNS优雅退出的配置更新成功。如果CoreDNS Pod出现异常，可以通过查看Pod事件及日志定位原因。

1. 执行以下命令打开CoreDNS配置文件。


```bash
kubectl -n kube-system edit configmap/coredns
```

3. 参考下列的Corefile文件，保证`health`插件开启，并调整lameduck参数为`15s`。


```yaml
.:53 {
        errors
        # health插件在不同的CoreDNS版本中可能有不同的设置情形。
        # 情形一：默认未启用health插件。
        # 情形二：默认启用health插件，但未设置lameduck时间。
        # health
        # 情形三：默认启用health插件，设置了lameduck时间为5s。
        # health {
        #     lameduck 5s
        # }
        # 对于以上三种情形，应统一修改成以下，调整lameduck参数为15s。
        health {
            lameduck 15s
        }
        # 其它插件不需要修改，此处省略。
    }
```

5. 修改CoreDNS配置文件后保存退出。

6. 如果CoreDNS正常运行则说明CoreDNS优雅退出的配置更新成功。如果CoreDNS Pod出现异常，可以通过查看Pod事件及日志定位原因。


### **配置Forward插件与上游VPC DNS服务器的默认协议**

NodeLocal DNSCache采用TCP协议与CoreDNS进行通信，CoreDNS会根据请求来源使用的协议与上游DNS服务器进行通信。因此默认情况下，来自业务容器的集群外部域名解析请求会依次经过NodeLocal DNSCache、CoreDNS，最终以TCP协议请求VPC内DNS服务器，即ECS上默认配置的100.100.2.136和100.100.2.138两个 IP。

VPC内DNS服务器对TCP协议支持有限，如果您使用了NodeLocal DNSCache，您需要修改CoreDNS配置，让其总是优先采用UDP协议与上游DNS服务器进行通信，避免解析异常。建议您使用以下方式修改CoreDNS配置文件，即修改命名空间kube-system下名为coredns的ConfigMap。具体操作，请参见 [管理配置项](https://help.aliyun.com/zh/ack/serverless-kubernetes/user-guide/manage-configmaps-1693818316836 "")。在`forward`插件中指定请求上游的协议为`prefer_udp`，修改之后CoreDNS会优先使用UDP协议与上游通信。修改方式如下所示：

```yaml
# 修改前
forward . /etc/resolv.conf
# 修改后
forward . /etc/resolv.conf {
  prefer_udp
}
```

### 配置Ready就绪探针插件

大于1.5.0版本的CoreDNS必须配置ready插件以启用就绪探针。

1. 执行如下命令，打开CoreDNS配置文件。

















```bash
kubectl -n kube-system edit configmap/coredns
```

2. 检查是否包含`ready`一行，若无，则增加`ready`一行，按Esc键、输入`:wq!`并按Enter键，保存修改后的配置文件并退出编辑模式。

















```yaml
apiVersion: v1
data:
    Corefile: |
     .:53 {
       errors
       health {
         lameduck 15s
       }
       ready # 如果没有这一行，请增加本行，注意缩进与Kubernetes保持一致。
       kubernetes cluster.local in-addr.arpa ip6.arpa {
         pods verified
         fallthrough in-addr.arpa ip6.arpa
       }
       prometheus :9153
       forward . /etc/resolv.conf {
         max_concurrent 1000
               prefer_udp
       }
       cache 30
       loop
       log
       reload
       loadbalance
     }
```

3. 检查CoreDNS Pod运行状态和运行日志，运行日志中出现`reload`字样后说明修改成功。


### 配置multisocket插件，增强CoreDNS解析性能

CoreDNS在v1.12.1版本新增了multisocket插件，启用此插件可使CoreDNS使用多个Socket同时监听同个端口，以增强在使用大量CPU场景中的CoreDNS性能。插件的详细介绍可以查看 [社区文档](https://coredns.io/plugins/multisocket/)。

您需要通过`coredns` ConfigMap启用multisocket：

```yaml
.:53 {
        ...
        prometheus :9153
        multisocket [NUM_SOCKETS]
        forward . /etc/resolv.conf
        ...
}
```

`NUM_SOCKETS`决定了监听同个端口的Socket数量。

配置建议：将 `NUM_SOCKETS` 与估计的CPU使用率、CPU资源限制及集群可用资源对齐，例如：

- 如果CoreDNS在高峰时消耗4核，且可用资源为8核，则将`NUM_SOCKETS`设置为 2。

- 如果CoreDNS在高峰时消耗8核，且可用资源为64核，则将`NUM_SOCKETS`设置为 8。


为了确定最佳配置，建议您使用不同的配置并测试QPS与负载。

如果不指定`NUM_SOCKETS` ，默认使用`GOMAXPROCS`，即与CoreDNS Pod的CPU限制相等。如果Pod CPU限制未设置，则与Pod所在节点CPU核数相等。

## 相关文档

- [服务发现DNS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/service-discovery-dns-1/#task-2038513 "")

- [DNS策略配置和域名解析说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-dns-resolution#task-1985778 "")

- [使用NodeLocal DNSCache组件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-nodelocal-dnscache#task-2008363 "")