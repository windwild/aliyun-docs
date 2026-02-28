### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/)bucket-versioning（版本控制）

# bucket-versioning（版本控制）

更新时间：2025-03-27 04:26:30

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：bucket-tagging（存储空间标签）](https://help.aliyun.com/zh/oss/developer-reference/bucket-tagging)[下一篇：cat（输出文件内容）](https://help.aliyun.com/zh/oss/developer-reference/cat)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

设置版本控制状态

获取版本控制状态

相关操作

通用选项

如果您希望在错误覆盖或者删除对象（Object）后，能够将Object恢复至任意时刻的历史版本。您需要通过bucket-versioning命令开启版本控制。版本控制是针对Bucket级别的数据保护功能。开启版本控制后，针对数据的覆盖和删除操作将会以历史版本的形式保存下来。

## 注意事项

- 要设置版本控制状态，您必须具有`oss:PutBucketVersioning`权限；要获取版本控制状态，您必须具有`oss:GetBucketVersioning`权限。具体操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。


- 从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。

- 关于版本控制的功能详情，请参见 [版本控制](https://help.aliyun.com/zh/oss/user-guide/overview-78/#concept-jdg-4rx-bgb "")。

- 当您在OSS ON云盒中使用该命令时：



1. 将配置文件中的Endpoint替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

2. 在本文已有示例的基础上添加--sign-version、--region以及--cloudbox-id选项。关于这三个选项的具体用法，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。


## 设置版本控制状态

- 命令格式















```bash
ossutil bucket-versioning --method put oss://bucketname versioning
```



参数说明如下：




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| bucketname | 待设置版本控制状态的目标Bucket名称。 |
| versioning | 为目标Bucket设置版本控制状态。取值如下：<br>  - enabled：开启版本控制。当Bucket处于开启版本控制状态时，OSS将为新上传的Object生成全局唯一的随机字符串版本ID。有关启用版本控制状态下Object相关操作的更多信息，请参见 [开启版本控制下Object的操作](https://help.aliyun.com/zh/oss/user-guide/manage-objects-in-a-versioning-enabled-bucket#concept-xw4-bxs-zgb "")。<br>    <br>  - suspended：暂停版本控制。当Bucket处于暂停版本控制状态时，OSS将为新上传的Object生成特殊字符串为“null”的版本ID。有关暂停版本控制状态下Object的相关操作的更多信息，请参见 [暂停版本控制下Object的操作](https://help.aliyun.com/zh/oss/user-guide/manage-objects-in-a-versioning-suspended-bucket#concept-anp-wvq-dgb "")。<br>    <br>**重要**<br>默认情况下，Bucket版本控制状态为“未开启”。一旦Bucket开启了版本控制，将无法返回至“未开启”状态。但是，您可以暂停Bucket版本控制。 |

- 使用示例



对目标存储空间examplebucket开启版本控制。

















```bash
ossutil bucket-versioning --method put oss://examplebucket enabled
```





对目标存储空间examplebucket暂停版本控制。















```bash
ossutil bucket-versioning --method put oss://examplebucket suspended
```



以下输出结果表明examplebucket已成功设置版本控制状态。















```bash
0.261209(s) elapsed
```


## 获取版本控制状态

- 命令格式















```bash
ossutil bucket-versioning --method get oss://bucketname
```

- 使用示例

查询examplebucket的版本控制状态。















```bash
ossutil bucket-versioning --method get oss://examplebucket
```



以下输出结果表明examplebucket已开启版本控制。















```bash
bucket versioning status:Enabled

0.218001(s) elapsed
```



以下输出结果表明examplebucket已暂停版本控制。















```bash
bucket versioning status:Suspended

0.168791(s) elapsed
```



以下输出结果表明examplebucket未开启版本控制。















```bash
bucket versioning status:Null

0.158691(s) elapsed
```


## 相关操作

- 在开启版本控制的Bucket中上传文件的行为与未开启版本控制状态下的上传行为一致。但Bucket开启版本控制后，OSS会为新上传至Bucket的Object生成全局唯一的versionID。详情请参见 [cp（上传文件）](https://help.aliyun.com/zh/oss/developer-reference/upload-objects-6#concept-1937458 "")。

- 开启Bucket的版本控制后，针对数据的覆盖和删除操作将会以历史版本的形式保存下来。您可以通过指定versionID的方式下载指定版本Object，详情请参见 [cp（下载文件）](https://help.aliyun.com/zh/oss/developer-reference/download-objects-5#concept-1937459 "")。您还可以通过指定versionID的方式将Object恢复至任意时刻的历史版本，详情请参见 [cp（拷贝文件）](https://help.aliyun.com/zh/oss/developer-reference/copy-objects-4#concept-1937460 "")。


## 通用选项

当您需要通过命令行工具ossutil切换至另一个地域的Bucket时，可以通过-e选项指定该Bucket所属的Endpoint。当您需要通过命令行工具ossutil切换至另一个阿里云账号下的Bucket时，可以通过-i选项指定该账号的AccessKey ID，并通过-k选项指定该账号的AccessKey Secret。

例如您需要为另一个阿里云账号下，华东1（杭州）名为examplebucket的存储空间开启版本控制，命令如下：

```plaintext
ossutil bucket-versioning--method put oss://examplebucket enabled -e oss-cn-hangzhou.aliyuncs.com -i yourAccessKeyID -k yourAccessKeySecret
```

关于此命令的其他通用选项的更多信息，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。