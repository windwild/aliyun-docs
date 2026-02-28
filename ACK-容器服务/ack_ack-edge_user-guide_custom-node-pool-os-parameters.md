### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/) [ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/) [操作指南](https://help.aliyun.com/zh/ack/ack-edge/user-guide/) [节点池管理](https://help.aliyun.com/zh/ack/ack-edge/user-guide/overview-of-cell-based-management-at-the-edge/) [云端节点池管理](https://help.aliyun.com/zh/ack/ack-edge/user-guide/cloud-node-pool-management/) [节点池运维](https://help.aliyun.com/zh/ack/ack-edge/user-guide/node-pool-o-and-m/) 管理节点池OS参数

# 自定义节点池OS参数

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：自定义节点池kubelet配置](https://help.aliyun.com/zh/ack/ack-edge/user-guide/customize-the-kubelet-configurations-of-a-node-pool)[下一篇：边缘节点池管理](https://help.aliyun.com/zh/ack/ack-edge/user-guide/edge-node-pool-management)

该文章对您有帮助吗？

反馈

当Linux系统的OS参数默认配置无法满足业务需求，您希望对集群节点进行个性化调整时，您可以在节点池维度自定义节点的OS参数配置，以调优系统性能。自定义OS参数后，系统将按批次变更节点配置。节点池中已有节点将即时生效，新增节点也会使用新配置。

## **使用说明**

本功能仅支持1.28及以上版本的 [ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/ "")、 [ACK专有集群（已停止新建）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-dedicated-cluster/ "")、 [ACK Edge集群](https://help.aliyun.com/zh/ack/ack-edge/user-guide/create-an-ack-edge-cluster-1 "")。如需升级集群，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster "")。

## **注意事项**

- 动态修改OS节点配置有可能会造成节点上已存在的Pod发生配置变更，从而触发Pod重建。请在使用前确保应用的高可用。

- 不恰当的OS参数调整会改变Linux内核的运作方式，可能导致节点性能恶化或不可用，从而对业务产生影响。请在修改前深入了解待修改参数的作用，并在生产环境操作前进行充分测试。


## **配置节点池OS参数**

您可以在节点池维度配置sysctl参数和Transparent Hugepage（THP）参数。这些参数均可通过修改配置文件的方式配置； [THP参数](https://help.aliyun.com/zh/ack/ack-edge/user-guide/custom-node-pool-os-parameters#598abe9500zht "") 和 [部分sysctl参数](https://help.aliyun.com/zh/ack/ack-edge/user-guide/custom-node-pool-os-parameters#10156b175blw6 "") 还支持通过控制台或OpenAPI配置。

### **通过控制台或OpenAPI配置**

## 控制台

自定义OS参数后，系统将按批次变更节点配置。配置变更后，节点池中已有节点将即时生效，新增节点也会使用新配置。自定义OS参数生效时会改变已有节点的OS参数配置，可能会对业务产生一定影响。请在业务低峰期操作。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**节点管理** \> **节点池**。

3. 在节点池列表的 **操作** 列，单击目标节点池对应的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3151252471/p931554.png)\> **OS 配置**。

4. 仔细阅读当前页面上的注意事项，单击 **\+ 自定义参数** 选择需要配置的参数，指定待升级的节点，设置 **每批次的最大并行数**（最大为10），然后单击 **提交**，按照页面指引完成操作。

配置 **每批次的最大并行数** 后，OS配置将按批次对节点生效。执行过程中，您可以在 **事件记录** 区域查看进度，并控制执行过程（暂停、继续、取消等）。您可以使用暂停功能对已升级的节点进行验证。暂停时，正在配置的节点会继续完成执行，未执行的节点在任务继续前不会被执行自定义配置。







**重要**

请尽快完成自定义配置任务。处于暂停状态的任务将在7天后自动取消，相关的事件和日志信息也会被清理。


## OpenAPI

除控制台外，您也可以通过 [ModifyNodePoolNodeConfig](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/developer-reference/api-cs-2015-12-15-modifynodepoolnodeconfig "") 接口自定义OS参数。

### **通过配置文件配置**

ACK允许将自定义参数写入至`/etc/sysctl.d/99-user-customized.conf`，该文件是节点初始化和重启时预留的可供自定义配置的文件。写入到该配置文件的 sysctl 参数会在节点重启时优先生效，覆盖操作系统默认值和通过节点池自定义 sysctl 配置功能写入的参数值。

**重要**

调整 sysctl 参数会改变 Linux 内核的运作方式，可能导致节点性能恶化或不可用，影响业务正常运行。请在操作前请充分评估变更风险。

- 对于节点池中的存量节点，可 [登录节点](https://help.aliyun.com/zh/ecs/user-guide/connect-to-instance "") 修改该自定义参数配置文件，同时手动执行`sysctl -p /etc/sysctl.d/99-user-customized.conf`命令使配置生效。

- 对于节点池未来扩容的节点，可将对自定义参数配置文件的写入脚本配置到节点池实例预自定义数据中，以确保新增节点可默认使用这些自定义参数值。方式如下。

在节点池配置中的 **实例预自定义数据** 中配置`echo '${sysctl_key}=${sysctl_value}' > /etc/sysctl.d/99-user-customized.conf`（`${sysctl_key}`和`${sysctl_value}`需替换实际值），将自定义配置写入`/etc/sysctl.d/`目录下的配置文件。


> 操作入口，请参见 [创建和管理节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool "")。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4761029471/p964850.png)


## **sysctl参数列表**

**说明**

- 下表中的 **默认值** 指通过ACK初始化节点池时ACK默认设置的值。

- 下列参数的取值范围请参见 [Linux Kernel sysctl参数](https://www.kernel.org/doc/Documentation/sysctl/fs.txt) 文档。

- 对于暂未支持通过控制台或 OpenAPI 配置的参数，以及未在表中列出的参数，您可以参见 [通过配置文件配置](https://help.aliyun.com/zh/ack/ack-edge/user-guide/custom-node-pool-os-parameters#5098c3887a2c5 "") 进行修改。


|     |     |     |     |
| --- | --- | --- | --- |
| **字段名称** | **说明** | **默认值** | **是否支持控制台或OpenAPI配置** |
| fs.aio-max-nr | 异步I/O操作的最大数量。 | 65536 | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |
| fs.file-max | 系统级别能够打开的最大文件句柄数。 | 2097152 | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |
| fs.inotify.max\_user\_watches | 单用户能够创建的inotify监视的最大数量。 | 524288 | ![对](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1215833561/p442272.png) |
| fs.nr\_open | 每个进程能够打开的文件描述符数的最大数量。<br>> 此值应小于fs.file-max的取值 | 1048576 | ![对](<Base64-Image-Removed>) |
| kernel.pid\_max | 系统可分配的最大PID数量。 | 4194303 | ![对](<Base64-Image-Removed>) |
| kernel.threads-max | 系统可创建的最大线程数量。 | 504581 | ![对](<Base64-Image-Removed>) |
| net.core.netdev\_max\_backlog | 接口接收数据包的速度快于内核的处理速度时，可以在INPUT端排队的数据包的最大数量。 | 16384 | ![对](<Base64-Image-Removed>) |
| net.core.optmem\_max | 每个网络套接字允许的最大辅助缓冲区（Ancillary Buffer）大小，以字节为单位。 | 20480 | ![对](<Base64-Image-Removed>) |
| net.core.rmem\_max | 每个网络套接字接收缓冲区的最大大小，以字节为单位。 | 16777216 | ![对](<Base64-Image-Removed>) |
| net.core.wmem\_max | 每个网络套接字发送缓冲区的最大大小，以字节为单位。 | 16777216 | ![对](<Base64-Image-Removed>) |
| net.core.wmem\_default | 每个网络套接字发送缓冲区的默认大小，以字节为单位。 | 212992 | ![对](<Base64-Image-Removed>) |
| net.ipv4.tcp\_mem | TCP栈可以使用的内存量，以内存页（大小通常为4KB）为单位。该参数由三个整数值组成，分别表示低水位、压力水位和最高水位，必须严格按照顺序设置。 | 根据系统总内存动态计算 | ![对](<Base64-Image-Removed>) |
| net.ipv4.neigh.default.gc\_thresh1 | ARP缓存中保留的最少条目数。缓存中的条目数量低于此值时，系统不会执行垃圾收集。 | 系统预设置 | ![对](<Base64-Image-Removed>) |
| net.ipv4.neigh.default.gc\_thresh2 | ARP缓存中的最大条目数，为软限制，即缓存中的条目数量达到此值时，系统会开始考虑执行垃圾收集，但不会立即强制执行，而会等待5秒延迟。 | 1024 | ![对](<Base64-Image-Removed>) |
| net.ipv4.neigh.default.gc\_thresh3 | ARP缓存中要保留的最大条目数，为硬限制，即缓存中的条目数量达到此值时，系统会立即执行垃圾收集。如果缓存中的条目数量一直超过此值，系统会不断进行清理。 | 8192 | ![对](<Base64-Image-Removed>) |
| user.max\_user\_namespaces | 单个用户支持创建的 User Namespace 数量上限。 | 0 | ![对](<Base64-Image-Removed>) |
| kernel.softlockup\_panic | 发生软锁定时，内核会触发Panic并重启系统，以快速恢复系统状态。 | 1 | ![错](<Base64-Image-Removed>) |
| kernel.softlockup\_all\_cpu\_backtrace | 检测到软锁定时，捕获所有CPU的调试信息，便于问题诊断。 | 1 | ![错](<Base64-Image-Removed>) |
| vm.max\_map\_count | 限制单个进程可拥有的最大内存映射区域数量，防止内存过度使用。 | 262144 | ![错](<Base64-Image-Removed>) |
| net.core.somaxconn | 设置Socket监听队列的最大连接数，控制并发连接处理能力。 | 32768 | ![错](<Base64-Image-Removed>) |
| net.ipv4.tcp\_wmem | 配置TCP连接发送缓冲区的最小值（minimum）、默认值（default）和最大值（maximum）。单位：字节。<br>此设置直接影响TCP连接的网络吞吐量和内存占用。 | 4096 12582912 16777216 | ![错](<Base64-Image-Removed>) |
| net.ipv4.tcp\_rmem | 配置TCP接收缓冲区的最小值（minimum）、默认值（default）和最大值（maximum）。单位：字节。<br>此设置直接影响TCP连接的网络吞吐量和内存占用。 | 4096 12582912 16777216 | ![错](<Base64-Image-Removed>) |
| net.ipv4.tcp\_max\_syn\_backlog | 限制SYN队列中未完成三次握手的连接请求数量。 | 8096 | ![错](<Base64-Image-Removed>) |
| net.ipv4.tcp\_slow\_start\_after\_idle | 控制TCP连接在长时间空闲后是否重新使用慢启动算法。 | 0 | ![错](<Base64-Image-Removed>) |
| net.ipv4.ip\_forward | 启用IPv4数据包转发功能，允许系统作为路由器转发数据包。 | 1 | ![错](<Base64-Image-Removed>) |
| net.bridge.bridge-nf-call-iptables | 使桥接设备在二层转发时应用iptables三层规则，以确保网络安全策略生效。 | 1 | ![错](<Base64-Image-Removed>) |
| fs.inotify.max\_user\_instances | 限制单个用户可创建的inotify监视器数量，防止资源耗尽。 | 16384 | ![错](<Base64-Image-Removed>) |
| fs.inotify.max\_queued\_events | 设置内核队列中可缓存的文件系统事件数量。 | 16384 | ![错](<Base64-Image-Removed>) |
| fs.may\_detach\_mounts | 允许内核在挂载点仍被进程访问时将其从命名空间中安全分离，避免整个命名空间被锁定。 | 1 | ![错](<Base64-Image-Removed>) |

## **THP参数列表**

透明大页THP（Transparent Huge Pages）是Linux内核中的一个通用特性，可以自动将小页面（通常为4 KB）合并成大页面（通常为2 MB或更大），以减少内存访问页表项PTE（Page Table Entries）大小和访问次数，同时减轻了TLB（Translation Lookaside Buffer）缓存的压力，提高内存访问的效率。

**说明**

- 以下参数均支持通过控制台或OpenAPI配置。

- 根据操作系统及其内核版本的不同，下列参数的默认值不同。更多信息，请参见 [Linux Kernel THP参数](https://docs.kernel.org/admin-guide/mm/transhuge.html) 文档。


|     |     |     |
| --- | --- | --- |
| **字段名称** | **说明** | **可取值** |
| transparent\_enabled | 是否在系统全局开启THP功能。 | - always：系统全局开启THP功能。<br>  <br>- never：系统全局关闭THP功能。<br>  <br>- madvise：仅在通过`madvise()`进行系统调用，并且设置了`MADV_HUGEPAGE`标记的内存区域中开启THP功能。 |
| transparent\_defrag | 是否开启透明大页THP相关的碎片整理配置。启用后，如果内存中的小页能够被合并成一个大页，可以减少页表的大小并提高系统的性能。 | - always：当系统分配不出透明大页时，暂停内存分配行为，总是等待系统进行内存的直接回收和内存的直接整理。内存回收和整理结束后，如果存在足够的连续空闲内存，则继续分配透明大页。<br>  <br>- defer：当系统分配不出透明大页时，转为分配普通的4 KB页。同时，系统会唤醒`kswapd`守护进程进行内存的后台回收，唤醒`kcompactd`守护进程进行内存的后台整理。一段时间后，如果存在足够的连续空闲内存，`khugepaged`守护进程可将此前分配的4 KB页合并为2 MB的透明大页。<br>  <br>- madvise：仅在通过`madvise()`进行系统调用，并且设置了`MADV_HUGEPAGE`标记的内存区域中，内存分配行为等同于always。<br>  <br>  其余部分的内存分配行为仍然为：发生缺页异常时，转为分配普通的4 KB页。<br>  <br>- defer+madvise：仅在通过`madvise()`进行系统调用，并且设置了`MADV_HUGEPAGE`标记的内存区域中，内存分配行为等同于always。其余部分的内存分配行为仍然为defer。<br>  <br>- never：禁止碎片整理。 |
| khugepaged\_defrag | `khugepaged`是一个内核线程，主要负责管理和整理大页，以减少内存碎片化并提高性能。它会监视系统中的大页面，当发现分散的大页时，尝试将它们合并成更大的页，以提高内存利用率和性能。<br>由于该操作会在内存路径中执行锁定操作，且`khugepaged`守护进程可能会在错误的时间启动扫描和转换大页的操作，因此存在影响应用性能的可能性。 | - 0：关闭khugepaged碎片整理功能。<br>  <br>- 1：`khugepaged`守护进程会在系统空闲时周期性唤醒，尝试将连续的4 KB页合并成2 MB的透明大页。 |
| khugepaged\_alloc\_sleep\_millisecs | 当透明大页THP分配失败时，`khugepaged`守护进程进行下一次大页分配前需要等待的时间，以避免短时间内连续发生大页分配失败。单位为毫秒。 | 请参见 [khugepaged碎片整理](https://help.aliyun.com/zh/alinux/support/performance-tuning-method-related-to-transparent-large-page-thp-in#95896c5cd73ld "")。 |
| khugepaged\_scan\_sleep\_millisecs | `khugepaged`守护进程每次唤醒的时间间隔。单位为毫秒。 |
| khugepaged\_pages\_to\_scan | `khugepaged`守护进程每次唤醒后扫描的内存页数量。单位为页。 |