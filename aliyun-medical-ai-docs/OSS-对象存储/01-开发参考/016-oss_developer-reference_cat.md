### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[常用命令](https://help.aliyun.com/zh/oss/developer-reference/common-commands/)cat（输出文件内容）

# cat（输出文件内容）

更新时间：2025-03-27 04:27:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

注意事项

命令格式

使用示例

通用选项

cat命令仅支持将存储空间（Bucket）内文件（Object）的内容输出到屏幕。

## **注意事项**

- 要输出文件内容，您必须具有`oss:GetObject`权限。具体操作，请参见 [为RAM用户授权自定义的权限策略](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#section-ucu-jv0-zip "")。

- 从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。


## 命令格式

```bash
ossutil cat oss://bucketname/objectname [--payer <value>] [--version-id <value>]
```

**重要**

仅建议使用此命令查看文本文件内容。

参数及选项说明如下：

| **配置项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **配置项** | **说明** |
| bucketname | Bucket名称。 |
| objectname | Object名称。 |
| --payer | 请求的支付方式。如果希望访问指定路径下的资源产生的流量、请求次数等费用由请求者支付，请将此选项的值设置为requester。 |
| --version-id | Object的指定版本。仅适用于已开启或暂停版本控制状态Bucket下的Object。 |

## 使用示例

- 将未开启版本控制的目标存储空间examplebucket内名为test.txt的文件内容输出到屏幕















```bash
ossutil cat oss://examplebucket/test.txt
```



以下输出结果表明test.txt文件包含的信息，以及完成输出操作所用时长。















```bash
My Website Home Page.

0.088092(s) elapsed
```

- 将已开启版本控制的目标存储空间examplebucket内名为exampleobject.txt文件的指定版本内容输出到屏幕















```bash
ossutil cat oss://examplebucket/exampleobject.txt --version-id  CAEQARiBgID8rumR2hYiIGUyOTAyZGY2MzU5MjQ5ZjlhYzQzZjNlYTAyZDE3****
```



有关获取Object所有版本的具体操作，请参见 [ls命令](https://help.aliyun.com/zh/oss/developer-reference/ls#concept-303804 "")。

以下输出结果表明指定版本的exampleobject.txt文件包含的信息，以及完成输出操作所用时长。















```bash
Hello World.

0.044820(s) elapsed
```


## 通用选项

当您需要通过命令行工具ossutil切换至另一个地域的Bucket时，可以通过-e选项指定该Bucket所属的Endpoint。当您需要通过命令行工具ossutil切换至另一个阿里云账号下的Bucket时，可以通过-i选项指定该账号的AccessKey ID，并通过-k选项指定该账号的AccessKey Secret。

例如您需要查看另一个阿里云账号下，华东2（上海）地域下目标存储空间examplebucket1下名为exampleobject1.txt文件内容，命令如下：

```plaintext
ossutil cat oss://examplebucket1/exampleobject1.txt -e oss-cn-shanghai.aliyuncs.com -i yourAccessKeyID -k yourAccessKeySecret
```

关于此命令的其他通用选项的更多信息，请参见 [通用选项](https://help.aliyun.com/zh/oss/developer-reference/view-options#section-yhn-ko6-gqj "")。