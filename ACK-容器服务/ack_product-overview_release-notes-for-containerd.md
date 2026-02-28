### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/) [产品概述](https://help.aliyun.com/zh/ack/product-overview/) [产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/) [运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-runtime/) containerd运行时发布记录

# containerd运行时发布记录

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-runtime/)[下一篇：containerd 2.1介绍](https://help.aliyun.com/zh/ack/product-overview/introduction-to-containerd-2-1)

该文章对您有帮助吗？

反馈

containerd是一个工业级标准的容器运行时，可以在宿主机中管理完整的容器生命周期。containerd提供更精简、更稳定的容器运行时。本文介绍containerd运行时的变更记录。

## 使用说明

- 关于containerd运行时与其他运行时的对比详情，请参见 [containerd、安全沙箱、Docker运行时的对比](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/comparison-of-docker-containerd-and-sandboxed-container#task-2455499 "")。

- 关于containerd 2.1的功能变更、废弃特性等，请参见 [containerd 2.1介绍](https://help.aliyun.com/zh/ack/product-overview/introduction-to-containerd-2-1 "")。


## 2026年01月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 2.1.6 | 2026年01月15日 | - 依赖升级：<br>  <br>  - 升级runc至1.3.4版本。<br>    <br>  - 升级Go至1.24.11版本。 | 此次升级不会对业务造成影响。 |

## 2025年11月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 2.1.5 | 2025年11月30日 | - 依赖升级：<br>  <br>  - 升级runc至1.3.3版本。<br>    <br>  - 升级Go至1.24.9版本。<br>- 缺陷修复：<br>  <br>  - 修复containerd CVE漏洞 [CVE-2024-25621](https://github.com/containerd/containerd/security/advisories/GHSA-pwhc-rpq9-4c8w)、 [CVE-2025-64329](https://github.com/containerd/containerd/security/advisories/GHSA-m6hq-p25p-ffr2)。 | 此次升级不会对业务造成影响。 |

## 2025年10月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 2.1.4 | 2025年10月13日 | - 优化：<br>  <br>  - 添加 [nerdctl](https://github.com/containerd/nerdctl) 工具。<br>- 缺陷修复：<br>  <br>  - 修复了从部分自建镜像仓库下载镜像时会导致的死锁问题，请参见 [#12126](https://github.com/containerd/containerd/pull/12126)。<br>    <br>  - 修复运行时创建失败时IO句柄未关闭的问题，请参见 [#11885](https://github.com/containerd/containerd/pull/11885)。 | 此次升级不会对业务造成影响。 |
| 1.6.39 | 2025年10月31日 | - 依赖升级：<br>  <br>  - runc升级至1.3版本。<br>- 缺陷修复：<br>  <br>  - 修复运行时创建失败时IO句柄未关闭的问题，请参见 [#12052](https://github.com/containerd/containerd/pull/12052)。 | 此次升级不会对业务造成影响。 |

## 2025年07月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 2.1.3 | 2025年07月07日 | - 修复了在服务器未返回 Content Length 时镜像分片拉取失败的问题，请参见 [#12003](https://github.com/containerd/containerd/pull/12003)。<br>  <br>- 优化了 Transfer Service 的平台兼容性，修复了本地导入镜像和处理 Registry 错误时可能出现的问题，请参见 [#11999](https://github.com/containerd/containerd/pull/11999)、 [#12000](https://github.com/containerd/containerd/pull/12000)、 [#11979](https://github.com/containerd/containerd/pull/11979)。<br>  <br>- 修复了 `fetch` 操作无论是否需要都会为请求添加 `range` 字段的问题，请参见 [#12001](https://github.com/containerd/containerd/pull/12001)。<br>  <br>- 优化了 `fetcher` 的错误信息，包含完整的 Registry 返回错误，便于排查问题，请参见 [#11997](https://github.com/containerd/containerd/pull/11997)。 | 此次升级不会对业务造成影响。 |

## 2025年05月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 2.1.1 | 2025年05月27日 | - 功能特性<br>  <br>  - 支持NRI (Node Resource Interface) 能力，已在containerd配置中默认启用。<br>    <br>  - 支持CDI (Container Device Interface) 能力，已在containerd配置中默认启用。<br>    <br>  - 支持Sandbox API。<br>- 废弃功能和API<br>  <br>  - 废弃配置 registry.auths、registry.configs、registry.mirrors。建议参见 [自定义节点池containerd配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/customize-the-containerd-configurations-of-a-node-pool "")，通过控制台自定义containerd参数。<br>    <br>  - 不再支持Docker Schema 1镜像，例如`application/vnd.docker.distribution.manifest.v1+json` 或 `application/vnd.docker.distribution.manifest.v1+prettyjws`，拉取时会被拒绝。请参见 [识别Docker Schema 1镜像](https://help.aliyun.com/zh/ack/product-overview/introduction-to-containerd-2-1#f89612f74b85r "") 进行识别。<br>    <br>  - `io_uring_*` 从containerd的默认Seccomp配置文件中移除。容器默认没有权限进行`io_uring_*`系统调用。<br>    <br>  - 移除CRI v1alpha2 API。Kubernetes自1.26起开始弃用该API，containerd 2.1随之同步移除。 | 此次升级不会对业务造成影响。 |

## 2025年03月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.6.37 | 2025年03月03日 | - 升级Go至1.22.10版本。<br>  <br>- 升级runC至1.2.5版本。<br>  <br>- 修复容器启用tty和stdin后可能导致TTY泄漏，进而导致容器启动失败的问题。详情请参见 [#11160](https://github.com/containerd/containerd/issues/11160)。<br>  <br>- 修复同个镜像在同时进行垃圾回收（GC）和拉取时可能导致镜像拉取失败的问题。详情请参见 [#3787](https://github.com/containerd/containerd/issues/3787)。 | 此次升级不会对业务造成影响。 |
| 1.6.38 | 2025年03月31日 | - 升级Go至1.23.7版本。<br>  <br>- 修复CVE问题 [CVE-2024-40635](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2024-40635) | 此次升级不会对业务造成影响。 |

## 2024年11月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.6.36 | 2024年11月08日 | - 升级Go至1.22.7版本。<br>  <br>- 升级runC至1.1.14版本。<br>  <br>- 修复容器有概率无法停止问题。更多信息，请参见 [#10651](https://github.com/containerd/containerd/pull/10651)。 | 此次升级不会对业务造成影响。 |

## 2024年09月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.6.34 | 2024年09月09日 | - 升级Go至1.21.12版本。<br>  <br>- 升级runC至1.1.13版本。<br>  <br>- 新增`drain_exec_sync_io_timeout`参数。更多信息，请参见 [#9768](https://github.com/containerd/containerd/pull/9768)。 | 此次升级不会对业务造成影响。 |

## 2024年02月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.6.28 | 2024年02月04日 | - 修复CVE问题 [CVE-2024-21626](https://github.com/advisories/GHSA-xr7r-f8xq-vfvv)。<br>  <br>- 升级runC至v1.1.12版本（ [GHSA-xr7r-f8xq-vfvv](https://github.com/opencontainers/runc/security/advisories/GHSA-xr7r-f8xq-vfvv)）。 | 此次升级不会对业务造成影响。 |

## 2024年01月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.6.21 | 2024年01月31日 | - 升级runC至v1.1.7版本。<br>  <br>- 修复CVE问题CVE-2024-21626。 | 此次升级不会对业务造成影响。 |

## 2023年05月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.6.20 | 2023年05月17日 | - 升级至Containerd第一个正式长期稳定（long-term stable，LTS）版本的最新版本。详情请参见 [Release Notes](https://github.com/containerd/containerd/blob/v1.6.20/releases/v1.6.20.toml)。<br>  <br>- 升级Go至1.18.8版本。<br>  <br>- 修复多个CVE问题：<br>  <br>  - [CVE-2022-41717](https://nvd.nist.gov/vuln/detail/CVE-2022-41717)<br>    <br>  - [CVE-2022-41720](https://nvd.nist.gov/vuln/detail/CVE-2022-41720)<br>    <br>  - [CVE-2022-41716](https://nvd.nist.gov/vuln/detail/CVE-2022-41716)<br>    <br>  - [CVE-2022-27191](https://nvd.nist.gov/vuln/detail/CVE-2022-27191)<br>- 新增支持自定义仓库，默认使用cert.d配置自定义Host。<br>  <br>- 升级runC至v1.1.5版本。 | 此次升级不会对业务造成影响。 |

## 2022年09月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.5.13 | 2022年09月08日 | - 修复CVE问题：<br>  <br>  - [CVE-2022-24769](https://nvd.nist.gov/vuln/detail/CVE-2022-24769)<br>    <br>  - [CVE-2022-31030](https://nvd.nist.gov/vuln/detail/CVE-2022-31030)<br>- 解决当Cgroup被删除时FD泄漏的问题。<br>  <br>- 需要Unpack容器时确保MaxConcurrentDownloads最高并发下载生效。<br>  <br>- 将为Dockerfile中的Volume临时创建的Mount更改为ReadOnly。 | 此次升级不会对业务造成影响。 |

## 2022年03月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.5.10 | 2022年03月22日 | - 修复CVE问题：<br>  <br>  - [CVE-2022-23648](https://nvd.nist.gov/vuln/detail/CVE-2022-23648)<br>    <br>  - [CVE-2021-43816](https://nvd.nist.gov/vuln/detail/CVE-2021-43816)<br>    <br>  - [CVE-2021-41190](https://nvd.nist.gov/vuln/detail/CVE-2021-41190)<br>- 升级runC至1.0.3版本。修复PID泄漏时，runC管道阻塞导致的节点NotReady等问题。 | 此次升级不会对业务造成影响。 |

## 2021年08月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.4.8 | 2021年08月03日 | - 解决因负载高导致的Sandbox创建超时，进而导致IP资源泄漏的问题。<br>  <br>- 修复CVE问题： [CVE-2021-32760](https://nvd.nist.gov/vuln/detail/CVE-2021-32760)。 | 此次升级不会对业务造成影响。 |

## 2021年06月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.4.6 | 2021年06月03日 | 修复CVE问题： [CVE-2021-30465](https://nvd.nist.gov/vuln/detail/CVE-2021-30465)。 | 此次升级不会对业务造成影响。 |

## 2021年03月

|     |     |     |     |
| --- | --- | --- | --- |
| **版本号** | **变更时间** | **变更内容** | **变更影响** |
| 1.4.4 | 2021年03月16日 | 创建集群时，支持使用containerd运行时。<br>**说明** <br>containerd运行时功能处于公测阶段。 | 此次升级不会对业务造成影响。 |

## 相关文档

- [Docker运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-docker#task-2058522 "")

- [安全沙箱运行时发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-of-sandboxed-container#task-2453570 "")