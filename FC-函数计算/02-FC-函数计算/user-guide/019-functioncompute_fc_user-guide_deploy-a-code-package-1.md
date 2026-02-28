### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[开发与执行环境](https://help.aliyun.com/zh/functioncompute/fc/user-guide/development-and-execution-environment/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc/user-guide/code-development/)[Python](https://help.aliyun.com/zh/functioncompute/fc/user-guide/python/)部署代码包

# 部署代码包

更新时间：2025-07-10 01:10:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：上下文](https://help.aliyun.com/zh/functioncompute/fc/user-guide/context-1)[下一篇：日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging-2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

准备工作

使用pip安装依赖并部署代码

前提条件

操作步骤

使用Serverless Devs工具安装依赖并部署项目

前提条件

操作步骤

更多信息

本文以安装第三方依赖emoji为例，介绍如何为您的Python代码安装依赖，打包并部署代码至函数计算。

## 准备工作

1. 创建一个用于测试的代码目录，如`mycode`。



   - Linux或macOS系统

     您可以执行`mkdir -p /tmp/mycode`创建。

   - Windows系统

     在任意位置新建文件夹，并将其命名为`mycode`即可。


2. 在`mycode`目录下，建立`index.py`文件。



文件内容如下。

















```python
from emoji import emojize
def handler(event, context):
       return emojize(":thumbs_up:")
```


## 使用pip安装依赖并部署代码

### **前提条件**

- 您的本机已安装Python 3，且具有执行pip3的权限。

- 您已在[函数计算控制台](https://fcnext.console.aliyun.com/)创建Python函数。具体操作，请参见 [创建事件函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/creating-an-event-function#45e9ee65bd8n7 "")。


### **操作步骤**

1. 在`mycode`目录下执行`pip3 install emoji -t .`安装emoji依赖库到当前目录。

2. 打包`mycode`目录下的所有文件。



   - Linux或macOS系统

     进入`mycode`目录，执行`zip code.zip -r ./*`。



     **说明**





     请确保您具有该目录的读写权限。

   - Windows系统

     进入`mycode`目录，选中所有文件，单击鼠标右键，选择打包为ZIP包。


3. 在 [函数计算控制台](https://fcnext.console.aliyun.com/)，找到目标函数，然后在函数详情页面的 **代码** 页签，单击右上角**上传代码** \> **上传 ZIP 包**，在弹出的对话框，上传您上一步打包的ZIP包，单击 **保存并部署**。


**重要**

由于函数计算的运行环境是Linux系统，您在Windows系统或macOS系统安装emoji依赖库时如果带有二进制文件，会导致您的代码包上传到函数计算后运行失败。因此，建议您 [使用WebIDE打包函数第三方依赖](https://help.aliyun.com/zh/functioncompute/fc/developer-reference/use-webide-to-package-third-party-dependencies-of-a-function-1 "") 或者 [使用Serverless Devs工具安装依赖并部署项目](https://help.aliyun.com/zh/functioncompute/fc/user-guide/deploy-a-code-package-1#section-hbb-uz4-d4w "")。

## 使用Serverless Devs工具安装依赖并部署项目

### **前提条件**

- [安装Serverless Devs和Docker](https://help.aliyun.com/zh/functioncompute/fc/developer-reference/install-serverless-devs-and-docker "")

- [配置Serverless Devs](https://help.aliyun.com/zh/functioncompute/fc-3-0/developer-reference/configure-serverless-devs-1 "")


### **操作步骤**

1. 执行`cd /tmp/mycode`进入`mycode`目录。

2. 新增`s.yaml`文件。



编写文件内容示例如下。

















```yaml
edition: 3.0.0
name: fcDeployApp
access: "default"

vars: # 全局变量
     region: "cn-hangzhou"

resources:
     hello_world:
       component: fc3 # 组件名称
       props:
         region: ${vars.region}
         functionName: "emojipy"
         description: 'this is emoji'
         runtime: "python3"
         code: ./
         handler: index.handler
         memorySize: 128
         timeout: 30
         environmentVariables:
           PYTHONUSERBASE: /code/python         # 增加环境变量获取依赖
```

3. 新增`requirements.txt`文件。



编写文件内容如下：

















```plaintext
emoji==2.0.0
```

4. 执行`sudo s build --use-docker`安装依赖。



执行完成后，依赖被安装到`./python`目录下。

5. 执行`sudo s deploy`部署项目。



执行完成后，即可部署函数到函数计算。


## 更多信息

您也可以使用函数计算的层功能安装依赖，推荐您使用官方公共层或在线构建依赖层。具体操作，请参见以下文档。

- [创建自定义层](https://help.aliyun.com/zh/functioncompute/fc/user-guide/create-a-custom-layer-1#section-c5l-g61-hgs "")

- [通过控制台配置官方公共层](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-common-layers-for-a-function-1#section-8ia-e87-98z "")