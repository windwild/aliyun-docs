### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 大模型服务平台百炼系统权限策略参考

# 大模型服务平台百炼系统权限策略参考

更新时间：2025-04-10 05:27:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

什么是系统权限策略

产品系统策略

AliyunBailianDataFullAccess

AliyunBailianDataReadOnlyAccess

AliyunBailianFullAccess

AliyunBailianReadOnlyAccess

AliyunSFMFullAccess

AliyunSFMReadOnlyAccess

服务角色策略

AliyunOpentrekManagerRolePolicy

服务关联角色策略

AliyunServiceRolePolicyForAIMiaoBiAccessingOss

AliyunServiceRolePolicyForAccessOSS

AliyunServiceRolePolicyForDataAnalysisGBIAccessingAdb

AliyunServiceRolePolicyForQuanMiaoAccessingIMS

AliyunServiceRolePolicyForSFMAccessAppFlow

AliyunServiceRolePolicyForSFMAccessCMS

AliyunServiceRolePolicyForSFMAccessCloudAPI

AliyunServiceRolePolicyForSFMAccessEB

AliyunServiceRolePolicyForSFMAccessICE

AliyunServiceRolePolicyForSFMAccessIQS

AliyunServiceRolePolicyForSFMAccessSLS

AliyunServiceRolePolicyForSFMAccessingCIP

AliyunServiceRolePolicyForSFMAccessingMNS

AliyunServiceRolePolicyForSFMModelDeveloper

AliyunServiceRolePolicyForSFMTelemetry

授权操作参考

本文描述大模型服务平台百炼支持的所有系统权限策略及其对应的权限描述，供您授权 RAM 身份时参考。

## **什么是系统权限策略**

权限策略是用语法结构描述的一组权限的集合，可以精确地描述被授权的资源集、操作集以及授权条件。阿里云访问控制（RAM）产品提供了两种类型的权限策略：系统策略和自定义策略。系统策略统一由阿里云创建，策略的版本更新由阿里云维护，用户只能使用不能修改。自定义策略由用户管理，策略的版本更新由用户维护。用户可以自主创建、更新和删除自定义策略。在产品迭代过程中，大模型服务平台百炼会向系统策略中添加新的权限，用来支持新的功能和能力。系统策略的更新将会影响所有授予了该策略的 RAM 身份，包括 RAM 用户、RAM 用户组和 RAM 角色。有关 RAM 权限策略的更多信息，请参阅 [权限策略概览](https://help.aliyun.com/zh/ram/policy-overview "")。

**说明**

产品系统策略旨在帮助用户快速入门，仅需简单配置即可通过控制台访问该产品及其依赖产品。虽然系统策略包含的权限同样适用于 OpenAPI 或 CLI 等访问方式，但为了提高安全性，我们推荐您在这些场景下使用自定义策略，按需授予人员及应用特定 API 的访问权限。

系统策略可进一步细分为产品系统策略、服务角色策略和服务关联角色策略三类。部分云产品仅提供三类策略中的一类或两类，请以本文实际展示的策略类型为准。

## **产品系统策略**

### **AliyunBailianDataFullAccess**

您可以将 AliyunBailianDataFullAccess 策略授权给RAM身份。本策略定义了阿里云百炼数据面（BailianData）权限。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunbailiandatafullaccess)

### **AliyunBailianDataReadOnlyAccess**

您可以将 AliyunBailianDataReadOnlyAccess 策略授权给RAM身份。本策略定义了只读管理阿里云百炼数据面（BailianData），及模型体验基本能力（创建会话、停止生成）的权限。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunbailiandatareadonlyaccess)

### **AliyunBailianFullAccess**

您可以将 AliyunBailianFullAccess 策略授权给RAM身份。本策略定义了 阿里云百炼（Bailian）权限。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunbailianfullaccess)

### **AliyunBailianReadOnlyAccess**

您可以将 AliyunBailianReadOnlyAccess 策略授权给RAM身份。本策略定义了 只读管理阿里云百炼（Bailian）的权限。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunbailianreadonlyaccess)

### **AliyunSFMFullAccess**

您可以将 AliyunSFMFullAccess 策略授权给RAM身份。本策略定义了管理阿里云百炼（SFM）的权限。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunsfmfullaccess)

### **AliyunSFMReadOnlyAccess**

您可以将 AliyunSFMReadOnlyAccess 策略授权给RAM身份。本策略定义了只读管理阿里云百炼（SFM）的权限。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunsfmreadonlyaccess)

