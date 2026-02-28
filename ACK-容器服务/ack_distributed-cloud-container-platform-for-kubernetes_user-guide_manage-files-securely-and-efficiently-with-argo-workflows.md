### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[分布式云容器平台ACK One](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/)[操作指南](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/)[分布式工作流Argo集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/kubernetes-clusters-for-distributed-argo-workflows/)[最佳实践](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/best-practices/)使用Argo Workflows安全高效管理文件

# 如何使用Argo Workflow安全高效管理文件

更新时间：2024-10-16 05:58:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用Argo Workflows编排基因计算工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/orchestrate-gene-computing-workflows-using-argo-workflows)[下一篇：使用Python SDK构建大规模Argo Workflows](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-pythonsdk-to-build-large-scale-argo-workflows)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

复杂工作流编排的存储难题

方案一：支持超大文件上传

使用示例

方案二：配置文件清理机制

使用示例

方案三：支持流式传输机制

联系我们

工作流集群是一个全托管的Argo服务，专注于高效安全的文件管理，并提供了一些增强功能。它在批处理、数据处理和持续集成等场景中比标准的Argo Workflows更具优势。本文将介绍工作流集群如何实现高效安全的文件管理。

## **复杂工作流编排的存储难题**

[Argo Workflows](https://github.com/argoproj/argo-workflows) 是一个开源的云原生工作流引擎，也是CNCF的毕业项目。Argo Workflows可以自动化管理Kubernetes上的复杂工作流程，适用于多种场景，如定时任务、机器学习、ETL和数据分析、模型训练、数据流Pipeline以及CI/CD等。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8072709271/CAEQThiBgIDLwKyviRkiIGE2MjQxNGE2NTZkZDQ4NmI4YmE5YjZjOTBlOGNlOTQ44565055_20240802154123.510.svg)

在使用Argo Workflows进行任务编排时，尤其是在数据量大的场景下，如模型训练、数据处理、生物信息学分析等，如何高效管理和存储Artifacts是非常重要的一环。然而，采用开源方案可能面临以下挑战。

- **超大文件无法上传**：对于超过5 GiB的文件，因客户端上传限制而导致上传失败。

- **缺乏文件清理机制**：随着工作流执行的推进，中间产生的临时文件或已完成任务的输出结果若未及时清理，会导致OSS存储空间的浪费。

- **Argo Server磁盘占用过高**：在使用Argo Server下载文件时，需要先落盘再传输，高磁盘占用不仅影响服务器性能，还可能导致服务中断或数据丢失。


[分布式工作流Argo集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/overview-12 "") 作为一款完全遵循社区规范的全托管式Argo Workflows服务，专注于解决大规模、高安全性的文件管理工作挑战。其一系列重要增强功能包括超大文件分片上传、Artifacts垃圾回收（GC）以及Artifacts流式传输。这些特性旨在帮助用户在阿里云环境下实现对OSS文件的高效、安全和精细管理。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8072709271/CAEQSBiBgICB5IDrhRkiIDdhYzg4ZjhkYjhjMzQxMTk5ZWNmYTE5Nzc5ZWNlZmQ14111679_20231215102844.883.svg)

分布式工作流Argo集群作为全托管的Argo工作流服务，在Artifacts文件管理上相比于开源方案具有以下优势：

| **OSS文件管理能力** | **分布式工作流Argo集群** | **开源Argo Workflows** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **OSS文件管理能力** | **分布式工作流Argo集群** | **开源Argo Workflows** |
| 文件上传 | 支持超大文件分片上传 | 仅支持 < 5 GiB，超大文件暂不支持 |
| 文件回收 | 支持Artifacts垃圾回收（GC） | 不支持文件回收 |
| 文件下载 | 支持流式传输 | 需要落盘，过程繁琐 |

## 方案一：支持超大文件上传

Argo开源方案不支持超大文件上传，限制了其在数据密集型任务中的应用。为解决这一问题，分布式工作流Argo集群优化了超大文件上传至OSS的逻辑，支持分片和断点续传，显著提升了大文件处理效率和可靠性。优化后的方案还能独立校验每个分片完整性，进一步增强数据完整性和系统容错能力。

### **使用示例**

