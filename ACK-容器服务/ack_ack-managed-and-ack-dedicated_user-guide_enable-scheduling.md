### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[GPU](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-5/)开启调度功能

# 开启调度功能

更新时间：2026-01-12 04:53:58

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调度标签介绍

开启调度功能

独占调度

共享调度

拓扑感知调度

卡型调度

在ACK托管集群Pro版集群中部署GPU计算任务时，可通过为GPU节点分配调度属性标签（如独占、共享、拓扑感知等）和指定卡型标签（卡型调度），实现资源利用率优化与应用精准调度。

## **调度标签介绍**

GPU调度标签通过标识GPU型号、资源分配策略等信息，实现资源精细化管理与高效调度。

| **调度模式** | **标签值** | **适用场景** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **调度模式** | **标签值** | **适用场景** |
| **独占调度**（ **默认**） | `ack.node.gpu.schedule: default` | 性能要求高、需独占整卡的任务，如模型训练、HPC等。 |
| **共享调度** | `ack.node.gpu.schedule: cgpu`<br>`ack.node.gpu.schedule: core_mem`<br>`ack.node.gpu.schedule: share`<br>`ack.node.gpu.schedule: mps` | 提升 GPU 利用率，适用于多租户、推理等多个轻量级任务并发运行的场景。<br>- `cgpu`：算力共享，显存隔离，基于阿里云cGPU共享技术实现。<br>  <br>- `core_mem`：算力与显存隔离。<br>  <br>- `share`：共享算力和显存资源，无隔离。<br>  <br>- `mps`：算力共享，显存隔离，基于NVIDIA MPS隔离功能结合阿里云cGPU技术实现。 |
| `ack.node.gpu.placement: binpack`<br>`ack.node.gpu.placement: spread` | 适用于在开启`cgpu`、`core_mem`、`share`、`mps`共享调度功能后，且单个节点含多张GPU卡，优化多GPU卡资源的分配策略。<br>- `binpack`：（默认）多卡紧凑调度，多个Pod优先填满一张GPU后再分配下一张，减少资源碎片，适合资源利用率或节能优先的场景。<br>  <br>- `spread`：多卡分散调度，将Pod分散到不同GPU上，降低单卡故障影响，适合高可用性任务。 |
| **拓扑感知调度** | `ack.node.gpu.schedule: topology` | 根据单机内GPU物理拓扑关系，为Pod自动分配通信带宽最优的GPU组合，适用于对GPU之间通信延迟敏感的任务。 |
| **卡型调度** | `aliyun.accelerator/nvidia_name：<GPU显卡名称>`<br>> 配合卡型调度设置GPU任务的显存容量、总GPU卡数。<br>> `aliyun.accelerator/nvidia_mem：<每张卡的显存容量>`<br>> `aliyun.accelerator/nvidia_count：<总共拥有的GPU卡数>` | 将任务调度到指定 GPU 型号的节点上，或避开特定型号。 |

## **开启调度功能**

一个节点只能启用一种 GPU 调度模式（独占、共享或拓扑感知）。启用后，其他调度模式所上报的扩展资源将自动置为 0。

### **独占调度**

节点未添加任何GPU调度标签，则 **默认** 启用独占调度。此时，节点以单张GPU卡为最小分配单元，为Pod提供GPU资源。

> 若已开启其他GPU调度模式，仅删除标签无法恢复独占调度，需手动将标签值修改为`ack.node.gpu.schedule: default`才能恢复独占调度能力。

### **共享调度**

