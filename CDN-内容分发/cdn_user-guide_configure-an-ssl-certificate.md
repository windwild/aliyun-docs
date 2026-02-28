### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)[HTTPS配置](https://help.aliyun.com/zh/cdn/user-guide/https-for-cdn-or-dcdn/)配置HTTPS证书

# 配置HTTPS证书

更新时间：2025-12-04 21:05:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：HTTPS配置](https://help.aliyun.com/zh/cdn/user-guide/https-for-cdn-or-dcdn/)[下一篇：配置HTTP/2](https://help.aliyun.com/zh/cdn/user-guide/enable-http-or-2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

适用范围

操作步骤

验证HTTPS配置是否生效

关闭HTTPS安全加速

上传自定义证书

计费说明

参考文档

常见问题

相关API

为CDN加速域名配置HTTPS证书，能够加密客户端与CDN节点间的通信链路，防止数据在公网传输中被窃取或篡改，提升业务安全。在阿里云数字证书管理服务（原SSL）中购买的证书支持批量部署至CDN平台，具体操作请参见： [批量配置HTTPS证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate-for-multiple-domain-names "")。

## 适用范围

配置前，需了解以下功能边界和约束，以确保证书能成功部署：

- **购买证书：** 如果您没有证书，可以选择在 [SSL证书管理控制台](https://yundunnext.console.aliyun.com/?p=cas#/certExtend/buy) 申请个人测试证书（原免费证书）或购买正式证书。

- **私钥要求：** 如果您选择上传自定义证书，则上传的证书私钥必须是无密码保护的，请先 [验证私钥文件是否已去除密码保护](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#9b577a1c3bw7a "")。


## **操作步骤**

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **HTTPS配置**。

5. 在 **HTTPS证书** 区域，单击 **修改配置**。

6. 在 **HTTPS设置** 界面，打开 **HTTPS安全加速** 开关，并配置证书相关参数。![证书](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5604718461/p93720.png)

   - 如果您已在 [数字证书管理服务（原SSL）](https://yundunnext.console.aliyun.com/?p=cas#/certExtend/buy) 中购买了证书，请选择 **云盾（SSL）证书中心**，并在 **证书名称** 中选择已购买的证书。



     **说明**





     如果无法选择您购买的证书，请检查已购买证书绑定的域名和加速域名是否相同。

   - 如果您使用的是第三方服务商签发的证书，请选择 **自定义上传（证书+私钥）**，您需要在设置 **证书名称** 后，上传 **证书（公钥）** 和 **私钥**，该证书将在阿里云数字证书管理服务中保存，您可以在 [我的证书](https://yundun.console.aliyun.com/?spm=5176.2020520110.all.12.16df56a1u1IhI6&p=cas#/cas/home) 中查看。

     自定义上传证书对 **证书（公钥）** 和 **私钥** 格式要求严格。如果您出现配置错误或看不懂配置示例，可以参考 [上传自定义证书](https://help.aliyun.com/zh/cdn/user-guide/configure-an-ssl-certificate#c2113b6e3bgvk "") 处理 **证书（公钥）** 和 **私钥**，然后上传。




     | **参数** | **说明** |
     | --- | --- |



     |     |     |
     | --- | --- |
     | **参数** | **说明** |
     | **证书名称** | 为要上传的证书设置一个名称。<br>仅支持使用英文字母、英文句号、数字、下划线（`_`）和短划线（`-`），且不能与已有证书名称重复。 |
     | **证书（公钥）** | 填写步骤一中证书文件内容的PEM编码。 |
     | **私钥** | 填写步骤一中私钥内容的PEM编码。由于私钥信息敏感，上传后不支持在控制台查看或导出，需在本地妥善保管。 |
7. 单击 **确定**，完成配置。


## 验证HTTPS配置是否生效

- 浏览器验证：使用浏览器访问 `https://您的加速域名`。如果地址栏出现安全锁标志，且点击后能看到正确的证书信息，则表示配置成功。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5732326371/p900778.png)

- 命令行验证：执行 `curl -I https://您的加速域名`，如果能正常返回 `200`，则表示HTTPS服务可用。


## 关闭HTTPS安全加速

如果您不再使用HTTPS安全加速功能，可随时在CDN控制台关闭HTTPS安全加速。关闭HTTPS安全加速实时生效，关闭后使用HTTPS方式无法访问资源，且不再保留证书或私钥信息。

再次开启HTTPS安全加速时，需要重新选择需要使用的证书。

## **上传自定义证书**

如果您拥有的是第三方服务商签发或自签名的证书，需要先将证书和私钥处理成CDN支持的格式，然后上传。

- 证书（公钥）

CDN只支持上传PEM格式的证书。其他格式的证书需要参考 [证书格式转换](https://help.aliyun.com/zh/cdn/user-guide/certificate-formats#section-cn2-rql-xdb "") 将其转换成PEM格式。针对不同证书颁发机构的证书，对证书内容的上传有不同的要求：

  - **Root CA机构颁发的证书（一个证书文件）**

    使用文本编辑器即可打开PEM格式的证书文件，将以`-----BEGIN CERTIFICATE-----`开头和以`-----END CERTIFICATE-----`结尾的内容一并上传。















    ```plaintext
    -----BEGIN CERTIFICATE-----
    [证书内容]
    -----END CERTIFICATE-----
    ```

  - **中级机构颁发的证书（多个证书文件）**

    需将服务器证书、所有中间CA证书按顺序拼接成一个完整的证书链文件。文件内容应遵循以下格式：















    ```plaintext
    -----BEGIN CERTIFICATE-----
    [服务器证书内容]
    -----END CERTIFICATE-----
    -----BEGIN CERTIFICATE-----
    [中间CA证书内容]
    -----END CERTIFICATE-----
    ```
- 私钥

私钥的扩展名一般为`.key`或`.pem`。使用文本编辑器即可打开私钥文件。不同内容的私钥上传要求区别如下：

  - **RSA私钥直接上传**

    如果私钥内容以`-----BEGIN RSA PRIVATE KEY-----`开头，`-----END RSA PRIVATE KEY-----`结尾，则直接上传私钥内容。















    ```plaintext
    -----BEGIN RSA PRIVATE KEY-----
    [私钥内容]
    -----END RSA PRIVATE KEY-----
    ```

  - **其他格式私钥先转换格式再上传**

    如果您得到的是以`-----BEGIN PRIVATE KEY-----`开头，以`-----END PRIVATE KEY-----`结尾的私钥，您需要使用OpenSSL工具的转换命令先对私钥进行转换，然后将转换后的私钥内容按照 **直接上传** 的操作处理。其中`old_server_key.pem`为转换前的私钥，`new_server_key.pem`为转换后的私钥。















    ```plaintext
    # 需要转换的私钥
    -----BEGIN PRIVATE KEY-----
    [私钥内容]
    -----END PRIVATE KEY-----
    ```

















    ```plaintext
    # 转换命令
    openssl rsa -in old_server_key.pem -out new_server_key.pem
    ```

## **计费说明**

启用HTTPS安全加速功能会产生额外费用。

- **计费项：** 静态HTTPS请求数。此费用独立于CDN流量费，按账户下所有加速域名产生的静态HTTPS请求总数计费。

- **付费模式：** 支持 **按量后付费** 和购买 [**静态HTTPS请求数资源包**](https://common-buy.aliyun.com/?spm=5176.7933777.J_3537169050.7.2429496eQ1aMgi&commodityCode=dcdnpaybag#/buy)（预付费）两种模式。

- **成本提醒：**

  - CDN下行流量包不可抵扣HTTPS请求产生的费用。

  - 购买的静态HTTPS请求数资源包可被CDN和DCDN共享使用。

## **参考文档**

| **文档** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **文档** | **描述** |
| [配置强制跳转](https://help.aliyun.com/zh/cdn/user-guide/configure-url-redirection "") | 您可以通过配置强制跳转HTTPS功能，将客户端到CDN节点的请求强制重定向为更安全的HTTPS请求。 |
| [配置HSTS](https://help.aliyun.com/zh/cdn/user-guide/configure-hsts "") | 开启HSTS（HTTP Strict Transport Security）功能，您可以强制客户端（例如：浏览器）使用HTTPS与CDN节点创建连接，提高安全性。 |
| [配置OCSP Stapling](https://help.aliyun.com/zh/cdn/user-guide/configure-ocsp-stapling "") | CDN节点预先缓存在线证书验证结果并下发给客户端，无需浏览器直接向CA站点查询证书状态，减少用户验证时间。 |

## **常见问题**

- [私钥文件如何去除密码保护？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#9b577a1c3bw7a "")

- [源站已经配置了HTTPS，CDN上还需要配置HTTPS吗？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-lq1-dyp-bea "")

- [源站的HTTPS证书更新了，CDN上需要同步更新吗？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#section-zjb-jyq-cc4 "")

- [为什么大多数设备能够顺利访问通过HTTPS协议加速的域名，但是一些设备却无法访问？](https://help.aliyun.com/zh/cdn/user-guide/faq-about-https#612fb5afb31yo "")


## 相关API

| **API** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **API** | **描述** |
| [CreateCdnCertificateSigningRequest](https://help.aliyun.com/zh/cdn/api-createcdncertificatesigningrequest#doc-api-Cdn-CreateCdnCertificateSigningRequest "") | 创建CSR文件。 |
| [DescribeDomainCertificateInfo](https://help.aliyun.com/zh/cdn/api-describedomaincertificateinfo#doc-api-Cdn-DescribeDomainCertificateInfo "") | 获取指定加速域名证书信息。 |
| [SetCdnDomainSSLCertificate](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-setcdndomainsslcertificate "") | 设置某域名下证书功能是否启用及更新证书信息。 |
| [SetCdnDomainCSRCertificate](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-setcdndomaincsrcertificate "") | 设置指定域名下的HTTPS证书。 |
| [DescribeCdnDomainByCertificate](https://help.aliyun.com/zh/cdn/api-describecdndomainbycertificate#doc-api-Cdn-DescribeCdnDomainByCertificate "") | 根据证书信息获取加速域名。 |
| [DescribeCdnCertificateDetail](https://help.aliyun.com/zh/cdn/api-describecdncertificatedetail#doc-api-Cdn-DescribeCdnCertificateDetail "") | 查询CDN证书详细信息。 |
| [DescribeCdnCertificateList](https://help.aliyun.com/zh/cdn/api-describecdncertificatelist#doc-api-Cdn-DescribeCdnCertificateList "") | 获取证书列表信息。 |
| [DescribeCertificateInfoByID](https://help.aliyun.com/zh/cdn/api-describecertificateinfobyid#doc-api-Cdn-DescribeCertificateInfoByID "") | 获取指定证书信息。 |
| [DescribeCdnHttpsDomainList](https://help.aliyun.com/zh/cdn/api-describecdnhttpsdomainlist#doc-api-Cdn-DescribeCdnHttpsDomainList "") | 获取用户所有证书信息。 |
| [DescribeUserCertificateExpireCount](https://help.aliyun.com/zh/cdn/api-describeusercertificateexpirecount#doc-api-Cdn-DescribeUserCertificateExpireCount "") | 获取用户证书过期的域名数。 |
| [SetCdnDomainSMCertificate](https://help.aliyun.com/document_detail/398671.html#doc-api-Cdn-SetCdnDomainSMCertificate "") | 设置某域名下国密证书功能是否启用。 |
| [DescribeCdnSMCertificateList](https://help.aliyun.com/document_detail/398681.html#doc-api-Cdn-DescribeCdnSMCertificateList "") | 获取指定加速域名下国密证书列表信息。 |
| [DescribeCdnSMCertificateDetail](https://help.aliyun.com/document_detail/398692.html#doc-api-Cdn-DescribeCdnSMCertificateDetail "") | 获取国密证书的详细信息。 |