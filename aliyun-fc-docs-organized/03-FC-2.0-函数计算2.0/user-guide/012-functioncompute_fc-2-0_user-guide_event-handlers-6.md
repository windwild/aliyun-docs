### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/programming-languages/)[Go](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/go-1/)事件请求处理程序（Event Handler）

# 事件请求处理程序（Event Handler）

更新时间：2025-08-04 01:25:55

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用示例

Event Handler签名

Context

本文介绍Go事件请求处理程序的结构和特点。

## 使用示例

在Go语言的代码中，您需要引入官方的SDK库`github.com/aliyun/fc-runtime-go-sdk/fc`，并实现`handler`函数和`main`函数。示例如下：

```go
package main

import (
    "fmt"
    "context"

    "github.com/aliyun/fc-runtime-go-sdk/fc"
)

type StructEvent struct {
    Key string `json:"key"`
}

func HandleRequest(ctx context.Context, event StructEvent) (string, error) {
    return fmt.Sprintf("hello, %s!", event.Key), nil
}

func main() {
    fc.Start(HandleRequest)
}
```

传入的`event`参数是一个包含`key`属性的JSON字符串，示例如下。

```go
{
  "key": "value"
}
```

具体的示例解析如下：

- `package main`：在Go语言中，Go应用程序都包含一个名为`main`的包。

- `import`：需要引用函数计算依赖的包，主要包括以下包：

  - `github.com/aliyun/fc-runtime-go-sdk/fc`：函数计算Go语言的核心库。

  - `context`：函数计算Go语言的Context对象。
- `func HandleRequest(ctx context.Context, event StructEvent) (string, error)`：处理事件请求的方法（即Handler），需包含将要执行的代码，参数含义如下：

  - `ctx context.Context`：为您的FC函数调用提供在调用时的运行上下文信息。更多信息，请参见 [上下文](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/context#task-2183680 "")。

  - `event StructEvent`：调用函数时传入的数据，可以支持多种类型。

  - `string, error`：返回两个值，字符串和错误信息。更多信息，请参见 [错误处理](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/error-handling-7#task-2187177 "")。

  - `return fmt.Sprintf("hello，%s !", event.Key), nil`：简单地返回`hello`信息，其中包含传入的`event`。`nil`表示没有报错。
- `func main()`：运行FC函数代码的入口点，Go程序必须包含`main`函数。通过添加代码`fc.Start(HandleRequest)`，您的程序即可运行在阿里云函数计算平台。



**重要**





HTTP请求处理程序和事件请求处理程序的启动方法不同。如果是事件请求处理程序，您需要在`main`函数中调用`fc.Start`函数。如果是HTTP请求处理程序，您需要在`main`函数中调用`fc.StartHttp`函数。


## Event Handler签名

下面列举出了有效的Event Handler签名，其中`InputType`和`OutputType`与`encoding/json`标准库兼容。

函数计算会使用`json.Unmarshal`方法对传入的`InputType`进行反序列化，以及使用`json.Marshal`方法对返回的`OutputType`进行序列化。关于如何反序列化函数的返回数据，请参考 [JSON Unmarshal](https://pkg.go.dev/encoding/json#Unmarshal)。

- `func ()`

- `func () error`

- `func (InputType) error`

- `func () (OutputType, error)`

- `func (InputType) (OutputType, error)`

- `func (context.Context) error`

- `func (context.Context, InputType) error`

- `func (context.Context) (OutputType, error)`

- `func (context.Context, InputType) (OutputType, error)`


Event Handler的使用需遵循以下规则：

- Handler必须是一个函数。

- Handler支持0～2个输入参数。如果有2个参数，则第一个参数必须是`context.Context`。

- Handler支持0～2个返回值。如果有1个返回值，则必须是`error`类型；如果有2个返回值，则第2个返回值必须是`error`。


事件函数的Handler示例代码：

- [event-struct.go](https://github.com/aliyun/fc-runtime-go-sdk/blob/master/examples/event-struct.go)：`event`为Struct类型的示例代码。

- [event-string.go](https://github.com/aliyun/fc-runtime-go-sdk/blob/master/examples/event-string.go)：`event`为String类型的示例代码。

- [event-map.go](https://github.com/aliyun/fc-runtime-go-sdk/blob/master/examples/event-map.go)：`event`为`map[string]interface{}`类型的示例代码。


更多Handler示例，请参见 [examples](https://github.com/aliyun/fc-runtime-go-sdk/tree/master/examples)。

## Context

Context的详细使用方法，请参见 [上下文](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/context#task-2183680 "")。