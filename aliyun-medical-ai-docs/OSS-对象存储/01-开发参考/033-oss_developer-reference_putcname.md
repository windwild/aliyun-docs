### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于Bucket操作](https://help.aliyun.com/zh/oss/developer-reference/bucket-operations/)[自定义域名（CNAME）](https://help.aliyun.com/zh/oss/developer-reference/cname/)PutCname

# 调用PutCname接口为某个存储空间Bucket绑定自定义域名

更新时间：2025-05-06 05:23:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

权限说明

请求语法

请求头

请求元素

响应头

示例

SDK

命令行工具ossutil

错误码

调用PutCname接口为某个存储空间（Bucket）绑定自定义域名。

## **权限说明**

阿里云账号默认拥有全部权限。阿里云账号下的RAM用户或RAM角色默认没有任何权限，需要阿里云账号或账号管理员通过 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/ "") 或 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 授予操作权限。

| **API** | **Action** | **说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **API** | **Action** | **说明** |
| PutCname | oss:PutCname | 为Bucket绑定自定义域名。 |
| yundun-cert:DescribeSSLCertificatePrivateKey | 为Bucket绑定自定义域名时，如果绑定证书，则需要这三个操作的权限。 |
| yundun-cert:DescribeSSLCertificatePublicKeyDetail |
| yundun-cert:CreateSSLCertificate |

## 请求语法

```plaintext
POST /?cname&comp=add HTTP/1.1
Host: BucketName.oss-cn-hangzhou.aliyuncs.com
Content-Type: application/xml
Content-Length: 186
Date: GMT Date
Authorization: SignatureValue
<BucketCnameConfiguration>
  <Cname>
    <Domain>example.com</Domain>
  </Cname>
</BucketCnameConfiguration>
```

## 请求头

此接口仅包含公共请求头。更多信息，请参见 [公共请求头（Common Request Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-eq1-b2y-wdb "")。

## 请求元素

| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例值** | **描述** |
| BucketCnameConfiguration | 容器 | 是 | 不涉及 | Cname配置的容器。<br>父节点：无<br>子节点：Cname |
| Cname | 容器 | 是 | 不涉及 | Cname信息的容器。<br>父节点：BucketCnameConfiguration<br>子节点：Domain |
| Domain | 字符串 | 是 | example.com | 自定义域名。<br>父节点：Cname<br>子节点：无 |
| CertificateConfiguration | 容器 | 否 | 不涉及 | 证书配置的容器。<br>父节点：Cname<br>子节点：CertId、Certificate、PrivateKey、PreviousCertId、Force和DeleteCertificate |
| CertId | 字符串 | 否 | 493\*\*\*\*-cn-hangzhou | 证书ID。<br>父节点：CertificateConfiguration<br>子节点：无 |
| Certificate | 字符串 | 否 | -----BEGIN CERTIFICATE----- MIIDhDCCAmwCCQCFs8ixARsyrDANBgkqhkiG9w0BAQsFADCBgzELMAkGA1UEBhMC \*\*\*\* -----END CERTIFICATE----- | 证书公钥。<br>父节点：CertificateConfiguration<br>子节点：无 |
| PrivateKey | 字符串 | 否 | -----BEGIN CERTIFICATE----- MIIDhDCCAmwCCQCFs8ixARsyrDANBgkqhkiG9w0BAQsFADCBgzELMAkGA1UEBhMC \*\*\*\* -----END CERTIFICATE----- | 证书私钥。<br>父节点：CertificateConfiguration<br>子节点：无 |
| PreviousCertId | 字符串 | 否 | 493\*\*\*\*-cn-hangzhou | 当前证书ID。如果Force值不为true，OSS Server会检查该值与当前证书ID是否匹配，不匹配则报错。<br>**重要**<br>绑定证书时，如果不填写PreviousCertId，需将Force置为true。<br>父节点：CertificateConfiguration<br>子节点：无 |
| Force | 字符串 | 否 | true | 是否强制覆盖证书。取值如下：<br>- true：强制覆盖证书。<br>  <br>- false：不覆盖证书。<br>  <br>父节点：CertificateConfiguration<br>子节点：无 |
| DeleteCertificate | 字符串 | 否 | true | 是否删除证书。取值如下：<br>- true：删除证书。<br>  <br>- false：不删除证书。<br>  <br>父节点：CertificateConfiguration<br>子节点：无 |

## 响应头

