### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) HTTP请求

# HTTP请求

更新时间：2025-07-22 22:46:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

定义

前置条件

支持的请求方法

可配置项

## **定义**

HTTP 请求节点允许您通过HTTP协议与外部服务进行交互。它支持多种常见的HTTP请求方法，并能灵活配置请求详情，适用于获取外部数据、触发Webhook、生成图片或下载文件等多种场景。

## **前置条件**

[创建AI Studio服务](https://help.aliyun.com/zh/cap/user-guide/create-an-ai-studio-service/ "")

## **支持的请求方法**

- **GET**：用于从服务器请求获取特定资源。

- **POST**：用于向服务器提交数据，例如提交表单或上传文件。

- **HEAD**：类似于GET请求，但服务器仅返回响应头，不返回资源主体。

- **PATCH**：用于对现有资源进行局部修改。

- **PUT**：用于向服务器上传资源，常用于更新或创建资源。

- **DELETE**：用于请求服务器删除指定的资源。


## **可配置项**

您可以根据需求配置HTTP请求的各个方面，包括：

- **URL**：目标网络地址。

- **请求头 (Headers)**：自定义HTTP请求头信息。

- **查询参数 (Query Parameters)**：URL中的查询字符串参数。

- **请求体 (Body)**：POST或PUT等请求方法中发送的数据内容。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0797323571/p983468.png)