### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/scheduling-overview/)[QoS感知调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/qos-aware-scheduling/)启用CPU Burst性能优化策略

# 启用CPU Burst性能优化策略

更新时间：2025-08-22 00:09:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用负载感知调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-load-aware-pod-scheduling)[下一篇：启用CPU拓扑感知调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/topology-aware-cpu-scheduling)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

为什么需要启用CPU Burst

功能优势

使用场景

费用说明

前提条件

配置说明

操作步骤

验证步骤

结果分析

高级参数配置

FAQ

当前已通过ack-slo-manager的旧版本协议使用了CPU Burst功能，升级为ack-koordinator后是否继续支持？

开启CPU Burst配置后，为什么Pod仍有CPU Throttled现象出现？

开启CPU Burst策略是否必须使用Alibaba Cloud Linux操作系统？

开启 CPU Burst 后，为什么应用内部代码获取到的线程数会变化？

相关文档

受CPU Limit约束，容器在运行过程中可用的CPU资源会受到限制，当真实用量触发上限时，内核会对其限流（Throttling），进而导致服务质量受损。CPU Burst功能能够动态感知CPU Throttled现象并对容器参数进行自适应调节。在出现突发负载时，CPU Burst可以为容器临时提供额外的CPU资源，缓解CPU限制带来的性能瓶颈，以保障并提升应用（尤其是延迟敏感型应用）的服务质量。

**说明**

