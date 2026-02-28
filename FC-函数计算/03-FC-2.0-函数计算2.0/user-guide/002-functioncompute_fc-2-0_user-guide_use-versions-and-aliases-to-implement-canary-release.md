### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[服务管理](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/service-management/)使用版本和别名实现灰度发布

# 使用版本和别名实现灰度发布

更新时间：2025-08-04 01:28:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：管理别名](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-aliases)[下一篇：配置网络](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-network-settings)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

视频演示

灰度发布流程

前提条件

步骤一：准备函数并测试

步骤二：发布版本并测试

步骤三：使用别名切换流量

常见问题

如何确定被调用的服务的版本？

您可以为服务发布一个或多个版本，版本就相当于服务的快照，当您发布版本时，函数计算会为服务生成快照，并自动分配一个版本号与其关联。您还可以为服务的版本创建别名，指向该版本。结合服务的版本和别名，您可以轻松实现发布、回滚以及灰度发布等功能。本文介绍如何在函数计算控制台使用服务的版本和别名实现灰度发布。

## 视频演示

使用版本和别名实现灰度发布

## 灰度发布流程

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8035824571/CAEQNBiBgMD6nbub4xgiIGJjMzUyNDA1ZjViMjRiZTVhNDFiZjcwYzIzNzZmYjc53963382_20230830144006.372.svg)

## 前提条件

