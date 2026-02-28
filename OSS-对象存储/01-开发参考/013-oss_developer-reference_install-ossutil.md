### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)安装ossutil

# 安装ossutil

更新时间：2025-12-18 04:47:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)[下一篇：配置ossutil](https://help.aliyun.com/zh/oss/developer-reference/configure-ossutil)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

版本升级

版本

下载地址

下载并安装ossutil

相关文档

当您需要快速上传大文件、下载文件、删除固定前缀文件时，可以使用ossutil工具。ossutil支持在Windows、Linux、macOS等系统中运行，您可以根据实际环境下载和安装合适的版本。

## 版本升级

推荐您使用全新升级的 [ossutil2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "")，快速安装并使用，请参见 [安装ossutil](https://help.aliyun.com/zh/oss/install-ossutil2 "")。

ossutil2.0重点功能如下：

- 全新的命令组织结构：引入了多级命令支持，包括API级命令（例如`ossutil api put-bucket-acl`）和高级命令（如`ossutil config`）。

- 改进的配置管理机制：简化了初始配置流程，用户仅需提供AccessKey ID、AccessKey Secret及地域ID即可完成安装后的基础配置，并且支持通过`--profile`参数指定多个配置文件，增强了灵活性。

- 丰富的过滤参数：对于批量处理命令（如`ls`、`cp`、`rm`等），新增了基于路径、文件大小、修改时间以及对象元数据等多种过滤条件的支持，极大地提升了操作的精确性和效率。

- 灵活的输出格式调整：新增`--output-format`参数，允许用户将输出格式设定为JSON、YAML或XML，以便更好地适配不同的数据处理需求；同时引入了`--output-query`选项，让用户能够对输出内容进行筛选，获取所需信息。

- 安全性增强：为了提高安全性，ossutil 2.0支持通过环境变量设置敏感参数，避免在命令行中直接暴露密钥，减少了泄露风险；此外，新增的`--dry-run`选项使用户能够在实际执行命令前验证其行为，确保操作无误。


## 版本

- 当前版本：1.7.19

- 历史版本：关于ossutil各版本源代码以及发布记录的更多信息，请参见 [GitHub](https://github.com/aliyun/ossutil/releases)。


## 下载地址

| **下载地址** | **SHA256校验和** |
| --- | --- |

|     |     |
| --- | --- |
| **下载地址** | **SHA256校验和** |
| [Linux x86 32bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-linux-386.zip) | f8a4a7e1df8529b06a3f3cca194a1c99163cb3b8ab3b5d64228c207c3ae63b86 |
| [Linux x86 64bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-linux-amd64.zip) | dcc512e4a893e16bbee63bc769339d8e56b21744fd83c8212a9d8baf28767343 |
| [Linux ARM 32bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-linux-arm.zip) | ffe8b479e5fd3c0e146a14cd32e8ef5736d23f6c8de157944288ee09db2d7b1d |
| [Linux ARM 64bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-linux-arm64.zip) | f612c2a88d4d28363e254168d521fac5df632f2547ba84eaebacf6497dc04d57 |
| [macOS 64bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-mac-amd64.zip) | 9cf82a53fe24d8b5cc3dfb441787e0ea19c24dd7a1246653d5f1a28b7923d6fe |
| [macOS ARM 64bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-mac-arm64.zip) | 10ece4d328c5d2440833adc5f4167168e9b2a4c5d364f673b0c45bcc4fd02ec5 |
| [Windows x86 32bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-windows-386.zip) | 772469ef02b91e893f7211acf732c2c07cd93214552ed7cf84157d3d9b9fb799 |
| [Windows x86 64bit](https://gosspublic.alicdn.com/ossutil/1.7.19/ossutil-v1.7.19-windows-amd64.zip) | 8e9176aedc87d230ccd97dc7236b16564f2a068609ed301acdc73dc27faf7e77 |

## 下载并安装ossutil

Linux

Windows

macOS

1. 安装ossutil。















```bash
sudo -v ; curl https://gosspublic.alicdn.com/ossutil/install.sh | sudo bash
```





**说明**





   - 安装过程中，需要使用解压工具（unzip、7z）解压软件包，请提前安装其中的一个解压工具。

   - 安装完成后，ossutil会安装到/usr/bin/目录下。


2. 配置ossutil。


1. 输入配置命令。















      ```bash
      ossutil config
      ```

2. 根据提示设置配置文件路径。















      ```bash
      请输入配置文件名，文件名可以带路径（默认为：/home/user/.ossutilconfig，回车将使用默认路径。
      如果用户设置为其它路径，在使用命令时需要将--config-file选项设置为该路径）：
      ```



      ossutil默认使用/home/user/.ossutilconfig作为配置文件，若您设置了配置文件的路径，则每次使用命令时需增加-c选项指定配置文件。例如配置文件保存为/home/config，使用ls时，命令格式如下：















      ```bash
      ossutil ls oss://examplebucket -c /home/config
      ```

3. 根据提示设置工具的语言。请输入语言`CH`或`EN`。工具使用的语言默认与操作系统保持一致。该配置项将在此次config命令设置成功后生效。

4. 根据提示设置工具的语言。

      请输入语言 `CH` 或 `EN`。工具使用的语言默认与操作系统保持一致。该配置项将在此次config命令设置成功后生效。

5. 根据提示分别设置Endpoint、AccessKey ID、AccessKey Secret和STSToken参数。使用STS临时授权账号访问OSS时需要配置STSToken，否则置空跳过即可。

      参数说明如下：


      |     |     |     |
      | --- | --- | --- |
      | **参数** | **是否必填** | **说明** |
      | endpoint | 是 | 填写Bucket所在地域的Endpoint。例如，本示例使用华东1（杭州）的外网Endpoint，设置为`https://oss-cn-hangzhou.aliyuncs.com`。<br>如果您希望通过与OSS同地域的其他阿里云产品访问OSS，请使用内网Endpoint，设置为`https://oss-cn-hangzhou-internal.aliyuncs.com`。<br>关于各地域Endpoint的更多信息，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。 |
      | accessKeyID | 是 | 填写账号的AccessKey，AccessKey的获取方式，请参见 [创建AccessKey](https://help.aliyun.com/zh/ram/create-an-accesskey-pair-1#section-rjh-18m-7kp "")。<br>使用ROS脚本快速创建有OSS管理权限的RAM用户AccessKey<br>在资源编排ROS控制台的 [**创建资源栈**](https://ros.console.aliyun.com/cn-hangzhou/stacks/create?templateUrl=https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241114/itgrlo/createossadmin.yaml&step=1&hideTemplateSelector=false) 页面的 **安全确认** 下，勾选确认，然后单击 **创建**。<br>![1.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1448561371/p873205.png)<br>创建完成后，在 **输出** 中，复制创建的AccessKey。<br>![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2306645471/p948493.png) |
      | accessKeySecret | 是 |
      | stsToken | 否 | 使用STS临时授权账号访问OSS时需要配置该项，否则置空跳过即可。关于stsToken的生成方式，请参见 [AssumeRole - 获取扮演角色的临时身份凭证](https://help.aliyun.com/zh/ram/developer-reference/api-sts-2015-04-01-assumerole "")。 |


3. 验证是否已成功安装ossutil。















```bash
ossutil
```



如果屏幕中输出ossutil所有支持的命令，表明已成功安装ossutil。


1. 安装ossutil。


1. 单击下载链接下载Windows安装包。

2. 将工具解压，并双击运行 _ossutil.bat_ 文件。


2. 配置ossutil。


1. 输入配置命令。















      ```bash
      ossutil config
      ```

2. 根据提示设置配置文件路径。
















      ```bash
      请输入配置文件名，文件名可以带路径（默认为：C:\\Users\user\.ossutilconfig，回车将使用默认路径。
      如果用户设置为其它路径，在使用命令时需要将--config-file选项设置为该路径）：
      ```





      ossutil默认使用C:\\\Users\\user\\.ossutilconfig作为配置文件，若您设置了配置文件的路径，则每次使用命令时需增加-c选项指定配置文件。例如配置文件保存为c:\\ossutil\\config，使用ls时，命令格式如下：

















      ```bash
      ossutil ls oss://examplebucket -c c:\ossutil\config
      ```

3. 根据提示设置工具的语言。请输入语言`CH`或`EN`。工具使用的语言默认与操作系统保持一致。该配置项将在此次config命令设置成功后生效。

4. 根据提示分别设置Endpoint、AccessKey ID、AccessKey Secret和STSToken参数。使用STS临时授权账号访问OSS时需要配置STSToken，否则置空跳过即可。

      参数说明如下：


      |     |     |     |
      | --- | --- | --- |
      | **参数** | **是否必填** | **说明** |
      | endpoint | 是 | 填写Bucket所在地域的Endpoint。例如，本示例使用华东1（杭州）的外网Endpoint，设置为`https://oss-cn-hangzhou.aliyuncs.com`。<br>如果您希望通过与OSS同地域的其他阿里云产品访问OSS，请使用内网Endpoint，设置为`https://oss-cn-hangzhou-internal.aliyuncs.com`。<br>关于各地域Endpoint的更多信息，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。 |
      | accessKeyID | 是 | 填写账号的AccessKey，AccessKey的获取方式，请参见 [创建AccessKey](https://help.aliyun.com/zh/ram/create-an-accesskey-pair-1#section-rjh-18m-7kp "")。<br>使用ROS脚本快速创建有OSS管理权限的RAM用户AccessKey<br>在资源编排ROS控制台的 [**创建资源栈**](https://ros.console.aliyun.com/cn-hangzhou/stacks/create?templateUrl=https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241114/itgrlo/createossadmin.yaml&step=1&hideTemplateSelector=false) 页面的 **安全确认** 下，勾选确认，然后单击 **创建**。<br>![1.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1448561371/p873205.png)<br>创建完成后，在 **输出** 中，复制创建的AccessKey。<br>![1.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7122561371/p872601.png) |
      | accessKeySecret | 是 |
      | stsToken | 否 | 使用STS临时授权账号访问OSS时需要配置该项，否则置空跳过即可。关于stsToken的生成方式，请参见 [AssumeRole - 获取扮演角色的临时身份凭证](https://help.aliyun.com/zh/ram/developer-reference/api-sts-2015-04-01-assumerole "")。 |


3. 验证是否已成功安装ossutil。















```bash
ossutil
```



如果屏幕中输出ossutil所有支持的命令，表明已成功安装ossutil。


1. 安装ossutil。















```bash
sudo -v ; curl https://gosspublic.alicdn.com/ossutil/install.sh | sudo bash
```





**说明**





默认安装到/usr/local/bin目录下。

2. 配置ossutil。


1. 输入配置命令。















      ```bash
      ossutil config
      ```

2. 根据提示设置配置文件路径。
















      ```bash
      请输入配置文件名，文件名可以带路径（默认为：/Users/user/.ossutilconfig，回车将使用默认路径。
      如果用户设置为其它路径，在使用命令时需要将--config-file选项设置为该路径）：
      ```





      ossutil默认使用/Users/user/.ossutilconfig作为配置文件。



      若您设置了配置文件的路径，则每次使用命令时需增加-c选项指定配置文件。例如配置文件保存为/home/config，使用ls时，命令格式如下：

















      ```bash
      ossutil ls oss://examplebucket -c /home/config
      ```

3. 根据提示设置工具的语言。请输入语言`CH`或`EN`。工具使用的语言默认与操作系统保持一致。该配置项将在此次config命令设置成功后生效。

4. 根据提示分别设置Endpoint、AccessKey ID、AccessKey Secret和STSToken参数。使用STS临时授权账号访问OSS时需要配置STSToken，否则置空跳过即可。

      参数说明如下：


      |     |     |     |
      | --- | --- | --- |
      | **参数** | **是否必填** | **说明** |
      | endpoint | 是 | 填写Bucket所在地域的Endpoint。例如，本示例使用华东1（杭州）的外网Endpoint，设置为`https://oss-cn-hangzhou.aliyuncs.com`。<br>如果您希望通过与OSS同地域的其他阿里云产品访问OSS，请使用内网Endpoint，设置为`https://oss-cn-hangzhou-internal.aliyuncs.com`。<br>关于各地域Endpoint的更多信息，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。 |
      | accessKeyID | 是 | 填写账号的AccessKey，AccessKey的获取方式，请参见 [创建AccessKey](https://help.aliyun.com/zh/ram/create-an-accesskey-pair-1#section-rjh-18m-7kp "")。<br>使用ROS脚本快速创建有OSS管理权限的RAM用户AccessKey<br>在资源编排ROS控制台的 [**创建资源栈**](https://ros.console.aliyun.com/cn-hangzhou/stacks/create?templateUrl=https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241114/itgrlo/createossadmin.yaml&step=1&hideTemplateSelector=false) 页面的 **安全确认** 下，勾选确认，然后单击 **创建**。<br>![1.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1448561371/p873205.png)<br>创建完成后，在 **输出** 中，复制创建的AccessKey。<br>![1.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7122561371/p872601.png) |
      | accessKeySecret | 是 |
      | stsToken | 否 | 使用STS临时授权账号访问OSS时需要配置该项，否则置空跳过即可。关于stsToken的生成方式，请参见 [AssumeRole - 获取扮演角色的临时身份凭证](https://help.aliyun.com/zh/ram/developer-reference/api-sts-2015-04-01-assumerole "")。 |


3. 验证是否已成功安装ossutil。















```bash
ossutil
```



如果屏幕中输出ossutil所有支持的命令，表明已成功安装ossutil。


## **相关文档**

安装ossutil成功后，您可以按需上传、下载、拷贝、删除文件等。更多信息，请参见 [cp（上传文件）](https://help.aliyun.com/zh/oss/developer-reference/upload-objects-6 "")、 [cp（下载文件）](https://help.aliyun.com/zh/oss/developer-reference/download-objects-5 "")、 [cp（拷贝文件）](https://help.aliyun.com/zh/oss/developer-reference/copy-objects-4 "") 和 [rm（删除）](https://help.aliyun.com/zh/oss/developer-reference/rm "")。