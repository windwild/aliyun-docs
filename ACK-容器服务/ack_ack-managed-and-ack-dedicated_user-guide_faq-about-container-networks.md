### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[网络](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/network/)[容器网络CNI](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/container-network/)容器网络FAQ

# 容器网络FAQ

更新时间：2025-09-21 21:50:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：在ACK集群使用自定义CNI插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-a-custom-cni-plugin-in-an-ack-cluster)[下一篇：使用ACK GlobalNetworkPolicy](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/using-ack-globalnetworkpolicy)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

索引

Terway相关

Flannel相关

kube-proxy相关

IPv6相关

ACK容器网络数据链路

其他

Terway的主要网络模式有哪些？

如何区分Terway是独占ENI模式还是共享ENI模式？

如何区分Terway网络加速是DataPathv2还是IPvlan+eBPF？

Terway DataPathv2或者IPvlan+eBPF模式路由是否绕过IPVS？

已经创建的ACK集群是否支持切换网络插件？

Terway网络模式下增加了虚拟交换机后，集群无法访问公网怎么办？

手动升级了Flannel镜像版本后，如何解决无法兼容1.16以上版本集群的问题？

如何解决Pod启动后存在时延的问题？

如何让Pod访问自己暴露的服务？

如何选择Kubernetes集群Terway和Flannel网络插件？

如何规划集群网络？

ACK是否支持hostPort的端口映射？

如何查看集群的网络类型及对应的虚拟交换机？

如何查看集群中使用的云资源？

如何修改kube-proxy配置？

如何提升Linux连接跟踪Conntrack数量限制？

如何修改kube-proxy中IPVS负载均衡模式？

如何修改kube-proxy中IPVS UDP会话保持的超时时间？

如何解决IPv6双栈的部分常见问题？

Terway网络插件下交换机的IP资源不足怎么办？

Terway网络模式下，Pod分配的IP不在虚拟交换机网段中怎么办？

Terway网络模式扩容vSwitch后，依然无法分配Pod IP怎么办？

如何为Terway IPvlan集群开启集群内负载均衡？

如何在ACK中对Terway网络下的Pod指定网段加白？

为什么Pod无法ping通部分ECS节点？

为什么集群节点有NodeNetworkUnavailable污点？

为什么Pod无法正常启动，且报错no IP addresses available in range？

如何修改节点IP数量、Pod IP网段、Service IP网段？

什么场景下需要为集群配置多个路由表？

问题场景

是否支持安装和配置第三方网络插件？

为什么Pod CIDR地址不足，报错no IP addresses available in range set？

Terway网络模式支持的Pod数量是多少？

Terway DataPath V2数据面模式

如何查看Terway网络Pod生命周期？

Terway组件升级失败常见问题

Terway网络模式下，创建Pod提示找不到mac地址

问题现象

解决办法

配置集群本地域名（ClusterDomain）有哪些注意事项？

本文为您介绍使用网络插件Terway或Flannel遇到的常见问题，以及如何解决。例如，如何选择网络插件、集群是否支持安装第三方网络插件、如何规划集群网络等。

## 索引

### Terway相关

