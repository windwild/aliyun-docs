### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/)

# ElasticQuotaTree

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

ElasticQuotaTree 是一种树形结构，用于定义和管理集群中的弹性配额（Elastic Quota）。Elastic Quota支持在一定范围内动态调整。当某Elastic Quota存在空闲资源时，这些资源可被其他需要资源的Elastic Quota共享，从而在满足保障资源的前提下提升集群资源利用率。

ElasticQuotaTree 是 ACK 集群中用于描述和管理Elastic Quota配置的自定义资源。Elastic Quota将用户的可用资源划分为两部分：

- 保障资源：用户提交的任务所使用的、不可被抢占的资源。

- 非保障资源：可被抢占的资源。


Elastic Quota允许在保障资源空闲时将其临时分配给其他用户使用，并在需要时通过抢占机制回收资源，从而在满足保障资源需求的同时提升集群的整体资源利用率。

## **ElasticQuotaTree YAML示例**

**重要**

当前 ACK 集群仅支持 kube-system 命名空间下的单个 ElasticQuotaTree。若存在多个 ElasticQuotaTree，可能导致配额管理混乱。

```yaml
apiVersion: scheduling.sigs.k8s.io/v1beta1
kind: ElasticQuotaTree
metadata:
  name: elasticquotatree
  namespace: kube-system
spec:
  root:
    children:
    - attributes:
        resourceflavors: "resourceflavor-sample1, resourceflavor-sample2"
      max:
        cpu: 1
        kube-queue/max-jobs: 1
        memory: 1Gi
      name: child-1
      namespaces:
      - default-group
    max:
      cpu: 999900
      kube-queue/max-jobs: 10000000000
      memory: 400000Gi
      nvidia.com/gpu: 100000
    min:
      cpu: 999900
      kube-queue/max-jobs: 10000000000
      memory: 400000Gi
      nvidia.com/gpu: 100000
    name: root
```

## **参数说明**

ElasticQuotaTree 将Elastic Quota以树形结构组织，顶层为 Root 节点，对应自定义资源的 `.Spec.Root` 路径。每个节点包含以下字段。

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `Name` | string | 该节点在 ElasticQuotaTree 中的名称。所有节点的 `Name` 必须唯一，以确保配额统计的准确性。 |
| `Namespace` | \[\]string | 指定哪些 Namespace 中的 Pod 会被默认计入该配额。每个 Namespace 只能属于一个配额，以避免配额统计冲突。 |
| `Max` | map\[string\]string | 定义该配额的资源使用上限。`key`为资源名称，`value`为资源量，需符合 Kubernetes 的资源量表示规范。其中，`kube-queue/max-jobs`是一种特殊资源类型，用于限制在该配额下 ACK Kube Queue 出队时可同时执行的任务数量。 |
| `Min` | map\[string\]string | 定义该配额的保障资源量（即资源下限）。`key`为资源名称，`value`为资源量，需符合 Kubernetes 的资源量表示规范。 |
| `Attributes` | map\[string\]string | （调度器版本 ≥ 6.9.0）描述该配额的属性。目前支持的`key`包括 `resourceflavors`，用于声明该弹性配额关联的节点。 |
| `Children` | list | 列表中的每个元素是一个配额节点，表示该配额的子配额。 |