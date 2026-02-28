### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[其他](https://help.aliyun.com/zh/ack/product-overview/others/)Argo Workflows

# Argo Workflows

更新时间：2025-07-27 22:19:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：（停止维护）resource-controller](https://help.aliyun.com/zh/ack/product-overview/resource-controller)[下一篇：AHPA Controller](https://help.aliyun.com/zh/ack/product-overview/application-intelligence-controller)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

安装Argo Workflows

变更记录

2024年11月

2022年03月

Argo Workflows是专为Kubernetes设计的编排批量任务的云原生工作流引擎，是CNCF毕业项目，符合用户采用、安全、广泛度的最高标准。本文介绍Argo Workflows组件的信息、安装步骤和变更记录。

## 组件介绍

该组件基于原生Argo Workflows开发，并在其基础上有稳定性和性能等方面的增强，支持您在集群中部署大型工作流。主要面向标准化的工作流场景，例如机器学习Pipeline、自动驾驶仿真、基因测序任务、批量数据处理、CI/CD、基础设施自动化等。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5619663571/CAEQURiBgICv4.v3mRkiIDBjOWY1ZDQ4YWZiYTQ4NjliODg5NDIzYzQ4NTlmYmU04764568_20241118094608.772.svg)

## 使用说明

- 若您有大规模任务编排、免运维、高性能等需求，建议使用 [Serverless Argo Workflows](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/overview-12 "")

- 关于如何提交工作流，请参考 [管理工作流](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/workflow/ "")，若您想获取更多最佳实践，请参见 [最佳实践](https://help.aliyun.com/zh/ack/distributed-cloud-container-platform-for-kubernetes/user-guide/best-practices/ "")。

- 若您有其他建议或疑问，请加入钉钉群（钉钉群号： **35688562**），联系产品技术专家进行反馈。


## 安装Argo Workflows

您可以通过容器服务ACK的组件管理页面安装Argo Workflows，具体操作如下：

1. 安装Argo Workflows。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)，在左侧导航栏选择 **集群列表**。

2. 在 **集群列表** 页面，单击目标集群名称，然后在左侧导航栏，单击 **组件管理**。

3. 在 **组件管理** 页面，搜索 **Argo Workflows**。

4. 在 **Argo Workflows** 卡片，单击 **安装**。

5. 在弹出的 **安装组件Argo Workflows** 对话框单击 **确认**。
2. 查看Argo Workflows部署状态。

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)。

2. 在 **集群列表** 页面，单击目标集群名称或者目标集群右侧 **操作** 列下的 **详情**。

3. 在集群管理页左侧导航栏中，选择**应用** \> **Helm**。

4. 在 **Helm** 页面，查看Argo Workflows的部署状态。



      当ack-workflow的 **状态** 显示为 **已部署**，说明Argo Workflows部署成功。

## 变更记录

### **2024年11月**

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v3.5.12-4ad4d3b | - registry.cn-hangzhou.aliyuncs.com/acs/workflow-controller:v3.5.12-4ad4d3b<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/argo:v3.5.12-4ad4d3b<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/argoexec:v3.5.12-4ad4d3b | 2024年11月15日 | 发布3.5.12。 | 无 |

### 2022年03月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| v3.3-0d060b7 | - registry.cn-hangzhou.aliyuncs.com/acs/workflow-controller:v3.3-0287b37<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/argo:v3.3-0287b37<br>  <br>- registry.cn-hangzhou.aliyuncs.com/acs/argoexec:v3.3-0d060b7 | 2022年03月29日 | 新增Argo Workflows组件。 | 无 |