### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[开发与执行环境](https://help.aliyun.com/zh/functioncompute/fc/user-guide/development-and-execution-environment/)[代码开发](https://help.aliyun.com/zh/functioncompute/fc/user-guide/code-development/)[Python](https://help.aliyun.com/zh/functioncompute/fc/user-guide/python/)错误处理

# 错误处理

更新时间：2023-09-12 05:31:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：日志](https://help.aliyun.com/zh/functioncompute/fc/user-guide/logging-2)[下一篇：函数实例生命周期回调方法](https://help.aliyun.com/zh/functioncompute/fc/user-guide/lifecycle-hooks-for-function-instances-1)

该文章对您有帮助吗？

反馈

本文介绍Python运行环境的错误处理相关内容。

如果函数在执行过程中抛出异常，那么函数计算会捕获并返回异常信息，示例如下所示。

```python
def my_handler(event, context):
    raise Exception('something is wrong')
```

发送异常时，函数调用响应的HTTP Header中会包含`X-Fc-Error-Type: UnhandledInvocationError`，HTTP请求体（Body）包含如下信息。函数计算的错误类型的更多信息，请参见 [错误处理](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/error-handling#task-2134831 "")。

```python
{
  "errorMessage": "something is wrong",
  "errorType": "Exception",
  "stackTrace": [\
    [\
      "File \"/code/index.py\"",\
      "line 2",\
      "in my_handler",\
      "raise Exception('something is wrong')"\
    ]\
  ]
}
```

异常信息包含如下三个字段：

| **字段** | **类型** | **解释说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **字段** | **类型** | **解释说明** |
| errorMessage | String | 异常信息。 |
| errorType | String | 异常类型。 |
| stackTrace | List | 异常堆栈。 |