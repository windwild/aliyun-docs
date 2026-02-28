### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[日志数据采集（Log）](https://help.aliyun.com/zh/sls/sls-log-collection/)[云产品日志采集](https://help.aliyun.com/zh/sls/collection-of-alibaba-cloud-service-logs/)[轻量消息队列（原 MNS）操作日志](https://help.aliyun.com/zh/sls/mns-operations-logs-usage-notes/)日志字段详情

# 日志字段详情

更新时间：2024-09-18 03:49:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：开启日志功能](https://help.aliyun.com/zh/sls/enable-logging)[下一篇：云渲染GCS会话数据](https://help.aliyun.com/zh/sls/graphic-computing-service-session-data-usage-notes/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

队列消息操作日志

主题消息操作日志

本文介绍轻量消息队列（原 MNS）的队列消息操作日志和主题消息操作日志的字段详情。

## 队列消息操作日志

队列消息操作日志是指操作队列消息所产生的日志，例如发送消息、消费消息、删除消息等操作。一条消息操作日志中包含多个字段，每个字段都有自己的含义。根据操作的不同，消息操作日志所包含的字段也不相同。以下分别介绍各个字段的含义和不同操作所包含的字段信息。

- 日志字段解析

一条消息操作日志中包含多个字段，各个字段的含义如下：




| **字段** | **含义** |
| --- | --- |



|     |     |
| --- | --- |
| **字段** | **含义** |
| Time | 本次操作的发生时间。 |
| MessageId | 消息的MessageId，标识本次操作处理的消息。 |
| QueueName | 本次操作对应的队列名称。 |
| AccountId | 本次操作对应队列的账号。 |
| RemoteAddress | 发起该操作的客户端地址。 |
| NextVisibleTime | 该操作执行完成后，这条消息的下次可见时间。 |
| ReceiptHandleInRequest | 客户端执行该操作时传入的ReceiptHandle参数。 |
| ReceiptHandleInResponse | 该操作执行完成后，返回客户端的ReceiptHandle。 |
| ProcessTime | 本次操作的处理时间。 |
| RequestId | 本次执行的任务ID。 |
| Action | 表示动作，例如：删除、发送等。 |

- 各个操作的字段列表

不同操作的日志包含的字段信息各不相同，具体每个操作包含的字段如下：




| **操作** | **Time** | **QueueName** | **AccountId** | **MessageId** | **RemoteAddress** | **NextVisibleTime** | **ReceiptHandleInResponse** | **ReceiptHandleInRequest** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |



|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **操作** | **Time** | **QueueName** | **AccountId** | **MessageId** | **RemoteAddress** | **NextVisibleTime** | **ReceiptHandleInResponse** | **ReceiptHandleInRequest** |
| SendMessage/BatchSendMessage | 有 | 有 | 有 | 有 | 有 | 有 | 无 | 无 |
| PeekMessage/BatchPeekMessage | 有 | 有 | 有 | 有 | 有 | 无 | 无 | 无 |
| ReceiveMessage/BatchReceiveMessage | 有 | 有 | 有 | 有 | 有 | 有 | 有 | 无 |
| ChangeMessageVisibility | 有 | 有 | 有 | 有 | 有 | 有 | 有 | 有 |
| DeleteMessage/BatchDeleteMessage | 有 | 有 | 有 | 有 | 有 | 有 | 无 | 有 |


## 主题消息操作日志

主题消息操作日志是指操作主题消息产生的日志，主要有两类：发布消息和推送消息。以下分别介绍主题消息操作日志各个字段的含义，以及不同的操作所包含的字段信息。

- 日志字段解析

一条消息操作日志中包含多个字段，各个字段的含义如下：




| **字段** | **含义** |
| --- | --- |



|     |     |
| --- | --- |
| **字段** | **含义** |
| Time | 本次操作的发生时间。 |
| MessageId | 消息的MessageId，标识本次操作处理的消息。 |
| TopicName | 本次操作对应的主题名称。 |
| SubscriptionName | 本次操作对应的订阅名称。 |
| AccountId | 本次操作对应主题的账号。 |
| RemoteAddress | 发起该操作的客户端地址。 |
| NotifyStatus | 轻量消息队列（原 MNS）将消息推送给用户时，用户返回的状态码或者相应的出错信息。 |
| ProcessTime | 本次操作的处理时间。 |
| MessageTag | 设置的消息标签。 |
| RequestId | 本次执行的任务ID。 |
| Action | 表示动作，例如：删除、发送等。 |

- 各个操作的字段列表

不同操作的日志包含的字段信息各不相同，具体每个操作包含的字段如下：




| **操作** | **Time** | **MessageId** | **TopicName** | **SubscriptionName** | **AccountId** | **RemoteAddress** | **NotifyStatus** | **SubscriptionName** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |



|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **操作** | **Time** | **MessageId** | **TopicName** | **SubscriptionName** | **AccountId** | **RemoteAddress** | **NotifyStatus** | **SubscriptionName** |
| PublishMessage | 有 | 有 | 有 | 无 | 有 | 有 | 无 | 无 |
| Notify | 有 | 有 | 有 | 有 | 有 | 无 | 有 | 有 |

- NotifyStatus

NotifyStatus是推送消息日志特有的字段，可以协助您调查轻量消息队列（原 MNS）推送消息到Endpoint失败的原因。 根据不同的NotifyStatus，您可以按照下表建议的处理方法进行处理。




| **错误码** | **描述** | **建议处理方法** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **错误码** | **描述** | **建议处理方法** |
| 2xx | 消息推送成功。 | 无。 |
| 其它HTTP状态码 | 消息推送给用户，Endpoint返回了非2xx的状态码。 | 检查Endpoint端处理逻辑。 |
| InvalidHost | 订阅指定的Endpoint不合法。 | 确认订阅中Endpoint是否真实有效，可使用curl或telnet进行确认。 |
| ConnectTimeout | 连接订阅指定的Endpoint超时。 | 确认订阅中Endpoint当前是否可访问，可使用curl或telnet进行确认。 |
| ConnectFailure | 连接订阅指定的Endpoint失败。 | 确认订阅中Endpoint当前是否可访问，可使用curl或telnet进行确认。 |
| UnknownError | 未知错误。 | 请联系轻量消息队列（原 MNS）技术人员支持。 |