### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[存储](https://help.aliyun.com/zh/ack/product-overview/storage-2/)storage-operator

# storage-operator

更新时间：2026-01-21 03:32:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：csi-compatible-controller](https://help.aliyun.com/zh/ack/product-overview/csi-compatible-controller)[下一篇：alicloud-disk-controller（已弃用）](https://help.aliyun.com/zh/ack/product-overview/alicloud-disk-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

变更记录

2026年01月

2025年10月

2025年08月

2025年05月

2025年03月

2024年09月

2024年07月

2024年05月

2024年01月

2023年12月

2023年10月

2023年07月

2023年02月

2022年11月

2022年09月

2022年08月

2022年07月

2022年05月

2022年04月

2022年03月

2021年12月

2021年09月

2021年08月

2021年06月

2021年03月

storage-operator 提供存储卷自动扩容、云盘在线变配、存储资源监控 **、** 数据预填充（创建预填充OSS数据的高性能存储卷）等存储功能，以提升在ACK集群中使用阿里云存储资源的运维效率。本文介绍storage-operator组件的使用说明以及变更记录。

## 组件介绍

storage-operator 是ACK提供的用于自动化管理存储组件生命周期的运维工具，集成了多种高级存储功能，以提升存储资源的运维效率。storage-operator默认以 Deployment 形式部署在集群中，提供以下功能模块。

- 存储卷扩容：负责云盘、NAS存储卷的自动扩容。

可通过添加Feature Gate`Expander=false`来关闭。

- 云盘变配：负责变更云盘配置。

可通过添加Feature Gate`DiskVolumeUpgradeControl=false`来关闭。

- 有状态应用迁移：负责有状态应用的跨可用区迁移。

可通过添加Feature Gate`ApplicationMigrationAcrossAZ=false`来关闭。

- 数据预填充：支持在创建PV时，指定一个OSS Bucket作为数据源。系统会自动将OSS中的数据预先填充到新创建的高性能存储卷（如CPFS）中。适用于AI训练、大数据分析等场景下，将冷数据从OSS预热到高性能文件系统以加速计算任务。

可通过添加Feature Gate`VolumePopulator=true`来启用。启用后，系统将默认创建 `ack-volume-populator` 命名空间，用于运行数据预填充期间产生的临时PVC与Pod。


## 变更记录

### 2026年01月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.35.1 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.35.1-4b60408 | - 新增支持VolumePopulator功能，可 [将 OSS 数据按需预填充到高性能存储卷](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/prefetch-oss-data-into-high-performance-volumes-on-demand "")。 | 2026年01月19日 | 此次升级不会对业务造成影响。 |

### 2025年10月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.33.2 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.33.2-f32da36 | - 修改基础镜像为distroless镜像<br>  <br>- 修复偶发的协程并发访问冲突问题 | 2025年10月17日 | 此次升级不会对业务造成影响。 |

### 2025年08月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.33.1 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.33.1-cb82bad | - storage-cnfs组件拆分为托管版cnfs-controller组件，单独上线组件中心。出于兼容性考虑，升级或安装本组件时将自动为您安装cnfs-controller组件。<br>  <br>- 去除子组件管理模式，组件现内置原storage-auto-expander和storage-controller组件的功能，无需再通过ConfigMap来管理。<br>  <br>- 支持通过FeatureGate的形式来控制各功能是否打开。 | 2025年8月20日 | 此次升级不会对业务造成影响。 |
| v1.32.10 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.32.10-aa189c8 | 优化storage-auto-expander组件内存占用 | 2025年08月8日 | 此次升级不会对业务造成影响。 |

### 2025年05月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.32.9 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.32.9 | 提升组件storage-cnfs、storage-controller安全性，使用安全加固模式访问元数据。 | 2025年05月14日 | 此次升级不会对业务造成影响。 |

### 2025年03月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.32.5 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.32.5 | 修复组件storage-cnfs的问题。 | 2025年03月31日 | 此次升级不会对业务造成影响。 |
| v1.32.4 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.32.4 | - 下线storage-monitor组件，相关功能由storage-cnfs组件代替。<br>  <br>- storage-cnfs组件支持NAS存储卷容量监控，并在可用容量低于15%时在PVC上发布告警事件。<br>  <br>- 修复storage-auto-expander组件NAS存储卷重复扩容问题。 | 2025年03月12日 | 此次升级不会对业务造成影响。 |

### 2024年09月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.31.1 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.31.1 | - 更新storage-controller组件基础镜像alpine版本至3.18。<br>  <br>- storage-monitor组件支持byte级别的NAS存储卷容量监控。<br>  <br>- 修复storage-auto-expander组件问题，更新基础镜像alpine版本至3.18。 | 2024年09月26日 | 此次升级不会对业务造成影响。 |

### 2024年07月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.30.2 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.30.2 | 优化组件日志。 | 2024年07月12日 | 此次升级不会对业务造成影响。 |

### 2024年05月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.30.1 | registry-{{regionID}}.ack.aliyuncs.com/acs/storage-operator:v1.30.1 | 例行更新依赖，关闭老版本的TLS以提升系统安全性。 | 2024年05月31日 | 此次升级不会对业务造成影响。 |

### 2024年01月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.28.2-be0cf84-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.28.2-be0cf84-aliyun | 修复组件storage-controller的问题。 | 2024年01月17日 | 此次升级不会对业务造成影响。 |

### 2023年12月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.28.1-4e62141-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.28.1-4e62141-aliyun | - 修复storage-monitor组件问题。<br>  <br>- 更新组件Baseimage为Alpine。 | 2023年12月25日 | 此次升级不会对业务造成影响。 |

### 2023年10月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.26.2-1de13b6-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.26.2-1de13b6-aliyun | - 更新storage-controller版本至v1.26.2-639bc21-aliyun，支持ESSD云盘有状态应用跨可用区迁移。<br>  <br>- 更新storage-cnfs版本至v1.24.39-0e24b92-aliyun，支持为创建的OSS Bucket开启版本控制，支持为NAS存储卷自动创建关联的StorageClass。 | 2023年10月25日 | 此次升级不会对业务造成影响。 |

### 2023年07月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.26.1-50a1499-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.26.1-50a1499-aliyun | 修复若干监控和快照问题。 | 2023年07月02日 | 此次升级不会对业务造成影响。 |

### 2023年02月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.24.102-b1cfa3d-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.24.102-b1cfa3d-aliyun | 增加storage-controller组件，支持变更云盘类型。 | 2023年02月06日 | 此次升级不会对业务造成影响。 |

### 2022年11月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.24.97-3eb7acc-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.24.97-3eb7acc-aliyun | - 更新storage-snapshot-manager版本至v1.22.1-464f816-aliyun。<br>  <br>- 解决storage-snapshot-manager在有virtual-node的集群中概率性Crash的问题。 | 2022年11月02日 | 此次升级不会对业务造成影响。 |

### 2022年09月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.24.95-e2d0756-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.24.95-e2d0756-aliyun | 更新storage-cnfs-controller版本至v1.24.31-262bf31-aliyun。 | 2022年09月27日 | 此次升级不会对业务造成影响。 |

### 2022年08月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.22.91-c4d5ab4-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/csi-plugin:v1.22.91-c4d5ab4-aliyun | 增加存储指标收集。 | 2022年08月25日 | 此次升级不会对业务造成影响。 |

### 2022年07月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.22.86-041b094-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/csi-plugin:v1.22.86-041b094-aliyun | - 支持使用文件存储客户端加速特性，默认不开启。更多信息，请参见 [开启CNFS NAS计算端分布式缓存](https://help.aliyun.com/zh/ack/enable-the-distributed-caching-feature-of-the-cnfs-client#task-2232103 "")。<br>  <br>- 修复自动扩容组件中当磁盘使用量大于100%时，数组越界访问的问题。 | 2022年07月13日 | 此次升级不会对业务造成影响。 |

### 2022年05月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.22.8-aa22537-aliyun | registry.cn-{{region}}.aliyuncs.com/acs/storage-operator:v1.22.8-aa22537-aliyun | 修改云盘快照YAML文件。 | 2022年05月13日 | 此次升级不会对业务造成影响。 |

### 2022年04月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.22.0.75-5bc07f7-aliyun | registry.cn-{{region}}.aliyuncs.com/acs/storage-operator:v1.22.0.75-5bc07f7-aliyun | 支持高级云盘快照功能。 | 2022年04月14日 | 此次升级不会对业务造成影响。 |

### 2022年03月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.18.8.68-9078250-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.18.8.68-9078250-aliyun | 修复基础镜像CentOS 7的安全漏洞。 | 2022年03月16日 | 此次升级不会对业务造成影响。 |

### 2021年12月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.18.8.67-c1aef60-aliyun | registry.cn-{{regionID}}.aliyuncs.com/acs/storage-operator:v1.18.8.67-c1aef60-aliyun | 修复NAS的quota生效慢，以及自动扩容失败的问题。 | 2021年12月22日 | 此次升级不会对业务造成影响。 |

### 2021年09月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.18.8.60-a5ba617-aliyun | registry-vpc.${region}.aliyuncs.com/acs/storage-operator:v1.18.8.60-a5ba617-aliyun | - CNFS托管NAS时默认开启Quota支持自动扩容。<br>  <br>- 修复Pod调度到不可用节点的问题。<br>  <br>- 支持Pod调度到Linux及非virtual-node。<br>  <br>- 修复CNFS状态无法变更的问题。 | 2021年09月24日 | 此次升级不会对业务造成影响。 |

### 2021年08月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.18.8.55-e398ce5-aliyun | registry-vpc.${region}.aliyuncs.com/acs/storage-operator:v1.18.8.55-e398ce5-aliyun | - 支持CNFS默认创建容量型NAS。<br>  <br>- 支持CNFS默认创建的StorageClass中参数archiveOnDelete为false，删除PV时默认支持删除PV对应的子目录。<br>  <br>- 修复storage-monitor的CPU占用过高问题。 | 2021年08月16日 | 此次升级不会对业务造成影响。 |

### 2021年06月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.18.8.37-c63030b-aliyun | registry-vpc.${region}.aliyuncs.com/acs/storage-operator:v1.18.8.37-c63030b-aliyun | - 支持自动扩容能力。<br>  <br>- 支持CNFS。 | 2021年06月25日 | 此次升级不会对业务造成影响。 |

### 2021年03月

| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更内容** | **变更时间** | **变更影响** |
| v1.18.8.28-18cca7b-aliyun | registry-vpc.${region}.aliyuncs.com/acs/storage-operator:v1.18.8.28-18cca7b-aliyun | 新功能：<br>- 支持批量快照。<br>  <br>- 支持定时快照。<br>  <br>- 支持集群监控。 | 2021年03月25日 | 此次升级不会对业务造成影响。 |