- [创建服务](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-services#section-765-0zj-cc4 "")

- [创建函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions#section-b9y-zn1-5wr "")


## 步骤一：准备函数并测试

当您初次创建一个服务以及该服务下的函数时，该服务的版本号为LATEST。您可以调试LATEST版本下的函数直至版本稳定运行。您可以通过控制台执行LATEST版本下的函数。

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务。
3. 在 **函数管理** 页面，单击目标函数名称，然后在函数详情页面，单击 **函数代码** 页签。
4. 在代码编辑器中，修改代码为查看函数版本的代码，单击 **部署代码**，然后单击 **测试函数**。



查看函数版本的代码示例如下。









Node.js



Python



PHP



C#

















Node.js

















```nodejs
module.exports.handler = function(eventBuf, context, callback) {
    var qualifier = context['service']['qualifier']
    var versionId = context['service']['versionId']
    console.log('Qualifier from context:', qualifier);
    console.log('VersionId from context: ', versionId);
    callback(null, qualifier);
};
```





Python

















```python
# -*- coding: utf-8 -*-

def handler(event, context):
     qualifier = context.service.qualifier
     versionId = context.service.version_id
     print('Qualifier from context:' + qualifier)
     print('VersionId from context:' + versionId)
     return 'hello world'
```





PHP

















```php
<?php
function handler($event, $context) {
     $qualifier = $context["service"]["qualifier"];
     $versionId = $context["service"]["versionId"];
     print($qualifier);
     print($versionId);

       return "hello world";
}
```





C#

















```csharp
using System;
using System.IO;
using Aliyun.Serverless.Core;
using Microsoft.Extensions.Logging;

namespace Desktop
{

       class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello World!");
           }
       }

       class App
       {
           public string Handler(Stream input, IFcContext context)
           {
               ILogger logger = context.Logger;
               var qualifier = context.ServiceMeta.Qualifier;
               var versionId = context.ServiceMeta.VersionId;
               logger.LogInformation("Qualifier from context: {0}", qualifier);
               logger.LogInformation("versionId from context: {0}", versionId);
               return "hello word";
           }
       }
}
```











执行完成后，可以查看日志输出。从日志输出中，可以看到表示版本信息的字段qualifier的值为LATEST，即本次执行的函数为LATEST版本下的函数。


## 步骤二：发布版本并测试

当LATEST版本的服务稳定时，就可以发布该版本的服务，使用稳定的版本服务线上的请求。具体操作，请参见 [发布版本](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-versions#section-jdg-qkr-9xv "")。

新版本发布后，您可以通过控制台执行新版本下的函数。

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务。
3. 在 **函数管理** 页面，在 **版本** 下拉框选择新版本的版本号。



![version1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6653527461/p348622.png)

4. 单击目标函数名称，单击 **函数代码** 页签，然后单击 **测试函数**。



执行完成后，可以查看执行日志。从日志输出中，可以看到函数执行时的版本信息qualifier为1，解析出的versionId为1，即本次执行的函数为版本1下的函数。


## 步骤三：使用别名切换流量

新版本上线后，您可以创建一个别名，设置别名指向该版本。当该版本更新时，可将别名指向的版本更改为更新的版本。调用方无需关心服务的具体版本，只需要使用正确的别名即可。关于创建别名的具体步骤，请参见 [创建别名](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-aliases#section-7aw-oca-2pz "")。

别名创建完成后，您可以通过控制台验证是否执行了正确版本的函数。

本文以别名 **alias1** 指向版本 **1** 为例。

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务。
3. 在 **函数管理** 页面，单击目标函数名称。
4. 在函数详情页面的右上方，在 **版本或别名** 下拉列表中选择新创建的别名 **alias1**。



![choose alias](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7783916361/p348623.png)

5. 单击 **函数代码** 页签，然后单击 **测试函数**。



执行完成后，可以查看日志输出。从日志输出中，可以看到函数执行时的版本信息qualifier为 **alias1**，解析出的versionId为 **1**，即本次执行的函数为别名 **alias1** 下的函数，该别名指向版本 **1**。


新版本开发完成后，需要使用灰度版本帮助新版本的稳定发布。

1. 发布新版本 **2**。具体操作，请参见 [发布版本](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-versions#section-jdg-qkr-9xv "")。



发布完成后，可在版本列表中查看新发布的版本。

2. 在左侧导航栏，单击 **别名管理**。

3. 在别名列表中找到指向版本 **1** 的别名 **alias1**，在其 **操作** 列，单击 **编辑**。

4. 在编辑服务的别名面板，将新版本 **2** 设置为 **灰度版本**，设置灰度类型，然后单击 **确定**。


   - **按百分比随机灰度**

     需填写 **灰度版本权重**，如下图所示。

     ![edit-alias1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7853260661/p475050.png)

     设置完成后，调用别名 **alias1** 验证是否已将部分线上流量切换到新版本 **2**。本示例中，如果共调用别名 **alias1** 执行函数10次，结果中将有3次调用版本 **2**，7次调用版本 **1**。

   - **按指定规则灰度**



     **说明**





     **按指定规则灰度** 目前仅支持HTTP函数。





     ![edit-alias1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7853260661/p477768.png)

     本示例中，仅当参数key取值为`x-test-uid`时，将请求消息路由至灰度版本。


创建灰度发布规则的参数说明如下。

| **参数名称** | **参数说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数名称** | **参数说明** |
| **名称** | 要创建的别名的名称。 |
| **主版本** | 设置别名的主版本。 |
| **启用灰度版本** | 是否启用灰度版本。 |
| **灰度版本** | 设置别名的灰度版本。 |
| **灰度类型** | 根据不同的灰度策略分为 **按百分比随机灰度** 和 **按指定规则灰度**。<br>   - **按百分比随机灰度**：设置一定的权重切换流量到灰度版本。<br>     <br>   - **按指定规则灰度**：设置一定的规则，并按照指定的规则模式进行灰度发布。 |
| **灰度版本权重** | 当 **灰度类型** 为 **按百分比随机灰度** 时，需配置此参数。<br>表示切换流量至灰度版本的百分比。例如，设置该参数的值为5%，函数计算将分配5%的流量到灰度版本，95%的流量到主版本。 |
| **规则模式** | 当 **灰度类型** 为 **按指定规则灰度** 时，需配置此参数。<br>表示对设置的规则的选择模式，取值如下：<br>   - **同时满足下列规则**<br>     <br>   - **满足下列任意规则** |
| **规则列表** | 当 **灰度类型** 为 **按指定规则灰度** 时，需配置此参数。<br>表示具体的规则内容，包含以下三部分：<br>   - **参数类型**：取值包含Header、Cookie和Query。<br>     <br>   - **参数**：控制灰度发布的参数名。<br>     <br>   - **条件**：计算条件。函数计算将 **参数** 的实际值与您填写的参数值按照您设置的条件进行计算，如果满足条件，则本条请求被路由至灰度版本。包含以下枚举值：<br>     <br>     - `=、!=、>、<、>=、<=`：运算符比较条件。例如，设置 **条件** 为`=`，表示仅当请求参数实际值等于设置的参数 **值** 时，将本条请求路由至灰度版本。<br>       <br>     - `in`：字符串匹配条件，仅当请求参数实际值包含在设置的参数 **值** 以内时，将本条请求路由至灰度版本。<br>       <br>     - `值分布百分比`：表示按照参数值的特定百分比灰度发布。例如，设置 **参数类型** 为Header， **参数** 为`user-id`， **值** 为`20`，表示根据HTTP请求Header`user-id`的具体分布，取其中20%分布值对应的请求路由至灰度版本。<br>   - **值**：控制灰度发布的参数值。<br>     <br>单击下方的 **+添加规则**，可以添加更多其他规则。 |
| 高级选项 |
| **预留实例灰度比例** | 用于控制预留模式的灰度实例比例。当预留的实例数量大于1时，会按照该参数设置的比例生成预留模式的实例数量，否则，按照默认的1%生成预留模式的实例数量。<br>**重要**<br>仅当您预留的实例数量大于1时，该参数的值有效。 |

待灰度版本运行稳定后，可以将线上流量全部切换到新版本 **2**。

## 常见问题

### 如何确定被调用的服务的版本？

使用灰度发布功能时，函数计算按照您指定的权重来分配流量。您可以通过以下方式来确定被调用的服务的版本：

- 通过context入参确定



每次函数调用，context入参的service参数中会包括qualifier和versionId两个字段。



  - qualifier：调用函数时传入的版本信息，可以是版本号，也可以是别名。

  - versionId：函数执行时根据qualifier解析出的具体版本号。


- 通过同步函数调用响应确定

同步函数调用的响应包含x-fc-invocation-service-version Header，可以指示已调用的服务版本。