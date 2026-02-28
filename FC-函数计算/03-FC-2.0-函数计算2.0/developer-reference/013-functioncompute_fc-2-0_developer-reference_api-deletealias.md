### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[别名](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/alias/)DeleteAlias

# DeleteAlias

更新时间：2025-08-20 04:22:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CreateAlias](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-createalias)[下一篇：UpdateAlias](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-updatealias)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

请求头

请求语法

请求参数

示例

错误码

调用DeleteAlias接口删除别名。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC&api=DeleteAlias&type=ROA&version=2020-09-30)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```plaintext
DELETE /services/{serviceName}/aliases/{aliasName}
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 服务的名称。 |
| aliasName | String | Path | 是 | alias\_test | 别名的名称。 |

## 示例

请求示例

```plaintext
DELETE /2016-08-15/services/service_name/aliases/alias_test HTTP/1.1
公共请求头
```

正常返回示例

`JSON` 格式

```plaintext
HTTP/1.1 204 No Content
公共响应头
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC) 查看更多错误码。