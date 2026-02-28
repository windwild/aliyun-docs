### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [服务支持](https://help.aliyun.com/zh/sae/support/) [Web应用文档合集（文档停止维护）](https://help.aliyun.com/zh/sae/web-application-documentation/) [Web应用操作指南](https://help.aliyun.com/zh/sae/web-application-new/) [高级设置](https://help.aliyun.com/zh/sae/advanced-settings/) 设置启动命令

# 设置启动命令

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：高级设置](https://help.aliyun.com/zh/sae/advanced-settings/)[下一篇：设置日志及监控metrics](https://help.aliyun.com/zh/sae/set-logs-and-monitor-metrics)

该文章对您有帮助吗？

反馈

通过Serverless 应用引擎 SAE（Serverless App Engine）控制台使用镜像方式部署应用时，SAE通过容器镜像预设的启动参数启动容器。如果在启动前需要进行特殊配置，例如Nginx，或者不采用预设的启动参数，您可以在SAE设置容器启动命令，进行特殊配置或者覆盖镜像的启动默认值。本文介绍如何在SAE控制台配置启动命令。

## **背景信息**

在制作镜像时，容器的启动配置已经在Dockerfile文件中的 [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/?spm=a2c4g.96677.0.0.52741ee3VEIUk0#entrypoint) 或 [CMD](https://docs.docker.com/engine/reference/builder/#cmd) 进行了配置。容器启动时，Dockerfile文件中的内容会被优先执行。

例如，Dockerfile中设置的以下命令，在容器启动时将被第一个执行。

```shell
FROM ubuntu
ENTRYPOINT [nginx, '-g', 'daemon off;']
```

在SAE中设置容器的启动命令，将覆盖DockerFile中的CMD配置。

## **操作步骤**

### **在创建Web应用时设置启动命令**

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击 **创建应用**。

4. 在 **基础信息设置** 页面，根据页面配置相关信息，然后单击 **下一步：高级设置**。

5. 在 **高级设置** 配置向导的 **启动命令设置** 区域，选择脚本类型，输入启动命令，然后单击 **创建应用**。

示例命令如下。


   - **>\_ /bin/sh**


     ```sh
     sh -c 'while true; do echo hello; sleep 10;done'
     ```

   - **>\_ /bin/bash**


     ```bash
     bash -c 'while true; do echo hello; sleep 10;done'
     ```


应用创建成功后，页面会跳转至应用的 **基础信息** 页面。

### **在部署新版本时设置启动命令**

启动命令既可以在创建应用时设置，也可以在更新应用版本时设置。本步骤以更新应用版本时为例。

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击目标应用名称。

4. 在左侧导航栏，单击 **版本列表**，然后单击 **新建版本**。

5. 在 **新建版本** 面板的 **启动命令设置** 区域，选择脚本类型，输入启动命令，然后单击 **确定**。

示例命令如下。


   - **>\_ /bin/sh**


     ```sh
     sh -c 'while true; do echo hello; sleep 10;done'
     ```

   - **>\_ /bin/bash**


     ```bash
     bash -c 'while true; do echo hello; sleep 10;done'
     ```


版本创建成功后，您可以在 **版本列表** 页面查看新建的版本。

## **验证结果**

如果您想要验证启动命令是否生效，可以登录 [SAE控制台](http://saenext.console.aliyun.com/)，在目标应用的 **日志管理** 页面，选择指定的版本以及对应的版本实例，查看应用的标准输出日志。