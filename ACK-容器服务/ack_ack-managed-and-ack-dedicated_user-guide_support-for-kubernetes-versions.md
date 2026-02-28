### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-cluster-overview/)版本说明

# Kubernetes版本概览及机制

更新时间：2025-11-06 01:54:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-cluster-overview/)[下一篇：Kubernetes 1.34](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-34-release-notes)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

版本发布

版本号说明

版本生命周期

版本支持策略

过期版本的风险

过期版本的强制升级

常见问题

相关文档

Kubernetes社区每4个月左右发布一个次要版本（minor version），容器服务 Kubernetes 版会跟随上游的发版节奏进行Kubernetes版本的迭代，包括版本的创建、维护以及停止维护。本文介绍ACK的Kubernetes版本支持机制，包括版本发布和支持情况、版本生命周期说明、版本支持策略等。

## 版本发布

ACK托管集群支持的Kubernetes版本详细信息如下。

| **版本** | **状态** | **ACK发布时间** | **ACK停止维护时间** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **版本** | **状态** | **ACK发布时间** | **ACK停止维护时间** |
| [1.34](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-34-release-notes "") | 已发布 | 2025年09月 | 2026年09月30日<br>> 支持周期为1年。 |
| [1.33](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-33-release-notes "") | 已发布 | 2025年05月 | 2026年05月31日<br>> 支持周期为1年。 |
| [1.32](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-32-release-notes "") | 已发布 | 2025年01月 | 2026年01月31日<br>> 支持周期为1年。 |
| [1.31](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-31-release-notes "") | 已发布 | 2024年09月 | 2025年09月30日<br>**重要**<br>自1.31版本起，ACK扩展了Kubernetes版本的支持范围，从仅支持偶数次要版本（例如1.28、1.30等）扩展至支持所有次要版本。同时，对于1.31及之后的次要版本，ACK支持周期调整为1年。 |
| [1.30](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-30-release-notes "") | 已发布 | 2024年06月 | 2026年06月30日 |

**展开查看停止维护版本**

**重要**

过期版本集群存在安全隐患和稳定性风险，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster#task-1664343 "") 或 [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "") 及时升级集群至维护中的版本。

