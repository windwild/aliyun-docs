### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[图形化管理工具ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/graphical-management-tools-ossbrowser-1-0/)常用操作

# ossbrowser 1.0常用操作

更新时间：2025-12-09 04:25:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

使用场景

管理Bucket

管理Object

ossbrowser是阿里云官方提供的OSS图形化管理工具，帮助您快速管理Bucket和文件，例如创建、删除Bucket，上传、下载、预览、复制、移动、分享文件等。

## 前提条件

已 [安装ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/install-ossbrowser-1-0#task-2065478 "") 并 [登录ossbrowser 1.0](https://help.aliyun.com/zh/oss/developer-reference/logon-to-ossbrowser-1-0#9ba38e7d178j4 "")。

## **使用场景**

- 大文件（超过5 GB）的传输和下载。

ossbrowser默认使用分片上传和断点续传上传文件，上传文件最大不能超过48.8 TB。文件上传的过程中，ossbrowser自动进行分片，上传完成后合并成一个文件。

- 通过授权码访问Bucket中的某个目录。

ossbrowser支持临时授权码登录。您可以将临时授权码提供给相应的人员，允许其在授权码到期前，临时访问您Bucket下某个目录。到期后，临时授权码会自动失效。


**说明**

本文操作以列表视图为准。您也可以单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7237904171/p794978.png)图标切换到平铺视图进行操作。

## **管理Bucket**

ossbrowser支持的Bucket级别的操作与控制台支持的操作类似，请按照ossbrowser界面指引完成Bucket相关操作。

**说明**

