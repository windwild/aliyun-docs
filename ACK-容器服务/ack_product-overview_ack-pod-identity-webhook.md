### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[产品概述](https://help.aliyun.com/zh/ack/product-overview/)[产品发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-1/)[组件介绍与发布记录](https://help.aliyun.com/zh/ack/product-overview/release-notes-for-components/)[安全](https://help.aliyun.com/zh/ack/product-overview/security-1/)ack-pod-identity-webhook

# ack-pod-identity-webhook组件介绍与变更记录

更新时间：2026-01-29 01:26:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ack-advanced-audit](https://help.aliyun.com/zh/ack/product-overview/ack-advanced-audit)[下一篇：ack-ram-authenticator](https://help.aliyun.com/zh/ack/product-overview/ack-ram-authenticator)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

组件介绍

使用说明

自定义配置

组件配置

命名空间配置

服务账户配置

Pod配置

变更记录

2026年01月

2025年11月

2025年09月

2025年06月

2025年03月

2024年12月

2023年06月

2023年02月

ack-pod-identity-webhook是实现应用免密访问与Pod权限隔离的关键组件。本文介绍ack-pod-identity-webhook组件信息、使用说明及变更记录。

## **组件介绍**

ack-pod-identity-webhook组件基于 Kubernetes 的 [MutatingAdmissionWebhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#mutatingadmissionwebhook) 机制，可以更便捷地使用容器服务提供的RRSA（RAM Roles for Service Accounts）特性，它可以为应用Pod自动注入应用依赖的挂载OIDC Token和环境变量配置，免去繁琐的手动配置工作。

## 使用说明

ack-pod-identity-webhook通过自动化配置 RRSA (RAM Roles for Service Accounts)，使 Pod 能直接扮演 RAM 角色，为集群提供安全、免密且精细到 Pod 级别的云资源权限管理方案。具体操作，请参见 [通过RRSA配置ServiceAccount的RAM权限实现Pod权限隔离](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-rrsa-to-authorize-pods-to-access-different-cloud-services "")。

## 自定义配置

ack-pod-identity-webhook组件的自定义配置包括组件配置、命名空间配置、服务账户配置以及Pod配置。

### **组件配置**

| **参数** | **类型** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **类型** | **说明** |
| `AutoInjectSTSEnvVars` | boolean | > 仅0.4.0及以上版本支持<br>是否启用默认为 Pod 注入 STS 相关环境变量的功能。<br>- `true`：启用该功能。<br>  <br>- `false`：禁用该功能。 |

### 命名空间配置

| **参数** | **类型** | **说明** | **代码示例** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **说明** | **代码示例** |
| `pod-identity.alibabacloud.com/injection` | 标签 | 是否为该命名空间下的Pod启用配置自动注入功能。<br>- `on`：启用命名空间级别的配置自动注入功能。<br>  <br>- 未配置或其他值：禁用命名空间级别的配置自动注入功能。 | ```yaml<br>apiVersion: v1<br>kind: Namespace<br>metadata:<br>  name: test<br>  labels:<br>    pod-identity.alibabacloud.com/injection: 'on'<br>``` |
| `pod-identity.alibabacloud.com/override-env` | 标签 | > 仅0.4.2及以上版本支持<br>是否为该命名空间下的Pod启用配置自动覆盖功能，即当Pod中定义的环境变量与组件注入的环境变量同名时，将以组件注入的环境变量值作为最终生效值。<br>- `true`：启用命名空间级别的配置自动覆盖功能。<br>  <br>- 未配置或其他值：禁用命名空间级别的配置自动覆盖功能。 | ```yaml<br>apiVersion: v1<br>kind: Namespace<br>metadata:<br>  name: test<br>  labels:<br>    pod-identity.alibabacloud.com/override-env: 'true'<br>``` |

### 服务账户配置

| **参数** | **类型** | **说明** | **代码示例** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **说明** | **代码示例** |
| `pod-identity.alibabacloud.com/role-name` | 注解 | 该服务账户关联的RAM角色名称。如未配置或配置的值不是合法的RAM角色名称时，使用该服务账户的Pod将不会被自动注入配置。 | ```yaml<br>apiVersion: v1<br>kind: ServiceAccount<br>metadata:<br>  name: test-sa<br>  namespace: test<br>  annotations:<br>    pod-identity.alibabacloud.com/role-name: test-role<br>``` |
| `pod-identity.alibabacloud.com/service-account-token-expiration` | 注解 | 指定使用该服务账户的Pod挂载的OIDC Token的有效期。<br>取值范围：\[600, 43200\]。单位：秒。<br>默认值为3600。配置值无效时，将使用3600作为此配置项的值。 | ```yaml<br>apiVersion: v1<br>kind: ServiceAccount<br>metadata:<br>  name: test-sa<br>  namespace: test<br>  annotations:<br>    pod-identity.alibabacloud.com/service-account-token-expiration: '3600'<br>``` |
| `pod-identity.alibabacloud.com/inject-sts-endpoint` | 注解 | > 仅0.3.0及以上版本支持<br>是否为使用该服务账户的Pod注入环境变量`ALIBABA_CLOUD_STS_ENDPOINT`。<br>- `on`：启用注入该环境变量。<br>  <br>- 未配置或其他值：禁用注入该环境变量。 | ```yaml<br>apiVersion: v1<br>kind: ServiceAccount<br>metadata:<br>  name: test-sa<br>  namespace: test<br>  annotations:<br>    pod-identity.alibabacloud.com/inject-sts-endpoint: 'on'<br>``` |

### Pod配置

| **参数** | **类型** | **说明** | **代码示例** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **说明** | **代码示例** |
| `pod-identity.alibabacloud.com/injection` | 标签 | > 仅0.2.0及以上版本支持<br>是否为该Pod启用配置自动注入功能。<br>- `on`：启用配置自动注入功能。<br>  <br>- 未配置或其他值：通过命名空间的配置控制是否启用配置自动注入功能。 | ```yaml<br>apiVersion: v1<br>kind: Pod<br>metadata:<br>  name: test<br>  labels:<br>    pod-identity.alibabacloud.com/injection: 'on'<br>``` |
| `pod-identity.alibabacloud.com/override-env` | 注解 | > 仅0.4.2及以上版本支持<br>是否为该Pod启用配置自动覆盖功能。即当Pod中定义的环境变量与组件注入的环境变量同名时，将以组件注入的环境变量值作为最终生效值。<br>- `true`：启用配置自动覆盖功能。<br>  <br>- 未配置或其他值：通过命名空间的配置控制是否启用配置自动覆盖功能。 | ```yaml<br>apiVersion: v1<br>kind: Pod<br>metadata:<br>  name: test<br>  annotations:<br>    pod-identity.alibabacloud.com/override-env: 'true'<br>``` |
| `pod-identity.alibabacloud.com/service-account-token-expiration` | 注解 | 指定该Pod挂载的OIDC Token的有效期。<br>取值范围：\[600, 43200\]。单位：秒。<br>默认值为3600，当配置值无效时，将使用3600作为此配置项的值。<br>**说明**<br>当服务账户和Pod上都存在该配置项时，服务账户上的配置将会被忽略。 | ```yaml<br>apiVersion: v1<br>kind: Pod<br>metadata:<br>  name: test-pod<br>  namespace: test<br>  annotations:<br>    pod-identity.alibabacloud.com/service-account-token-expiration: '3600'<br>``` |
| `pod-identity.alibabacloud.com/only-containers` | 注解 | 限制只为Pod内特定名称的容器自动注入配置，使用英文半角逗号（,）分隔多个容器名称。<br>如果未配置该配置项，将为Pod内所有容器自动注入配置。 | ```yaml<br>apiVersion: v1<br>kind: Pod<br>metadata:<br>  name: test-pod<br>  namespace: test<br>  annotations:<br>    pod-identity.alibabacloud.com/only-containers: 'controller,test'<br>``` |
| `pod-identity.alibabacloud.com/skip-containers` | 注解 | 配置不为特定名称的容器自动注入配置，使用英文半角逗号（,）分隔多个容器名称。<br>**说明**<br>当某个容器名称同时存在于`pod-identity.alibabacloud.com/only-containers`和`pod-identity.alibabacloud.com/skip-containers`配置中时，`pod-identity.alibabacloud.com/only-containers`中的配置将会被自动忽略。 | ```yaml<br>apiVersion: v1<br>kind: Pod<br>metadata:<br>  name: test-pod<br>  namespace: test<br>  annotations:<br>    pod-identity.alibabacloud.com/skip-containers: 'controller,test'<br>``` |

## 变更记录

### 2026年01月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.4.2 | registry-cn-hangzhou.ack.aliyuncs.com/acs/ack-pod-identity-webhook:0.4.2 | 2026年01月29日 | - 新增配置自动覆盖功能，即当Pod中定义的环境变量与组件注入的环境变量同名时，将以组件注入的环境变量值作为最终生效值。可通过`pod-identity.alibabacloud.com/override-env`标签/注解开启命名空间级别或Pod级别的配置自动覆盖功能。<br>  <br>- 升级组件使用的Golang版本至1.25.6，提升组件稳定性。 | 组件升级异常可能会导致Pod创建失败，建议在业务低谷期进行升级操作。 |

### 2025年11月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.4.0 | registry-cn-hangzhou.ack.aliyuncs.com/acs/ack-pod-identity-webhook:0.4.0 | 2025年11月24日 | - 新增默认为 Pod 注入 STS 相关环境变量：`ALIBABA_CLOUD_STS_ENDPOINT`、`ALIBABA_CLOUD_STS_REGION`以及`ALIBABA_CLOUD_VPC_ENDPOINT_ENABLED`。<br>  <br>  可通过设置组件配置项`AutoInjectSTSEnvVars`的值为`false`来禁用该特性。<br>  <br>- 升级组件使用的Golang版本至1.24.10，提升组件稳定性。 | 组件升级异常可能会导致Pod创建失败，建议在业务低谷期进行升级操作。 |

### 2025年09月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.3.1 | registry-cn-hangzhou.ack.aliyuncs.com/acs/ack-pod-identity-webhook:0.3.1 | 2025年09月08日 | 升级组件使用的Golang版本为1.24.6，提升组件稳定性。 | 组件升级异常可能会导致Pod创建失败，建议在业务低谷期进行升级操作。 |

### 2025年06月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.3.0 | registry-cn-hangzhou.ack.aliyuncs.com/acs/ack-pod-identity-webhook:v0.3.0.0-g433f84b-aliyun | 2025年06月06日 | 新增支持通过ServiceAccount配置`pod-identity.alibabacloud.com/inject-sts-endpoint`，开启为Pod注入环境变量`ALIBABA_CLOUD_STS_ENDPOINT`。 | 组件升级异常可能会导致Pod创建失败，建议在业务低谷期进行升级操作。 |

### 2025年03月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.1 | registry-cn-hangzhou.ack.aliyuncs.com/acs/ack-pod-identity-webhook:v0.2.1.0-g52e519c-aliyun | 2025年03月18日 | 升级组件使用的Golang版本为1.23.7，提升组件稳定性。 | 组件升级异常可能会导致Pod创建失败，建议在业务低谷期进行升级操作。 |

### 2024年12月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.2.0 | registry-cn-hangzhou.ack.aliyuncs.com/acs/ack-pod-identity-webhook:v0.2.0.11-g2f0c2e7-aliyun | 2024年12月19日 | - 新增支持通过增加Pod标签`pod-identity.alibabacloud.com/injection: 'on'`启用配置注入。<br>  <br>- 优化对Kubernetes 1.32版本的支持。 | 组件升级异常可能会导致Pod创建失败，建议在业务低谷期进行升级操作。 |

### 2023年06月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.1.1 | registry.cn-hangzhou.aliyuncs.com/acs/ack-pod-identity-webhook:v0.1.1.0-gbddcb74-aliyun | 2023年06月07日 | 增强组件对ACK Serverless集群的兼容性。 | 组件升级异常可能会导致Pod创建失败，建议在业务低谷期进行升级操作。 |

### 2023年02月

| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **版本号** | **镜像地址** | **变更时间** | **变更内容** | **变更影响** |
| 0.1.0 | registry.cn-hangzhou.aliyuncs.com/acs/ack-pod-identity-webhook:v0.1.0.9-g26b8fde-aliyun | 2023年02月01日 | 实现为应用Pod自动挂载OIDC Token以及自动配置环境变量的功能。 | 首个版本。 |