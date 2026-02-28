### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[分布式云容器平台ACK One](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/)[操作指南](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/)[注册集群](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/registered-clusters/)[接入云上Serverless算力](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/integrate-serverless-computing-power-on-the-cloud/)[ACS算力](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/acs-computing-power/)[ACS算力高级配置](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/advanced-configuration-for-acs-compute-resources/)ACS Pod Annotation功能说明

# ACS Pod Annotation功能说明

更新时间：2025-03-12 05:10:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：通过配置项eci-profile配置ACS算力参数](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/configure-computing-power-through-eci-profile-configmap)[下一篇：ack-virtual-node组件权限说明与自定义指南](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/permissions-specifications-and-customization-guide-for-ack-virtual-node)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

ACS Pod支持配置的Annotation

网络

镜像

ACS自动追加的Annotation

ACS Pod支持通过Annotation的方式进行部分扩展功能的开启和配置。本文介绍ACS支持的所有Pod Annotation的定义和功能。

## **ACS Pod支持配置的Annotation**

您可以通过Pod Annotation中配置支持的Key和Value以开启相关功能和配置，示例如下。

Pod配置示例

Deployment配置示例

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: annotation-pod
  annotations:
    network.alibabacloud.com/vswitch-ids: "vsw-foo"
spec:
  ...
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: foo
  ...
spec:
  ...
  template:
    metadata:
      annotations:
        network.alibabacloud.com/vswitch-ids: "vsw-foo"
    ...