该功能在工作流集群中默认开通，在 [配置Artifacts](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/configure-artifacts "") 后，提交示例工作流，即可在OSS上获得一个大小为20 GiB的文件testfile.txt，证明超大文件已上传。

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: artifact-
spec:
  entrypoint: main
  templates:
    - name: main
      metadata:
        annotations:
          k8s.aliyun.com/eci-extra-ephemeral-storage: "20Gi"   # 自定义设置要增加的临时存储空间大小。
          k8s.aliyun.com/eci-use-specs : "ecs.g7.xlarge"
      container:
        image: alpine:latest
        command:
          - sh
          - -c
        args:
          - |
            mkdir -p /out
            dd if=/dev/random of=/out/testfile.txt bs=20M count=1024   # 生成20 GiB的文件。
            echo "created files!"
      outputs:    # 触发文件上传到OSS。
        artifacts:
          - name: out
            path: /out/testfile.txt
```

## **方案二：配置文件清理机制**

开源的Argo方案无法实现OSS文件的自动回收，增加了用户的使用和运维成本。Argo Workflows的Artifacts垃圾回收（GC）机制主要用于在工作流结束后清理不再需要的文件，如中间结果、日志等，从而节省存储空间和成本，避免存储资源的无限制地被消耗。

工作流集群优化了OSS上的文件清理方法，用户只需配置简单的回收逻辑，就可以实现以下功能：

- **自动清理**：在工作流完成后，或在管理员手动清理工作流相关资源一定时间后，自动回收上传至OSS的文件。

- **灵活配置回收**：您可以选择只为成功的工作流任务配置回收策略，避免清理失败日志，便于后续追踪定位问题，或者选择只为失败的工作流任务配置回收策略，清除无效的中间产出。

- **生命周期管理策略**：利用OSS提供的生命周期管理策略，您可以设置规则，根据时间、前缀等参数，自动删除旧的Artifacts，或将早期的Artifacts归档至冷存储。这样不仅能够确保数据完整性，也可以有效降低存储成本。


### **使用示例**

通过配置Artifacts垃圾回收（GC）策略，可以启用该功能。以下示例中，工作流整体的Artifacts垃圾回收（GC）策略为删除后回收，其中on-completion.txt文件的回收策略为完成时回收。提交该工作流后，可以在OSS上观察到，工作流完成时on-completion.txt文件被回收，删除工作流后on-deletion.txt文件也会被回收。

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: artifact-gc-
spec:
  entrypoint: main
  artifactGC:
    strategy: OnWorkflowDeletion  # 全局回收策略，在Workflow被删除时回收Artifact，可被覆盖。
  templates:
    - name: main
      container:
        image: argoproj/argosay:v2
        command:
          - sh
          - -c
        args:
          - |
            echo "hello world" > /tmp/on-completion.txt
            echo "hello world" > /tmp/on-deletion.txt
      outputs: # 上传文件到OSS。
        artifacts:
          - name: on-completion
            path: /tmp/on-completion.txt
            artifactGC:
              strategy: OnWorkflowCompletion  # 覆盖全局回收策略，在Workflow完成时回收Artifact。
          - name: on-deletion
            path: /tmp/on-deletion.txt
```

## **方案三：支持流式传输机制**

使用开源方案时，Argo Server在下载文件时需要先写入磁盘再传输，这可能导致较高的磁盘占用率，从而影响服务器性能，甚至可能导致服务中断或数据丢失。

工作流集群实现了OSS的OpenStream接口，当您在Argo Workflows UI界面下载文件时，Argo Server可以直接将OSS服务端的文件流式传输给用户，并非将文件完整下载到服务器本地再提供给用户。这种流式传输机制特别适合处理大规模数据传输和存储的工作流任务，具有以下优势。

- **提升下载性能**：通过流式传输文件直接从OSS服务端传输，无需等待整个文件下载到Argo Server，从而减少下载开始的延迟，提升响应速度，提供更流畅的体验。

- **减少资源占用以增强并发能力**：流式处理降低了Argo Server对内存和磁盘的需求，使其能在相同硬件资源下处理更多的并行文件传输请求，提高了系统的并发处理能力。随着使用者数量增加或文件大小增大，直接通过流式传输可以更好地扩展服务来处理这种增长，不必担心Argo Server的磁盘空间限制。

- **提升安全合规性**：避免了数据在Argo Server空间中的临时存储，减小了安全风险和数据泄露的可能性，更有效地遵循数据保护和合规性要求。


通过流式传输Artifacts文件，Argo Server能够减轻单点压力，同时提升UI文件下载的性能，从而有效转型为轻量级的数据流转中心，而非存储和计算的重负载中心。

## 联系我们

如果您对于ACK One有任何疑问，欢迎使用钉钉搜索钉钉群号 **35688562** 加入钉钉群。