为了帮助您更好地理解本文档并使用本功能，推荐您提前了解 [CFS Scheduler](https://docs.kernel.org/scheduler/sched-design-CFS.html)、 [节点CPU管理策略](https://kubernetes.io/docs/tasks/administer-cluster/cpu-management-policies/) 等相关概念。

## 为什么需要启用CPU Burst

Kubernetes集群使用CPU Limit资源约束机制，用于限制容器可以使用的最大CPU资源量，以确保了多个容器之间的资源分配的公平性，防止某个容器过度消耗CPU资源，从而影响其他容器的性能。

CPU是一种分时复用型资源，即多个进程或容器可以共享一个CPU时间片。容器配置了CPU Limit后，操作系统内核会根据CFS (Completely Fair Scheduler) 来控制容器在每个时间周期内（`cpu.cfs_period_us`）的CPU使用量（`cpu.cfs_quota_us`）。例如，如果一个容器的CPU Limit = 4，操作系统内核会限制该容器在每段时间周期内（一个调度周期通常是100 ms）最多使用400 ms的CPU时间片。

### **功能优势**

CPU使用率是衡量容器运行状态的关键指标，集群管理员通常会参考该指标来配置容器的CPU Limit。相较于常用的秒级别指标，百毫秒级别下容器的CPU使用率往往呈现更为明显的毛刺特征，展示出更多瞬时变化。以下图为例，如果以秒级别为单位（紫色折线），CPU用量明显少于4核；而如果以毫秒级别为单位（绿色折线），那么容器CPU用量在部分时段会超出4核，若将CPU Limit配置为4核，就会导致线程因CPU限流而被操作系统挂起。

![原理说明](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9748369361/p369240.png)

下方图片展示了在一台4核节点上，一个CPU Limit = 2的Web服务容器在收到请求（req）后，各个线程（Thread）的CPU资源分配情况。左图为常规情况，右图为开启CPU Burst后的情况。

|     |     |
| --- | --- |
| 即使容器在最近1s内整体的CPU使用率较低，但受CPU限流的影响，Thread 2仍需要等待下一个时间周期才能继续将req 2处理完成，导致请求的响应时延（RT）变大。这是容器RT长尾问题的一个重要原因。![ack-slo-manager example.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9748369361/p369426.png) | 启用CPU Burst功能后，容器可以在空闲时积累一些CPU时间片，用于满足突发时的资源需求，进而可以提升容器性能，降低延迟指标。![CPU Burst.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0848369361/p369431.png) |

除了上述场景之外，CPU Burst还适用于容器CPU资源需求突增的场景。例如，当业务流量突然上涨时，ack-koordinator可以在保障整机负载水位安全的前提下，在秒级别内快速解决CPU的资源瓶颈。

**说明**

ack-koordinator的调节仅涉及节点cgroup参数中的`cfs quota`，并不会修改Pod Spec的CPU Limit字段。

### **使用场景**

CPU Burst功能的典型使用场景如下。

- 容器在大多数时间内CPU资源用量低于设置的CPU Limit，但容器CPU Throttled仍然时常出现，影响应用性能表现。开启CPU Burst可以让容器在突发负载时使用积累的时间片，有效解决CPU Throttled限流问题，提升应用服务质量。

- 容器应用在启动加载阶段CPU资源消耗较高，但在加载完成并进入稳定运行状态后，其CPU用量会降到一个较低且稳定的水平。开启CPU Burst后，您无需为容器配置过高的CPU Limit，即可让应用在启动阶段使用更多时间片，确保应用能够快速启动。


## 费用说明

ack-koordinator组件本身的安装和使用免费，但在以下场景中可能产生额外费用。

- ack-koordinator是非托管组件，安装后将占用Worker节点资源。您可以在安装组件时配置各模块的资源申请量。

- ack-koordinator默认会将资源画像、精细化调度等功能的监控指标以Prometheus的格式对外透出。若您配置组件时开启了 **ACK-Koordinator开启Prometheus监控指标** 选项并使用了阿里云Prometheus服务，这些指标将被视为 [自定义指标](https://help.aliyun.com/zh/arms/prometheus-monitoring/basic-metrics/ "") 并产生相应费用。具体费用取决于您的集群规模和应用数量等因素。建议您在启用此功能前，仔细阅读阿里云Prometheus [Prometheus 实例计费](https://help.aliyun.com/zh/arms/prometheus-monitoring/product-overview/billing-description/ "")，了解自定义指标的免费额度和收费策略。您可以通过 [用量查询](https://help.aliyun.com/zh/arms/prometheus-monitoring/product-overview/billing-and-usage-query "")，监控和管理您的资源使用情况。


## 前提条件

- 已创建ACK托管集群Pro版且集群版本为1.18及以上，请参见 [创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/ "")、 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。



**说明**





推荐使用Alibaba Cloud Linux作为操作系统，请参见 [开启CPU Burst策略是否必须使用Alibaba Cloud Linux操作系统？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cpu-burst#2913f4c823e4k "")。

- 已安装ack-koordinator组件，且组件版本为0.8.0及以上，请参见 [ack-koordinator](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#section-7sg-0ck-qmm "")。


## 配置说明

您可以通过Pod Annotation为指定的Pod开启CPU Burst功能，也可以通过ConfigMap在集群或命名空间维度开启。

通过Annotation为指定Pod开启

通过ConfigMap在集群维度开启

通过ConfigMap在Namespace维度开启

通过Pod YAML的`metadata`字段下配置CPU Burst策略的Annotation，针对指定Pod生效。

**说明**

如需在工作负载（例如Deployment）中配置，请在`template.metadata`字段下配置Pod对应的Annotation。

```yaml
annotations:
  # 设置为auto，开启该Pod的CPU Burst功能。
  koordinator.sh/cpuBurst: '{"policy": "auto"}'
  # 设置为none，关闭该Pod的CPU Burst功能。
  koordinator.sh/cpuBurst: '{"policy": "none"}'
```

通过ConfigMap配置的CPU Burst策略默认针对全集群生效。

1. 使用以下ConfigMap示例，创建configmap.yaml文件。















```yaml
apiVersion: v1
data:
     cpu-burst-config: '{"clusterStrategy": {"policy": "auto"}}'
     #cpu-burst-config: '{"clusterStrategy": {"policy": "cpuBurstOnly"}}'
     #cpu-burst-config: '{"clusterStrategy": {"policy": "none"}}'
kind: ConfigMap
metadata:
     name: ack-slo-config
     namespace: kube-system
```

2. 查看命名空间kube-system下是否存在ConfigMap`ack-slo-config`。

   - 存在：使用PATCH方式进行更新，避免干扰ConfigMap中其他配置项。















     ```bash
     kubectl patch cm -n kube-system ack-slo-config --patch "$(cat configmap.yaml)"
     ```

   - 不存在：执行以下命令进行创建ConfigMap。















     ```bash
     kubectl apply -f configmap.yaml
     ```

通过指定Namespace，为部分Pod配置CPU Burst策略时，针对指定命名空间生效。

1. 使用以下ConfigMap示例，创建configmap.yaml文件。















```yaml
apiVersion: v1
kind: ConfigMap
metadata:
     name: ack-slo-pod-config
     namespace: koordinator-system # 首次使用时需要先手动创建该Namespace。
data:
     # 单独开启或关闭部分Namespace的Pod。
     cpu-burst: |
       {
         "enabledNamespaces": ["allowed-ns"],
         "disabledNamespaces": ["blocked-ns"]
       }
     # 为allowed-ns命名空间下的所有Pod开启了CPU Burst策略，对应policy为auto。
     # 为blocked-ns命名空间下的所有Pod关闭了CPU Burst策略，对应policy为none。
```

2. 查看命名空间kube-system下是否存在ConfigMap`ack-slo-config`。

   - 存在：使用PATCH方式进行更新，避免干扰ConfigMap中其他配置项。















     ```bash
     kubectl patch cm -n kube-system ack-slo-config --patch "$(cat configmap.yaml)"
     ```

   - 不存在：执行以下命令创建ConfigMap。















     ```bash
     kubectl apply -f configmap.yaml
     ```

## 操作步骤

本示例以一个Web服务型应用为例，展示开启CUP Burst策略前后的访问延迟情况，验证CPU Burst策略带来的优化效果。

### **验证步骤**

1. 使用以下示例应用的YAML内容，创建名为apache-demo.yaml文件。

在Pod对象的`metadata`字段下配置Annotation，为Pod单独开启CPU Burst策略。















```yaml
apiVersion: v1
kind: Pod
metadata:
     name: apache-demo
     annotations:
       koordinator.sh/cpuBurst: '{"policy": "auto"}'   # 开启CPU Burst策略。
spec:
     containers:
  - command:
    - httpd
    - -D
    - FOREGROUND
    image: registry.cn-zhangjiakou.aliyuncs.com/acs/apache-2-4-51-for-slo-test:v0.1
    imagePullPolicy: Always
    name: apache
    resources:
      limits:
        cpu: "4"
        memory: 10Gi
      requests:
        cpu: "4"
        memory: 10Gi
nodeName: $nodeName # 修改为实际的节点名称。
hostNetwork: False
restartPolicy: Never
schedulerName: default-scheduler
```

2. 执行以下命令，部署Apache HTTP Server作为目标评测应用。















```bash
kubectl apply -f apache-demo.yaml
```

3. 使用wrk2压测工具发送请求。















```shell
# 下载wrk2开源测试工具并解压安装。具体操作，请参见https://github.com/giltene/wrk2。
# 当前在Apache镜像配置中开启了Gzip压缩模块，用于模拟服务端处理请求的计算逻辑。
# 执行发压命令，注意修改目标应用的IP地址。
./wrk -H "Accept-Encoding: deflate, gzip" -t 2 -c 12 -d 120 --latency --timeout 2s -R 24 http://$target_ip_address:8010/static/file.1m.test
```





**说明**





   - 修改命令中的目标地址为Apache Pod的IP地址。

   - 通过修改`-R`参数来调节发送端的QPS压力。


### **结果分析**

以下数据分别展示了Alibaba Cloud Linux和社区CentOS在CPU Burst策略开启前后的表现情况。

- 全部关闭表示CPU Burst策略为`none`。

- 全部开启表示CPU Burst策略为`auto`。


**重要**

以下数据仅为理论值，实际请以您的操作环境为准。

| **Alibaba Cloud Linux** | **全部关闭** | **全部开启** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **Alibaba Cloud Linux** | **全部关闭** | **全部开启** |
| apache RT-p99 | 107.37 ms | 67.18 ms（-37.4%） |
| CPU Throttled Ratio | 33.3% | 0% |
| Pod CPU平均利用率 | 31.8% | 32.6% |

| **CentOS** | **全部关闭** | **全部开启** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **CentOS** | **全部关闭** | **全部开启** |
| apache RT-p99 | 111.69 ms | 71.30 ms （-36.2%） |
| CPU Throttled Ratio | 33% | 0% |
| Pod CPU平均利用率 | 32.5% | 33.8% |

由以上对比数据可知：

- 开启CPU Burst能力后，应用的RT指标的p99分位值有明显优化。

- 对开启CPU Burst能力后，CPU Throttled情况大幅减少，而同时Pod整体CPU利用率基本保持不变。


## **高级参数配置**

CPU Burst策略的高级配置参数支持在ConfigMap参数中配置，也支持在Pod Annotation中配置。对于同时在Pod Annotation和ConfigMap配置的参数，Pod Annotation配置优先级大于ConfigMap配置。如果Pod Annotation中没有对应配置，ack-koordinator会进一步参考Namespace维度的ConfigMap配置；如果Namespace维度也没有对应配置，ack-koordinator会以集群维度的ConfigMap配置为准。

配置示例如下。

```yaml
# ConfigMap ack-slo-config样例。
data:
cpu-burst-config: |
    {
      "clusterStrategy": {
        "policy": "auto",
        "cpuBurstPercent": 1000,
        "cfsQuotaBurstPercent": 300,
        "sharePoolThresholdPercent": 50,
        "cfsQuotaBurstPeriodSeconds": -1
      }
    }

# Pod Annotation样例。
koordinator.sh/cpuBurst: '{"policy": "auto", "cpuBurstPercent": 1000, "cfsQuotaBurstPercent": 300, "cfsQuotaBurstPeriodSeconds": -1}'
```

以下为CPU Burst策略的相关高级参数：

**说明**

**Annotation** 和 **ConfigMap** 两列分别代表是否允许通过Pod Annotation或ConfigMap进行配置。其中，![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png)代表支持，![错](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2479979171/p442273.png)代表不支持。

| **参数** | **类型** | **说明** | **Annotation** | **ConfigMap** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数** | **类型** | **说明** | **Annotation** | **ConfigMap** |
| `policy` | string | - `none`（默认值）：关闭CPU Burst策略，相关参数会被恢复为创建初始值。<br>  <br>- `cpuBurstOnly`：仅开启Alibaba Cloud Linux内核级别的CPU Burst弹性。<br>  <br>- `cfsQuotaBurstOnly`：仅开启CFS quota的自动弹性能力，支持所有内核版本。<br>  <br>- `auto`：自适应开启以上两种弹性能力，包括Alibaba Cloud Linux内核特性，以及CFS quota的自动弹性能力。 | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |
| `cpuBurstPercent` | int | 默认值为`1000`，单位为百分比。<br>Alibaba Cloud Linux内核级别的CPU Burst弹性，表示相较于CPU Limit，CPU Burst放大的百分比。对应Pod的cgroup参数`cpu.cfs_burst_us`。更多信息，请参见 [在cgroup v1接口开启CPU Burst功能](https://help.aliyun.com/zh/alinux/user-guide/enable-the-cpu-burst-feature-for-cgroup-v1#task-2108025 "")。<br>例如，按默认配置，`CPU Limit = 1`对应的`cpu.cfs_quota_us`为100,000，`cpu.cfs_burst_us`会放大10倍为1,000,000。 | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |
| `cfsQuotaBurstPercent` | int | 默认值为`300`，单位为百分比。<br>开启CFS quota弹性能力时，Pod的cgroup参数（`cpu.cfs_quota_us`）可上调的最大比例，默认为3倍。 | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |
| `cfsQuotaBurstPeriodSeconds` | int | 默认值为`-1`，表示不限制，单位为秒。<br>开启CFS quota弹性能力时，Pod可以按上限（`cfsQuotaBurstPercent`）持续消耗CPU的时间限制。单个Pod超出时限后，其已经上调的cgroup参数（`cpu.cfs_quota_us`）会被恢复为原始值，其他Pod不受影响。 | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |
| `sharePoolThresholdPercent` | int | 默认值为`50`，单位为百分比。<br>开启CFS quota弹性能力时，节点CPU使用率的安全水位阈值。超出阈值后，节点中所有已经上调的Pod的cgroup参数（`cpu.cfs_quota_us`）会被恢复为创建初始值。 | ![错](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2479979171/p442273.png) | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |

**说明**

- 当您开启CFS quota的自动调整时（`policy`设置为`cfsQuotaBurstOnly`或`auto`），Pod的CPU Limit在节点上对应的参数（`cpu.cfs_quota_us`）会随CPU Throttled情况而动态调整。

- 在对Pod进行压测时，建议您同时保持对Pod CPU用量的观察，或者临时关闭CFS quota的自动调整（`policy`设置为`cpuBurstOnly`或`none`），以便在生产环境保持更好的资源弹性。


## FAQ

### 当前已通过ack-slo-manager的旧版本协议使用了CPU Burst功能，升级为ack-koordinator后是否继续支持？

旧版本的Pod协议要求在Annotation中填写`alibabacloud.com/cpuBurst`，ack-koordinator对此旧版本协议完全兼容，您可将组件无缝升级至新版本。

**说明**

ack-koordinator对旧版本协议的兼容期限截止至2023年07月30日。强烈建议您将原协议资源字段及时升级到新版本。

ack-koordinator对各版本协议的适配如下。

| ack-koordinator **版本** | **alibabacloud.com协议** | **koordinator.sh协议** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| ack-koordinator **版本** | **alibabacloud.com协议** | **koordinator.sh协议** |
| ≥0.2.0 | 支持 | 不支持 |
| ≥0.8.0 | 支持 | 支持 |

### 开启CPU Burst配置后，为什么Pod仍有CPU Throttled现象出现？

通常会有以下几个原因，您可以参考以下说明进行调整。

- 配置格式错误，导致CPU Burst策略没有生效，请参见 [高级参数配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cpu-burst#3c6d6cc3147ne "") 修改并验证。

- CPU利用率达到`cfsQuotaBurstPercent`配置的上限时，由于CPU资源不足，仍会出现CPU Throttled现象。

建议您根据应用实际需求情况调整Reqeuest和Limit值。

- CPU Burst策略会调整Pod的两个cgroup参数：`cpu.cfs_quota_us`和`cpu.cfs_burst_us`，详情请参见 [高级参数配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cpu-burst#3c6d6cc3147ne "")。其中，`cpu.cfs_quota_us`在ack-koordinator感知到CPU Throttled后才会进行设置，存在少许延迟；而`cpu.cfs_burst_us`直接参考配置进行设置，效果更灵敏。

建议您搭配Alibaba Cloud Linux操作系统使用，效果更佳。

- CPU Burst策略在调整`cpu.cfs_quota_us`时会有保护机制，即整机安全水位阈值配置的`sharePoolThresholdPercent`。当整机利用率过高时，为了避免单个Pod产生更多干扰，`cpu.cfs_quota_us`会被重置为初始值。

建议您结合自身应用的实际情况，合理设置整机安全水位阈值，避免因整机利用率过高而影响应用性能。


### **开启CPU Burst策略是否必须使用Alibaba Cloud Linux操作系统？**

ack-koordinator的CPU Burst策略适用于所有Alibaba Cloud Linux及CentOS开源内核。推荐您使用Alibaba Cloud Linux操作系统。借助Alibaba Cloud Linux内核特性，ack-koordinator可以提供更加细粒度的CPU弹性管理机制。更多信息，请参见 [在cgroup v1接口开启CPU Burst功能](https://help.aliyun.com/zh/alinux/user-guide/enable-the-cpu-burst-feature-for-cgroup-v1#task-2108025 "")。

### 开启 CPU Burst 后，为什么应用内部代码获取到的线程数会变化？

这是因为 CPU Burst 的工作机制与某些应用获取系统资源的方式存在冲突。ack-koordinator 实现 CPU Burst 时，会动态调整容器底层的 cgroup 参数 `cpu.cfs_quota_us`。此值代表容器在当前调度周期内可用的CPU时间配额。ack-koordinator 会根据应用的负载情况，动态伸缩此配额。

许多应用（例如Java的 `Runtime.getRuntime().availableProcessors()`）会直接读取 `cpu.cfs_quota_us` 来推算可用的CPU核心数。因此，当CPU配额被动态调整时，应用获取到的核心数也随之变化，导致线程池大小等依赖此值的参数变得不稳定。

建议让应用依赖Pod中定义的、固定不变的 `limits.cpu` 值。

1. 注入环境变量：通过 `resourceFieldRef`，将 Pod 的 `limits.cpu` 值作为环境变量注入到容器中。















```yaml
env:
  - name: CPU_LIMIT
    valueFrom:
      resourceFieldRef:
        resource: limits.cpu
```

2. 修改应用代码：修改应用启动逻辑，使其优先读取 `CPU_LIMIT` 来计算和设置线程池大小。配置后，无论CPU Burst如何调整配额，应用都会基于一个稳定可靠的值来运行。


## 相关文档

Alibaba Cloud Linux为cgroup v1接口提供了CPU Burst功能。您可以在cgroup v1接口开启CPU Burst功能，并查询CPU Burst的统计数据，请参见 [在cgroup v1接口开启CPU Burst功能](https://help.aliyun.com/zh/alinux/user-guide/enable-the-cpu-burst-feature-for-cgroup-v1#task-2108025 "")。