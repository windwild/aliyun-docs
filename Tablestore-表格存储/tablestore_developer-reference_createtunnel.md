### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[API概览](https://help.aliyun.com/zh/tablestore/developer-reference/operation-summary-of-tablestore-api/)[通道服务操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-tunnel-service-operations/)CreateTunnel

# CreateTunnel

更新时间：2024-04-28 02:24:06

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：通道服务操作](https://help.aliyun.com/zh/tablestore/developer-reference/tablestore-api-for-tunnel-service-operations/)[下一篇：ListTunnel](https://help.aliyun.com/zh/tablestore/developer-reference/listtunnel)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求消息结构

响应消息结构

使用SDK

调用CreateTunnel接口为表创建一个数据通道。数据通道可用于实时消费表中数据。

## **请求消息结构**

```protobuf
message CreateTunnelRequest {
    required Tunnel tunnel = 1;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **tunnel** | [Tunnel](https://help.aliyun.com/zh/tablestore/developer-reference/tunnel "") | 是 | 通道配置信息。 |

## **响应消息结构**

```protobuf
message CreateTunnelResponse {
    required string tunnel_id = 1;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **tunnel\_id** | string | 是 | 通道ID，用于唯一标识一个通道。 |

## **使用SDK**

您可以使用如下语言的SDK创建通道。

- [Java SDK：创建通道](https://help.aliyun.com/zh/tablestore/developer-reference/create-tunnel-by-using-java-sdk "")

- [Go SDK：创建通道](https://help.aliyun.com/zh/tablestore/developer-reference/create-tunnel-by-using-go-sdk "")