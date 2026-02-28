### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[HTTPS配置](https://help.aliyun.com/zh/cdn/user-guide/https-for-cdn-or-dcdn/)配置TLS版本与加密套件

# 配置TLS版本与加密套件

更新时间：2024-04-01 07:52:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

操作步骤

当客户端对CDN节点发起请求时，节点响应并启动TLS握手，使用设置的TLS版本以确保通信安全。若客户端不支持该版本，连接将无法建立。您可按需调整TLS版本可平衡老旧浏览器兼容性与安全性：较低TLS版本扩大支持范围，但安全强度减弱；较高TLS版本则增强安全，但可能限制旧版浏览器访问。

## 背景信息

TLS（Transport Layer Security）即安全传输层协议，在两个通信应用程序之间提供保密性和数据完整性，最典型的应用就是HTTPS。HTTPS即HTTP over TLS，就是更安全的HTTP，运行在HTTP层之下，TCP层之上，为HTTP层提供数据加解密服务。

| **协议** | **说明** | **支持的主流浏览器** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **协议** | **说明** | **支持的主流浏览器** |
| TLSv1.0 | RFC2246，1999年发布，基于SSLv3.0，该版本易受各种攻击（如BEAST和POODLE），除此之外，支持较弱加密，对当今网络连接的安全已失去应有的保护效力。不符合PCI DSS合规判定标准。 | - IE6+<br>  <br>- Chrome 1+<br>  <br>- Firefox 2+ |
| TLSv1.1 | RFC4346，2006年发布，修复TLSv1.0若干漏洞。 | - IE 11+<br>  <br>- Chrome 22+<br>  <br>- Firefox 24+<br>  <br>- Safri 7+ |
| TLSv1.2 | RFC5246，2008年发布，目前广泛使用的版本。 | - IE 11+<br>  <br>- Chrome 30+<br>  <br>- Firefox 27+<br>  <br>- Safri 7+ |
| TLSv1.3 | RFC8446，2018年发布，最新的TLS版本，支持0-RTT模式（更快），只支持完全前向安全性密钥交换算法（更安全）。 | - Chrome 70+<br>  <br>- Firefox 63+ |

## 操作步骤

执行操作前，请您确保已成功配置HTTPS证书，操作方法请参见 [配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate#task-261642 "")。

**说明**

默认开启TLSv1.0、TLSv1.1、TLSv1.2和TLSv1.3版本。

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **HTTPS配置**。

5. 在 **TLS加密套件与协议版本配置** 区域，根据需要选择加密套件和开启对应的TLS版本。





![TLS版本控制](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9962368961/p47114.png)



支持如下加密套件，请根据需求选择：



   - **全部加密算法套件(默认)**：安全性较低，兼容性较高，支持的加密算法请见[CDN默认支持的TLS加密算法](https://help.aliyun.com/zh/cdn/user-guide/default-tls-encryption-algorithms "")。

   - **强加密算法套件**：安全性较高，兼容性较低，支持的加密算法：

     - TLS\_AES\_256\_GCM\_SHA384

     - TLS\_AES\_128\_GCM\_SHA256

     - TLS\_CHACHA20\_POLY1305\_SHA256

     - ECDHE-ECDSA-CHACHA20-POLY1305

     - ECDHE-RSA-CHACHA20-POLY1305

     - ECDHE-ECDSA-AES128-GCM-SHA256

     - ECDHE-RSA-AES128-GCM-SHA256

     - ECDHE-ECDSA-AES128-CCM8

     - ECDHE-ECDSA-AES128-CCM

     - ECDHE-ECDSA-AES256-GCM-SHA384

     - ECDHE-RSA-AES256-GCM-SHA384

     - ECDHE-ECDSA-AES256-CCM8

     - ECDHE-ECDSA-AES256-CCM

     - ECDHE-ECDSA-ARIA256-GCM-SHA384

     - ECDHE-ARIA256-GCM-SHA384

     - ECDHE-ECDSA-ARIA128-GCM-SHA256

     - ECDHE-ARIA128-GCM-SHA256
   - **自定义加密算法套件**：请根据需要选择加密套件。


TLS协议版本说明请参见 [背景信息](https://help.aliyun.com/zh/cdn/user-guide/configure-tls-version-control#table-mx5-6ra-z6g "")。