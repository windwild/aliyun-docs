### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[日志审计（新版）](https://help.aliyun.com/zh/sls/new-log-audit-service/)查询分析

# 查询分析

更新时间：2024-08-08 04:24:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：日志审计创建Logtail配置采集Systemd Journal日志](https://help.aliyun.com/zh/sls/log-audit-create-logtail-configuration-to-collect-systemd-journal-logs)[下一篇：Tetragon运行时日志字段说明](https://help.aliyun.com/zh/sls/tetragon-runtime-log-field-descriptions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

云产品

前提条件

功能入口

日志类型

运行时

前提条件

功能入口

日志类型

使用新版日志审计服务启动云产品采集后，您可以在 [关联Logstore](https://help.aliyun.com/zh/sls/cloud-product-configuration-considerations "") 查询分析日志。本文主要为您介绍云产品以及运行时的日志类型。

## 云产品

### **前提条件**

已开启对应云产品的采集功能。具体操作，请参见 [开启新版日志审计](https://help.aliyun.com/zh/sls/enable-new-log-audit "")。

### **功能入口**

1. 登录 [日志服务控制台](https://sls.console.aliyun.com/)，在 **日志应用** 区域，选择**审计与安全** \> **新版日志审计服务**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5445013271/p831749.png)

2. 单击目标Project。在 **查询分析** 页面，单击**查询分析** \> **云产品**。在 **云产品** 页签中，单击目标云产品，执行查询分析操作。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5445013271/p831508.png)


### **日志类型**

| 云产品分类 | 产品名称 | 日志类型 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 云产品分类 | 产品名称 | 日志类型 |
| 云原生 | [日志服务](https://help.aliyun.com/zh/sls/getting-started "") | [审计日志](https://help.aliyun.com/zh/sls/log-fields-46#section-was-qk1-s70 "") |
| [错误日志](https://help.aliyun.com/zh/sls/log-fields-46#section-iqj-mvz-zlh "") |
| [监控指标](https://help.aliyun.com/zh/sls/log-fields-46#section-z98-9d4-eu4 "") |
| [详细日志](https://help.aliyun.com/zh/sls/log-types#section-gnn-3pr-m2b "") |
| [任务运行日志](https://help.aliyun.com/zh/sls/log-types#entry-e5x-mpu-icd "") |
| 存储 | 对象存储（OSS） | [访问明细日志](https://help.aliyun.com/zh/sls/log-fields-17#section-uzb-eoc-28t "") |
| [计量日志](https://help.aliyun.com/zh/sls/log-fields-17#section-zgb-f6q-qhc "") |
| 网络 | 应用型负载均衡ALB | [访问日志](https://help.aliyun.com/zh/slb/application-load-balancer/user-guide/access-logs#section-nqb-bds-tr1 "") |
| 传统型负载均衡CLB | [访问日志](https://help.aliyun.com/zh/slb/classic-load-balancer/user-guide/configure-access-logs#5cf162d21fmai "") |
| 专有网络VPC | [流日志](https://help.aliyun.com/zh/vpc/vpc-flow-logs#e2397ac5650f0 "") |
| 企业基础服务 | 云解析DNS | [内网DNS日志](https://help.aliyun.com/zh/dns/intranet-dns-parsing-log-transfer-to-sls#3974b66755myi "") |
| 安全 | Web 应用防火墙 2.0 | [访问日志](https://help.aliyun.com/zh/waf/web-application-firewall-2-0/user-guide/log-fields-supported-by-waf "") |
| Web 应用防火墙 3.0（预付费版）、Web 应用防火墙 3.0（按量付费版） | [访问日志](https://help.aliyun.com/zh/waf/web-application-firewall-3-0/user-guide/fields-in-logs "") |
| 云安全中心、云安全中心（按量付费版） | [Web访问日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#7bc64b023c9kg "") |
| [DNS解析日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#7bc6722e3ccm2 "") |
| [网络会话日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#23356f503c3v4 "") |
| [本地DNS日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#1b2779303c3xd "") |
| [登录流水日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#eb0cf9d03clie "") |
| [网络连接日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#b90b64603cajt "") |
| [进程启动日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#6b8dc4413cy9w "") |
| [暴力破解日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#47003e803c25r "") |
| [账号快照日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#01a96e503cbnk "") |
| [客户端事件日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#b9967ccf22ivr "") |
| [进程快照日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#24bb68e03ce37 "") |
| [网络快照日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#24d464903csmj "") |
| [DNS请求日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#532a81603cnvl "") |
| 安全日志（ [漏洞日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#86e9c9003c0xj "")、 [基线日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#6ba726303ceg8 "")、 [安全告警日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#f7bfb2203c21n "")、 [云平台配置检查日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#ca19aea03c889 "")、 [网络防御日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#44c6b3f066npm "")、 [应用防护日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#8e54f1dff2ynf "")、 [恶意文件检测日志](https://help.aliyun.com/zh/security-center/user-guide/log-category-and-field-description-v2-0#63133f2fe5psy "")） |
| DDoS原生防护 | [访问日志](https://help.aliyun.com/zh/anti-ddos/anti-ddos-origin/user-guide/fields-in-logs "") |
| DDoS高防（中国内地）、DDoS高防（非中国内地） | [访问日志](https://help.aliyun.com/zh/anti-ddos/anti-ddos-pro-and-premium/user-guide/fields-included-in-full-logs "") |
| 云防火墙、云防火墙（按量付费版） | [防火墙日志](https://help.aliyun.com/zh/cloud-firewall/cloudfirewall/user-guide/log-fields#6980535754nvz "") |

## 运行时

### **前提条件**

已开启对应运行时的采集功能。具体操作，请参见 [配置容器运行时](https://help.aliyun.com/zh/sls/configure-runtime-log-collection/ "")。

### **功能入口**

1. 登录 [日志服务控制台](https://sls.console.aliyun.com/)，在 **日志应用** 区域，选择**审计与安全** \> **新版日志审计服务**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5445013271/p831749.png)

2. 单击目标Project。在 **查询分析** 页面，单击**查询分析** \> **运行时**。在 **运行时** 页签中，单击目标应用，执行查询分析操作。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5445013271/p831508.png)


### **日志类型**

| **应用** | **日志类型** |
| --- | --- |

|     |     |
| --- | --- |
| **应用** | **日志类型** |
| Tetragon | [运行时日志](https://help.aliyun.com/zh/sls/tetragon-runtime-log-field-descriptions "") |
| Falco | [运行时日志](https://help.aliyun.com/zh/sls/falco-runtime-security-log-field-descriptions "") |
| Systemd Journal | [Systemd Journal日志](https://help.aliyun.com/zh/sls/systemd-journal-log-field-description "") |