编排模板是对一组资源的定义和描述，您可通过编排模板快速创建应用。本文介绍如何创建和编辑编排模板。

## 创建编排模板

### 方式一：直接创建编排模板

1. 登录[容器服务管理控制台](https://cs.console.aliyun.com/)。
2. 在控制台左侧导航栏中，选择市场 \> 编排模板。
3. 在模板列表页面右上角单击创建。
4. 在创建对话框中，配置编排模板，最后单击保存。


   - 名称：设置该模板的名称。

   - 描述：输入对该模板的描述，可不配置。

   - 模板：配置符合Kubernetes YAML语法规则的编排模板。



     **说明**





     - 可包含多个资源对象，以`---`进行分割。

     - 可在YAML中添加`${params}`格式的值（例如`app: ${nginx}`），该值会在您部署应用时被自动识别为参数。


创建完毕后，默认进入模板列表页面，单击模板名称下的详情可看到该模板。


### 方式二：通过容器服务内置模板创建

1. 在集群列表页面中，单击目标集群名称或者目标集群右侧操作列下的详情。
2. 在集群管理页左侧导航栏中，选择工作负载 \> 无状态。
3. 在无状态页面单击右上角的使用YAML创建资源。
4. 选择一个内置模板，然后单击保存模板。
5. 在保存模板的对话框中，配置模板信息，包括名称、描述和模板。然后单击保存。




**说明**



您可在内置模板的基础上进行修改。






创建完毕后，默认进入模板列表页面，单击模板名称下的详情可看到该模板。



## 编辑编排模板

1. 在模板列表页选择所需的模板，单击详情。
2. 在该模板的详情页中，编辑集群、命名空间、版本描述和模板内容。
配置完成后，根据需要可对编排模板进行更新、另存、下载和删除操作。


   - 单击保存完成编排模板的更新。

   - 单击右上角另存为，输入新的模板名称，然后单击确定另存模板。

   - 单击右上角下载完成后缀为`yml`格式的模板文件下载。

   - 单击右上角删除，在提示对话框中单击确定，删除编排模板。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[市场](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/marketplace/)编排模板管理

# 编排模板管理

更新时间：2022-05-16 22:22:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：容器镜像服务ACR](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/container-registry)[下一篇：应用市场](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/app-marketplace)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

创建编排模板

方式一：直接创建编排模板

方式二：通过容器服务内置模板创建

编辑编排模板