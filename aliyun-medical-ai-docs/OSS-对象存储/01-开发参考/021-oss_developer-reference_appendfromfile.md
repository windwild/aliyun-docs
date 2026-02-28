### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/)appendfromfile（追加上传）

# appendfromfile（追加上传）

更新时间：2025-03-27 04:27:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：access-monitor（访问跟踪）](https://help.aliyun.com/zh/oss/developer-reference/access-monitor)[下一篇：bucket-cname（自定义域名）](https://help.aliyun.com/zh/oss/developer-reference/bucket-cname)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

命令格式

使用示例

通用选项

appendfromfile命令用于在已上传的追加类型文件（Appendable Object）末尾直接追加内容。

## 注意事项

- 要追加上传，您必须具有`oss:GetObject`和`oss:PutObject`权限。具体操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

- 从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。


- 关于追加上传的更多信息，请参见 [追加上传](https://help.aliyun.com/zh/oss/user-guide/append-upload-11#concept-ls5-yhb-5db "")。

- 当您在OSS ON云盒中使用该命令时：



1. 将配置文件中的Endpoint替换为云盒Endpoint。更多信息，请参见 [云盒Endpoint](https://help.aliyun.com/zh/oss/user-guide/oss-deployed-in-cloudbox-overview#section-y34-bhr-ijj "")。

2. 在本文已有示例的基础上添加--sign-version、--region以及--cloudbox-id选项。关于这三个选项的具体用法，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。


## 命令格式

```bash
ossutil appendfromfile localfilename oss://bucketname/objectname
[--meta <value>]
```

参数说明如下：

| **选项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **选项** | **说明** |
| localfilename | 本地文件完整路径。 |
| bucketname | 目标Bucket名称。 |
| objectname | 目标Object名称。追加上传时可直接将本地文件名称保留为Object名称，也可以自定义上传至Bucket后的Object名称。 |
| --meta | 设置Object的meta信息。仅支持在首次追加上传时附加此选项，例如`--meta "x-oss-object-acl:private"`。<br>Object的meta信息配置完成后，您可以通过 [set-meta（管理文件元数据）](https://help.aliyun.com/zh/oss/developer-reference/set-meta#concept-303809 "") 命令修改Object的meta信息。 |

## 使用示例

将本地根目录下的文件exampleobject.txt首次追加上传至目标存储空间examplebucket，然后直接在exampleobject.txt文件末尾多次追加内容。

1. 上传文件exampleobject.txt，并指定文件读写权限为私有。















```bash
ossutil appendfromfile exampleobject.txt oss://examplebucket/exampleobject.txt --meta "x-oss-object-acl:private"
```



以下输出结果表明exampleobject.txt已追加上传至目标Bucket，此时文件大小为5 Byte。















```bash
total append 5(100.00%) byte,speed is 0.00(KB/s)
local file size is 5,the object new size is 5,average speed is 0.04(KB/s)
```

2. 在exampleobject.txt文件末尾追加文件dest.txt的内容。

如果需要在exampleobject.txt文件末尾多次追加内容，请相应替换如下示例中的待追加上传文件dest.txt。















```bash
ossutil appendfromfile dest.txt oss://examplebucket/exampleobject.txt
```



以下输出结果已在exampleobject.txt文件后追加了内容，此时文件大小为150 Byte。















```bash
total append 150(100.00%) byte,speed is 0.00(KB/s)
local file size is 150,the object new size is 150,average speed is 1.19(KB/s)
```


## 通用选项

当您需要通过命令行工具ossutil切换至另一个地域的Bucket时，可以通过-e选项指定该Bucket所属的Endpoint。当您需要通过命令行工具ossutil切换至另一个阿里云账号下的Bucket时，可以通过-i选项指定该账号的AccessKey ID，并通过-k选项指定该账号的AccessKey Secret。

例如，您需要向另一个阿里云账号下，华东2（上海）下名为examplebucket的存储空间追加上传exampleobject.txt文件，示例如下：

```bash
ossutil appendfromfile exampleobject.txt oss://examplebucket/exampleobject.txt -e shanghai.aliyuncs.com -i yourAccessKeyID -k yourAccessKeySecret
```

关于此命令的其他通用选项的更多信息，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。