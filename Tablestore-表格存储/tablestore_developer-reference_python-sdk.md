### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)Python SDK

# Python SDK

更新时间：2026-01-06 20:40:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速接入

准备环境

安装SDK

配置访问凭证

初始化客户端

版本兼容性

常见问题

相关文档

表格存储 Python SDK 支持宽表模型和时序模型操作。

## **快速接入**

通过以下步骤快速接入表格存储 Python SDK，完成从环境准备到客户端验证的完整流程。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1500577671/CAEQYxiBgMCZ.bur0RkiIGQ2MTExODNjMjZkYTQ1YzRiOTRmNzg4OWU0MzdmYjBm5832293_20251028163056.914.svg)

### **准备环境**

下载并安装 [Python](https://www.python.org/downloads/) 运行环境，通过 `python3 --version` 命令查看Python版本信息。

> Python SDK 从 6.0.0 版本开始仅支持 Python 3，不再支持 Python 2。如需使用 Python 2，请选择 5.4.4 及之前的版本。

### **安装SDK**

根据开发环境选择合适的安装方式。推荐使用最新版本的SDK，确保代码示例正常运行。

通过pip安装（推荐）

通过Github安装

通过源码安装

执行以下命令安装表格存储 Python SDK。

```bash
pip3 install tablestore
```

通过 `git` 命令从 GitHub 下载表格存储 SDK 后进行安装。

1. 执行以下命令下载SDK。















```bash
git clone https://github.com/aliyun/aliyun-tablestore-python-sdk.git
```

2. 执行以下命令进入SDK安装包目录。















```bash
cd aliyun-tablestore-python-sdk
```

3. 执行以下命令安装SDK。















```bash
python3 setup.py install
```


下载SDK源码后进行安装。

1. 下载 [Python SDK](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-sdk-for-python "") 并解压。

2. 进入SDK包解压目录。

3. 执行以下命令进行SDK安装。















```bash
python3 setup.py install
```


### **配置访问凭证**

为阿里云账号或RAM用户 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "")，并按如下方式将AccessKey配置到环境变量中。通过环境变量配置AccessKey可避免在代码中硬编码敏感信息，提升安全性。

