### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/)[持久化存储](https://help.aliyun.com/zh/sae/persistent-storage/)设置NAS存储

# 设置NAS存储

更新时间：2025-09-11 08:28:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：持久化存储](https://help.aliyun.com/zh/sae/persistent-storage/)[下一篇：设置OSS存储](https://help.aliyun.com/zh/sae/copnfigure-oss-storage-2-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

在创建应用过程中配置NAS存储

在部署应用过程中配置NAS存储

取消挂载NAS

结果验证

常见问题

如何查看NAS中的内容？

可以使用NAS存储日志吗？

通常，当容器被销毁时，其内部的数据也会随之丢失，这对生产环境来说可能会产生负面影响。NAS适用于高性能计算和数据共享场景。将NAS挂载至SAE应用实例，可以有效解决应用数据的持久化存储需求，并实现应用实例之间的数据共享。

## 前提条件

- [开通NAS服务](https://nas.console.aliyun.com/)

- [通过控制台创建通用型NAS文件系统](https://help.aliyun.com/zh/nas/user-guide/create-a-file-system#section-5jo-0kj-jn5 "")

- [添加挂载点](https://help.aliyun.com/zh/nas/user-guide/manage-mount-targets#section-6xi-a3u-zkq "")


## 操作步骤

### 在创建应用过程中配置NAS存储

1. 在[SAE应用列表](https://saenext.console.aliyun.com/cn-hangzhou/app-list/micro)中，在顶部选择目标地域和命名空间，点击 **创建应用**。

2. 在 **应用基本信息** 配置向导，设置应用相关信息，并单击 **下一步：高级设置**。

3. 找到并展开 **持久化存储** 区域，配置相关参数。

1. 打开 **启用NAS文件存储** 的开关。

2. 在 **NAS文件系统** 所在行的下拉列表，选择待挂载的NAS，并设置 **挂载源**、 **挂载目录**、 **容器路径**、 **权限**。





      **说明**





      - **挂载目录** 只能为根目录/或者非/开头的子目录。

      - **容器路径** 不能重复，也不能存在包含关系，例如/tmp和/tmp/nas。

      - 单击 **+添加** 增加挂载路径。最多支持10条挂载路径。
4. 单击 **创建应用**。


### 在部署应用过程中配置NAS存储

**警告**

重新部署应用后，该应用将会被重启。为避免业务中断等不可预知的错误，请在业务低峰期执行部署操作。

更新应用配置的路径因实例数的不同而不同。本文以实例数大于等于1为例，介绍如何配置目标功能。当实例数等于0时的操作路径，请参见 [更新应用](https://help.aliyun.com/zh/sae/serverless-app-engine-classic/user-guide/manage-the-lifecycle-of-an-application#section-3qn-6i4-g2p "")。

1. 在[SAE应用列表](https://saenext.console.aliyun.com/cn-hangzhou/app-list/micro)中，在顶部选择目标地域和命名空间，点击目标 **应用ID** 跳转到应用详情页。

2. 在目标应用的 **基础信息** 页面，单击 **部署应用**。

3. 找到并展开 **持久化存储** 区域，配置相关参数。

1. 打开 **启用NAS文件存储** 的开关。

2. 在 **NAS文件系统** 所在行的下拉列表，选择待挂载的NAS，并设置 **挂载源**、 **挂载目录**、 **容器路径**、 **权限**。





      **说明**





      - **挂载目录** 只能为根目录/或者非/开头的子目录。

      - **容器路径** 不能重复，也不能存在包含关系，例如/tmp和/tmp/nas。

      - 单击 **+添加** 增加挂载路径。最多支持10条挂载路径。
4. 配置完成后，单击 **确定**。


### 取消挂载NAS

**警告**

重新部署应用后，该应用将会被重启。为避免业务中断等不可预知的错误，请在业务低峰期执行部署操作。

挂载NAS后，如果您不再使用NAS存储，可以取消挂载NAS。在 [SAE控制台](https://sae.console.aliyun.com/) 取消挂载NAS后，NAS中所存储的数据仍然存在，不会被删除。具体操作，请参见 [在部署应用过程中配置NAS存储](https://help.aliyun.com/zh/sae/configure-nas-storage-2-0#p-rfn-neh-71w "")。参照 [步骤](https://help.aliyun.com/zh/sae/configure-nas-storage-2-0#step-f9u-1pn-dfv "") [4](https://help.aliyun.com/zh/sae/configure-nas-storage-2-0#step-f9u-1pn-dfv "")，关闭 **启用NAS存储** 的开关，并单击 **确定**。

## 结果验证

按需选择不同系统下，验证NAS挂载是否成功的方式。

- 从变更详情判断。

如果单次创建或部署的变更已经成功，变更生成的新的实例没有出现异常事件，表示NAS挂载成功。

![sae挂载nas成功](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5232573661/p70176.png)

- 从容器角度判断。

在Webshell执行以下命令，查询应用中是否存在NAS挂载信息。















```shell
cat /proc/mounts | grep nfs
```



当显示如下信息时，表示NAS挂载成功。

![成功挂载nas存储](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2022251361/p70160.png)

- 从业务角度判断。

在Webshell中，对挂载NAS路径进行操作。如果NAS文件系统中可查找到NAS路径，表示NAS挂载成功。


## 常见问题

### 如何查看NAS中的内容？

不支持使用白屏化工具来查看NAS的文件内容。如果您想查看NAS中的内容，需要将NAS挂载到SAE应用或ECS服务器。具体操作，请参见以下文档：

- [挂载NFS协议文件系统（通用型NAS）](https://help.aliyun.com/zh/nas/user-guide/mount-a-general-purpose-nfs-file-system-on-a-windows-ecs-instance#concept-67165-zh "")

- [挂载SMB协议文件系统](https://help.aliyun.com/zh/nas/user-guide/mount-smb-protocol-file-system-on-windows-system#task-2526664 "")

- [挂载SMB协议文件系统](https://help.aliyun.com/zh/nas/user-guide/mount-an-smb-file-system-on-a-linux-ecs-instance#task-1580275 "")

- [挂载NFS协议文件系统](https://help.aliyun.com/zh/nas/user-guide/mount-an-nfs-file-system-on-a-linux-ecs-instance#concept-hpp-dkh-cfb "")


### **可以使用NAS存储日志吗？**

不建议使用NAS作为日志持久化工具，以免多客户端同时写入同一文件时，可能会导致并发访问冲突和性能瓶颈。

建议在日志场景中使用SLS，确保日志数据持久化。具体操作，请参见 [设置日志收集至SLS](https://help.aliyun.com/zh/sae/set-log-collection-to-sls-2-0 "")。