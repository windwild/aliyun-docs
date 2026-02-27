### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 使用Funcraft管理函数资源

# 使用Funcraft管理函数资源

更新时间：2024-10-17 05:43:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

操作步骤

进阶教程

本文以编写Hello World函数为例，介绍如何使用Funcraft管理函数资源。

**重要**

本文介绍的内容后期将不再维护。如果您的函数计算资源是使用Funcraft管理的，建议您将资源迁移至Serverless Devs管理。

关于如何将函数计算的相关资源从Funcraft迁移到Serverless Devs进行管理的详细操作，请参见 [从Funcraft迁移到Serverless Devs](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/migrate-resources-from-funcraft-to-serverless-devs#concept-2100642 "")。

关于如何使用Serverless Devs管理函数资源，请参见 [通过Serverless Devs工具管理函数资源](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/manage-function-resources-by-using-serverless-devs#task-2099648 "")。

由此带来的不便，敬请谅解！

## 背景信息

Funcraft是函数计算提供的应用部署工具，可以帮助您便捷地管理函数计算、API网关及日志服务等资源，快速部署应用。关于Funcraft的更多信息，请参见 [功能概览](https://help.aliyun.com/zh/functioncompute/fc-2-0/features-2#concept-2260071 "")。

## 前提条件

您已完成以下操作：

- [开通服务](https://help.aliyun.com/document_detail/253972.html#task-2076731 "")

- [安装Funcraft](https://help.aliyun.com/zh/functioncompute/fc-2-0/install-funcraft#topic2715 "")

- [配置Funcraft](https://help.aliyun.com/zh/functioncompute/fc-2-0/configure-funcraft#concept-2260072 "")


## 操作步骤

1. 创建初始化模板。

1. 执行以下命令初始化项目模板。

















      ```plaintext
      fun init -n demo
      ```

2. 根据提示选择一个项目模板。

















      ```plaintext
      ? Select a template to init (Use arrow keys or type to search)
      > event-nodejs12
        event-nodejs10
        event-nodejs8
        event-nodejs6
        event-python3
        event-python2.7
        event-java8
        event-php7.2
        event-dotnetcore2.1
        http-trigger-nodejs12
        http-trigger-nodejs10
        http-trigger-nodejs8
        http-trigger-nodejs6
        http-trigger-python3
        http-trigger-python2.7
        http-trigger-java8
      (Move up and down to reveal more choices)
      ```







      项目模板类型如下：



      - 以`event-`为前缀的模板是普通的事件函数。

      - 以`http-trigger`为前缀的模板会默认为您创建HTTP触发器。HTTP触发器以Request、Response为入参，帮助您快速搭建Web应用。


本示例中以`event-nodejs10`为例。

Funcraft在执行命令的目录下，创建了一个demo的目录，并添加了两个文件，分别是index.js和template.yml。

      - index.js包含了函数的示例代码。

      - template.yml指定了函数资源的相关信息。

        - 本示例为您创建了一个名为`demo`的服务与一个名为`demo`的函数。

        - template.yml文件支持的配置项，请参见 [Serverless Application Model](https://github.com/alibaba/funcraft/blob/master/docs/specs/2018-04-03-zh-cn.md)。
2. **可选：**本地调试。



本地调试需要您本地安装Docker，详细信息，请参见 [安装Docker](https://github.com/alibaba/funcraft/blob/master/docs/usage/installation-zh.md?file=installation-zh.md#%E5%AE%89%E8%A3%85-docker%E5%8F%AF%E9%80%89)。如果您本地无法安装Docker，可以跳过此步骤，在云端调试。



1. 执行以下命令进入Demo函数中。

















      ```plaintext
      cd demo
      ```

2. 本地执行以下命令调试函数。

















      ```plaintext
      fun local invoke demo
      ```





      ![local_test](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0435297951/p96627.png)





      **说明**





      第一次执行会拉取执行环境的镜像到本地，耗时较长。
3. 部署到云端。

1. 执行以下命令将函数部署到云端。

















      ```plaintext
      fun deploy
      ```

2. 部署过程中，输入`Y`确认需要创建的资源。



      ![deploy](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0435297951/p96629.png)





      创建完成后，提示`service demo deploy success`代表您的资源部署成功。
4. 云端测试。



您可以登录函数计算控制台，查看是否部署成功。



1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)。

2. 在左侧导航栏，单击 **服务及函数**。

3. 在顶部菜单栏，选择地域。

4. 在 **服务列表** 页面，单击目标服务。

5. 在 **函数管理** 页面，单击目标函数名称。

6. 在目标函数详情页面的 **函数代码** 页签，单击 **测试函数**，即可在函数计算控制台执行函数。
5. 查看日志。



每次执行完毕，您可以在当前页面查看本次执行日志。如果需要查看历史执行日志，可以单击 **调用日志** 页签，查看历史日志时，需要您为函数配置日志仓库。详细信息，请参见 [配置日志](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-the-logging-feature#multiTask2691 "")。


## 进阶教程

完成以上教程后您可以根据使用场景查阅以下文档。

- [触发器简介](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/trigger-overview#concept-2259970 "")