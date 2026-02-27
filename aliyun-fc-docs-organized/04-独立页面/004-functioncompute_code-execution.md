### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 代码执行

# 代码执行

更新时间：2025-07-22 22:46:30

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

定义

前置条件

节点配置

使用场景

结构化数据处理

数学计算

拼接数据

## **定义**

代码节点支持您在工作流中运行 Python 或 NodeJS 代码，从而实现强大的数据转换功能。它能极大简化您的工作流程，特别适用于 **算术运算、JSON 转换、文本处理** 等场景。

该节点赋予开发者极高的灵活性，允许您在工作流中嵌入自定义的 Python 或 JavaScript 脚本，以预设节点无法比拟的方式操作变量。通过简单的配置，您可以指定所需的 **输入变量** 和 **输出变量**，并编写相应的执行代码。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6697323571/p983440.png)

## **前置条件**

[创建AI Studio服务](https://help.aliyun.com/zh/cap/user-guide/create-an-ai-studio-service/ "")

## **节点配置**

点击 **开始** 后面的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9497323571/p983665.png)添加 **代码执行** 节点。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4597323571/p983723.png)

如果你需要在代码节点中使用其他节点的变量，你需要在`输入变量`中定义变量名，并引用这些变量。

## 使用场景

使用代码节点，你可以完成以下常见的操作。

### 结构化数据处理

在工作流中，经常要面对非结构化的数据处理，如JSON字符串的解析、提取、转换等。最典型的例子就是HTTP节点的数据处理，在常见的API返回结构中，数据可能会被嵌套在多层JSON对象中，而我们需要提取其中的某些字段。代码节点可以帮助你完成这些操作，下面是一个简单的例子，它从HTTP节点返回的JSON字符串中提取了 **data.name** 字段：

```plaintext
def main(http_response: str) -> dict:
    import json
    data = json.loads(http_response)
    return {
        # 注意在输出变量中声明result
        'result': data['data']['name']
    }
```

### 数学计算

当工作流中需要进行一些复杂的数学计算时，也可以使用代码节点。例如，计算一个复杂的数学公式，或者对数据进行一些统计分析。下面是一个简单的例子，它计算了一个数组的平方差。

```plaintext
def main(x: list) -> dict:
    return {
        # 注意在输出变量中声明result
        'result' : sum([(i - sum(x) / len(x)) ** 2 for i in x]) / len(x)
    }
```

### 拼接数据

有时，也许你需要拼接多个数据源，如多个知识检索、数据搜索、API调用等，代码节点可以帮助你将这些数据源整合在一起。下面是一个简单的例子，它将两个知识库的数据合并在一起。

```plaintext
def main(knowledge1: list, knowledge2: list) -> dict:
    return {
        # 注意在输出变量中声明result
        'result': knowledge1 + knowledge2
    }
```