> 配置完成后请重启或刷新编译运行环境，包括IDE、命令行界面、其它桌面应用程序及后台服务，确保最新的系统环境变量成功加载。更多访问凭证类型，请参见 [配置访问凭证](https://help.aliyun.com/zh/tablestore/developer-reference/access-credential-configuration "")。

Linux

macOS

Windows

1. 在命令行界面执行以下命令来将环境变量设置追加到 `~/.bashrc` 文件中。















```bash
echo "export TABLESTORE_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.bashrc
echo "export TABLESTORE_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.bashrc
```

2. 执行以下命令使变更生效。















```bash
source ~/.bashrc
```

3. 执行以下命令检查环境变量是否生效。















```bash
echo $TABLESTORE_ACCESS_KEY_ID
echo $TABLESTORE_ACCESS_KEY_SECRET
```


1. 在终端中执行以下命令，查看默认 Shell 类型。















```bash
echo $SHELL
```

2. 根据默认 Shell 类型进行操作。






Zsh



Bash



















1. 执行以下命令来将环境变量设置追加到 `~/.zshrc` 文件中。















      ```bash
      echo "export TABLESTORE_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.zshrc
      echo "export TABLESTORE_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.zshrc
      ```

2. 执行以下命令使变更生效。















      ```bash
      source ~/.zshrc
      ```

3. 执行以下命令检查环境变量是否生效。















      ```bash
      echo $TABLESTORE_ACCESS_KEY_ID
      echo $TABLESTORE_ACCESS_KEY_SECRET
      ```


1. 执行以下命令来将环境变量设置追加到 `~/.bash_profile` 文件中。















      ```bash
      echo "export TABLESTORE_ACCESS_KEY_ID='YOUR_ACCESS_KEY_ID'" >> ~/.bash_profile
      echo "export TABLESTORE_ACCESS_KEY_SECRET='YOUR_ACCESS_KEY_SECRET'" >> ~/.bash_profile
      ```

2. 执行以下命令使变更生效。















      ```bash
      source ~/.bash_profile
      ```

3. 执行以下命令检查环境变量是否生效。















      ```bash
      echo $TABLESTORE_ACCESS_KEY_ID
      echo $TABLESTORE_ACCESS_KEY_SECRET
      ```


CMD

PowerShell

1. 在CMD中运行以下命令设置环境变量。















```bash
setx TABLESTORE_ACCESS_KEY_ID "YOUR_ACCESS_KEY_ID"
setx TABLESTORE_ACCESS_KEY_SECRET "YOUR_ACCESS_KEY_SECRET"
```

2. 重启CMD后，运行以下命令，检查环境变量是否生效。















```bash
echo %TABLESTORE_ACCESS_KEY_ID%
echo %TABLESTORE_ACCESS_KEY_SECRET%
```


1. 在PowerShell中运行以下命令。















```powershell
[Environment]::SetEnvironmentVariable("TABLESTORE_ACCESS_KEY_ID", "YOUR_ACCESS_KEY_ID", [EnvironmentVariableTarget]::User)
[Environment]::SetEnvironmentVariable("TABLESTORE_ACCESS_KEY_SECRET", "YOUR_ACCESS_KEY_SECRET", [EnvironmentVariableTarget]::User)
```

2. 运行以下命令，检查环境变量是否生效。















```powershell
[Environment]::GetEnvironmentVariable("TABLESTORE_ACCESS_KEY_ID", [EnvironmentVariableTarget]::User)
[Environment]::GetEnvironmentVariable("TABLESTORE_ACCESS_KEY_SECRET", [EnvironmentVariableTarget]::User)
```


### **初始化客户端**

以下示例代码初始化客户端，并通过列举表格存储实例下的数据表和时序表进行连接验证。

**重要**

新创建的实例默认未启用公网访问功能。如果需要通过公网访问实例中的资源，请在实例的 **网络管理** 中设置允许公网访问。

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import os
import sys
from tablestore import OTSClient

def main():
    try:
        # 从环境变量中获取访问凭证（需要配置TABLESTORE_ACCESS_KEY_ID和TABLESTORE_ACCESS_KEY_SECRET）
        access_key_id = os.getenv("TABLESTORE_ACCESS_KEY_ID")
        access_key_secret = os.getenv("TABLESTORE_ACCESS_KEY_SECRET")

        # TODO: 根据实例信息修改以下配置
        instance_name = "n01k********"  # 填写实例名称
        endpoint = "https://n01k********.cn-hangzhou.ots.aliyuncs.com"  # 填写实例访问地址

        # 创建客户端实例
        client = OTSClient(endpoint, access_key_id, access_key_secret, instance_name)

        # 列举数据表
        resp = client.list_table()

        print(f"在实例 '{instance_name}' 中共找到 {len(resp)} 个数据表:")
        for table_name in resp:
            print(f"{table_name}")

        # 列举时序表
        resp = client.list_timeseries_table()

        print(f"\n在实例 '{instance_name}' 中共找到 {len(resp)} 个时序表:")
        for tableMeta in resp:
            print(f"{tableMeta.timeseries_table_name}")

    except Exception as e:
        print(f"操作失败: {str(e)}")
        sys.exit(1)

if __name__ == "__main__":
    main()
```

## **版本兼容性**

当前最新版本为6.x.x版本，新版本对历史版本的兼容性如下：

- 对5.x.x系列的SDK兼容。

5.4.x版本、5.3.x版本和5.2.x版本兼容。5.2.1 和 5.1.0 在以下情况不兼容：

  - `Search`接口返回结果的类型。

    5.1.0 及以前版本的返回结果默认为 `Tuple` 类型。从 5.2.0 开始默认返回结果为 `SearchResponse` 对象，`SearchResponse` 已实现 `__iter__` 方法，支持遍历；如需返回 `Tuple` 类型的结果，请使用 `SearchResponse.v1_response()` 方法实现。

  - 新增`ParallelScan`接口。

    默认返回结果为 `ParallelScanResponse` 对象。如需返回 `Tuple` 类型的结果，请使用 `ParallelScanResponse.v1_response()` 方法实现。
- 对4.x.x系列的SDK兼容。

- 对2.x.x系列的SDK不兼容，原因是 2.0 系列版本中支持主键乱序，而 4.0.0 版本开始不允许主键乱序，涉及的不兼容点包括：

  - 包名称由 `ots2` 变更为 `tablestore`。

  - `Client.create_table` 接口新增 `TableOptions` 参数。

  - `put_row`、`get_row`、`update_row` 等接口的 `primary_key` 参数由 `dict` 类型变更为 `list` 类型，目的是保证主键的顺序性。

  - `put_row`、`update_row` 等接口的 `attribute_columns` 参数由 `dict` 类型变更为 `list` 类型。

  - `put_row`、`update_row` 等接口的 `attribute_columns` 参数新增 `timestamp`。

  - `get_row`、`get_range` 等接口新增 `max_version、time_range` 参数，这两个参数必须至少存在一个。

  - `put_row`、`update_row`、`delete_row` 等接口新增 `return_type` 参数，目前仅支持 `RT_PK`，表示返回值中包含当前行 `PK` 值。

  - `put_row`、`update_row`、`delete_row` 等接口返回值中新增 `return_row`，如果在请求中指定了 `return_type` 为 `RT_PK`，则 `return_row` 中包含此行的 `PK` 值。

## **常见问题**

#### **使用SDK时出现Signature mismatch异常？**

使用SDK进行功能操作时出现如下异常：

```plaintext
Error Code: OTSAuthFailed, Message: Signature mismatch., RequestId: 0005f55a-xxxx-xxxx-xxxx-xxxxxxxxxxxx, TraceId: 10b0f0e0-xxxx-xxxx-xxxx-xxxxxxxxxxxx, HttpStatus: 403
```

- **问题原因**：初始化客户端时设置的AccessKey ID或者AccessKey Secret不匹配。

- **解决方案**：填写正确的AccessKey（包括AccessKey ID及AccessKey Secret）。


#### **使用SDK时出现Request denied by instance ACL policies异常？**

使用SDK访问表格存储实例中的资源时出现`Request denied by instance ACL policies`异常。报错示例如下：

```plaintext
[ErrorCode]:OTSAuthFailed, [Message]:Request denied by instance ACL policies., [RequestId]:XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, [TraceId]:XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, [HttpStatus:]403
```

- **问题原因**：客户端所用的网络类型不符合实例的网络访问要求。例如客户端所用的网络类型为公网，但实例未设置允许通过公网进行访问。

- **解决方案**：新创建的实例默认未开启公网访问功能，如果要使用公网访问实例中的资源，可按以下步骤开启公网访问。

1. 前往 [表格存储控制台](https://otsnext.console.aliyun.com/)，单击实例别名。

2. 单击 **网络管理**， **允许网络类型** 勾选 **公网**，然后单击 **设置**。

#### **使用SDK时出现Request denied because this instance can only be accessed from the binded VPC异常？**

使用SDK访问表格存储实例中的资源时出现`Request denied because this instance can only be accessed from the binded VPC`异常。报错示例如下：

```plaintext
[ErrorCode]:OTSAuthFailed, [Message]:Request denied because this instance can only be accessed from the binded VPC., [RequestId]:XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, [TraceId]:XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, [HttpStatus:]403
```

- **问题原因**：在设置表格存储实例的访问类型为 **限定绑定VPC访问** 或 **限定控制台或绑定VPC访问** 后，需要为该实例绑定VPC，并且确保实例与客户端位于同一VPC中，通过VPC地址访问表格存储。

- **解决方案**：修改实例的访问类型支持公网访问，或者将VPC绑定到表格存储实例并确保客户端位于该VPC网络下。VPC绑定方式：

1. 前往 [表格存储控制台](https://otsnext.console.aliyun.com/)，单击实例别名。

2. 单击**网络管理** \> **绑定VPC**，选择 **VPC** 和 **交换机**，并填写 **VPC名称**，然后单击 **确定**。

#### **如何使用** HTTPS协议访问表格存储资源？

使用最新版本的Python SDK，并且确保OpenSSL版本最少为0.9.8j，推荐OpenSSL 1.0.2d。

#### **部分protobuf版本不兼容？**

部分protobuf版本无法和当前安装包中的`*pb2.py`文件兼容，可以通过手动生成`*pb2.py`文件的方式尝试解决。具体操作如下：

1. 使用自己当前版本的protoc依次生成对应proto文件的代码。















```bash
protoc --python_out=. tablestore/protobuf/search.proto
protoc --python_out=. tablestore/protobuf/table_store.proto
protoc --python_out=. tablestore/protobuf/table_store_filter.proto
```

2. 将生成的3个文件更名为`pb2.py`后缀，然后拷贝文件到安装目录下的`tablestore/protobuf/`目录中，替换掉原有的`*pb2.py`文件。


#### **如何使用Credentials工具读取访问凭证？**

1. 执行以下命令安装alibabacloud\_credentials包。















```bash
pip3 install alibabacloud_credentials
```

2. 配置环境变量。

配置环境变量`ALIBABA_CLOUD_ACCESS_KEY_ID`和`ALIBABA_CLOUD_ACCESS_KEY_SECRET`，分别代表阿里云账号的AccessKey ID和AccessKey Secret。

3. 读取访问凭证。

以下示例代码使用Credentials工具读取环境变量的访问凭证。















```python
# -*- coding: utf-8 -*-
from alibabacloud_credentials.client import Client as CredClient

# 使用 CredClient 获取环境变量里的 AccessKey ID 和 AccessKey Secret
cred = CredClient()
access_key_id = cred.get_credential().access_key_id
access_key_secret = cred.get_credential().access_key_secret
```


## **相关文档**

- [错误处理](https://help.aliyun.com/zh/tablestore/developer-reference/error-handling-of-tablestore-python-sdk "")