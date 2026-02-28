### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[分布式云容器平台ACK One](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/)[操作指南](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/)[分布式工作流Argo集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/kubernetes-clusters-for-distributed-argo-workflows/)[最佳实践](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/best-practices/)迁移Batch批量计算到分布式工作流Argo集群

# 迁移Batch批量计算到分布式工作流Argo集群

更新时间：2025-06-15 21:43:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：在Argo UI配置SLS日志链接](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/configure-sls-log-links-in-argo-ui)[下一篇：使用Argo Workflow编排动态DAG Fan-out/Fan-in任务](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-argo-workflow-to-orchestrate-dynamic-dag-fan-out-fan-in-tasks)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

Batch批量计算相关概念

分布式工作流Argo相关概念

Batch批量计算和Argo工作流对比

功能映射

Argo工作流示例

简单工作流

Loops工作流

DAG工作流（MapReduce）

迁移Batch批处理系统到Argo工作流

使用建议

相关参考

批处理作业（Batch）通常用于数据处理、仿真计算、科学计算等领域，往往需要大规模的计算资源。分布式工作流Argo集群基于开源Argo Workflows项目开发，完全符合开源工作流标准。通过工作流集群，您可以轻松编排工作流，每个工作流步骤使用容器运行，可以在短时间内轻松运行大规模机器学习、仿真计算和数据处理等计算密集型作业，也可以快速运行CI/CD流水线任务。将离线任务和批量计算任务迁移到工作流集群可以帮助您降低运维复杂度、节约运行成本。

## **背景信息**

工作流集群是无服务器Serverless工作流引擎，基于Kubernetes集群构建，托管了开源 [Argo Workflows](https://argoproj.github.io/argo-workflows/)。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6328300571/CAEQSBiBgICB5IDrhRkiIDdhYzg4ZjhkYjhjMzQxMTk5ZWNmYTE5Nzc5ZWNlZmQ14111679_20231215102844.883.svg)

## Batch批量计算相关概念

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6328300571/CAEQORiBgMCiica55hgiIDFmMzkyNjQ5NTI5NDRmYTM5MmQxZGYzM2FkNmFmZjQy4147132_20240103141638.330.svg)

#### **作业（Jobs）**

一个任务单元（例如Shell脚本、Linux可执行文件或Docker容器镜像），可以提交给Batch批量计算系统，批量计算系统会在计算环境中分配计算资源并运行作业。

#### **Array Jobs**

Array Job是指一系列相似或相同的作业，这些作业作为一个数组批量提交并运行。同一Array Job下的作业都有相同的作业定义，但可以通过索引来区分，每个作业实例会处理不同的数据集或执行稍有差异的任务。

#### **作业定义（Job Definitions）**

作业定义指定了作业的运行方式，运行作业前需要先创建作业定义。

作业定义一般包含：作业运行所使用的镜像、具体命令与参数、需要的CPU/Memory资源、环境变量、磁盘存储等。

#### **作业队列（Job Queues）**

向Batch批量计算系统提交作业时，会提交到指定的作业队列中排队，直到作业被调度运行。作业队列可以设置优先级，并指定关联的计算环境。

#### **计算环境（Compute Environment）**

计算环境是一组计算资源，可以运行作业。计算环境需要指定虚拟机的机型、环境的最小和最大vCPU数量、以及Spot竞价实例的价格。

## 分布式工作流Argo相关概念

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6328300571/CAEQORiBgIDkl8i55hgiIDgwMmNlYmNmNGIyNzQwMzZhYTE2ZmJiZGZkZGU1Y2Mx4147132_20240103141638.330.svg)

#### **模板（Templates）**

模板定义了一个任务（作业），是工作流的组成部分，一个工作流至少要包含一个模板。模板中包含要运行的Kubernetes容器和相应的输入输出参数。

#### **工作流（Workflows）**

