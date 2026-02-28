### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[成本套件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-suite/)[成本优化](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-optimization-1/)资源画像

# 通过资源画像推荐容器规格配置

更新时间：2025-09-17 08:43:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：成本优化](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cost-optimization-1/)[下一篇：成本优化检查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/idle-resource-optimization)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件及注意事项

费用说明

资源画像介绍

通过控制台使用资源画像

步骤一：安装资源画像

步骤二：资源画像策略管理

步骤三：查看应用画像概览

步骤四：查看应用画像详情

步骤五：变更应用资源规格

通过命令行使用资源画像

步骤一：启用资源画像

步骤二：（可选）通过Prometheus查看结果

FAQ

资源画像的算法原理是什么？

资源画像对应用的类型有什么要求？

是否可以直接使用画像值来设置容器的Request和Limit？

自建Prometheus如何查看资源画像监控指标？

如何清理资源画像结果和规则？

如何授权子账号使用资源画像？

ACK为Kubernetes原生的工作负载提供了资源画像的能力，通过对资源使用量历史数据的分析，实现了容器粒度的资源规格推荐，可以有效简化为容器配置Request和Limit的复杂度。本文介绍如何通过控制台和命令行使用资源画像功能。

## 前提条件及注意事项

- 仅支持ACK托管集群Pro版，且满足以下条件：

  - 已安装ack-koordinator组件（原ack-slo-manager），且组件版本为v0.7.1及以上，请参见 [ack-koordinator](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#task-2172306 "")。

  - 已安装metrics-server组件，且组件版本为v0.3.8及以上。

  - 如果节点的容器运行时为containerd，且加入集群的时间早于2022年01月19日14:00，请重新加入节点或升级集群到最新版本。具体操作，请参见 [添加已有节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-existing-ecs-instances-to-an-ack-cluster "")、 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster#task-1664343 "")。
- 目前资源画像控制台已在成本套件中开放公测，可直接访问使用。

- 为了确保画像结果的准确性，建议开启工作负载的资源画像后观察等待1天以上，以便累积充足的数据。


## **费用说明**

ack-koordinator组件本身的安装和使用免费，但在以下场景中可能产生额外费用。

- ack-koordinator是非托管组件，安装后将占用Worker节点资源。可在安装组件时配置各模块的资源申请量。

- ack-koordinator默认会将资源画像、精细化调度等功能的监控指标以Prometheus的格式对外透出。若配置组件时开启了 **ACK-Koordinator开启Prometheus监控指标** 选项并使用了阿里云Prometheus服务，这些指标将被视为 [基础指标](https://help.aliyun.com/zh/arms/prometheus-monitoring/container-cluster-metrics "") 上报至阿里云Prometheus中。如果修改默认设置（例如默认存储时长），可能会产生额外费用。详情请参见 [可观测计费说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/observable-billing-description "")。


## **资源画像介绍**

Kubernetes为容器资源管理提供了资源请求（Request）的资源语义描述。当容器指定Request时，调度器会将其与节点的资源容量（Allocatable）进行匹配，决定Pod应该分配到哪个节点。容器的Request一般基于人工经验填写，管理员会参考容器的历史利用率情况、应用的压测表现，并根据线上运行情况的反馈持续调整。

但基于人工经验的资源规格配置模式存在以下局限性：

- 为了保障线上应用的稳定性，管理员通常会预留相当数量的资源Buffer来应对上下游链路的负载波动，容器的Request配置会远高于其实际的资源利用率，导致集群资源利用率过低，造成大量资源浪费。

- 当集群分配率较高时，为了提升集群资源利用率，管理员会主动缩小Request配置，协调更多的资源容量。该操作会提升容器的部署密度，当应用流量上涨时会影响集群的稳定性。


针对上述问题，ack-koordinator提供资源画像能力，实现容器粒度的资源规格推荐，降低容器配置的复杂性。ACK通过控制台提供了相应功能，便于应用管理员快速分析应用资源规格的合理性，按需进行资源规格配置的变更。同时，ACK还提供命令行的访问方式，支持通过CRD直接对应用资源画像进行管理。

## 通过控制台使用资源画像

### 步骤一：安装资源画像

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**成本套件** \> **成本优化**。

3. 在 **成本优化** 页面，单击 **资源画像** 页签，然后在 **资源画像** 区域，按照页面提示开启功能。

   - 组件安装或升级：按照页面提示安装或升级ack-koordinator组件。首次使用时，需要安装ack-koordinator组件。



     **说明**





     如ack-koordinator版本低于0.7.0，需进行迁移和升级。具体操作，请参见 [将ack-koordinator从应用市场迁移至组件中心](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#section-9yj-oaq-ilp "")。

   - 画像配置：首次使用时，在安装或升级完成后，可勾选启用 **默认配置** 控制资源画像的开启范围（推荐使用），也可后续在控制台中单击画像配置进行调整。
4. 单击 **开启画像**，进入 **资源画像** 页面。


### 步骤二：资源画像策略管理

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**成本套件** \> **成本优化**。

3. 在 **成本优化** 页面，单击 **资源画像** 页签，然后单击 **画像配置**。

画像配置分为 **全量配置** 和 **自动化运维配置** 两种模式，资源画像组件安装过程中推荐的默认配置为全量配置模式。可在此对配置模式和配置参数进行修改，并单击确定生效。






全量配置模式（推荐）



自动化运维配置模式



















全量配置模式将为所有工作负载开启资源画像，默认排除arms-prom和kube-system两个系统命名空间。



|     |     |     |
| --- | --- | --- |
| **配置项** | **说明** | **取值范围** |
| **排除的命名空间** | 不开启资源画像的命名空间，一般为系统组件对应的命名空间。最终开启范围为命名空间和负载类型的交集。 | 当前集群内已经存在的命名空间，支持多选，默认值为kube-system和arms-prom。 |
| **开启的负载类型** | 开启资源画像的负载类型范围。最终开启范围为命名空间和负载类型的交集。 | 支持K8s原生的三类工作负载，包括Deployment、StatefulSet和DaemonSet，支持多选。 |
| **CPU消耗冗余** | 生成资源画像参考的安全冗余水位，详见下文描述。 | 要求为非负数，提供三档常用的冗余度70%、50%、30%。 |
| **内存消耗冗余** | 生成资源画像参考的安全冗余水位，详见下文描述。 | 要求为非负数，提供三档常用的冗余度70%、50%、30%。 |



自定义配置模式仅开启一部分命名空间的工作负载，若集群规模较大（例如1000节点以上），或仅需试用开启一部分工作负载，可以通过自定义配置模式按需指定。



|     |     |     |
| --- | --- | --- |
| **配置项** | **说明** | **取值范围** |
| **开启的命名空间** | 开启资源画像的命名空间，最终开启范围为命名空间和负载类型的交集。 | 当前集群内已经存在的命名空间，支持多选。 |
| **开启的负载类型** | 开启资源画像的负载类型范围，最终开启范围为命名空间和负载类型的交集。 | 支持K8s原生的三类工作负载，包括Deployment、StatefulSet和DaemonSet，支持多选。 |
| **CPU消耗冗余** | 生成资源画像参考的安全冗余水位，详见下文描述。 | 要求为非负数，提供三档常用的冗余度（70%、50%、30%）。 |
| **内存消耗冗余** | 生成资源画像参考的安全冗余水位，详见下文描述。 | 要求为非负数，提供三档常用的冗余度（70%、50%、30%）。 |



资源消耗冗余：管理员在评估应用业务容量时（例如QPS），通常不会将物理资源使用到100%。这既包括超线程等物理资源的局限性，也包括应用自身需要保留部分资源以应对高峰时段的负载请求。当画像值与原始资源请求的差距超过安全冗余时，会提示降配建议，具体算法参见 [应用画像概览](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/resource-profiling#p-3je-czf-9kt "") 部分中有关画像建议的说明。![资源冗余](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6141483661/p494464.jpg)


### 步骤三：查看应用画像概览

资源画像的策略配置完成后，可在 **资源画像** 页面查看各工作负载的资源画像情况。

为提高画像结果准确性，首次使用时系统将提示需要至少累积24小时的数据。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1008358861/p687293.png)

画像总体概览以及各列的详细说明如下表所示。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9650658861/p687294.png)

**说明**

下表中，“-”代表不涉及。

| **列名** | **含义** | **取值说明** | **是否支持字段筛选** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **列名** | **含义** | **取值说明** | **是否支持字段筛选** |
| 工作负载名称 | 对应工作负载的名字（Name）。 | - | 支持。可在菜单栏顶部按名称进行精确查找。 |
| 命名空间 | 对应工作负载的名字（Namespace） | - | 支持。默认筛选条件中不包括kube-system命名空间。 |
| 工作负载类型 | 对应工作负载的类型。 | 包括Deployment、DaemonSet和StatefulSet三种类型。 | 支持。默认筛选条件为全部。 |
| CPU请求 | 工作负载Pod的CPU资源申请量（Request）。 | - | 不支持。 |
| 内存请求 | 工作负载Pod的内存资源申请量。 | - | 不支持。 |
| 画像数据状态 | 工作负载资源画像。 | - 收集中：资源画像刚创建，累积的数据较少，首次使用时建议至少等待一天以上，确保工作负载稳定运行一段时间，完整覆盖了流量的波峰波谷之后再使用。<br>  <br>- 正常：资源画像结果已经生成。<br>  <br>- 工作负载已删除：对应的工作负载已经删除，画像结果将在保留一段时间后自动删除。 | 不支持。 |
| CPU画像、内存画像 | 资源画像针对工作负载原始的资源请求量给出的规格（Request）调整建议，建议参考了资源画像值、原始资源请求量（Request）以及画像策略配置的资源消耗冗余，详见下文描述。 | 包括升配、降配以及保持三种。对应的百分比为偏差幅度。计算公式为：请求值∣画像值−请求值∣​。 | 支持，默认筛选条件包括升配和降配。 |
| 创建时间 | 画像结果的创建时间。 | - | 不支持。 |
| 资源变配 | 评估画像结果和改配建议后，单击 **资源变配** 进行资源的升降配置。更多信息，请参见下文的 [步骤五：变更应用资源规格](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/resource-profiling#p-wcg-uj4-h8z "")。 | - | 不支持。 |

ACK资源画像会为工作负载的每个容器资源规格生成画像值，通过对比画像值（Recommend）、原始资源请求量（Request），以及画像配置的资源消耗冗余（Buffer）。资源画像控制台会为工作负载生成操作的提示，例如对资源请求提高或降低（即升配或降配）。若工作负载有多个容器，则会提示偏差幅度最大的容器，具体计算原理如下。

- 画像值（Recommend）大于原始资源请求量（Request）：表示容器长期处于资源超用状态（使用量大于申请量），存在稳定性风险，应及时提高资源规格，控制台提示“建议升配”。


- 画像值（Recommend）小于原始资源请求量（Request）：表示容器可能有一定程度的资源浪费，可以降低资源规格，需要结合画像配置的资源消耗冗余进行判断，详情如下：

1. 根据画像值和配置的资源消耗冗余，计算目标资源规格（Target）：`Target = Recommend * (1 + Buffer)` **。**

2. 计算目标资源规格（Target）与原始资源请求量（Request）的偏离程度（Degree）：`Degree = 1 - Request / Target` **。**

3. 根据画像值以及偏离程度（Degree）的水位，生成CPU和内存建议的提示操作，若偏离程度（Degree）的绝对值大于0.1，则提示建议降配信息。
- 针对其他情况，资源画像为应用资源规格建议的提示为 **保持**，表示可以暂时不调整。


### 步骤四：查看应用画像详情

在 **资源画像** 页面，单击工作负载名称，进入对应的画像详情页面。

详情页包括三部分功能：工作负载基本信息、各容器的画像详情资源曲线、针对应用进行资源规格变更窗口。![应用画像详情](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7141483661/p494483.jpg)

如上图所示，以CPU为例，画像详情资源曲线中各项指标的含义如下。

| **曲线名称** | **含义** |
| --- | --- |

|     |     |
| --- | --- |
| **曲线名称** | **含义** |
| cpu limit | 容器的CPU资源限制值。 |
| cpu request | 容器的CPU资源请求值。 |
| cpu recommend | 容器的CPU资源画像值。 |
| cpu usage（average） | 对应工作负载内，各容器副本CPU使用量的平均值。 |
| cpu usage（max） | 对应工作负载内，各容器副本CPU使用量的最大值。 |

### 步骤五：变更应用资源规格

1. 在应用画像详情页面底部的 **资源变配** 区域，根据画像生成的画像值修改各容器的资源规格。

各列含义如下：![资源变更](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8877548861/p494497.png)




| **配置项** | **含义** |
| --- | --- |



|     |     |
| --- | --- |
| **配置项** | **含义** |
| 当前所需资源 | 容器当前填写的资源请求量（Request）。 |
| 当前限制资源 | 容器当前填写的资源限制量（Limit）。 |
| 画像值 | 资源画像为容器生成的画像值，可作为资源请求量（Request）的参考值。 |
| 安全冗余 | 资源画像策略管理中配置的安全冗余，可作为目标所需资源的参考值，例如在画像值的基础上累加冗余系数（如上图4.742 \* 1.3 ≈ 6.2）。 |
| 目标所需资源 | 容器资源请求量（Request）计划调整的目标值。 |
| 目标限制资源 | 容器资源限制量（Limit）计划调整的目标值。注意，若工作负载使用了CPU拓扑感知调度，CPU资源的限制需要配置为整数。 |

2. 配置完成后，单击 **提交**，将执行资源规格更新操作并自动跳转到工作负载详情页。

资源规格更新后，控制器会对工作负载进行滚动更新并重新创建Pod。


## 通过命令行使用资源画像

### 步骤一：启用资源画像

1. 使用以下YAML内容，创建`recommendation-profile.yaml`文件，开启工作负载的资源规格画像。



创建RecommendationProfile CRD，可以开启工作负载的资源画像，并获取容器的资源规格画像数据。RecommendationProfile CRD支持通过命名空间（Namespace）以及工作负载类型控制开启范围，开启范围为二者的交集。

















```yaml
apiVersion: autoscaling.alibabacloud.com/v1alpha1
kind: RecommendationProfile
metadata:
     # 对象名称，nonNamespaced类型不需指定命名空间。
     name: profile-demo
spec:
     # 开启资源画像的工作负载类型。
     controllerKind:
  - Deployment
# 开启资源画像的命名空间范围。
enabledNamespaces:
  - default
```

各项配置字段含义如下：

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `metadata.name` | String | 对象的名称。若RecommendationProfile为nonNamespaced类型，则无需指定命名空间。 |
| `spec.controllerKind` | String | 开启资源画像的工作负载类型。支持的工作负载类型包括Deployment、StatefulSet和DaemonSet。 |
| `spec.enabledNamespaces` | String | 开启资源画像的命名空间范围。 |

2. 为目标应用开启资源画像。















```bash
kubectl apply -f recommendation-profile.yaml
```

3. 使用以下YAML内容，创建`cpu-load-gen.yaml`文件。















```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
     name: cpu-load-gen
     labels:
       app: cpu-load-gen
spec:
     replicas: 2
     selector:
       matchLabels:
         app: cpu-load-gen-selector
     template:
       metadata:
         labels:
           app: cpu-load-gen-selector
       spec:
         containers:
      - name: cpu-load-gen
        image: registry.cn-zhangjiakou.aliyuncs.com/acs/slo-test-cpu-load-gen:v0.1
        command: ["cpu_load_gen.sh"]
        imagePullPolicy: Always
        resources:
          requests:
            cpu: 8 # 该应用的CPU请求资源为8核。
            memory: "1Gi"
          limits:
            cpu: 12
            memory: "2Gi"
```

4. 通过cpu-load-gen.yaml部署cpu-load-gen应用。















```bash
kubectl apply -f cpu-load-gen.yaml
```

5. 获取资源规格画像结果。















```bash
kubectl get recommendations -l \
     "alpha.alibabacloud.com/recommendation-workload-apiVersion=apps-v1, \
     alpha.alibabacloud.com/recommendation-workload-kind=Deployment, \
     alpha.alibabacloud.com/recommendation-workload-name=cpu-load-gen" -o yaml
```



ack-koordinator为每个开启资源画像的工作负载生成对应的资源规格画像，并将结果保存在Recommendation CRD中。名为`cpu-load-gen`的工作负载资源规格画像结果示例如下。















```yaml
apiVersion: autoscaling.alibabacloud.com/v1alpha1
kind: Recommendation
metadata:
     labels:
       alpha.alibabacloud.com/recommendation-workload-apiVersion: apps-v1
       alpha.alibabacloud.com/recommendation-workload-kind: Deployment
       alpha.alibabacloud.com/recommendation-workload-name: cpu-load-gen
     name: f20ac0b3-dc7f-4f47-b3d9-bd91f906****
     namespace: recommender-demo
spec:
     workloadRef:
       apiVersion: apps/v1
       kind: Deployment
       name: cpu-load-gen
status:
     recommendResources:
       containerRecommendations:
    - containerName: cpu-load-gen
      target:
        cpu: 4742m
        memory: 262144k
      originalTarget: # 表示资源画像算法的中间结果，不建议直接使用。
       # ...
```

为了便于检索，Recommendation和工作负载的Namespace一致，同时在Label中保存了工作负载的API Version、类型以及名称，格式如下表所示。

| **Label Key** | **说明** | **示例** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **Label Key** | **说明** | **示例** |
| `alpha.alibabacloud.com/recommendation-workload-apiVersion` | 工作负载的API Version，由Kubernetes的Label规范约束，正斜线（/）将被替换为短划线（-）。 | apps-v1（替换前为apps/v1） |
| `alpha.alibabacloud.com/recommendation-workload-kind` | 对应的工作负载类型，例如Deployment、StatefulSet等。 | Deployment |
| `alpha.alibabacloud.com/recommendation-workload-name` | 工作负载名称，由Kubernetes的Label规范约束，长度不能超过63个字符。 | cpu-load-gen |

各容器的资源规格画像结果保存在`status.recommendResources.containerRecommendations`中，各字段含义如下表所示。

| **字段名称** | **含义** | **格式** | **示例** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **字段名称** | **含义** | **格式** | **示例** |
| `containerName` | 表示容器名称。 | string | cpu-load-gen |
| `target` | 表示资源规格画像结果，包括CPU和Memory两个维度。 | map\[ResourceName\]resource.Quantity | cpu: 4742m<br>memory: 262144k |
| `originalTarget` | 表示资源规格画像算法的中间结果，不建议直接使用。 | - | - |

**说明**

单个Pod画像的CPU最小值为0.025核，内存的最小值为250 MB。

通过对比目标应用（`cpu-load-gen`）中声明的资源规格和本步骤画像检测结果，以CPU为例，可以发现该容器的Request申请过大。可通过调小Request来节省集群资源容量。

| **类别** | **原始资源规格** | **资源画像规格** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **类别** | **原始资源规格** | **资源画像规格** |
| CPU | 8核 | 4.742核 |

### **步骤二：（可选）通过Prometheus查看结果**

ack-koordinator组件为资源画像结果提供了Prometheus查询接口，可通过ACK提供的Prometheus监控直接查看。

- 若首次使用该功能的大盘，请确保 **资源画像** 大盘已经升级到最新版本。关于升级的具体操作，请参见 [相关操作](https://help.aliyun.com/zh/prometheus/view-grafana-dashboards-1#title-bd9-r7y-ix4 "")。

通过ACK控制台Prometheus监控查看资源画像结果的具体操作如下：

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**运维管理** \> **Prometheus 监控**。

3. 在 **Prometheus监控** 页面，选择**成本分析/资源优化** \> **资源画像**。

     在 **资源画像** 页签，查看详细数据，包括容器的规格（Request）、容器实际的资源使用量（Usage）以及容器的资源规格画像值（Recommend）。更多信息，请参见 [使用阿里云Prometheus监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-managed-service-for-prometheus-to-monitor-an-ack-cluster#task-2461398 "")。
- 如果自建了Prometheus监控，请参考以下监控项来配置大盘。















```bash
# 指定工作负载中容器的CPU资源规格画像。
koord_manager_recommender_recommendation_workload_target{exported_namespace="$namespace", workload_name="$workload", container_name="$container", resource="cpu"}
# 指定工作负载中容器的Memory资源规格画像。
koord_manager_recommender_recommendation_workload_target{exported_namespace="$namespace", workload_name="$workload", container_name="$container", resource="memory"}
```





**重要**





ack-koordinator组件提供的资源画像监控指标已于v1.5.0-ack1.14版本中更名为`koord_manager_recommender_recommendation_workload_target`，但同时对于更早版本中提供的资源画像监控指标`slo_manager_recommender_recommendation_workload_target`也仍然兼容。如果自建了Prometheus监控，建议在升级ack-koordinator组件至v1.5.0-ack1.14版本后将监控指标切换至`koord_manager_recommender_recommendation_workload_target`。


## FAQ

### 资源画像的算法原理是什么？

资源画像算法涉及一套多维度的数据模型，算法原理可以总结为以下几点：

- 资源画像算法会持续不断地收集容器的资源使用数据，计算CPU和内存使用量的采样峰值、加权平均、分位值等聚合统计值。

- 最终给出的画像结果中，将CPU的推荐值设置为P95分位值，将内存的推荐值设置为P99分位值，并为二者再加上一定的安全边际，以确保工作负载的可靠性。

- 针对时间这一因素进行了优化，画像算法只会参考最近14天内的数据，并通过半衰期滑动窗口模型进行聚合统计，旧的数据采样点权重会逐渐降低。

- 算法参考了容器出现OOM等运行状态信息，可以进一步提高画像值的准确性。


更多信息，请参见 [资源画像技术原理介绍](https://developer.aliyun.com/article/903090?spm=5176.28426678.J_HeJR_wZokYt378dwP-lLl.331.3d605181eMjHKm&scm=20140722.S_community@@%E6%96%87%E7%AB%A0@@903090._.ID_903090-RL_%E8%B5%84%E6%BA%90%E7%94%BB%E5%83%8F%E8%AE%A9%E5%AE%B9%E5%99%A8%E8%B5%84%E6%BA%90%E8%A7%84%E6%A0%BC%E7%9A%84%E5%A1%AB%E5%86%99%E4%B8%8D%E5%86%8D%E7%BA%A0%E7%BB%93-LOC_search~UND~community~UND~item-OR_ser-V_3-P0_0)、 [资源画像原理介绍及使用建议](https://developer.aliyun.com/article/1038925?spm=5176.28426678.J_HeJR_wZokYt378dwP-lLl.11.3d605181eMjHKm&scm=20140722.S_community@@%E6%96%87%E7%AB%A0@@1038925._.ID_1038925-RL_%E8%B5%84%E6%BA%90%E7%94%BB%E5%83%8F%E7%9C%8B%E5%BE%97%E8%A7%81%E7%9A%84%E5%AE%B9%E5%99%A8%E8%B5%84%E6%BA%90%E4%BC%98%E5%8C%96%E5%8A%A9%E6%89%8B-LOC_search~UND~community~UND~item-OR_ser-V_3-P0_0)。

### 资源画像对应用的类型有什么要求？

适合于在线服务类应用。

目前资源画像的结果优先考虑满足容器的资源需求，确保可以覆盖绝大部分数据样本。不过对于离线应用来说，这种批处理类型的任务更加关注整体的吞吐量，可以接受一定程度的资源竞争，以提高集群资源的整体利用率，画像结果对于离线应用来说会显得有些保守。此外，对于关键的系统组件，通常以“主备”的形式部署多个副本，处于“备份”角色的副本长期处于闲置状态，这些副本的资源用量样本也会对画像算法产生一定程度的干扰。针对以上场景，请对画像结果按需加工后再使用，建议持续关注资源画像的产品动态。

### 是否可以直接使用画像值来设置容器的Request和Limit？

需要结合业务自身特点来判断。资源画像提供的结果是对应用当前资源需求情况的总结，管理员应在画像值的基础上，结合应用特性加工后使用。

例如，为了应对流量高峰或实现“同城双活”的无缝切换，需要预留额外的资源冗余。此外，如果应用对资源较为敏感，无法在宿主机高负载下平稳运行，也应在画像值的基础上适当调高规格。

### 自建Prometheus如何查看资源画像监控指标？

资源画像的相关监控指标会在ack-koordinator组件的ack-koord-manager模块以Prometheus的格式提供HTTP接口。可执行以下命令获取Pod IP，并访问查看指标数据。

1. 获取Pod IP地址















   ```bash
   kubectl get pod -A -o wide | grep koord-manager
   ```



   预期输出：















   ```bash
   kube-system    ack-koord-manager-b86bd47d9-92f6m                                 1/1     Running     0               16h     10.10.0.xxx   cn-hangzhou.10.10.0.xxx   <none>           <none>
   kube-system    ack-koord-manager-b86bd47d9-vg5z7                                 1/1     Running     0               16h     10.10.0.xxx   cn-hangzhou.10.10.0.xxx   <none>           <none>
   ```

2. 执行以下命令查看指标数据（注意ack-koord-manager是双副本主备模式，数据只会在主副本Pod中提供），其中端口`port`（默认9326）请参考ack-koord-manager应用的Deployment配置。


   > 请确保当前执行命令的服务器与集群的容器网络互通。
















   ```bash
   curl -s http://10.10.0.xxx:9326/all-metrics | grep slo_manager_recommender_recommendation_workload_target
   # 若使用较低版本ack-koordinator组件（v1.5.0-ack1.12之前），请执行以下命令查看指标数据
   curl -s http://10.10.0.xxx:9326/metrics | grep slo_manager_recommender_recommendation_workload_target
   ```



   预期输出：















   ```bash
   # HELP slo_manager_recommender_recommendation_workload_target Recommendation of workload resource request.
   # TYPE slo_manager_recommender_recommendation_workload_target gauge
   slo_manager_recommender_recommendation_workload_target{container_name="xxx",namespace="xxx",recommendation_name="d2169dbf-fb36-4bf4-99d1-673577fb85c1",resource="cpu",workload_api_version="apps/v1",workload_kind="Deployment",workload_name="xxx"} 0.025
   slo_manager_recommender_recommendation_workload_target{container_name="xxx",namespace="xxx",recommendation_name="d2169dbf-fb36-4bf4-99d1-673577fb85c1",resource="memory",workload_api_version="apps/v1",workload_kind="Deployment",workload_name="xxx"} 2.62144e+08
   ```


ack-koordinator组件安装后，会自动创建Service和Service Monitor对象，关联对应的Pod。如果正在使用阿里云Prometheus，那么这些指标会被自动采集，并展示在对应的Grafana大盘上。

由于Prometheus有多种采集方式，如果使用的是自建Prometheus，请自行参见Prometheus官方文档进行配置，并在配置过程中参考以上过程进行调试。调试完成后，可参见 [步骤二：（可选）通过Prometheus查看结果](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/resource-profiling#45723ea414o5k "")，在环境中配置对应的Grafana监控大盘。

### 如何清理资源画像结果和规则？

资源画像结果和规则分别保存在Recommendation和RecommendationProfile两个CRD中，执行以下命令删除所有资源画像结果和规则。

```bash
# 删除所有资源画像结果。
kubectl delete recommendation -A --all

# 删除所有资源画像规则。
kubectl delete recommendationprofile -A --all
```

### 如何授权子账号使用资源画像？

ACK的授权体系包含对基础资源层的RAM授权和对ACK集群层的RBAC（Role-Based Access Control）授权两部分，有关ACK的授权体系介绍，请参见 [授权最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practices-of-authorization "")。若希望为某一子账号授权使用集群的资源画像功能，推荐参考以下最佳实践进行授权：

1. **RAM授权**

   可以使用主账号登录 [RAM管理控制台](https://ram.console.aliyun.com/)，为该子账号授予系统内置的 **AliyunCSFullAccess** 权限。具体操作，请参见 [授权](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/authorization-overview/#764e042d25ky7 "")。

2. **RBAC授权**

   完成RAM授权后，还需要为该子账号授予目标集群中 **开发人员或以上** 的RBAC权限。具体操作，请参见 [使用RBAC授予集群内资源操作权限](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/grant-rbac-permissions-to-ram-users-or-ram-roles "")。


**说明**

系统预置的开发人员或以上的RBAC权限拥有对集群中所有Kubernetes资源的读写权限。若希望对子账号授予更精细化的权限，可以参考 [使用自定义RBAC限制集群内资源操作](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-an-rbac-role "") 创建或编辑自定义ClusterRole实例。资源画像功能需要为ClusterRole添加如下内容：

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
name: recommendation-clusterrole
rules:
- apiGroups:
  - "autoscaling.alibabacloud.com"
resources:
  - "*"
verbs:
  - "*"
```