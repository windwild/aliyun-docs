### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[日志数据采集（Log）](https://help.aliyun.com/zh/sls/sls-log-collection/)[云产品日志采集](https://help.aliyun.com/zh/sls/collection-of-alibaba-cloud-service-logs/)[WAF 3.0日志](https://help.aliyun.com/zh/sls/waf-3-0-logs/)[日志设置](https://help.aliyun.com/zh/sls/log-settings-1/)日志容量升级

# 日志容量升级

更新时间：2024-11-27 01:33:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

何时进行日志容量升级

升级日志容量

相关文档

Web应用防火墙（Web Application Firewall，简称WAF）开通日志服务后，请实时查看日志容量，如果您的日志容量已接近或已达到饱和状态，为了避免日志数据无法写入日志库，请及时升级日志容量。

## **何时进行日志容量升级**

除了避免日志存储容量不足新日志无法写入情况外，您还可以通过升级日志容量满足以下方面的长期业务需求：

- 提高可见性和监控能力：

升级日志容量可以记录更多的请求和事件，有助于更全面地监控流量和潜在威胁。详细的日志数据使安全团队能够更好地了解攻击行为和模式，从而采取更有效的防御措施。

- 合规性需求：

部分行业和法规要求企业保留详细的访问和安全日志，以满足合规性标准。增加日志容量可以确保企业能够满足这些法规要求，避免潜在的法律和财务风险。

- 长期趋势分析：

通过存储更多历史数据，企业可以进行长期趋势分析，识别出潜在的安全威胁和流量模式变化。这有助于制定更有效的安全策略和资源配置。


## 升级日志容量

**重要**

- 仅针对包年包月高级版、企业版、旗舰版的实例，支持查看和升级日志存储容量。按量付费实例按实际用量结算费用，并由日志服务统一出账，因此没有容量限制，无需单独设置日志容量。

- 当您的日志存储使用量达到80%时，系统将通过短信和邮件通知您，提示日志存储空间接近上限。为防止新的日志数据因存储空间不足而无法写入，造成数据丢失，请您收到通知后及时升级日志存储容量。


1. 登录[Web应用防火墙3.0控制台](https://yundunnext.console.aliyun.com/?p=wafnew)。在顶部菜单栏，选择WAF实例的资源组和地域（ **中国内地**、 **非中国内地**）

2. 在左侧导航栏，选择**检测与响应** \> **日志服务**

3. 管理日志存储空间：

   - 查看日志存储空间：在 **日志服务** 页面右上方，可查看已开通及当前已使用的日志存储容量及比例。

   - 升级日志存储容量：单击 **日志服务** 页面右上角的 **升级容量**，选择更大的 **日志存储容量** 规格，并完成购买。

## **相关文档**

如果您当前的日志容量超过需求，导致额外的费用支出，您可以通过降低日志服务容量配置来减少成本。具体操作，请参见 [升级与降配](https://help.aliyun.com/zh/waf/web-application-firewall-3-0/upgrade-or-downgrade-a-waf-instance#section-xau-1f1-eoi "")。