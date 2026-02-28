### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[访问域名与网络连接](https://help.aliyun.com/zh/oss/user-guide/access-domain-name-and-network-connection/)通过Bucket域名访问OSS

# 通过Bucket域名访问OSS

更新时间：2025-12-24 20:48:12

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：访问域名与网络连接概述](https://help.aliyun.com/zh/oss/user-guide/access-and-network-overview)[下一篇：通过自定义域名访问OSS](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

核心概念

域名类型

外网访问域名

内网访问域名

传输加速域名

CNAME域名

协议支持

HTTP/HTTPS协议

IP协议

相关文档

OSS为每个存储空间（Bucket）分配一系列默认访问域名，支持根据不同业务需求和网络环境（公网、内网、传输加速网络）灵活访问OSS资源。

## **核心概念**

标准的OSS访问地址由多个层级组合构成。准确理解以下四个核心概念，对于正确访问OSS至关重要：

| **概念** | **说明** | **示例** | **用途** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **概念** | **说明** | **示例** | **用途** |
| **Region ID** | **通用地域标识** | `cn-hangzhou` | 用于SDK、ossutil进行V4签名等场景 |
| **专用Region ID** | **OSS专用地域标识** | `oss-cn-hangzhou` | 用于 **构成Endpoint**、API入参、返回参数等场景 |
| **Endpoint** | **服务访问地址** | `oss-cn-hangzhou.aliyuncs.com` | 在SDK、ossutil中配置，用于建立与OSS服务的 **网络连接** 等场景 |
| **Bucket域名** | **具体Bucket的访问地址** | `bucket-name.oss-cn-hangzhou.aliyuncs.com` | 用于 **浏览器直接访问**、生成签名URL或托管静态网站、自定义域名 CNAME 解析等场景。 |

这四个概念存在层级关系： **Region ID** 表示一个地理位置，OSS为其分配对应的 **专用Region ID**，专用RegionID与域名后缀组合构成 **Endpoint**（服务访问地址）。访问具体Bucket时，使用Bucket名称与Endpoint组合形成的 **Bucket域名**（资源访问地址）。

## **域名类型**

OSS根据网络环境和性能需求提供不同类型的访问域名。

### **外网访问域名**

专为互联网访问设计，适用于Web应用、移动客户端、跨地域访问等场景。

#### **域名格式**

- **Endpoint**：`oss-[RegionID].aliyuncs.com`

- **Bucket域名**：`[BucketName].oss-[RegionID].aliyuncs.com`


#### **访问示例**

文件URL

ossutil

SDK

以下示例演示通过控制台获取私有Bucket的文件签名URL，更多获取签名URL的方式请参见 [使用预签名URL下载或预览文件](https://help.aliyun.com/zh/oss/user-guide/how-to-obtain-the-url-of-a-single-object-or-the-urls-of-multiple-objects "")。

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket。

2. 单击目标访问文件的 **文件名** 或操作列的 **详情**。

3. **域名** 选择 **外网域名**，单击 **复制文件URL**。

4. 在浏览器中访问URL。


通过OSS Bucket域名访问HTML、图片等文件时，浏览器会强制下载而非在线预览。如需实现文件预览功能，请 [通过自定义域名访问OSS](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names "")。

以下示例演示使用命令行工具ossutil 2.0下载文件。使用前需要 [安装并配置ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "")，工具默认使用外网访问Endpoint，也可通过`-e`参数显式指定外网访问Endpoint。

```bash
ossutil cp oss://example-bucket/dest.jpg dest.jpg -e oss-cn-hangzhou.aliyuncs.com
```

以下展示常见语言的SDK集成示例，更多语言的集成示例请参见[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)中对应语言的初始化方法。

Java SDK V2

Java SDK V1

Python SDK V2

Python SDK V1

Go SDK V2

Go SDK V1

SDK初始化客户端时默认使用外网访问域名，只需填写地域（Region）ID即可完成配置，无需额外指定Endpoint。完整的初始化代码示例请参见 [OSS Java SDK V2（预览版）](https://help.aliyun.com/zh/oss/developer-reference/oss-sdk-for-java-2-0/ "")。

初始化OSS客户端实例时指定外网访问域名，完整的初始化代码请参见 [OSS Java SDK V1](https://help.aliyun.com/zh/oss/developer-reference/oss-java-sdk/ "")。

```java
// 以华东1（杭州）的外网访问Endpoint为例
String endpoint = "oss-cn-hangzhou.aliyuncs.com";
// 初始化OSS客户端
OSS ossClient = OSSClientBuilder.create()
        .credentialsProvider(provider)
        .clientConfiguration(clientBuilderConfiguration)
        .region("cn-hangzhou")
        .endpoint(endpoint)
        .build();
```

SDK初始化客户端时默认使用外网访问域名，只需填写地域（Region）ID即可完成配置，无需额外指定Endpoint。完整的初始化代码示例请参见 [OSS Python SDK V2](https://help.aliyun.com/zh/oss/developer-reference/2-0-manual-preview-version/ "")。

初始化OSS客户端实例时指定外网访问域名，完整的初始化代码请参见 [初始化（Python SDK V1）](https://help.aliyun.com/zh/oss/initialization-2 "")。

```python
# 以华东1（杭州）的外网访问Endpoint为例
endpoint = "https://oss-cn-hangzhou.aliyuncs.com"
# 初始化OSS客户端实例
bucket = oss2.Bucket(auth, endpoint, "example-bucket", region="cn-hangzhou")
```

SDK初始化客户端时默认使用外网访问域名，只需填写地域（Region）ID即可完成配置，无需额外指定Endpoint。完整的初始化代码示例请参见 [OSS Go SDK V2](https://help.aliyun.com/zh/oss/developer-reference/manual-for-go-sdk-v2/ "")。

初始化OSS客户端实例时指定外网访问域名，完整的初始化代码请参见 [配置客户端（Go SDK V1）](https://help.aliyun.com/zh/oss/initialization-9 "")。

```go
// 创建OSS客户端实例
client, _ := oss.New(
        "oss-cn-hangzhou.aliyuncs.com",	// 以华东1（杭州）的外网访问Endpoint为例
        "",
        "",
        oss.SetCredentialsProvider(&provider),
        oss.AuthVersion(oss.AuthV4),
        oss.Region("cn-hangzhou"),
)
```

### **内网访问域名**

专为阿里云内网环境设计，适用于同地域的ECS实例访问OSS等场景。通过内网访问可避免产生外网流量费用，同时获得更稳定的网络连接和更低的访问延迟。

#### **域名格式**

- **Endpoint**：`oss-[RegionID]-internal.aliyuncs.com`

- **Bucket域名**：`[BucketName].oss-[RegionID]-internal.aliyuncs.com`


#### **使用建议**

- **DNS配置优化**

使用内网Endpoint时，强烈建议配置阿里云的云上私网DNS地址（`100.100.2.136`和`100.100.2.138`），确保获取正确的VIP地址，避免因DNS解析问题导致OSS访问异常。

- **VIP网段路由配置完整性**

OSS为每个Region内网VIP网段划分了固定地址段，系统会在指定VIP网段内动态切换IP地址。本地设备和数据中心通过内网访问OSS时，路由配置必须涵盖完整的VIP网段，否则可能因网络路由不完整导致连接中断。各地域的内网VIP网段信息请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#ec304ac5f79f1 "")。



**重要**





请确保路由配置涵盖完整的VIP网段，避免因配置不完整导致网络连通性问题。若因VIP网段配置缺失影响OSS服务可用性，相关损失需由配置方承担。

- **安全组规则配置**

使用ECS实例通过内网访问OSS时，安全组规则不能禁止访问任何一个VIP网段，确保网络连通性。


#### **访问示例**

ossutil

SDK

以下示例演示在同地域的ECS中使用命令行工具ossutil 2.0下载文件。使用前需要 [安装并配置ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "")，可在配置时使用内网访问Endpoint，也可在下载时通过`-e`参数指定内网访问Endpoint。

```bash
ossutil cp oss://example-bucket/dest.jpg dest.jpg -e oss-cn-hangzhou-internal.aliyuncs.com
```

以下展示常见语言的SDK集成示例，更多语言的集成示例请参见[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)中对应语言的初始化方法。

Java SDK V2

Java SDK V1

Python SDK V2

Python SDK V1

Go SDK V2

Go SDK V1

初始化OSS客户端实例时通过指定Endpoint或`useInternalEndpoint(true)`设置使用内网访问域名，完整的初始化代码请参见 [OSS Java SDK V2（预览版）](https://help.aliyun.com/zh/oss/developer-reference/oss-sdk-for-java-2-0/ "")。

- **方式一：指定内网访问Endpoint**















```java
// 以华东1（杭州）的内网访问Endpoint为例
String endpoint = "oss-cn-hangzhou-internal.aliyuncs.com";
// 初始化OSS客户端
OSSClient client = OSSClient.newBuilder()
          .credentialsProvider(provider)
          .region("cn-hangzhou")
          .endpoint(endpoint)
          .build();
```

- **方式二：通过**`useInternalEndpoint(true)` **设置**















```java
// 初始化OSS客户端
OSSClient client = OSSClient.newBuilder()
          .credentialsProvider(provider)
          .region("cn-hangzhou")
          .useInternalEndpoint(true)
          .build();
```


初始化OSS客户端实例时指定内网访问域名，完整的初始化代码请参见 [OSS Java SDK V1](https://help.aliyun.com/zh/oss/developer-reference/oss-java-sdk/ "")。

```java
// 以华东1（杭州）的内网访问Endpoint为例
String endpoint = "oss-cn-hangzhou-internal.aliyuncs.com";
// 初始化OSS客户端
OSS ossClient = OSSClientBuilder.create()
        .credentialsProvider(provider)
        .clientConfiguration(clientBuilderConfiguration)
        .region("cn-hangzhou")
        .endpoint(endpoint)
        .build();
```

初始化OSS客户端实例时通过指定Endpoint或`use_internal_endpoint = True`设置使用内网访问域名，完整的初始化代码请参见 [OSS Python SDK V2](https://help.aliyun.com/zh/oss/developer-reference/2-0-manual-preview-version/ "")。

- **方式一：指定内网访问Endpoint**















```python
# 以华东1（杭州）的内网访问Endpoint为例
config.endpoint = "https://oss-cn-hangzhou-internal.aliyuncs.com"
# 初始化OSS客户端
client = oss.Client(config)
```

- **方式二：通过**`use_internal_endpoint = True` **设置**















```python
config.use_internal_endpoint = True
# 初始化OSS客户端
client = oss.Client(config)
```


初始化OSS客户端实例时指定内网访问域名，完整的初始化代码请参见 [初始化（Python SDK V1）](https://help.aliyun.com/zh/oss/initialization-2 "")。

```python
# 以华东1（杭州）的内网访问Endpoint为例
endpoint = "oss-cn-hangzhou-internal.aliyuncs.com"
# 初始化OSS客户端实例
bucket = oss.Bucket(auth, endpoint, bucket, region="cn-hangzhou")
```

初始化OSS客户端实例时通过指定Endpoint或`WithUseInternalEndpoint(true)`设置使用内网访问域名，完整的初始化代码请参见 [OSS Go SDK V2](https://help.aliyun.com/zh/oss/developer-reference/manual-for-go-sdk-v2/ "")。

- **方式一：指定内网访问Endpoint**















```go
// 配置OSS客户端，设置凭证提供者和服务地域
config := oss.LoadDefaultConfig().
          WithCredentialsProvider(credentials.NewEnvironmentVariableCredentialsProvider()).
          WithRegion("cn-hangzhou").
          WithEndpoint("oss-cn-hangzhou-internal.aliyuncs.com") // 以华东1（杭州）的内网访问Endpoint为例

// 初始化OSS客户端实例
client := oss.NewClient(config)
```

- **方式二：通过**`WithUseInternalEndpoint(true)` **设置**















```go
// 配置OSS客户端，设置凭证提供者和服务地域
config := oss.LoadDefaultConfig().
          WithCredentialsProvider(credentials.NewEnvironmentVariableCredentialsProvider()).
          WithRegion("cn-hangzhou").
          WithUseInternalEndpoint(true)

// 初始化OSS客户端实例
client := oss.NewClient(config)
```


初始化OSS客户端实例时指定内网访问域名，完整的初始化代码请参见 [配置客户端（Go SDK V1）](https://help.aliyun.com/zh/oss/initialization-9 "")。

```go
// 创建OSS客户端实例
client, _ := oss.New(
        "oss-cn-hangzhou-internal.aliyuncs.com", // 以华东1（杭州）的内网访问Endpoint为例
        "",
        "",
        oss.SetCredentialsProvider(&provider),
        oss.AuthVersion(oss.AuthV4),
        oss.Region("cn-hangzhou"),
)
```

### **传输加速域名**

启用 [通过传输加速访问OSS](https://help.aliyun.com/zh/oss/user-guide/transfer-acceleration#task-1813962 "") 功能后可使用的专用域名，通过全球加速节点优化数据传输路径，适用于跨地域、跨国际的高速上传/下载场景，显著改善远距离访问的网络质量。

#### **域名格式**

- **Endpoint**：`oss-accelerate.aliyuncs.com`

- **Bucket域名**：`[BucketName].oss-accelerate.aliyuncs.com`


#### **访问示例**

ossutil

SDK

以下示例演示在杭州地域的ECS中使用命令行工具ossutil 2.0下载跨国地域的文件。使用前需要 [安装并配置ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "")，可在配置时使用传输加速Endpoint，也可在下载时通过`-e`参数指定传输加速Endpoint。

```bash
ossutil cp oss://example-bucket/dest.jpg dest.jpg -e oss-accelerate.aliyuncs.com
```

以下展示常见语言的SDK集成示例，更多语言的集成示例请参见[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)中对应语言的初始化方法。

Java SDK V2

Java SDK V1

Python SDK V2

Python SDK V1

Go SDK V2

Go SDK V1

初始化OSS客户端实例时通过指定Endpoint或`useAccelerateEndpoint(true)`设置使用传输加速域名，完整的初始化代码请参见 [OSS Java SDK V2（预览版）](https://help.aliyun.com/zh/oss/developer-reference/oss-sdk-for-java-2-0/ "")。

- **方式一：指定传输加速Endpoint**















```java
String endpoint = "oss-accelerate.aliyuncs.com";
// 初始化OSS客户端
OSSClient client = OSSClient.newBuilder()
          .credentialsProvider(provider)
          .region("cn-hangzhou")
          .endpoint(endpoint)
          .build();
```

- **方式二：通过**`useAccelerateEndpoint(true)` **设置**















```java
// 初始化OSS客户端
OSSClient client = OSSClient.newBuilder()
          .credentialsProvider(provider)
          .region("cn-hangzhou")
          .useAccelerateEndpoint(true)
          .build();
```


初始化OSS客户端实例时指定传输加速域名，完整的初始化代码请参见 [OSS Java SDK V1](https://help.aliyun.com/zh/oss/developer-reference/oss-java-sdk/ "")。

```java
String endpoint = "oss-accelerate.aliyuncs.com";
// 初始化OSS客户端
OSS ossClient = OSSClientBuilder.create()
        .credentialsProvider(provider)
        .clientConfiguration(clientBuilderConfiguration)
        .region("cn-hangzhou")
        .endpoint(endpoint)
        .build();
```

初始化OSS客户端实例时通过指定Endpoint或`use_accelerate_endpoint = True`设置使用传输加速域名，完整的初始化代码请参见 [OSS Python SDK V2](https://help.aliyun.com/zh/oss/developer-reference/2-0-manual-preview-version/ "")。

- **方式一：指定传输加速Endpoint**















```python
config.endpoint = "oss-accelerate.aliyuncs.com"
# 初始化OSS客户端
client = oss.Client(config)
```

- **方式二：通过**`use_accelerate_endpoint = True` **设置**















```python
config.use_accelerate_endpoint = True
# 初始化OSS客户端
client = oss.Client(config)
```


初始化OSS客户端实例时指定传输加速域名，完整的初始化代码请参见 [初始化（Python SDK V1）](https://help.aliyun.com/zh/oss/initialization-2 "")。

```python
endpoint = "oss-accelerate.aliyuncs.com"
# 初始化OSS客户端实例
bucket = oss.Bucket(auth, endpoint, bucket, region="cn-hangzhou")
```

初始化OSS客户端实例时通过指定Endpoint或`WithUseAccelerateEndpoint(true)`设置使用传输加速域名，完整的初始化代码请参见 [OSS Go SDK V2](https://help.aliyun.com/zh/oss/developer-reference/manual-for-go-sdk-v2/ "")。

- **方式一：指定传输加速Endpoint**















```go
// 配置OSS客户端，设置凭证提供者和服务地域
config := oss.LoadDefaultConfig().
          WithCredentialsProvider(credentials.NewEnvironmentVariableCredentialsProvider()).
          WithRegion("cn-hangzhou").
          WithEndpoint("oss-accelerate.aliyuncs.com")

// 初始化OSS客户端实例
client := oss.NewClient(config)
```

- **方式二：通过**`WithUseAccelerateEndpoint(true)` **设置**















```go
// 配置OSS客户端，设置凭证提供者和服务地域
config := oss.LoadDefaultConfig().
          WithCredentialsProvider(credentials.NewEnvironmentVariableCredentialsProvider()).
          WithRegion("cn-hangzhou").
          WithUseAccelerateEndpoint(true)

// 初始化OSS客户端实例
client := oss.NewClient(config)
```


初始化OSS客户端实例时指定传输加速域名，完整的初始化代码请参见 [配置客户端（Go SDK V1）](https://help.aliyun.com/zh/oss/initialization-9 "")。

```go
// 创建OSS客户端实例
client, _ := oss.New(
        "oss-accelerate.aliyuncs.com",
        "",
        "",
        oss.SetCredentialsProvider(&provider),
        oss.AuthVersion(oss.AuthV4),
        oss.Region("cn-hangzhou"),
)
```

### **CNAME域名**

OSS 为 Bucket 生成的专用解析域名，专门用于自定义域名绑定，不可直接访问。当需要 [通过自定义域名访问OSS](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names "") 时，通过将自定义域名 CNAME 解析到该专用域名，即可实现域名绑定，适用于网站图片、脚本等静态资源的托管场景。

#### **使用须知**

- **仅用于 DNS 解析**：CNAME 专用域名仅用于自定义域名的 DNS 解析配置，不支持直接访问

- **通过自定义域名访问**：完成域名绑定后，可通过自定义域名访问 OSS 资源

- **地域支持**：目前支持华东 1（杭州）、华东 2（上海）、华北 1（青岛）、新加坡地域


#### **域名格式**

OSS 会为 Bucket 分配地域内的 CNAME 域名，不同 Bucket 可能分配到不同的域名。

- **Bucket 域名**：`[BucketName].[RegionId].[CnameDomain]`（如 `example-***.cn-hangzhou.taihang***.cn`）


## **协议支持**

### **HTTP/HTTPS协议**

所有地域的Endpoint和Bucket域名均支持HTTP和HTTPS两种协议访问。为确保数据传输安全性，强烈建议在生产环境中使用HTTPS协议。

### **IP协议**

所有地域均支持IPv4访问，部分地域额外支持IPv4和IPv6双栈访问Endpoint，允许IPv6网络环境下的客户端直连OSS资源。对于支持IPv6的Endpoint，客户端无需特殊配置，在纯IPv6或双栈网络环境中，DNS会自动解析并优先使用IPv6地址建立连接。经典网络环境下的ECS实例不支持通过IPv4协议或IPv6协议访问OSS资源。

**如何验证Endpoint的IPv6支持？**

通过`dig AAAA`命令验证Endpoint是否支持IPv6访问。

```bash
dig AAAA cn-hangzhou.oss.aliyuncs.com
```

如果Endpoint支持IPv6，命令返回结果的`ANSWER SECTION`部分会显示AAAA记录，表示该域名已配置IPv6地址。

```shell
cn-hangzhou.oss.aliyuncs.com. 60 IN     AAAA    2403:28c0:300:4:6413:9f34:f4a6:d22c
```

## **相关文档**

- [地域和Endpoint列表](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")