```

## 网络

| **功能** | **参数** | **示例值** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能** | **参数** | **示例值** | **说明** |
| [为Pod指定交换机和安全组](https://help.aliyun.com/zh/cs/user-guide/specify-vswitch-and-securitygroups-for-the-pod "") | network.alibabacloud.com/vswitch-ids | "vsw-slw1\*\*\*,vsw-lkjwo\*\*\*" | 指定交换机ID，支持指定多个交换机开启多可用区创建Pod功能。 |
| network.alibabacloud.com/security-group-ids | "sg-sljwo\*\*\*,sg-lwirp\*\*\*" | 指定安全组ID，支持指定多个安全组。 |
| [为ACS Pod配置自定义DNS](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/configure-custom-dns-for-acs-pods "") | network.alibabacloud.com/custom-dnsconfig | {"servers":\["20.1.xx.xx","30.1.xx.xx"\],"searches":\["xx.com","yy.com"\],"options":\["ndots:2","edns0"\]} | 指定自定义DNS配置。 |
| [在ACS集群中使用网络策略](https://help.aliyun.com/zh/cs/user-guide/use-network-policies-in-container-compute "") | alibabacloud.com/enable-network-policy-agent | "true" | 对ACS Pod启用NetworkPolicy。默认值为`false`。 |
| [为Pod挂载独立公网EIP](https://help.aliyun.com/zh/cs/user-guide/mount-an-independent-public-network-eip-for-a-pod/ "") | network.alibabacloud.com/pod-with-eip | "true" | 是否自动创建并绑定EIP。取值：<br>- `true`：自动创建并绑定EIP。<br>  <br>- `false`：不自动创建并绑定EIP。 |
| network.alibabacloud.com/pod-eip-instanceid | "eip-bp14q\*\*\*" | 使用指定的EIP，请填写EIP实例ID，例如：eip-bp14q\*\*\*。更多信息，请参见 [申请EIP](https://help.aliyun.com/zh/eip/apply-for-new-eips#task-bh5-dll-vdb "")。 |
| k8s.aliyun.com/eci-eip-instanceid（兼容ECI注解） |
| network.alibabacloud.com/eip-bandwidth | "5" | EIP峰值带宽，单位：Mbps。 |
| network.alibabacloud.com/eip-internet-charge-type | "PayByTraffic" | EIP流量的计费方式。取值：<br>- `PayByTraffic`： **默认值**，按使用流量计费。<br>  <br>- `PayByBandwidth`：按带宽计费。<br>  <br>更多信息，请参见 [EIP计费方式](https://help.aliyun.com/zh/eip/product-overview/billing-overview/#section-j0c-7wh-cko "")。 |
| k8s.aliyun.com/eip-charge-type（兼容早期版本的注解） |
| network.alibabacloud.com/eip-instance-charge-type | "PrePaid" | EIP实例的付费模式。取值：<br>- `PrePaid`：包年包月。<br>  <br>- `PostPaid`：按量计费。<br>  <br>更多信息，请参见 [包年包月](https://help.aliyun.com/zh/eip/product-overview/subscription#task-2240237 "") 和 [按量付费](https://help.aliyun.com/zh/eip/product-overview/pay-as-you-go/#task-rcd-sgl-vdb "")。 |
| network.alibabacloud.com/eip-common-bandwidth-package-id | "cbwp-slex\*\*\*" | 绑定已有的共享带宽包。 |
| network.alibabacloud.com/eip-isp | "BGP" | EIP的线路类型。取值：<br>- `BGP`：BGP（多线）线路。<br>  <br>- `BGP_PRO`：BGP（多线）精品线路。<br>  <br>更多信息，请参见 [申请EIP](https://help.aliyun.com/zh/eip/apply-for-new-eips#task-bh5-dll-vdb "")。 |
| network.alibabacloud.com/eip-public-ip-address-pool-id | "pippool-dlsw\*\*\*" | EIP地址池。关于EIP地址池的使用限制、使用步骤等，请参见 [创建和管理IP地址池](https://help.aliyun.com/zh/eip/create-and-manage-ip-address-pools "")。 |
| network.alibabacloud.com/eip-resource-group-id |  | EIP资源组。更多信息，请参见 [申请EIP](https://help.aliyun.com/zh/eip/apply-for-new-eips#task-bh5-dll-vdb "")。 |
| network.alibabacloud.com/eip-name |  | EIP名称。更多信息，请参见 [申请EIP](https://help.aliyun.com/zh/eip/apply-for-new-eips#task-bh5-dll-vdb "")。 |
| network.alibabacloud.com/eip-description |  | EIP描述。更多信息，请参见 [申请EIP](https://help.aliyun.com/zh/eip/apply-for-new-eips#task-bh5-dll-vdb "")。 |
| network.alibabacloud.com/eip-security-protection-types |  | EIP安全防护级别。若配置多个，请通过半角逗号`,`分隔。更多信息，请参见 [申请EIP](https://help.aliyun.com/zh/eip/apply-for-new-eips#task-bh5-dll-vdb "")。 |
| network.alibabacloud.com/pod-eip-release-strategy | "Never" | Pod EIP的回收策略。取值：<br>- `Follow`： **默认值**，跟随Pod生命周期。<br>  <br>- `Never`：不删除Pod EIP。当不需要时需要手动删除这个Pod EIP。 <br>  <br>- 配置过期时间，例如：`5m30s`，表示在Pod删除5分钟30秒之后删除Pod EIP。支持符合规范的Go类型时间表达式。 |

## **镜像**

| **功能** | **参数** | **示例值** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能** | **参数** | **示例值** | **说明** |
| [使用自建镜像仓库创建ACS Pod](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/create-an-acs-pod-using-a-user-built-image-repository "") | registry.alibabacloud.com/plain-http-registry | "harbor\*\*\*.pre.com,192.168.XX.XX:5000,reg\*\*\*.test.com:80" | 拉取采用HTTP协议的自建镜像仓库中的镜像时，需配置该参数，避免因协议不同而导致镜像拉取失败。 |
| registry.alibabacloud.com/insecure-registry | "harbor\*\*\*.pre.com,192.168.XX.XX:5000,reg\*\*\*.test.com:80" | 拉取使用自签发证书的自建镜像仓库中的镜像时，需要配置该参数来跳过证书认证，避免因证书认证失败而导致镜像拉取失败。 |

## ACS自动追加的Annotation

**说明**

以下Annotation信息为ACS相关功能处理完成后产生的结果信息，如网卡分配结果和EIP分配结果等，这部分Annotation参数不允许用户进行设置和修改。

| **功能** | **参数** | **示例值** | **说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **功能** | **参数** | **示例值** | **说明** |
| 网卡分配信息 | network.alibabacloud.com/allocated-eni-id | "eni-esdxs\*\*\*" | 分配的网卡（ENI）ID。 |
| network.alibabacloud.com/vpc-id | "vpc-sljwo\*\*\*" | 当前网卡归属的VPC ID。 |
| network.alibabacloud.com/vswitch-id | "vsw-lskdw\*\*\*" | 当前网卡归属的交换机ID，如果您创建ACS Pod时指定了多个交换机，这里展示的是最终使用的交换机。 |
| EIP分配信息 | network.alibabacloud.com/allocated-eip-id | "eip-bp1m\*\*\*" | 分配的EIP ID信息。 |
| network.alibabacloud.com/allocated-eip-address | "116.62.\*\*\*" | 分配的EIP的IP地址。 |
| 资源规格 | alibabacloud.com/pod-use-spec | "2.5-5Gi" | 规格规整后ACS Pod的CPU/Memory规格，表示的格式和单位是为"xxvCPU-xxGiB"。 |
| alibabacloud.com/pod-gpu-use-spec | "1" | 规格规整后ACS Pod的GPU卡数量。 |
| alibabacloud.com/pod-ephemeral-storage | "30Gi" | 规格规整后ACS Pod的临时存储空间大小，单位是GiB。 |
| 调度结果信息 | topology.kubernetes.io/region | "cn-hangzhou" | ACS Pod的所属地域。 |
| topology.kubernetes.io/zone | "cn-hangzhou-i" | ACS Pod的所属可用区。 |
| 其他元信息 | alibabacloud.com/instance-id | "acs-sdsf\*\*\*" | ACS Pod实例ID。 |
| alibabacloud.com/request-id | "6925D4B7-\*\*\*" | 请求ID。 |