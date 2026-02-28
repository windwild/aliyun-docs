### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/)bucket-encryption（服务器端加密）

# bucket-encryption（服务器端加密）

更新时间：2025-03-27 04:26:39

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

添加或修改Bucket加密配置

获取Bucket加密配置

删除Bucket加密配置

通用选项

配置服务器端加密（即Bucket加密）后，OSS对上传的文件（Object）进行加密，再将得到的加密文件持久化保存。下载文件时，OSS自动将加密文件解密后返回给用户。本文介绍如何通过 bucket-encryption命令添加、修改、查询和删除Bucket的加密配置。

## 注意事项

- 要添加或修改Bucket加密配置，您必须具有`oss:PutBucketEncryption`权限；要获取Bucket加密配置，您必须具有`oss:GetBucketEncryption`权限；要删除Bucket加密配置，您必须具有`oss:DeleteBucketEncryption`权限。具体操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。


- 从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。

- 关于服务器端加密的更多信息，请参见 [服务器端加密](https://help.aliyun.com/zh/oss/user-guide/server-side-encryption-8#concept-lqm-fkd-5db "")。

- 当您在OSS ON云盒中使用该命令时：



1. 将配置文件中的Endpoint替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

2. 在本文已有示例的基础上添加--sign-version、--region以及--cloudbox-id选项。关于这三个选项的具体用法，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。


## 添加或修改Bucket加密配置

- 命令格式















```bash
ossutil bucket-encryption --method put oss://bucketName  --sse-algorithm algorithmName
[--kms-masterkey-id keyid]
[--kms-data-encryption SM4]
```



参数说明如下：




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| bucketName | 配置服务器端加密的目标Bucket。 |
| --sse-algorithm | Bucket的加密方式。<br>取值：<br>  - KMS：使用KMS托管密钥进行加解密，即SSE-KMS。<br>    <br>  - AES256：使用OSS完全托管密钥进行加解密，即SSE-OSS。<br>    <br>**说明**<br>在OSS ON云盒使用场景中，仅支持AES256。 |
| --kms-masterkey-id | 当加密方式为SSE-KMS时，OSS使用默认托管的KMS CMK进行加密。如果您希望通过指定的KMS CMK进行加密，请通过此选项设置正确的CMK ID。<br>**说明**<br>在OSS ON云盒使用场景中，不支持使用此选项。 |
| --kms-data-encryption | 当加密方式为SSE-KMS时，OSS使用默认加密算法AES256进行加密。如果您希望通过加密算法SM4进行加密，请通过此选项指定。<br>**说明**<br>在OSS ON云盒使用场景中，不支持使用此选项。 |

- 使用示例

  - 将examplebucket的服务器端加密方式设置为SSE-OSS，并指定加密算法为AES256。















    ```bash
    ossutil bucket-encryption --method put oss://examplebucket --sse-algorithm AES256
    ```

  - 将examplebucket的服务器端加密方式设置为SSE-KMS，指定CMK ID，并使用默认加密算法AES256进行加密。















    ```bash
    ossutil bucket-encryption --method put oss://examplebucket --sse-algorithm KMS --kms-masterkey-id 9468da86-3509-4f8d-a61e-6eab1eac****
    ```

  - 将examplebucket的服务器端加密方式设置为SSE-KMS，不指定CMK ID，并使用加密算法SM4进行加密。















    ```bash
    ossutil bucket-encryption --method put oss://examplebucket --sse-algorithm KMS --kms-data-encryption SM4
    ```

  - 以下输出结果表明examplebucket已成功配置服务器端加密。















    ```bash
    0.856895(s) elapsed
    ```

## 获取Bucket加密配置

- 命令格式















```bash
ossutil bucket-encryption --method get oss://bucketname
```

- 使用示例

获取examplebucket的加密配置。命令如下：















```bash
ossutil bucket-encryption --method get oss://examplebucket
```





以下输出结果表明examplebucket配置的服务器端加密方式为SSE-KMS，未指定CMK ID，且加密算法为AES256。

















```bash
SSEAlgorithm:KMS
KMSMasterKeyID:
KMSDataEncryption:
```


## 删除Bucket加密配置

- 命令格式















```bash
ossutil bucket-encryption --method delete oss://bucketname
```

- 使用示例



删除examplebucket的加密配置。命令如下：

















```bash
ossutil bucket-encryption --method delete oss://examplebucket
```





以下输出结果表明已成功删除examplebucket的服务器端加密配置。















```bash
0.856686(s) elapsed
```


## 通用选项

当您需要通过命令行工具ossutil切换至另一个地域的Bucket时，可以通过-e选项指定该Bucket所属的Endpoint。当您需要通过命令行工具ossutil切换至另一个阿里云账号下的Bucket时，可以通过-i选项指定该账号的AccessKey ID，并通过-k选项指定该账号的AccessKey Secret。

例如，您需要为另一个阿里云账号下，华东1（杭州）名为examplebucket的存储空间配置AES256的加密方式，命令如下：

```plaintext
ossutil bucket-encryption --method put oss://examplebucket --sse-algorithm AES256 -e oss-cn-hangzhou.aliyuncs.com -i yourAccessKeyID -k yourAccessKeySecret
```

关于此命令的其他通用选项的更多信息，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。