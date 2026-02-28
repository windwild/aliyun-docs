### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Serverless集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/)[安全合规](https://help.aliyun.com/zh/ack/serverless-kubernetes/security-and-compliance/)安全责任共担模型

# 安全责任共担模型

更新时间：2024-05-23 02:38:28

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：安全体系概述](https://help.aliyun.com/zh/ack/serverless-kubernetes/security-and-compliance/security-system-overview)[下一篇：安全概览](https://help.aliyun.com/zh/ack/serverless-kubernetes/security-and-compliance/security-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

阿里云负责

客户负责

理解责任共担模型

安全合规在ACK集群托管架构下遵循责任共担原则，其中容器服务ACK负责集群控制面组件（包括Kubernetes控制平面组件和etcd）以及集群服务相关阿里云基础设施的默认安全性。本文介绍阿里云容器服务ACK的安全责任共担模型。

## 阿里云负责

首先在管控面侧，阿里云会通过完备的平台安全能力负责管控侧基础设施（包括计算、存储、网络等云服务资源）的安全性；同时基于阿里云OS安全加固等业务通用的安全标准基线，对ACK集群管控面组件配置和镜像进行符合标准定义的安全加固。针对集群节点OS或K8s组件层面的安全漏洞，阿里云会负责及时提供相关公告并发布对应的漏洞补丁或版本更新能力。同时阿里云会面向企业云原生应用生命周期中安全防护的典型场景，提供必要的 [安全防护功能](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/security-system-overview#concept-jyf-5sb-wdb "") 和 [最佳实践指导](https://help.aliyun.com/document_detail/347684.html#task-2134590 "")。

## 客户负责

客户的安全管理运维人员需要负责部署在云上的业务应用安全防护以及对云上资源的安全配置和更新，包含以下内容：

- 基于阿里云公告和提供的补丁或版本升级方式及时进行OS、集群侧系统组件、运行时等漏洞的修复和版本更新。

- 遵循安全原则进行ACK集群、节点池和网络等参数配置，避免因为不当的参数或权限配置给攻击者可乘之机。

- 基于使用需求，遵循权限最小化原则进行应用或账号、角色的授权，凭据的管理，相关安全策略的部署实施以及应用自身参数配置安全。

- 负责应用制品的供应链安全。

- 负责应用敏感数据和应用运行时刻的安全。

- 对于离职员工或非受信人员，删除RAM用户或RAM角色并不会同步删除该用户或角色拥有的集群KubeConfig中的RBAC权限。因此，在删除RAM用户或RAM角色之前，请吊销离职员工或非受信用户的KubeConfig权限。具体操作，请参见 [吊销集群的KubeConfig凭证](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/revoke-a-kubeconfig-credential "")。


## 理解责任共担模型

在您设计和部署企业应用系统之前，请您充分理解企业自身和阿里云的安全责任边界。

ACK托管架构下集群安全的责任共担模型如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6036446171/CAEQQRiBgIDS68aD9xgiIDA2MWY2NmI2ZjBlZDQ0MzM5YTU2ZGM3ODZmM2MwMzcx3963382_20230830144006.372.svg)

当您选择使用ACK Serverless集群或在ACK托管集群中部署虚拟节点组件（ack-virtual-node）时，除了集群控制面和基础设施安全外，阿里云还将负责Pod底层 [弹性容器实例（ECI）运行时](https://help.aliyun.com/zh/eci/product-overview/what-is-elastic-container-instance "") 的安全，由客户负责重建应用Pod以使修复生效。下图为Serverless架构下使用ACK Serverless集群或在ACK托管集群中部署虚拟节点组件（ack-virtual-node）时的安全责任共担模型。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6036446171/CAEQQRiBgMDuhcmD9xgiIDgyMTgyZDdkMjM3NTQxZDViYTY3ZGZlZjUzM2JkNTAw3963382_20230830144006.372.svg)

对于使用 [托管节点池](https://help.aliyun.com/zh/ack/overview-of-managed-node-pools#task-1998740 "") 的ACK集群，阿里云会负责根据客户对于托管节点池的配置尝试自动化的修复节点OS漏洞和Kubelet版本升级，其中，节点OS漏洞的修复补丁由 [云安全中心](https://help.aliyun.com/zh/security-center/user-guide/purchase-security-center#task-lxj-3bc-zdb "") 提供。如果集群节点使用的是自定义OS镜像，仍需要由客户负责节点漏洞的修复更新。下图为托管架构下ACK集群使用托管节点池时的安全责任共担模型。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7036446171/CAEQQRiBgMCj4cyD9xgiIDcyNjQwMTQ3MzhiODRkMjlhYmQ3NmE4YzNmZGZkYTRh3963382_20230830144006.372.svg)