- [Terway的主要网络模式有哪些？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#1202fa6b63n16 "")

- [如何区分Terway是独占ENI模式还是共享ENI模式？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#e15ae47c6bmfs "")

- [如何区分Terway网络加速是DataPathv2还是IPvlan+eBPF？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#dc0f9801bdkzy "")

- [Terway DataPathv2或者IPvlan+eBPF模式路由是否绕过IPVS？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#3d34fd3434m4e "")

- [已经创建的ACK集群是否支持切换网络插件？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#1c068bd245jcx "")

- [Terway网络模式下增加了虚拟交换机后，集群无法访问公网怎么办？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-7hi-dnx-552 "")

- [Terway网络插件下交换机的IP资源不足怎么办？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#398bf3d07c8e2 "")

- [Terway网络模式下，Pod分配的IP不在虚拟交换机网段中怎么办？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-t4a-ene-hcq "")

- [Terway网络模式扩容vSwitch后，依然无法分配Pod IP怎么办？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-a8o-p0p-qod "")

- [如何选择Kubernetes集群Terway和Flannel网络插件？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-ylr-ln7-pfe "")

- [如何为Terway IPvlan集群开启集群内负载均衡？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-75m-g9d-3w4 "")

- [如何在ACK中对Terway网络下的Pod指定网段加白？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-4un-o1u-r7h "")

- [Terway网络模式支持的Pod数量是多少？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#6c3a27adf9gwe "")

- [如何查看Terway网络Pod生命周期？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#cc1c9a9b24jwi "")

- [Terway DataPath V2数据面模式](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#8d795cd6096zy "")

- [Terway组件升级失败常见问题](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#929cd5d1bbkc1 "")

- [Terway网络模式下，创建Pod提示找不到mac地址](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#c7718eb235kej "")


### Flannel相关

- [手动升级了Flannel镜像版本后，如何解决无法兼容1.16以上版本集群的问题？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-z0i-qcj-rz7 "")

- [如何选择Kubernetes集群Terway和Flannel网络插件？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-ylr-ln7-pfe "")

- [为什么Pod无法ping通部分ECS节点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-b72-fy0-vvp "")

- [为什么集群节点有NodeNetworkUnavailable污点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-3zu-99s-d8q "")

- [什么场景下需要为集群配置多个路由表？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#30bda7d5fa0ob "")

- [为什么Pod无法正常启动，且报错no IP addresses available in range？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-iiz-3h3-xyl "")

- [如何修改节点IP数量、Pod IP网段、Service IP网段？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-cg6-hkg-8w0 "")


### kube-proxy相关

- [如何修改kube-proxy配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-816-94g-skp "")

- [如何修改kube-proxy中IPVS负载均衡模式？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-elo-tp0-pay "")

- [如何修改kube-proxy中IPVS UDP会话保持的超时时间？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-vkv-808-6wc "")


### IPv6相关

[如何解决IPv6双栈的部分常见问题？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-bir-732-rem "")

### ACK容器网络数据链路

- [ACK容器网络数据链路（Flannel）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-network-fabric-flannel#main-2305042 "")

- [ACK容器网络数据链路（Terway ENI）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-network-fabric-terway-eni#main-2305047 "")

- [ACK容器网络数据链路（Terway ENIIP）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-network-fabric-terway-eniip#main-2305054 "")

- [ACK容器网络数据链路（Terway IPVLAN+Terway＜1.8.0）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-network-fabric-terway-ipvlan-ebpf#main-2305057 "")

- [ACK容器网络数据链路（Terway ENI-Trunking）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-network-fabric-terway-eni-trunking#main-2305056 "")

- [ACK容器网络数据链路（Terway DataPath V2+Terway≥1.8.0）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/ack-network-fabric-terway-datapath-v2 "")


### 其他

- [如何解决Pod启动后存在时延的问题？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-g60-wqh-qtq "")

- [如何让Pod访问自己暴露的服务？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-w3o-3as-8lq "")

- [如何规划集群网络？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-8td-x8b-qez "")

- [ACK是否支持hostPort的端口映射？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-hlo-gm1-u0l "")

- [如何查看集群的网络类型及对应的虚拟交换机？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-bgi-kgm-etw "")

- [如何查看集群中使用的云资源？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-8b1-slo-xiu "")

- [如何提升Linux连接跟踪Conntrack数量限制？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-jbl-6zq-9b5 "")

- [是否支持安装和配置第三方网络插件？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#0e27ee075atv6 "")

- [为什么Pod CIDR地址不足，报错no IP addresses available in range set？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#6b08c3a77d87r "")

- [配置集群本地域名（ClusterDomain）有哪些注意事项？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#52430cbfb6ddj "")


## Terway的主要网络模式有哪些？

共享ENI模式和独占ENI模式。每种模式的详细信息，请参见 [共享ENI模式与独占ENI模式](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#9909637f6e34h "")。需要特别注意的是，只有Terway共享ENI模式支持 [网络加速](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#0240fff858j64 "")（DataPathv2或者IPvlan+eBPF），其中DataPathv2是早期IPvlan+eBPF加速模式的升级版，在Terway v1.8.0及以上版本中，创建集群并安装Terway插件时只支持选择DataPathv2加速。

## 如何区分Terway是独占ENI模式还是共享ENI模式？

- 在Terway v1.11.0及以上的版本中，Terway默认使用共享ENI模式，支持通过 [为节点池配置独占ENI网络模式](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-a-node-pool-level-container-network "") 开启独占ENI模式。

- 在Terway v1.11.0之前的版本中，创建集群时可以单独选择独占ENI模式或者共享ENI模式。集群创建之后可以使用以下方式区分：

  - 独占ENI模式: 在kube-system命名空间下Terway守护进程DaemonSet的名字是`terway-eni`。

  - 共享ENI模式: 在kube-system命名空间下Terway守护进程DaemonSet的名字是`terway-eniip`。

## 如何区分Terway网络加速是DataPathv2还是IPvlan+eBPF？

只有Terway共享ENI模式支持 [网络加速](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#0240fff858j64 "")（DataPathv2或者IPvlan+eBPF），其中DataPathv2是早期IPvlan+eBPF加速模式的升级版，在Terway v1.8.0及以上版本中，创建集群并安装Terway插件时只支持选择DataPathv2加速。

可以通过kube-system命名空间下eni-config配置项中的`eniip_virtual_type`配置区分具体是否开启网络加速。网络加速模式的取值为`datapathv2`或`ipvlan`。

## Terway DataPathv2或者IPvlan+eBPF模式路由是否绕过IPVS？

Terway开启加速模式（DataPathv2或者IPvlan+eBPF）后，Terway会采取不同于常规共享ENI模式的流量转发路径， 在特定场景（如Pod访问内部Service时）可以绕过节点中网络协议栈，不需要经过节点IPVS路由，使用eBPF将Service地址解析为Service后端某个Pod的地址。具体流量走向，请参见 [网络加速](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#0240fff858j64 "")。

## **已经创建的ACK集群是否支持切换网络插件？**

网络插件类型（Terway和Flannel）仅支持在集群创建阶段选择，集群创建后不支持修改。如需切换，请重新创建集群，具体操作，请参见 [创建ACK托管集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-an-ack-managed-cluster-2/ "")。

## Terway网络模式下增加了虚拟交换机后，集群无法访问公网怎么办？

**问题现象**

在Terway网络下，因Pod没有IP资源而手动增加虚拟交换机，在增加虚拟交换机后，发现集群不能正常访问公网。

**问题原因**

Pod IP所属的虚拟交换机不具备公网访问的能力。

**解决方法**

您可以通过NAT网关的SNAT功能，为Pod IP所属的虚拟交换机配置公网SNAT规则。更多信息，请参见 [为集群开启访问公网的能力](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/enable-an-existing-ack-cluster-to-access-the-internet#task-1936294 "")。

## 手动升级了Flannel镜像版本后，如何解决无法兼容1.16以上版本集群的问题？

**问题现象**

集群版本升级到1.16之后，集群节点变成NotReady。

**问题原因**

手动升级了Flannel版本，而并没有升级Flannel的配置，导致Kubelet无法识别。

**解决方法**

1. 编辑Flannel，增加`cniVersion`字段。

















```shell
kubectl edit cm kube-flannel-cfg -n kube-system
```





返回结果中增加`cniVersion`字段。

















```yaml
"name": "cb0",
"cniVersion":"0.3.0",
"type": "flannel",
```

2. 重启Flannel。

















```shell
kubectl delete pod -n kube-system -l app=flannel
```


## 如何解决Pod启动后存在时延的问题？

**问题现象**

Pod启动后网络需要延迟一会才能通信。

**问题原因**

配置Network Policy会有一定的时延，关闭Network Policy后，就能解决该问题。

**解决方法**

1. 修改Terway的ConfigMap，增加禁用NetworkPolicy的配置。

















```shell
kubectl edit cm -n kube-system eni-config
```





在返回结果中增加以下字段。

















```yaml
disable_network_policy: "true"
```

2. **可选：**如果Terway版本不是最新的，请在控制台升级Terway版本。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

3. 在 **组件管理** 页面，单击 **网络** 页签，单击目标Terway组件区域的 **升级**。

4. 在对话框中按提示完成配置，单击 **确认**。
3. 重启所有Terway的Pod。

















```shell
    kubectl delete pod -n kube-system -l app=terway-eniip
```


## 如何让Pod访问自己暴露的服务？

**问题现象**

Pod无法访问自己暴露的服务，存在时好时坏或者调度到自己就出问题的现象。

**问题原因**

Flannel集群可能未开启回环访问。

**说明**

- 低于v0.15.1.4-e02c8f12-aliyun版本的Flannel不允许回环访问。升级版本后，仍默认不允许回环访问，但可以手动开启。

- 只有全新部署的v0.15.1.4-e02c8f12-aliyun及以上版本的Flannel，才默认开启回环访问。


**解决方法**

- 使用Headless Service暴露服务和访问，具体操作，请参见 [Headless Services](https://kubernetes.io/zh/docs/concepts/services-networking/service/#headless-services)。



**说明**





推荐使用此方法。

- 重建集群使用Terway的网络插件，具体操作，请参见 [使用Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#task-1797447 "")。

- 修改Flannel的配置，然后重建Flannel和Pod。



**说明**





不推荐此方法，可能会被后续升级覆盖。





1. 编辑cni-config.json。















     ```shell
     kubectl edit cm kube-flannel-cfg -n kube-system
     ```

2. 在返回结果的`delegate`中增加`hairpinMode: true`。



     示例如下：

















     ```yaml
     cni-conf.json: |
         {
           "name": "cb0",
           "cniVersion":"0.3.1",
           "type": "flannel",
           "delegate": {
             "isDefaultGateway": true,
             "hairpinMode": true
           }
         }
     ```

3. 重启Flannel。















     ```shell
     kubectl delete pod -n kube-system -l app=flannel
     ```

4. 删除并重新创建Pod。

## 如何选择Kubernetes集群Terway和Flannel网络插件？

下面为您详细介绍在ACK创建集群时使用的两种网络插件：Terway和Flannel。

在创建Kubernetes集群时，阿里云容器服务提供以下两种网络插件：

- Flannel：使用的是简单稳定的社区的 [Flannel](https://github.com/coreos/flannel) CNI插件，配合阿里云的VPC的高速网络，能给集群提供高性能和稳定的容器网络体验，但功能偏简单，支持的特性少，例如：不支持基于Kubernetes标准的Network Policy。

- Terway：是阿里云容器服务自研的网络插件，功能上完全兼容Flannel，支持将阿里云的弹性网卡分配给容器，支持基于Kubernetes标准的NetworkPolicy来定义容器间的访问策略，支持对单个容器做带宽的限流。对于不需要使用Network Policy的用户，可以选择Flannel，其他情况建议选择Terway。了解更多Terway网络插件的相关内容，请参见 [使用Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#task-1797447 "")。


## 如何规划集群网络？

在创建ACK集群时，需要指定专有网络VPC、虚拟交换机、Pod网络CIDR（地址段）和Service CIDR（地址段）。建议您提前规划ECS地址、Kubernetes Pod地址和Service地址。详情请参见 [ACK托管集群网络规划](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-cluster-network-planning#concept-izq-sg4-vdb "")。

## ACK是否支持hostPort的端口映射？

- 只有Flannel插件支持hostPort，其他插件暂不支持hostPort。

- 容器服务ACK的Pod地址是可以直接被VPC中其他资源访问的，不需要额外的端口映射。

- 如果需要把服务暴露到外部，可以使用NodePort或者LoadBalancer类型的Service。


## 如何查看集群的网络类型及对应的虚拟交换机？

ACK支持两种容器网络类型，分别是Flannel网络类型和Terway网络类型。

- 通过以下步骤查看您创建集群时所选择的网络类型。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏单击 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择 **集群信息**。

3. 单击 **基本信息** 页签，在 **网络** 区域查看集群的容器网络类型，即 **网络插件** 右侧的值。

     - 如果 **网络插件** 右侧显示 **Terway**，则容器的网络类型为Terway网络。

     - 如果 **网络插件** 右侧显示 **Flannel**，则容器的网络类型为Flannel网络。
- 通过以下步骤查看对应网络类型使用的节点虚拟交换机。

1. 在左侧导航栏，选择**节点管理** \> **节点池**。

2. 在 **节点池** 页面，单击目标节点池右侧 **操作** 列下的 **详情**，然后单击 **基本信息** 页签。

     在 **节点配置** 区域查看 **节点虚拟交换机** ID。
- 通过以下步骤查询Terway网络类型使用的Pod虚拟交换机ID。



**说明**





只有Terway网络类型使用Pod虚拟交换机，Flannel网络类型无需使用Pod虚拟交换机。





1. 在左侧导航栏，单击 **组件管理**。

2. 在组件管理页面，单击 **terway-eniip** 卡片中的 **配置**， **PodVswitchId** 选项中展示了目前使用的Pod虚拟交换机。

## 如何查看集群中使用的云资源？

通过以下步骤查看集群中使用的云资源信息，包括虚拟机、虚拟专有网络VPC、Worker RAM角色等。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏单击 **集群列表**。

2. 在集群列表页面中，单击目标集群名称或者目标集群右侧操作列下的 **详情**。

3. 单击 **基本信息** 页签，查看集群中使用的云资源信息。


## 如何修改kube-proxy配置？

ACK托管版默认部署kube-proxy-worker DaemonSet作为负载均衡，可通过其同名配置项kube-proxy-worker ConfigMap控制其参数。如果您使用的是ACK专有版，您在集群中会额外部署kube-proxy-master DaemonSet和同名配置项，其会运行于Master节点上。

kube-proxy配置项均兼容社区KubeProxyConfiguration标准，您可以参考社区KubeProxyConfiguration标准进行自定义配置，更多信息，请参见 [kube-proxy Configuration](https://kubernetes.io/docs/reference/config-api/kube-proxy-config.v1alpha1/)。kube-proxy配置文件对格式要求严格，请勿漏填冒号和空格。修改kube-proxy配置操作如下：

- 如果您使用的是托管版集群，您需要修改kube-proxy-worker的配置。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏单击 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**配置管理** \> **配置项**。

3. 在顶部选择 **kube-system** 命名空间，然后单击配置项kube-proxy-worker右侧的 **YAML编辑**。

4. 在 **查看YAML** 面板上修改参数，然后单击 **确定**。

5. 重建所有名为kube-proxy-worker的容器，使配置生效。



     **重要**





     kube-proxy的重启不会导致已有运行业务中断，如果有并发业务发布，新启动的业务在kube-proxy的生效时间会略有延迟，请尽量于业务低峰期操作。





     1. 在集群管理页左侧导航栏中，选择**工作负载** \> **守护进程集**。

     2. 在守护进程集列表中，找到并单击 **kube-proxy-worker**。

     3. 在 **kube-proxy-worker** 页面的 **容器组** 页签下，选择**更多** \> **删除**，然后单击 **确定**。

        重复操作删除所有容器组。删除容器组后，系统会自动重建所有容器。
- 如果您使用的是专有版集群，您需要修改kube-proxy-worker和kube-proxy-master的配置，然后删除kube-proxy-worker和kube-proxy-master Pod，该Pod自动重新创建后会使配置生效。具体操作，请参见上文。


## 如何提升Linux连接跟踪Conntrack数量限制？

内核日志（dmesg）中出现conntrack full的报错日志，说明Conntrack数量已经达到conntrack\_max数量限制。您需要提升Linux连接跟踪Conntrack数量限制。

1. 执行以下命令，确认目前Conntrack中的各协议占用情况和数量。















```bash
# 查看表明细，可以配合grep管道查看状态，也可以使用cat /proc/net/nf_conntrack查看
conntrack -L

# 查看计数
cat /proc/sys/net/netfilter/nf_conntrack_count

# 查看表当前最大值
cat /proc/sys/net/netfilter/nf_conntrack_max
```



   - 如果出现大量TCP协议的占用，您需要确认具体业务，如果是短连接型应用可以考虑整改成长连接型。

   - 如果出现大量DNS的占用，您需要在ACK集群中使用NodeLocal DNSCache，提高DNS的性能，具体操作，请参见 [使用NodeLocal DNSCache组件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-nodelocal-dnscache#task-2008363 "")。

   - 如果出现大量应用层返回timeout或者504的报错，或者操作系统内核⽇志打印`kernel: nf_conntrack: table full, dropping packet.`的报错，请慎重调整conntrack相关参数⼤⼩。



     调整/etc/sysctl.conf文件中conntrack相关参数示例




















     ```bash
     # 修改表当前最大值
     net.netfilter.nf_conntrack_max = 655350

     # 修改ct表中的超时参数,比如established最长时间，按业务定制（慎重），21600为6小时
     net.netfilter.nf_conntrack_tcp_timeout_established = 21600

     # 优化tcp挥手状态的值实现加快清理，按业务定制（慎重）
     net.netfilter.nf_conntrack_tcp_timeout_time_wait =60
     net.netfilter.nf_conntrack_tcp_timeout_close_wait =120
     net.netfilter.nf_conntrack_tcp_timeout_fin_wait =30
     ```
2. 如果Conntrack实际占用情况合理，或者您不希望对业务进行整改，您可以通过配置kube-proxy增加maxPerCore参数，调整连接跟踪数量限制。

   - 如果您使用的是托管版集群，您需要在kube-proxy-worker中增加maxPerCore参数，并设置其值为65536或更高的数值，然后删除kube-proxy-worker Pod，该Pod自动重新创建后会使配置生效。关于如何修改并删除kube-proxy-worker，请参见 [如何修改kube-proxy配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-816-94g-skp "")。















     ```yaml
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: kube-proxy-worker
       namespace: kube-system
     data:
       config.conf: |
         apiVersion: kubeproxy.config.k8s.io/v1alpha1
         kind: KubeProxyConfiguration
         featureGates:
           IPv6DualStack: true
         clusterCIDR: 172.20.0.0/16
         clientConnection:
           kubeconfig: /var/lib/kube-proxy/kubeconfig.conf
         conntrack:
           maxPerCore: 65536 # 需设置maxPerCore至合理值，此处65536为默认设置。
         mode: ipvs
     # 其它略
     ```

   - 如果您使用的是专有版集群，您需要在kube-proxy-worker和kube-proxy-master中增加maxPerCore参数，并设置其值为65536或更高的数值，然后删除kube-proxy-worker和kube-proxy-master Pod，该Pod自动重新创建后会使配置生效。关于如何修改并删除kube-proxy-worker和kube-proxy-master，请参见 [如何修改kube-proxy配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-816-94g-skp "")。

**说明**

如果在Terway Datapath V2或者IPvlan模式下，容器内流量对应的conntrack信息在eBPF map内存储，其他模式下conntrack信息在Linux conntrack存储。关于如何调整eBPF conntrack大小，请参见 [优化Terway模式下conntrack配置](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/optimize-conntrack-configuration-in-terway-mode "")。

## 如何修改kube-proxy中IPVS负载均衡模式？

如果业务为长连接，由于每个连接会发多次请求，后端Pod请求数可能是不均衡的。您可以通过修改kube-proxy中IPVS负载均衡模式来解决大量长连接的负载不均问题，具体操作如下：

1. 选择合适的调度算法。关于如何选择合适的调度算法，请参见K8s官方文档 [parameter-changes](https://kubernetes.io/blog/2018/07/09/ipvs-based-in-cluster-load-balancing-deep-dive/#parameter-changes)。

2. 早于2022年10月创建的集群节点可能未默认启用所有IPVS调度算法，您需要手动在所有集群节点上启用IPVS调度算法内核模块（以最小连接数调度算法lc为例，如果选用其他算法，请替换lc关键字），逐台登录每个节点，并运行lsmod \| grep ip\_vs\_lc查看是否有输出。

   - 如果命令输出ip\_vs\_lc，则说明调度算法内核模块已经加载，可以跳过本步骤。

   - 如果没有加载，运行modprobe ip\_vs\_lc使节点立即生效，并运行echo "ip\_vs\_lc" >> /etc/modules-load.d/ack-ipvs-modules.conf使机器重启后生效。
3. 设置kube-proxy中的ipvs.scheduler参数值为合理的调度算法。

   - 如果您使用的是托管版集群，您需要修改kube-proxy-worker的ipvs.scheduler参数值为合理的调度算法，然后删除kube-proxy-worker Pod，该Pod自动重新创建后会使配置生效。关于如何修改并删除kube-proxy-worker，请参见 [如何修改kube-proxy配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-816-94g-skp "")。















     ```yaml
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: kube-proxy-worker
       namespace: kube-system
     data:
       config.conf: |
         apiVersion: kubeproxy.config.k8s.io/v1alpha1
         kind: KubeProxyConfiguration
         featureGates:
           IPv6DualStack: true
         clusterCIDR: 172.20.0.0/16
         clientConnection:
           kubeconfig: /var/lib/kube-proxy/kubeconfig.conf
         conntrack:
           maxPerCore: 65536
         mode: ipvs
         ipvs:
           scheduler: lc # 需设置scheduler成合理的调度算法。
     # 其它略
     ```

   - 如果您使用的是专有版集群，您需要修改kube-proxy-worker和kube-proxy-master中的ipvs.scheduler参数值为合理的调度算法，然后删除kube-proxy-worker和kube-proxy-master Pod，该Pod自动重新创建后会使配置生效。关于如何修改并删除kube-proxy-worker和kube-proxy-master，请参见 [如何修改kube-proxy配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-816-94g-skp "")。
4. 查看kube-proxy运行日志。

   - 通过kubectl get pods命令查看kube-system命名空间下新建的kube-proxy-worker容器（如果您使用专有版集群，还需查看kube-proxy-master）是否为Running状态。

   - 通过kubectl logs命令查看新建容器的日志。

     - 如果出现Can't use the IPVS proxier: IPVS proxier will not be used because the following required kernel modules are not loaded: \[ip\_vs\_lc\]则说明IPVS调度算法内核模块未成功加载，您需要检查上述步骤是否已经正确执行，并尝试重试。

     - 如果出现Using iptables Proxier.说明kube-proxy无法启用IPVS模块，开始自动回退使用iptables模式，此时建议先回滚kube-proxy配置，再对机器进行重启操作。

     - 如果未出现上述日志，并显示Using ipvs Proxier.说明IPVS模块成功启用。
   - 如果上述检查均返回正常，说明变更成功。

> 关于如何抓取容器内部的网络报文来判断负载是否不均衡的更多步骤，请参考 [阿里云开发者社区](https://developer.aliyun.com/article/775829)。

## 如何修改kube-proxy中IPVS UDP会话保持的超时时间？

如果您的ACK集群使用了kube-proxy IPVS模式，IPVS的默认会话保持策略会使UDP协议后端在摘除后五分钟内出现概率性丢包的问题。如果您业务依赖于CoreDNS，当CoreDNS组件升级或所在节点重启时，您可能会在五分钟内遇到业务接口延迟、请求超时等现象。

若您在ACK集群中的业务没有使用UDP协议，您可以通过降低IPVS UDP协议的会话保持的超时时间来减少解析延迟或失败的影响时间。具体操作如下：

**说明**

若您的自有业务使用了UDP协议，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)咨询。

- K8s 1.18及以上版本集群

  - 如果您使用的是托管版集群，您需要在kube-proxy-worker中修改udpTimeout参数值。然后删除kube-proxy-worker Pod，该Pod自动重新创建后会使配置生效。关于如何修改并删除kube-proxy-worker，请参见 [如何修改kube-proxy配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-816-94g-skp "")。















    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: kube-proxy-worker
      namespace: kube-system
    data:
      config.conf: |
        apiVersion: kubeproxy.config.k8s.io/v1alpha1
        kind: KubeProxyConfiguration
        # 其它不相关字段已省略。
        mode: ipvs
        # 如果ipvs键不存在，需要添加此键。
        ipvs:
          udpTimeout: 10s # 此处默认为300秒，调整成10秒可以将IPVS UDP类型后端摘除后丢包问题的影响时间缩短到10秒。
    ```

  - 如果您使用的是专有版集群，您需要在kube-proxy-worker和kube-proxy-master中修改udpTimeout参数值。然后删除kube-proxy-worker和kube-proxy-master Pod，该Pod自动重新创建后会使配置生效。关于如何修改并删除kube-proxy-worker，请参见 [如何修改kube-proxy配置？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#section-816-94g-skp "")。
- K8s 1.16及以下版本集群



此类版本集群的kube-proxy不支持udpTimeout参数，推荐使用系统运维管理 OOS（CloudOps Orchestration Service）批量在所有集群机器上执行`ipvsadm`命令以调整UDP超时时间配置。命令如下：

















```shell
yum install -y ipvsadm
ipvsadm -L --timeout > /tmp/ipvsadm_timeout_old
ipvsadm --set 900 120 10
ipvsadm -L --timeout > /tmp/ipvsadm_timeout_new
diff /tmp/ipvsadm_timeout_old /tmp/ipvsadm_timeout_new
```





关于OOS的批量操作实例介绍，请参见 [批量操作实例](https://help.aliyun.com/zh/oos/getting-started/manage-multiple-instances#topic542 "")。


## 如何解决IPv6双栈的部分常见问题？

- **问题现象：** 在kubectl中显示的Pod IP仍然是IPv4地址。

**解决方法：** 执行以下命令，展示Pod IPs字段，预期输出IPv6地址。















```shell
kubectl get pods -A -o jsonpath='{range .items[*]}{@.metadata.namespace} {@.metadata.name} {@.status.podIPs[*].ip} {"\n"}{end}'
```

- **问题现象：** 在kubectl中显示的Cluster IP仍然是IPv4地址。



**解决方法：**



1. 请确认spec.ipFamilyPolicy配置的不是SingleStack。

2. 执行以下命令，展示Cluster IPs字段，预期输出IPv6地址。















     ```shell
     kubectl get svc -A -o jsonpath='{range .items[*]}{@.metadata.namespace} {@.metadata.name} {@.spec.ipFamilyPolicy} {@.spec.clusterIPs[*]} {"\n"}{end}'
     ```


- **问题现象：** 无法通过IPv6地址访问Pod。

**问题原因：** 部分应用默认不监听IPv6地址，例如Nginx容器。

**解决方法：** 执行`netstat -anp`命令，确认Pod已监听IPv6地址。

预期输出：















```shell
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.XX.XX:10248         0.0.0.0:*               LISTEN      8196/kubelet
tcp        0      0 127.0.XX.XX:41935         0.0.0.0:*               LISTEN      8196/kubelet
tcp        0      0 0.0.XX.XX:111             0.0.0.0:*               LISTEN      598/rpcbind
tcp        0      0 0.0.XX.XX:22              0.0.0.0:*               LISTEN      3577/sshd
tcp6       0      0 :::30500                :::*                    LISTEN      1916680/kube-proxy
tcp6       0      0 :::10250                :::*                    LISTEN      8196/kubelet
tcp6       0      0 :::31183                :::*                    LISTEN      1916680/kube-proxy
tcp6       0      0 :::10255                :::*                    LISTEN      8196/kubelet
tcp6       0      0 :::111                  :::*                    LISTEN      598/rpcbind
tcp6       0      0 :::10256                :::*                    LISTEN      1916680/kube-proxy
tcp6       0      0 :::31641                :::*                    LISTEN      1916680/kube-proxy
udp        0      0 0.0.0.0:68              0.0.0.0:*                           4892/dhclient
udp        0      0 0.0.0.0:111             0.0.0.0:*                           598/rpcbind
udp        0      0 47.100.XX.XX:323           0.0.0.0:*                           6750/chronyd
udp        0      0 0.0.0.0:720             0.0.0.0:*                           598/rpcbind
udp6       0      0 :::111                  :::*                                598/rpcbind
udp6       0      0 ::1:323                 :::*                                6750/chronyd
udp6       0      0 fe80::216:XXXX:fe03:546 :::*                                6673/dhclient
udp6       0      0 :::720                  :::*                                598/rpcbind
```



`Proto`显示为`tcp`即监听IPv4地址，显示为`tcp6`即监听IPv6地址。

- **问题现象：** 通过IPv6地址可以在集群内访问Pod，但无法从公网访问。

**问题原因：** 该IPv6地址可能未配置公网带宽。

**解决方法：** 配置该IPv6地址的公网带宽。具体操作，请参见 [开通和管理IPv6公网带宽](https://help.aliyun.com/zh/ipv6-gateway/user-guide/enable-and-manage-ipv6-internet-bandwidth#task-g1w-pg5-zfb "")。

- **问题现象：** 无法通过IPv6 Cluster IP访问Pod。



**解决方法：**



1. 请确认spec.ipFamilyPolicy配置的不是SingleStack。

2. 执行`netstat -anp`命令，确认Pod已监听IPv6地址。

     预期输出：















     ```shell
     Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
     tcp        0      0 127.0.XX.XX:10248         0.0.0.0:*               LISTEN      8196/kubelet
     tcp        0      0 127.0.XX.XX:41935         0.0.0.0:*               LISTEN      8196/kubelet
     tcp        0      0 0.0.XX.XX:111             0.0.0.0:*               LISTEN      598/rpcbind
     tcp        0      0 0.0.XX.XX:22              0.0.0.0:*               LISTEN      3577/sshd
     tcp6       0      0 :::30500                :::*                    LISTEN      1916680/kube-proxy
     tcp6       0      0 :::10250                :::*                    LISTEN      8196/kubelet
     tcp6       0      0 :::31183                :::*                    LISTEN      1916680/kube-proxy
     tcp6       0      0 :::10255                :::*                    LISTEN      8196/kubelet
     tcp6       0      0 :::111                  :::*                    LISTEN      598/rpcbind
     tcp6       0      0 :::10256                :::*                    LISTEN      1916680/kube-proxy
     tcp6       0      0 :::31641                :::*                    LISTEN      1916680/kube-proxy
     udp        0      0 0.0.0.0:68              0.0.0.0:*                           4892/dhclient
     udp        0      0 0.0.0.0:111             0.0.0.0:*                           598/rpcbind
     udp        0      0 47.100.XX.XX:323           0.0.0.0:*                           6750/chronyd
     udp        0      0 0.0.0.0:720             0.0.0.0:*                           598/rpcbind
     udp6       0      0 :::111                  :::*                                598/rpcbind
     udp6       0      0 ::1:323                 :::*                                6750/chronyd
     udp6       0      0 fe80::216:XXXX:fe03:546 :::*                                6673/dhclient
     udp6       0      0 :::720                  :::*                                598/rpcbind
     ```



     `Proto`显示为`tcp`即监听IPv4地址，显示为`tcp6`即监听IPv6地址。

3. **问题现象：** Pod无法通过IPv6访问公网。

     **解决方法：** 对IPv6使用公网，需要开通IPv6网关，并对IPv6地址配置公网带宽。详细信息，请参见 [创建和管理IPv6网关](https://help.aliyun.com/zh/ipv6-gateway/user-guide/create-and-manage-an-ipv6-gateway#task-2202006 "") 和 [开通和管理IPv6公网带宽](https://help.aliyun.com/zh/ipv6-gateway/user-guide/enable-and-manage-ipv6-internet-bandwidth#task-2202589 "")。


## **Terway网络插件下交换机的IP资源不足怎么办？**

**问题描述**

在创建Pod时发现无法创建，登录 [VPC控制台](https://vpc.console.aliyun.com/vpc/cn-hangzhou/switches)，选择目标 **地域**，查看集群使用的交换机（vSwitch）信息，发现该vSwitch **可用IP数** 为0。如何进一步确认问题请参见 [更多信息](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#RwhzA "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8703898371/p913158.png)

**问题原因**

该节点的Terway所使用的交换机没有空余IP地址，导致Pod会因为没有IP资源而一直处于ContainerCreating状态。

**解决方案**

您可以参考以下内容，扩容交换机，即添加新的交换机，扩容集群的IP资源：

1. 登录 [VPC控制台](https://vpc.console.aliyun.com/vpc/cn-huhehaote/switches)，选择目标 **地域**，创建新的交换机。




**说明**





该交换机必须与IP资源不足的交换机在同一个地域和可用区。如果Pod密度越来越大，建议给Pod使用的交换机网段的网络位小于等于19，也就是网段至少包含8192个IP地址。

2. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

在组件管理中找到terway-eniip卡片，单击 **配置**，在 **PodVswitchId** 选项中添加上一步骤中创建的交换机ID。

3. 参考以下命令，删除全部Terway Pod，删除后Terway Pod会重新创建。




**说明**





如果您在创建集群时，使用Terway并勾选了 **Pod独占弹性网卡以获得最佳性能**，说明您是ENI单IP；没有勾选则是ENI多IP，详细信息请参见 [Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway "")。





   - 针对ENI多IP场景：`kubectl delete -n kube-system pod -l app=terway-eniip`

   - 针对ENI单IP场景：`kubectl delete -n kube-system pod -l app=terway-eni`
4. 然后执行`kubectl get pod`命令，确认全部Terway Pod重建成功。

5. 创建新的Pod，确认Pod创建成功且可以重新交换机成功分配获得IP。


**更多信息**

连接Kubernetes集群，如何连接请参见 [通过kubectl连接Kubernetes集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/obtain-the-kubeconfig-file-of-a-cluster-and-use-kubectl-to-connect-to-the-cluster "")，执行`kubectl get pod`命令，发现Pod状态为ContainerCreating。执行以下命令，查看Pod所在节点上的Terway容器的日志。

```shell
kubectl get pod -l app=terway-eniip -n kube-system | grep [$Node_Name] # [$Node_Name] 为Pod所在节点的节点名，用来找出该节点上的Terway Pod的名称
kubectl logs --tail=100 -f [$Pod_Name] -n kube-system -c terway # [$Pod_Name]为Pod所在节点上的Terway Pod的名称。
```

系统显示类似如下，出现类似InvalidVSwitchId.IpNotEnough错误信息，表明存在交换机IP不足的情况。

```shell
time="2020-03-17T07:03:40Z" level=warning msg="Assign private ip address failed: Aliyun API Error: RequestId: 2095E971-E473-4BA0-853F-0C41CF52651D Status Code: 403 Code: InvalidVSwitchId.IpNotEnough Message: The specified VSwitch \"vsw-AAA\" has not enough IpAddress., retrying"
```

## Terway网络模式下，Pod分配的IP不在虚拟交换机网段中怎么办？

**问题现象**

在Terway网络下，创建的Pod IP不在配置的虚拟交换机网段内。

**问题原因**

Pod IP来源于VPC地址，并且通过ENI分配给容器使用。只有在新建ENI时，才可以配置虚拟交换机。如果ENI已经创建，则Pod IP将继续从该ENI对应的虚拟交换机中分配。

通常以下两个使用场景会遇到该问题：

- 纳管一个节点到集群内，但这个节点之前在其他集群使用，且删除节点时没有排空节点Pod。这种情况下节点上可能残留之前集群使用的ENI资源。

- 手动增加、修改Terway使用的虚拟交换机配置，由于节点上可能还存在原有配置的ENI，则新建的Pod将可能继续使用原有ENI上的IP。


**解决方法**

您可以通过新建节点、轮转老节点的方式来确保配置文件在新节点上生效。

**轮转老节点操作步骤如下：**

1. 排空并移除老节点。操作详情，请参考 [移除节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/remove-a-node "")。

2. 将移出的节点的Eni网卡解除绑定。操作详情，请参见 [管理弹性网卡](https://help.aliyun.com/zh/ecs/user-guide/manage-eni "")。

3. 弹性网卡解除后，再将移出节点添加回原ACK集群中。操作详情，请参见 [添加已有节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-existing-ecs-instances-to-an-ack-cluster#title-7lu-zoz-rjh "")。


## Terway网络模式扩容vSwitch后，依然无法分配Pod IP怎么办？

**问题现象**

在Terway网络下，Terway网络模式扩容vSwitch后依然无法分配Pod IP。

**问题原因**

Pod IP来源于VPC地址，并且通过ENI分配给容器使用。只有在新建ENI时，才可以配置虚拟交换机。如果ENI已经创建，则Pod IP将继续从该ENI对应的虚拟交换机中分配。由于节点上ENI配额已经用完，无法新建ENI，也就无法让新配置生效。关于ENI配额的具体信息，请参见 [弹性网卡概述](https://help.aliyun.com/zh/ecs/user-guide/eni-overview#section-ic1-qnw-ydb "")。

**解决方法**

您可以通过新建节点、轮转老节点的方式来确保配置文件在新节点上生效。

**轮转老节点操作步骤如下：**

1. 排空并移除老节点。操作详情，请参考 [移除节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/remove-a-node "")。

2. 将移出的节点的Eni网卡解除绑定。操作详情，请参见 [管理弹性网卡](https://help.aliyun.com/zh/ecs/user-guide/manage-eni "")。

3. 弹性网卡解除后，再将移出节点添加回原ACK集群中。操作详情，请参见 [添加已有节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-existing-ecs-instances-to-an-ack-cluster#title-7lu-zoz-rjh "")。


## 如何为Terway IPvlan集群开启集群内负载均衡？

**问题现象**

在IPvlan模式下，v1.2.0及以上版本的Terway，新建的集群默认开启集群内负载均衡功能。在集群内访问ExternalIP，LoadBalancer流量将被负载到Service网络。如何为已创建的Terway IPvlan集群开启集群内负载均衡？

**问题原因**

Kube-Proxy会短路集群内访问ExternalIP、LoadBalancer的流量，即集群内访问这些外部地址，实际流量不会到外部，而会被转为对应后端的Endpoint直接访问。在Terway IPvlan模式下，Pod访问这些地址流量由Cilium而不是kube-proxy进行处理， 在Terway v1.2.0之前版本并不支持这种链路的短路。在Terway v1.2.0版本发布后，新建集群将默认开启该功能，已创建的集群不会开启。

**解决方法**

**说明**

- Terway需要v1.2.0及以上版本，且使用IPvlan模式。

- 如果集群未启用IPvlan模式，则该配置无效，无需配置。

- 新建集群此功能默认开启，无需配置。


1. 执行以下命令，修改Terway的配置ConfigMap。

















```shell
kubectl edit cm eni-config -n kube-system
```

2. 在eni\_conf中增加以下内容。

















```yaml
in_cluster_loadbalance: "true"
```







**说明**





请保持`in_cluster_loadbalance`和`eni_conf`在同级别。

3. 执行以下命令，重建Terway Pod，使集群内负载均衡配置生效。

















```shell
kubectl delete pod -n kube-system -l app=terway-eniip
```







**验证配置**





执行以下命令，检查terway-ennip中policy日志，如果显示`enable-in-cluster-loadbalance=true`则配置生效。

















```shell
kubectl logs -n kube-system <terway pod name> policy | grep enable-in-cluster-loadbalance
```


## 如何在ACK中对Terway网络下的Pod指定网段加白？

**问题现象**

您通常需要在一些类似数据库之类的服务设置白名单，以此来给服务提供更安全的访问控制能力。在容器网络下同样有此需求，需要在容器中给动态变化的Pod IP设置白名单。

**问题原因**

ACK的容器网络主要有Flannel和Terway两种：

- 在Flannel网络下，因为Pod是通过节点访问其他服务，所以在Flannel网络下的数据库设置白名单时，首先可以将客户端Pod通过节点绑定的方式调度到固定的少数节点上去，然后在数据库侧直接对节点的IP地址做加白操作即可。

- 在Terway网络下，Pod IP是通过ENI提供。Pod通过ENI访问外部服务，外部服务得到的客户端IP是ENI提供的IP地址，即使把Pod和节点设置了亲和性绑定，Pod访问外部服务的客户端IP仍然是ENI提供的IP而不是节点的IP。Pod IP还是会从Terway指定的vSwitch中随机分配IP地址，而且客户端Pod通常都会有自动伸缩之类的配置，那即使能固定Pod IP也很难满足弹性伸缩的场景，建议直接给客户端指定一个网段来分配IP，然后在数据库侧对这个网段来做加白操作。


**解决方法**

通过给指定节点添加标签来指定Pod使用的vSwitch，从而当Pod调度到有固定标签的节点上时，该Pod就可以通过自定义的vSwitch去创建Pod IP。

1. 在kube-system命名空间下单独创建一个名称为eni-config-fixed的ConfigMap ，其中需要指定专门的vSwitch。



本示例以vsw-2zem796p76viir02c\*\*\*\*，10.2.1.0/24为例。

















```yaml
apiVersion: v1
data:
     eni_conf: |
       {
          "vswitches": {"cn-beijing-h":["vsw-2zem796p76viir02c****"]},
          "security_group": "sg-bp19k3sj8dk3dcd7****",
          "security_groups": ["sg-bp1b39sjf3v49c33****","sg-bp1bpdfg35tg****"]
       }
kind: ConfigMap
metadata:
     name: eni-config-fixed
     namespace: kube-system


```

2. 创建节点池，为节点打上标签`terway-config:eni-config-fixed`。关于创建节点池的具体操作，请参见 [创建节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/create-a-node-pool#section-eq0-lmv-4a7 "")。



为了保证该节点池内的节点上不会出现其他Pod，可以给该节点池同时配置上污点，例如`fixed=true:NoSchedule`。![节点标签.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7054976461/p412489.png)

3. 扩容该节点池。具体操作，请参见 [手动扩缩容节点池](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/scale-a-node-pool "")。



通过该节点池扩容出来的节点默认会带有上一步设置的节点标签和污点。

4. 创建Pod，调度到已有`terway-config:eni-config-fixed`标签的节点上，需要添加容忍。

















```yaml
apiVersion: apps/v1 # 1.8.0以前的版本请使用apps/v1beta1。
kind: Deployment
metadata:
     name: nginx-fixed
     labels:
       app: nginx-fixed
spec:
     replicas: 2
     selector:
       matchLabels:
         app: nginx-fixed
     template:
       metadata:
         labels:
           app: nginx-fixed
       spec:
         tolerations:        # 添加容忍。
      - key: "fixed"
        operator: "Equal"
        value: "true"
        effect: "NoSchedule"
      nodeSelector:
        terway-config: eni-config-fixed
      containers:
      - name: nginx
        image: nginx:1.9.0 #替换成您实际的镜像<image_name:tags>。
        ports:
        - containerPort: 80
```

**结果验证**

1. 执行以下命令，查看Pod IP。















      ```shell
      kubectl get po -o wide | grep fixed
      ```





      预期输出：

















      ```plaintext
      nginx-fixed-57d4c9bd97-l****                   1/1     Running             0          39s    10.2.1.124    bj-tw.062149.aliyun.com   <none>           <none>
      nginx-fixed-57d4c9bd97-t****                   1/1     Running             0          39s    10.2.1.125    bj-tw.062148.aliyun.com   <none>           <none>
      ```





      可以看到Pod IP已经从指定的vSwitch分配。

2. 执行以下命令，将Pod扩容到30个。















      ```shell
      kubectl scale deployment nginx-fixed --replicas=30
      ```





      预期输出：

















      ```plaintext
      nginx-fixed-57d4c9bd97-2****                   1/1     Running     0          60s     10.2.1.132    bj-tw.062148.aliyun.com   <none>           <none>
      nginx-fixed-57d4c9bd97-4****                   1/1     Running     0          60s     10.2.1.144    bj-tw.062149.aliyun.com   <none>           <none>
      nginx-fixed-57d4c9bd97-5****                   1/1     Running     0          60s     10.2.1.143    bj-tw.062148.aliyun.com   <none>           <none>
      ...
      ```





      可以看到生成的Pod IP全部在指定的vSwitch下，然后在数据库侧直接对此vSwitch做加白操作，从而实现对动态Pod IP的访问控制。


**说明**

- 建议您使用新创建的节点，如果使用已有节点，需要在节点添加进集群之前先将ENI和ECS实例解绑，再添加进集群。添加方式要选用自动添加已有节点（替换系统盘）。具体操作，请参见 [管理弹性网卡](https://help.aliyun.com/zh/ecs/user-guide/manage-eni#concept-ulq-w3k-zdb "") 和 [自动添加节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/add-existing-ecs-instances-to-an-ack-cluster#section-7if-k60-1yx "")。

- 注意给特定的节点池打上标签和污点，尽可能保证不需要加白的业务不会调度到这部分节点上。

- 这个设置白名单的方法其实是配置覆盖，ACK会用现在指定的ConfigMap里的配置来覆盖之前的eni-config的配置，关于配置参数的具体信息，请参见 [Terway节点动态配置](https://github.com/AliyunContainerService/terway/blob/main/docs/dynamic-config.md)。

- 指定vSwitch的IP个数建议为预计Pod个数的2倍（或更多），一方面可以给将来的扩容多一些余量，另一方面也可以避免当发生故障导致Pod IP无法及时回收时，出现没有IP可分配的情况。


## 为什么Pod无法ping通部分ECS节点？

**问题现象**

Flannel网络模式下，检查VPN路由正常，进入Pod，发现部分ECS节点无法ping通。

**问题原因**

Pod无法ping通部分ECS节点的原因分为两种。

- 原因一：Pod访问的ECS和集群在同一个VPC下，但不在同一个安全组。

- 原因二：Pod访问的ECS和集群不在同一个VPC下。


**解决方法**

根据不同的原因，提供不同的解决方法。

- 针对原因一，需要将ECS加入到集群的安全组中。具体操作，请参见 [配置安全组](https://help.aliyun.com/zh/ecs/getting-started/configure-a-security-group#concept-wdb-42w-wdb "")。

- 针对原因二，需要通过ECS的公网入口访问，需要在ECS的安全组中加入集群的公网出口IP地址。具体操作，请参见 [ECS通过EIP对公网提供服务](https://help.aliyun.com/document_detail/181168.html#section-i7g-gfl-2t1 "")。


## 为什么集群节点有NodeNetworkUnavailable污点？

**问题现象**

Flannel网络模式下，新增的集群节点上有NodeNetworkUnavailable污点，导致Pod无法调度。

**问题原因**

Cloud Controller Manager没有及时删除该节点污点，可能原因是路由表满、VPC存在多路由表等情况。

**解决方法**

使用`kubectl describe node`命令查看节点的Event事件信息，根据实际输出的报错进行处理。关于多路由表的问题，需要手动配置CCM的支持，更多详情请参见 [使用VPC的多路由表功能](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-multiple-route-tables-for-a-vpc#task-2057616 "")。

## 为什么Pod无法正常启动，且报错no IP addresses available in range？

**问题现象**

Flannel网络模式下，Pod无法正常启动，查看Pod事件时显示类似于`failed to allocate for range 0: no IP addresses available in range set: 172.30.34.129-172.30.34.190`的错误信息。

**问题原因**

Flannel网络模式下，每个集群节点会被分配到一个指定的容器IP段。容器调度到节点上时，Flannel会从节点所属的容器IP段中获取一个未被占用的IP分配给容器。当Pod提示`failed to allocate for range 0: no IP addresses available in range set: 172.30.34.129-172.30.34.190`错误信息时，说明没有IP可以分配给Pod。该种情况有可能是发生了IP地址泄露，存在以下两个原因：

- ACK低于1.20版本时，如果发生Pod反复重启、CronJob中Pod短时间内退出等事件，可能会导致IP地址泄漏。详情请参见 [Issues 75665](https://github.com/kubernetes/kubernetes/pull/75665) 和 [Issues 92614](https://github.com/kubernetes/kubernetes/pull/92614)。

- Flannel低于v0.15.1.11-7e95fe23-aliyun版本时，如果发生节点重启或突然关机的事件，可能会导致Pod直接销毁，从而导致IP地址泄漏。详情请参见 [Issues 332](https://github.com/containernetworking/plugins/issues/332)。


**解决方案**

- 针对低版本ACK导致的IP地址泄露，您可以升级集群至1.20及以上版本。具体操作，请参见 [手动升级集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/update-the-kubernetes-version-of-an-ack-cluster#task-1664343 "")。

- 针对低版本Fannel导致的IP地址泄露，您可以升级Flannel至v0.15.1.11-7e95fe23-aliyun及以上版本。操作如下：

Flannel只要在v0.15.1.11-7e95fe23-aliyun及以上版本，ACK会在Flannel中将默认IP段分配数据库迁移至临时目录 /var/run中，重启时系统会自动清空，避免IP地址泄露。

1. 升级Flannel组件至v0.15.1.11-7e95fe23-aliyun及以上版本。具体操作，请参见 [管理组件](https://help.aliyun.com/zh/ack/manage-system-components#task-z3j-tvk-2gb "")。

2. 执行以下命令，编辑kube-flannel-cfg文件，然后在kube-flannel-cfg文件中新增dataDir和ipam参数。















     ```shell
     kubectl -n kube-system edit cm kube-flannel-cfg
     ```



     kube-flannel-cfg文件示例如下。















     ```json
     # 修改前
         {
           "name": "cb0",
           "cniVersion":"0.3.1",
           "plugins": [\
             {\
               "type": "flannel",\
               "delegate": {\
                 "isDefaultGateway": true,\
                 "hairpinMode": true\
                },\
             },\
             # portmap # 低版本可能没有，如不使用请忽略。\
             {\
               "type": "portmap",\
               "capabilities": {\
                 "portMappings": true\
               },\
               "externalSetMarkChain": "KUBE-MARK-MASQ"\
             }\
           ]
         }

     # 修改后
         {
           "name": "cb0",
           "cniVersion":"0.3.1",
           "plugins": [\
             {\
               "type": "flannel",\
               "delegate": {\
                 "isDefaultGateway": true,\
                 "hairpinMode": true\
                },\
               # 注意逗号。\
               "dataDir": "/var/run/cni/flannel",\
               "ipam": {\
                 "type": "host-local",\
                 "dataDir": "/var/run/cni/networks"\
                }\
             },\
             {\
               "type": "portmap",\
               "capabilities": {\
                 "portMappings": true\
               },\
               "externalSetMarkChain": "KUBE-MARK-MASQ"\
             }\
           ]
         }
     ```

3. 执行以下命令，重启Flannel Pod。

     重启Flannel Pod不会影响运行中的业务。















     ```shell
     kubectl -n kube-system delete pod -l app=flannel
     ```

4. 删除节点上的IP目录，重启节点。

     1. 排空节点上的已有Pod，请参见 [节点排水和调度状态](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-management/#50c6d833db3rp "")。

     2. 登录节点，执行以下命令，删除IP目录。















        ```shell
        rm -rf /etc/cni/
        rm -rf /var/lib/cni/
        ```

     3. 重启节点。具体操作，请参见 [重启实例](https://help.aliyun.com/zh/ecs/user-guide/restart-instances#concept-yxw-dwm-xdb "")。

     4. 重复执行以上步骤，删除所有节点上的IP目录。
5. 在节点上执行以下命令，验证节点是否启用临时目录。















     ```shell
     if [ -d /var/lib/cni/networks/cb0 ]; then echo "not using tmpfs"; fi
     if [ -d /var/run/cni/networks/cb0 ]; then echo "using tmpfs"; fi
     cat /etc/cni/net.d/10-flannel.conf*
     ```



     返回`using tmpfs`，说明当前节点已经启用临时目录/var/run作为IP段分配数据库，变更成功。
- 如果短时间内无法升级ACK或Flannel，您可以按照以下方法临时紧急处理。临时紧急处理适用于以上两种原因导致的泄漏。

临时紧急处理操作只是帮助您清理泄露的IP地址，IP地址泄露的情况仍然有可能发生，因此您还是需要升级Flannel或集群的版本。



**说明**





  - 以下命令不适用于v0.15.1.11-7e95fe23-aliyun及以上版本的Flannel，并且已经切换使用/var/run存储IP地址分配信息的节点。

  - 以下脚本仅供参考，如果节点曾有过自定义修改，脚本可能无法正常工作。


1. 将问题节点设置为不可调度状态，请参见 [节点排水和调度状态](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-management/#50c6d833db3rp "")。

2. 使用以下脚本，按照运行时引擎清理节点。

     - 如果您使用的是Docker运行时，请使用以下脚本清理节点。















       ```shell
       #!/bin/bash
       cd /var/lib/cni/networks/cb0;
       docker ps -q > /tmp/running_container_ids
       find /var/lib/cni/networks/cb0 -regex ".*/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" -printf '%f\n' > /tmp/allocated_ips
       for ip in $(cat /tmp/allocated_ips); do
         cid=$(head -1 $ip | sed 's/\r#g' | cut -c-12)
         grep $cid /tmp/running_container_ids > /dev/null || (echo removing leaked ip $ip && rm $ip)
       done
       ```

     - 如果您使用的是Containerd运行时，请使用以下脚本清理节点。















       ```shell
       #!/bin/bash
       # install jq
       yum install -y jq

       # export all running pod's configs
       crictl -r /run/containerd/containerd.sock pods -s ready -q | xargs -n1 crictl -r /run/containerd/containerd.sock inspectp > /tmp/flannel_ip_gc_all_pods

       # export and sort pod ip
       cat /tmp/flannel_ip_gc_all_pods | jq -r '.info.cniResult.Interfaces.eth0.IPConfigs[0].IP' | sort > /tmp/flannel_ip_gc_all_pods_ips

       # export flannel's all allocated pod ip
       ls -alh /var/lib/cni/networks/cb0/1* | cut -f7 -d"/" | sort > /tmp/flannel_ip_gc_all_allocated_pod_ips

       # print leaked pod ip
       comm -13 /tmp/flannel_ip_gc_all_pods_ips /tmp/flannel_ip_gc_all_allocated_pod_ips > /tmp/flannel_ip_gc_leaked_pod_ip

       # clean leaked pod ip
       echo "Found $(cat /tmp/flannel_ip_gc_leaked_pod_ip | wc -l) leaked Pod IP, press <Enter> to clean."
       read sure

       # delete leaked pod ip
       for pod_ip in $(cat /tmp/flannel_ip_gc_leaked_pod_ip); do
           rm /var/lib/cni/networks/cb0/${pod_ip}
       done

       echo "Leaked Pod IP cleaned, removing temp file."
       rm /tmp/flannel_ip_gc_all_pods_ips /tmp/flannel_ip_gc_all_pods /tmp/flannel_ip_gc_leaked_pod_ip /tmp/flannel_ip_gc_all_allocated_pod_ips
       ```
3. 将问题节点设置为可调度状态，请参见 [节点排水和调度状态](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-of-node-management/#50c6d833db3rp "")。

## 如何修改节点IP数量、Pod IP网段、Service IP网段？

节点IP数量、Pod IP网段、Service IP网段在集群创建后一律不支持修改，请在创建集群时合理规划您的网段。

## **什么场景下需要为集群配置多个路由表？**

在Flannel网络模式下，以下是需要为cloud-controller-manager配置多路由表的常见场景。关于如何为集群配置多路由表，请参见 [使用VPC的多路由表功能](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-multiple-route-tables-for-a-vpc#task-2057616 "")。

### **问题场景**

- 场景一：

系统诊断中提示“节点Pod网段不在VPC路由表条目中，请参考添加自定义路由条目到自定义路由表添加Pod网段的下一跳路由到当前节点”。

原因：集群中创建自定义路由表时，需要给CCM配置支持多路由表功能。

- 场景二：

cloud-controller-manager组件报错，提示网络异常`multiple route tables found`。

原因：集群中存在多个路由表时，需要给CCM配置支持多路由表功能。

- 场景三：

Flannel网络模式下，新增的集群节点上有NodeNetworkUnavailable污点，而cloud-controller-manager组件没有及时删除该节点污点，导致Pod无法调度。详情请参见 [为什么集群节点有NodeNetworkUnavailable污点？](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/faq-about-container-networks#title-stn-rqy-eva "")。


## **是否支持安装和配置第三方网络插件？**

ACK集群不支持安装和配置第三方网络插件，如果安装了可能会导致集群网络不可用。

## 为什么Pod CIDR地址不足，报错`no IP addresses available in range set`？

这是因为您的ACK集群使用了Flannel网络插件。Flannel定义了Pod网络CIDR，即为每个节点提供一组有限的IP地址用于分配给Pod，且不支持更改。一旦范围内的IP地址用尽，新的Pod便无法在此节点上创建。请释放一些IP地址或重构集群。关于如何规划集群网络，请参见 [ACK托管集群网络规划](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/kubernetes-cluster-network-planning "")。

## **Terway网络模式支持的Pod数量是多少？**

Terway网络模式的集群支持的Pod数量是ECS支持的IP数量。详细信息，请参见 [使用Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#ebecc326b5ams "")。

## **Terway DataPath V2数据面模式**

- 从Terway v1.8.0版本起，新建集群时选择IPvlan选项将默认启用DataPath V2模式。对于已经启用 IPvlan功能的现有集群，数据面维持原有的IPvlan方式。

- DataPath V2是新一代的数据面路径，与原有的IPvlan模式相比，DataPath V2模式具有更好的兼容性。详细信息，请参见 [使用Terway网络插件](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/work-with-terway#task-1797447 "")。


## **如何查看Terway网络Pod生命周期？**

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **守护进程集**。

3. 在 **守护进程集** 页面顶部，单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7208570171/p780316.png)选择 **kube-system** 命名空间。

4. 在 **守护进程集** 页面搜索 **terway-eniip**，单击 **名称** 列表下的 **terway-eniip**。





以下为容器组现状详情的说明：






| **类型** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **类型** | **说明** |
| **Ready** | Pod内的所有容器都已经启动并运行正常。 |
| **Pending** | Pod正在等待Terway为其配置网络资源。<br>Pod因节点资源不足未调度到节点上。详细信息，请参见 [Pod异常问题排查](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/pod-troubleshooting-1#section-elq-kxx-bzx "")。 |
| **ContainerCreating** | Pod已调度至节点，表明Pod正在等待网络初始化完成。 |





更多信息，请参见 [Pod的生命周期](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)。


## **Terway组件升级失败常见问题**

| **问题现象** | **处理办法** |
| --- | --- |

|     |     |
| --- | --- |
| **问题现象** | **处理办法** |
| 升级时提示错误码`eip pool is not supported`。 | EIP功能在Terway组件中已不再支持，如需继续使用此功能，请参见 [将EIP从Terway迁移至ack-extend-network-controller](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/migrate-terway-eip-function-to-ack-extend-network-controller "")。 |

## Terway网络模式下，创建Pod提示找不到mac地址

### **问题现象**

创建Pod失败，提示MAC地址找不到。

```plaintext
failed to do add; error parse config, can't found dev by mac 00:16:3e:xx:xx:xx: not found
```

### **解决办法**

1. 网卡在系统中加载是异步的，在CNI配置时，可能网卡还没有加载成功。这种情况下CNI会自动重试，并不会有影响。请通过Pod最终状态判断是否成功。

2. 如果Pod长时间没有创建成功，并提示上述错误，通常是由于在弹性网卡挂载时，由于高阶内存不足导致驱动加载失败。您可以通过重启实例解决。


## **配置集群本地域名（ClusterDomain）有哪些注意事项？**

ACK集群默认ClusterDomain为`cluster.local`。您也可以在创建集群时自定义集群本地域名。有如下注意事项。

- 仅支持在创建集群时配置，创建后不支持修改。

- 集群ClusterDomain是集群内Service对应域名所在的一级域名，是一个独立的、专门用于集群内部服务的域名解析区域。ClusterDomain需避免与集群外的 [私有](https://dnsnext.console.aliyun.com/privateDNS) 或公网DNS Zone重叠，以避免DNS解析冲突。



**原理说明**






ACK默认使用CoreDNS作为DNS Server。如自定义了ClusterDomain， [CoreDNS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/configure-coredns#section-ynf-vrc-5io "") 默认Corefile配置如下。

















```yaml
    Corefile: |
      .:53 {
          errors
          log
          health {
             lameduck 15s
          }
          ready
          kubernetes {{.ClusterDomain}} in-addr.arpa ip6.arpa {
            pods insecure
            fallthrough in-addr.arpa ip6.arpa
            ttl 30
          }
          ...
          forward . /etc/resolv.conf {
            prefer_udp
          }
          ...
        }
```





未定义ClusterDomain时，对应Corefile配置类似如下。

















```yaml
          kubernetes cluster.local in-addr.arpa ip6.arpa {
            pods insecure
            fallthrough in-addr.arpa ip6.arpa
            ttl 30
          }
          ...
          forward . /etc/resolv.conf {
            prefer_udp
          }
```





CoreDNS处理ClusterDomain的域名解析时，默认不会将这些请求转发给上游DNS Server（即不会触发 `fallthrough` 到 `forward` 插件），以保证集群内DNS查询高效、安全，且不会受到外部网络的影响。如果集群内部的DNS请求被错误地转发给上游DNS Server，它们会继续向上游转发请求，形成递归查询。由于递归查询链路过长，DNS解析请求会超过设定的超时时间，最终导致解析失败。



如果自定义ClusterDomain与集群外的公网一级域名或 [云解析PrivateZone](https://dnsnext.console.aliyun.com/privateDNS) 中已定义的一级域名发生重叠，且集群内所有Pod均使用CoreDNS作为DNS Server，那么CoreDNS不会将ClusterDomain的解析请求转发给上游DNS Server，也就无法正确解析。



此外，如果ClusterDomain与集群外的公网一级域名或 [云解析PrivateZone](https://dnsnext.console.aliyun.com/privateDNS) 中已定义的一级域名发生重叠，同时集群内的一个Service的名称和公网Zone或PrivateZone下存在的子域名重叠，那么CoreDNS会优先解析为集群内Service对应的IP地址，而不是外部的域名，从而导致访问错误。