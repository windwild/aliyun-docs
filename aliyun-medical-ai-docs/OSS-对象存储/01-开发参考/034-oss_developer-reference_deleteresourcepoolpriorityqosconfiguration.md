### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[API参考](https://help.aliyun.com/zh/oss/developer-reference/api-reference/)[关于资源池QoS操作](https://help.aliyun.com/zh/oss/developer-reference/resource-pool-qos-operations/)DeleteResourcePoolPriorityQosConfiguration

# DeleteResourcePoolPriorityQosConfiguration

更新时间：2025-11-11 03:39:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

SDK

命令行工具ossutil

调用`DeleteResourcePoolPriorityQosConfiguration`接口删除指定资源池中Bucket与BucketGroup的优先级流控配置，停止对该资源池的服务质量控制策略。

### 请求语法

```http
DELETE /?priorityQos&resourcePool=ResoucePoolName
Host: oss-cn-hangzhou.aliyuncs.com
Date: Fri, 10 Oct 2025 07:38:42 GMT
Content-Type: application/xml
Content-Length: content length
```

### 请求元素

| **名称** | **类型** | **参数位置** | **描述** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **参数位置** | **描述** |
| resourcePool | 字符串 | Query | 待删除优先级流控配置的目标资源池名称 |

### 示例

- 请求示例















```http
DELETE /?priorityQos&resourcePool=ResoucePoolName
Host: oss-cn-shanghai.aliyuncs.com
Date: Fri, 10 Oct 2025 07:38:42 GMT
Content-Type: application/xml
Content-Length: content length
```

- 响应示例















```http
HTTP/1.1 204 OK
Date: Fri, 10 Oct 2025 07:38:42 GMT
Content-Type: application/xml
Content-Length: 0
```


## **SDK**

DeleteResourcePoolPriorityQosConfiguration接口所对应的各语言SDK如下：

- [Go V2](https://help.aliyun.com/zh/oss/developer-reference/resource-pool-qos-management-using-oss-sdk-for-go-v2#0dc79073ca4ay "")


## **命令行工具ossutil**

DeleteResourcePoolPriorityQosConfiguration接口所对应的ossutil命令，请参见 [delete-resource-pool-priority-qos-configuration](https://help.aliyun.com/zh/oss/developer-reference/delete-resource-pool-priority-qos-configuration "")。