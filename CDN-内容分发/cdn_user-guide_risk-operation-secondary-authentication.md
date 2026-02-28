### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)风险操作二次身份验证

# 风险操作二次身份验证

更新时间：2025-01-26 03:16:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：停止加速服务](https://help.aliyun.com/zh/cdn/user-guide/disable-or-remove-an-accelerated-domain-name)[下一篇：域名管理FAQ](https://help.aliyun.com/zh/cdn/user-guide/faq-about-domain-name-management)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

阿里云账号（主账号）安全核身说明

RAM用户（子账号）安全核身说明

在使用阿里云CDN产品过程中，停用和删除域名都属于高风险操作，建议您开启二次身份验证功能，控制潜在风险。

## **概述**

风控是控制台数据请求流程的必要环节，用于识别用户的风险操作，并进行二次验证（以下简称核身）。

核身通过弹窗采集用户的多因素验证信息（如手机验证码、邮箱验证码、VMFA 码、U2F 等），进行二次验证。风控验证成功则放行操作，否则阻止。

## 阿里云账号（主账号） **安全核身说明**

使用阿里云账号（主账号）执行CDN产品的停用或删除域名操作时，会触发二次身份验证，请完成验证。首次验证通过后，有15分钟的免验证时间。

## RAM用户（子账号） **安全核身说明**

阿里云账号（主账号）或RAM管理员可以通过修改RAM用户安全设置，提升账号安全性。此设置为全局设置，适用于所有RAM用户。详细信息请参见 [管理RAM用户安全设置](https://help.aliyun.com/zh/ram/getting-started/manage-security-settings-of-ram-users-1 "")。

1. 开启多因素认证，MFA设备默认开启，手机和邮箱需要主动开启。

1. 使用阿里云账号或RAM管理员登录[RAM控制台](https://ram.console.aliyun.com/)。

2. 在左侧导航栏选择 **身份管理** > **设置**。

3. 在 **安全设置** 页签的 **用户安全设置** 区域，单击 **修改用户安全设置**。

4. 在 **修改用户安全设置** 面板， **多因素认证手段** 中勾选 **手机** 和 **邮箱** 选项。![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8846738861/p689316.png)

5. 单击 **确定**。
2. 给RAM用户绑定核身方式。

1. 在左侧导航栏选择 **身份管理** > **用户**。

2. 在 **用户** 页面，单击需要设置的RAM用户名。

3. 选择 **认证管理** > **安全信息管理**，编辑安全手机和邮箱。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4294301271/p820190.png)
3. RAM用户的二次身份效果验证。完成以上配置后，使用RAM用户执行阿里云CDN产品的停用或者删除域名操作都会触发二次身份验证，请按照提示完成验证操作。首次验证通过以后，将会有15分钟的免验证时间。