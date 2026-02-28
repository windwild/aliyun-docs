### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[工作负载](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/workloads/)Pod异常问题排查

# Pod异常问题排查

更新时间：2026-01-16 04:21:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：将微服务应用接入MSE治理中心（Java版）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/access-microservice-applications-to-mse-governance-center)[下一篇：工作负载FAQ](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-applications)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速诊断流程

Pod持续处于调度中状态（Pending）

镜像拉取失败（ImagePullBackOff/ErrImagePull）

Pod启动失败（CrashLoopBackOff）

Pod启动失败（Pod处于Running但未就绪状态）

Pod出现内存溢出状态（OOMKilled）

完整诊断流程

阶段一：调度问题

Pod未调度到节点

Pod已调度到节点

阶段二：镜像拉取问题

ImagePullBackOff或ErrImagePull

阶段三：启动问题

Pod处于init状态

Pod创建中（Creating）

Pod启动失败（CrashLoopBackOff）

Pod处于Running但未就绪状态（Ready: False）

阶段四：Pod运行问题

OOMKilled

Terminating

Evicted

Completed

常见问题

本文介绍Pod异常问题排查的诊断流程、排查方法、常见问题及对应的解决方案。

**说明**

如需了解排查Pod问题常用的控制台界面，例如如何查看Pod状态、基础信息、配置、事件和日志，使用终端进入容器，启用Pod故障诊断等，可跳转至 [常用排查界面](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#section-qg5-gds-iwn "") 了解。

## **快速诊断流程**

查看工作负载Pod异常状态，进入目标 **容器组** 详情页，单击 **事件** 页签，查看异常事件的对应描述信息。单击 **日志** 页签，查看最近发生的异常日志记录。

### Pod持续处于调度中状态（Pending）

若 Pod **现状详情** 中出现Unschedulable状态或 **事件** 中出现FailedScheduling，请通过**节点管理** \> **节点**检查目标节点健康状态及资源水位（CPU/内存）。此外，需排查 Pod 的亲和性策略是否过于严格，包括nodeSelector、nodeAffinity 以及污点（Taints）与容忍（Tolerations）配置。如需进一步排查，请参考 [调度问题](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#8e73e5fd3azxp "")。

### 镜像拉取失败（ImagePullBackOff/ErrImagePull）

在 **容器组** 详情页下方，选择 **容器** 页签检查 **镜像** 地址。登录Pod所在节点，使用`crictl pull <镜像地址>`或`curl -v https://<镜像地址>`验证与镜像仓库网络连通性。单击右上角 **YAML 编辑**，检查工作负载`spec.imagePullSecrets`指定的Secret是否存在且正确。如需进一步排查，请参考 [镜像拉取问题](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#c638c00074o8e "")。

### Pod启动失败（CrashLoopBackOff）

因应用反复崩溃重启导致。在 **容器组** 详情页下方单击 **日志** 页签，勾选 **显示上个容器退出时的日志**，会记录进程发生异常的原因。如需进一步排查，请参考 [Pod启动失败排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#0402c829af9x0 "")。

### **Pod启动失败（Pod处于Running但未就绪状态）**

因Pod就绪检查失败导致。在目标 **工作负载** 的 **编辑** 页，确认健康检查请求路径（如/healthz）和端口与应用实际提供的是否一致。如需进一步排查，请参考 [Pod处于Running但未就绪状态（Ready: False）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#9c2d5d4cdat3q "")。

> 可临时关闭健康检查，进入Pod终端或Pod宿主机，使用命令（如curl）验证健康检查方法是否通过。

### **Pod出现内存溢出状态（OOMKilled）**

在 **容器组** 详情页下方单击 **日志** 页签，勾选 **显示上个容器退出时的日志**，会记录OOM日志。确认应用是否存在内存泄漏或内存溢出（Java应用可优化-Xmx参数），按需调整应用的内存资源限制（`resources.limits.memory`）。如需进一步排查，请参考 [OOMKilled](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#f691571f75vk9 "")。

> 如已配置存活检查，则Pod只会短暂停留在OOMKilled状态，然后自动重启。

## 完整诊断流程

如果Pod状态异常，可通过查看Pod的事件、Pod的日志、Pod的配置等信息确定异常原因。

**排查流程导览**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4925558671/CAEQUBiBgICjhuGJlxkiIGRkZmRmN2Q5OTY2MTRiYzE5MmY3NTU4MWFjZDRkNDgx4700556_20241009135458.830.svg)

## **阶段一：调度问题**

### Pod未调度到节点

如果Pod长时间处于“未调度到节点”（Pending）状态，没有被安排到任何节点上运行，可能是由以下原因导致。

| **报错信息** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **报错信息** | **说明** | **推荐的解决方案** |
| `no nodes available to schedule pods.` | 当前集群中无可用节点可供调度。 | 1. 查看集群节点状态是否为NotReady。如果存在节点处于NotReady状态，则对问题节点进行检查和修复。<br>   <br>2. 检查Pod中是否声明了nodeSelector、nodeAffinity或污点容忍。若不存在亲和性策略，可以增加节点池中的节点数量。 |
| - `0/x nodes are available: x Insufficient cpu.`<br>  <br>- `0/x nodes are available: x Insufficient memory.` | 集群中没有可用节点能够满足Pod所需的CPU或内存资源。<br>> 即使节点当前的实际 CPU/内存使用率很低，只要其注册的Requests总和已满，依然会被判定为不可调度。 | 在目标集群详情页选择**节点管理** \> **节点**，查看目标节点的CPU或内存的 **请求量（Requests）** 分配率，鼠标可悬停在分配率上查看具体的资源分配数值。<br>![request中](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6862558671/p1045204.png)<br>如需查看详细的节点资源使用明细，请参见 [使用kubectl查看节点资源占用](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#f51c49d634g0j "")。<br>- **优化资源配置：**<br>  <br>  - 如节点资源 **使用量（Usage）** 长期低于 **请求量**，说明资源使用存在浪费，可降低工作负载的`requests`配置。请参见 [设置容器的CPU和内存资源上下限](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/manage-pods#section-pha-i7u-5ow "")。<br>    <br>    <br>    > 可启用 [资源画像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/resource-profiling "")，获得`requests`推荐配置。<br>    <br>  - 为业务容器 [开启弹性伸缩（HPA）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/horizontal-pod-autoscaling#p-8d9-8xy-crw "")，在业务低峰期减少副本数以降低整体的资源消耗。<br>- **清理无效负载**：下线非必要的业务Pod **。**<br>  <br>- **节点池扩容**：如目标节点的资源使用率都很高，说明节点资源已饱和，可进行 [节点池扩容](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/scale-a-node-pool#title-8o2-dfx-r5s "")。 |
| `x node(s) didn't match Pod's node affinity/selector.` | 集群现有节点没有匹配Pod声明的节点亲和性策略（`nodeAffinity`/`nodeSelector`）。请参考 [Pod指派策略](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector)。 | 1. 查看节点所有的标签。<br>   <br>   <br>   <br>   <br>   <br>   <br>   控制台<br>   <br>   <br>   <br>   kubectl<br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   1. 进入目标集群详情页，选择**节点管理** \> **节点**。<br>      <br>   2. 在 **节点** 页，找到目标节点，单击右侧 **操作** 列中**更多** \> **标签与污点管理**，进行查看。<br>      <br>将`<YOUR_NODE_NAME>`替换为实际的节点名称。<br>```bash<br>kubectl get node <YOUR_NODE_NAME> --show-labels<br>```<br>2. 检查并调整工作负载（Deployment）的节点亲和性策略。<br>   <br>   <br>   <br>   <br>   <br>   <br>   控制台<br>   <br>   <br>   <br>   YAML示例<br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   新建工作负载时：<br>   <br>   <br>   <br>   1. 在 **创建** Deployment的 **高级配置** 页面，找到 **调度设置** 区块的 **节点亲和性**，单击 **添加**。<br>      <br>   2. **必须满足** 和 **尽量满足** 根据业务任选其一进行配置。多个 **选择器** 之间为逻辑与（and）关系，多个 **规则** 之间为逻辑或（or）关系。<br>      <br>已有工作负载时：<br>   1. 在**节点管理** \> **节点**页面，单击目标Deployment右侧 **操作** 列的**![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6862558671/p1034154.png)** \> **节点亲和性**。<br>      <br>   2. 配置方法同上。<br>      <br>nodeAffinity<br>nodeSelector<br>亲和性策略分为硬亲和性（`requiredDuringSchedulingIgnoredDuringExecution`）和软亲和性（`preferredDuringSchedulingIgnoredDuringExecution`），硬亲和性表示必须满足，而软亲和性为尽量满足。以下以硬亲和为例。<br>```yaml<br>apiVersion: apps/v1<br>kind: Deployment<br>metadata:<br>  name: app-demo-node-affinity-deploy<br>  labels:<br>    app: demo-node-affinity<br>spec:<br>  replicas: 2<br>  selector:<br>    matchLabels:<br>      app: demo-node-affinity<br>  template:<br>    metadata:<br>      labels:<br>        app: demo-node-affinity<br>    spec:<br>      containers:<br>      - name: nginx<br>        image: anolis-registry.cn-zhangjiakou.cr.aliyuncs.com/openanolis/nginx:1.14.1-8.6<br>      affinity:<br>        nodeAffinity:<br>          # 【必须满足】节点亲和性<br>          requiredDuringSchedulingIgnoredDuringExecution:<br>            nodeSelectorTerms:<br>            - matchExpressions:<br>              - key: disktype<br>                operator: In<br>                values:<br>                - ssd<br>                - nvme  # 逻辑：SSD 或 NVMe 均可<br>```<br>简单的完全匹配，仅当节点标签满足条件才允许调度。<br>```yaml<br>apiVersion: apps/v1<br>kind: Deployment<br>metadata:<br>  name: app-demo-node-selector-deploy<br>  labels:<br>    app: demo-node-selector<br>spec:<br>  replicas: 2  <br>  selector:<br>    matchLabels:<br>      app: demo-node-selector  <br>  template:<br>    metadata:<br>      labels:<br>        app: demo-node-selector<br>    spec:<br>      containers:<br>      - name: nginx<br>        image: anolis-registry.cn-zhangjiakou.cr.aliyuncs.com/openanolis/nginx:1.14.1-8.6<br>      # 仅当节点拥有标签 disktype=ssd 时，Pod 才会被调度<br>      nodeSelector:<br>        disktype: ssd<br>``` |
| - `x node(s) didn't match pod affinity rules.`<br>  <br>- `x node(s) didn't match pod anti-affinity rules.` | - 亲和性匹配失败。Pod 设置了 **应用亲和性** 规则（如指定标签），但所有节点上均不存在标签匹配的 Pod，无法调度。<br>  <br>- 反亲和性互斥。Pod 设置了 **应用反亲和性** 规则（如不可与某应用共存），但所有节点上均已存在互斥的 Pod，无法调度。 | 1. 查看节点内Pod的标签。<br>   <br>   <br>   <br>   <br>   <br>   <br>   控制台<br>   <br>   <br>   <br>   kubectl<br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   1. 进入目标集群详情页，选择**节点管理** \> **节点**。<br>      <br>   2. 在 **节点** 页，点击目标节点名称进入详情页。下滑页面到 **容器组** 区块，可在 **标签** 列查看不同Pod的标签值。<br>      <br>   - **通过Pod查询标签**：将`<YOUR_NAMESPACE>`替换为命名空间名称，`<YOUR_NODE_NAME>`替换为实际的节点名称。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```bash<br>     kubectl get pods -n <YOUR_NAMESPACE> --field-selector spec.nodeName=<YOUR_NODE_NAME> -o custom-columns=NAME:.metadata.name,LABELS:.metadata.labels<br>     ```<br>     <br>   - **通过标签查询Pod**：将`<LABEL>`替换为实际的标签键值，如`app=nginx`。<br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     <br>     ```bash<br>     kubectl get pods -A -l <LABEL> -o wide<br>     ```<br>     <br>2. 检查并调整工作负载（Deployment）的应用亲和性策略。<br>   <br>   <br>   <br>   <br>   <br>   <br>   控制台<br>   <br>   <br>   <br>   YAML示例<br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   <br>   1. 新建工作负载时，在 **创建** Deployment的 **高级配置** 页面，找到 **调度设置** 区块的 **应用亲和性**/ **应用反亲和性**，单击 **添加**。<br>      <br>   2. **必须满足** 和 **尽量满足** 根据业务任选其一进行配置。多个 **选择器** 之间为逻辑与（and）关系，多个 **添加规则** 之间也为逻辑与（and）关系。<br>      <br>亲和性策略分为硬亲和性（`requiredDuringSchedulingIgnoredDuringExecution`）和软亲和性（`preferredDuringSchedulingIgnoredDuringExecution`），硬亲和性表示必须满足，而软亲和性为尽量满足。以下以必须满足的 **应用亲和性** 配置为例。<br>应用反亲和性配置只需将`podAffinity`替换为`podAntiAffinity`即可。<br>```yaml<br>apiVersion: apps/v1<br>kind: Deployment<br>metadata:<br>  name: app-demo-podaffinity-deploy<br>spec:<br>  replicas: 2<br>  selector:<br>    matchLabels:<br>      app: demo-podaffinity<br>  template:<br>    metadata:<br>      labels:<br>        app: demo-podaffinity<br>    spec:<br>      containers:<br>      - name: nginx<br>        image: anolis-registry.cn-zhangjiakou.cr.aliyuncs.com/openanolis/nginx:1.14.1-8.6<br>      affinity:<br>        podAffinity:<br>          # 【必须满足】应用亲和性<br>          requiredDuringSchedulingIgnoredDuringExecution:<br>          - labelSelector:<br>              matchExpressions:<br>              - key: app<br>                operator: In<br>                values:<br>                - nginx<br>            # 拓扑域范围：物理机隔离级别<br>            topologyKey: kubernetes.io/hostname<br>``` |
| `0/x nodes are available: x node(s) had volume node affinity conflict.` | Pod所使用的存储卷与待调度的节点之间存在亲和性冲突，云盘无法跨可用区挂载，导致调度失败。 | - 若为静态PVC，希望Pod能够调度到与PV所在相同可用区的节点，需配置Pod的节点亲和性。<br>  <br>- 若为动态PVC，需设置StorageClass的云盘的绑定模式为WaitForFirstConsumer，以便PV等到Pod已调度到节点后再创建，确保云盘被创建在Pod实际运行的节点所在的可用区。 |
| `InvalidInstanceType.NotSupportDiskCategory` | ECS实例不支持挂载的云盘类型。 | 请参见 [实例规格族](https://help.aliyun.com/zh/ecs/user-guide/overview-of-instance-families#concept-sx4-lxv-tdb "") 确认当前ECS支持的云盘类型。挂载时，将云盘类型更新为ECS实例当前支持的类型。 |
| `0/x nodes are available: x node(s) had taints that the pod didn't tolerate.` | 由于节点拥有Pod无法容忍的污点，导致Pod无法调度。 | - 如果污点是手动添加的，可删除非预期的污点。如果无法删除污点，可以为Pod配置相应的容忍，请参见 [污点和容忍](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)、 [管理节点标签和污点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/manage-taints-and-tolerations#task-2553278 "")。<br>  <br>- 如果污点为系统自动添加，可参见下文解决对应的问题，并等待Pod重新调度。<br>  <br>  <br>  <br>  **展开查看系统自行添加的污点**<br>  <br>  <br>  <br>  <br>  <br>  <br>  - `node.kubernetes.io/not-ready`：节点未准备好，处于NotReady状态。<br>    <br>  - `node.kubernetes.io/unreachable`：节点控制器访问不到节点，相当于节点状态`Ready` 的值为`Unknown`。<br>    <br>  - `node.kubernetes.io/memory-pressure`：节点存在内存压力。<br>    <br>  - `node.kubernetes.io/disk-pressure`：节点存在磁盘压力。<br>    <br>  - `node.kubernetes.io/pid-pressure`：节点存在PID压力。<br>    <br>  - `node.kubernetes.io/network-unavailable`：节点网络不可用。<br>    <br>  - `node.kubernetes.io/unschedulable`：节点不可调度。 |
| `0/x nodes are available: x Insufficient ephemeral-storage.` | 节点临时存储容量不足。 | 1. 检查Pod是否配置了临时存储卷的限制，即Pod YAML中`spec.containers.resources.requests.ephemeral-storage`的取值。如果取值过高，超出了节点的实际可用容量，Pod会调度失败。<br>   <br>2. 执行`kubectl describe node | grep -A10 Capacity`命令，查看各个节点上可用于临时存储的总容量。如果容量不足，可扩容节点磁盘或增加节点数量。 |
| `0/x nodes are available: pod has unbound immediate PersistentVolumeClaims.` | Pod绑定PVC失败。 | 检查Pod所指定的PVC或PV是否已经创建，通过`kubectl describe pvc <pvc-name>` 或 `kubectl describe pv <pv-name>`命令查看PVC、PV的Event信息，进一步进行判断。更多信息，请参见 [存储FAQ-CSI](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-csi#section-4xc-k2n-l04 "")。 |

### Pod已调度到节点

如果Pod已经被调度到某个节点上但仍处于Pending状态，请参见下文解决。

1. 判断Pod是否配置了`hostPort`：如果Pod配置了`hostPort`，那么每个节点上只能运行一个使用该`hostPort`的Pod实例。因此，Deployment或ReplicationController中`Replicas`值不能超过集群中的节点数。如果该端口被其他应用占用，将导致Pod调度失败。

`hostPort`会带来一些管理和调度上的复杂性，推荐使用Service来访问Pod，请参见 [服务（Service）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/#section-8r6-o68-beu "")。

2. 如果Pod没有配置`hostPort`，请参见下方步骤排查。

1. 通过`kubectl describe pod <pod-name>`命令查看Pod的Event信息，并解决对应的问题。Event可能会解释Pod启动失败的原因，例如镜像拉取失败、资源不足、安全策略限制、配置错误等。

2. Event中没有有效信息时，进一步查看该节点kubelet的日志，以排查Pod启动过程中存在的问题。可通过`grep -i <pod name> /var/log/messages* | less`命令搜索系统日志文件（`/var/log/messages*`）中包含指定Pod名称的日志条目。

## **阶段二：镜像拉取问题**

### **ImagePullBackOff或ErrImagePull**

Pod状态为`ImagePullBackOff`或`ErrImagePull`时，即表明拉取镜像失败。在这种情况下，请查看Pod事件（Event），并根据下方的信息排查问题。

| **报错信息** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **报错信息** | **说明** | **推荐的解决方案** |
| `Failed to pull image "xxx": rpc error: code = Unknown desc = Error response from daemon: Get xxx: denied:` | 请求访问镜像仓库时被拒绝，创建Pod时未指定`imagePullSecret`。 | 检查工作负载YAML中`spec.imagePullSecrets`指定的Secret是否存在。<br>使用ACR时，可以使用免密插件拉取镜像，请参见 [同账号拉取镜像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/non-secret-pulling-container-image "")。 |
| `Failed to pull image "xxxx:xxx": rpc error: code = Unknown desc = Error response from daemon: Get https://xxxxxx/xxxxx/: dial tcp: lookup xxxxxxx.xxxxx: no such host` | 通过HTTPS协议从指定的镜像仓库地址拉取镜像时，镜像地址解析失败。 | 1. 检查Pod YAML中`spec.containers.image`配置的镜像仓库地址是否正确。如有误，需修改为正确地址。<br>   <br>2. 如地址无误，进一步验证从Pod所在节点到镜像仓库的网络连接是否通畅。参见 [选择ECS远程连接方式](https://help.aliyun.com/zh/ecs/user-guide/connect-to-instance "") 登录到Pod所在节点，运行命令`curl -kv https://xxxxxx/xxxxx/` 判断地址是否可以访问。如有报错，进一步判断是否存在网络配置、防火墙规则、DNS解析等网络访问问题。 |
| `Failed create pod sandbox: rpc error: code = Unknown desc = failed to create a sandbox for pod "xxxxxxxxx": Error response from daemon: mkdir xxxxx: no space left on device` | 节点磁盘空间不足。 | 参见 [选择ECS远程连接方式](https://help.aliyun.com/zh/ecs/user-guide/connect-to-instance "") 登录到Pod所在节点，运行`df -h`查看磁盘空间状态。如磁盘已满，请扩容磁盘，请参见 [步骤一：扩容云盘容量](https://help.aliyun.com/zh/ecs/user-guide/step-1-resize-a-disk-to-extend-its-capacity#concept-syg-jxz-2hb "")。 |
| `Failed to pull image "xxx": rpc error: code = Unknown desc = error pulling image configuration: xxx x509: certificate signed by unknown authority` | 第三方仓库使用了非知名或不安全的CA签署的证书。 | 1. 建议第三方仓库使用CA签发的证书。

2. 如使用的是私有镜像仓库，请参见 [使用私有镜像仓库创建应用](https://help.aliyun.com/zh/ack/create-an-application-by-using-a-private-image-repository#task-1614276 "")。

3. 如果无法更改，可酌情参考下面流程，配置允许节点从使用非安全证书的仓库中拉取和推送镜像。建议仅在测试环境中使用，可能会对节点其他Pod的运行产生影响。


**展开查看详细步骤**

控制台方式

命令行方式

### 通过控制台自定义节点池containerd参数

修改 containerd 配置不会对存量容器造成影响。为确保集群稳定性，请在业务低峰期操作。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点池**。

3. 在节点池列表页面，单击目标节点池 **操作** 列下的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2851252471/p931503.png)\> **Containerd 配置**。

4. 仔细阅读当前页面上的注意事项，按照页面指引添加待配置的参数，指定目标节点，并设置批量配置策略，然后单击 **提交**，完成相应操作。


> 可参见下方 [配置示例](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-the-containerd-configurations-of-a-node-pool#74c1a184300pl "")。


   - 配置 [容器运行时自定义配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-the-containerd-configurations-of-a-node-pool#3c46ea50edik7 "") 时，如移除该配置，将自动恢复为默认值。

   - 提交后，containerd配置将按批次对节点生效。执行需要一定时间，可在事件列表区域查看执行进度，并控制执行过程，例如暂停、继续、取消等。如果有节点任务执行失败，可排查节点问题后单击 **继续**，重新执行。

     可使用暂停功能对已升级的节点进行验证。执行暂停操作时，正在配置中的节点会继续完成执行；尚未执行的节点在任务继续前不会被执行自定义配置。建议尽快完成自定义配置任务。处于暂停状态的任务将在7天后自动取消，相关的事件和日志信息也会被清理。

### 配置示例

|     |     |     |
| --- | --- | --- |
| **为docker.io配置替换的镜像仓库** | **指定私有仓库跳过证书的认证** | **配置HTTP私有镜像仓库** |
| ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4354632471/p920660.png) | ![image](<Base64-Image-Removed>) | ![image](<Base64-Image-Removed>) |

1. 为containerd创建证书目录，用于存放与特定镜像仓库相关的证书配置文件。















```shell
mkdir -p /etc/containerd/cert.d/xxxxx
```

2. 配置containerd信任特定的非安全镜像仓库。















```shell
cat << EOF > /etc/containerd/cert.d/xxxxx/hosts.toml
      server = "https://harbor.test-cri.com"
      [host."https://harbor.test-cri.com"]
        capabilities = ["pull", "resolve", "push"]
        skip_verify = true
        # ca = "/opt/ssl/ca.crt"  # 或者上传ca证书
      EOF
```

3. 修改Docker Daemon配置以添加非安全仓库。















```shell
vi /etc/docker/daemon.json
```



    添加以下内容。其中需替换`your-insecure-registry`为目标私有仓库地址。















```json
      {
        "insecure-registries": ["your-insecure-registry"]
      }
```

4. 重启相关服务，使更新的配置生效。















```shell
systemctl restart containerd
``` |
| `Failed to pull image "XXX": rpc error: code = Unknown desc = context canceled` | 操作取消，可能是由于镜像文件过大。Kubernetes默认设置了拉取镜像超时时间，如果一定时间内镜像下载没有任何进度更新，Kubernetes会认为此操作异常或处于无响应状态，主动取消该任务。 | 1. 检查Pod YAML中配置的`imagePullPolicy`是否为`IfNotPresent`。<br>   <br>2. 参见 [选择ECS远程连接方式](https://help.aliyun.com/zh/ecs/user-guide/connect-to-instance "") 登录到Pod所在节点，运行命令`docker pull`或`crictl pull`判断镜像是否可以被拉取。 |
| `Failed to pull image "xxxxx": rpc error: code = Unknown desc = Error response from daemon: Get https://xxxxxxx: xxxxx/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)` | 无法连接镜像仓库，网络不通。 | 1. 参见 [选择ECS远程连接方式](https://help.aliyun.com/zh/ecs/user-guide/connect-to-instance "") 登录到Pod所在节点，运行命令`curl https://xxxxxx/xxxxx/`判断地址是否可以访问。如有报错，进一步判断是否存在网络配置、防火墙规则、DNS解析等网络访问问题。<br>   <br>2. 判断节点的公网策略是否正常，例如SNAT条目、绑定的弹性公网IP等配置。 |
| `Failed to pull image "xxxx:xxx": failed to pull and unpack image "xxxx:xxx": failed to resolve reference "xxxx:xxx": failed to do request: Head "xxxx:xxx": dial tcp xxx.xxx.xx.x:xxx: i/o timeout` | 拉取海外源镜像时，因网络问题导致的连接超时。 | 受运营商网络的影响，在ACK集群中拉取Docker Hub海外源镜像可能出现拉取失败的情况。可采用下列解决方案：<br>- 通过 [容器镜像服务ACR](https://help.aliyun.com/zh/acr/product-overview/what-is-container-registry "") 订阅海外源镜像，请参见 [通过制品订阅获取海外源镜像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/subscribe-to-image-tags "")。<br>  <br>- 创建 [全球加速GA（Global Accelerator）](https://help.aliyun.com/zh/ga/product-overview/what-is-global-accelerator/ "") 实例，使用其覆盖全球的网络加速服务直接拉取海外源镜像，请参见 [使用GA实现ACK跨域加速拉取容器镜像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cross-domain-accelerated-pulling-container-images "")。 |
| `Too Many Requests.` | DockerHub对用户拉取容器镜像的请求设定了 [上限](https://www.docker.com/increase-rate-limits/)。 | 将镜像上传至 [容器镜像服务ACR](https://help.aliyun.com/zh/acr/product-overview/what-is-container-registry "")，从ACR镜像仓库中拉取镜像。 |
| 一直显示`Pulling image` | 可能触发了kubelet的镜像拉取限流机制。 | 通过 [自定义节点池kubelet配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-the-kubelet-configurations-of-a-node-pool "") 功能调整registryPullQPS（镜像仓库的QPS上限）和registryBurst（突发性镜像拉取的个数上限）。 |

## **阶段三：启动问题**

### **Pod处于init状态**

| **错误信息** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误信息** | **说明** | **推荐的解决方案** |
| 停留在`Init:N/M`状态 | 该Pod包含M个Init容器，其中N个已经启动完成，但仍有M-N个Init容器未启动成功。 | 1. 通过`kubectl describe pod -n <ns> <pod name>`命令查看Pod的事件，确认当前Pod中未启动的Init容器是否存在异常。<br>   <br>2. 通过`kubectl logs -n <ns> <pod name> -c <container name>`命令查看Pod中未启动的Init容器的日志，通过日志内容排查问题。<br>   <br>3. 查看Pod的配置，例如检查健康检查配置，进一步确认未启动的Init容器配置是否正常。<br>   <br>关于Init容器的更多信息，请参见 [调试Init容器](https://kubernetes.io/zh/docs/tasks/debug/debug-application/debug-init-containers/)。 |
| 停留在`Init:Error`状态 | Pod中的Init容器启动失败。 |
| 停留在`Init:CrashLoopBackOff`状态 | Pod中的Init容器启动失败并处于反复重启状态。 |

### **Pod创建中（Creating）**

| **错误信息** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误信息** | **说明** | **推荐的解决方案** |
| `failed to allocate for range 0: no IP addresses available in range set: xx.xxx.xx.xx-xx.xx.xx.xx` | 由于Flannel网络插件设计原因导致，是预期内现象。 | 升级Flannel组件版本至v0.15.1.11-7e95fe23-aliyun及以上版本，请参见 [Flannel](https://help.aliyun.com/zh/ack/product-overview/flannel "")。 |
| 集群低于1.20版本时，如果发生Pod反复重启、CronJob中的Pod在短时间内完成任务并退出等事件，可能会导致IP地址泄漏。 | 升级集群版本至1.20及以上，推荐使用最新版本的集群，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。 |
| containerd、runC存在的缺陷。 | 参见 [为什么Pod无法正常启动，且报错no IP addresses available in range？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-iiz-3h3-xyl "") 进行临时紧急处理。 |
| `error parse config, can't found dev by mac 00:16:3e:01:c2:e8: not found` | Pod所在的节点中，Terway网络插件维护的用于追踪和管理网络接口ENI的内部数据库状态与实际的网络设备配置之间存在数据不一致，造成ENI分配失败。 | 1. 网卡在系统中加载是异步的。在CNI配置过程中，网卡可能仍在加载中，可能导致CNI自动重试。这种情况不会影响ENI最终的分配，请通过Pod最终状态判断操作是否成功。<br>   <br>2. 如果Pod长时间没有创建成功，仍然提示上述错误，通常是由于ENI挂载时高阶内存不足导致驱动加载失败。请通过重启ECS实例来解决，请参见 [重启实例](https://help.aliyun.com/zh/ecs/user-guide/restart-instances "")。 |
| - `cmdAdd: error alloc ip rpc error: code = DeadlineExceeded desc = context deadline exceeded`<br>  <br>- `cmdAdd: error alloc ip rpc error: code = Unknown desc = error wait pod eni info, timed out waiting for the condition` | 可能是Terway向vSwitch申请IP时失败。 | 1. 查看Pod所在节点中Terway组件Pod的Terway容器日志，查看ENI分配过程。<br>   <br>2. 执行`kubectl logs -n kube-system  <terwayPodName > -c terway | grep <podName>`命令，查看Terway Pod中Terway网卡的ENI情况，获取到申请IP操作的Request ID以及OpenAPI的报错信息。<br>   <br>3. 根据Request ID和报错信息进一步排查失败的原因。 |

### **Pod启动失败（CrashLoopBackOff）**

| **错误信息** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误信息** | **说明** | **推荐的解决方案** |
| 日志中存在`exit(0)`。 | 1. 登录异常工作负载所在的节点。<br>   <br>2. 执行`docker ps -a | grep $podName`命令，如果容器中无持续进程，会出现`exit (0)`。 |
| Pod事件中存在`Liveness probe failed: ...`。 | 存活探针（Liveness Probe）检测失败，应用重启。 | - 存活检查配置：进入目标 **工作负载** 的 **编辑** 页，确认健康检查请求路径（如/healthz）和端口与应用实际提供的是否一致。增加 **延迟探测时间（秒）**，确保应用已启动完毕才开始进行存活检查。<br>  <br>  <br>  > 可临时关闭 **存活检查**，进入Pod终端或Pod宿主机，使用命令（如curl）验证健康检查方法是否通过。<br>  <br>- 排查业务异常：结合Pod **事件** 和 **日志**（勾选 **显示上个容器退出时的日志**）排查。 |
| Pod事件中出现`Startup probe failed: ...`信息。 | 启动探针（Startup Probe）检测失败，应用重启。 | - 启动检测配置：进入目标 **工作负载** 的 **编辑** 页，确认健康检查请求路径（如/healthz）和端口与应用实际提供的是否一致。如启动时间较长，可增加 **不健康阈值**，避免过早判定为失败而自动重启。<br>  <br>  <br>  > 可临时关闭 **启动探测**，进入Pod终端或Pod宿主机，使用命令（如curl）验证健康检查方法是否通过。<br>  <br>- 排查业务异常：结合Pod **事件** 和 **日志**（勾选 **显示上个容器退出时的日志**）排查。 |
| Pod日志中存在`no left space`。 | 磁盘空间不足。 | - 参见 [步骤一：扩容云盘容量](https://help.aliyun.com/zh/ecs/user-guide/step-1-resize-a-disk-to-extend-its-capacity "") 扩容磁盘。<br>  <br>- 清理不必要的镜像，释放磁盘空间，并按需配置imageGCHighThresholdPercent，控制节点上触发镜像垃圾回收（Image GC）的阈值。 |
| 启动失败，无Event信息。 | Pod中声明的Limit资源少于实际所需资源时，会导致启动容器失败。 | 检查Pod的资源配置是否正确。可启用 [资源画像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/resource-profiling "")，获得容器Request和Limit的推荐配置。 |
| Pod日志中出现`Address already in use`。 | 同一Pod中的容器端口存在冲突。 | 1. 检查Pod是否配置了`hostNetwork: true`，这意味着Pod内的容器会直接与宿主机共享网络接口和端口空间。如果无需使用，请改为`hostNetwork: false`。<br>   <br>2. 如果Pod需要使用`hostNetwork: true`，请配置Pod的反亲和性，确保同一副本集中的Pod被调度到不同节点。<br>   <br>3. 检查并确保同一节点上没有其他Pod占用该端口。 |
| Pod日志中出现`container init caused "setenv: invalid argument": unknown`。 | 工作负载中挂载了Secret，但Secret对应的值没有进行Base64加密。 | - 通过控制台创建Secret，Secret对应的值会自动进行Base64加密。具体操作，请参见 [管理保密字典](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/manage-secrets "")。<br>  <br>- 通过YAML创建Secret，并执行`echo -n "xxxxx" | base64`命令手动对密钥值进行Base64加密。 |
| 自身业务问题。 | 查看Pod日志，通过日志内容排查问题。 |

### **Pod处于Running但未就绪状态（Ready: False）**

| **报错信息** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **报错信息** | **说明** | **推荐的解决方案** |
| ![image](<Base64-Image-Removed>)Pod事件中出现`Readiness probe failed: ...`信息。 | 就绪探针（Readiness Probe）检测失败，目标Pod无法接入流量。 | - 就绪检查配置：进入目标 **工作负载** 的 **编辑** 页，确认健康检查请求路径（如/healthz）和端口与实际应用提供的是否一致。如启动时间较长，可增加 **不健康阈值**，避免过早判定为失败。<br>  <br>  <br>  > 可临时关闭 **就绪检查**，进入Pod终端或其所在宿主机，使用命令（如curl）验证健康检查方法是否能正确响应。<br>  <br>- 排查业务异常：结合Pod **事件** 和 **日志**（勾选 **显示上个容器退出时的日志**）排查。 |
| Pod状态同上。Pod事件中出现`Startup probe failed: ...`信息。 | 启动探针（Startup Probe）检测失败，目标Pod无法接入流量。 | 同上，配置合适的 **启动探测** 项。 |

## **阶段四：Pod运行问题**

### OOMKilled

当集群中的容器使用超过其限制的内存，容器可能会被终止，触发OOM（Out Of Memory）事件，导致容器异常退出。关于OOM事件，请参见 [为容器和Pod分配内存资源](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/)。

- 若被终止的进程为容器的阻塞进程，可能会导致容器异常重启。

- 若出现OOM异常问题，在控制台的Pod详情页面单击 **事件** 页签将展示OOM事件`pod was OOM killed. node:XXX pod:XXX namespace:XXX`。

- 若集群配置了集群容器副本异常报警，OOM事件出现时会收到相关报警信息，请参见 [容器副本异常报警规则集](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/alert-management#f40d8c0ed30jl "")。


| **OOM级别** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **OOM级别** | **说明** | **推荐的解决方案** |
| 节点级 | 查看Pod所在节点的内核日志`/var/log/messages`，日志中存在Killed Process，但不存在cgroup日志，表明OOM为OS级别。 | - 扩容节点内存资源或将工作负载分散到更多节点，详情请参见 [升降配节点资源](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-the-configurations-of-a-worker-node "")、 [调度应用至指定节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/schedule-pods-to-specific-nodes "")。<br>  <br>- 排查节点上内存占用高的Pod，并为其设置合理的memory limits。 |
| CGroup级 | 查看Pod所在节点的内核日志`/var/log/messages`，日志中存在类似`Task in /kubepods.slice/xxxxx killed as a result of limit of /kubepods.slice/xxxx`的报错信息，表明OOM为cgroup级别。 | - 根据业务需求适当提升 Pod 的memory limits，建议实际用量不超过 limits 的 80%。相关操作，请参见 [管理容器组（Pod）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/manage-pods#section-pha-i7u-5ow "")、 [升降配节点资源](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-the-configurations-of-a-worker-node "")。<br>  <br>- 启用 [资源画像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/resource-profiling "")，获得容器requests/limits的推荐配置。 |

更多OOM现象出现的原因及解决方案，请参见 [出现OOM Killer的原因及解决方案](https://help.aliyun.com/zh/alinux/support/causes-of-and-solutions-to-the-issue-of-oom-killer-being-triggered#section-v6c-lau-22i "")。

### **Terminating**

| **可能原因** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **可能原因** | **说明** | **推荐的解决方案** |
| 节点存在异常，处于NotReady状态。 | 处于NotReady状态的节点恢复正常后会被自动删除。 |
| Pod配置了Finalizers。 | 如果Pod配置了Finalizers，Kubernetes会在删除Pod之前执行Finalizers指定的清理操作。如果相关的清理操作没有正常响应，Pod将保持在Terminating状态。 | 通过`kubectl get pod -n <ns> <pod name> -o yaml`查看Pod的Finalizers配置，进一步排查异常原因。 |
| Pod的preStop配置异常。 | 如果Pod配置了preStop，Kubernetes会在容器被终止之前执行preStop指定的操作。Pod正处于终止流程的preStop阶段时，Pod将处于Terminating状态。 | 通过`kubectl get pod -n <ns> <pod name> -o yaml`查看Pod的preStop配置，进一步排查异常原因。 |
| Pod配置了优雅退出时间。 | 如果Pod配置了优雅退出时间（`terminationGracePeriodSeconds`），Pod收到终止命令后（例如`kubectl delete pod <pod_name>`命令）会进入Terminating状态。等待`terminationGracePeriodSeconds`设定的时间后，或容器提前退出后，Kubernetes才认为Pod已经成功关闭。 | 等待容器优雅退出后，Kubernetes将自动删除Pod。 |
| 容器无响应。 | 发起停止或删除Pod的请求后，Kubernetes会向Pod内的容器发送`SIGTERM`信号。如果容器在终止过程中没有正确响应`SIGTERM`信号，Pod可能会停留在Terminating状态。 | 1. 使用`kubectl delete pod <pod-name> --grace-period=0 --force`强制删除，释放Pod资源。<br>   <br>2. 检查Pod所在节点的containerd或Docker日志，进一步进行排查。 |

### **Evicted**

| **可能原因** | **说明** | **推荐的解决方案** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **可能原因** | **说明** | **推荐的解决方案** |
| 节点存在资源压力，包括内存不足、磁盘空间不足等，引发kubelet主动驱逐节点上的一个或者多个Pod，以回收节点资源。 | 可能存在内存压力、磁盘压力、Pid压力等。<br>- 通过`kubectl describe node <node name> | grep Taints`命令查询，显示如下内容。<br>  <br>  - 内存压力：带有污点`node.kubernetes.io/memory-pressure`。<br>    <br>  - 磁盘压力：带有污点`node.kubernetes.io/disk-pressure`。<br>    <br>  - Pid压力：带有污点`node.kubernetes.io/pid-pressure`。<br>- Pod状态如下：<br>  <br>  - `Evicted`。<br>    <br>  - `ContainerStatusUnknown`，且Pod YAML中的`reason`字段显示`Evicted`。 | - 内存压力：<br>  <br>  - 根据自身业务情况，调整Pod的资源配置， [管理容器组（Pod）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/manage-pods#section-pha-i7u-5ow "")。<br>    <br>  - 升配节点，请参见 [升降配节点资源](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-the-configurations-of-a-worker-node#task-895194 "")。<br>- 磁盘压力：<br>  <br>  - 定时清理节点上的业务Pod日志，防止磁盘空间被耗尽。<br>    <br>  - 为节点进行磁盘扩容，请参见 [步骤一：扩容云盘容量](https://help.aliyun.com/zh/ecs/user-guide/step-1-resize-a-disk-to-extend-its-capacity#concept-syg-jxz-2hb "")。<br>- Pid压力：根据自身业务情况，调整Pod的资源配置，请参见 [进程ID约束与预留](https://kubernetes.io/docs/concepts/policy/pid-limiting/)。 |
| 发生了非预期的驱逐行为。 | 待运行Pod的节点被手动打上了NoExecute的污点，导致出现非预期的驱逐行为。 | 通过`kubectl describe node <node name> | grep Taints`命令检查节点是否被打上了NoExecute污点。如是，请删除。 |
| 未按照预期流程执行驱逐。 | - `--pod-eviction-timeout`：当节点宕机时间超过设置时间后，开始驱逐宕机节点上的Pod，默认为5min。<br>  <br>- `--node-eviction-rate`：每秒从节点上驱逐的Pod数量。默认为0.1，即每10s至多从一个节点上驱逐Pod。<br>  <br>- `--secondary-node-eviction-rate`：第二档的节点驱逐速率。当集群中宕机节点过多时，节点驱逐速率会降低至第二档，默认值为0.01。<br>  <br>- `--unhealthy-zone-threshold`：可用区的不健康阈值，默认为0.55，即当宕机的节点数量超过总节点数的55%时，该可用区被判定为不健康。<br>  <br>- `--large-cluster-size-threshold`：集群的大规模阈值，默认为50，即当集群节点数量超过50时判定集群为大规模集群。 | 在小规格的集群（集群节点数小于等于50个节点）中，如果故障的节点大于总节点数的55%，实例的驱逐会被停止，更多信息请参见 [节点驱逐速率限制](https://kubernetes.io/docs/concepts/architecture/nodes/#rate-limits-on-eviction)。 |
| 在大规模集群中（集群节点数大于50），如果集群中不健康的节点数量占总节点数的比例超过了预设的阈值`--unhealthy-zone-threshold`（默认为0.55），驱逐速率由`--secondary-node-eviction-rate`控制（代表每分钟驱逐节点上Pod的最大比例），默认值为0.01。更多信息，请参见 [节点驱逐速率限制](https://kubernetes.io/docs/concepts/architecture/nodes/#rate-limits-on-eviction)。 |
| 容器被驱逐后仍然频繁调度到原节点。 | 节点驱逐容器时会根据节点的资源使用率进行判断，而容器的调度规则是根据节点上的“资源分配量”进行判断，被驱逐的Pod有可能被再次调度到这个节点，从而出现频繁调度到原节点的现象。 | 根据集群节点的可分配资源检查Pod的资源Request请求配置是否合理。如需调整，请参见 [设置容器的CPU和内存资源上下限](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/manage-pods#section-pha-i7u-5ow "")。可启用 [资源画像](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/resource-profiling "")，获得容器Request和Limit的推荐配置。 |

### **Completed**

Completed状态下，Pod中容器的启动命令已执行完毕，容器中的所有进程均已成功退出。Completed状态通常适用于Job、Init容器等。

## **常见问题**

#### **Pod状态为Running但没正常工作**

如果业务YAML存在问题，Pod可能会处于Running状态但没有正常工作。可参见以下流程解决。

1. 查看Pod的配置，确定Pod中容器的配置是否符合预期。

2. 使用以下方法，排查YAML配置中的某一个Key是否存在拼写错误。

创建Pod时，如果YAML中的某个Key拼写错误（例如将`command`拼写为`commnd`），集群会忽略该错误并使用该YAML成功创建资源。但在容器运行过程中，系统无法执行YAML文件中指定的命令。

下文以`command`拼写成`commnd`为例，介绍拼写问题的排查方法。

1. 在执行`kubectl apply -f`命令前为其添加`--validate`，然后执行`kubectl apply --validate -f XXX.yaml`命令。



      如拼写存在错误，会提示报错`XXX] unknown field: commnd XXX] this may be a false alarm, see https://gXXXb.XXX/6842pods/test`。

2. 执行以下命令，将输出结果的pod.yaml与创建Pod使用的YAML进行对比。



      **说明**





      `[$Pod]`为异常Pod的名称，可通过`kubectl get pods`命令查看。



















      ```bash
        kubectl get pods [$Pod] -o yaml > pod.yaml
      ```



      - pod.yaml文件比创建Pod所使用的文件行数更多，表明已创建的Pod符合预期。

      - 如创建Pod的YAML代码行不存在于pod.yaml文件中，表明YAML中存在拼写问题。
3. 查看Pod的日志，通过日志内容排查问题。

4. 通过终端进入容器，查看容器内的本地文件是否符合预期。


#### **如何使用kubectl查看节点资源占用？**

1. 查看集群所有节点的CPU/内存占用情况。















```bash
kubectl describe nodes | awk '/^Name:/{print "\n"$2} /Resource +Requests +Limits/{print $0} /^[ \t]+cpu.*%/{print $0} /^[ \t]+memory.*%/{print $0}'
```



预期输出：















```bash
cn-hangzhou.192.168.0.xxx
     Resource           Requests      Limits
     cpu                1725m (44%)   10320m (263%)
     memory             1750Mi (11%)  16044Mi (109%)

cn-hangzhou.192.168.16.xxx
     Resource           Requests      Limits
     cpu                1885m (48%)   16820m (429%)
     memory             2536Mi (17%)  25760Mi (179%)
```



Requests占比较高的节点可能无法满足新Pod的`requests`需求从而无法进行调度。

2. 将`YOUR_NODE_NAME`替换成实际的节点名称，查看该节点所有Pod资源占用情况。















```bash
kubectl describe node YOUR_NODE_NAME | awk '/Non-terminated Pods/,/Allocated resources/{ if ($0 !~ /Allocated resources/) print }'
```



预期输出：















```bash
Non-terminated Pods:          (11 in total)
     Namespace                   Name                                                        CPU Requests  CPU Limits   Memory Requests  Memory Limits  Age
     ---------                   ----                                                        ------------  ----------   ---------------  -------------  ---
     arms-prom                   node-exporter-gp95p                                         20m (0%)      1020m (26%)  160Mi (1%)       1152Mi (7%)    6d21h
     csdr                        csdr-velero-77c8bbc9c7-w46lq                                500m (12%)    1 (25%)      128Mi (0%)       2Gi (13%)      6d19h
     kube-system                 ack-cost-exporter-5b647ffc65-zdrsl                          100m (2%)     1 (25%)      200Mi (1%)       1Gi (6%)       6d21h
     kube-system                 ack-node-local-dns-admission-controller-5dfd74f5f4-9rl6n    100m (2%)     1 (25%)      100Mi (0%)       1Gi (6%)       6d21h
     kube-system                 ack-node-problem-detector-daemonset-6wql2                   200m (5%)     1200m (30%)  300Mi (2%)       1324Mi (9%)    6d21h
     kube-system                 coredns-7784559f6-dr9sn                                     100m (2%)     0 (0%)       100Mi (0%)       2Gi (13%)      6d21h
     kube-system                 csi-plugin-knz7j                                            130m (3%)     2 (51%)      176Mi (1%)       4Gi (27%)      6d21h
     kube-system                 kube-proxy-worker-rkbzv                                     100m (2%)     0 (0%)       100Mi (0%)       0 (0%)         6d21h
     kube-system                 loongcollector-ds-kw7cj                                     100m (2%)     2 (51%)      256Mi (1%)       2Gi (13%)      6d21h
     kube-system                 node-local-dns-pgzcn                                        25m (0%)      0 (0%)       30Mi (0%)        1Gi (6%)       6d21h
     kube-system                 terway-eniip-lnn8n                                          350m (8%)     1100m (28%)  200Mi (1%)       256Mi (1%)     6d21h
```



业务应用可依据实际资源消耗情况，调整`requests`配置项。


#### **Pod访问数据库概率性网络中断**

针对ACK集群中Pod访问数据库有概率性网络中断的问题，可以按照以下步骤进行排查。

##### **1、检查Pod**

- 查看目标集群中该Pod的事件记录，检查是否存在连接不稳定的异常事件，例如网络异常、重启事件、资源不足等。

- 查看Pod的日志输出，确定是否有与数据库连接相关的错误信息，例如超时、认证失败或者重连机制触发等。

- 查看Pod的CPU和内存使用情况，避免资源耗尽导致应用程序或数据库驱动程序异常退出。

- 查看Pod的资源Request和Limit配置，确保Pod分配了足够的CPU和内存资源。


##### **2、检查节点**

- 查看节点的资源使用情况，确认是否有内存、磁盘等资源不足等情况。具体操作，请参见 [监控节点](https://help.aliyun.com/zh/ack/monitor-nodes "")。

- 测试节点与目标数据库之间是否出现概率性网络中断。


##### **3、检查数据库**

- 检查数据库的状态和性能指标，是否出现重启或性能瓶颈。

- 查看异常连接数和连接超时设置，并根据业务需求进行调整。

- 检查数据库日志是否有相关断开连接的记录。


##### **4、检查集群组件状态**

集群组件异常会影响Pod与集群内其他组件的通信。使用如下命令，检查ACK集群组件状态。

```bash
kubectl get pod -n kube-system  # 查看组件Pod状态。
```

同时检查网络组件：

- CoreDNS组件：检查组件状态和日志，确保Pod能正常解析数据库服务的地址。

- Flannel插件：查看kube-flannel组件的状态和日志。

- Terway插件：查看terway-eniip组件的状态和日志。


##### **5、分析网络流量**

可使用 `tcpdump` 来抓包并分析网络流量，以帮助定位问题的原因。

1. 获取Pod信息与节点信息：

使用以下命令获取指定命名空间中的Pod信息及其所在节点：















```bash
kubectl  get pod -n [namespace] -o wide
```

2. 登录到目标节点，使用以下命令查看容器PID。






containerd（1.22以上集群）



Docker（1.22及以下集群）



















1. 执行以下命令查看容器`CONTAINER`。















      ```bash
      crictl ps |grep <Pod名称关键字>
      ```



      预期输出：















      ```shell
      CONTAINER           IMAGE               CREATED             STATE
      a1a214d2*****       35d28df4*****       2 days ago          Running
      ```

2. 使用`CONTAINER ID`参数，执行以下命令查看容器PID















      ```bash
      crictl inspect a1a214d2***** |grep -i PID
      ```



      预期输出：















      ```bash
          "pid": 2309838,    # 目标容器的PID进程号。
                  "pid": 1
                  "type": "pid"
      ```


1. 执行以下命令查看容器`CONTAINER ID`。















      ```bash
      docker ps |grep <pod名称关键字>
      ```



      预期输出：















      ```bash
      CONTAINER ID        IMAGE                  COMMAND
      a1a214d2*****       35d28df4*****          "/nginx
      ```

2. 使用`CONTAINER ID`参数，执行以下命令查看容器PID。















      ```bash
      docker inspect  a1a214d2***** |grep -i PID
      ```



      预期输出：















      ```bash
                  "Pid": 2309838,  # 目标容器的PID进程号。
                  "PidMode": "",
                  "PidsLimit": null,
      ```


3. 执行抓包命令。

使用获取到的容器PID，执行以下命令，捕获Pod与目标数据库之间的网络通信数据包。















```bash
nsenter -t <容器PID> tcpdump -i any -n -s 0 tcp and host <数据库IP地址>
```



使用获取到的容器PID，执行以下命令，捕获Pod与宿主机之间的网络通信数据包。















```bash
nsenter -t <容器PID> tcpdump -i any -n -s 0 tcp and host <节点IP地址>
```



执行以下命令，捕获宿主机与数据库之间的网络通信数据包。















```bash
tcpdump -i any -n -s 0 tcp and host <数据库IP地址>
```


##### **6、优化业务应用程序**

- 在业务应用程序中实现数据库连接的自动重连机制，确保数据库发生切换或迁移时，应用程序能够自动恢复连接，无需人工干预。

- 使用持久化的长连接而非短连接来与数据库通信。长连接能显著降低性能损耗和资源消耗，提高系统整体效率。


#### **常用排查界面**

可登录[容器服务管理控制台](https://cs.console.aliyun.com/)，进入集群的详情页面，排查Pod可能存在的问题。

| **操作** | **控制台界面** |
| --- | --- |

|     |     |
| --- | --- |
| **操作** | **控制台界面** |
| 检查Pod的状态 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。<br>   <br>2. 在 **容器组** 页面左上角选择Pod所在的 **命名空间**，查看Pod状态。<br>   <br>   - 若状态为Running，表明Pod运行正常。<br>     <br>   - 若状态不为Running，表明Pod状态异常，请参见本文处理。 |
| 检查Pod的基础信息 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。<br>   <br>2. 在 **容器组** 页面左上角选择Pod所在的 **命名空间**，然后单击目标Pod名称或者目标Pod右侧操作列下的详情，查看Pod的名称、镜像、Pod IP、所在节点等详细信息。 |
| 检查Pod的配置 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。<br>   <br>2. 在 **容器组** 页面左上角选择Pod所在的 **命名空间**，然后单击目标Pod名称或者目标Pod右侧操作列下的详情。<br>   <br>3. 在Pod详情页面右上角单击 **YAML 编辑**，查看Pod的YAML文件和详细配置。 |
| 检查Pod的事件 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。<br>   <br>2. 在 **容器组** 页面左上角选择Pod所在的 **命名空间**，然后单击目标Pod名称或者目标Pod右侧操作列下的详情。<br>   <br>3. 在Pod详情页面下方单击 **事件** 页签，查看Pod的事件。<br>   <br>   <br>   <br>   **说明**<br>   <br>   <br>   <br>   <br>   <br>   Kubernetes默认保留最近1小时的事件，若需保存更长时间的事件，请参见 [创建并使用K8s事件中心](https://help.aliyun.com/zh/sls/create-and-use-an-event-center#task-2389213 "")。 |
| 查看Pod的日志 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。<br>   <br>2. 在 **容器组** 页面左上角选择Pod所在的 **命名空间**，然后单击目标Pod名称或者目标Pod右侧操作列下的详情。<br>   <br>3. 在Pod详情页面下方单击 **日志** 页签，查看Pod的日志。<br>   <br>**说明**<br>ACK集群集成了日志服务SLS。可在集群中启用SLS，快速采集集群的容器日志，请参见 [采集ACK集群容器日志](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/collect-text-logs-from-ack-clusters-using-daemonset-deployed-logtail-agents "")。 |
| 检查Pod的监控 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**运维管理** \> **Prometheus 监控**。<br>   <br>2. 在 **Prometheus 监控** 页面，单击 **集群监控概览** 页签，选择查看Pod的CPU、内存、网络I/O等监控大盘。<br>   <br>**说明**<br>ACK集群集成了阿里云Prometheus。可在集群中快速启用阿里云Prometheus，以实时监控集群和容器的健康状况，并查看可视化的Grafana监控数据大盘，请参见 [接入与配置阿里云Prometheus监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-managed-service-for-prometheus-to-monitor-an-ack-cluster "")。 |
| 使用终端进入容器，进入容器内部查看本地文件等信息 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。<br>   <br>2. 在 **容器组** 页面，单击目标容器组右侧 **操作** 列下的 **终端**。 |
| 启用Pod故障诊断 | 1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。<br>   <br>2. 在 **容器组** 页面，单击目标容器组右侧 **操作** 列下的 **诊断**，对该容器组进行故障诊断，根据诊断结果解决问题。<br>   <br>**说明**<br>容器智能运维平台提供了一键故障诊断能力，辅助定位集群中出现的问题，请参见 [使用集群诊断](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-cluster-diagnostics/ "")。 |

#### **集群中的Pod被异常删除**

**问题现象及原因**：集群里 Completed 的 Pod 数量较多时，KCM（kube-controller-manager）为了避免无用的 Pod 数量过多，影响各类控制器效率，会在数量超过12500个后清理一下无用的 Pod。具体对应的 KCM 配置参数为`--terminated-pod-gc-threshold`，请参考社区 [KCM 参数文档](https://kubernetes.io/zh-cn/docs/reference/command-line-tools-reference/kube-controller-manager/)。

**处理建议**：定期清理集群中Completed状态的Pod，防止数量过多，影响各类控制器效率。