工作流包含一个或者多个任务（模板），并可以编排多个任务，支持定义复杂的任务流程，如序列化、并行化任务，以及在条件满足时执行特定的任务。创建工作流后，工作流中的任务会在Kubernetes集群中以Pod形式运行。

#### **工作流模板（Workflow Templates）**

工作流模板是可复用的工作流的静态定义，类似于函数，可以在多个工作流中被引用并运行。在定义复杂工作流时可以复用已有的工作流模板，减少重复性定义。

#### **Serverless Kubernetes集群**

分布式工作流Argo集群自带计算环境，不需要手动创建和管理。工作流提交后，使用阿里云弹性容器ECI，以Serverless方式运行工作流中的任务，不需要维护Kubernetes节点。利用阿里云的弹性能力，可以运行大规模工作流（数万任务Pod），同时使用数十万核CPU的算力资源，在工作流运行完成后自动释放资源。加快工作流运行速度，并节省计算成本。

## **Batch批量计算和Argo工作流对比**

#### **Batch批量计算**

- 使用者需要学习Batch批量计算作业定义规范与用法，有厂商绑定风险。


- 还需要管理计算环境，设置机型和规模等，非Serverless方式，运维成本比较高。

- 由于计算环境规模的限制，需要管理作业队列以设置作业的优先级，复杂度比较高。


#### **Argo工作流**

- 基于Kubernetes集群和开源Argo Workflows构建，以云原生的方式编排运行工作流，无厂商绑定风险。

- 支持复杂工作流任务的编排，可以应对数据处理、仿真计算、科学计算等复杂业务场景。

- 计算环境采用阿里云弹性容器ECI，无需维护节点。

- 大规模算力的按需使用，按量计费，避免工作流排队等待，提高效率，节省计算成本。


### **功能映射**

