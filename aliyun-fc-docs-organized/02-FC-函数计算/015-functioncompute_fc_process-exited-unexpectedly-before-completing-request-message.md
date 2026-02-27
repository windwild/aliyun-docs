### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[常见问题](https://help.aliyun.com/zh/functioncompute/fc/faq-3-0/)[代码开发FAQ](https://help.aliyun.com/zh/functioncompute/fc/faq-about-code-development-1/)[自定义运行时FAQ](https://help.aliyun.com/zh/functioncompute/fc/faq-about-custom-runtimes/)函数执行异常退出，报错Process exited unexpectedly before completing request怎么办？

# 函数执行异常退出，报错Process exited unexpectedly before completing request怎么办？

更新时间：2024-12-11 05:16:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：当我使用浏览器或cURL方式访问函数时出现404怎么办？](https://help.aliyun.com/zh/functioncompute/fc/404-error-occurs-when-i-use-a-browser-or-curl-tool-to-access-a-function-1)[下一篇：如何使用函数计算的WebIDE转换文件格式？](https://help.aliyun.com/zh/functioncompute/fc/how-to-convert-file-formats-by-using-webide-provided-by-function-compute)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

HTTP Server连接主动关闭

解决方案

函数本身的原因导致进程退出

解决方案

实例内存不足导致程序OOM

解决方案

启动命令缺少可执行权限、文件不存在、文件格式错误

解决方案

发生实例进程异常退出的错误，可能存在以下问题，您可以根据不同的问题采用不同的解决方案。

1. [HTTP Server连接主动关闭](https://help.aliyun.com/zh/functioncompute/fc/process-exited-unexpectedly-before-completing-request-message#eed6594d79l2l "")。

2. [函数本身原因导致进程退出](https://help.aliyun.com/zh/functioncompute/fc/process-exited-unexpectedly-before-completing-request-message#cause-lat-t0y-i3f "")。

3. [实例内存不足导致进程OOM](https://help.aliyun.com/zh/functioncompute/fc/process-exited-unexpectedly-before-completing-request-message#5525e84a0emec "")。

4. [启动命令缺少可执行权限、文件不存在、文件格式错误](https://help.aliyun.com/zh/functioncompute/fc/process-exited-unexpectedly-before-completing-request-message#fba6a287073o4 "")。


## **HTTP Server连接主动关闭**

HTTP Server连接主动关闭，主动关闭的可能原因如下：

- 连接未设置Keep-Alive。

- 空闲一段时间后，主动关闭。

- 读写超时或出错时关闭。


## 解决方案

当前的函数计算使用Keep-Alive连续访问自定义运行时内的HTTP Server，对于幂等请求例如GET、HEAD、OPTIONS或TRACE等，在连接失败时例如`EOF`、`connection reset by peer`等，会主动重试。但对于非幂等请求例如POST、PATCH等，在连接失败时会直接返回502报错。为避免502报错，自定义运行时的服务端需要设置以下两类参数：

- 将连接模式Connection设置为Keep-Alive。

- 关闭IDLE超时时间或将IDLE超时时间设置为15分钟以上。


对于不同的HTTP Server框架以上两种参数的配置方式可能会不一样，例如GoFrame框架，不仅需要将`SetIdletimeout`设置为0，还需要设置`ReadTimeout`和`python uvicorn`参数，`python uvicorn`还需要在命令行中设置`--timeout-keep-alive`等参数。建议您自行验证，对于Keep-Alive模式的HTTP客户端在进行稀疏性调用时，是否会触发HTTP server主动关闭连接。

## **函数本身的原因导致进程退出**

函数本身的原因导致进程退出，可能原因如下：

- 主动调用`exit`等接口退出。

- 运行过程中出现的`exception`未被捕获。


示例代码如下。您可以增加日志功能，根据日志调试解决。

```plaintext
# -*- coding: utf-8 -*-
import os
import logging

def handler(event, context):
    logger = logging.getLogger()
    logger.info('something is wrong')
    os._exit(-1)
    return 'hello world'
```

## 解决方案

您可以按照以下方式检查您的代码：

- 检查您的代码中是否存在主动退出的逻辑。

- 在运行环境进程顶层增加异常捕获或覆盖，避免发生`exception`时进程退出。


强烈建议不要在代码中直接使用os.\_exist(-1)等方式退出进程，该方式导致函数计算侧无法获取到退出时的堆栈信息。

建议使用抛出异常的方式，或者在退出进程前，手动打印堆栈到日志。

## **实例内存不足导致程序OOM**

实例内存不足导致程序OOM，可以分析函数计算控制台“日志”界面的请求内存用量（需要开启日志的请求级别指标）。请参见 [请求级别指标日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/request-level-metric-logs "")。

## **解决方案**

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **函数**。

2. 在顶部菜单栏，选择地域，然后在 **函数** 页面，单击目标函数。

3. 在函数详情页面，选择 **配置** 页签，然后在左侧选择 **基础配置**。

4. 在 **基础配置** 页面点击 **编辑**，增加内存规格，点击 **部署**。


## **启动命令缺少可执行权限、文件不存在、文件格式错误**

启动命令问题，可能原因如下：

- 启动命令缺少可执行权限。

- 启动命令指定的文件不存在。

- 文件格式错误。


## **解决方案**

详见请参见 [自定义运行时错误处理](https://help.aliyun.com/zh/functioncompute/fc/user-guide/troubleshooting-2#section-4er-gi7-4rk "")。