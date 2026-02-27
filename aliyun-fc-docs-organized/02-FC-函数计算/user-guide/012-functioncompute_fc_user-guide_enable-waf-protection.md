### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[函数调用与触发器](https://help.aliyun.com/zh/functioncompute/fc/user-guide/function-calls-and-triggers/)[管理域名](https://help.aliyun.com/zh/functioncompute/fc/user-guide/manage-domain-names-1/)开启Web应用防火墙

# 开启Web应用防火墙

更新时间：2025-09-28 05:58:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

使用限制

计费说明

前提条件

操作步骤

后续操作

阿里云Web应用防火墙（简称WAF 3.0）支持对函数或者应用的业务流量进行恶意特征识别，对流量进行清洗和过滤后，将正常和安全的流量回源至后端函数，避免函数被恶意侵入。本文介绍如何通过控制台为函数计算的自定义域名开启Web应用防火墙功能。

## 背景信息

函数计算与WAF 3.0深度集成后，支持自定义域名级别的防护，为您的网站或App业务提供一站式安全防护。

## 使用限制

函数计算自定义域名的Web应用防火墙功能目前仅支持华东1（杭州）、华东2（上海）、华北2（北京）、华南1（深圳）和华北3（张家口）地域。

## 计费说明

开启自定义域名的Web应用防火墙后，函数计算本身不计费，但WAF 3.0将根据使用情况计费。更多信息，请参见 [WAF 3.0计费概述](https://help.aliyun.com/zh/waf/web-application-firewall-3-0/overview-7#task-2238382 "")。

## 前提条件

已开通WAF 3.0服务。具体操作，请参见 [购买WAF 3.0包年包月实例](https://help.aliyun.com/zh/waf/web-application-firewall-3-0/purchase-a-subscription-waf-3-0-instance#task-2152697 "") 或 [开通WAF 3.0按量付费实例](https://help.aliyun.com/zh/waf/web-application-firewall-3-0/purchase-a-pay-as-you-go-waf-3-0-instance#task-2152697 "")。

## 操作步骤

您可以在创建自定义域名的同时开启Web应用防火墙，也可以为已有自定义域名开启Web应用防火墙。

创建自定义域名时开启Web应用防火墙

为已有自定义域名开启Web应用防火墙

1. 登录[函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，选择**函数管理** \> **域名管理**。

2. 在顶部菜单栏，选择地域，然后在 **域名管理** 页面，单击 **添加自定义域名**。

3. 在 **添加自定义域名** 页面，填写 **域名**，配置项 **Web 应用防火墙** 选择 **启用**，然后单击 **创建**。

关于各配置项的说明，请参见 [配置自定义域名](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-custom-domain-names#section-4yb-ztm-q9v "")。


1. 登录[函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，选择**函数管理** \> **域名管理**。

2. 在 **域名管理** 页面，单击目标自定义域名右侧 **操作** 列的 **编辑**。

3. 在 **编辑自定义域名** 页面，配置项 **Web 应用防火墙** 选择 **启用**，然后单击 **保存**。


## 后续操作

开启Web应用防火墙后，网站访问流量将经过WAF并受到WAF的防护。WAF包含多种防护检测模块，帮助网站防御不同类型的安全威胁。其中规则防护引擎和CC安全防护模块默认开启，分别用于防御常见的Web应用攻击（例如SQL注入、XSS跨站或WebShell上传等）和CC攻击。其他防护模块需要您手动开启并配置具体防护规则。更多信息，请参见 [防护配置概述](https://help.aliyun.com/zh/waf/web-application-firewall-3-0/user-guide/protection-configuration-overview#concept-tzp-g2m-42b "")。