|     |     |     |     |
| --- | --- | --- | --- |
| **版本** | **状态** | **ACK发布时间** | **ACK停止维护时间** |
| [1.28](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-28-release-notes "") | 停止维护 | 2023年10月 | 2025年10月31日 |
| [1.26](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-26-release-notes "") | 停止维护 | 2023年04月 | 2025年04月 |
| [1.24](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-24-release-notes#task-2249356 "") | 停止维护 | 2022年09月 | 2024年09月 |
| [1.22](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-22-release-notes#concept-2170736 "") | 停止维护 | 2021年12月 | 2023年10月 |
| [1.20](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-20-release-notes#task-2070898 "") | 停止维护 | 2021年04月 | 2023年04月 |
| [1.18](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-18-release-notes#concept-1964323 "") | 停止维护 | 2020年09月 | 2022年09月 |
| [1.16](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-16-release-notes#task-2434487 "") | 停止维护 | 2020年02月 | 2022年06月 |
| 1.14 | 停止维护 | 2019年08月 | 2021年07月 |
| [1.12](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-1-12-release-notes#concept-270435 "") | 停止维护 | 2019年03月 | 2020年12月 |

## **版本号说明**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8502142671/CAEQWhiBgMC1lMDruBkiIDk2NzQwMTAwOWQ5NTRmM2ZiNmE0MGIwZmRhMDYxZTAw4828145_20241217173930.084.svg)

ACK Kubernetes版本的表达方式为 **x.y.z-aliyun.n**。x.y.z表示社区Kubernetes版本，其中，x表示主要版本（major version），y表示次要版本（minor version），z表示补丁版本（patch version）；n表示阿里云补丁版本（ACK patch version）。

## **版本生命周期**

在Kubernetes社区发布新的次要（minor version）版本后，ACK会对该版本进行风险评估和一致性测试，通常在社区发布补丁版本两周内开放新版本的创建和升级。

在Kubernetes社区针对次要版本发布新的补丁版本后，ACK会根据补丁所修复问题的风险等级判定是否发布该补丁版本的升级更新。对于高危安全漏洞的补丁版本，ACK通常在24小时内完成评估验证，而后开放新版本的创建和升级。

## 版本支持策略

- **集群创建**

ACK支持创建最近的三个Kubernetes次要版本的集群。例如，最近的三个次要版本为1.33、1.32、1.31。ACK支持1.33版本后，1.30版本不再开放创建功能，过期补丁版本也不再开放创建功能。

当某个次要版本发布了新的补丁版本后，低版本的补丁版本不再开放创建功能。例如，1.30.7发布后，1.30.1不再支持新建。

- **集群升级**

版本升级功能目前仅支持逐级升级版本，不支持跨多个版本升级，且不支持回退版本。例如，如果您的ACK集群Kubernetes版本为1.31，期望升级至1.33，则需进行两次集群升级，即先升级到1.32，再升级到1.33。

对于补丁版本，集群升级仅支持最新补丁版本的升级，不支持过期补丁版本的升级。

- **技术支持**

对于ACK仍在维护的版本，ACK提供的技术支持包括答疑、在线指导、排查、排错等工作。


## **过期版本的风险**

过期版本集群存在安全隐患和稳定性风险。集群版本过期后，将无法享受新Kubernetes版本支持的功能特性及缺陷修复，无法获得及时有效的技术支持，面临无法修复安全漏洞的风险。

您需要升级集群到安全稳定的版本。

- [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")：逐级升级版本至最新版本。您可以通过指定待升级节点、设置每批次可升级的最大节点数、配置升级间隔和暂停策略等配置控制升级节奏。

- [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "")：开启集群自动升级功能，选择合理的升级频次，保持集群周期性的自动升级。


## **过期版本的强制升级**

Kubernetes社区对于超出维护期限的版本不披露CVE风险且不提供修复补丁，过期版本的潜在安全风险可能无法被及时发现和修复。由于ACK集群主要采用托管架构，这些安全风险不仅会对您的集群产生影响，也可能会影响阿里云的整体安全。因此，ACK不允许集群长期处于过期状态，会采取强制升级方式将集群升级至安全稳定的版本。

集群版本过期后，ACK不会立即进行强制升级，建议手动升级集群到安全稳定版本。执行强制升级操作前，ACK会至少提前一个月通过短信、邮件、站内信等方式通知。

强制升级集群版本时，会升级如下内容：

- 升级 [集群组件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/component-overview "")（只会升级与更高集群版本存在兼容性问题的部分组件）。

- 升级集群控制面。

- 升级节点池和节点。


针对以下情况，不会进行强制升级，需手动升级：

- 集群类型为ACK专有集群。建议迁移至ACK托管集群Pro版，请参见 [热迁移ACK专有集群至ACK托管集群Pro版](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/hot-migration-from-ack-dedicated-clusters-to-ack-pro-clusters "")。

- 集群版本为1.22且使用Docker容器运行。需迁移至containerd运行时，请参见 [将节点容器运行时从Docker迁移到containerd](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/change-the-container-runtime-from-docker-to-containerd "")。

- 使用的ACK Nginx Ingress组件版本较老，与高版本ACK存在兼容性问题。组件说明请参见组件变更记录 [Nginx Ingress Controller](https://help.aliyun.com/zh/ack/product-overview/nginx-ingress-controller "")。


## **常见问题**

#### **我能不能不升级集群版本，永远停留在一个版本？**

不能。过期版本的潜在安全风险不仅会对您的集群产生影响，也可能影响阿里云的整体安全。ACK不允许集群长期处于过期状态，会采取强制升级方式将集群升级至安全稳定的版本。

请及时升级集群版本（ [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")），以便享受ACK提供的最新功能特性和更好的技术支持。升级前，请参见 [版本发布说明](https://help.aliyun.com/document_detail/2361875.html "") 了解各版本的特性变更和注意事项。推荐您启用 [自动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/automatically-upgrade-an-ack-cluster "") 功能，保持集群的周期性自动升级。

#### **我的集群版本很老了，如何快速升级我的集群版本？**

您可以通过以下两种方案来实现。

- 方案一：逐级升级版本。每次升级后，请观察集群业务是否持续稳定运行，再进行下一次升级。具体操作，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。

- 方案二：新建一个最新版本的集群，将集群应用逐步迁移至新集群，再下线老集群。关于如何创建并配置集群，请参见 [创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/ "")。


#### **ACK支持跨多个版本升级吗？**

ACK不支持跨次要版本升级，您需要逐级升级版本。此外，升级集群控制面前，请确保集群节点的版本与控制面版本相同。

#### **1.22版本的集群升级至1.24时需要切换Docker至containerd，如何操作？**

ACK在1.24及更高版本中不再支持将Docker作为内置容器运行时，您需要将节点容器运行时从Docker迁移到containerd。

您可以通过节点池升级功能在原节点池完成运行时切换，也可以新建containerd节点池完成轮转迁移。具体操作，请参见 [将节点容器运行时从Docker迁移到containerd](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/change-the-container-runtime-from-docker-to-containerd "")。

#### **ACK如何保证集群升级的稳定性？**

一个ACK集群由控制面和节点池两部分组成。

- 控制面升级：ACK提供升级前的前置检查功能，对废弃API、组件兼容性、功能配置兼容性、控制面组件等进行检查。检查结果不影响集群中业务的正常运行。如检查结果异常，可参见控制台获取修复建议。更多信息，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。

- 节点池升级：节点池升级包括kubelet和containerd的升级。ACK提供升级前的前置检查功能，检查节点状态、系统资源、磁盘状态、网络环境等。检查结果不影响集群中业务的正常运行。如检查结果异常，可参见控制台获取修复建议。

您也可以自行配置升级策略，例如通过指定待升级节点、设置每批次可升级的最大节点数、配置升级暂停策略等配置控制升级节奏。如节点系统盘上有重要业务数据，也可以在升级节点池前为节点创建 [快照](https://help.aliyun.com/zh/ecs/user-guide/snapshot-overview "")。更多信息，请参见 [升级节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates "")。


#### **集群升级有哪些注意事项？**

- 集群升级不支持回滚。建议您先升级测试环境，验证通过后再升级生产环境。您也可以在升级过程中 [优先升级某些节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates#289a37543e2ke "") 进行验证。

- 每个Kubernetes版本支持的组件版本、功能特性、功能废弃情况不同，请参见不同版本的 [版本发布说明](https://help.aliyun.com/document_detail/2361875.html "")。

- 遵循 [控制面升级注意事项](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster#bedb60902bxau "")。

- 遵循 [节点池升级注意事项](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/node-pool-updates#7ac2e16ab0yx1 "")。


## **相关文档**

- 集群升级说明，包括升级影响、升级流程、注意事项、升级方式等，请参见 [升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/upgrade-clusters/ "")。

- ACK支持的操作系统类型及镜像版本，请参见 [操作系统镜像发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-os-images "")。

- ACK提供的CVE漏洞修复说明及对应解决方案，请参见 [CVE漏洞修复](https://help.aliyun.com/zh/ack/product-overview/security-bulletins/ "")。

- 集群升级前置检查的检查项和废弃API说明，请参见 [集群检查项及修复方案](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/cluster-check-items-and-suggestions-on-how-to-fix-cluster-issues "")。

- ACK托管集群Pro版在基础版的基础上，针对企业大规模生产环境进一步增强了可靠性、安全性，并且提供可赔付的SLA，如需迁移，请参见 [热迁移ACK托管集群基础版至ACK托管集群Pro版](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/hot-migration-from-ack-standard-clusters-to-ack-pro-clusters "")。