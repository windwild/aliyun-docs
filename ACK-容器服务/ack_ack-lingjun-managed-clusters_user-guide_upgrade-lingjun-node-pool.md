### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 升级灵骏节点池

# 升级灵骏节点池

更新时间：2025-03-12 05:05:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：【产品公告】关于停止维护Nginx Ingress Controller组件的公告](https://help.aliyun.com/zh/ack/product-overview/product-announcement-announcement-on-end-of-maintenance-for-nginx-ingress-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

功能说明

操作步骤

相关操作

参考信息：原地升级

原地升级流程

常见问题

每个批次升级大概需要多长时间？

升级过程中业务是否受影响？

节点池升级后支持版本回退吗？

如何升级不属于任何节点池的集群节点？

灵骏节点池的升级包含前置检查和执行升级。前置检查提示影响升级的风险。前置检查通过后您可以升级kubelet和容器运行时。

## 使用限制

- 灵骏节点池仅支持升级有节点的节点池。

- 灵骏节点池暂不支持更新操作系统。

- 灵骏节点池暂不支持通过替换系统盘方式升级以及升级前为节点建立快照。


## 功能说明

节点池升级功能支持升级以下组件。

| **组件名称** | **升级说明** | **升级操作** | **注意事项** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **组件名称** | **升级说明** | **升级操作** | **注意事项** |
| kubelet | 如果kubelet发布了新的版本，您可以将该节点池内节点的kubelet升级到与控制平面相同的版本。可用的升级版本以当前集群的管控版本为准。 | 采取原地升级的方式升级kubelet组件。 | 升级kubelet版本的注意事项，请参见 [升级集群](https://help.aliyun.com/zh/ack/ack-lingjun-managed-clusters/user-guide/upgrade-ack-lingjun-cluster "")。 |
| 容器运行时 | 如果容器运行时发布了新的版本，您可以升级节点池内节点到新版本的容器运行时。 | - Docker升级到containerd新版本时，先排水，再卸载Docker，最后安装containerd，不会替换系统盘。<br>  <br>- containerd升级到containerd新版本时，采用原地升级，不排水。<br>  <br>**说明**<br>不支持Docker升级到Docker新版本。 | 运行时升级过程中可能造成Pod Probe、Lifecycle Hook失败，也可能会出现Pod原地重启情况。 |

## 操作步骤

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点池**。

3. 在 **节点池列表** 页面中，选择目标灵骏节点池，选择 **更多** > **升级**。

4. 选择需要升级的操作对象，单击 **前置检查**。





**说明**





如果前置检查执行失败或者存在警告项，请参见 [异常检查项修复方案](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-check-items-and-suggestions-on-how-to-fix-cluster-issues#section-f4g-7bd-f51 "") 或通过单击 **查看详情** 进入 **检查报告** 页面进行排查。

5. 选择需要升级的操作对象，单击 **开始升级**。您可以通过设置 **批量升级策略** 的参数定义每批次最大并行升级的节点数。


## 相关操作

升级时，在 **事件轮转** 区域，您可以进行如下操作：

- 暂停或继续：在升级到某个阶段时，如果您需要暂停或继续升级，您可以单击 **暂停** 或 **继续**。



  - 集群暂停状态为节点池升级的中间状态，建议您不要在此时对集群进行操作，并尽快完成升级过程。处于中间状态的集群会在7日之后关闭升级过程，同时清理一切升级相关的事件和日志信息。

  - 单击 **暂停** 后，已完成升级的节点的kubelet和容器运行时在版本升级后不支持版本回退。


- 取消：在升级到某个阶段时，如果您需要取消升级，您可以单击 **取消**。



单击 **取消** 后，已完成升级的节点的kubelet和容器运行时在版本升级后不支持版本回退。


![节点池升级暂停](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2550483761/p551015.png)

## **参考信息：原地升级**

### 原地升级流程

节点池升级过程会根据设置的最大并行数，依次对节点进行升级，最大并行数不会超过节点总数的10%。每个批次的升级节点数为：1、2、4、8……直至达到最大并行数，达到最大并行数后，每个批次都按最大并行数的节点进行升级。例如最大并行数设置为4，那么第一批升级的节点个数为1，第二批升级的节点个数为2，第三批升级的节点个数为4，以后每批的升级节点个数均为4。

![图片1.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7631668961/p712281.png)

## 常见问题

### **每个批次升级大概需要多长时间？**

原地升级每批次升级时间大约为5min。

### **升级过程中业务是否受影响？**

原地升级时，Pod不会重启，不会影响业务。

### 节点池升级后支持版本回退吗？

目前，kubelet和容器运行时在版本升级后不支持版本回退。

### **如何升级不属于任何节点池的集群节点？**

在节点池功能上线前创建的老集群，会存在不属于任何节点池的游离节点。您可以将游离节点迁移到一个节点池后，对节点池进行升级。关于如何迁移游离节点至节点池，请参见 [迁移游离节点至节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-free-nodes-to-a-node-pool "")。