此接口仅涉及公共响应头。更多信息，请参见 [公共响应头（Common Response Headers）](https://help.aliyun.com/zh/oss/developer-reference/common-http-headers#section-hcd-m2y-wdb "")。

## 示例

- 请求示例

  - 绑定域名















    ```plaintext
    POST /?cname&comp=add HTTP/1.1
    Host: oss-example.oss-cn-hangzhou.aliyuncs.com
    Content-Type: application/xml
    Content-Length: 186
    Date: Thu, 24 Sep 2015 15:39:12 GMT
    Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=host,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
    <BucketCnameConfiguration>
      <Cname>
        <Domain>example.com</Domain>
      </Cname>
    </BucketCnameConfiguration>
    ```

  - 绑定证书















    ```plaintext
    POST /?cname&comp=add HTTP/1.1
    Host: oss-example.oss-cn-hangzhou.aliyuncs.com
    Content-Type: application/xml
    Content-Length: 186
    Date: Thu, 24 Sep 2015 15:39:12 GMT
    Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=host,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
    <BucketCnameConfiguration>
      <Cname>
        <Domain>example.com</Domain>
        <CertificateConfiguration>
          <CertId>493****-cn-hangzhou</CertId>
          <Certificate>-----BEGIN CERTIFICATE----- MIIDhDCCAmwCCQCFs8ixARsyrDANBgkqhkiG9w0BAQsFADCBgzELMAkGA1UEBhMC **** -----END CERTIFICATE-----</Certificate>
          <PrivateKey>-----BEGIN CERTIFICATE----- MIIDhDCCAmwCCQCFs8ixARsyrDANBgkqhkiG9w0BAQsFADCBgzELMAkGA1UEBhMC **** -----END CERTIFICATE-----</PrivateKey>
          <PreviousCertId>493****-cn-hangzhou</PreviousCertId>
          <Force>true</Force>
        </CertificateConfiguration>
      </Cname>
    </BucketCnameConfiguration>
    ```

  - 解绑证书

    如果您不希望该域名继续使用该证书，可以执行解绑证书的操作。















    ```plaintext
    POST /?cname&comp=add HTTP/1.1
    Host: oss-example.oss-cn-hangzhou.aliyuncs.com
    Content-Type: application/xml
    Content-Length: 186
    Date: Thu, 24 Sep 2015 15:39:12 GMT
    Authorization: OSS4-HMAC-SHA256 Credential=LTAI********************/20250417/cn-hangzhou/oss/aliyun_v4_request,AdditionalHeaders=host,Signature=a7c3554c729d71929e0b84489addee6b2e8d5cb48595adfc51868c299c0c218e
    <BucketCnameConfiguration>
      <Cname>
        <Domain>example.com</Domain>
          <CertificateConfiguration>
          <DeleteCertificate>True</DeleteCertificate>
        </CertificateConfiguration>
      </Cname>
    </BucketCnameConfiguration>
    ```
- 返回示例















```plaintext
content-length: 0
x-oss-console-auth: success
server: AliyunOSS
x-oss-server-time: 980
connection: keep-alive
x-oss-request-id: 5C1B138A109F4E405B2D
date: Wed, 15 Sep 2021 03:33:37 GMT
```


## SDK

本接口对应的各语言SDK如下：

- [Java](https://help.aliyun.com/zh/oss/developer-reference/map-custom-domain-names-14 "")

- [Python V2](https://help.aliyun.com/zh/oss/developer-reference/bind-custom-domain-using-oss-sdk-for-python-v2 "")

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/v2-map-custom-domain-names "")

- [Node.js](https://help.aliyun.com/zh/oss/developer-reference/use-custom-domain-names "")

- [PHP V2](https://help.aliyun.com/zh/oss/developer-reference/php-v2-map-custom-domain-names "")


## **命令行工具ossutil**

PutCname接口所对应的ossutil命令，请参见 [put-cname](https://help.aliyun.com/zh/oss/developer-reference/put-cname "")。

## 错误码

| **错误码** | **HTTP状态码** | **描述** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误码** | **HTTP状态码** | **描述** |
| InvalidArgument | 400 | Cname格式错误，您可以在返回XML中查看具体错误字段和原因。 |
| NeedVerifyDomainOwnership | 403 | 未验证域名所有权。<br>验证域名所有权的步骤说明如下：<br>1. 调用 [CreateCnameToken](https://help.aliyun.com/zh/oss/developer-reference/createcnametoken#reference-2210351 "") 接口创建域名所有权验证所需的CnameToken。<br>   <br>   <br>   <br>   **说明**<br>   <br>   <br>   <br>   <br>   <br>   CnameToken默认在创建完成后72小时内过期。如果在CnameToken过期时间内重复创建CnameToken，则返回已存在的CnameToken。<br>   <br>2. 在您的域名服务商处添加TXT记录。<br>   <br>   例如，您需要为自定义域名`example.com`添加TXT记录。添加记录时，记录类型选择TXT、主机记录需填写 `_dnsauth.example`、记录值填写 [步骤1](https://help.aliyun.com/zh/oss/developer-reference/putcname#li-yw4-iem-x80 "") 返回的CnameToken，其他参数保留默认配置。具体步骤，请参见 [手动添加Cname记录](https://help.aliyun.com/zh/oss/manage-a-domain-map-custom-domain-names#section-6de-13t-9cr "")。<br>   <br>   <br>   <br>   **说明**<br>   <br>   <br>   <br>   <br>   <br>   添加的TXT记录需等待几分钟后生效。<br>   <br>3. 调用PutCname接口绑定自定义域名。 |
| CnameDenied | 403 | 域名已被占用。 |
| CnameIsForbidden | 403 | 该域名为OSS内部保留域名，无法绑定。 |
| CnameIsRisk | 403 | 该域名为存在较高风险，无法绑定。 |
| NoSuchCnameInRecord | 404 | 域名未备案。关于备案域名的具体步骤，请参见 [什么是阿里云域名服务](https://help.aliyun.com/zh/dws/product-overview/what-is-domains#concept-t42-dlv-12b "")。 |
| CnameAlreadyExists | 409 | 返回此错误的可能原因如下：<br>- 该域名已绑定至当前账号下的另一个Bucket。<br>  <br>  问题现象：返回错误信息中的CnameType为CNAME\_OSS。<br>  <br>- 该域名是图片处理域名。<br>  <br>  问题现象：返回错误信息中的CnameType为CNAME\_IMG。<br>  <br>针对以上问题，您需要解除域名绑定。具体步骤，请参见 [解除域名绑定](https://help.aliyun.com/zh/oss/user-guide/http-status-code-409#section-p5a-h8b-3mh "")。 |