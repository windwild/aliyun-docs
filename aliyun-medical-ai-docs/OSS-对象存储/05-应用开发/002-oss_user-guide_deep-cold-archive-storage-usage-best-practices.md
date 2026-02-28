### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[成本优化](https://help.aliyun.com/zh/oss/user-guide/expense-optimization/)[存储类型](https://help.aliyun.com/zh/oss/user-guide/overview-53/)深度冷归档存储使用最佳实践

# 深度冷归档存储使用最佳实践

更新时间：2024-04-08 05:53:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：转换存储类型](https://help.aliyun.com/zh/oss/user-guide/convert-storage-classes)[下一篇：生命周期](https://help.aliyun.com/zh/oss/user-guide/overview-54/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

通过生命周期将Object的存储类型转换为深度冷归档存储

通过生命周期删除深度冷归档存储类型Object

满足Object的最低存储时间要求

深度冷归档存储提供高持久性、低成本的对象存储服务，适用于需要超长时间存放的极冷数据。本文介绍使用深度冷归档存储的最佳实践，避免产生额外费用，帮助您更经济地使用深度冷归档存储。

## **通过生命周期将Object的存储类型转换为深度冷归档存储**

为避免产生较高的PUT类型请求费用，建议您先上传标准存储的Object，然后通过生命周期转换为深度冷归档存储，不建议您直接上传深度冷归档存储的Object。通过生命周期转换为深度冷归档存储时，按Object源存储类型的PUT类型请求次数计费，即按照标准存储的PUT类型请求次数计费。

以华东1（杭州）地域为例，不同存储类型的PUT类型请求次数单价如下。

| **存储类型** | **PUT类型请求单价** |
| --- | --- |

|     |     |
| --- | --- |
| **存储类型** | **PUT类型请求单价** |
| 标准存储 | 0.01元/万次 |
| 深度冷归档存储 | 3.5元/万次 |

如何使用生命周期转换Object的存储类型，请参见 [生命周期规则概述](https://help.aliyun.com/zh/oss/user-guide/overview-54/#t2118096.html "")。

## **通过生命周期删除深度冷归档存储类型Object**

手动删除深度冷归档存储类型Object调用的是DeleteObject接口，成功调用一次DeleteObject接口计算一次Put类请求费用。为避免删除深度冷归档存储类型Object时产生Put类请求费用，建议您配置生命周期实现自动删除。通过生命周期自动删除深度冷归档Object调用的是ExpireObject接口，不收取Put类请求费用。

关于Put类请求费用的更多信息，请参见 [Put类请求](https://help.aliyun.com/zh/oss/api-operation-calling-fees#section-0h5-sdd-8t2 "")。

## 满足Object的最低存储时间要求

为避免产生不足规定时长容量费用，建议您将Object转换为深度冷归档存储时，确保Object满足转换前后的存储类型的最低存储时间要求。

不同存储类型的最低存储时间要求如下。

| **存储类型** | **最低存储时间** |
| --- | --- |

|     |     |
| --- | --- |
| **存储类型** | **最低存储时间** |
| 低频访问 | 30天 |
| 归档存储 | 60天 |
| 冷归档存储 | 180天 |
| 深度冷归档存储 | 180天 |

关于不足规定时长容量费用的更多信息，请参见 [存储费用](https://help.aliyun.com/zh/oss/storage-fees "")。