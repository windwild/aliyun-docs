### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)权限管理

# 权限管理

更新时间：2024-12-27 00:43:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：事件中心](https://help.aliyun.com/zh/sae/event-center-new)[下一篇：权限策略和示例](https://help.aliyun.com/zh/sae/policies-and-examples-2-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能概述

背景信息

业务场景

场景一

场景二

场景三

场景四

场景五

Serverless应用引擎SAE（Serverless App Engine）的权限管理通过阿里云访问控制RAM（Resource Access Management）产品实现。权限管理帮助您对资源数据进行必要的隔离和权限控制，以保证安全性。本文以某企业的日常业务为例，介绍SAE权限管理的应用场景与功能实现。

## 功能概述

- 如果您需要系统地了解SAE权限管理的内容，可以通过本文的应用场景示例，逐步学习与SAE相关的权限功能。具体信息，请参见 [背景信息](https://help.aliyun.com/zh/sae/permission-management-overview-new/#section-723-qub-nmy "") 和 [业务场景](https://help.aliyun.com/zh/sae/permission-management-overview-new/#section-6fq-ma2-1ur "")。

- 如果您已熟知权限管理相关的功能，可以根据以下内容定位您的问题。

  - [权限策略和示例](https://help.aliyun.com/zh/sae/policies-and-examples-2-0 "")：介绍权限策略的基本概念、SAE支持的权限策略以及权限策略示例。

  - [SAE权限助手](https://help.aliyun.com/zh/sae/sae-permission-assistant-2-0 "")：介绍如何通过SAE权限助手工具生成权限语句，简化自定义策略的设置。

  - [为RAM用户授权](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-user-2-0 "")：介绍如何创建RAM用户并为其授权，按需分配权限。

  - [为RAM角色授权](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-role-2-0 "")：介绍如何创建RAM角色并为其授权，使用安全令牌就能以角色身份访问被授权的资源。

  - [联系人管理](https://help.aliyun.com/zh/sae/contact-management "")：介绍如何为指定的联系人设置权限规则、发送通知等。

  - [操作审批](https://help.aliyun.com/zh/sae/approval-configuration "")：介绍如何为SAE平台的重要功能设定审批流程，对操作权限进行细粒度管控。

  - [服务关联角色](https://help.aliyun.com/zh/sae/service-linked-role-2-0 "")：介绍SAE如何通过服务关联角色来获取其他云资源的访问权限。

## 背景信息

托管在SAE的应用，可能包含多个服务或子系统，这些服务或子系统又可能由团队、成员进行开发与运维。SAE通过账号体系及基于账号体系的一系列权限管理操作，提供企业级的权限管理系统，帮助您对应用、资源和数据进行必要的隔离和权限控制，以保证安全性。

企业A通过阿里云账号（主账号）A购买了SAE服务，最初企业内多名员工共享该账号；随着业务发展，新增了多名员工，共享一个账号无法明确分工且存在信息安全风险。于是企业A通过RAM功能管理权限，实现了分权分账的功能。

![dg_use_ram_before_and_after](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9514742461/p379354.png)

## 业务场景

### 场景一

场景一涉及明确业务分工，了解如何按需为部门员工分配权限（初步了解权限策略）。

为了明确分工，企业A可以通过1个阿里云账号，创建多个RAM用户并为员工授权，实现不同RAM用户有不同资源访问权限的目的。企业A购买资源是为了将自己的应用托管到SAE，因此需先熟悉SAE在RAM中的权限策略和授权配置示例。RAM支持以下策略。

- 系统策略：统一由阿里云创建，您只能使用不能修改，策略的版本更新由阿里云维护。

- 自定义策略：您可以自主创建、更新和删除，策略的版本更新由您自己维护。


同时，某些场景下SAE为了完成自身的某个功能，需要获取其他云服务的访问权限。例如创建应用时要获取VPC等信息，就可以通过SLR获取VPC等产品的访问权限。

具体信息，请参见 [权限策略和示例](https://help.aliyun.com/zh/sae/policies-and-examples-2-0 "") 和 [服务关联角色](https://help.aliyun.com/zh/sae/service-linked-role-2-0 "")。

### 场景二

场景二涉及业务精细化程度加深，了解如何为部门员工配置仅适用于本部门的权限（深入了解权限策略）。

通过对权限策略的学习，企业A认为可以为员工们先设置系统权限，即一般通用的权限，例如SAE资源的读权限。如果系统策略无法满足需求，则可以通过创建自定义策略精细化权限。

配置自定义策略时，SAE权限助手能够简化前期编辑脚本的工作，企业A能够将自动生成的、完整的脚本复制到RAM控制台，创建相应的自定义策略并授权给RAM用户，有效避免直接在RAM控制台操作时出错。

具体信息，请参见 [SAE权限助手](https://help.aliyun.com/zh/sae/sae-permission-assistant-2-0 "")。

### 场景三

场景三涉及为部门员工配置权限（公司内创建RAM用户并授权）。

通过对权限策略的学习，企业A准备创建RAM用户并按需分配权限，并指派给不同员工。

具体信息，请参见 [为RAM用户授权](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-user-2-0 "")。

### 场景四

场景四涉及与合作伙伴共同处理业务（跨公司跨账号创建RAM角色并授权）。

随着业务不断发展，企业A与企业B建立了良好的合作伙伴关系，并希望将部分业务授权给企业B。需求如下。

- 企业A希望能专注于业务系统，仅作为SAE的资源所有者；而将部分业务授权给企业B，例如应用发布、应用管理、自动弹性、一键启停应用和应用监控等服务。

- 企业A希望当企业B的员工加入或离职时，无需做任何权限变更。企业B可以进一步将A的资源访问权限分配给企业B的RAM用户，并可以精细控制其员工或应用对资源的访问和操作权限。

- 企业A希望如果双方合同终止，企业A随时可以撤销对企业B的授权。


具体信息，请参见 [为RAM角色授权](https://help.aliyun.com/zh/sae/grant-permissions-to-a-ram-role-2-0 "")。

### 场景五

场景五涉及严格把控审批环节（公司内严格把控各项环节的操作）。

企业A的阿里云账号A下部署了多个命名空间，包括测试环境、开发环境、预发环境和线上环境等，企业A希望严格把控线上环境的权限，避免出现人员随意操作该环境下的应用，造成线上环境崩溃的情况。企业A可以通过设定审批流程，接收审批通知，对操作权限进行细粒度管控。

具体信息，请参见 [操作审批](https://help.aliyun.com/zh/sae/approval-configuration "") 和 [联系人管理](https://help.aliyun.com/zh/sae/contact-management "")。