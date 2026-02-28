### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[命令行工具ossutil 1.0](https://help.aliyun.com/zh/oss/developer-reference/overview-59/)常见问题

# 常见问题

更新时间：2025-03-12 23:15:51

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil)[下一篇：使用OSS Vectors Embed CLI工具写入和检索向量数据](https://help.aliyun.com/zh/oss/developer-reference/use-oss-vectors-embed-cli-to-write-refined-vector-data)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

ossutil支持v4签名么？

低频存储或标准存储的文件是否支持同步文件操作？

如何设置不覆盖同名文件

使用-u参数上传文件时出现skip提示

文件解冻时出现403报错

使用ls命令查看Bucket无文件，删除Bucket时报错

文件上传、下载进度超过100%

使用ossutil发起单个文件的下载请求，但OSS日志里面有多条请求记录

使用ossutil下载文件时，下载任务中断怎么办

使用ossutil执行相关命令时，报错Error: accessKeyID and ecsUrl are both empty

通过ossutil上传的文件的content-type为什么会有charset=utf-8

是否可以通过ossutil查询一个目录的大小

如何生成包含自定义域名的签名URL

ossutil查询文件时，是否支持排序？

使用ossutil执行相关命令时，报错no such host

du命令如何计费

本文介绍在使用ossutil时可能出现的问题及处理方法。

**说明**

从ossutil 1.6.16版本开始，命令行中Binary名称支持直接使用ossutil，您无需根据系统刷新Binary名称。如果您的ossutil版本低于1.6.16，则需要根据系统刷新Binary名称。更多信息，请参见 [命令行工具ossutil命令参考](https://help.aliyun.com/zh/oss/developer-reference/ossutil#task-2012304 "")。

## **ossutil支持v4签名么？**

1.7.12及以上版本支持v4签名。关于v4签名的更多信息，请参见 [签名版本4（推荐）](https://help.aliyun.com/zh/oss/developer-reference/recommend-to-use-signature-version-4 "")。

ossutil在原有命令的基础上，添加--sign-version、--region参数。例如：您可以使用以下命令，创建杭州地域的Bucket。

```bash
./ossutil64 --sign-version v4 --region cn-hangzhou mb oss://examplebucket
```

## 低频存储或标准存储的文件是否支持同步文件操作？

低频存储或标准存储的文件支持同步文件操作。关于同步文件的更多信息，请参见 [简介](https://help.aliyun.com/zh/oss/sync-overview#concept-2105804 "")。

## 如何设置不覆盖同名文件

在ossutil执行命令中增加-u参数，则不会覆盖同名文件。

## 使用-u参数上传文件时出现skip提示

问题分析：使用-u参数上传文件的时候，ossutil会将上传文件和存储空间（Bucket）内已有文件进行一次比对。

若发现上传的文件与目标Bucket内已有文件同名，且该文件的最后修改时间早于或等于Bucket内已有文件，上传时会跳过该文件；若该文件的最后修改时间晚于Bucket内已有文件，则重新上传该文件。所以使用-u参数上传文件时出现skip提示是正常现象。

解决方案：确认Bucket内文件上传无问题后忽略该提示。

## 文件解冻时出现403报错

问题分析：操作解冻文件的过程中出现403，有以下两种可能性。

- 若您是使用RAM用户操作文件，可能是RAM用户权限不足，无目标文件的操作权限。

- 您文件内容违禁OSS被封禁了。


解决方案：

- RAM用户权限不足：增加RAM用户权限。

- 文件内容违禁：删除或忽略该文件。


## 使用ls命令查看Bucket无文件，删除Bucket时报错

问题分析：使用ls命令列举Bucket内的文件且未携带任何选项时，无法列举碎片、历史版本文件（仅存在于开启过版本控制的Bucket）。若Bucket为非空（即Bucket中存在碎片、历史版本文件），仅使用rm命令无法删除该Bucket。

解决方案：

**警告**

Bucket及文件被删除后，无法恢复，请谨慎使用该命令。

- 先删除碎片和历史版本文件（未开启过版本控制请忽略），再删除Bucket。

1. 删除碎片和历史版本文件。

     - 列举并删除碎片：















       ```bash
       ./ossutil64 ls oss://bucket1 -m
       ./ossutil64 rm -m oss://bucket1 -r
       ```

     - 列举并删除历史版本文件：















       ```bash
       ./ossutil64 ls oss://bucket1 --all-versions
       ./ossutil64 rm oss://bucket1 --all-versions -r
       ```
2. 删除Bucket。















     ```bash
     ./ossutil64 rm oss://bucket1 -b
     ```
- 强制删除Bucket。

  - 若存储空间未开启版本控制，使用如下命令强制删除Bucket：















    ```bash
    ./ossutil64 rm oss://bucketname -abrf
    ```

  - 若存储空间已开启版本控制，使用如下命令强制删除Bucket：















    ```bash
    ./ossutil64 rm oss://bucketname -abrf --all-versions
    ```

## 文件上传、下载进度超过100%

问题分析：ossutil在上传、下载文件时，会自动生成一个名为.ossutil\_checkpoint文件夹。当目标文件超过100 MB时，ossutil默认使用断点续传上传或下载目标文件，并将过程中生成的断点信息文件保存在.ossutil\_checkpoint文件夹中。上传、下载任务完成后，会自动删除这个文件夹。若单机运行超过一个ossutil实例，且都在进行上传或下载任务，当其中一个ossutil的任务完成后，会自动删除.ossutil\_checkpoint文件夹，导致其它需要使用断点续传的ossutil任务进度超过100%且无法完成。

解决方案：

- 将当前任务结束，重新开始上传、下载任务。

- 在cp命令中加上--checkpoint-dir参数，并手动指定一个与默认checkpoint文件夹不同名的文件夹。例如：















```bash
./ossutil64 cp oss://bucket1/myphoto.jpg  /dir  --checkpoint-dir checkpoint
```


## 使用ossutil发起单个文件的下载请求，但OSS日志里面有多条请求记录

问题分析：出现该问题有两种可能。

- 请求异常或请求失败时，ossutil会进行重试操作，默认为10次。

- 如果您下载的文件超过100 MB，ossutil会使用range方式去请求，即每次请求该文件的部分内容，通过多次请求完成完整文件的下载。因此，超过100 MB的文件下载时也会产生多条请求记录 。


## 使用ossutil下载文件时，下载任务中断怎么办

1. 文件下载任务中断的场景与影响因素

   - 下载较大文件时，可能出现下载时间过长，任务中断的情况。

     影响因素：网络带宽限制，网络稳定性较差。

   - 下载较大文件时返回EOF错误码，任务中断。

     影响因素：网络中断、磁盘读写速度较慢无法匹配大文件高速下载的数据写入需求。
2. 解决方案：配置断点文件续传。

   - 以cp命令为例，您可以在上传文件时设置断点文件（ **--checkpoint-dir**），指定断点续传所在的目录。















     ```bash
     ./ossutil64 cp examplefile.txt oss://examplebucket/desfolder/ --checkpoint-dir localfolder/
     ```

   - 关于如何设置断点文件（ **--checkpoint-dir**），请参见 [命令格式](https://help.aliyun.com/zh/oss/developer-reference/upload-objects-6#section-mt3-55q-dtk "")。

## 使用ossutil执行相关命令时，报错Error: accessKeyID and ecsUrl are both empty

问题分析：未在home目录下生成配置文件。

解决方案：

- 使用ossutil执行相关命令之前，需在当前用户的home目录下生成配置文件。具体步骤，请参见 [安装ossutil](https://help.aliyun.com/zh/oss/developer-reference/install-ossutil#concept-303829 "")。

- 使用ossutil执行相关命令时单独指定配置文件路径。例如，通过cp命令上传文件时指定配置文件路径：















```bash
./ossutil64 cp examplefile.txt oss://examplebucket/destfolder/ -c /home/admin/.ossutilconfig
```


## 通过ossutil上传的文件的content-type为什么会有charset=utf-8

问题分析：上传文件时，ossutil会根据文件的扩展名，查找关联的MIME类型来设置文件的Content-Type。在查找关联的MIME类型时，会通过Go的标准库MIME的接口查找，该接口对于文本类型的会自动添加`charset=utf-8`，例如，对于.htm扩展名的文件会返回`text/html; charset=utf-8`。

解决方法：请升级到1.7.14及之后的版本。你可以通过重新安装来升级ossutil，具体操作，请参见 [安装ossutil](https://help.aliyun.com/zh/oss/developer-reference/install-ossutil#concept-303829 "")。

## 是否可以通过ossutil查询一个目录的大小

您可以通过du命令查询目录的大小，du命令会通过ListObjects接口获取目录下的所有文件信息，再进行统计。如果该目录下的文件数量很多，需要花费很长时间。

更多信息，请参见 [du（获取大小）](https://help.aliyun.com/zh/oss/developer-reference/du#concept-1614437 "")。

## 如何生成包含自定义域名的签名URL

1. 为Bucket配置自定义域名。

具体操作，请参见 [配置自定义域名](https://help.aliyun.com/zh/oss/developer-reference/configure-ossutil#section-etk-zjk-kug "")。

2. 通过sign命令生成签名URL。

具体操作，请参见 [sign（生成签名URL）](https://help.aliyun.com/zh/oss/developer-reference/sign#concept-303817 "")。


## ossutil查询文件时，是否支持排序？

ossutil在查询文件时，不支持排序。

## 使用ossutil执行相关命令时，报错no such host

问题原因：Endpoint设置不正确。

解决方案：正确设置-e参数，或者将Endpoint放入配置文件中。其中，-e参数指定Bucket对应的Endpoint，例如：`-e oss-cn-shanghai.aliyuncs.com`，Endpoint中请不要添加其他字段。各地域Endpoint详情，请参见 [OSS地域和访问域名](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints#concept-zt4-cvy-5db "")。

## **du命令如何计费**

du命令执行后，如果不开启--all-versions，调用ListObjects接口；如果开启--all-versions，调用ListObjectVersions接口。同时会调用ListMultipartUploads接口，产生对应的请求费用。更多信息，请参见 [请求费用](https://help.aliyun.com/zh/oss/api-operation-calling-fees "")。

**说明**

如果有分片，会额外产生 ListUploadedParts请求。