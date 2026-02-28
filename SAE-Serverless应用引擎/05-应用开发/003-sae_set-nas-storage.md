### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[服务支持](https://help.aliyun.com/zh/sae/support/)[Web应用文档合集（文档停止维护）](https://help.aliyun.com/zh/sae/web-application-documentation/)[Web应用操作指南](https://help.aliyun.com/zh/sae/web-application-new/)[高级设置](https://help.aliyun.com/zh/sae/advanced-settings/)[设置持久化存储](https://help.aliyun.com/zh/sae/set-up-persistent-storage/)设置NAS存储

# 设置NAS存储

更新时间：2024-11-01 01:53:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置OSS存储](https://help.aliyun.com/zh/sae/set-oss-storage)[下一篇：通过公网访问应用](https://help.aliyun.com/zh/sae/access-applications-through-the-internet)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

使用限制

前提条件

操作步骤

验证结果

文件存储 NAS（File Storage NAS）是一种可共享访问、弹性扩展高可靠、高性能的分布式文件系统，为阿里云ECS实例、E-HPC、Serverless 应用引擎、容器服务等计算节点提供了文件存储服务。本文介绍如何在SAE控制台为应用设置NAS存储。

## **背景信息**

通常，容器中的数据不是持久化的，意味着容器销毁时，数据也会随之丢失，这可能对生产环境造成严重影响。阿里云Serverless 应用引擎通过支持NAS存储功能，为应用实例数据的持久化及实例间的数据共享提供了解决方案，您可以根据需要选择使用NAS或OSS存储。

- NAS

NAS在吞吐和共享上有明显优势，适合高性能计算以及数据共享场景。

- OSS

OSS在吞吐上有明显优势，既适合互联网图片、音视频海量文件处理场景，也适合网页、移动应用的静态和动态资源分离的场景。更多信息，请参见 [设置OSS存储](https://help.aliyun.com/zh/sae/set-oss-storage "")。


## **使用限制**

- 单应用版本最多支持10条挂载路径。

- 不建议使用NAS作为日志持久化的工具，以免出现多客户端并发写导致冲突的问题。更多信息，请参见 [挂载访问FAQ](https://help.aliyun.com/zh/nas/user-guide/faq-about-mounting/ "") 和 [日志管理（SLS）](https://help.aliyun.com/zh/sae/log-management-sls "")。


## **前提条件**

- NAS

  - [创建NAS文件系统](https://help.aliyun.com/zh/nas/user-guide/create-a-file-system#task-27530-zh "")

  - [添加挂载点](https://help.aliyun.com/zh/nas/user-guide/manage-mount-targets#section-6xi-a3u-zkq "")
- VPC

  - [创建和管理专有网络](https://help.aliyun.com/zh/vpc/user-guide/create-and-manage-a-vpc "")

  - [创建和管理交换机](https://help.aliyun.com/zh/vpc/user-guide/create-and-manage-vswitch "")
- ECS

  - [创建安全组](https://help.aliyun.com/zh/ecs/user-guide/create-a-security-group-1 "")

## **操作步骤**

在创建Web应用时设置NAS存储

在部署新版本时设置NAS存储

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击 **创建应用**。

4. 在 **应用基本信息** 页面，按照页面提示完成参数配置，然后单击 **下一步：高级设置**。

5. 在 **高级设置** 配置页面，配置相关信息。

1. 展开网络设置区域，单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4250435271/p808532.png)图标，打开 **允许应用访问VPC** 开关，然后选择 **专有网络 VPC**、 **交换机 vSwitch**、 **安全组** 以及 **应用访问公网方式**。

      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4250435271/p808534.png)

2. 展开 **持久化存储** 区域，单击 **启用NAS文件存储** 对应的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4250435271/p809542.png)图标，然后设置以下参数。




      **说明**





      NAS支持在私有的VPC环境添加挂载点。因此，需确保SAE配置与NAS相同的VPC，才能访问指定的NAS文件系统。配置项的详细信息，请参见 [设置网络](https://help.aliyun.com/zh/sae/set-up-the-network "")。







      |     |     |
      | --- | --- |
      | **配置项** | **说明** |
      | **NAS文件系统** | 选择已创建的NAS文件系统。 |
      | **挂载源** | 选择已创建的NAS挂载点。 |
      | **挂载目录** | 只能为根目录`/`或者非`/`开头的子目录。 |
      | **容器路径** | 不支持重复、包含关系，例如不支持同时配置`/tmp`和`/tmp/nas`。 |



      ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4250435271/p808550.png)
6. 单击 **创建应用**，应用创建成功后，页面会跳转至应用的 **基础信息** 页面。


**警告**

部署新版本后，该应用将会被重启。为避免业务中断等不可预知的错误，请在业务低峰期执行部署操作。

设置NAS存储既可以在创建应用时设置，也可以在更新应用版本时设置。本步骤以更新应用版本时为例，因此您需要先创建应用。具体操作，请参见 [管理应用](https://help.aliyun.com/zh/sae/application-management-2384758 "")。

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击目标应用名称。

4. 在左侧导航栏，单击 **版本列表**，然后单击 **新建版本**。

5. 在弹出的 **新建版本** 面板中展开 **持久化存储**，单击 **启用NAS文件存储** 对应的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4250435271/p809542.png)图标，设置以下参数，然后单击 **确定**。




**说明**





NAS支持在私有的VPC环境添加挂载点。因此，需确保SAE配置与NAS相同的VPC，才能访问指定的NAS文件系统。配置项的详细信息，请参见 [设置网络](https://help.aliyun.com/zh/sae/set-up-the-network "")。







|     |     |
| --- | --- |
| **配置项** | **说明** |
| **NAS文件系统** | 选择已创建的NAS文件系统。 |
| **挂载源** | 选择已创建的NAS挂载点。 |
| **挂载目录** | 只能为根目录`/`或者非`/`开头的子目录。 |
| **容器路径** | 不支持重复、包含关系，例如不支持同时配置`/tmp`和`/tmp/nas`。 |



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4250435271/p808550.png)


## **验证结果**

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)，在左侧导航栏选择**应用管理** \> **Web应用**，然后在顶部菜单栏选择目标地域。

2. 在 **应用列表** 页面，单击目标应用名称。

3. 在左侧导航栏，单击 **版本列表**，然后单击目标版本 **操作** 列的 **Webshell**。

4. 登录实例，验证NAS是否挂载成功。















```shell
    mount | grep nfs
```



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4250435271/p808589.png)