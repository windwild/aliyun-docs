### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[开发参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/)[API参考](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference-3/)[API参考（2016-08-15不推荐）](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-reference/)[层](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/layer/)PublishLayerVersion

# PublishLayerVersion

更新时间：2025-08-20 04:27:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：StopStatefulAsyncInvocation](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-stopstatefulasyncinvocation)[下一篇：DeleteLayerVersion](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-deletelayerversion)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

请求头

请求语法

请求参数

返回数据

示例

错误码

调用PublishLayerVersion接口发布层版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=FC&api=PublishLayerVersion&type=ROA&version=2020-09-30)

![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)
调试

## 请求头

该接口无特殊请求头，关于公共请求头信息，请参见 [公共参数](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/common-parameters)。

## 请求语法

```plaintext
POST /layers/{layerName}/versions/ HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **名称** | **类型** | **位置** | **是否必选** | **示例值** | **描述** |
| layerName | String | Path | 是 | Layer-name | 层的名称。 |
|  | Object | Body | 否 |  | 层的描述。 |
| code | [Code](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#Code "") | Body | 否 |  | 指定Code ZIP包。 |
| description | String | Body | 否 | Layer-description | 层的描述。 |
| compatibleRuntime | Array of String | Body | 否 | nodejs12 | 层支持的运行环境。当前支持**nodejs12**、**nodejs10**、**nodejs8**、**nodejs6**、**python3**及**python2.7**。 |

## 返回数据

| **名称** | **类型** | **示例值** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **示例值** | **描述** |
| ETag | String | e19d5cd5af0378da05f63f891c7467af | 确保实际修改的层和期望更改的层是一致的。 |
|  | [Layer](https://help.aliyun.com/zh/functioncompute/fc-2-0/developer-reference/api-common-data-structures#Layer "") |  | 层的模式响应。 |

## 示例

请求示例

```plaintext
POST /2016-08-15/layers/Layer-name/versions HTTP/1.1
公共请求头

{
  "code" : {
    "ossBucketName" : "demo-bucket",
    "ossObjectName" : "demo-key",
    "zipFile" : "cHJpbnQoImhlbGxvIHdvcmxkIikK"
  },
  "description" : "Layer-description",
  "compatibleRuntime" : [ "nodejs12" ]
}
```

正常返回示例

`JSON`格式

```plaintext
HTTP/1.1 200 OK
Content-Type:application/json

{
  "layerName" : "Layer-name",
  "version" : 1,
  "description" : "Layer-description",
  "code" : {
    "repositoryType" : "OSS",
    "location" : "https://xyz.oss-cnxxx.aliyuncs.com/xxx/xxx/xxx"
  },
  "codeSize" : 421,
  "codeChecksum" : "2825179536350****",
  "createTime" : "2020-11-11T11:08:00Z",
  "acl" : 0,
  "compatibleRuntime" : [ "python3" ],
  "arn" : "02f81d283888f5ec63442a88fe82b260#Layer-name#1"
}
```

## 错误码

访问 [错误中心](https://error-center.aliyun.com/status/product/FC) 查看更多错误码。