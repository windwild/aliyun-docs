### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[函数调用与触发器](https://help.aliyun.com/zh/functioncompute/fc/user-guide/function-calls-and-triggers/)调用示例

# 调用示例

更新时间：2024-05-11 01:14:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：HTTP触发器调用函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/http-trigger-invoking-function-1)[下一篇：重试机制](https://help.aliyun.com/zh/functioncompute/fc/user-guide/error-handling-1-2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

调用API

调用SDK

函数计算的2021-04-06及以后版本的API符合阿里云OpenAPI规范，您可以在阿里云[OpenAPI Explorer](https://next.api.aliyun.com/api/)查看和调试API/SDK。本文介绍如何在[OpenAPI Explorer](https://next.api.aliyun.com/api/)调用函数计算的API和SDK。

## 前提条件

[创建函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/function-instance-1/ "")

## 调用API

1. 登录[OpenAPI Explorer](https://next.api.aliyun.com/api/)。

2. 在顶部菜单栏，单击 **选择云产品**，在搜索框输入 **函数计算**，在搜索结果中选择 **函数计算3.0**。

3. 在左侧导航栏，找到 **调用函数InvokeFunction**。

4. 填写以下参数，单击 **发起调用**，执行完成后在 **调用结果** 页签查看执行结果。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4444045171/p798646.png)

参数说明如下。




| 参数名称 | 解释说明 |
| --- | --- |



|     |     |
| --- | --- |
| 参数名称 | 解释说明 |
| **服务地址** | 选择您要执行的函数所在的地域。 |
| **X-Fc-Invocation-Type** | 填写函数调用类型。取值说明如下：<br>   - Sync：同步调用<br>     <br>   - Async：异步调用 |
| **functionName** | 填写函数名称。 |


## 调用SDK

1. 登录[OpenAPI Explorer](https://next.api.aliyun.com/api/)。

2. 在顶部菜单栏，单击 **选择云产品**，在搜索框输入 **函数计算**，在搜索结果中选择 **函数计算3.0**。

3. 在左侧导航栏，找到 **调用函数InvokeFunction**。

4. 填写以下参数，然后在 **SDK示例** 页签选择对应的语言，系统自动为您生成示例代码。单击 **运行示例**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4444045171/p798675.png)

参数说明如下。




| 参数名称 | 解释说明 |
| --- | --- |



|     |     |
| --- | --- |
| 参数名称 | 解释说明 |
| **服务地址** | 选择您要执行的函数所在的地域。 |
| **X-Fc-Invocation-Type** | 填写函数调用类型。取值说明如下：<br>   - Sync：同步调用<br>     <br>   - Async：异步调用 |
| **functionName** | 填写函数名称。 |


执行完成后，在下方 **阿里云云命令行** 区域查看执行结果。