### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/) [函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/) [开发参考](https://help.aliyun.com/zh/functioncompute/fc/developer-reference/) 签名机制

# 签名机制

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：服务接入地址](https://help.aliyun.com/zh/functioncompute/fc/developer-reference/fc-endpoints)[下一篇：API参考（函数）](https://help.aliyun.com/zh/functioncompute/fc/developer-reference/api-reference-1/)

该文章对您有帮助吗？

反馈

函数计算产品提供的API采用ROA签名风格，本文介绍V3版本的签名机制，更多信息，请参见 [V3版本请求体&签名机制](https://help.aliyun.com/zh/sdk/product-overview/v3-request-structure-and-signature "")。

## 签名机制

采用AK/SK方式进行签名与认证。对于每一次HTTP或HTTPS协议请求，阿里云API网关将依据请求参数信息重新计算签名，通过对比该签名与请求中提供的签名是否一致，从而验证请求者的身份，以确保传输数据的完整性与安全性。

**重要**

**请求及返回结果都使用UTF-8字符集进行编码。**

### 步骤一：构造规范化请求

构造规范化请求（CanonicalRequest）的伪代码如下：

```java
CanonicalRequest =
  HTTPRequestMethod + '\n' +    // http请求方法，全大写
  CanonicalURI + '\n' +         // 规范化URI
  CanonicalQueryString + '\n' + // 规范化查询字符串
  CanonicalHeaders + '\n' +     // 规范化消息头
  SignedHeaders + '\n' +        // 已签名消息头
  HashedRequestPayload		// 请求body的hash值
```

- #### HTTPRequestMethod（请求方法）


即大写的HTTP方法名，如GET、POST。

- #### CanonicalURI（规范化URI）


URL的资源路径部分经过编码之后的结果。资源路径部分指URL中host与查询字符串之间的部分，包含host之后的`/`但不包含查询字符串前的`?`。用户发起请求时的URI应使用规范化URI，编码方式使用UTF-8字符集按照 [RFC3986](http://tools.ietf.org/html/rfc3986) 的规则对URI中的每一部分（即被`/`分割开的字符串）进行编码：


  - 字符A~Z、a~z、0~9以及字符`-`、`_`、`.`、`~`不编码。

  - 其他字符编码成`%`加字符对应ASCII码的16进制。示例：半角双引号（`"`）对应`%22`。需要注意的是，部分特殊字符需要特殊处理，具体如下：


    |     |     |
    | --- | --- |
    | 编码前 | 编码后 |
    | 空格（ ） | `%20` |
    | 星号（`*`） | `%2A` |
    | `%7E` | 波浪号（`~`） |


    如果您使用的是Java标准库中的`java.net.URLEncoder`，可以先用标准库中`encode`编码，随后将编码后的字符中加号（`+`）替换为`%20`、星号（`*`）替换为`%2A`、`%7E`替换为波浪号（`~`），即可得到上述规则描述的编码字符串。


**重要**

RPC风格API使用正斜杠(`/`)作为CanonicalURI，

ROA风格API该参数为OpenAPI元数据中`path`的值，例如`/api/v1/clusters`。

- #### CanonicalQueryString（规范化查询字符串）


在 [OpenAPI元数据](https://help.aliyun.com/zh/sdk/product-overview/openapi-metadata#32c6c74961o1j "") 中，如果API的请求参数信息包含了`"in":"query"`时，需要将这些请求参数按照如下构造方法拼接起来：


1. 将请求参数按照参数名称的字符顺序升序排列。

2. 使用UTF-8字符集按照 [RFC3986](http://tools.ietf.org/html/rfc3986) 的规则对每个参数的参数名称和参数值分别进行URI编码，具体规则与上一节中的CanonicalURI编码规则相同。

3. 使用等号（`=`）连接编码后的请求参数名称和参数值，对于没有值的参数使用空字符串。

4. 多个请求参数之间使用与号（`&`）连接。


**重要**

  - 当请求参数类型是array、object时，需要将参数平铺为一个映射结构（map）。例如`{"ImageId":"win2019_1809_x64_dtc_zh-cn_40G_alibase_20230811.vhd","RegionId":"cn-shanghai","Tag":[{"tag1":"value1","tag2":"value2"}]}`平铺后为`{"ImageId":"win2019_1809_x64_dtc_zh-cn_40G_alibase_20230811.vhd","RegionId":"cn-shanghai","Tag.1.tag1":"value1","Tag.1.tag2":"value2"}`。

  - 当请求的查询字符串为空时，使用空字符串作为规范化查询字符串。


示例值：

```json
ImageId=win2019_1809_x64_dtc_zh-cn_40G_alibase_20230811.vhd&RegionId=cn-shanghai
```

- #### HashedRequestPayload


使用哈希函数对RequestPayload进行转换得到HashedRequestPayload，并将 [RequestHeader](https://help.aliyun.com/zh/sdk/product-overview/v3-request-structure-and-signature#p-nvi-zbo-752 "") 中`x-acs-content-sha256`的值修改为HashedRequestPayload的值。伪代码如下：


```java
HashedRequestPayload = HexEncode(Hash(RequestPayload))
```



  - RequestPayload的值有以下两种情况：

    - 在 [OpenAPI元数据](https://help.aliyun.com/zh/sdk/product-overview/openapi-metadata#32c6c74961o1j "") 中，如果API的请求参数信息包含了`"in": "body"`或`"in": "formData"`时，需通过请求body传递参数，RequestPayload的值为请求body对应的JSON字符串。







      **重要**

      - 当请求参数信息包含`"in": "formData"`时，需要将这类参数按照固定格式拼接为一个字符串，拼接格式为：`key1=value1&key2=value2&key3=value3`。若请求参数类型是array、object时，需要将参数平铺为一个映射结构（map）。例如`{"key":["value1","value2"]}`平铺后为`{"key.1":"value1","key.2":"value2"}`。同时需要在RequestHeader中添加`content-type=application/x-www-form-urlencoded`。

      - 当请求参数信息包含`"in": "body"`时，需要在RequestHeader中添加content-type，content-type的值与请求内容类型有关。例如：

        - 请求内容类型为JSON数据时，content-type的值为`application/json`。

        - 请求内容类型为二进制文件流时，content-type的值为`application/octet-stream`。

    - 若没有请求body，RequestPayload的值固定为一个空字符串。
  - Hash表示消息摘要函数，目前仅支持SHA256算法。

  - HexEncode表示以小写的十六进制的形式返回摘要的编码函数（即Base16编码）。


当请求body为空时的示例值：

```json
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

- #### CanonicalHeaders（规范化请求头）


将 [RequestHeader](https://help.aliyun.com/zh/sdk/product-overview/v3-request-structure-and-signature#p-nvi-zbo-752 "") 中的参数按照如下构造方法拼接起来：


1. 过滤出RequestHeader中包含以`x-acs-`为前缀、`host`、`content-type`的参数。

2. 将参数的名称转换为小写，并按照字符顺序升序排列。

3. 将参数的值去除首尾空格。

4. 将参数名称和参数值以英文冒号（`:`）连接，并在尾部添加换行符（`\n`），组成一个规范化消息头（CanonicalHeaderEntry）。

5. 将多个规范化消息头（CanonicalHeaderEntry）拼接成一个字符串。


**说明**

除Authorization外的所有RequestHeader，只要符合要求都必须被加入签名。

伪代码如下：

```java
CanonicalHeaderEntry = Lowercase(HeaderName) + ':' + Trim(HeaderValue) + '\n'

CanonicalHeaders =
    CanonicalHeaderEntry0 + CanonicalHeaderEntry1 + ... + CanonicalHeaderEntryN
```

示例值：

```json
host:ecs.cn-shanghai.aliyuncs.com
x-acs-action:RunInstances
x-acs-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
x-acs-date:2023-10-26T10:22:32Z
x-acs-signature-nonce:3156853299f313e23d1673dc12e1703d
x-acs-version:2014-05-26
```

- #### SignedHeaders（已签名消息头列表）


用于说明此次请求中参与签名的公共请求头信息，与CanonicalHeaders中的参数名称一一对应。其构造方法如下：


  - 将CanonicalHeaders中包含的请求头的名称转为小写。

  - 按首字母升序排列并以英文分号（`;`）分隔。


伪代码如下：

```java
SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ... + Lowercase(HeaderNameN)
```

示例值：

```json
host;x-acs-action;x-acs-content-sha256;x-acs-date;x-acs-signature-nonce;x-acs-version
```

### 步骤二：构造待签名字符串

按照以下伪代码构造待签名字符串（stringToSign）：

```java
StringToSign =
    SignatureAlgorithm + '\n' +
    HashedCanonicalRequest
```

- SignatureAlgorithm

签名协议目前仅支持ACS3-HMAC-SHA256算法。

- HashedCanonicalRequest

规范化请求摘要串，计算方法伪代码如下：


```java
HashedCanonicalRequest = HexEncode(Hash(CanonicalRequest))
```


  - Hash表示消息摘要函数，目前仅支持SHA256算法。

  - HexEncode表示以小写的十六进制的形式返回摘要的编码函数（即Base16编码）。

示例值：

```json
ACS3-HMAC-SHA256
7ea06492da5221eba5297e897ce16e55f964061054b7695beedaac1145b1e259
```

### 步骤三：计算签名

按照以下伪代码计算签名值（Signature）。

```java
Signature = HexEncode(SignatureMethod(Secret, StringToSign))
```

- StringToSign：步骤二中构造的待签名字符串，UTF-8编码。

- SignatureMethod：使用HMAC-SHA256作为签名算法。

- Secret：AccessKey Secret。

- HexEncode：以小写的十六进制的形式返回摘要的编码函数（即Base16编码）。


示例值：

```json
06563a9e1b43f5dfe96b81484da74bceab24a1d853912eee15083a6f0f3283c0
```

### 步骤四：将签名添加到请求中

计算完签名后，构造Authorization请求头，格式为：`Authorization:<SignatureAlgorithm> Credential=<AccessKeyId>,SignedHeaders=<SignedHeaders>,Signature=<Signature>`。

示例值：

```json
ACS3-HMAC-SHA256 Credential=YourAccessKeyId,SignedHeaders=host;x-acs-action;x-acs-content-sha256;x-acs-date;x-acs-signature-nonce;x-acs-version,Signature=06563a9e1b43f5dfe96b81484da74bceab24a1d853912eee15083a6f0f3283c0
```