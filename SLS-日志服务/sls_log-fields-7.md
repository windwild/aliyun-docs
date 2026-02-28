### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[日志数据采集（Log）](https://help.aliyun.com/zh/sls/sls-log-collection/)[云产品日志采集](https://help.aliyun.com/zh/sls/collection-of-alibaba-cloud-service-logs/)[IoT日志](https://help.aliyun.com/zh/sls/iot-platform-logs-usage-notes/)日志字段详情

# 日志字段详情

更新时间：2024-04-22 22:27:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：开通日志转储功能](https://help.aliyun.com/zh/sls/enable-the-log-dump-feature)[下一篇：微服务引擎MSE访问日志](https://help.aliyun.com/zh/sls/mse-access-logs-usage-notes/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

参数说明

本文介绍IoT日志字段详情。

## **参数说明**

| **参数名称** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数名称** | **说明** |
| requestId | 消息请求ID。 |
| time | 日志打印时间。 |
| utcTime | 日志打印时间的UTC时间。 |
| traceId | 追踪ID，可用于追踪消息流转路径。 |
| messageId | 消息ID。 |
| instanceId | 物联网平台实例ID。 |
| uid | 阿里云账号ID。 |
| productKey | 产品标识符。 |
| deviceName | 设备名称。 |
| bizCode | 业务类型。 |
| operation | 业务类型相应的操作名称、API名称、服务的method或消息的Topic。<br>操作名称具体说明，请参见 [云端运行日志的字段说明](https://help.aliyun.com/zh/iot/user-guide/iot-platform-logs#section-fjz-ngs-bon "")。API名称的具体说明，请参见 [API列表](https://help.aliyun.com/zh/iot/developer-reference/list-of-operations-by-function#reference-kd4-l4z-wdb "")，服务的method或消息的Topic具体说明，请参见 [Alink协议](https://help.aliyun.com/zh/iot/user-guide/alink-protocol-1#concept-pfw-hdg-cfb "")。 |
| status | **operation** 状态：<br>- **true**：操作否成功。<br>  <br>- **false**：操作失败。 |
| code | 错误码。详细信息，请参见 [云端运行日志](https://help.aliyun.com/zh/iot/user-guide/iot-platform-logs "")。 |
| reason | 错误原因。 |
| content | 日志内容。 |
| password | 设备连接时指定的密码。 |
| sourceIp | 端侧出口IP地址。 |
| protocol | 通信协议。取值为：<br>- `mqtt`：MQTT协议。<br>  <br>- `mqtt-over-websocket`：基于WebSocket的MQTT协议。 |
| transport | 传输协议。例如：TLSv1.2、TLSv1.3等。 |
| clientId | 客户端ID。 |
| authType | 认证方式。 |
| size | 消息内容大小。 |
| deviceFingerprint | 设备指纹。 |
| connectionId | 连接ID。 |
| params | 消息中参数信息。 |
| resultData | 执行结果数据。 |
| dtInstanceId | 孪生空间的ID。 |