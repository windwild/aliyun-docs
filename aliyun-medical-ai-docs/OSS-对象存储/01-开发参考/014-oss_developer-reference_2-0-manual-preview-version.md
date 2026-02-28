### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[SDK参考](https://help.aliyun.com/zh/oss/developer-reference/sdk-code-samples/)OSS Python SDK V2

# OSS Python SDK V2

更新时间：2026-01-23 03:01:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：视频转码（Java SDK V1）](https://help.aliyun.com/zh/oss/developer-reference/java-video-transcoding)[下一篇：创建存储空间（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/create-bucket-using-oss-sdk-for-python-v2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速接入

环境准备

安装SDK

配置访问凭证

初始化客户端

客户端配置

使用自定义域名

超时控制

重试策略

设置连接池大小

HTTP/HTTPS 协议

代理服务器

使用内网域名

使用传输加速域名

使用专有域

使用金融云域名

使用政务云域名

自定义HTTPClient

访问凭证配置

使用RAM用户的AK

使用STS临时访问凭证

使用RAMRoleARN

使用ECSRAMRole

使用OIDCRoleARN

使用自定义访问凭证

匿名访问

错误自助排查

示例代码

[Github](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/tree/master) \| [OSS Python SDK V2开发者指南](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/DEVGUIDE-CN.md) ｜ [OSS Python SDK V2 Docs](https://gosspublic.alicdn.com/sdk-doc/alibabacloud-oss-python-sdk-v2/latest/index.html#)

## **快速接入**

接入OSS Python SDK V2的流程如下：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9925519671/CAEQWhiBgIDW15qzwBkiIGQ3MjQ0N2ZiODJhYjQyMGJhMDQ0NmRlY2YzNTRmMzVl5272737_20250624105943.598.svg)

### **环境准备**

要求 Python 3.8 及以上版本。

> 可以通过 `Python -version` 命令查看 Python 版本。如果当前环境没有 Python 或版本低于 Python 3.8，请 [下载并安装Python](https://www.python.org/downloads/)。

### **安装SDK**

- 执行以下命令安装OSS Python SDK V2代码包。请根据需求选择合适的OSS Python SDK V2版本，推荐使用最新的版本，确保本文中的代码示例可以正常运行。关于版本功能的更多信息，请参见 [Releases](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/releases)。















```shell
pip install alibabacloud-oss-v2
```

- 使用以下代码引入OSS Python SDK V2包。















```python
import alibabacloud_oss_v2 as oss
```


### **配置访问凭证**

使用 RAM 用户的 AccessKey 配置访问凭证。

1. 在 [RAM 控制台](https://ram.console.aliyun.com/users/create)，创建 **使用永久 AccessKey 访问** 的 RAM 用户，保存 AccessKey，然后为该用户授予 `AliyunOSSFullAccess` 权限。

2. 使用 RAM 用户 AccessKey 配置环境变量。






Linux



macOS



Windows



















1. 在命令行界面执行以下命令来将环境变量设置追加到`~/.bashrc`文件中。















      ```bash
      echo "export OSS_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.bashrc
      echo "export OSS_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.bashrc
      ```



      1. 执行以下命令使变更生效。















         ```bash
         source ~/.bashrc
         ```

      2. 执行以下命令检查环境变量是否生效。















         ```bash
         echo $OSS_ACCESS_KEY_ID
         echo $OSS_ACCESS_KEY_SECRET
         ```

1. 在终端中执行以下命令，查看默认Shell类型。















      ```bash
      echo $SHELL
      ```



      1. 根据默认Shell类型进行操作。






         Zsh



         Bash



















         1. 执行以下命令来将环境变量设置追加到 `~/.zshrc` 文件中。















            ```zsh
            echo "export OSS_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.zshrc
            echo "export OSS_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.zshrc
            ```

         2. 执行以下命令使变更生效。















            ```zsh
            source ~/.zshrc
            ```

         3. 执行以下命令检查环境变量是否生效。















            ```zsh
            echo $OSS_ACCESS_KEY_ID
            echo $OSS_ACCESS_KEY_SECRET
            ```


         1. 执行以下命令来将环境变量设置追加到 `~/.bash_profile` 文件中。















            ```zsh
            echo "export OSS_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.bash_profile
            echo "export OSS_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.bash_profile
            ```

         2. 执行以下命令使变更生效。















            ```zsh
            source ~/.bash_profile
            ```

         3. 执行以下命令检查环境变量是否生效。















            ```zsh
            echo $OSS_ACCESS_KEY_ID
            echo $OSS_ACCESS_KEY_SECRET
            ```

CMD

PowerShell

1. 在CMD中运行以下命令。















      ```bash
      setx OSS_ACCESS_KEY_ID "YOUR_ACCESS_KEY_ID"
      setx OSS_ACCESS_KEY_SECRET "YOUR_ACCESS_KEY_SECRET"
      ```



      1. 运行以下命令，检查环境变量是否生效。















         ```bash
         echo %OSS_ACCESS_KEY_ID%
         echo %OSS_ACCESS_KEY_SECRET%
         ```

1. 在PowerShell中运行以下命令。















      ```powershell
      [Environment]::SetEnvironmentVariable("OSS_ACCESS_KEY_ID", "YOUR_ACCESS_KEY_ID", [EnvironmentVariableTarget]::User)
      [Environment]::SetEnvironmentVariable("OSS_ACCESS_KEY_SECRET", "YOUR_ACCESS_KEY_SECRET", [EnvironmentVariableTarget]::User)
      ```



      1. 运行以下命令，检查环境变量是否生效。















         ```powershell
         [Environment]::GetEnvironmentVariable("OSS_ACCESS_KEY_ID", [EnvironmentVariableTarget]::User)
         [Environment]::GetEnvironmentVariable("OSS_ACCESS_KEY_SECRET", [EnvironmentVariableTarget]::User)
         ```

### 初始化客户端

> 运行示例代码前，请将代码中的 `<region-id>`等占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。

同步 OSSClient

异步 OSSClient

```python
import alibabacloud_oss_v2 as oss

def main():
    """
    Python SDK V2 客户端初始化配置说明：

    1. 签名版本：Python SDK V2 默认使用 V4 签名，提供更高的安全性
    2. Region配置：初始化 Client 时，必须指定阿里云 Region ID 作为请求地域标识
    3. Endpoint配置：
       - 可通过Endpoint参数自定义服务请求的访问域名
       - 当不指定 Endpoint 时，将根据 Region 自动构造公网访问域名
    4. 协议配置：
       - SDK 默认使用 HTTPS 协议构造访问域名
       - 如需使用 HTTP 协议，在指定域名时明确指定
    """

    # 从环境变量中加载凭证信息，用于身份验证
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()

    # 加载SDK的默认配置，并设置凭证提供者
    cfg = oss.config.load_default()
    cfg.credentials_provider = credentials_provider

    # 方式一：只填写Region（推荐）
    # 必须指定Region ID，SDK会根据Region自动构造HTTPS访问域名
    cfg.region = '<region-id>'

    # # 方式二：同时填写Region和Endpoint
    # # 必须指定Region ID
    # cfg.region = '<region-id>'
    # # 填写Bucket所在地域对应的外网Endpoint
    # cfg.endpoint = '<endpoint>'

    # 使用配置好的信息创建OSS客户端
    client = oss.Client(cfg)

    # 定义要上传的字符串内容
    text_string = "Hello, OSS!"
    data = text_string.encode('utf-8')  # 将字符串编码为UTF-8字节串

    # 执行上传对象的请求，指定存储空间名称、对象名称和数据内容
    result = client.put_object(oss.PutObjectRequest(
        bucket="Your Bucket Name",
        key="Your Object Key",
        body=data,
    ))

    # 输出请求的结果状态码、请求ID、ETag，用于检查请求是否成功
    print(f'status code: {result.status_code}\n'
          f'request id: {result.request_id}\n'
          f'etag: {result.etag}'
    )

# 当此脚本被直接运行时，调用main函数
if __name__ == "__main__":
    main()  # 脚本入口，当文件被直接运行时调用main函数
```

使用异步 OSSClient 需要：

- **alibabacloud-oss-v2**：>= 1.2.0

- **安装 aiohttp**：`pip install aiohttp`


```python
import asyncio
import alibabacloud_oss_v2 as oss
import alibabacloud_oss_v2.aio as oss_aio

async def main():
    """
    Python SDK V2 异步客户端初始化配置说明：

    1. 签名版本：Python SDK V2 默认使用 V4 签名，提供更高的安全性

    2. Region配置：初始化 AsyncClient 时，必须指定阿里云 Region ID 作为请求地域标识

    3. Endpoint配置：
       - 可通过Endpoint参数自定义服务请求的访问域名
       - 当不指定 Endpoint 时，将根据 Region 自动构造公网访问域名

    4. 协议配置：
       - SDK 默认使用 HTTPS 协议构造访问域名
       - 如需使用 HTTP 协议，在指定域名时明确指定

    5. 异步特性：
       - 导入异步模块：import alibabacloud_oss_v2.aio as oss_aio
       - 创建异步客户端：oss_aio.AsyncClient(cfg)
       - 所有操作需要使用 await 关键字
       - 需要在 finally 块中调用 await client.close() 关闭连接
       - 需要安装 aiohttp 依赖：pip install aiohttp
    """

    # 从环境变量中加载凭证信息，用于身份验证
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()

    # 加载SDK的默认配置，并设置凭证提供者
    cfg = oss.config.load_default()
    cfg.credentials_provider = credentials_provider

    # 方式一：只填写Region（推荐）
    # 必须指定Region ID，SDK会根据Region自动构造HTTPS访问域名
    cfg.region = '<region-id>'

    # # 方式二：同时填写Region和Endpoint
    # # 必须指定Region ID
    # cfg.region = '<region-id>'
    # # 填写Bucket所在地域对应的外网Endpoint
    # cfg.endpoint = '<endpoint>'

    # 使用配置好的信息创建OSS异步客户端
    client = oss_aio.AsyncClient(cfg)

    try:
        # 定义要上传的字符串内容
        text_string = "Hello, OSS!"
        data = text_string.encode('utf-8')  # 将字符串编码为UTF-8字节串

        # 执行异步上传对象的请求，指定存储空间名称、对象名称和数据内容
        # 注意：使用 await 关键字等待异步操作完成
        result = await client.put_object(
            oss.PutObjectRequest(
                bucket="Your Bucket Name",
                key="Your Object Key",
                body=data,
            )
        )

        # 输出请求的结果状态码、请求ID、ETag，用于检查请求是否成功
        print(f'status code: {result.status_code}\n'
              f'request id: {result.request_id}\n'
              f'etag: {result.etag}'
        )

    except Exception as e:
        print(f'上传失败: {e}')

    finally:
        # 关闭异步客户端连接（重要：避免资源泄漏）
        await client.close()

# 当此脚本被直接运行时，调用main函数
if __name__ == "__main__":
    # 使用 asyncio.run() 运行异步主函数
    asyncio.run(main())
```

运行后将会输出上传文件成功的结果：

```shell
status code: 200
request id: 6875F95738B0ED3030F086A0
etag: "56AAD346F0899BFE8BDD02C06BBE511E"
```

## **客户端配置**

**客户端支持哪些配置？**

|     |     |     |
| --- | --- | --- |
| 参数名 | 说明 | 示例 |
| region | (必选)请求发送的区域, 必选 | oss.config.Config(region="<region-id>") |
| credentials\_provider | (必选)设置访问凭证 | oss.config.Config(credentials\_provider=provider) |
| endpoint | 访问域名 | oss.config.Config(endpoint="oss-<region-id>.aliyuncs.com") |
| http\_client | HTTP客户端 | oss.config.Config(http\_client=customClient) |
| retry\_max\_attempts | HTTP请求时的最大尝试次数, 默认值为 3 | oss.config.Config(retry\_max\_attempts=5) |
| retryer | HTTP请求时的重试实现 | oss.config.Config(retryer=customRetryer) |
| connect\_timeout | 建立连接的超时时间, 默认值为 10 秒 | oss.config.Config(connect\_timeout=20) |
| readwrite\_timeout | 应用读写数据的超时时间, 默认值为 20 秒 | oss.config.Config(readwrite\_timeout=30) |
| insecure\_skip\_verify | 是否跳过SSL证书校验，默认检查SSL证书 | oss.config.Config(insecure\_skip\_verify=true) |
| enabled\_redirect | 是否开启HTTP重定向, 默认不开启 | oss.config.Config(enabled\_redirect=true) |
| proxy\_host | 设置代理服务器 | oss.config.Config(proxy\_host=" [http://user:passswd@proxy.example-\*\*\*.com](http://user:passswd@proxy.example-***.com/)") |
| signature\_version | 签名版本，默认值为v4 | oss.config.Config(signature\_version="v1") |
| disable\_ssl | 不使用https请求，默认使用https | oss.config.Config(disable\_ssl=true) |
| use\_path\_style | 使用路径请求风格，即二级域名请求风格，默认为bucket托管域名 | oss.config.Config(use\_path\_style=true) |
| use\_cname | 是否使用自定义域名访问，默认不使用 | oss.config.Config(use\_cname=true) |
| use\_dualstack\_endpoint | 是否使用双栈域名访问，默认不使用 | oss.config.Config(use\_dualstack\_endpoint=true) |
| use\_accelerate\_endpoint | 是否使用传输加速域名访问，默认不使用 | oss.config.Config(use\_accelerate\_endpoint=true) |
| use\_internal\_endpoint | 是否使用内网域名访问，默认不使用 | oss.config.Config(use\_internal\_endpoint=true) |
| disable\_upload\_crc64\_check | 上传时关闭CRC64校验，默认开启CRC64校验 | oss.config.Config(disable\_upload\_crc64\_check=true) |
| disable\_download\_crc64\_check | 下载时关闭CRC64校验，默认开启CRC64校验 | oss.config.Config(disable\_download\_crc64\_check=true) |
| additional\_headers | 指定额外的签名请求头，V4签名下有效 | oss.config.Config(additional\_headers=\["content-length"\]) |
| user\_agent | 指定额外的User-Agent信息 | oss.config.Config(user\_agent="user identifier") |

### **使用自定义域名**

使用OSS默认域名访问时，可能会出现文件禁止访问、文件无法预览等问题；通过 [通过自定义域名访问OSS](https://help.aliyun.com/zh/oss/user-guide/access-buckets-via-custom-domain-names#concept-zt4-cvy-5db "")，不仅支持浏览器直接预览文件，还可结合CDN加速分发。

> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。

```python
import alibabacloud_oss_v2 as oss

def main():
    # 从环境变量中加载凭证信息，用于身份验证
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()

    # 加载SDK的默认配置，并设置凭证提供者
    cfg = oss.config.load_default()
    cfg.credentials_provider = credentials_provider

    # 填写Bucket所在地域
    cfg.region = '<region-id>'

    # 请填写您的自定义域名。例如www.example-***.com
    cfg.endpoint = 'https://www.example-***.com'

    # 请注意，设置true开启CNAME选项，否则无法使用自定义域名
    cfg.use_cname = True

    # 使用配置好的信息创建OSS客户端
    client = oss.Client(cfg)

    # 使用创建好的client执行后续操作...

# 当此脚本被直接运行时，调用main函数
if __name__ == "__main__":
    main()  # 脚本入口，当文件被直接运行时调用main函数
```

### **超时控制**

> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。

```python
import alibabacloud_oss_v2 as oss
from typing import Dict, Any

def main():
    # 从环境变量中加载凭证信息，用于身份验证
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()

    # 加载默认的配置信息
    cfg = oss.config.load_default()

    # 设置建立连接的超时时间, 默认值 10秒
    cfg.connect_timeout = 30

    # 设置应用读写数据的超时时间, 默认值 20秒
    cfg.readwrite_timeout = 30

    # 设置凭证提供者
    cfg.credentials_provider = credentials_provider

    # 填写Bucket所在地域
    cfg.region = '<region-id>'

    # 使用配置好的信息创建OSS客户端
    client = oss.Client(cfg)

    # 使用创建好的client执行后续操作...

# 当此脚本被直接运行时，调用main函数
if __name__ == "__main__":
    main()  # 脚本入口，当文件被直接运行时调用main函数
```

### **重试策略**

> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。

```python
import alibabacloud_oss_v2 as oss

def main():
    """
    SDK 重试策略配置说明：

    默认重试策略：
    当没有配置重试策略时，SDK 使用 StandardRetryer() 作为客户端的默认实现，其默认配置如下：
    - max_attempts：设置最大尝试次数。默认为3次
    - max_backoff：设置最大退避时间（单位：秒）。默认为20秒
    - base_delay：设置基础延迟时间（单位：秒）。默认为0.2秒
    - backoff_delayer：设置退避算法。默认使用FullJitter退避算法
      计算公式为：[0.0, 1.0) * min(2^attempts * baseDelay, maxBackoff)\
    - error_retryables：可重试的错误类型，请参阅https://gosspublic.alicdn.com/sdk-doc/alibabacloud-oss-python-sdk-v2/latest/_modules/alibabacloud_oss_v2/retry/error_retryable.html\
\
    当发生可重试错误时，将使用其提供的配置来延迟并随后重试该请求。\
    请求的总体延迟会随着重试次数而增加，如果默认配置不满足您的场景需求时，\
    可配置重试参数或者修改重试实现。\
    """\
\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载默认的配置信息\
    cfg = oss.config.load_default()\
\
    # 配置重试策略示例：\
\
    # 1. 自定义最大重试次数（默认为3次，这里设置为5次）\
    cfg.retryer = oss.retry.StandardRetryer(max_attempts=5)\
\
    # 2. 自定义退避延迟时间\
    # 调整基础延迟时间 base_delay 为0.5秒（默认0.2秒），最大退避时间 max_backoff 为25秒（默认20秒）\
    # cfg.retryer = oss.retry.StandardRetryer(max_backoff=25, base_delay=0.5)\
\
    # 3. 自定义退避算法\
    # 使用固定时间退避算法替代默认的FullJitter算法，每次延迟2秒\
    # cfg.retryer = oss.retry.StandardRetryer(backoff_delayer=oss.retry.FixedDelayBackoff(2))\
\
    # 4. 禁用重试策略\
    # 如需禁用所有重试尝试时，可以使用retry.NopRetryer实现\
    # cfg.retryer = oss.retry.NopRetryer()\
\
    # 设置凭证提供者\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **设置连接池大小**\
\
在`http_client`中指定`max_connections`参数即可配置连接池大小。\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
#!/usr/bin/env python3\
# -*- coding: utf-8 -*-\
\
# OSS Python SDK V2 连接池配置示例\
\
import alibabacloud_oss_v2 as oss\
\
def main():\
\
    # 从环境变量中加载访问凭证（需要设置OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET）\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    config = oss.config.load_default()\
    config.credentials_provider = credentials_provider\
\
    # 设置OSS服务地域\
    config.region = "<region-id>"\
\
    # ============ 自定义HTTPClient配置 ============\
    # 创建HTTP客户端配置参数字典\
    http_client_config = {}\
\
    # 设置连接池大小为100，默认为20\
    http_client_config["max_connections"] = 100\
\
    # 使用自定义配置创建HTTP客户端\
    http_client = oss.transport.RequestsHttpClient(**http_client_config)\
\
    # 将自定义的HTTP客户端设置到配置对象中\
    config.http_client = http_client\
    # ============================================\
\
    # 初始化OSS客户端实例\
    client = oss.Client(config)\
\
    # 配置Bucket和文件信息\
    bucket = "example-bucket"             # Bucket名称\
    key = "dest.jpg"                      # OSS中的文件路径\
    file_path = "dest.jpg"                # 本地保存路径\
\
    # 将OSS中的文件下载到本地指定路径\
    client.get_object_to_file(oss.GetObjectRequest(bucket, key), file_path)\
    print(f"文件下载完成: {key} -> {file_path}")\
    print(f"连接池大小已设置为: {http_client_config['max_connections']}")\
\
if __name__ == "__main__":\
    # 程序入口点\
    try:\
        main()\
    except Exception as e:\
        print(f"运行过程中发生错误: {e}")\
        raise\
```\
\
### **HTTP/HTTPS 协议**\
\
使用 `cfg.disable_ssl = True` 设置不使用HTTPS协议。\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
\
    # 设置不使用https请求\
    cfg.disable_ssl = True\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **代理服务器**\
\
企业安全策略通常限制直接访问公网，配置代理服务器访问 OSS。\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
\
    # 设置user_agent\
    cfg.user_agent = 'aliyun-sdk-python'\
\
    # 设置代理服务器\
    cfg.proxy_host = 'http://user:passswd@proxy.example-***.com'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **使用内网域名**\
\
使用内网域名访问同地域的OSS资源，可以降低流量成本并提高访问速度。\
\
> 运行示例代码前，请将代码中的 `<region-id>`等占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 方式一： 填写Region并设置use_internal_endpoint为true\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
    cfg.use_internal_endpoint = True\
\
    # # 方式二： 直接填写Region和Endpoint\
    # # 填写Bucket所在地域\
    # cfg.region = '<region-id>'\
    # # 填写Bucket所在地域对应的内网Endpoint\
    # cfg.endpoint = '<endpoint>'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **使用传输加速域名**\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 方式一： 填写Region并设置use_accelerate_endpoint为true\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
    cfg.use_accelerate_endpoint = True\
\
    # # 方式二： 直接填写Region和传输加速Endpoint\
    # # 填写Bucket所在地域\
    # cfg.region = '<region-id>'\
    # # 填写Bucket所在地域对应的传输加速Endpoint\
    # cfg.endpoint = 'https://oss-accelerate.aliyuncs.com'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **使用专有域**\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
\
    # 请填写您的专有域。例如：https://service.corp.example.com\
    cfg.endpoint = 'https://service.corp.example.com'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **使用金融云域名**\
\
以下是使用 [金融云](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#dbe294402aq6j "") 域名配置OSSClient的示例代码。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Region和Endpoint\
    # 填写Bucket所在地域。以华东1 金融云为例，Region填写为cn-hangzhou-finance\
    cfg.region = 'cn-hangzhou-finance'\
    # 填写Bucket所在地域对应的内网Endpoint。以华东1 金融云为例，Endpoint填写为'https://oss-cn-hzjbp-a-internal.aliyuncs.com',\
    # 如需指定为http协议，请在指定域名时填写为'http://oss-cn-hzjbp-a-internal.aliyuncs.com'\
    cfg.endpoint = 'https://oss-cn-hzjbp-a-internal.aliyuncs.com'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **使用政务云域名**\
\
以下是使用 [政务云](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#3e2a1817f0pps "") 域名配置OSSClient的示例代码。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Region和Endpoint\
    # 填写Bucket所在地域。以华北2 阿里政务云1为例，Region填写为cn-north-2-gov-1\
    cfg.region = 'cn-north-2-gov-1'\
    # 填写Bucket所在地域对应的内网Endpoint。以华北2 阿里政务云1为例，Endpoint填写为'https://oss-cn-north-2-gov-1-internal.aliyuncs.com',\
    # 如需指定为http协议，请在指定域名时填写为'http://oss-cn-north-2-gov-1-internal.aliyuncs.com'\
    cfg.endpoint = 'https://oss-cn-north-2-gov-1-internal.aliyuncs.com'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **自定义HTTPClient**\
\
当常用配置参数无法满足场景需求时，您可以使用cfg.http\_client替换默认的 HTTP 客户端。\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
from typing import Dict, Any\
\
def main():\
    # 从环境变量中加载凭证信息，用于身份验证\
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
    # 加载默认的配置信息\
    cfg = oss.config.load_default()\
\
    # 设置HTTP客户端的参数\
    kwargs: Dict[str, Any] = {}\
\
    # 设置session\
    # kwargs["session"] = requests.Session()\
\
    # 设置adapter\
    # kwargs["adapter"] = HTTPAdapter()\
\
    # 是否跳过证书检查，默认不跳过\
    # kwargs["insecure_skip_verify"] = False\
\
    # 是否打开启HTTP重定向，默认不启用\
    # kwargs["enabled_redirect"] = False\
\
    # 设置代理服务器\
    # kwargs["proxy_host"] = config.proxy_host\
\
    # 设置块大小\
    # kwargs["block_size"] = 16 * 1024\
\
    # 连接超时, 默认值 10秒\
    kwargs["connect_timeout"] = 30\
\
    # 应用读写数据的超时时间, 默认值 20秒\
    kwargs["readwrite_timeout"] = 30\
\
    # 最大连接数，默认值 20\
    kwargs["max_connections"] = 1024\
\
    # 创建HTTP客户端，并传入HTTP客户端参数\
    cfg.http_client = oss.transport.RequestsHttpClient(**kwargs)\
\
    # 设置凭证提供者\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
## 访问凭证配置\
\
OSS 提供多种凭证初始化方式。请根据您的认证和授权需求选择合适的初始化方式。\
\
如何选择访问凭证？\
\
|     |     |     |     |     |     |\
| --- | --- | --- | --- | --- | --- |\
| **凭证提供者初始化方式** | **适用场景** | **是否需要提供前置的AK或STS Token** | **底层实现基于的凭证** | **凭证有效期** | **凭证轮转或刷新方式** |\
| [使用RAM用户的AK](https://help.aliyun.com/zh/oss/developer-reference/configure-access-credentials-for-python-v2#33cf434613akr "") | 部署运行在安全、稳定且不易受外部攻击的环境的应用程序，无需频繁轮转凭证就可以长期访问云服务 | 是 | AK | 长期 | 手动轮转 |\
| [使用STS临时访问凭证](https://help.aliyun.com/zh/oss/developer-reference/configure-access-credentials-for-python-v2#bdd891bc88eok "") | 部署运行在不可信的环境的应用程序，希望能控制访问的有效期、权限 | 是 | STS Token | 临时 | 手动刷新 |\
| [使用RAMRoleARN](https://help.aliyun.com/zh/oss/developer-reference/configure-access-credentials-for-python-v2#3cdc03a332cf6 "") | 需要授权访问云服务，例如跨阿里云账号访问云服务的应用程序 | 是 | STS Token | 临时 | 自动刷新 |\
| [使用ECSRAMRole](https://help.aliyun.com/zh/oss/developer-reference/configure-access-credentials-for-python-v2#3cd8c42aad2c0 "") | 部署运行在阿里云的ECS实例、ECI实例、容器服务Kubernetes版的Worker节点中的应用程序 | 否 | STS Token | 临时 | 自动刷新 |\
| [使用OIDCRoleARN](https://help.aliyun.com/zh/oss/developer-reference/configure-access-credentials-for-python-v2#64a6283d08vpq "") | 部署运行在阿里云的容器服务Kubernetes版的Worker节点中的不可信应用程序 | 否 | STS Token | 临时 | 自动刷新 |\
| [使用自定义访问凭证](https://help.aliyun.com/zh/oss/developer-reference/configure-access-credentials-for-python-v2#389b3e0cfc9wz "") | 如果以上凭证配置方式都不满足要求时，您可以自定义获取凭证的方式 | 自定义 | 自定义 | 自定义 | 自定义 |\
\
### 使用RAM用户的AK\
\
如果您的应用程序部署运行在安全、稳定且不易受外部攻击的环境中，需要长期访问您的OSS，且不能频繁轮转凭证时，您可以使用阿里云主账号或RAM用户的AK（Access Key ID、Access Key Secret）初始化凭证提供者。需要注意的是，该方式需要您手动维护一个AK，存在安全性风险和维护复杂度增加的风险。\
\
**警告**\
\
- 阿里云账号拥有资源的全部权限，AK一旦泄露，会给系统带来巨大风险，不建议使用。推荐使用最小化授权的RAM用户的AK。\
\
- 如需创建RAM用户的AK，请直接访问 [创建AccessKey](https://help.aliyun.com/zh/ram/create-an-accesskey-pair-1#section-rjh-18m-7kp "")。RAM用户的Access Key ID、Access Key Secret信息仅在创建时显示，请及时保存，如若遗忘请考虑创建新的AK进行轮换。\
\
\
环境变量\
\
静态凭证\
\
1. 使用RAM用户AccessKey配置环境变量。\
\
\
\
\
\
\
Linux\
\
\
\
macOS\
\
\
\
Windows\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
1. 在命令行界面执行以下命令来将环境变量设置追加到`~/.bashrc`文件中。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
      ```bash\
      echo "export OSS_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.bashrc\
      echo "export OSS_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.bashrc\
      ```\
\
\
\
      1. 执行以下命令使变更生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
         ```bash\
         source ~/.bashrc\
         ```\
\
      2. 执行以下命令检查环境变量是否生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
         ```bash\
         echo $OSS_ACCESS_KEY_ID\
         echo $OSS_ACCESS_KEY_SECRET\
         ```\
\
1. 在终端中执行以下命令，查看默认Shell类型。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
      ```bash\
      echo $SHELL\
      ```\
\
\
\
      1. 根据默认Shell类型进行操作。\
\
\
\
\
\
\
         Zsh\
\
\
\
         Bash\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
         1. 执行以下命令来将环境变量设置追加到 `~/.zshrc` 文件中。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
            ```zsh\
            echo "export OSS_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.zshrc\
            echo "export OSS_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.zshrc\
            ```\
\
         2. 执行以下命令使变更生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
            ```zsh\
            source ~/.zshrc\
            ```\
\
         3. 执行以下命令检查环境变量是否生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
            ```zsh\
            echo $OSS_ACCESS_KEY_ID\
            echo $OSS_ACCESS_KEY_SECRET\
            ```\
\
\
         1. 执行以下命令来将环境变量设置追加到 `~/.bash_profile` 文件中。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
            ```zsh\
            echo "export OSS_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.bash_profile\
            echo "export OSS_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.bash_profile\
            ```\
\
         2. 执行以下命令使变更生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
            ```zsh\
            source ~/.bash_profile\
            ```\
\
         3. 执行以下命令检查环境变量是否生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
            ```zsh\
            echo $OSS_ACCESS_KEY_ID\
            echo $OSS_ACCESS_KEY_SECRET\
            ```\
\
CMD\
\
PowerShell\
\
1. 在CMD中运行以下命令。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
      ```bash\
      setx OSS_ACCESS_KEY_ID "YOUR_ACCESS_KEY_ID"\
      setx OSS_ACCESS_KEY_SECRET "YOUR_ACCESS_KEY_SECRET"\
      ```\
\
\
\
      1. 运行以下命令，检查环境变量是否生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
         ```bash\
         echo %OSS_ACCESS_KEY_ID%\
         echo %OSS_ACCESS_KEY_SECRET%\
         ```\
\
1. 在PowerShell中运行以下命令。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
      ```powershell\
      [Environment]::SetEnvironmentVariable("OSS_ACCESS_KEY_ID", "YOUR_ACCESS_KEY_ID", [EnvironmentVariableTarget]::User)\
      [Environment]::SetEnvironmentVariable("OSS_ACCESS_KEY_SECRET", "YOUR_ACCESS_KEY_SECRET", [EnvironmentVariableTarget]::User)\
      ```\
\
\
\
      1. 运行以下命令，检查环境变量是否生效。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
         ```powershell\
         [Environment]::GetEnvironmentVariable("OSS_ACCESS_KEY_ID", [EnvironmentVariableTarget]::User)\
         [Environment]::GetEnvironmentVariable("OSS_ACCESS_KEY_SECRET", [EnvironmentVariableTarget]::User)\
         ```\
\
2. 参考上述方式修改系统环境变量后，请重启或刷新您的编译运行环境，包括IDE、命令行界面、其他桌面应用程序及后台服务，以确保最新的系统环境变量成功加载。\
\
3. 使用环境变量来传递凭证信息。\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
       # 从环境变量中加载凭证信息，用于身份验证\
       credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
       # 加载SDK的默认配置，并设置凭证提供者\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 填写Bucket所在地域\
       cfg.region = '<region-id>'\
\
       # 使用配置好的信息创建OSS客户端\
       client = oss.Client(cfg)\
\
       # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
\
以下示例代码展示了如何对访问凭据直接进行硬编码，显式设置要使用的访问密钥。\
\
**警告**\
\
请勿将访问凭据嵌入到生产环境的应用程序中，此方法仅用于测试目的。\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 创建静态凭证提供者，显式设置访问密钥和密钥密码，请替换为您的RAM用户的AccessKey ID和AccessKey Secret\
    credentials_provider = oss.credentials.StaticCredentialsProvider(\
        access_key_id="RAM AccessKey ID",\
        access_key_secret="RAM AccessKey Secret"\
    )\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### 使用STS临时访问凭证\
\
如果您的应用程序需要临时访问OSS，您可以使用通过STS服务获取的临时身份凭证（Access Key ID、Access Key Secret和Security Token）初始化凭证提供者。需要注意的是，该方式需要您手动维护一个STS Token，存在安全性风险和维护复杂度增加的风险。此外，如果您需要多次临时访问OSS，您需要手动刷新STS Token。\
\
**重要**\
\
- 如果您希望通过OpenAPI的方式简单快速获取到STS临时访问凭证，请参见 [AssumeRole - 获取扮演角色的临时身份凭证](https://help.aliyun.com/zh/ram/developer-reference/api-sts-2015-04-01-assumerole "")。\
\
- 如果您希望通过SDK的方式获取STS临时访问凭证，请参见 [使用STS临时访问凭证访问OSS](https://help.aliyun.com/zh/oss/developer-reference/use-temporary-access-credentials-provided-by-sts-to-access-oss#section-rjh-18m-7kp "")。\
\
- 请注意，STS Token在生成的时候需要指定过期时间，过期后自动失效不能再使用。\
\
- 如果您希望获取关于STS服务的接入点列表，请参见 [服务接入点](https://help.aliyun.com/zh/ram/developer-reference/api-sts-2015-04-01-endpoint "")。\
\
\
环境变量\
\
静态凭证\
\
1. 使用临时身份凭证设置环境变量。\
\
\
\
\
\
\
Mac OS X/Linux/Unix\
\
\
\
Windows\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
**警告**\
\
\
\
\
\
   - 请注意，此处使用的是通过STS服务获取的临时身份凭证（Access Key ID、Access Key Secret和Security Token），而非RAM用户的Access Key和Access Key Secret。\
\
   - 请注意区分STS服务获取的Access Key ID以STS开头，例如“STS.L4aBSCSJVMuKg5U1\*\*\*\*”。\
\
\
```shell\
export OSS_ACCESS_KEY_ID=<STS_ACCESS_KEY_ID>\
export OSS_ACCESS_KEY_SECRET=<STS_ACCESS_KEY_SECRET>\
export OSS_SESSION_TOKEN=<STS_SECURITY_TOKEN>\
```\
\
**警告**\
\
   - 请注意，此处使用的是通过STS服务获取的临时身份凭证（Access Key ID、Access Key Secret和Security Token），而非RAM用户的AK（Access Key ID、Access Key Secret）。\
\
   - 请注意区分STS服务获取的Access Key ID以STS开头，例如“STS.L4aBSCSJVMuKg5U1\*\*\*\*”。\
\
\
```shell\
set OSS_ACCESS_KEY_ID=<STS_ACCESS_KEY_ID>\
set OSS_ACCESS_KEY_SECRET=<STS_ACCESS_KEY_SECRET>\
set OSS_SESSION_TOKEN=<STS_SECURITY_TOKEN>\
```\
\
2. 通过环境变量来传递凭证信息。\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
       # 从环境变量中加载访问OSS所需的认证信息，用于身份验证\
       credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
       # 加载SDK的默认配置，并设置凭证提供者\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 填写Bucket所在地域\
       cfg.region = '<region-id>'\
\
       # 使用配置好的信息创建OSS客户端\
       client = oss.Client(cfg)\
\
       # 使用创建好的client执行后续操作...\
\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
\
以下示例代码展示了如何对访问凭据直接进行硬编码，显式设置要使用的临时访问密钥。\
\
**警告**\
\
请勿将访问凭据嵌入到生产环境的应用程序中，此方法仅用于测试目的。\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
    # 填写获取的临时访问密钥AccessKey ID和AccessKey Secret，非阿里云账号AccessKey ID和AccessKey Secret。\
    # 请注意区分STS服务获取的Access Key ID是以STS开头，如下所示。\
    sts_access_key_id = 'STS.****************'\
    sts_access_key_secret = 'yourAccessKeySecret'\
    # 填写获取的STS安全令牌（SecurityToken）。\
    sts_security_token = 'yourSecurityToken'\
\
    # 创建静态凭证提供者，显式设置临时访问密钥AccessKey ID和AccessKey Secret，以及STS安全令牌\
    credentials_provider = oss.credentials.StaticCredentialsProvider(\
        access_key_id=sts_access_key_id,\
        access_key_secret=sts_access_key_secret,\
        security_token=sts_security_token,\
    )\
\
    # 加载SDK的默认配置，并设置凭证提供者\
    cfg = oss.config.load_default()\
    cfg.credentials_provider = credentials_provider\
\
    # 填写Bucket所在地域\
    cfg.region = '<region-id>'\
\
    # 使用配置好的信息创建OSS客户端\
    client = oss.Client(cfg)\
\
    # 使用创建好的client执行后续操作...\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
    main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
### **使用RAMRoleARN**\
\
如果您的应用程序需要授权访问OSS，例如跨阿里云账号访问OSS，您可以使用RAMRoleARN初始化凭证提供者。该方式底层实现是STS Token。通过指定RAM角色的ARN（Alibabacloud Resource Name），Credentials工具会前往STS服务获取STS Token，并在会话到期前调用AssumeRole接口申请新的STS Token。此外，您还可以通过为`policy`赋值来限制RAM角色到一个更小的权限集合。\
\
**重要**\
\
- 阿里云账号拥有资源的全部权限，AK一旦泄露，会给系统带来巨大风险，不建议使用。推荐使用最小化授权的RAM用户的AK。\
\
- 如需创建RAM用户的AK，请直接访问 [创建AccessKey](https://help.aliyun.com/zh/ram/create-an-accesskey-pair-1#section-rjh-18m-7kp "")。RAM用户的Access Key ID、Access Key Secret信息仅在创建时显示，请及时保存，如若遗忘请考虑创建新的AK进行轮换。\
\
- 如需获取RAMRoleARN，请直接访问 [创建角色](https://help.aliyun.com/zh/ram/developer-reference/api-ram-2015-05-01-createrole "")。\
\
\
1. 添加alibabacloud\_credentials依赖。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```shell\
pip install alibabacloud_credentials\
```\
\
2. 配置AK和RAMRoleARN作为访问凭证。\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
# -*- coding: utf-8 -*-\
import os\
from alibabacloud_credentials.client import Client\
from alibabacloud_credentials.models import Config\
import alibabacloud_oss_v2 as oss\
\
def main():\
       config = Config(\
           # 从环境变量中获取RAM用户的访问密钥（AccessKey ID和AccessKey Secret）\
           access_key_id=os.getenv('ALIBABA_CLOUD_ACCESS_KEY_ID'),\
           access_key_secret=os.getenv('ALIBABA_CLOUD_ACCESS_KEY_SECRET'),\
           type='ram_role_arn',\
           # 要扮演的RAM角色ARN，示例值：acs:ram::123456789012****:role/adminrole，可以通过环境变量ALIBABA_CLOUD_ROLE_ARN设置RoleArn\
           role_arn='<RoleArn>',\
           # 角色会话名称，可以通过环境变量ALIBABA_CLOUD_ROLE_SESSION_NAME设置RoleSessionName\
           role_session_name='<RoleSessionName>',\
           # 设置更小的权限策略，非必填。示例值：{"Statement": [{"Action": ["*"],"Effect": "Allow","Resource": ["*"]}],"Version":"1"}\
           policy='<Policy>',\
           # 设置角色会话有效期，单位为秒，默认值为3600秒（1小时），非必填\
           role_session_expiration=3600\
       )\
\
       cred_client = Client(config)\
\
       def get_credentials_wrapper():\
           cred = cred_client.get_credential()\
           return oss.credentials.Credentials(access_key_id=cred.access_key_id, access_key_secret=cred.access_key_secret, security_token=cred.security_token)\
\
       # 创建凭证提供者，用于动态加载凭证\
       credentials_provider = oss.credentials.CredentialsProviderFunc(func=get_credentials_wrapper)\
\
       # 加载OSS SDK的默认配置\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 填写Bucket所在地域\
       cfg.region = '<region-id>'\
\
       # 创建OSS客户端实例\
       client = oss.Client(cfg)\
\
       # 使用client进行后续操作...\
\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
\
### 使用ECSRAMRole\
\
如果您的应用程序运行在ECS实例、ECI实例、容器服务Kubernetes版的Worker节点中，建议您使用ECSRAMRole初始化凭证提供者。该方式底层实现是STS Token。ECSRAMRole允许您将一个角色关联到ECS实例、ECI实例或容器服务 Kubernetes 版的Worker节点，实现在实例内部自动刷新STS Token。该方式无需您提供一个AK或STS Token，消除了手动维护AK或STS Token的风险。如何获取ECSRAMRole，请参见 [创建角色](https://help.aliyun.com/zh/ram/developer-reference/api-ram-2015-05-01-createrole "")。\
\
1. 添加alibabacloud\_credentials依赖。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```shell\
pip install alibabacloud_credentials\
```\
\
2. 配置ECSRAMRole作为访问凭证。\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
from alibabacloud_credentials.client import Client\
from alibabacloud_credentials.models import Config\
import alibabacloud_oss_v2 as oss\
\
def main():\
       config = Config(\
           type='ecs_ram_role',      # 访问凭证类型。固定为ecs_ram_role。\
           role_name='EcsRoleExample'    # 为ECS授予的RAM角色的名称。可选参数。如果不设置，将自动检索。强烈建议设置，以减少请求。\
       )\
\
       cred_client = Client(config)\
\
       def get_credentials_wrapper():\
           cred = cred_client.get_credential()\
           return oss.credentials.Credentials(access_key_id=cred.access_key_id, access_key_secret=cred.access_key_secret, security_token=cred.security_token)\
\
       # 创建凭证提供者，用于动态加载凭证\
       credentials_provider = oss.credentials.CredentialsProviderFunc(func=get_credentials_wrapper)\
\
       # 加载OSS SDK的默认配置\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 填写Bucket所在地域\
       cfg.region = '<region-id>'\
\
       # 创建OSS客户端实例\
       client = oss.Client(cfg)\
\
       # 使用client进行后续操作...\
\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
\
### **使用OIDCRoleARN**\
\
在容器服务Kubernetes版中设置了Worker节点RAM角色后，对应节点内的Pod中的应用也就可以像ECS上部署的应用一样，通过元数据服务（Meta Data Server）获取关联角色的STS Token。但如果容器集群上部署的是不可信的应用（比如部署您的客户提交的应用，代码也没有对您开放），您可能并不希望它们能通过元数据服务获取Worker节点关联实例RAM角色的STS Token。为了避免影响云上资源的安全，同时又能让这些不可信的应用安全地获取所需的STS Token，实现应用级别的权限最小化，您可以使用RRSA（RAM Roles for Service Account）功能。该方式底层实现是STS Token。阿里云容器集群会为不同的应用Pod创建和挂载相应的服务账户OIDC Token文件，并将相关配置信息注入到环境变量中，Credentials工具通过获取环境变量的配置信息，调用STS服务的AssumeRoleWithOIDC接口换取绑定角色的STS Token。该方式无需您提供一个AK或STS Token，消除了手动维护AK或STS Token的风险。详情请参见 [通过RRSA配置ServiceAccount的RAM权限实现Pod权限隔离](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/use-rrsa-to-authorize-pods-to-access-different-cloud-services#task-2142941 "")。\
\
1. 添加alibabacloud\_credentials依赖。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```shell\
pip install alibabacloud_credentials\
```\
\
\
2. 配置OIDCRoleArn作为访问凭证。\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
# -*- coding: utf-8 -*-\
import os\
from alibabacloud_credentials.client import Client\
from alibabacloud_credentials.models import Config\
import alibabacloud_oss_v2 as oss\
\
def main():\
       config = Config(\
           # 指定Credential类型，固定值为oidc_role_arn。\
           type='oidc_role_arn',\
           # RAM角色名称ARN，可以通过环境变量ALIBABA_CLOUD_ROLE_ARN设置RoleArn\
           role_arn=os.environ.get('<RoleArn>'),\
           # OIDC提供商ARN，可以通过环境变量ALIBABA_CLOUD_OIDC_PROVIDER_ARN设置OidcProviderArn\
           oidc_provider_arn=os.environ.get('<OidcProviderArn>'),\
           # OIDC Token文件路径，可以通过环境变量ALIBABA_CLOUD_OIDC_TOKEN_FILE设置OidcTokenFilePath\
           oidc_token_file_path=os.environ.get('<OidcTokenFilePath>'),\
           # 角色会话名称，可以通过环境变量ALIBABA_CLOUD_ROLE_SESSION_NAME设置RoleSessionName\
           role_session_name='<RoleSessionName>',\
           # 设置更小的权限策略，非必填。示例值：{"Statement": [{"Action": ["*"],"Effect": "Allow","Resource": ["*"]}],"Version":"1"}\
           policy='<Policy>',\
           # 设置角色会话有效期，单位为秒，默认值为3600秒（1小时），非必填\
           role_session_expiration=3600\
       )\
\
       cred_client = Client(config)\
\
       def get_credentials_wrapper():\
           cred = cred_client.get_credential()\
           return oss.credentials.Credentials(access_key_id=cred.access_key_id, access_key_secret=cred.access_key_secret, security_token=cred.security_token)\
\
       # 创建凭证提供者，用于动态加载凭证\
       credentials_provider = oss.credentials.CredentialsProviderFunc(func=get_credentials_wrapper)\
\
       # 加载OSS SDK的默认配置\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 填写Bucket所在地域\
       cfg.region = '<region-id>'\
\
       # 创建OSS客户端实例\
       client = oss.Client(cfg)\
\
       # 使用client进行后续操作...\
\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
\
### 使用自定义访问凭证\
\
当以上凭证配置方式不满足要求时，您可以自定义获取凭证的方式。SDK 支持多种实现方式。\
\
1. 通过credentials.CredentialsProviderFunc接口\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
import argparse\
import alibabacloud_oss_v2 as oss\
import os\
\
def main():\
\
       def get_credentials_wrapper():\
           # 返回长期凭证\
           return oss.credentials.Credentials(access_key_id='access_key_id', access_key_secret='access_key_security')\
           # 返回STS临时凭证\
           # return oss.credentials.Credentials(access_key_id='access_key_id', access_key_secret='access_key_security', security_token='security_token')\
\
       credentials_provider = oss.credentials.CredentialsProviderFunc(func=get_credentials_wrapper)\
\
      # 加载SDK的默认配置，并设置凭证提供者\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 填写Bucket所在地域\
       cfg.region = "<region-id>"\
\
       # 使用配置好的信息创建OSS客户端\
       client = oss.Client(cfg)\
\
       # 使用client进行后续操作...\
\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
2. 实现credentials.CredentialsProvider接口\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
# -*- coding: utf-8 -*-\
import alibabacloud_oss_v2 as oss\
\
class CredentialProviderWrapper(oss.credentials.CredentialsProvider):\
       def get_credentials(self):\
           # TODO\
           # 自定义访问凭证的获取方法\
\
           # 返回长期凭证access_key_id, access_key_secrect\
           return oss.credentials.Credentials('<access_key_id>', '<access_key_secrect>')\
\
           # 返回 STS临时凭证access_key_id, access_key_secrect, token\
           # 对于临时凭证，需要根据过期时间，刷新凭证。\
           # return oss.credentials.Credentials('<access_key_id>', '<access_key_secrect>', '<token>');\
\
\
def main():\
       # 创建凭证提供者，用于动态加载凭证\
       credentials_provider = CredentialProviderWrapper()\
\
       # 加载OSS SDK的默认配置\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 填写Bucket所在地域\
       cfg.region = '<region-id>'\
\
       client = oss.Client(cfg)\
\
       # 使用client进行后续操作...\
\
\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
\
### **匿名访问**\
\
如果您只需要访问公共读取权限的OSS资源，可以使用匿名访问方式，无需提供任何凭证。\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
```python\
import alibabacloud_oss_v2 as oss\
\
# 创建匿名凭证提供者\
credentials_provider = oss.credentials.AnonymousCredentialsProvider()\
\
# 配置客户端\
cfg = oss.config.load_default()\
cfg.credentials_provider = credentials_provider\
# 填写Bucket所在地域\
cfg.region = '<region-id>'\
\
# 创建OSS客户端\
client = oss.Client(cfg)\
```\
\
## **错误自助排查**\
\
使用OSS Python SDK V2访问OSS出现错误时，OSS会返回HTTP Code、Message、RequestId、EC错误码等信息，其中EC码对应一个具体的错误原因，您可以使用EC码自助进行错误排查。\
\
1. 例如，当您使用以下代码下载一个并不存在的文件时。\
\
\
> 运行示例代码前，请将代码中的 `<region-id>`占位符替换为实际的 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")，如 `cn-hangzhou`。\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
```python\
import alibabacloud_oss_v2 as oss\
\
def main():\
       # 从环境变量中加载凭证信息，用于身份验证\
       credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()\
\
       # 加载SDK的默认配置，并设置凭证提供者\
       cfg = oss.config.load_default()\
       cfg.credentials_provider = credentials_provider\
\
       # 设置配置中的区域信息\
       cfg.region = '<region-id>'\
\
       # 使用配置好的信息创建OSS客户端\
       client = oss.Client(cfg)\
\
       # 执行获取对象的请求，指定存储空间名称和对象名称\
       result = client.get_object(oss.GetObjectRequest(\
           bucket="Your Bucket Name",  # 指定存储空间名称\
           key="Your Object Key",  # 指定对象键名\
       ))\
\
       # 输出获取对象的结果信息，用于检查请求是否成功\
       print(f'status code: {result.status_code},'\
             f' request id: {result.request_id},'\
       )\
\
       # 使用上下文管理器确保资源释放\
       with result.body as body_stream:\
           data = body_stream.read()\
           print(f"文件读取完成，数据长度：{len(data)} bytes")\
\
           path = "./get-object-sample.txt"\
           with open(path, 'wb') as f:\
               f.write(data)\
           print(f"文件下载完成，保存至路径：{path}")\
\
# 当此脚本被直接运行时，调用main函数\
if __name__ == "__main__":\
       main()  # 脚本入口，当文件被直接运行时调用main函数\
```\
\
2. 返回示例如下，返回结果中包含'EC': '0026-00000001'，作为该错误原因的唯一标识。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0604331471/p925464.png)\
\
3. 通过以上错误请求示例返回的EC错误码查找问题原因及对应解决方法的操作步骤如下。\
\
1. 打开 [OpenAPI问题自助诊断平台](https://api.aliyun.com/troubleshoot?q=&requestId=&product=)。\
\
2. 在搜索框中，输入EC错误码，例如0026-00000001。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4726210471/p918982.png)\
\
3. 在搜索结果中查找问题原因及对应解决方案。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4726210471/p918986.png)\
\
## **示例代码**\
\
OSS Python SDK V2提供丰富的示例代码供参考或直接使用。\
\
| 示例内容 | GitHub示例文件 |\
| --- | --- |\
\
|     |     |\
| --- | --- |\
| 示例内容 | GitHub示例文件 |\
| [创建存储空间（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/create-bucket-using-oss-sdk-for-python-v2 "") | [put\_bucket.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket.py) |\
| [列举存储空间（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/list-buckets-using-oss-sdk-for-python-v2 "") | [list\_buckets.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/list_buckets.py) |\
| [判断存储空间是否存在（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/determine-whether-the-bucket-exists-using-oss-sdk-for-python-v2 "") | [is\_bucket\_exist.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/is_bucket_exist.py) |\
| [获取存储空间的地域（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/query-the-region-of-the-bucket-using-oss-sdk-for-python-v2 "") | [get\_bucket\_location.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_location.py) |\
| [获取存储空间的信息（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/obtain-bucket-information-using-oss-sdk-for-python-v2 "") | [get\_bucket\_info.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_info.py) |\
| [获取存储空间的存储容量（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/query-the-storage-capacity-of-a-bucket-using-oss-sdk-for-python-v2 "") | [get\_bucket\_stat.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_stat.py) |\
| [删除存储空间（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/delete-buckets-using-oss-sdk-for-python-v2 "") | [delete\_bucket.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/delete_bucket.py) |\
| [资源组（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/resource-group-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_resource\_group.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_resource_group.py)<br>  <br>- [get\_bucket\_resource\_group.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_resource_group.py) |\
| [存储空间标签（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/bucket-labels-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_tags.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_tags.py)<br>  <br>- [get\_bucket\_tags.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_tags.py) |\
| [请求者付费模式（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/requester-payment-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_request\_payment.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_request_payment.py)<br>  <br>- [get\_bucket\_request\_payment.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_request_payment.py) |\
| [查询Endpoint信息（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/query-endpoint-information-using-oss-sdk-for-python-v2 "") | [describe\_regions.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/describe_regions.py) |\
| [简单上传（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/simple-upload-using-oss-sdk-for-python-v2 "") | [put\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_object.py) |\
| [追加上传（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/append-upload-using-oss-sdk-for-python-v2 "") | [append\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/append_object.py) |\
| [分片上传（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/multipart-upload-using-oss-sdk-for-python-v2 "") | [complete\_multipart\_upload.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/complete_multipart_upload.py) |\
| [表单上传（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/form-upload-using-oss-sdk-for-python-v2 "") | [post\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/post_object.py) |\
| [使用预签名URL上传（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/upload-an-object-using-a-signed-url-generated-with-oss-sdk-for-python-v2 "") | [presigner\_put\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/presigner_put_object.py) |\
| [文件上传管理器（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/large-file-upload-manager-using-oss-sdk-for-python-v2 "") | [upload\_file.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/upload_file.py) |\
| [简单下载（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/simple-download-using-oss-sdk-for-python-v2 "") | [get\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_object.py) |\
| [范围下载（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/scope-download-using-oss-sdk-for-python-v2 "") | [get\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_object.py) |\
| [类文件只读（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/file-read-only-using-oss-sdk-for-python-v2 "") | [open\_file.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/open_file.py) |\
| [使用预签名URL下载（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/download-an-object-using-a-signed-url-generated-with-oss-sdk-for-python-v2 "") | [presigner\_get\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/presigner_get_object.py) |\
| [文件下载管理器（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/large-file-download-manager-using-oss-sdk-for-python-v2 "") | [download\_file.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/download_file.py) |\
| [拷贝对象（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/copy-object-using-oss-sdk-for-python-v2 "") | [copy\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/copy_object.py) |\
| [分片拷贝（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/fragment-copy-using-oss-sdk-for-python-v2 "") | [upload\_part\_copy.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/upload_part_copy.py) |\
| [文件拷贝管理器（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/file-copy-manager-using-oss-sdk-for-python-v2 "") | [copier.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/copier.py) |\
| [判断文件是否存在（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/determine-whether-the-file-exists-using-oss-sdk-for-python-v2 "") | [is\_object\_exist.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/is_object_exist.py) |\
| [列举文件（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/list-objects-using-oss-sdk-for-python-v2 "") | [list\_objects\_v2.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/list_objects_v2.py) |\
| [删除文件（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/delete-file-using-oss-sdk-for-python-v2 "") | - [delete\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/delete_object.py)<br>  <br>- [delete\_multiple\_objects.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/delete_multiple_objects.py) |\
| [解冻文件（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/restore-file-using-oss-sdk-for-python-v2 "") | - [restore\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/restore_object.py) |\
| [管理文件元数据（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/manage-object-metadata-using-oss-sdk-for-python-v2 "") | - [head\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/head_object.py)<br>  <br>- [get\_object\_meta.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_object_meta.py) |\
| [转换文件存储类型（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/convert-file-storage-type-using-oss-sdk-for-python-v2 "") | [copy\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/copy_object.py) |\
| [重命名文件（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/rename-file-using-oss-sdk-for-python-v2 "") | [copy\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/copy_object.py) |\
| [管理软链接（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/manage-soft-links-using-oss-sdk-for-python-v2 "") | - [put\_symlink.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_symlink.py)<br>  <br>- [get\_symlink.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_symlink.py) |\
| - [设置对象标签（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/set-object-tags-using-oss-sdk-for-python-v2 "")<br>  <br>- [获取对象标签（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/get-object-tags-using-oss-sdk-for-python-v2 "")<br>  <br>- [删除对象标签（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/delete-object-tags-using-oss-sdk-for-python-v2 "") | - [put\_object\_tagging.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_object_tagging.py)<br>  <br>- [get\_object\_tagging.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_object_tagging.py)<br>  <br>- [delete\_object\_tagging.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/delete_object_tagging.py) |\
| [管理存储空间的读写权限（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/manage-bucket-acl-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_acl.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_acl.py)<br>  <br>- [get\_bucket\_acl.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_acl.py) |\
| [管理文件访问权限（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/manage-object-acl-using-oss-sdk-for-python-v2 "") | - [put\_object\_acl.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_object_acl.py)<br>  <br>- [get\_object\_acl.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_object_acl.py) |\
| [Bucket Policy（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/bucket-policy-using-oss-sdk-for-python-v2 "") | [put\_bucket\_policy.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_policy.py) |\
| [管理版本控制（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/manage-versioning-using-oss-sdk-for-python-v2 "") | [put\_bucket\_version.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_version.py) |\
| [防盗链（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/bucket-referer-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_referer.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_referer.py)<br>  <br>- [get\_bucket\_referer.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_referer.py) |\
| [跨域资源共享（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/cross-domain-resource-sharing-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_cors.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_cors.py)<br>  <br>- [get\_bucket\_cors.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_cors.py)<br>  <br>- [delete\_bucket\_cors.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/delete_bucket_cors.py) |\
| [合规保留策略（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/compliance-retention-policy-for-python-sdk-v2 "") | - [initiate\_bucket\_worm.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/initiate_bucket_worm.py)<br>  <br>- [abort\_bucket\_worm.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/abort_bucket_worm.py)<br>  <br>- [complete\_bucket\_worm.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/complete_bucket_worm.py)<br>  <br>- [extend\_bucket\_worm.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/extend_bucket_worm.py) |\
| [服务端加密（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/server-side-encryption-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_encryption.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_encryption.py)<br>  <br>- [get\_bucket\_encryption.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_encryption.py) |\
| [客户端加密（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/client-side-encryption-using-oss-sdk-for-python-v2 "") | - [encryption\_get\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/encryption_get_object.py)<br>  <br>- [encryption\_put\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/encryption_put_object.py) |\
| [数据复制（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/data-replication-using-oss-sdk-for-python-v2 "") | [put\_bucket\_replication.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_replication.py) |\
| [访问跟踪（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/access-monitor-using-oss-sdk-for-python-v2 "") | [put\_bucket\_access\_monitor.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_access_monitor.py) |\
| [生命周期管理（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/lifecycle-management-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_lifecycle.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_lifecycle.py)<br>  <br>- [get\_bucket\_lifecycle.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_lifecycle.py)<br>  <br>- [delete\_bucket\_lifecycle.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/delete_bucket_lifecycle.py) |\
| [存储空间清单（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/bucket-inventory-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_inventory.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_inventory.py)<br>  <br>- [get\_bucket\_inventory.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_inventory.py) |\
| [日志转存（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/bucket-logging-using-oss-sdk-for-python-v2 "") | - [put\_bucket\_logging.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_logging.py)<br>  <br>- [get\_bucket\_logging.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_bucket_logging.py) |\
| [归档直读（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/archive-direct-read-using-oss-sdk-for-python-v2 "") | [put\_bucket\_archive\_direct\_read.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_archive_direct_read.py) |\
| [标量检索（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/data-indexing-using-oss-sdk-for-python-v2 "")<br>[向量索引（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/vector-retrieval-using-oss-sdk-for-python-v2 "") | - [open\_meta\_query.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/open_meta_query.py)<br>  <br>- [do\_meta\_query.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/do_meta_query.py)<br>  <br>- [get\_meta\_query\_status.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_meta_query_status.py)<br>  <br>- [close\_meta\_query.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/close_meta_query.py) |\
\
| [绑定自定义域名（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/bind-custom-domain-using-oss-sdk-for-python-v2 "") | - [create\_cname\_token.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/create_cname_token.py)<br>  <br>- [get\_cname\_token.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/get_cname_token.py)<br>  <br>- [put\_cname.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_cname.py)<br>  <br>- [list\_cname.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/list_cname.py)<br>  <br>- [delete\_cname.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/delete_cname.py) |\
| [传输加速（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/transfer-acceleration-using-oss-sdk-for-python-v2 "") | [put\_bucket\_transfer\_acceleration.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_transfer_acceleration.py) |\
| [同步处理（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/synchronous-processing-using-oss-sdk-for-python-v2 "") | [process\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/process_object.py) |\
| [异步处理（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/asynchronous-processing-using-oss-sdk-for-python-v2 "") | [async\_process\_object.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/async_process_object.py) |\
| [OSS全局阻止公共访问（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/oss-global-block-public-access-using-oss-sdk-for-python-v2 "") | [put\_public\_access\_block.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_public_access_block.py) |\
| [Bucket级别阻止公共访问（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/blocking-public-access-at-the-bucket-level-using-oss-sdk-for-python-v2 "") | [put\_bucket\_public\_access\_block.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_bucket_public_access_block.py) |\
| [接入点级别阻止公共访问（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/access-point-level-block-public-access-using-oss-sdk-for-python-v2 "") | [put\_access\_point\_public\_access\_block.py](https://github.com/aliyun/alibabacloud-oss-python-sdk-v2/blob/master/sample/put_access_point_public_access_block.py) |\
| [资源池QoS管理（Python SDK V2）](https://help.aliyun.com/zh/oss/developer-reference/resource-pool-qos-management-using-oss-sdk-for-python-v2 "") | - |