### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Serverless集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/)[安全合规](https://help.aliyun.com/zh/ack/serverless-kubernetes/security-and-compliance/)安全体系概述

# 安全体系概述

更新时间：2025-08-17 22:21:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：通过ACK Serverless创建Spark计算任务](https://help.aliyun.com/zh/ack/serverless-kubernetes/use-cases/use-ask-to-create-spark-tasks)[下一篇：安全责任共担模型](https://help.aliyun.com/zh/ack/serverless-kubernetes/security-and-compliance/shared-responsibility-model)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

运行时安全

可信软件供应链

基础架构安全

本文从运行时安全、可信软件供应链和基础架构安全三个维度介绍阿里云容器服务Kubernetes版的安全体系，包括安全巡检、策略管理、运行时监控和告警、镜像扫描、镜像签名、云原生应用交付链、默认安全、身份管理、细粒度访问控制等。

![61](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2124139061/p203109.png)

## 运行时安全

- 安全巡检

集群的应用开发人员应该遵循权限的最小化原则配置应用部署模板，攻击者往往是利用应用Pod中开启的不必要的特权能力发起逃逸攻击，因此阿里云容器服务Kubernetes版ACK（Alibaba Cloud Container Service for Kubernetes）提供了应用运行时刻的安全配置巡检能力，帮助您实时了解当前状态下运行应用的配置是否存在安全隐患。

巡检结果支持以报表化的方式展示，同时展示巡检对应扫描项的说明和修复建议。您还可以配置定期巡检，对应的扫描结果会写入到SLS指定的日志库中存储。具体操作，请参见 [使用配置巡检检查集群Workload安全隐患](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/use-the-inspection-feature-to-detect-security-risks-in-the-workloads-of-an-ack-cluster#task-2552179 "")。

- 策略管理

ACK基于使用OPA策略的Gatekeeper准入控制器，扩展了策略治理状态统计和日志上报检索等能力，同时内置了种类丰富的策略治理规则库，提供更多符合K8s应用场景的策略规则。您可以在容器服务管理控制台上进行策略治理规则可视化配置，降低使用策略治理相关能力的门槛。更多信息，请参见 [配置容器安全策略（新版）](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/configure-and-enforce-ack-pod-security-policies "")。

通过使用ACK策略管理能力，可以帮助企业安全运维人员在应用部署阶段自动化阻断不符合策略要求的风险应用，提升集群内应用运行时安全水位，降低企业应用开发和运维团队的沟通和学习成本。

- 运行时监控和告警



当容器应用通过API Server的认证鉴权和准入控制校验成功部署后，在云原生应用零信任的安全原则下，还需要在容器应用的运行时刻提供相应的安全监控和告警能力。因此，阿里云容器服务和云安全中心深度集成了告警处理和漏洞检测能力，集群管理员可以在应用运行时提供监控和告警能力，主要的容器侧攻击防护行为如下：



  - 恶意镜像启动告警。

  - 病毒和恶意程序的查杀。

  - 容器内部入侵告警。

  - 容器逃逸和高风险操作预警。


您可以在集群管理页面的**安全管理** \> **安全监控**页面实时接收到相应告警，并根据页面提示查看和处理告警详情。具体操作，请参见 [使用安全监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/use-security-monitoring-capabilities#task-1930740 "")。

- 安全沙箱管理

相比于原有Docker运行时，安全沙箱为您提供了一种新的容器运行时选项，可以让您的应用运行在一个轻量虚拟机沙箱环境中，拥有独立的内核，具备更好的安全隔离能力。

安全沙箱特别适合于不可信应用隔离、故障隔离、性能隔离、多用户间负载隔离等场景。在提升安全性的同时，对性能影响非常小，并且具备与Docker容器一样的用户体验，例如日志、监控、弹性等。关于安全沙箱管理的详细介绍，请参见 [安全沙箱](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-10/#concept-2329190 "")。

- ACK-TEE机密计算

当面向诸如金融、政府等有很强安全诉求的应用场景时，ACK-TEE机密计算提供了基于硬件加密技术的云原生一站式机密计算容器平台 ，它可以帮助您保护数据使用（计算）过程中的安全性、完整性和机密性，同时简化了可信或机密应用的开发、交付和管理成本。

机密计算可以让您把重要的数据和代码放在一个特殊的可信执行加密环境（Trusted Execution Environment，TEE）中，而不会暴露给系统其他部分，其他应用、BIOS、OS、Kernel、管理员、运维人员、云厂商，甚至除了CPU以外的其他硬件均无法访问机密计算平台数据，极大减少敏感数据的泄露风险，为您提供了更好的控制、透明度和隐秘性。更多信息，请参见 [ACK-TEE机密计算](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/tee-based-confidential-computing/#task-2490003 "")。


## 可信软件供应链

- 镜像扫描

容器镜像服务支持所有基于Linux的容器镜像安全扫描，可以识别镜像中已知的漏洞信息。您可以收到相应的漏洞信息评估和相关的漏洞修复建议，为您大幅降低使用容器的安全风险。容器镜像服务也接入了云安全的扫描引擎，可支持镜像系统漏洞、镜像应用漏洞和镜像恶意样本的识别。关于镜像扫描的详细介绍，请参见 [容器镜像安全扫描](https://help.aliyun.com/zh/acr/user-guide/scan-container-images#task-2458925 "")。

- 镜像签名

在容器镜像管理中，您可以通过内容可信的机制保障镜像来源的安全性及不被篡改。镜像的创建者可以对镜像做数字签名，数字签名将保存在容器镜像服务中。通过在部署前对容器镜像进行签名验证可以确保集群中只部署可信授权方签名的容器镜像，降低在您的环境中运行意外或恶意代码的风险，确保从软件供应链到容器部署流程中应用镜像的安全和可溯源性。关于镜像签名和验签的配置使用流程，请参见 [使用kritis-validation-hook组件实现自动验证容器镜像签名](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-kritis-validation-hook-to-automatically-verify-the-signatures-of-container-images#task-2479083 "")。

- 云原生应用交付链

在容器安全高效交付场景中，您可以使用容器镜像服务的云原生应用交付链功能，配置镜像构建、镜像扫描、镜像全球同步和镜像部署等，自定义细粒度安全策略，实现全链路可观测、可追踪的安全交付。保障代码一次提交，全球多地域安全分发和高效部署，将DevOps的交付流程全面升级成DevSecOps。关于云原生应用交付链的详细介绍，请参见 [创建交付链](https://help.aliyun.com/zh/acr/user-guide/create-a-delivery-chain#task-2345265 "")。


## 基础架构安全

- 默认安全



阿里云容器服务Kubernetes版ACK（Alibaba Cloud Container Service for Kubernetes）集群节点，控制面组件配置基于阿里云Kubernetes安全加固能力加固，且集群内所有系统组件均依据容器安全最佳实践进行了组件配置上的加固，同时保证系统组件镜像没有严重级别的CVE漏洞。



  - 每个新建的集群会默认分配一个与之对应的安全组，该安全组对于公网入方向仅允许ICMP请求。创建的集群默认不允许公网SSH连接，如果您需要配置通过公网SSH连接到集群节点，具体操作，请参见 [通过SSH连接ACK专有版集群的Master节点](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-ssh-to-connect-to-the-master-nodes-of-a-dedicated-kubernetes-cluster#task-1664343 "")。

  - 集群节点通过NAT网关访问公网，可以进一步减少安全风险。

  - 在托管集群的Worker节点上，遵循权限最小化原则，节点上绑定的RAM角色对应的阿里云资源访问权限经过了最小化收敛。更多信息，请参见 [【产品变更】托管集群节点RAM角色收敛公告](https://help.aliyun.com/zh/ack/product-overview/ack-reduces-the-permissions-of-worker-ram-roles-in-managed-kubernetes-clusters#concept-2485733 "")。


- 身份管理

ACK集群内所有组件之间的通讯链路均需要TLS证书校验，保证全链路通讯的数据传输安全，同时ACK管控侧会负责集群系统组件的证书自动更新。RAM账号或角色扮演用户均可以通过控制台或OpenAPI的方式获取连接指定集群API Server的Kubeconfig访问凭证，具体操作，请参见 [获取集群KubeConfig接口](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/developer-reference/api-query-the-kubeconfig-file-of-a-cluster#doc-api-CS-DescribeClusterUserKubeconfig "")。ACK负责维护访问凭证中签发的身份信息，对于可能泄露的已下发Kubeconfig，可以及时进行吊销操作，具体操作，请参见 [吊销集群的KubeConfig凭证](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/revoke-a-kubeconfig-credential#task-2333177 "")。

在集群创建时，ACK支持 **服务账户令牌卷投影**（Service Account Token Volume Projection）特性以增强在应用中使用ServiceAccount的安全性。具体操作，请参见 [部署服务账户令牌卷投影](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/enable-service-account-token-volume-projection#task-2460323 "")。

- 细粒度访问控制

基于Kubernetes RBAC实现了对ACK集群内Kubernetes资源的访问控制，它是保护应用安全的一个基本且必要的加固措施。ACK在控制台的 **授权管理** 页面中提供了命名空间维度的细粒度RBAC授权能力，主要包括以下几点。


  - 根据企业内部不同人员对权限需求的不同，系统预置了管理员、运维人员、开发人员等对应的RBAC权限模板，降低了RBAC授权的使用难度。

  - 支持多集群和多个子账号的批量授权。

  - 支持RAM角色扮演用户的授权。

  - 支持绑定用户在集群中自定义的ClusterRole。


更多信息，请参见 [配置RAM用户或RAM角色的RBAC权限](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/grant-rbac-permissions-to-ram-users-or-ram-roles#task-1664343 "")。

ACK同时支持以组件管理的方式安装Gatekeeper组件，提供基于OPA策略引擎的细粒度访问控制能力。具体操作，请参见 [gatekeeper](https://help.aliyun.com/zh/ack/product-overview/gatekeeper#task-1938542 "")。

- 审计



ACK和SLS日志服务进行了深度集成，支持多种审计日志的采集、检索和图表化展示功能，具体包括以下三种：



  - 集群API Server审计日志：帮助您记录或追溯集群访问者的日常操作，是集群安全运维中的重要环节。在 **集群审计** 页面，您可以查看内容丰富的审计报表，同时可基于日志内容设置对指定资源类型操作的实时告警。具体操作，请参见 [使用集群API Server审计功能](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/work-with-cluster-auditing#task-1797722 "")。

  - Ingress流量审计：通过不同的可视化流量报表帮助您了解集群Ingress的整体状态，比如服务访问的PV和UV，成功和失败比例，以及延迟信息等全方位的流量监控，同时支持基于日志服务提供的机器学习算法，通过多种时序分析算法从Ingress的指标中自动检测异常点，提高问题发现的效率。具体操作，请参见 [Nginx Ingress访问日志分析与监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/analyze-and-monitor-the-access-log-of-nginx-ingress#task-1796525 "")。

  - 事件监控审计：基于事件的监控可以帮助您通过事件获取，实时诊断集群的异常和安全隐患。更多信息，请参见 [事件监控](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/event-monitoring#task-1461430 "")。


- Secret落盘加密

Kubernetes原生的Secret模型在etcd落盘时只经过了Base64编码，为了保护Secret中敏感数据的落盘安全性，在ACK Pro托管集群中，您可以使用在阿里云密钥管理服务KMS（Key Management Service）中创建的密钥加密Kubernetes集群Secret，实现应用敏感数据的落盘加密。具体操作，请参见 [使用阿里云KMS进行Secret的落盘加密](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/security-and-compliance/use-kms-to-encrypt-kubernetes-secrets-2#task-2568562 "")。