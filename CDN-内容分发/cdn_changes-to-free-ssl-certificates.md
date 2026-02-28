### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 关于HTTPS免费证书调整的公告

# 关于HTTPS免费证书调整的公告

更新时间：2024-10-18 05:52:21

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

适用对象

变更内容

政策影响

应对策略

相关文档

如果您目前HTTPS证书为免费证书，受CA/B最新提案的策略变化影响，阿里云CDN控制台的免费证书申请成功率会大幅下降。若您后续有免费证书申请的需求，请您尽快到SSL证书控制台重新申请和部署。

## 适用对象

本公告仅针对使用HTTPS免费证书，或者即将申请免费证书的用户。

## 变更内容

尊敬的阿里云用户：

SSL证书产品公告： [关于域名所有权验证策略调整的通知](https://help.aliyun.com/zh/ssl-certificate/product-overview/notice-on-policy-changes-for-domain-ownership-verification#concept-2080738 "")。

受CA/B最新提案的影响，阿里云SSL证书服务将对域名所有权的验证策略（ **文件验证** 方式）进行调整。

**说明**

CA/B：国际CA/浏览器产业联盟（CA/Browser Forum，简称CA/B）是制定CA国际标准的技术联盟，其发布的规定在数字证书行业内具有权威和普适性。

**生效时间**：2021年09月21日起。

**变更内容**：

- 通配符域名（例如，\*.aliyundoc.com、\*.developer.aliyundoc.com等）不再支持通过文件验证的方式进行域名所有权验证。

届时，您通过SSL证书服务申请通配符证书时，只能使用DNS验证的方式验证域名所有权。关于DNS验证的更多介绍，请参见 [DNS验证方式](https://help.aliyun.com/zh/ssl-certificate/verify-the-ownership-of-a-domain-name#task-2086114 "")。

- 单域名（包含顶级域和子域名，例如，aliyundoc.com、developer.aliyundoc.com等）仍支持通过文件验证的方式进行域名所有权验证，但是使用文件验证时，所有单域名都必须单独完成验证。

届时，如果您使用文件验证方式验证域名所有权，必须分别对顶级域（例如，aliyundoc.com）和相关子域名（例如，developer.aliyundoc.com）进行验证。关于文件验证的更多介绍，请参见 [文件验证方式](https://help.aliyun.com/zh/ssl-certificate/verify-the-ownership-of-a-domain-name#task-2086114 "")。


**相关信息**：

- [关于CDN免费证书及CSR证书功能下线通知](https://help.aliyun.com/noticelist/articleid/1060896054.html)

- [Domain validation policy changes in 2021](https://knowledge.digicert.com/alerts/domain-authentication-changes-in-2021.html)


给您带来不便，敬请谅解。如果您有任何疑问，请提交工单或者通过钉钉售后服务群联系我们。

## 政策影响

| **域名类别** | **政策影响** |
| --- | --- |

|     |     |
| --- | --- |
| **域名类别** | **政策影响** |
| 顶级域名：例如example.com。 | 无影响。 |
| www单域名：例如www.example.com。 | 无影响。 |
| 非www单域名：例如\*.aliyundoc.com。 | 申请免费证书会失败。<br>**说明**<br>阿里云CDN免费证书仅针对单域名可申请，单域名申请通过文件验证进行域名所有权验证时，会获取认证文件，并存储在阿里云CDN边缘节点，以便CA机构可以通过边缘节点获取验证文件，完成免费证书申请。新政策要求非www单域名必须分别对顶级域名（例如，aliyundoc.com）和相关子域名（例如，example.aliyundoc.com，demo.aliyundoc.com）同时进行验证，才能成功申请免费证书。而阿里云CDN控制台不支持非www单域名场景获取顶级域名验证文件功能，因此非www单域名无法验证成功，最终结论为非www单域名申请免费证书会失败。 |

**说明**

阿里云CDN控制台的免费证书申请功能入口也会逐步迁移至SSL证书中心，具体时间另行通知。建议您通过证书中心进行免费证书申请，然后部署在阿里云CDN上。

## 应对策略

**您已经申请过免费证书并部署至阿里云CDN**

阿里云CDN控制台的续签证书逻辑：老证书到期前自动申请一张新证书，然后自动部署在域名上。由于受CA/B最新提案的影响，您之前在阿里云CDN控制台申请的免费证书，自动重新申请的成功率会大幅降低。如果您之前在阿里云CDN控制台申请了免费证书，建议您在老证书到期前，在SSL证书产品重新申请一张新证书并部署到您的网站上。

SSL证书产品中申请免费证书可以采用DNS验证，文件验证等多种方式，申请成功率较高。

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，选择**工具管理** \> **证书服务**。

3. 如果您的 **证书来源** 显示为免费证书。

4. 建议您在2021年09月21日前，通过云盾SSL证书产品重新申请域名的免费证书。具体申请方式，请参见 [申请个人测试证书](https://help.aliyun.com/zh/ssl-certificate/apply-for-a-single-domain-dv-certificate-for-free-trial#task-2436672 "")。





**重要**





申请免费证书时，需要 [域名所有权验证](https://help.aliyun.com/zh/ssl-certificate/verify-the-ownership-of-a-domain-name#task-2086114 "")，在验证时主要注意如下几点。



   - 通配符域名（例如，\*.aliyundoc.com、\*.developer.aliyundoc.com等）不再支持通过文件验证的方式进行域名所有权验证。您通过SSL证书服务申请通配符证书时，只能使用DNS验证的方式验证域名所有权。

   - 单域名（包含顶级域和子域名，例如，aliyundoc.com、example.aliyundoc.com等）仍支持通过文件验证的方式进行域名所有权验证，但是使用文件验证时，所有单域名都必须单独完成验证。如果您使用文件验证方式验证域名所有权，必须分别对顶级域（例如，aliyundoc.com）和相关子域名（例如，example.aliyundoc.com）进行验证。

   - 验证方式，请参见 [域名所有权验证](https://help.aliyun.com/zh/ssl-certificate/verify-the-ownership-of-a-domain-name#task-2086114 "")。


5. 配置HTTPS免费证书至阿里云CDN域名。具体方式，请参见 [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate#task-261642 "")。


**新申请免费证书**

建议您在SSL证书产品申请免费证书： [提交证书申请](https://help.aliyun.com/zh/ssl-certificate/submit-a-certificate-application#concept-wxz-3xn-yfb "")。

如果您仍在阿里云CDN控制台进行免费证书申请，需要关注免费证书申请条件政策前后变化（不再推荐您通过阿里云CDN申请免费证书）：

| **变更前** | **变更后** |
| --- | --- |

|     |     |
| --- | --- |
| **变更前** | **变更后** |
| 当前加速域名需已正确配置CNAME。 | 无变化 |
| 当前加速域名的DNS记录中不能有CAA记录，或者CAA记录包含Digicert.com和digicert.com，不支持泛域名申请。 | 无变化 |
| 免费证书仅能保护一个明细域名（当前加速域名）。 | 无变化 |
| 需授权阿里云代申请免费证书。 | 无变化 |
| 生效之后加速域名的SSL Labs安全等级为A。 | 无变化 |
| 免费证书有效期一年，到期前七天还未自动续签成功，请在证书过期前进行手动更新证书。 | 无变化 |
| 如需申请www域名免费证书，则必须将顶级域名也配置并全量解析到阿里云CDN。<br>**说明**<br>www.aliyundoc.com，aliyundoc.com均需配置到阿里云CDN，并DNS解析全量切到阿里云CDN CNAME。其他子域名无需做此配置。 | - www域名影响：无变化。<br>  <br>- 其他子域名影响：非www域名将无法通过阿里云CDN免费证书工程申请免费证书。 |

## 相关文档

- [云盾SSL证书产品](https://yundun.console.aliyun.com/)。

- [免费证书申请流程](https://help.aliyun.com/zh/ssl-certificate/overview-of-free-certificates-overview-of-free-certificates#concept-2044742 "")。

- [免费证书申请常见问题](https://help.aliyun.com/zh/ssl-certificate/faq-5#task-2046507 "")。

- [阿里云CDN证书配置流程](https://help.aliyun.com/zh/edge-security-acceleration/dcdn/user-guide/enable-http-or-2#task-2345458 "")。

- [证书验证方式](https://help.aliyun.com/zh/ssl-certificate/verify-the-ownership-of-a-domain-name#task-2086114 "")。