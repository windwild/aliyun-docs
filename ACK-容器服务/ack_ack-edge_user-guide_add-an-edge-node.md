### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/)[操作指南](https://help.aliyun.com/zh/ack/ack-edge/user-guide/)[节点管理](https://help.aliyun.com/zh/ack/ack-edge/user-guide/node-management-overview/)[边缘节点管理](https://help.aliyun.com/zh/ack/ack-edge/user-guide/node-management/)添加边缘节点

# 添加边缘节点

更新时间：2026-01-04 20:54:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置节点调度状态](https://help.aliyun.com/zh/ack/ack-edge/user-guide/set-node-schedulability)[下一篇：添加GPU节点](https://help.aliyun.com/zh/ack/ack-edge/user-guide/add-a-gpu-node)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

使用限制

添加节点

参数列表

相关文档

ACK Edge集群的边缘节点池支持添加多种类型的资源，例如不同地域的ECS节点，IDC节点，其他厂商云节点，以及分布在工厂、门店、车辆和船舶中的服务器节点。本文介绍如何在ACK Edge集群中的边缘节点池中添加边缘节点。

## 前提条件

已 [创建ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/user-guide/create-an-ack-edge-cluster-1#task-skz-qwk-qfb "")。

## 使用限制

- 请确保您的集群配额充足。如需添加更多节点，请[到配额平台提交申请](https://quotas.console.aliyun.com/products/csk/quotas)扩大配额。关于ACK Edge集群的配额限制，请参见 [配额与限制](https://help.aliyun.com/zh/ack/product-overview/limits#concept-gsf-w2b-5db "")。

- 添加边缘节点时会访问部分域名地址，需要节点侧网络安全组放开限制允许访问。具体信息，请参见 [公网接入的网络配置](https://help.aliyun.com/zh/ack/ack-edge/user-guide/network-configuration-for-public-network-access "")。

- 在添加边缘节点时需要选择节点操作系统，目前支持接入以下节点操作系统。




| **系统架构** | **系统版本** | **系统内核版本** | **边缘Kubernetes集群版本** |
| --- | --- | --- | --- |



|     |     |     |     |
| --- | --- | --- | --- |
| **系统架构** | **系统版本** | **系统内核版本** | **边缘Kubernetes集群版本** |
| AMD64/x86\_64 | Anolis7.9、Anolis8.6 | 4.19.X | ≥1.16.9-aliyunedge.1 |
| AMD64/x86\_64 | Alibaba Cloud Linux 2.1903 | 4.19.X | ≥1.20.11-aliyunedge.1 |
| AMD64/x86\_64 | Alibaba Cloud Linux 3 | 5.10.X | ≥1.20.11-aliyunedge.1 |
| AMD64/x86\_64 | CentOS 7.4、CentOS 7.5、CentOS 7.6、CentOS 7.7、CentOS 7.8、CentOS 7.9 | 3.10.X | 1.12.6-aliyunedge.1≤集群版本≤1.30.7-aliyun.1 |
| AMD64/x86\_64 | CentOS 8.0、CentOS 8.2 | 4.18.X | 1.18.8-aliyunedge.1≤集群版本≤1.30.7-aliyun.1 |
| AMD64/x86\_64 | Ubuntu 16.04 | 4.4.X | 1.18.8-aliyunedge.1≤集群版本≤1.30.7-aliyun.1 |
| AMD64/x86\_64 | Ubuntu 18.04 | 4.15.X | 1.12.6-aliyunedge.1≤集群版本≤1.30.7-aliyun.1 |
| AMD64/x86\_64 | Ubuntu 18.04 | 5.4.X | ≥1.16.9-aliyunedge.1 |
| AMD64/x86\_64 | Ubuntu 18.04 | 5.11.X | ≥1.18.8-aliyunedge.1 |
| AMD64/x86\_64 | Ubuntu 20.04 | 5.4.X | ≥1.18.8-aliyunedge.1 |
| AMD64/x86\_64 | Ubuntu 20.04、Ubuntu 22.04 | 5.15.X | ≥1.26.3-aliyun.1 |
| AMD64/x86\_64 | Ubuntu 24.04 | 6.8.X | ≥1.30.7-aliyun.1 |
| AMD64/x86\_64 | Red Hat Enterprise Linux 8.8、Red Hat Enterprise Linux 8.10 | 4.18.X | 1.26.3-aliyun.1≤集群版本≤1.30.7-aliyun.1 |
| AMD64/x86\_64 | Kylin V10 | 4.19.X | ≥1.26.3-aliyun.1 |
| AMD64/x86\_64 | UnionTech OS Server 20 | 4.19.X | ≥1.26.3-aliyun.1 |
| AMD64/x86\_64 | Red Hat Enterprise Linux 9.3 | 5.14.X | ≥1.30.7-aliyun.1 |
| Arm64 | CentOS 8.0 | 4.19.X | ≥1.14.8-aliyunedge.1 |
| Arm64 | Ubuntu 18.04 | 4.9.X | 1.14.8-aliyunedge.1≤集群版本≤1.30.7-aliyun.1 |
| Arm64 | Ubuntu 18.04 | 4.19.X | ≥1.14.8-aliyunedge.1 |
| Arm64 | Ubuntu 20.04 | 5.10.X | ≥1.22.15-aliyunedge.1 |

- 若您想在集群中添加GPU节点，添加方式请参见 [添加GPU节点](https://help.aliyun.com/zh/ack/ack-edge/user-guide/add-a-gpu-node "")。


## 添加节点

1.26及以上版本集群

1.26以下版本集群

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点池**。

3. 在 **节点池** 页面，选择目标节点池右侧 **操作** 列的 **![图标](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0072161761/p537429.png) \> 添加已有节点**。

4. 进入添加现有边缘节点页面，配置云边缘通信参数和高级选项。



**说明**





如果以下界面参数无法满足需求，您可以参考下文 [参数列表](https://help.aliyun.com/zh/ack/ack-edge/user-guide/add-an-edge-node#section-640-7ra-xed "") 修改生成脚本中edgeadm的参数完成配置。





![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6710513471/p934460.png)


|     |     |     |
| --- | --- | --- |
| **分类** | **配置项** | **说明** |
| 云边缘通信配置 | Token 有效时间 | 表示脚本的有效时间。默认值为1小时。<br>如果您需要长时间使用同一个脚本做批量添加，可以适当增加脚本的生效时间。 |
|  |  |
| 启用静默模式 | 是否启用静默模式。<br>在边缘节点接入执行过程中，某些步骤可能需要您介入做出判断，例如是否需要将节点上已存在的运行时重新安装。<br>默认为是，表示所有的问题回答自动回复`yes`，自动推进流程。 |
| 高级选项 | 节点标签（Labels） | 为待接入的节点添加标签。<br>节点池支持给节点池内所有节点添加标签的功能。如果该`label`与节点池上的`label key`名称冲突，节点池上定义的`label`优先级更高。 |
| 污点（Taints） | 为待接入的节点添加污点。 |
| 注释 | 为待接入的节点添加注解。<br>如果该`annotations`与节点池上的`annotations`名称冲突，节点池上定义的`annotations`优先级更高。 |
| 自动完成时间同步 | 开启后，表示由edgeadm自动完成时间同步。 |
| 节点网络接口 | 指定用于获取节点IP和容器网络通信使用的主机网卡名称。如设置为空，将自动选择默认路由对应的网卡。 |
| 组件下载自 | 节点上系统组件镜像的下载来源。默认为公网。<br>通过私网下载时，节点需已接入专线节点池。 |
| 运行时工作目录 | 指定运行时的工作目录，该配置在`manageRuntime`为`true`时才会生效。<br>containerd运行时的默认路径为/var/lib/containerd。 |

5. 配置完成后单击 **确定**，进入提交结果页面，单击 **复制**，到您的边缘节点上粘贴并执行该脚本。

添加边缘节点成功的结果如下图所示。

![接入成功](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8888162661/p433986.png)


1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点池**。

3. 在 **节点池** 页面，选择目标节点池右侧 **操作** 列的![图标](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0072161761/p537429.png) **>** **添加已有节点**。

4. 进入添加节点页面，默认通过 **手动添加** 方式添加现有实例。





**说明**





目前手动添加的方式支持添加云上ECS节点、云上ENS节点和非云节点。







1. 单击 **下一步** 进入实例信息页面，您可以在此处填写节点接入配置，具体的配置参数，请参见 [参数列表](https://help.aliyun.com/zh/ack/ack-edge/user-guide/add-an-edge-node#title-7bk-955-nc0 "")。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1823698271/p859287.png)



      **说明**





      **脚本有效时间** 的默认值是1小时，如果您需要长时间使用同一个脚本做批量添加，可以适当增加脚本的生效时间。当 **脚本有效时间** 配置为0小时，表示脚本永远生效。

2. 配置完成后单击 **下一步**，进入 **添加完成** 页面，单击 **复制**，到您的边缘节点上粘贴并执行该脚本。


添加边缘节点成功的结果如下图所示。

![接入成功](<Base64-Image-Removed>)

## 参数列表

如果控制台上已有参数无法满足需求，您可以根据以下参数列表修改生成脚本中edgeadm的参数完成配置。

| **参数** | **与控制台对应的参数** | **参数说明** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **与控制台对应的参数** | **参数说明** | **描述** |
| `quiet` | 启用静默模式 | 是否启用静默模式。在节点接入执行过程中，某些步骤可能需要您介入做出判断，例如是否需要将节点上已存在的运行时重新安装。 | - `true`：默认值，假设所有的问题回答自动回复`yes`，自动推进流程。<br>  <br>- `false`：节点接入过程中，可能需暂停以获取您的确认，节点接入过程可能中断。 |
| `manageRuntime` | 无 | 是否由`edgeadm`检测并安装运行时。 | - `true`：默认值，检测并安装运行时。<br>  <br>- `false`：不安装运行时，需要用户在节点上提前安装好运行时。 |
| `nodeNameOverride` | 无 | 设置节点名。 | - `""`：默认值，表示使用主机名。<br>  <br>- `"XXX"`：表示指定节点名为XXX。<br>  <br>- `"*"`：表示随机生成6位字符串。<br>  <br>- `"*.XXX"`：表示随机生成6位字符串+XXX后缀。 |
| `allowedClusterAddons` | 无 | 需要安装的组件列表。普通节点需要配置为\["kube-proxy","flannel","coredns"\]。 | `["kube-proxy","flannel","coredns"]`：默认值。 |
| `gpuVersion` | 无 | 表示要接入的节点是否为GPU节点，默认为空。<br>当前支持的GPU版本，请参见 [GPU型号](https://help.aliyun.com/zh/ack/ack-edge/user-guide/add-a-gpu-node#3fc96a390ehkl "")。 | `""`：默认值，表示不作为GPU节点接入。<br>ACK Edge集群从1.26版本开始，接入Nvidia GPU时，无需配置`gpuVersion`参数直接接入，由接入工具自动检查GPU型号并安装相关组件。 |
| `labels` | 节点标签（Labels） | 表示接入时节点要加的标签。节点池支持给节点池内所有节点添加标签的功能。如果该`label`与节点池上的`label key`名称冲突，节点池上定义的`label`优先级更高。 | `{}`：表示不添加任何标签。 |
| `annotations` | 注释 | 表示接入时给节点加的注解。如果该`annotations`与节点池上的`annotations`名称冲突，节点池上定义的`annotations`优先级更高。 | `{}`：表示不添加任何注解。 |
| `taints` | 污点（Taints） | 表示接入时给节点加上的污点。 | `[]` |
| `nodeIface` | 无 | 指定主机网卡，该参数有两个作用：<br>- kubelet从指定的网卡获取节点IP信息。<br>  <br>- 设置容器网络插件flannel使用的网卡。 | `""`：如果设为空，kubelet将按如下顺序获取节点IP。<br>- 在/etc/hosts中寻找与主机名同名的记录。<br>  <br>- 默认路由所在的网络接口的IP地址。<br>  <br>flannel将使用节点默认路由所在的网卡。 |
| ` runtimeRootDir` | 运行时工作目录 | 指定运行时的工作目录，该配置在`manageRuntime`为`true`时才会生效。 | `""`：默认值。<br>- 当运行时为Docker时，默认路径为/var/lib/docker。<br>  <br>- 当运行时为Containerd时，默认路径为/var/lib/containerd。 |
| ` imageRepoType` | 组件下载自 | 指定节点上系统组件镜像的下载来源。 | - `""`：默认值，表示专线节点池的节点从内网下载镜像，普通节点池的节点从公网下载镜像。<br>  <br>- `public`：表示从公网下载镜像。<br>  <br>- `private`：表示从内网下载镜像（节点已接入专线节点池）。 |
| `selfHostNtpServer` | 自动完成时间同步 | 是否手动完成时间同步。 | - `false`：默认值，表示由edgeadm自动完成时间同步。<br>  <br>- `true`：表示不需要自动时间同步，已经手动完成时间同步。 |
| `flannelIface` | 节点网络接口 | flannel使用的网卡名（不推荐使用，可以使用 **nodeIface** 参数代替）。 | `""`：默认值，flannel使用节点默认路由所使用的网卡。 |
| `enableIptables` | 无 | edgehub是否开启iptables优化（不推荐使用，1.22后已废弃）。 | `false`：表示不启用iptables。 |

## **相关文档**

- 如果您在添加边缘节点时遇到问题，请参见 [诊断边缘节点问题](https://help.aliyun.com/zh/ack/ack-edge/user-guide/diagnose-edge-node-problems "")。

- 如果您需要移除不使用的边缘节点，请参见 [移除边缘节点](https://help.aliyun.com/zh/ack/ack-edge/user-guide/remove-edge-nodes "")。

- 如果您需要实现边缘节点的自主管理，请参见 [设置边缘节点自治](https://help.aliyun.com/zh/ack/ack-edge/user-guide/configure-node-autonomy "")。配置后，当云边网络断开时，边缘节点上的业务仍然可以持续稳定地运行。