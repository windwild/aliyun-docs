### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[CloudLens](https://help.aliyun.com/zh/sls/cloudlens-46/)[CloudLens for CLB（原SLB日志中心）](https://help.aliyun.com/zh/sls/cloudlens-for-clb-usage-notes/)日志字段详情

# 日志字段详情

更新时间：2024-01-23 02:38:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：指标说明](https://help.aliyun.com/zh/sls/metrics-4)[下一篇：智能异常分析](https://help.aliyun.com/zh/sls/intelligent-anomaly-analysis/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

访问日志

审计配置日志

云监控事件

本文介绍负载均衡7层访问日志、配置审计日志和云监控日志的字段详情。

## 访问日志

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为slb\_layer7\_access\_log。 |
| body\_bytes\_sent | 发送给客户端的http body字节数。 |
| client\_ip | 请求客户端IP地址。 |
| host | 优先从请求参数中获取host，如果获取不到则从host header取值，如果还是获取不到则以处理请求的后端服务器IP地址作为host。 |
| http\_host | 请求报文host header的内容。 |
| http\_referer | Proxy收到的请求报文中HTTP的referer header的内容。 |
| http\_user\_agent | Proxy收到的请求报文中HTTP的user-agent header的内容。 |
| http\_x\_forwarded\_for | Proxy收到的请求报文中x-forwarded-for header的内容。 |
| http\_x\_real\_ip | 真实的客户端IP地址。 |
| read\_request\_time | Proxy读取请求的时间，单位：毫秒。 |
| request\_length | 请求报文的长度，包括startline、http header和http body。 |
| request\_method | 请求报文的方法。 |
| request\_time | Proxy收到第一个请求报文的时间到proxy返回应答之间的间隔时间，单位：秒。 |
| request\_uri | Proxy收到的请求报文的URI。 |
| scheme | 请求的schema，包括http、https。 |
| server\_protocol | Proxy收到的HTTP协议的版本，例如HTTP/1.0或HTTP/1.1。 |
| slb\_vport | 负载均衡的监听端口。 |
| slbid | 负载均衡实例ID。 |
| ssl\_cipher | 建立SSL连接使用的密码，例如ECDHE-RSA-AES128-GCM-SHA256等。 |
| ssl\_protocol | 建立SSL连接使用的协议，例如TLSv1.2。 |
| status | Proxy应答报文的状态。 |
| tcpinfo\_rtt | 客户端TCP连接时间，单位：微秒。 |
| time | 日志记录时间。 |
| upstream\_addr | 后端服务器的IP地址和端口。 |
| upstream\_response\_time | 从负载均衡向后端建立连接开始到接收完数据然后关闭连接为止的时间，单位：秒。 |
| upstream\_status | Proxy收到的后端服务器的响应状态码。 |
| vip\_addr | 虚拟IP地址。 |
| write\_response\_time | Proxy收到后端的请求后，把这个请求发送给客户端的时间。单位：毫秒。 |

## 审计配置日志

- 配置变更记录




| **字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **字段** | **说明** |
| accountId | 资源归属的阿里云账号ID。 |
| arn | RAM角色标识。 |
| availabilityZone | 资源可用区。 |
| captureTime | 记录资源合规评估的时间戳。单位：毫秒。 |
| configuration | 资源关联的规则列表和规则合规详情。 |
| configurationDiff | 触发本次评估的资源变更细节。 |
| dataType | 事件类型，固定为ConfigurationItemChangeNotification。 |
| regionId | 地域ID。 |
| relationship | 相关资源的详细信息，包括相关资源所在地域ID、资源关系、资源ID和资源类型。 |
| relationshipDiff | 触发本次评估的资源变更细节。 |
| requestId | 请求ID。 |
| resourceCreateTime | 创建资源的时间戳。单位：毫秒。 |
| resourceEventType | 资源事件。 |
| resourceGroupId | 资源组。 |
| resourceId | 资源ID。 |
| realResourceId | 一级资源ID。 |
| resourceName | 资源名。 |
| resourceStatus | 资源状态。 |
| resourceType | 资源类型。 |
| serviceName | 服务名。 |
| tags | 资源标签。 |
| version | 版本号。 |

- 资源不合规事件




| **字段** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **字段** | **说明** |
| accountId | 资源归属的阿里云账号ID。 |
| annotation | 描述信息。 |
| riskLevel | 风险水平。包括：1：高风险。2：中风险。3：低风险。 |
| dataType | 不合规事件，固定为NonCompliantNotification。 |
| evaluationResultIdentifier | 资源评估结果标识符。 |
| eventType | 事件类型。 |
| invokingEventMessageType | 规则触发机制。 |
| complianceType | 规则合规评估结果。包括：COMPLIANT：合规。NON\_COMPLIANT：不合规。NOT\_APPLICABLE：不适用。INSUFFICIENT\_DATA：无数据。 |
| requestId | 请求ID。 |
| eventName | 事件名称。 |
| notificationCreationTime | 创建通知的时间。 |
| regionId | 地域ID。 |
| resourceId | 资源ID。 |
| resourceType | 资源类型。 |
| serviceName | 服务名。 |


## 云监控事件

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| event\_id | 云监控事件ID。 |
| source | 事件源。一般包含事件源的类型，发布事件的机制或生产事件的过程。 |
| version | CloudEvents协议版本。 |
| publish\_time | 事件推送时间。 |
| type | 事件类型，描述事件源相关的事件类型。 |
| data | 事件内容。JSON对象，内容由发起事件的服务决定。 |
| data\_type | 云监控事件。 |
| region | 事件所在地域。 |
| account\_id | 事件所属的阿里云账号ID。 |