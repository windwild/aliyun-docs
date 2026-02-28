### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-cluster-overview/)[集群最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-cluster/)集群高可用架构推荐配置

# ACK集群高可用架构推荐配置

更新时间：2025-12-24 00:42:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：删除集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/delete-a-cluster-1)[下一篇：大规模集群使用建议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/suggestions-on-how-to-work-with-large-ack-pro-clusters)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

本文使用指引

集群示例架构

控制面架构高可用

节点池和虚拟节点高可用配置

节点池高可用配置

虚拟节点高可用配置

工作负载高可用配置

配置拓扑分布约束

配置Pod反亲和

配置Pod Disruption Budget

配置Pod健康检测与自愈

负载均衡高可用配置

指定CLB实例的主备可用区

启用拓扑感知提示 (Topology Aware Hints)

组件推荐配置

合理部署Nginx Ingress Controller

合理部署CoreDNS

相关文档

高可用性（High Availability，HA）旨在优化系统设计，提升服务的可靠性和持续性。容器服务 Kubernetes 版基于Kubernetes架构提供了多种集群高可用保障机制，确保集群控制面、节点与节点池、工作负载、负载均衡等维度的高可用，以构建稳定、安全、可靠的集群和应用架构。

## **本文使用指引**

本文主要面向容器服务 Kubernetes 版的集群开发和管理人员，提供规划和构建高可用集群的通用性建议。实际情况仍以您的集群环境和业务需求为准。本文主要提供了关于集群控制面和集群数据面的相关高可用推荐配置。

