### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[存储](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/csi-overview-1/)[本地存储卷](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-17/)HostPath数据卷

# 使用HostPath数据卷

更新时间：2026-02-11 03:23:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：本地存储卷](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-17/)[下一篇：LocalVolume数据卷](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-local-volumes)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作原理

流程介绍

使用方式

适用范围

方式一：在Pod中直接挂载HostPath

方式二：通过PV和PVC挂载HostPath

应用于生产环境

常见问题

HostPath 数据卷可以将宿主机（节点）上的文件或目录直接挂载到 Pod 中，使Pod能够直接读写节点的文件系统，适用于需要读取节点日志、访问特定配置文件，在开发环境中快速共享数据等场景。

## 工作原理

### **流程介绍**

Pod被调度到目标节点后，该节点的kubelet会在容器启动前，执行 [HostPath](https://kubernetes.io/zh/docs/concepts/storage/volumes/#hostpath) 的挂载操作。kubelet会根据`hostPath`字段中定义的挂载模式（`type`），对主机路径（`path`）进行验证和准备。

- `DirectoryOrCreate`：检查主机`path`是否存在。如不存在，则自动创建一个权限为0755的空目录，其属主和属组与 kubelet 一致。

- `Directory`：检查主机`path`是否存在且必须是一个目录。如果不是，Pod将启动失败。

- `FileOrCreate`：检查主机`path`是否存在。如不存在，则自动创建一个权限为0644的空文件，其属主和属组与 kubelet 一致。

- `File`：检查主机`path`是否存在且必须是一个文件。如果不是，Pod将启动失败。


验证通过后，kubelet会将主机`path`绑定挂载到容器中。后续容器对挂载点的所有读写操作，都将直接作用于主机文件系统。

### **使用方式**

- [在Pod中直接挂载HostPath](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-hostpath-volumes#06deec4b2d86k "")：在Pod的`volumes`中直接定义`hostPath`。配置简单，但存储与应用强耦合，不建议用于需要长期维护或未来可能变更存储的生产应用。

- [通过PV和PVC挂载HostPath](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-hostpath-volumes#c159f69599wpn "")：通过独立 PV 定义`hostPath`，再由Pod通过PVC申请。存储与应用解耦，可独立管理底层存储，无需改动应用Pod配置。


## **适用范围**

本功能仅支持ECS节点。不支持异构计算节点（GPU节点、灵骏节点），以及Serverless算力（ECI、ACS）。

## **方式一：在Pod中直接挂载HostPath**

1. 创建`pod-hostpath-direct.yaml`。


> 该示例将节点的`/data`目录挂载到Pod内的`/test`目录。
















```yaml
apiVersion: v1
kind: Pod
metadata:
     name: test-pod
spec:
     containers:
  - image: anolis-registry.cn-zhangjiakou.cr.aliyuncs.com/openanolis/nginx:1.14.1-8.6
    name: test-container
    volumeMounts:
    - mountPath: /test
      name: test-volume
volumes:
  - name: test-volume
    hostPath:
      # 指定主机上的路径
      path: /data
      # 指定挂载模式
      type: DirectoryOrCreate
```

2. 部署Pod。















```bash
kubectl apply -f pod-hostpath-direct.yaml
```

3. 验证挂载结果。

可通过在Pod内部创建文件，然后在节点上检查该文件是否存在，来验证挂载是否成功。

1. 在Pod内创建文件。

      在Pod的`/test`目录（挂载点）下创建一个`test.txt`文件。















      ```bash
      kubectl exec test-pod -- sh -c 'echo "This file was created from within the Pod." > /test/test.txt'
      ```

2. 获取Pod所在的节点名称。















      ```bash
      NODE_NAME=$(kubectl get pod test-pod -o jsonpath='{.spec.nodeName}')
      echo "Pod is running on node: $NODE_NAME"
      ```

3. 在节点上验证文件。

      [登录节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-management/#ac78e94553p3v "")，执行`ls /data`命令，检查主机的`/data`目录下是否存在刚刚创建的文件。

      输出中包括`test.txt`文件，表明HostPath数据卷挂载成功。

## **方式二：** 通过PV和PVC挂载HostPath

1. 创建`pv-pvc-hostpath.yaml`。


> 该示例创建了一个指向主机`/data`目录的PV，一个申请该存储的PVC，以及一个使用此PVC的Pod。
















```yaml
# --- PersistentVolume 定义 ---
apiVersion: v1
kind: PersistentVolume
metadata:
     name: hostpath-pv
     labels:
       type: local
spec:
     capacity:
       storage: 10Gi
     accessModes:
    - ReadWriteOnce
hostPath:
    path: "/data"
---
# --- PersistentVolumeClaim 定义 ---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: hostpath-pvc
spec:
accessModes:
  - ReadWriteOnce
resources:
    requests:
      storage: 10Gi
# 使用selector确保PVC绑定到此前创建的PV上
selector:
    matchLabels:
      type: local
---
# --- Pod 定义 ---
apiVersion: v1
kind: Pod
metadata:
name: test-pod-pvc
spec:
containers:
    - name: test-container
      image: anolis-registry.cn-zhangjiakou.cr.aliyuncs.com/openanolis/nginx:1.14.1-8.6
      ports:
        - containerPort: 80
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: storage
volumes:
    - name: storage
      persistentVolumeClaim:
        # 引用此前定义的PVC
        claimName: hostpath-pvc
```

2. 创建PV、PVC和Pod。















```bash
kubectl apply -f pv-pvc-hostpath.yaml
```

3. 验证挂载结果。

可通过在Pod内部创建文件，然后在节点上检查该文件是否存在，验证挂载是否成功。

1. 在Pod内创建文件。


      在Pod的`/usr/share/nginx/html`目录（挂载点）下创建一个名为`test.txt`的文件。















      ```bash
      kubectl exec test-pod-pvc -- sh -c 'echo "File from PV/PVC Pod." > /usr/share/nginx/html/test.txt'
      ```

2. 获取Pod所在的节点名称。















      ```bash
      NODE_NAME=$(kubectl get pod test-pod-pvc -o jsonpath='{.spec.nodeName}')
      echo "Pod is running on node: $NODE_NAME"
      ```

3. 在节点上验证文件。

      [登录节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-management/#ac78e94553p3v "")，执行`ls /data`命令，检查主机的`/data`目录下是否存在刚刚创建的文件。

      输出中包括`test.txt`文件，表明通过PV、PVC方式挂载的HostPath数据卷运行正常。

## 应用于生产环境

- 强化安全隔离

  - 挂载为只读模式：如果应用仅需读取节点数据，请将其挂载为只读模式（`ReadOnlyMany`），以防主机文件被意外修改。

  - 遵循最小权限：避免挂载宿主机根目录（`/`）或敏感系统目录（如`/etc`、`/var`），应为HostPath使用专门目录。
- 关注节点资源

  - 监控主机磁盘：容器写入HostPath会消耗节点磁盘。对磁盘分区进行 [监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-management/#d6c83b3d48nti "") 和 [告警](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-managed-service-for-prometheus-to-monitor-an-ack-cluster#5ebd6dd0308cy "")，防止节点因磁盘耗尽而故障。

  - 评估I/O影响：对HostPath的高频读写会占用节点I/O资源，可能影响节点上其他业务Pod甚至kubelet的稳定性。应评估其性能影响。
- HostPath会将Pod与特定节点的物理存储直接绑定，导致HostPath卷的数据与节点强相关，不具备跨节点的数据持久性。

  - 不适用于需要高可用和持久化存储的有状态应用（如数据库、缓存）。

    - HostPath 卷的数据仅存在于单个节点。当 Pod 因故障或更新被重新调度到其他节点时，原有数据访问将丢失。

    - 授权 Pod 访问宿主机文件系统会打破容器的隔离边界。若配置不当（如挂载根目录 `/`）或容器自身存在漏洞，可能威胁节点安全和稳定性。
  - 不适用于只读根文件系统的节点，例如 [ContainerOS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/containeros-overview/ "")。

## 常见问题

#### **如果Pod被删除后重建，HostPath卷里的数据还在吗？**

取决于Pod被调度到哪个节点。

- 调度回同一节点：新Pod会挂载节点上完全相同的目录，可以访问所有历史数据。

- 调度到新节点：新Pod会挂载新节点上的一个空目录。数据仍留在原节点上，但新Pod无法访问。


=