要进行Bucket相关操作，您需要具备相应权限。更多信息，请参见 [权限管理](https://help.aliyun.com/zh/oss/developer-reference/permission-management-1#concept-c3k-mvr-gfb "")。

| **操作** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **操作** | **说明** |
| 创建Bucket | Bucket是您用于存储Object的容器。在上传任何文件到OSS之前，您必须先创建存储空间。有关创建Bucket时如何填写Bucket名称、选择所在地域、ACL权限和存储类型信息，请参见 [创建存储空间](https://help.aliyun.com/zh/oss/user-guide/create-a-bucket-4 "")。 |
| 列举Bucket | 登录ossbrowser后，将自动列举Bucket。 |
| 删除Bucket | 如果您不再需要Bucket，请将其删除，以免产生额外费用。有关删除Bucket的注意事项，请参见 [删除存储空间](https://help.aliyun.com/zh/oss/user-guide/delete-buckets "")。 |
| 获取存储空间的地域信息 | 单击Bucket名称，然后在界面右上角查看地域信息（地域ID）。例如：oss-cn-hangzhou表示华东1（杭州）。<br>关于地域ID和具体地域的对应关系，请参见 [地域和Endpoint](https://help.aliyun.com/zh/oss/user-guide/regions-and-endpoints "")。 |

## 管理Object

ossbrowser支持的Object级别的操作与控制台支持的操作类似，请按照ossbrowser界面指引完成Object相关操作。管理Object前，您需要先单击Bucket名称，进入文件列表页面。

**说明**

- 要进行Object相关操作，您需要具备相应权限。更多信息，请参见 [权限管理](https://help.aliyun.com/zh/oss/developer-reference/permission-management-1#concept-c3k-mvr-gfb "")。

- Object各类操作的注意事项，请参见控制台用户指南对应文档。


| 操作 | 说明 |
| --- | --- |

|     |     |
| --- | --- |
| 操作 | 说明 |
| 上传文件 | ossbrowser默认使用分片上传和断点续传上传文件，上传文件最大不能超过48.8 TB。若您因意外中断了文件上传的过程，且未继续完成该文件的上传，则已上传的部分会以碎片（Part）的形式存储在OSS的存储空间（Bucket）中。若您不再需要这些Part，建议您通过以下方式删除，以免产生额外的存储费用。<br>- 手动删除Part的具体操作，请参见 [删除碎片](https://help.aliyun.com/zh/oss/user-guide/delete-parts#concept-r3h-c1y-5db "")。<br>  <br>- 通过生命周期规则自动删除Part的具体操作，请参见 [基于最后一次修改时间的生命周期规则](https://help.aliyun.com/zh/oss/user-guide/lifecycle-rules-based-on-the-last-modified-time "")。<br>  <br>**重要**<br>如果上传的文件与Bucket中已有的文件重名，则覆盖已有文件。 |
| 上传文件夹 | 单击页面上方![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8347701071/p742274.png)图标，上传文件夹。 |
| 下载文件 | 选中文件，然后单击操作列的 **下载** 进行下载。<br>**说明**<br>您也可以选中多个文件，然后单击页面上方的 **下载** 进行批量下载。 |
| 下载文件夹 | 选中文件夹，然后单击页面上方![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8347701071/p742278.png)图标进行下载。 |
| 列举文件 | 单击Bucket名称后，直接列举Object信息。 |
| 预览文件 | 直接单击文件名称进行预览。 |
| 拷贝文件 | 在Bucket1选中文件单击 **复制**，然后在Bucket2单击 **粘贴**。<br>**重要**<br>- 复制文件最大不能超过5 GB，5 GB以上文件的复制操作建议使用 [ossutil](https://help.aliyun.com/zh/oss/developer-reference/overview-59/#concept-cnr-3d4-vdb "")。<br>  <br>- 批量拷贝文件时，如果由于意外情况导致操作中断，则工具无法恢复执行。 |
| 移动文件 | 选中 **更多** > **移动** 进行操作。<br>**重要**<br>移动操作通过先将源文件复制到目标地址，再删除源文件的方式实现。操作注意事项如下：<br>- 移动文件最大不能超过5 GB，5 GB以上文件的移动操作建议使用 [ossutil](https://help.aliyun.com/zh/oss/developer-reference/overview-59/#concept-cnr-3d4-vdb "") 复制后再删除源文件。<br>  <br>- 在移动文件过程中，如果复制失败，则源文件不会被删除。如果复制成功但后续删除源文件失败（例如无权限），则源文件和目标文件将同时存在。<br>  <br>- 批量移动文件时，如果由于意外情况导致操作中断，则工具无法恢复执行。 |
| 重命名文件 | 选中 **更多** > **重命名** 进行操作。<br>**重要**<br>重命名操作通过先将源文件复制到目标地址，再删除源文件的方式实现。操作注意事项如下：<br>- 在重命名文件过程中，如果复制失败，则源文件不会被删除。如果复制成功但后续删除源文件失败（例如无权限），则源文件和目标文件将同时存在。<br>  <br>- 重命名文件夹时，如果由于意外情况导致操作中断，则工具无法恢复执行。 |
| 搜索文件 | 在页面上方搜索框中输入指定的文件名前缀，您可以查看Bucket根目录下与指定前缀匹配的文件和文件夹。 |
| 解冻文件 | 选中 **更多** > **解冻** 进行操作。 |
| 删除文件 | 单击文件操作列的 **删除**，删除文件。 |
| 设置软链接 | 1. 选中 **更多** > **设置软链接**。<br>   <br>2. 在 **设置软链接** 面板，设置 **软链接文件目录**，然后单击确定。 |
| 管理文件元数据 | 1. 选中 **更多** > **HTTP头**。<br>   <br>2. 在 **HTTP头** 对话框，设置文件元数据，然后单击确定。 |
| 分享文件 | 文件上传至Bucket后，您可以将文件URL分享给第三方，供其下载或预览。单击目标文件操作列的 **获取地址**，生成文件分享地址。 |
| 设置ACL | 1. 选中 **更多** > **ACL权限**。<br>   <br>2. 在 **设置ACL权限** 对话框，设置文件ACL权限，然后单击确定。 |