## **服务角色策略**

### **AliyunOpentrekManagerRolePolicy**

AliyunOpentrekManagerRolePolicy 是服务角色 AliyunOpentrekManagerRole 专用的授权策略，SFM使用此角色来访问您在其他云产品中的资源。请勿将本策略授权给服务角色之外的RAM身份。如果产品提供精确授权的能力，请严格参考产品提供的帮助文档进行操作。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunopentrekmanagerrolepolicy)

## **服务关联角色策略**

### **AliyunServiceRolePolicyForAIMiaoBiAccessingOss**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForAIMiaoBiAccessingOss 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForAIMiaoBiAccessingOss 是 AliyunServiceRoleForAIMiaoBiAccessingOss 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforaimiaobiaccessingoss)

### **AliyunServiceRolePolicyForAccessOSS**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForAccessOSS 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForAccessOSS 是 AliyunServiceRoleForAccessOSS 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforaccessoss)

### **AliyunServiceRolePolicyForDataAnalysisGBIAccessingAdb**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForDataAnalysisGBIAccessingAdb 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForDataAnalysisGBIAccessingAdb 是 AliyunServiceRoleForDataAnalysisGBIAccessingAdb 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyfordataanalysisgbiaccessingadb)

### **AliyunServiceRolePolicyForQuanMiaoAccessingIMS**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForQuanMiaoAccessingIMS 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForQuanMiaoAccessingIMS 是 AliyunServiceRoleForQuanMiaoAccessingIMS 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforquanmiaoaccessingims)

### **AliyunServiceRolePolicyForSFMAccessAppFlow**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessAppFlow 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessAppFlow 是 AliyunServiceRoleForSFMAccessAppFlow 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccessappflow)

### **AliyunServiceRolePolicyForSFMAccessCMS**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessCMS 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessCMS 是 AliyunServiceRoleForSFMAccessCMS 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccesscms)

### **AliyunServiceRolePolicyForSFMAccessCloudAPI**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessCloudAPI 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessCloudAPI 是 AliyunServiceRoleForSFMAccessCloudAPI 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccesscloudapi)

### **AliyunServiceRolePolicyForSFMAccessEB**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessEB 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessEB 是 AliyunServiceRoleForSFMAccessEB 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccesseb)

### **AliyunServiceRolePolicyForSFMAccessICE**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessICE 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessICE 是 AliyunServiceRoleForSFMAccessICE 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccessice)

### **AliyunServiceRolePolicyForSFMAccessIQS**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessIQS 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessIQS 是 AliyunServiceRoleForSFMAccessIQS 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccessiqs)

### **AliyunServiceRolePolicyForSFMAccessSLS**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessSLS 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessSLS 是 AliyunServiceRoleForSFMAccessSLS 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccesssls)

### **AliyunServiceRolePolicyForSFMAccessingCIP**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessingCIP 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessingCIP 是 AliyunServiceRoleForSFMAccessingCIP 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccessingcip)

### **AliyunServiceRolePolicyForSFMAccessingMNS**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMAccessingMNS 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMAccessingMNS 是 AliyunServiceRoleForSFMAccessingMNS 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmaccessingmns)

### **AliyunServiceRolePolicyForSFMModelDeveloper**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMModelDeveloper 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMModelDeveloper 是 AliyunServiceRoleForSFMModelDeveloper 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmmodeldeveloper)

### **AliyunServiceRolePolicyForSFMTelemetry**

大模型服务平台百炼使用服务关联角色 AliyunServiceRoleForSFMTelemetry 来访问您在其他云产品中的资源。AliyunServiceRolePolicyForSFMTelemetry 是 AliyunServiceRoleForSFMTelemetry 专用的授权策略。本策略由大模型服务平台百炼定义和使用，您不能修改或删除，请勿将其授权给服务关联角色之外的RAM身份。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyunservicerolepolicyforsfmtelemetry)

## **授权操作参考**

RAM 身份默认没有任何权限，需要由阿里云账号管理员为其授权后才能访问阿里云账号下的资源。为保证资源的数据安全，建议您遵循最小授权原则为允许访问云资源的身份授予恰好够用的权限。授权的详细操作请参见：

- [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")

- [为RAM用户组授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-a-ram-user-group "")

- [为RAM角色授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-a-ram-role "")