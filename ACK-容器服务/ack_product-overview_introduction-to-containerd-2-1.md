### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-runtime/)[containerd运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-containerd/)containerd 2.1介绍

# containerd2.1介绍

更新时间：2025-05-28 09:23:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：containerd运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-containerd/)[下一篇：Docker运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-docker)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能特性

废弃功能和API

升级注意事项

识别废弃 API

识别Docker Schema 1镜像

升级方式

FAQ

相关文档

ACK 1.33 版本默认使用containerd 2.1。containerd 2.1在镜像安全、性能、稳定性方面均有所提升。本文介绍containerd 2.1的主要变更说明，包括功能特性变更、废弃功能、废弃API等。

## **功能特性**

> 下文仅介绍主要功能特性，详细信息请参见 [containerd发布记录](https://github.com/containerd/containerd/blob/main/docs/containerd-2.0.md)。

- 支持NRI (Node Resource Interface) 能力，已在containerd配置中默认启用。

- 支持CDI (Container Device Interface) 能力，已在containerd配置中默认启用。

- 支持Sandbox API。


## **废弃功能和API**

> 下文仅介绍主要废弃功能和API，详细信息请参见 [containerd发布记录](https://github.com/containerd/containerd/blob/main/docs/containerd-2.0.md)

- 废弃配置 registry.auths、registry.configs、registry.mirrors。建议参见 [自定义节点池containerd配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-the-containerd-configurations-of-a-node-pool "")，通过控制台自定义containerd参数。

- 不再支持Docker Schema 1镜像，例如`application/vnd.docker.distribution.manifest.v1+json` 或 `application/vnd.docker.distribution.manifest.v1+prettyjws`，拉取时会被拒绝。请参见 [识别Docker Schema 1镜像](https://help.aliyun.com/zh/ack/product-overview/introduction-to-containerd-2-1#f89612f74b85r "") 进行识别。

- `io_uring_*` 从containerd的默认Seccomp配置文件中移除。容器默认没有权限进行`io_uring_*`系统调用。

- 移除CRI v1alpha2 API。Kubernetes自1.26起开始弃用该API，containerd 2.1随之同步移除。

- 移除AUFS snapshotter。

- 移除`[plugins."io.containerd.internal.v1".tracing]`配置项。


## **升级注意事项**

- containerd 2.1不再支持CRI v1alpha2 API。如依赖该版本API，需切换至CRI v1版本API以确保兼容性。

- 建议在升级前参见 [识别废弃 API](https://help.aliyun.com/zh/ack/product-overview/introduction-to-containerd-2-1#26ab10923ffu9 "") 进行自检。您也可以在集群信息页面的左侧导航栏，选择 **运维管理** \> **集群升级**，触发 **前置检查** 以完成自动检查。

- 升级过程中，系统会进行废弃 API 检测，若检测到使用弃用 API，升级过程将中断。


### **识别废弃 API**

#### **使用 kubectl**

参见以下代码，检查集群下是否有Pod挂载了containerd 相关目录。

> 需提前安装kubectl和jq命令行工具。jq可通过`yum install jq`命令安装。

```bash
kubectl get pods --all-namespaces -o json |
jq -r '.items[] |
  select(.spec.volumes[]?.hostPath.path as $p |
    ["/", "/var", "/var/","/var/run", "/var/run/",\
     "/var/run/containerd", "/var/run/containerd/",\
     "/var/run/containerd/containerd.sock",\
     "/run", "/run/", "/run/containerd", "/run/containerd/",\
     "/run/containerd/containerd.sock"] | index($p)) |
  .metadata.namespace + "/" + .metadata.name'
```

#### **使用ctr**

若当前 containerd 实例中存在已弃用的 API，执行`ctr deprecations list`命令将列出所有废弃API。

```bash
ctr deprecations list
```

### 识别Docker Schema 1镜像

```bash
ctr --namespace k8s.io images list 'labels."io.containerd.image/converted-docker-schema1"'
```

### **升级方式**

升级至 containerd 2.1 前，请先参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "") 将集群控制面版本升级至1.33及以上版本，然后参见 [升级节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates "") 升级容器运行时版本。

## FAQ

#### **升级过程中，业务是否会受影响？**

请参见 [升级节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates "") 完成containerd版本的升级。通过此方式升级时，默认采取原地升级，容器不会重启，业务可正常运行。

#### **从containerd 1.6升级至containerd 2.1后还支持回退吗？**

不支持回退。containerd 2.1 版本引入了 shim-v3 API，不支持回退至 containerd 1.6 的 shim-v2 API。

#### **将containerd 1.6升级至containerd 2.1的过程中，节点数据会丢失吗？**

参见 [升级节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates "") 升级containerd时默认采取原地升级，containerd 2.1 仍旧使用原数据目录，不会丢失。

## 相关文档

- [containerd发布记录](https://github.com/containerd/containerd/blob/v2.0.0/RELEASES.md)

- [containerd 变更说明](https://github.com/containerd/containerd/blob/main/docs/containerd-2.0.md)

- [Kubernetes 1.33](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-33-release-notes "")

- [containerd运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-containerd/ "")