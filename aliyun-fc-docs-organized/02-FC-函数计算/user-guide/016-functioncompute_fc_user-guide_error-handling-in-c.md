### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[开发与执行环境](https://help.aliyun.com/zh/functioncompute/fc/user-guide/development-and-execution-environment/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc/user-guide/code-development/)[C#](https://help.aliyun.com/zh/functioncompute/fc/user-guide/csharp-1-1/)错误处理

# 错误处理

更新时间：2024-07-18 05:59:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/log-management-1-2)[下一篇：函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-5)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

函数抛出异常

函数主动退出

本文介绍C#运行环境发生错误信息时，函数计算如何处理 。

## 函数抛出异常

如果您的函数在执行过程中抛出异常，函数计算会捕获并返回异常信息。

示例代码如下。

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aliyun.Serverless.Core;
using Microsoft.Extensions.Logging;

namespace Example
{
    public class Hello
    {
        public async void StreamHandler(Stream input, IFcContext context)
        {
            throw new Exception("oops");
        }

        static void Main(string[] args){}
    }
}
```

调用函数时收到的响应如下所示。

```plaintext
{
    "errorMessage": "oops",
    "errorType": "System.Exception",
    "stackTrace": [...]
}
```

发生异常时，函数调用相应的HTTP Header中会包含X-Fc-Error-Type`UnhandledInvocationError`。关于函数计算错误类型的更多信息，请参见 [基础信息](https://help.aliyun.com/zh/functioncompute/fc/user-guide/basics#section-cgk-2tl-g4v "")。

## 函数主动退出

通过主动退出运行中的函数获取错误信息时，无法获取退出时的报错信息和堆栈信息。不推荐使用该方法。

示例代码如下。

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aliyun.Serverless.Core;
using Microsoft.Extensions.Logging;

namespace Example
{
    public class Hello
    {
        public async void StreamHandler(Stream input, IFcContext context)
        {
            System.Environment.Exit(1);
        }

        static void Main(string[] args){}
    }
}
```

调用函数时收到的响应如下所示。

```plaintext
{
    "errorMessage": "Process exited unexpectedly before completing request (duration: 45ms, maxMemoryUsage: 49MB)"
}
```