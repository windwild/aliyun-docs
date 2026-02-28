### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/programming-languages/)[C#](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/csharp/)事件请求处理程序（Event Handler）

# 事件请求处理程序（Event Handler）

更新时间：2025-08-04 01:25:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：请求处理程序（Handler）](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/handler-1)[下一篇：HTTP请求处理程序（HTTP Handler）](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/http-handlers-4)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

处理程序接口

事件请求处理程序类型

Stream Handler

POCO Handler

自定义序列化接口（Custom Serializer）

示例程序

本文介绍C#事件请求处理程序的结构和特点。

## 处理程序接口

当您创建一个基于C#的函数时，需要指定一个Handler方法，该方法在函数执行时被执行。这个Handler方法可以是Static方法或Instance方法。如果您想在Handler方法中访问`IFcContext`对象，则需要将该方法中的第二个参数指定为`IFcContext`对象。事件函数支持的Handler方法定义如下所示。

```c
ReturnType HandlerName(InputType input, IFcContext context);  //包含IFcContext。
ReturnType HandlerName(InputType input); // 不包含IFcContext。
Async Task<ReturnType> HandlerName(InputType input, IFcContext context);
Async Task<ReturnType> HandlerName(InputType input);
```

函数计算支持在使用C#编写的函数中应用Async，此时函数的执行会等待异步方法执行结束。以下是对ReturnType、InputType和IFcContext的说明。

- ReturnType：返回对象可以是`void`、`System.IO.Stream`对象或者任何可以被JSON序列化和反序列化的对象。如果返回对象是Stream，该Stream内容将直接在响应体返回，否则返回对象被JSON序列化后，在响应体返回。
- InputType：输入参数可以是System.IO.Stream或任何可以被JSON序列化和反序列化的对象。
- IFcContext：函数的Context对象。更多信息，请参见 [上下文](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/context-1#concept-2258453 "")。

## 事件请求处理程序类型

函数计算使用C#编写函数，需要引入`Aliyun.Serverless.Core`依赖包，可以通过以下方式在.csproj文件中引入该依赖包。

```plaintext
  <ItemGroup>
        <PackageReference Include="Aliyun.Serverless.Core" Version="1.0.1" />
  </ItemGroup>
```

`Aliyun.Serverless.Core`包为事件请求处理程序定义了两个参数类型。

- Stream Handler
以流的方式接收输入的`event`事件并返回执行结果，您需要从输入流中读取调用函数时的输入，处理完成后把函数执行结果写入到输出流中来返回。

- POCO Handler
通过POCO（Plain old CLR objects）方式，您可以自定义输入和输出的类型，但是输入和输出的类型必须是POCO类型。


### Stream Handler

一个最简单的Stream Handler示例如下所示。


```plaintext
using System.IO;
using System.Threading.Tasks;
using Aliyun.Serverless.Core;
using Microsoft.Extensions.Logging;

namespace Example
{
    public class Hello
    {
        public async Task<Stream> StreamHandler(Stream input, IFcContext context)
        {
            IFcLogger logger = context.Logger;
            logger.LogInformation("Handle request: {0}", context.RequestId);
            MemoryStream copy = new MemoryStream();
            await input.CopyToAsync(copy);
            copy.Seek(0, SeekOrigin.Begin);
            return copy;
        }

        static void Main(string[] args){}
    }
}
```

示例解析如下。

- 命名空间和类
命名空间为`Example`，类名为`Hello`，方法名为`StreamHandler`，假设程序集名称为`HelloFcApp`，则请求处理程序的配置为`HelloFcApp::Example.Hello::StreamHandler`。

- 参数Stream input
处理程序的输入，该示例的输入类型为Stream。

- 参数IFcContext context（可选）
上下文对象，包含函数和请求的信息。

- 返回值Task<Stream>
返回值为Stream类型。


### POCO Handler

一个最简单的POCO Handler示例如下所示。


```plaintext
using Aliyun.Serverless.Core;
using Microsoft.Extensions.Logging;

namespace Example
{
    public class Hello
    {
        public class Product
        {
            public string Id { get; set; }
            public string Description { get; set; }
        }

        // optional serializer class, if it’s not specified, the default serializer (based on JSON.Net) will be used.
        // [FcSerializer(typeof(MySerialization))]
        public Product PocoHandler(Product product, IFcContext context)
        {
            string Id = product.Id;
            string Description = product.Description;
            context.Logger.LogInformation("Id {0}, Description {1}", Id, Description);
            return product;
        }

        static void Main(string[] args){}
    }
}
```

除了Stream作为输入输出参数，POCO（Plain old CLR objects）对象同样也可以作为输入和输出。如果该POCO没有指定特定的JSON序列化对象，则函数计算默认使用JSON.Net进行对象的JSON序列化和反序列化。具体解析如下。

- 命名空间和类
命名空间为`Example`，类名为`Hello`，方法名为`PocoHandler`，假设程序集名称为 `HelloFcApp`, 则请求处理程序的配置为`HelloFcApp::Example.Hello::PocoHandler`。

- 参数`Product product`
处理程序的输入，该示例的输入类型为`Product Class`。如果该POCO没有指定特定的JSON序列化对象，则函数计算默认使用JSON.Net进行对象的JSON反序列化。

- 参数IFcContext context（可选）
上下文对象，包含函数和请求的信息。

- 返回值`Product`
返回值为`POCO Product`类型。如果该POCO没有指定特定的JSON序列化对象，则函数计算默认使用JSON.Net进行对象的JSON序列化。


### 自定义序列化接口（Custom Serializer）

函数计算针对POCO Handler提供了默认的基于 [JSON .NET](https://www.newtonsoft.com/json) 的序列化接口。如果默认的序列化接口不能满足需求，您可以基于`Aliyun.Serverless.Core`中的接口`IFcSerializer`实现自定义序列化接口。

```c
public interface IFcSerializer
{
    T Deserialize<T>(Stream requestStream);
    void Serialize<T>(T response, Stream responseStream);
}
```

## 示例程序

函数计算官方库包含使用各种处理程序类型和接口的示例应用程序。每个示例应用程序都包含用于轻松编译部署的方法。

- [dotnet3-blank-stream-event](https://github.com/awesome-fc/code-example/tree/master/dotnet/dotnet3-blank-stream-event)：使用Stream格式的事件回调处理程序。
- [dotnet3-blank-poco-event](https://github.com/awesome-fc/code-example/tree/master/dotnet/dotnet3-blank-poco-event)：使用POCO格式的事件回调处理程序。