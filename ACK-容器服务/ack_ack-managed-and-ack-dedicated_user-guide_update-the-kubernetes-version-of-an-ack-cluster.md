### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-cluster-overview/)[升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-clusters/)手动升级集群

# 手动升级ACK集群

更新时间：2025-07-30 07:54:51

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-clusters/)[下一篇：自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

操作入口

升级控制面

1\. 前置检查

2\. 执行升级

3\. 升级后验证

升级节点池

1\. 前置检查

2\. 配置升级策略并执行升级

3\. 升级后验证

相关文档

为避免过期版本存在的安全和稳定性风险，请及时升级集群。集群升级包括控制面升级和节点池升级。

**重要**

升级集群前，请确保已参见 [升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-clusters/ "") 了解升级流程、升级方式和注意事项。

## **操作入口**

您可以先升级控制面，再升级节点池。升级控制面之前，请确保节点的kubelet和容器运行时版本与控制面版本保持匹配，避免引发升级失败或业务中断。例如，如控制面版本为1.32，而节点的版本为1.31，则需将节点的版本升级至1.32后，才能将控制面升级至1.33。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**运维管理** \> **集群升级**。

3. 在 **集群升级** 页面选择可升级的 **目标版本**，按照页面提示完成升级。


## 升级控制面

### 1\. 前置检查

控制面升级前置检查包括检查废弃API、组件兼容性、集群状态等。

> 1.20及以上版本的集群会检查当前版本是否使用了 [废弃API](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-check-items-and-suggestions-on-how-to-fix-cluster-issues#section-bff-eip-5xe "")。检查结果不影响升级流程，仅作为提示信息。建议在升级前完成修复，避免影响下一版本集群的正常运行。

在 **集群升级** 页面单击 **前置检查**，提前扫描集群升级可能存在的潜在风险。检查完成后，在 **前置检查结果** 区域查看检查结果。示例如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1746783571/p986430.png)

- 结果正常：升级检查成功，继续执行升级。

- 结果异常：不影响当前集群的运行及集群状态。请参见解决方案完成修复。更多信息，请参见 [集群检查项及修复方案](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-check-items-and-suggestions-on-how-to-fix-cluster-issues "")。


### 2\. 执行升级

> 耗时：ACK托管集群、ACK Serverless集群由ACK托管升级，约5分钟；ACK专有集群的Master节点需逐一串行升级，每个节点约8分钟。

前置检查处理完成后，单击 **立即升级**，按照页面提示进行控制面的升级。

控制面升级后，新扩容节点的版本也将遵循控制面版本。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0946783571/p986452.png)

### 3\. 升级后验证

控制面完成升级后，建议检查如下内容：

![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) 控制面升级成功，在集群列表查看集群版本时已更新至新版本。

![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) API Server和核心组件状态正常。

![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) 业务应用运行正常。

![对](<Base64-Image-Removed>) 可正常创建Pod。

![对](<Base64-Image-Removed>) 可正常添加节点。

## **升级节点池**

控制面升级完成后，请尽快在业务低峰期完成节点池升级，包括节点kubelet和容器运行时升级。

### 1\. 前置检查

节点池升级前置检查包括检查节点状态、系统资源、磁盘状态、网络环境等。

在 **节点池升级** 页面的节点池列表，单击目标节点池对应的 **升级**，然后在页面下方单击 **前置检查**，提前扫描升级过程中可能存在的风险。检查完成后，在 **前置检查结果** 区域查看检查结果。

![image](<Base64-Image-Removed>)

- 结果正常：升级检查成功，继续执行升级。

- 结果异常：不影响当前集群的运行及集群状态。请参见 [集群检查项及修复方案](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-check-items-and-suggestions-on-how-to-fix-cluster-issues "") 及控制台提示完成修复。


### **2\.** 配置升级策略并执行升级

> 耗时：取决于节点分批情况。原地升级每批次约5～10分钟；替盘升级（不涉及快照）约8分钟，具体时长受排水情况影响；如需创建快照，升级需等待快照结束后执行，快照创建时间受数据量影响。

参见下表配置升级策略，然后单击 **立即升级**，按照页面提示进行节点池的升级。

| **配置项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **配置项** | **说明** |
| 版本信息 | kubelet 和容器运行时的当前版本及可升级版本。 |
| **升级节点** | 可升级所有节点，也可先升级部分节点，观测无误后再陆续完成升级。 |
| **升级方式** | - **原地升级**：直接在原节点上更新替换所需的组件。不替换系统盘，也不会重新初始化节点，原节点的数据不受影响。<br>  <br>- **替盘升级**：通过替换节点系统盘的方式重新初始化节点。节点的实例属性（如节点名称、实例ID、IP等）不发生改变，但节点系统盘上的数据将被删除。额外挂载到该节点上的数据盘不受影响。<br>  <br>  <br>  > 可参见 [参考信息：原地升级和替盘升级](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates#6bb86c60557cq "") 了解升级逻辑和流程说明。 |
| **批量升级策略** | - **每批次执行最多节点数**：ACK同一时间只升级一个节点池，节点池内部根据此配置执行分批升级。如需暂停后重新恢复升级，依然遵循该分批策略。批次节点数递增：1、2、4、8……直至达到最大并行数，之后每批均按最大并行数执行。<br>  <br>  <br>  > 例如：最大并行数为4时，批次节点数依次为1、2、4、4、4……详细说明请参见 [参考信息：原地升级和替盘升级](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates#6bb86c60557cq "")。<br>  <br>- **自动暂停策略**：节点升级过程中的暂停策略。如选择 **不暂停** 时，还可配置 **每批次间隔时间**，即每个升级批次之间是否需要时间间隔或间隔的时长（5～120分钟）。<br>  <br>- **自动快照**：如节点系统盘上有重要业务数据，可选择是否在升级节点池前为节点创建 [快照](https://help.aliyun.com/zh/ecs/user-guide/snapshot-overview "")，以便进行节点数据的备份和恢复。<br>  <br>  <br>  <br>  **重要**<br>  <br>  <br>  <br>  <br>  <br>  - 替盘升级时建议开启自动快照。<br>    <br>  - 使用快照将产生 [快照计费](https://help.aliyun.com/zh/ecs/snapshots-1 "")， [创建快照耗时](https://help.aliyun.com/zh/ecs/user-guide/create-a-snapshot "") 会动态变化。快照默认保留7天，升级后若快照无需使用，请及时 [删除快照](https://help.aliyun.com/zh/ecs/user-guide/delete-a-snapshot-1 "")。 |

### **3\.** 升级后验证

节点池完成升级后，建议检查如下内容：

![对](<Base64-Image-Removed>) 节点升级成功，且在节点详情页面查看kubelet和containerd版本时已更新至新版本。

![对](<Base64-Image-Removed>) Pod调度正常。

![对](<Base64-Image-Removed>) 业务应用运行正常。

## 相关文档

- 关于升级集群前和升级过程中可能遇到的常见问题，请参见 [常见问题](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-clusters/#23f9ffb1f9i37 "")。

- ACK对Kubernetes版本支持的机制，请参见 [ACK版本发布说明](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/support-for-kubernetes-versions/ "")。

- 自1.24版本起不再支持将Docker作为内置容器运行时，升级至1.24及更高版本时需要 [将节点容器运行时从Docker迁移到containerd](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/change-the-container-runtime-from-docker-to-containerd "")。

- 自1.30版本起不再支持CentOS和Alibaba Cloud Linux 2，可转而使用其他支持中的 [操作系统](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-os-images/ "")。

- 您也可以启用集群自动升级功能，降低版本运维压力，请参见 [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "")。