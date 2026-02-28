### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[其他](https://help.aliyun.com/zh/ack/product-overview/others/)（停止维护）resource-controller

# （停止维护）resource-controller

更新时间：2024-09-23 03:21:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ack-koordinator（ack-slo-manager）](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager)[下一篇：Argo Workflows](https://help.aliyun.com/zh/ack/product-overview/argo-workflows)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

卸载resource-controller

变更记录

本文介绍resource-controller组件相关内容的最新动态。

## 组件介绍

目前，ack-slo-manager已经适配了resource-controller的所有功能，并在原组件的基础上进行了优化，resource-controller于2022年10月14日下线。您可访问 [ack-koordinator（ack-slo-manager）](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#task-2172306 "")，获取相关功能的使用说明。若您正在使用resource-controller，请参考 [组件迁移](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#section-9yj-oaq-ilp "") 完成迁移。

## 卸载resource-controller

为了方便从resource-controller迁移到 [ack-koordinator（ack-slo-manager）](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#task-2172306 "")，从v1.2.3-ea712cc6-aliyun版本起，resource-controller卸载后不会直接删除Cgroup CRD。关于Cgroup CRD的更多信息，请参见 [动态修改Pod资源参数](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/dynamically-modify-the-resource-parameters-of-a-pod#task-2017508 "")。若您卸载后不再使用Cgroup CRD的相关功能，请参考以下步骤及时清理集群中剩余的Cgroup CR对象，避免后续对ack-slo-manager功能的使用产生干扰。

卸载resource-controller及删除Cgroup CR对象的具体步骤如下：

1. 卸载resource-controller。具体操作，请参见 [管理组件](https://help.aliyun.com/zh/ack/manage-system-components#task-z3j-tvk-2gb "")。

2. 删除Cgroup CR对象。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏单击 **集群**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，选择**工作负载** \> **自定义资源**。

3. 在 **自定义资源** 页面单击 **资源定义（CustomResourceDefinition）** 页签，然后单击 **Cgroups**。

4. 在 **资源对象浏览器** 页签，选择 **命名空间** 为 **所有命名空间**。

5. 在下方列表中，勾选所有Cgroups对象，单击 **删除**，然后在 **确认删除** 对话框，单击 **确定**。

## 变更记录

**2022年08月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 1.2.3-ea712cc6-aliyun | - registry.cn-hangzhou.aliyuncs.com/acs/node-resource-agent:v21.5.20.1-2f4c30e-aliyun<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/resource-controller:v1.2.3-ea712cc6-aliyun | 2022年08月04日 | 优化内部相关接口，便于将组件升级至 [ack-koordinator（ack-slo-manager）](https://help.aliyun.com/zh/ack/product-overview/ack-koordinator-fka-ack-slo-manager#task-2172306 "")。 | 组件卸载后会保留Cgroup CRD对象，请参考 [卸载resource-controller](https://help.aliyun.com/zh/ack/product-overview/resource-controller#section-5em-eoi-19v "") 完成组件的卸载。 |

**2021年06月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v1.2.2-0ac97de0-aliyun | - registry.cn-hangzhou.aliyuncs.com/acs/node-resource-agent:v21.3.9.0-adecd8a-aliyun<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/resource-controller:v1.2.2-0ac97de0-aliyun | 2021年06月21日 | 增加MBA控制、修复Change Memory和Containerd、升级client-go 。 | 无 |

**2021年05月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v1.2.1-d1e280f-aliyun | - registry.cn-hangzhou.aliyuncs.com/acs/node-resource-agent:v21.3.9.0-adecd8a-aliyun<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/resource-controller:v1.2.1-d1e280f-aliyun | 2021年05月21日 | 增加L3控制、适配AMD拓扑感知调度。 | 无 |

**2021年04月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v1.2.0-ec8a979-aliyun | - registry.cn-hangzhou.aliyuncs.com/acs/node-resource-agent:v21.3.9.0-adecd8a-aliyun<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/resource-controller:v1.2.0-ec8a979-aliyun | 2021年04月20日 | 适配containerd、多container、meta-data访问、container粒度日志、增加实时动态水位控制等。 | 无 |

**2021年03月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v1.1.0-e7388cb | - registry.cn-hangzhou.aliyuncs.com/acs/node-resource-agent:v21.3.9.0-adecd8a-aliyun<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/resource-controller:v1.1.0-e7388cb | 2021年03月09日 | 发布node-agent，为记录numainfo的configmap添加`label`字段。 | 无 |

**2021年01月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v1.1.0-e7388cb | - registry.cn-hangzhou.aliyuncs.com/acs/node-resource-agent:121ffbe<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/resource-controller:v1.1.0-e7388cb | 2021年01月26日 | resource-controller支持分布式部署分发、cpuset参数调节等。 | 无 |