| **文档架构** | **维护角色** | **适用的集群类型** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **文档架构** | **维护角色** | **适用的集群类型** |
| [控制面架构高可用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#3fd55002f0q5j "") | 由ACK托管。 | 仅面向托管类的部分ACK集群，包括ACK托管集群（Pro版、基础版）、ACK Serverless集群（Pro版、基础版）、ACK Edge集群、ACK灵骏集群。其他集群类型，例如ACK专有集群、注册集群等，控制面由您自行维护，均不适用。但您可参见本章节获取配置建议。 |
| [节点池和虚拟节点高可用配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#RbHWV "") | 由您维护。 | 通用。 |
| [工作负载高可用配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#uaVtM "") |
| [负载均衡高可用配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#0d1f8a9d0cx66 "") |
| [组件推荐配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#47d8a5d5d9r1x "") |

## **集群示例架构**

ACK集群主要由控制面和普通节点或虚拟节点两部分构成。

- 集群控制面：负责集群管理和协调，例如调度工作负载、维护集群状态等。以ACK托管集群为例，ACK托管集群采用Kubernetes on Kubernetes架构来托管您集群的控制面组件，例如Kube API Server、etcd、Kube Scheduler等。

- 普通节点或虚拟节点：ACK集群支持普通节点（ECS节点）和虚拟节点。节点负责执行实际的工作负载和提供运行容器所需的资源。


ACK集群默认提供了多可用区（Availability Zone，AZ）的高可用集群部署架构。以ACK托管集群为例，集群架构示例如下。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6117019071/p770284.png)

## **控制面架构高可用**

针对托管类的部分ACK集群，包括ACK托管集群（Pro版、基础版）、ACK Serverless集群（Pro版、基础版）、ACK Edge集群、ACK灵骏集群，其控制面及控制面相关组件（例如kube-apiserver、etcd、kube-scheduler等）由ACK进行托管。

- 多可用区的地域：所有托管组件均严格采用多副本、多AZ均衡打散部署策略，确保在单个可用区或节点发生故障时，集群仍然能够正常提供服务。

- 单可用区地域：所有托管组件均严格采用多副本、多节点打散部署策略，确保在单个节点发生故障时，集群仍然能够正常提供服务。


其中，etcd至少为3副本，Kube API Server至少为2副本。所有Kube API Server副本均通过挂载ENI与集群VPC实现网络互通，节点侧kubelet和Kube Proxy通过API Server CLB或者ENI连接Kube API Server。

ACK核心托管组件均可以根据实际的资源使用情况（例如CPU、内存使用量等）进行弹性伸缩，以动态满足API Server的资源使用需求，提供稳定的SLA保障。关于容器服务 Kubernetes 版的SLA协议，请参见 [阿里云容器服务Kubernetes版服务等级协议说明](https://help.aliyun.com/zh/ack/support/ack-service-level-agreement "")。

* * *

除集群控制面默认采用的多可用区的高可用架构外，您也可以进一步配置集群数据面的高可用架构，包括 [节点池和虚拟节点高可用配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#RbHWV "")、 [工作负载高可用配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#uaVtM "")、 [负载均衡高可用配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#0d1f8a9d0cx66 "")、 [组件推荐配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-high-availability-architecture-recommend-configuration#47d8a5d5d9r1x "")。

## **节点池和虚拟节点高可用配置**

ACK集群支持普通节点（ECS节点）和虚拟节点。您可以通过节点池来纳管节点，对节点进行分组管理，包括升级、扩缩容、日常运维等操作。如果您的业务流量相对稳定，或波峰波谷相对稳定，您可以使用ECS节点；如果您的业务有不易提前预测的瞬时波峰，您可以使用虚拟节点，应对突发流量，降低计算成本。更多信息，请参见 [节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-overview/ "")、 [托管节点池概述](https://help.aliyun.com/zh/ack/overview-of-managed-node-pools "")、 [虚拟节点](https://help.aliyun.com/zh/ack/ack-on-eci "")。

### **节点池高可用配置**

您可以基于节点的弹性伸缩、部署集、多AZ，结合K8s调度的拓扑分布约束，确保服务在不同的故障域（failure-domain）资源充足且有所隔离，从而当某一故障域出现问题时，服务仍然可以保持运行，减少单点故障的风险，提高系统的整体可靠性和可用性。

#### **配置节点弹性伸缩**

每个节点池背后是一个弹性伸缩组（ESS），支持在负载调度层或集群资源层对节点进行手动扩缩容与自动化弹性伸缩，以更低成本、更灵活地调整弹性计算资源。关于ACK提供的弹性伸缩方案，请参见 [弹性伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-scaling-overview/ "")、 [启用节点自动伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-scaling-of-nodes "")。

#### **启用部署集**

部署集是控制ECS实例分布的策略，该策略将ECS实例分散部署在不同的物理服务器上，避免由于一台物理机失效导致多台ECS实例宕机。通过为节点池指定部署集，能够保证节点池扩容出的ECS实例不会分布于同一物理机上，并通过亲和性配置，使您的应用对底层的节点拓扑进行感知，使其均匀地分布在不同节点上，保证应用的容灾能力和高可用性。关于如何启用部署集功能，请参见 [节点池部署集最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-associating-deployment-sets-with-node-pools "")。

#### **配置多AZ分布**

ACK支持多AZ节点池。在节点池的创建和运行过程中，推荐您为节点池选择多个不同AZ的vSwitch，并在配置 **扩缩容策略** 时选择 **均衡分布策略**，允许在伸缩组指定的多可用区（即指定多个专有网络交换机）之间均匀分配ECS实例。如果由于库存不足等原因导致可用区之间资源不平衡，您可以再进行均衡操作来平衡资源的可用区分布。关于如何配置自动伸缩策略，请参见 [启用节点自动伸缩](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/auto-scaling-of-nodes#section-3bg-2ko-inl "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5117019071/p768848.png)

#### **启用拓扑分布约束**

基于节点的弹性伸缩、部署集、多AZ分布等手段，结合K8s调度中的拓扑分布约束（ [Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)），可以实现不同级别的故障域隔离能力。ACK节点池上所有节点会自动添加拓扑相关的label，例如`kubernetes.io/hostname`、`topology.kubernetes.io/zone`、`topology.kubernetes.io/region`等。您可以使用拓扑分布约束来控制Pod在不同故障域之间的分布，提升对底层基础设施故障的容忍能力。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4394556671/CAEQTRiBgIC_86D4hhkiIGZmNDhlZDY0YjkwNjQ4NmFhZjgxZmNhYjQwYWE4NzY24210557_20240222135626.153.svg)

关于如何在ACK集群中使用拓扑感知调度能力，例如使Pod在多个拓扑域中重试或将Pod调度到属于同一低延时部署集的ECS中，请参见 [拓扑感知调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/topology-aware-scheduling "")。

### **虚拟节点高可用配置**

您可以借助ACK虚拟节点将Pod快速地调度到弹性容器实例ECI上运行。使用ECI时，您无需购买和管理底层ECS服务器，可以更加关注容器应用而非底层基础设施的维护工作。您可按需创建ECI，仅为容器配置的资源付费（按量按秒计费）。

但为应对突发流量而进行业务的快速水平扩容，或者启动大量实例进行Job任务处理时，可能会遇到可用区对应的规格实例库存不足或者指定的交换机IP耗尽等情况，从而导致ECI实例创建失败。ACK Serverless集群的多可用区特性可以提高ECI实例的创建成功率。

您可以配置虚拟节点的ECI Profile，指定跨不同AZ的vSwitch，实现跨多AZ应用部署。

- ECI会把创建Pod的请求分散到所有的vSwitch中，从而达到分散压力的效果。

- 如果创建Pod的请求在某一个vSwitch中无库存，会自动切换到下一个vSwitch继续尝试创建。


您执行以下命令，按需修改 **kube-system/eci-profile configmap** 中的`vSwitchIds`字段，追加vSwitch ID，多个vSwitch ID之间采用英文半角逗号（,）分隔。修改后即时生效。更多信息，请参见 [创建多可用区的ECI Pod](https://help.aliyun.com/zh/ack/create-ecis-across-zones "")。

```bash
kubectl -n kube-system edit cm eci-profile
```

```yaml
apiVersion: v1
data:
  kube-proxy: "true"
  privatezone: "true"
  quota-cpu: "192000"
  quota-memory: 640Ti
  quota-pods: "4000"
  regionId: cn-hangzhou
  resourcegroup: ""
  securitygroupId: sg-xxx
  vpcId: vpc-xxx
  vSwitchIds: vsw-xxx,vsw-yyy,vsw-zzz
kind: ConfigMap
```

## **工作负载高可用配置**

工作负载的高可用能够保障在故障发生时，应用Pod能够正常运行，或迅速恢复。您可以通过配置拓扑分布约束（Topology Spread Constraints）、Pod反亲和（PodAntiAffinity）、Pod Disruption Budget（PDB）、Pod健康检测与自愈等来实现应用Pod的高可用。

### **配置拓扑分布约束**

拓扑分布约束（ [Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)）是一种在Kubernetes集群中管理Pod分布的功能。它可以确保Pod在不同的节点和可用区之间均匀分布，以提高应用程序的高可用性和稳定性。该技术适用于Deployment、StatefulSet、DaemonSet、Job、CronJob等工作负载类型。

您可以设置`maxSkew.topologyKey`等配置来控制Pod的分布，以确保Pod在集群中按照期望的拓扑分布进行部署，例如指定工作负载在不同的可用区之间均匀分布，以提高可靠性和可用性。示例如下。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-run-per-zone
spec:
  replicas: 3
  selector:
    matchLabels:
      app: app-run-per-zone
  template:
    metadata:
      labels:
        app: app-run-per-zone
    spec:
      containers:
        - name: app-container
          image: app-image
      topologySpreadConstraints:
        - maxSkew: 1
          topologyKey: "topology.kubernetes.io/zone"
          whenUnsatisfiable: DoNotSchedule
          labelSelector:
            matchLabels:
              app: app-run-per-zone
```

### **配置Pod反亲和**

Pod反亲和（PodAntiAffinity）是Kubernetes中的一种调度策略，用于在调度Pod时确保它们不会被调度到同一个节点上，以提高应用程序的高可用性和故障隔离能力。示例如下。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-run-per-node
spec:
  replicas: 3
  selector:
    matchLabels:
      app: app-run-per-node
  template:
    metadata:
      labels:
        app: app-run-per-node
    spec:
      containers:
        - name: app-container
          image: app-image
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            - labelSelector:
                matchExpressions:
                  - key: app
                    operator: In
                    values:
                      - app-run-per-node
              topologyKey: "kubernetes.io/hostname"
```

基于拓扑分布约束，您也可实现在每个节点上最多只运行1个Pod的效果。当指定`topologyKey: "kubernetes.io/hostname"`时，相当于将每个节点作为一个拓扑域。

下方示例创建了一个拓扑分布约束，其中`maxSkew`设置为`1`，`topologyKey`设置为`"kubernetes.io/hostname"`，`whenUnsatisfiable`设置为`DoNotSchedule`，表明允许同一拓扑域（节点）中的 Pod 数量比其他域最多多1个，以实现强制Pod按节点高可用打散的效果。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app-container
          image: my-app-image
      topologySpreadConstraints:
        - maxSkew: 1
          topologyKey: "kubernetes.io/hostname"
          whenUnsatisfiable: DoNotSchedule
          labelSelector:
            matchLabels:
              app: my-app
```

### **配置Pod Disruption Budget**

您可以使用 [Pod Disruption Budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)（PDB）进一步提高应用的可用性。PDB允许定义一个最小可用副本数，当节点处于维护或故障状态时，集群将确保至少有指定数量的副本保持运行。PDB可以防止过多的副本同时终止，尤其适合多副本处理流量型的场景。示例如下。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-with-pdb
spec:
  replicas: 3
  selector:
    matchLabels:
      app: app-with-pdb
  template:
    metadata:
      labels:
        app: app-with-pdb
    spec:
      containers:
        - name: app-container
          image: app-container-image
          ports:
            - containerPort: 80
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: pdb-for-app
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: app-with-pdb
```

### **配置Pod健康检测与自愈**

在ACK集群中，您可以配置不同类型的探针来监测和管理容器的状态和可用性，包括存活探针（Liveness Probes）、就绪探针（Readiness Probes）、启动探针（Startup Probes）。您可以通过在Pod配置中添加相应的探针和重启策略来进行配置。示例如下。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-with-probe
spec:
  containers:
    - name: app-container
      image: app-image
      livenessProbe:
        httpGet:
          path: /health
          port: 80
        initialDelaySeconds: 10
        periodSeconds: 5
      readinessProbe:
        tcpSocket:
          port: 8080
        initialDelaySeconds: 15
        periodSeconds: 10
      startupProbe:
        exec:
          command:
            - cat
            - /tmp/ready
        initialDelaySeconds: 20
        periodSeconds: 15
  restartPolicy: Always
```

## **负载均衡高可用配置**

在集群中实现负载均衡的高可用对于提高服务的稳定性、响应速度、故障隔离性等至关重要。您可以指定负载均衡实例的主备可用区、启用拓扑感知提示（Topology Aware Hints）等手段来实现。

### **指定CLB实例的主备可用区**

传统型负载均衡CLB已在大部分地域部署了多可用区，以实现同地域下的跨机房容灾。您可以通过Service Annotation来指定CLB实例的主备可用区，使得主备可用区与节点池中ECS可用区保持一致，减少跨可用区数据转发，提升网络访问性能。关于CLB支持的地域和可用区，请参见 [CLB支持的地域信息](https://help.aliyun.com/zh/slb/classic-load-balancer/product-overview/regions-that-support-clb "")；关于如何指定CLB实例的主备可用区，请参见 [创建负载均衡时，指定主备可用区](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-annotations-to-the-yaml-file-of-a-service-to-configure-clb-instances#7e1ff7a06cj1y "")。

示例如下。

```yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/alibaba-cloud-loadbalancer-master-zoneid: "cn-hangzhou-b"
    service.beta.kubernetes.io/alibaba-cloud-loadbalancer-slave-zoneid: "cn-hangzhou-i"
  name: nginx
  namespace: default
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  type: LoadBalancer
```

### 启用拓扑感知提示 (Topology Aware Hints)

为了减少跨可用区网络流量，提升网络性能，Kubernetes 1.23引入拓扑感知路由（Topology Aware Routing，也可以称为拓扑感知提示，Topology Aware Hints）特性，实现了拓扑感知的就近路由功能。

您可以在Service中启用该功能。启用后，当可用区（Zone）内有足够的端点（Endpoint）可用时，EndpointSlice控制器会根据在EndpointSlice上的拓扑提示（Topology Hint）信息将流量优先路由到距离发起请求的地点更近的端点。在网络流量跨可用区的场景下，该功能会优先将网络流量保持在同一区域内，从而提高网络效率并减少相应的成本。更多信息，请参见 [Topology Aware Routing](https://kubernetes.io/docs/concepts/services-networking/topology-aware-routing/)。

## 组件推荐配置

ACK提供多种类型的组件，您可以根据业务需求为新建集群或已创建集群配置特定组件，拓展集群功能。关于ACK支持的组件及其介绍与变更记录，请参见 [组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/ "")；关于如何升级和管理（配置、卸载、升级等）组件，请参见 [管理组件](https://help.aliyun.com/zh/ack/manage-system-components "")。

### **合理部署Nginx Ingress Controller**

在部署Nginx Ingress Controller时，请确保Nginx Ingress Controller分布在不同的节点上，避免不同Nginx Ingress Controller之间资源的抢占和单点故障。您也可以为其使用独占节点来保证性能与稳定性，具体操作，请参见 [使用独占节点保证Nginx Ingress性能与稳定性](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-the-nginx-ingress-controller-2#task-2170008 "")。

建议您不要为Nginx Ingress Controller设定资源限制，避免OOM所带来的流量中断。如果确实有限制的需要，建议资源限制CPU不低于1000 Milicore（YAML配置里格式为1000m）和内存不低于2 GiB。关于Nginx Ingress Controller的更多配置建议，请参见 [Nginx Ingress Controller使用建议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-the-nginx-ingress-controller-2#task-2175597 "")。

**说明**

如果您创建的Ingress Controller类型为ALB Ingress Controller或MSE Ingress Controller，建议您在创建对应的Ingress Controller时配置多可用区，具体操作请参见 [新建云原生网关](https://help.aliyun.com/zh/mse/user-guide/create-a-cloud-native-gateway-1 "")、 [创建并使用ALB Ingress对外暴露服务](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-and-use-alb-ingress-to-expose-services-to-the-public#task-2098039 "")。关于不同Ingress Controller的对比，请参见 [Nginx Ingress、ALB Ingress和MSE Ingress对比](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-among-nginx-ingresses-alb-ingresses-and-mse-ingresses-1 "")。

### **合理部署CoreDNS**

建议您在部署CoreDNS副本时，将CoreDNS副本分散在不同可用区、不同集群节点上，避免单节点、单可用区故障。CoreDNS默认配置了按节点的弱反亲和性，可能会因为节点资源不足导致部分或全部副本部署在同一节点上，如果遇到这种情况，请删除Pod重新触发其调度来进行调整。

CoreDNS所运行的集群节点应避免CPU、内存用满的情况，否则会影响域名解析的QPS和响应延迟。关于CoreDNS的更多配置建议，请参见 [DNS最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dns-best-practices#task-2175597 "")。

## **相关文档**

- 推荐您的Worker节点使用较大规格的ECS实例，更多信息请参见 [ECS实例规格配置建议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/select-ecs-instances-to-create-the-master-and-worker-nodes-of-an-ack-cluster "")。

- 如您的ACK托管集群Pro版规模较大（通常为超过500个节点或者10,000个Pod的集群），请参见 [大规模集群使用建议](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/suggestions-on-how-to-work-with-large-ack-pro-clusters "") 获取使用建议。

- 关于节点与节点池的最佳实践，请参见 [节点与节点池最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-nodes-and-node-pools/ "")。

- 关于弹性伸缩的最佳实践，请参见 [弹性伸缩最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-for-auto-scaling/ "")。