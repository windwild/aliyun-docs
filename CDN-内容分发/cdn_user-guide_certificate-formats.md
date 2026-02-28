### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/) [操作指南](https://help.aliyun.com/zh/cdn/user-guide/) [域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/) [HTTPS配置](https://help.aliyun.com/zh/cdn/user-guide/https-for-cdn-or-dcdn/) [相关参考](https://help.aliyun.com/zh/cdn/user-guide/cdn-https-references/) 证书格式说明

# 证书格式说明

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：相关参考](https://help.aliyun.com/zh/cdn/user-guide/cdn-https-references/)[下一篇：CDN默认支持的TLS加密算法](https://help.aliyun.com/zh/cdn/user-guide/default-tls-encryption-algorithms)

该文章对您有帮助吗？

反馈

CDN只支持上传PEM格式的证书和私钥，针对不同证书颁发机构的证书，对证书内容的上传有不同的要求。

## Root CA机构颁发的证书

Root CA机构可以颁发多个证书，这些证书可以用于Apache、IIS、Nginx和Tomcat等Web服务器。阿里云CDN使用的证书格式与Nginx兼容，包含后缀为`.crt`（证书）和后缀为`.key`（私钥）的这两个文件。

进入Nginx文件夹，使用文本编辑器打开`.crt`文件，您可以看到PEM格式的证书内容，如下图所示。

图 1\. PEM格式证书![PEM格式证书](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5397150161/p214015.png)

**PEM格式证书**

- 以“-----BEGIN CERTIFICATE-----”开头，以“-----END CERTIFICATE-----”结尾。

- 每行64个字符，最后一行可以不足64个字符。


**证书上传要求**

- 请将以“-----BEGIN CERTIFICATE-----”开头和以“-----END CERTIFICATE-----”结尾的内容一并上传。

- 每行64个字符，最后一行可以不足64个字符。


## 中级机构颁发的证书

配置HTTPS时，您需要将服务器证书与中间证书拼接成一份完整的证书后再上传。拼接后的证书如下图所示。

图 2\. 拼接后的PEM格式证书![拼接后的PEM格式证书](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7167150161/p214007.png)

**证书链格式**

中级机构颁发的证书链格式如下：

-----BEGIN CERTIFICATE-----

-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----

-----END CERTIFICATE-----

**拼接规则**

- 通过文本编辑器打开所有\*.PEM格式的证书文件。

- 将服务器证书放在第一位，中间证书放在第二位，证书之间不能有空行。


## RSA私钥格式要求

私钥扩展名一般为`.pem`或`.key`，在文本编辑器中打开私钥文件，您可以看到与下图格式相似的私钥内容。

图 3\. RSA格式私钥![RSA格式私钥](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1131250161/p214176.png)

**私钥PEM格式**

- 以“-----BEGIN RSA PRIVATE KEY-----”开头，“-----END RSA PRIVATE KEY-----”结尾。

- 每行64个字符，最后一行可以不足64个字符。


**私钥上传要求**

上传RSA私钥之前，您需要通过`openssl genrsa -out privateKey.pem 2048`在本地先生成私钥，`privateKey.pem`为您的私钥文件。

- 请将以“-----BEGIN RSA PRIVATE KEY-----”开头和以“-----END RSA PRIVATE KEY-----”结尾的内容一并上传。

- 每行64个字符，最后一行可以不足64个字符。


如果您得到的是以“-----BEGIN PRIVATE KEY-----”开头，以“-----END PRIVATE KEY-----”结尾的私钥，您需要使用OpenSSL工具执行以下命令进行转换，然后将`new_server_key.pem`的内容与证书一起上传。

```plaintext
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

## 证书格式转换方式

HTTPS配置只支持PEM格式的证书，其他格式的证书需要转换成PEM格式，建议通过OpenSSL工具进行转换。下面是几种比较流行的证书格式转换为PEM格式的方法。

**说明**

- CRT文件可能是PEM或DER编码格式，转换前请确认您的证书格式。

- PEM一般为文本格式，以 “-----BEGIN \*\*\*-----”开头，以 “-----END \*\*\*-----”结尾，中间的内容是Base64编码。PEM格式的私钥后缀一般为`.key`。


- ### **DER转换为PEM**




DER格式一般出现在Java平台中。



  - 证书转换：


    ```plaintext
    openssl x509 -inform der -in certificate.cer -out certificate.pem
    ```

  - 私钥转换：


    ```plaintext
    openssl rsa -inform DER -outform pem -in privatekey.der -out privatekey.pem
    ```


- ### **P7B转换为PEM**




P7B格式一般出现在Windows Server和Tomcat中。



  - 证书转换：


    ```plaintext
    openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
    ```


    获取`outcertificate.cer`中的-----BEGIN CERTIFICATE-----和-----END CERTIFICATE-----内容作为证书进行上传。

  - 私钥转换：

    P7B证书无私钥，您只需在CDN控制台填写证书部分，私钥无需填写。


- ### **PFX转换为PEM**




PFX格式一般出现在Windows Server中。



  - 证书转换：


    ```plaintext
    openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
    ```

  - 私钥转换：


    ```plaintext
    openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
    ```