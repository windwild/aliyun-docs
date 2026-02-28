### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[云原生AI套件](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/)[操作指南](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/)[弹性数据集](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/overview-of-fluid/)[Serverless数据访问加速](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/overview-of-data-access-in-serverless-cloud-computing/)[ACK缓存模式](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/ack-cache-mode/)加速Job应用数据访问

# 加速Job应用数据访问

更新时间：2025-07-15 04:40:24

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：加速在线应用数据访问](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/accelerate-online-applications-1)[下一篇：加速Argo任务数据访问](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/accelerate-argo-workflows-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

使用限制

步骤一：上传测试数据到OSS Bucket

步骤二：创建Dataset和JindoRuntime

（可选）步骤三：数据预热

步骤四：创建Job类型应用容器访问OSS

步骤五：清理环境

Fluid支持在Serverless场景下，通过JindoRuntime优化对象存储的访问，该访问支持缓存模式和无缓存模式。本文介绍如何使用缓存模式加速Job应用数据访问。

## 前提条件

- 已创建一个 **非ContainerOS** 操作系统的ACK Pro版集群，且集群版本为1.18及以上。具体操作，请参见 [创建ACK Pro版集群](https://help.aliyun.com/document_detail/176833.html#task-skz-qwk-qfb "")。



**重要**





ack-fluid组件暂不支持在ContainerOS操作系统上使用。

- 已安装云原生AI套件并部署ack-fluid组件。



**重要**





若您已安装开源Fluid，请卸载后再部署ack-fluid组件。





  - 未安装云原生AI套件：部署 **Fluid**，开启数据缓存加速。具体操作，请参见 [安装云原生AI套件](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/deploy-the-cloud-native-ai-suite#task-2038811 "")。

  - 已安装云原生AI套件：在[容器服务管理控制台](https://cs.console.aliyun.com/)的 **云原生AI套件** 页面部署 **ack-fluid**。
- 已部署ACK虚拟节点（Virtual Node）。具体操作，请参见 [通过部署ACK虚拟节点组件创建ECI Pod](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/deploy-the-virtual-node-controller-and-use-it-to-create-elastic-container-instance-based-pods#task-1443354 "")。

- 已通过kubectl连接Kubernetes集群。具体操作，请参见 [通过kubectl工具连接集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/obtain-the-kubeconfig-file-of-a-cluster-and-use-kubectl-to-connect-to-the-cluster#task-ubf-lhg-vdb "")。

- 已开通阿里云对象存储（OSS）服务和存储空间（Bucket）。具体操作，请参见 [开通OSS服务](https://help.aliyun.com/zh/oss/getting-started/activate-oss#task-njz-hf4-tdb "") 和 [控制台创建存储空间](https://help.aliyun.com/zh/oss/getting-started/create-buckets-6#task-u3p-3n4-tdb "")。


## 使用限制

本功能与ACK弹性调度功能冲突，暂不支持同时使用。关于弹性调度功能的更多信息，请参见 [自定义弹性资源优先级调度](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-priority-based-resource-scheduling "")。

## 步骤一：上传测试数据到OSS Bucket

1. 创建一个2 GB的测试文件，本文以 [test](https://storage.googleapis.com/bert_models/2019_05_30/wwm_uncased_L-24_H-1024_A-16.zip) 为例。

2. 将测试文件上传到阿里云OSS对应的Bucket。



您可以通过OSS提供的客户端工具ossutil上传数据。具体操作，请参见 [安装ossutil](https://help.aliyun.com/zh/oss/developer-reference/install-ossutil#concept-303829 "")。


## 步骤二：创建Dataset和JindoRuntime

当K8s和OSS环境配置完毕后，您只需要花费几分钟即可完成Dataset和JindoRuntime环境的部署。

1. 使用以下内容，创建secret.yaml文件。



在创建Dataset之前，您可以创建如下YAML文件，保存OSS的`fs.oss.accessKeyId`和`fs.oss.accessKeySecret`。

















```plaintext
apiVersion: v1
kind: Secret
metadata:
     name: access-key
stringData:
     fs.oss.accessKeyId: ****
     fs.oss.accessKeySecret: ****
```

2. 执行以下命令，部署Secret。

















```plaintext
kubectl create -f secret.yaml
```

3. 使用以下内容，创建dataset.yaml文件。



YAML文件中包含以下两部分信息：



   - `Dataset`：描述远端存储数据集和UFS的信息。

   - `JindoRuntime`：启动一个JindoFS的集群来提供缓存服务。


```plaintext
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: serverless-data
spec:
  mounts:
  - mountPoint: oss://<oss_bucket>/<bucket_dir>
    name: demo
    path: /
    options:
      fs.oss.endpoint: <oss_endpoint>
    encryptOptions:
      - name: fs.oss.accessKeyId
        valueFrom:
          secretKeyRef:
            name: access-key
            key: fs.oss.accessKeyId
      - name: fs.oss.accessKeySecret
        valueFrom:
          secretKeyRef:
            name: access-key
            key: fs.oss.accessKeySecret
---
apiVersion: data.fluid.io/v1alpha1
kind: JindoRuntime
metadata:
  name: serverless-data
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: MEM
        volumeType: emptyDir
        path: /dev/shm
        quota: 5Gi
        high: "0.95"
        low: "0.7"
```

部分参数说明如下：

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| `mountPoint` | 表示挂载UFS的路径，路径格式为`oss://<oss_bucket>/<bucket_dir>`。路径中不需要包含Endpoint信息。例如：oss://mybucket/path/to/dir。<br>如果您使用单挂载点，可以将`path`设置为`/`。 |
| `fs.oss.endpoint` | 表示OSS Bucket的Endpoint信息，配置您的公网或私网地址。<br>配置私网地址可以提高数据访问性能，但是需要您的K8s集群所在区域和OSS区域相同。例如您的Bucket在杭州Region，则公网地址为`oss-cn-hangzhou.aliyuncs.com`，私网地址为`oss-cn-hangzhou-internal.aliyuncs.com`。 |
| `fs.oss.accessKeyId` | 表示OSS Bucket的AK ID信息，有权限访问Bucket。 |
| `fs.oss.accessKeySecret` | 表示OSS Bucket的AK ID密钥信息，有权限访问Bucket。 |
| `replicas` | 表示创建JindoRuntime缓存Worker的数量。 |
| `mediumtype` | 缓存类型。仅支持HDD（机械硬盘）、SSD（固态硬盘）和MEM（内存）三种类型。<br>关于mediumtype的推荐配置，请参见 [策略二：选择缓存介质](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/best-practices-for-optimizing-fluid-data-caching-strategies#eR0Ay "")。 |
| `volumeType` | 缓存介质存储卷类型。仅支持emptyDir和hostPath两种类型，默认为hostPath类型。<br>   - 如果使用内存或本地存储的系统盘作为缓存介质，推荐选择emptyDir类型，避免节点上缓存数据残留，进而影响节点可用性。<br>     <br>   - 如果使用本地存储的数据盘作为缓存介质，可使用hostPath类型，并配置path指定为宿主机上数据盘的挂载路径。<br>     <br>关于volumeType的推荐配置，请参见 [策略二：选择缓存介质](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/best-practices-for-optimizing-fluid-data-caching-strategies#eR0Ay "")。 |
| `path` | 表示缓存路径，目前只支持单个路径。 |
| `quota` | 表示缓存最大容量。例如100 Gi表示最大可用100 GiB。 |
| `high` | 表示存储容量上限。 |
| `low` | 表示存储容量下限。 |

**重要**

数据访问模式默认为只读模式，如果您想使用读写模式，请参考 [配置数据集访问模式](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/configure-the-access-mode-of-a-dataset "")。

4. 执行以下命令，部署JindoRuntime和Dataset。

















```plaintext
kubectl create -f dataset.yaml
```

5. 执行以下命令，查看Dataset的部署情况。

















```plaintext
kubectl get dataset serverless-data
```







预期输出：

















```plaintext
NAME              UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
serverless-data   1.16GiB          0.00B    5.00GiB          0.0%                Bound   2m8s
```





由预期输出得到，`PHASE`为`Bound`，表示Dataset部署成功。

6. 执行以下命令，查看JindoRuntime的部署情况。

















```plaintext
kubectl get jindo serverless-data
```







预期输出：

















```plaintext
NAME              MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
serverless-data   Ready          Ready          Ready        2m51s
```





由预期输出得到，`FUSE`为`Ready`，表示JindoRuntime部署成功。


## （可选）步骤三：数据预热

预先加热数据可以提升首次数据的访问性能。如果您希望在首次访问数据时得到更好的性能体验，建议您使用该功能。

1. 使用以下内容，创建dataload.yaml文件。

















```plaintext
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
     name: serverless-data-warmup
spec:
     dataset:
       name: serverless-data
       namespace: default
     loadMetadata: true
```

2. 执行以下命令，部署Dataload。

















```plaintext
kubectl create -f dataload.yaml
```

3. 执行以下命令，查看数据预热的进度。

















```plaintext
kubectl get dataload
```







预期输出：

















```plaintext
NAME                     DATASET           PHASE      AGE     DURATION
serverless-data-warmup   serverless-data   Complete   2m49s   45s
```





由预期输出得到，数据预热耗时为`45s`。

4. 执行以下命令，查看缓存结果。

















```plaintext
kubectl get dataset
```







预期输出：

















```plaintext
NAME              UFS TOTAL SIZE   CACHED    CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
serverless-data   1.16GiB          1.16GiB   5.00GiB          100.0%              Bound   5m20s
```





由预期输出得到，未进行数据预热时，`CACHED`为`0.0%`，数据预热后，`CACHED`为`100.0%`。


## 步骤四：创建Job类型应用容器访问OSS

您可以通过创建应用容器来使用JindoFS加速服务，或者提交机器学习作业来体验相关功能。本文以创建一个Job类型应用容器访问OSS数据服务为例进行说明。

1. 使用以下内容，创建job.yaml文件。







创建ECI应用Pod



创建ACS应用Pod

































```yaml
apiVersion: batch/v1
kind: Job
metadata:
     name: demo-app
spec:
     template:
       metadata:
         labels:
           alibabacloud.com/fluid-sidecar-target: eci
           alibabacloud.com/eci: "true"
       spec:
         containers:
        - name: demo
          image: debian:buster
          args:
            - -c
            - du -sh /data && time cp -r /data/ /tmp
          command:
            - /bin/bash
          volumeMounts:
            - mountPath: /data
              name: demo
      restartPolicy: Never
      volumes:
        - name: demo
          persistentVolumeClaim:
            claimName: serverless-data
backoffLimit: 4
```

为应用Pod添加`alibabacloud.com/fluid-sidecar-target=eci`标签，声明应用Pod将以ECI弹性容器实例方式运行。应用Pod创建时，Fluid会自动将该应用Pod转换为ECI弹性容器实例中可运行的方式，用户无需感知。

**重要**

   - 在ACS应用容器中访问Fluid缓存中的数据要求ack-fluid版本为1.0.11及以上，请确保集群内ack-fluid版本已满足要求。

   - 在ACS应用容器中访问Fluid缓存中的数据依赖于ACS Pod特权能力，请 [提交工单](https://smartservice.console.aliyun.com/service/create-ticket) 开启。


```yaml
apiVersion: batch/v1
kind: Job
metadata:
name: demo-app
spec:
template:
    metadata:
      labels:
        alibabacloud.com/fluid-sidecar-target: acs
        alibabacloud.com/acs: "true"
        alibabacloud.com/compute-qos: default
        alibabacloud.com/compute-class: general-purpose
    spec:
      containers:
        - name: demo
          image: debian:buster
          args:
            - -c
            - du -sh /data && time cp -r /data/ /tmp
          command:
            - /bin/bash
          volumeMounts:
            - mountPath: /data
              name: demo
      restartPolicy: Never
      volumes:
        - name: demo
          persistentVolumeClaim:
            claimName: serverless-data
backoffLimit: 4
```

为应用Pod添加`alibabacloud.com/fluid-sidecar-target=acs`标签，声明应用Pod将会使用ACS算力运行。应用Pod创建时，Fluid会自动将该应用Pod转换为ACS环境中可运行的方式，用户无需感知。

2. 执行以下命令，创建应用容器。

















```plaintext
kubectl create -f job.yaml
```

3. 执行以下命令，查看启动日志。

















```plaintext
kubectl  logs demo-app--1-7zqdm  -c demo
```







预期输出：

















```plaintext
real    0m1.760s
user    0m0.002s
sys     0m0.740s
```





由预期输出得到，文件拷贝时间`real`为`0m1.760s`。使用无缓存模式 [加速Job应用数据访问](https://help.aliyun.com/zh/ack/cloud-native-ai-suite/user-guide/accelerate-jobs-1#task-2233378 "")，文件拷贝时间为`0m23.644s`。缓存模式相比无缓存模式，速度提升了约14倍。


## 步骤五：清理环境

当您不再使用数据访问功能时，请及时清理环境。

1. 执行以下命令，删除应用容器。

















```plaintext
kubectl delete job demo-app
```

2. 执行以下命令，删除Dataset。

















```plaintext
kubectl delete dataset serverless-data
```