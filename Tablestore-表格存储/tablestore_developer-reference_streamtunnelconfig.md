### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/)[API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/)[DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/)StreamTunnelConfig

# StreamTunnelConfig

更新时间：2024-04-28 02:24:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：StreamRecord](https://help.aliyun.com/zh/tablestore/developer-reference/streamrecord)[下一篇：StreamShard](https://help.aliyun.com/zh/tablestore/developer-reference/streamshard)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

数据结构

相关操作

表示通道stream的配置信息。

## **数据结构**

```protobuf
message StreamTunnelConfig {
    optional StartOffsetFlag flag = 1;
    optional uint64 startOffset = 2;
    optional uint64 endOffset = 3;
}
```

| **名称** | **类型** | **是否必选** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **是否必选** | **描述** |
| **flag** | [StartOffsetFlag](https://help.aliyun.com/zh/tablestore/developer-reference/startoffsetflag "") | 否 | 起始偏移量标记。 |
| **startOffset** | uint64 | 否 | 起始偏移量。 |
| **endOffset** | uint64 | 否 | 结束偏移量。 |

## **相关操作**

- [CreateTunnel](https://help.aliyun.com/zh/tablestore/developer-reference/createtunnel "")

- [ListTunnel](https://help.aliyun.com/zh/tablestore/developer-reference/listtunnel "")

- [DescribeTunnel](https://help.aliyun.com/zh/tablestore/developer-reference/describetunnel "")