共享调度，仅支持ACK托管集群Pro版。具体信息，请参见 [使用限制](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/install-and-use-ack-ai-installer-and-the-gpu-inspection-tool#ac13289bfaj59 "")。

1. **安装共享调度组件**`ack-ai-installer` **。**



1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**应用** \> **云原生AI套件**。

3. 在 **云原生AI套件** 页面，单击 **一键部署**。在一键部署 **云原生AI套件** 页面，选中 **调度策略扩展（批量任务调度、GPU共享、GPU拓扑感知）。**


      > 如何设置cGPU服务支持的算力调度Policy策略，请参见 [安装并使用cGPU服务](https://help.aliyun.com/zh/egs/developer-reference/use-docker-to-install-and-use-the-cgpu-component-of-kubergpu-products#table-vde-zd3-930 "")。

4. 在 **云原生AI套件** 页面，单击 **部署云原生AI套件**。

      在 **云原生AI套件** 页面组件列表，查看已安装的共享GPU组件 **ack-ai-installer**。


2. **开启共享调度功能。**



1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点池**。

2. 在 **节点池** 页面，单击 **创建节点池** 配置节点标签，单击 **确认配置**。


      > 其余配置项信息可保持默认。关于节点标签的使用场景，请参见 [调度标签介绍](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-scheduling#83fc229594p68 "")。



      - 配置基础共享调度。

        单击 **节点标签（Labels）** 的![节点标签](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7405585061/p183919.png)，设置 **键** 为`ack.node.gpu.schedule`，可选择配置`cgpu`、`core_mem`、`share`、`mps`（需 [安装MPS Control Daemon组件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-mps-to-isolate-gpu-memory-resources#8d9423fa74nrd "")）标签值之一。

      - 配置多卡共享调度。

        当节点包含多张GPU卡，优化多GPU卡资源的分配策略时，可在基础共享调度上，进一步配置多卡共享调度。

        单击 **节点标签（Labels）** 的![节点标签](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7405585061/p183919.png)，设置 **键** 为`ack.node.gpu.placement`，可选择配置`binpack`、`spread`标签值之一。


3. **验证是否已开启共享调度功能。**







cgpu/share/mps



core\_mem



binpack



spread



















将变量<NODE\_NAME>替换为目标节点名称后，执行以下命令，验证节点池是否开启`cgpu`/`share`/`mps`共享调度功能。



















```bash
kubectl get nodes <NODE_NAME> -o yaml | grep -q "aliyun.com/gpu-mem"
```





预期输出：

















```bash
aliyun.com/gpu-mem: "60"
```





`aliyun.com/gpu-mem`字段不为0，说明已开启`cgpu`/`share`/`mps`共享调度功能。







将变量`<NODE_NAME>`替换为目标节点名称后，执行以下命令，验证节点池是否开启`core_mem`共享调度功能。



















```bash
kubectl get nodes <NODE_NAME> -o yaml | grep -E 'aliyun\.com/gpu-core\.percentage|aliyun\.com/gpu-mem'
```





预期输出：

















```bash
aliyun.com/gpu-core.percentage:"80"
aliyun.com/gpu-mem:"6"
```





字段`aliyun.com/gpu-core.percentage`和`aliyun.com/gpu-mem`均不为0，说明已开启`core_mem`共享调度功能。









使用共享GPU调度 [GPU资源查询工具](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/install-and-use-ack-ai-installer-and-the-gpu-inspection-tool#section-ibc-wm5-2zx "")，执行以下命令，查询节点GPU资源分配情况：

















```bash
kubectl inspect cgpu
```





预期输出：

















```bash
NAME                   IPADDRESS      GPU0(Allocated/Total)  GPU1(Allocated/Total)  GPU2(Allocated/Total)  GPU3(Allocated/Total)  GPU Memory(GiB)
cn-shanghai.192.0.2.109  192.0.2.109  15/15                   9/15                   0/15                   0/15                   24/60
   --------------------------------------------------------------------------------------
Allocated/Total GPU Memory In Cluster:
24/60 (40%)
```





输出结果表明，GPU0资源已全部分配15/15，GPU1已分配资源为9/15，符合优先填满一张GPU后再分配下一张的调度策略，`binpack`策略生效。





使用共享调度 [GPU资源查询工具](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/install-and-use-ack-ai-installer-and-the-gpu-inspection-tool#section-ibc-wm5-2zx "")，执行以下命令，查询节点GPU资源分配情况：

















```bash
kubectl inspect cgpu
```





预期输出：

















```bash
NAME                   IPADDRESS      GPU0(Allocated/Total)  GPU1(Allocated/Total)  GPU2(Allocated/Total)  GPU3(Allocated/Total)  GPU Memory(GiB)
cn-shanghai.192.0.2.109  192.0.2.109  4/15                   4/15                   0/15                   4/15                   12/60
   --------------------------------------------------------------------------------------
Allocated/Total GPU Memory In Cluster:
12/60 (20%)
```





输出结果表明，GPU0已分配资源4/15，GPU1已分配资源为4/15，GPU3已分配资源为4/15，符合优先将Pod分散到不同GPU上的调度策略，`spread`策略生效。


### **拓扑感知调度**

拓扑感知调度，仅支持ACK托管集群Pro版。具体信息，请参见 [系统组件版本要求](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/install-ack-ai-installer#taskbody-828-79a-zdr "")。

1. [安装共享调度组件ack-ai-installer](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-scheduling#b7058b6b6d7je "")。

2. **开启拓扑感知调度功能。**



将变量<NODE\_NAME>替换为目标节点名称后，执行以下命令，为节点增加Label，显式激活节点的GPU拓扑感知调度功能。

















```bash
kubectl label node <NODE_NAME> ack.node.gpu.schedule=topology
```





> 节点激活GPU拓扑感知调度后，不再支持非拓扑感知GPU资源的调度。可以执行`kubectl label node <NODE_NAME> ack.node.gpu.schedule=default --overwrite`命令更改Label，恢复独占调度。

3. **验证是否已开启拓扑感知调度功能。**

将变量<NODE\_NAME>替换为目标节点名称后，执行以下命令，验证节点池是否开启`topology`拓扑感知调度功能。

















```bash
kubectl get nodes <NODE_NAME> -o yaml | grep aliyun.com/gpu
```





预期输出：

















```bash
aliyun.com/gpu: "2"
```





`aliyun.com/gpu`字段不为0，说明已开启`topology`拓扑感知调度功能。


### **卡型调度**

将任务调度到指定 GPU 型号的节点上，或避开特定型号。

1. **查看节点GPU卡型。**

执行以下命令，在集群中查询节点的GPU卡型。


> 节点GPU卡型名称： **NVIDIA\_NAME** 字段。
















```bash
kubectl get nodes -L aliyun.accelerator/nvidia_name
```



预期输出如下：















```bash
NAME                        STATUS   ROLES    AGE   VERSION            NVIDIA_NAME
cn-shanghai.192.XX.XX.176   Ready    <none>   17d   v1.26.3-aliyun.1   Tesla-V100-SXM2-32GB
cn-shanghai.192.XX.XX.177   Ready    <none>   17d   v1.26.3-aliyun.1   Tesla-V100-SXM2-32GB
```





**展开查看更多方式查看GPU卡型。**






在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **容器组**。在创建的容器所在行（例如tensorflow-mnist-multigpu-\*\*\*），单击 **操作** 列的 **终端**。然后从下拉列表中选择需要登录的容器，执行如下命令。



   - 查询卡型：`nvidia-smi --query-gpu=gpu_name --format=csv,noheader --id=0 | sed -e 's/ /-/g'`

   - 查询每张卡显存容量：`nvidia-smi --id=0 --query-gpu=memory.total --format=csv,noheader | sed -e 's/ //g'`

   - 查询节点上总共拥有的GPU卡数：`nvidia-smi -L | wc -l`


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9341515571/p992502.png)

2. **开启卡型调度。**

1. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **任务**。

2. 在 **任务** 页面，单击 **使用YAML创建资源**。使用如下示例创建应用，并开启卡型调度功能。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9341515571/p996447.png)






      指定特定卡型



      屏蔽特定卡型



















      利用GPU卡型调度标签，让业务运行在指定卡型的节点上。



      将`aliyun.accelerator/nvidia_name: "Tesla-V100-SXM2-32GB"` 代码中`Tesla-V100-SXM2-32GB`替换为节点实际卡型。




      **展开查看YAML文件详细信息**




















      ```yaml
      apiVersion: batch/v1
      kind: Job
      metadata:
        name: tensorflow-mnist
      spec:
        parallelism: 1
        template:
          metadata:
            labels:
              app: tensorflow-mnist
          spec:
            nodeSelector:
              aliyun.accelerator/nvidia_name: "Tesla-V100-SXM2-32GB" # 使该应用运行在Tesla V100-SXM2-32GB上
            containers:
      - name: tensorflow-mnist
        image: registry.cn-beijing.aliyuncs.com/acs/tensorflow-mnist-sample:v1.5
        command:
        - python
        - tensorflow-sample-code/tfjob/docker/mnist/main.py
        - --max_steps=1000
        - --data_dir=tensorflow-sample-code/data
        resources:
          limits:
            nvidia.com/gpu: 1
        workingDir: /root
      restartPolicy: Never
```

创建成功后，可以在左侧导航栏中选择**工作负载** \> **容器组**。在容器组列表中，可看到一个示例Pod（容器组）成功调度到对应的节点上，从而实现基于GPU卡型调度标签的灵活调度。

利用GPU卡型调度标签，通过节点亲和性与反亲和性，避免让业务运行在某些卡型上。

将`values: - "Tesla-V100-SXM2-32GB"`中`Tesla-V100-SXM2-32GB`替换为节点实际卡型。

**展开查看YAML文件详细信息**

```yaml
apiVersion: batch/v1
kind: Job
metadata:
name: tensorflow-mnist
spec:
parallelism: 1
template:
    metadata:
      labels:
        app: tensorflow-mnist
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: aliyun.accelerator/nvidia_name  # 卡型调度标签
                operator: NotIn
                values:
                - "Tesla-V100-SXM2-32GB"            # 避免Pod调度到卡型为Tesla-V100-SXM2-32GB上。
      containers:
      - name: tensorflow-mnist
        image: registry.cn-beijing.aliyuncs.com/acs/tensorflow-mnist-sample:v1.5
        command:
        - python
        - tensorflow-sample-code/tfjob/docker/mnist/main.py
        - --max_steps=1000
        - --data_dir=tensorflow-sample-code/data
        resources:
          limits:
            nvidia.com/gpu: 1
        workingDir: /root
      restartPolicy: Never
```

创建成功后，应用不会调度到标签键为`aliyun.accelerator/nvidia_name`且对应值为`Tesla-V100-SXM2-32GB`的节点，但允许调度到其他卡型的GPU节点。