| **功能分类** | **Batch批量计算** | **Argo Workflows** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **功能分类** | **Batch批量计算** | **Argo Workflows** |
| 用户体验 | 批量计算CLI | [Argo Workflows CLI](https://argo-workflows.readthedocs.io/en/latest/walk-through/argo-cli/) |
| Json定义作业 | YMAL定义作业 |
| SDK | [SDK](https://argo-workflows.readthedocs.io/en/latest/client-libraries/) |
| 核心能力 | 作业（Jobs） | [工作流（Workflows)](https://argo-workflows.readthedocs.io/en/latest/walk-through/hello-world/) |
| Array jobs | [工作流（Workflows）Loops](https://argo-workflows.readthedocs.io/en/latest/walk-through/loops/) |
| Job dependencies | [工作流（Workflows）DAG](https://argo-workflows.readthedocs.io/en/latest/walk-through/dag/) |
| Job Environments Variables | [工作流（Workflows）Parameters](https://argo-workflows.readthedocs.io/en/latest/walk-through/parameters/) |
| Automated Job retries | [工作流（Workflows）Retrying](https://argo-workflows.readthedocs.io/en/latest/walk-through/retrying-failed-or-errored-steps/) |
| Job timeouts | [工作流（Workflows）Timeouts](https://argo-workflows.readthedocs.io/en/latest/walk-through/timeouts/) |
| 无 | [工作流（Workflows）Artifacts](https://argo-workflows.readthedocs.io/en/latest/walk-through/artifacts/) |
| 无 | [工作流（Workflows）Conditions](https://argo-workflows.readthedocs.io/en/latest/walk-through/conditionals/) |
| 无 | [工作流（Workflows）Recursion](https://argo-workflows.readthedocs.io/en/latest/walk-through/recursion/) |
| 无 | [工作流（Workflows）Suspending/Resuming](https://argo-workflows.readthedocs.io/en/latest/walk-through/suspending/) |
| GPU jobs | [工作流指定GPU机型运行工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/run-a-workflow-using-a-specified-ecs-specification "") |
| Volumes | [Volumes](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-volumes "") |
| Job priority | [工作流（Workflows）Priority](https://argo-workflows.readthedocs.io/en/latest/cli/argo_submit/) |
| 作业定义（JobDefinition） | [工作流模板（Workflows Templates）](https://argo-workflows.readthedocs.io/en/latest/workflow-templates/) |
| 计算环境 | Job queues | 无，云上Serverless弹性，作业无需排队。 |
| 计算环境（Compute Environment) | [Serverless Kubernetes集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/overview-12 "") |
| 生态集成 | 事件驱动 | [事件驱动](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/turn-on-event-driven-functions "") |
| 可观测性 | [可观测性](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/observability/ "") |

## Argo工作流示例

### 简单工作流

以下示例表示：启动了一个任务Pod，使用alpine镜像，运行Shell命令echo helloworld。

在此工作流基础上，可以在args中指定多个Shell命令并执行，也可以使用自定义镜像运行镜像中的命令。

```yaml
cat > helloworld.yaml << EOF
apiVersion: argoproj.io/v1alpha1
kind: Workflow                  # new type of k8s spec
metadata:
  generateName: hello-world-    # name of the workflow spec
spec:
  entrypoint: main         # invoke the main template
  templates:
    - name: main              # name of the template
      container:
        image: registry.cn-hangzhou.aliyuncs.com/acs/alpine:3.18-update
        command: [ "sh", "-c" ]
        args: [ "echo helloworld" ]
EOF
argo submit helloworld.yaml
```

### Loops工作流

以下示例表示：在镜像print-pet中打包了pets.input文本文件和print-pet.sh脚本文件，print-pet.sh以job-index为输入参数，打印pets.input文件行号为job-index的pet。具体文件内容请访问 [GitHub仓库](https://github.com/AliyunContainerService/argo-workflow-examples/tree/main/loops)。

在工作流中，会同时启动5个Pod，并分别传入参数job-index 1到job-index 5，每个Pod根据输入的job-index的值，打印相应行的pet。

通过Loops工作流可以实现数据分片和并行处理，加快海量数据的处理速度。更多Loops示例，请参见 [工作流（Workflows）Loops](https://argo-workflows.readthedocs.io/en/latest/walk-through/loops/)。

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: loops-
spec:
  entrypoint: loop-example
  templates:
  - name: loop-example
    steps:
    - - name: print-pet
        template: print-pet
        arguments:
          parameters:
          - name: job-index
            value: "{{item}}"
        withSequence:  # loop to run print-pet template with parameter job-index 1 ~ 5 respectively.
          start: "1"
          end: "5"
  - name: print-pet
    inputs:
      parameters:
      - name: job-index
    container:
      image: acr-multiple-clusters-registry.cn-hangzhou.cr.aliyuncs.com/ack-multiple-clusters/print-pet
      command: [/tmp/print-pet.sh]
      args: ["{{inputs.parameters.job-index}}"] # input parameter job-index as args of container
```

### DAG工作流（MapReduce）

真实的批处理场景中，往往需要多个Job配合完成，所以需要指定Job间的依赖关系，DAG是指定依赖关系的最佳方式。

但主流的Batch批处理系统，需要通过Job ID指定Job依赖，由于Job ID需要在Job提交后才能获取，因此需要编写脚本实现Job间依赖（伪代码如下），Job较多时，依赖关系不够直观，维护成本较高。

```yaml
//Batch批处理系统Job间依赖，JobB依赖JobA，在JobA完成后运行。
batch submit JobA | get job-id
batch submit JobB --dependency job-id (JobA)
```

Argo工作流可以通过DAG定义子任务之间的依赖关系，示例如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6328300571/CAEQORiBgIDUmMy55hgiIGExOTJhM2RiMzA4MzQ2ZWM5OGNlYzU5M2E1NzY2NzVj4147132_20240103152302.610.svg)

- Task B和Task C依赖Task A运行

- Task D依赖Task B和Task C运行


```yaml
# The following workflow executes a diamond workflow
apiVersion: argoproj.io/v1alpha1
kind: Workflow
metadata:
  generateName: dag-diamond-
spec:
  entrypoint: diamond
  templates:
  - name: diamond
    dag:
      tasks:
      - name: A
        template: echo
        arguments:
          parameters: [{name: message, value: A}]
      - name: B
        depends: "A"
        template: echo
        arguments:
          parameters: [{name: message, value: B}]
      - name: C
        depends: "A"
        template: echo
        arguments:
          parameters: [{name: message, value: C}]
      - name: D
        depends: "B && C"
        template: echo
        arguments:
          parameters: [{name: message, value: D}]
  - name: echo
    inputs:
      parameters:
      - name: message
    container:
      image: alpine:3.7
      command: [echo, "{{inputs.parameters.message}}"]
```

在Git仓库中，还为您提供了一个MapReduce工作流示例，支持对数据进行分片处理，并对计算结果进行聚合。具体示例，请参见 [map-reduce](https://github.com/AliyunContainerService/argo-workflow-examples/tree/main/map-reduce)。

## 迁移Batch批处理系统到Argo工作流

1. 评估与规划


评估现有Batch批处理作业，包括依赖关系、资源需求、参数配置等。了解Argo Workflows的特性和最佳实践，并根据本文选择Argo Workflows的功能以替代Batch批处理作业。另外，由于分布式工作流Argo集群的Serverless ECI能力，您可以跳过规划Compute Environment和管理优先级队列。

2. 创建分布式工作流Argo集群


具体操作，请参见 [工作流集群快速入门](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/workflow-cluster-quickstart "")。

3. 转换作业定义


根据Batch批量计算到Argo工作流的功能映射，重写Batch批量计算作业为Argo工作流，也可以通过调用Argo工作流 [SDK](https://argoproj.github.io/argo-workflows/client-libraries/)，以自动化方式创建工作流，并接入业务系统。

4. 数据存储


确保分布式工作流Argo集群可以访问工作流运行所需要的数据，工作流集群可以挂载访问阿里云OSS、NAS、CPFS、云盘等存储资源。更多信息，请参见 [使用存储卷](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-volumes "")。

5. 测试验证


验证工作流运行正常、数据访问、结果输出正常、资源用量符合预期。


6. 运维：监控和日志


开启分布式工作流Argo集群 [可观测能力](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/observability/ "")，查看工作流运行状态和日志。


## 使用建议

- 在用户体验、核心能力、计算环境和生态集成方面，Argo工作流可以覆盖主流Batch批处理系统的功能，同时在复杂工作流编排和计算环境管理方面更具优势。

- 工作流集群基于Kubernetes构建，工作流定义符合Kubernetes YAML规范，子任务定义符合Kubernetes Container规范。如果您已经在使用Kubernetes运行在线应用，可以快速上手编排工作流集群，统一使用Kubernetes作为在线应用和离线应用的技术底座。

- 工作流集群计算环境采用阿里云弹性容器ECI，不需要维护节点，同时提供大规模算力的按需使用，按量计费，避免工作流排队等待，提高运行效率，节省计算成本。

- 结合使用阿里云Spot实例，可以大幅降低计算成本。

- 分布式工作流适合CI/CD、数据处理、仿真计算、科学计算等业务场景。


## 相关参考

- 了解更多开源Argo工作流内容，请参见 [开源Argo Workflows](https://argoproj.github.io/argo-workflows/)。

- 了解工作流集群的功能原理及相关操作，请参见 [分布式工作流Argo集群概述](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/overview-12 "")。

- 创建工作流集群，具体操作，请参见 [创建工作流集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-a-workflow-cluster "")。

- 创建工作流，具体操作，请参见 [创建工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-a-workflow "")。

- 在工作流集群中挂载存储卷，具体操作，请参见 [使用存储卷](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/use-volumes "")。