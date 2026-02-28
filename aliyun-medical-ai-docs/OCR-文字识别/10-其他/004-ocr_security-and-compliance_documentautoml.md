### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[安全合规](https://help.aliyun.com/zh/ocr/security-and-compliance/)[使用RAM进行访问控制](https://help.aliyun.com/zh/ocr/security-and-compliance/use-ram-for-access-control/)[基于身份的策略](https://help.aliyun.com/zh/ocr/security-and-compliance/identity-based-polici/)文字识别系统权限策略参考

# 文字识别系统权限策略参考

更新时间：2024-10-31 06:14:38

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

什么是系统权限策略

产品系统策略

AliyunDocumentAutomlFullAccess

AliyunDocumentAutomlReadOnlyAccess

授权操作参考

本文描述文字识别支持的所有系统权限策略及其对应的权限描述，供您授权 RAM 身份时参考。

## **什么是系统权限策略**

权限策略是用语法结构描述的一组权限的集合，可以精确地描述被授权的资源集、操作集以及授权条件。阿里云访问控制（RAM）产品提供了两种类型的权限策略：系统策略和自定义策略。系统策略统一由阿里云创建，策略的版本更新由阿里云维护，用户只能使用不能修改。自定义策略由用户管理，策略的版本更新由用户维护。用户可以自主创建、更新和删除自定义策略。在产品迭代过程中，文字识别会向系统策略中添加新的权限，用来支持新的功能和能力。系统策略的更新将会影响所有授予了该策略的 RAM 身份，包括 RAM 用户、RAM 用户组和 RAM 角色。有关 RAM 权限策略的更多信息，请参阅 [权限策略概览](https://help.aliyun.com/zh/ram/policy-overview "")。

**说明**

产品系统策略旨在帮助用户快速入门，仅需简单配置即可通过控制台访问该产品及其依赖产品。虽然系统策略包含的权限同样适用于 OpenAPI 或 CLI 等访问方式，但为了提高安全性，我们推荐您在这些场景下使用自定义策略，按需授予人员及应用特定 API 的访问权限。

系统策略可进一步细分为产品系统策略、服务角色策略和服务关联角色策略三类。部分云产品仅提供三类策略中的一类或两类，请以本文实际展示的策略类型为准。

## **产品系统策略**

### **AliyunDocumentAutomlFullAccess**

您可以将 AliyunDocumentAutomlFullAccess 策略授权给RAM身份。本策略定义了用于文档自学习AliyunDocumentAutomlFullAccess权限策略。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyundocumentautomlfullaccess)

### **AliyunDocumentAutomlReadOnlyAccess**

您可以将 AliyunDocumentAutomlReadOnlyAccess 策略授权给RAM身份。本策略定义了文档自学习读取权限策略。

[查看策略详情](https://help.aliyun.com/zh/ram/developer-reference/aliyundocumentautomlreadonlyaccess)

## **授权操作参考**

RAM 身份默认没有任何权限，需要由阿里云账号管理员为其授权后才能访问阿里云账号下的资源。为保证资源的数据安全，建议您遵循最小授权原则为允许访问云资源的身份授予恰好够用的权限。授权的详细操作请参见：

- [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")

- [为RAM用户组授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-a-ram-user-group "")

- [为RAM角色授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-a-ram-role "")