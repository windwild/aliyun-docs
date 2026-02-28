### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/trigger/)DeleteTrigger

# DeleteTrigger

更新时间：2025-08-20 04:20:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：CreateTrigger](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-createtrigger)[下一篇：UpdateTrigger](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-updatetrigger)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

请求头

请求语法

请求参数

示例

错误码

调用DeleteTrigger接口删除触发器。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC-RAM&api=DeleteTrigger&type=ROA&version=2021-06-22)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

| **名称** | **类型** | **是否必选** | **示例** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **示例** | **描述** |
| If-Match | String | 否 | e19d5cd5af0378da05f63f891c74\*\*\*\* | 用于确保实际更改的资源和期望更改的资源是一致的，该值来自 [CreateTrigger](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-createtrigger)、 [GetTrigger](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-gettrigger) 和 [UpdateTrigger](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-updatetrigger) 的响应。 |

## 请求语法

```plaintext
DELETE /services/{serviceName}/functions/{functionName}/triggers/{triggerName} HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| serviceName | String | Path | 是 | service\_name | 服务的名称。 |
| functionName | String | Path | 是 | function\_name | 函数的名称。 |
| triggerName | String | Path | 是 | trigger\_name | 需要删除的触发器名称。 |

无响应参数

## 示例

请求示例

```plaintext
DELETE /services/service_name/functions/function_name/triggers/trigger_name HTTP/1.1
Host:fc-ram.aliyuncs.com
If-Match:e19d5cd5af0378da05f63f891c74****
Content-Type:application/json
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC-RAM) 查看更多错误码。