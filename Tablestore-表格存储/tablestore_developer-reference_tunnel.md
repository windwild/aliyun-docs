### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)Tunnel

# Tunnel

更新时间：2024-04-28 02:24:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：TopRowsAggregation](https://help.aliyun.com/zh/tablestore/developer-reference/toprowsaggregation)[下一篇：TunnelInfo](https://help.aliyun.com/zh/tablestore/developer-reference/tunnelinfo)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

相关操作

表示通道的配置信息。

## **数据结构**

```protobuf
message Tunnel {
    required string table_name = 1;
    required string tunnel_name = 3;
    required TunnelType tunnel_type = 4;
    optional StreamTunnelConfig StreamTunnelConfig = 5;
}
```

| **参数** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数** | **类型** | **是否必选** | **描述** |
| table\_name | string | 是 | 表名称。 |
| tunnel\_name | string | 是 | 通道名称。 |
| tunnel\_type | [TunnelType](https://help.aliyun.com/zh/tablestore/developer-reference/tunneltype "") | 是 | 通道类型。 |
| StreamTunnelConfig | [StreamTunnelConfig](https://help.aliyun.com/zh/tablestore/developer-reference/streamtunnelconfig "") | 否 | 通道stream的配置信息。 |

## **相关操作**

[CreateTunnel](https://help.aliyun.com/zh/tablestore/developer-reference/createtunnel "")