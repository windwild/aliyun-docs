### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能语音交互](https://help.aliyun.com/zh/isi/)[开发参考](https://help.aliyun.com/zh/isi/developer-reference/)[语音分析](https://help.aliyun.com/zh/isi/developer-reference/speech-analysis/)[性别识别](https://help.aliyun.com/zh/isi/developer-reference/gender-recognition/)接口说明

# 接口说明

更新时间：2025-01-15 04:18:13

复制为 MD 格式

[产品详情](https://ai.aliyun.com/nls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java-1)[下一篇：Java SDK](https://help.aliyun.com/zh/isi/developer-reference/sdk-for-java-2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

计费和并发限制

使用须知

服务地址

交互流程

1. 鉴权

2. 开始检测

3. 接收识别结果

4. 结束识别

服务状态码

性别识别功能用于识别音频中说话人的性别（男或女）。

## **计费和并发限制**

- 性别识别提供试用版和商用版两种计费模式，详情请参见 [试用版和商用版](https://help.aliyun.com/zh/isi/product-overview/pricing#40ba8a7127hw1 "")。如果您需要将试用版升级为商用版，请参见 [试用版升级为商用版](https://help.aliyun.com/zh/isi/product-overview/billing-10#41bb3ea20c3v4 "")。

- 计费方式详情请参见 [计费方式](https://help.aliyun.com/zh/isi/product-overview/billing-10 "")。

- 并发限制请参见 [并发和QPS说明](https://help.aliyun.com/zh/isi/product-overview/faq-about-concurrency-and-monitoring "")。


## 使用须知

- 支持的输入格式：PCM编码（无压缩的PCM或WAV文件）、16 bit采样位数、单声道（mono）。

- 音频时长限制小于60秒。

- 支持的音频采样率：8000 Hz。


## 服务地址

| **访问类型** | **说明** | **URL** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **访问类型** | **说明** | **URL** |
| 外网访问 | 所有服务器均可使用外网访问URL（SDK中默认设置了外网访问URL，无需您设置）。 | wss://nls-gateway-cn-shanghai.aliyuncs.com/ws/v1 |
| 阿里云上海ECS内网访问 | 使用阿里云上海ECS（ECS地域为华东2（上海）），可使用内网访问URL。 ECS的经典网络不能访问AnyTunnel，即不能在内网访问语音服务；如果希望使用AnyTunnel，需要创建专有网络在其内部访问。<br>**说明**<br>- 使用内网访问方式，将不会产生ECS实例的公网流量费用。<br>  <br>- 关于ECS的网络类型请参见 [网络类型](https://help.aliyun.com/zh/ecs/user-guide/network-types#concept-nfj-dz2-5db "")。 | ws://nls-gateway-cn-shanghai-internal.aliyuncs.com:80/ws/v1 |

## 交互流程

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1962396371/CAEQShiBgIDYhJP42BgiIGE1YTMxMzc5ZmQ4YjRkOTNhYTFlYTFlMmFmOGQ3Y2Jj4024928_20231008170233.737.svg)

### 1. 鉴权

客户端在与服务端建立WebSocket连接时，使用Token进行鉴权。Token获取请参见 [获取Token概述](https://help.aliyun.com/zh/isi/overview-of-obtaining-an-access-token#587dee8029x7r "")。

### 2. 开始检测

客户端发起请求，服务端确认请求有效。其中在请求消息中进行参数设置，各参数通过SDK中CommonRequest对象的相关set方法设置，含义如下。

| **参数名称** | **参数类型** | **参数说明** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数名称** | **参数类型** | **参数说明** |
| namespace | String | 命名空间，请在创建CommonRequest时设置为GenderIdentification。 |
| format | String | 音频编码格式，默认值：PCM。支持的格式：PCM、WAV。 |
| sample\_rate | Integer | 音频采样率，默认值：8000，单位：Hz。 |

### 3. 接收识别结果

客户端循环发送语音数据，持续接收识别结果。

- onEvent事件表示服务端检测到声音事件，举例如下：















```json
{
      "header":{
          "namespace":"GenderIdentification",
          "name":"TaskResult",
          "status":20000000,
          "message_id":"6b97ae72cf434e19aa797996fad9****",
          "task_id":"ce70e356743b47b9b80dc283bdf0****",
          "status_text":"Gateway:SUCCESS:Success."
      },
      "payload":{
          "type":3,
          "score":243.18978881835938
      }
}
```

- header对象参数说明：




| **参数名称** | **参数类型** | **参数说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数名称** | **参数类型** | **参数说明** |
| namespace | String | 消息所属的命名空间。 |
| name | String | 消息名称，TaskResult表示一个音频事件。 |
| status | Integer | 状态码，表示请求是否成功，具体请参见 [服务状态码](https://help.aliyun.com/zh/isi/developer-reference/sdk-reference-5#section-kto-5ni-aql "")。 |
| status\_text | String | 状态消息。 |
| task\_id | String | 任务全局唯一ID，请记录该值，便于排查问题。 |
| message\_id | String | 本次消息的ID。 |

- payload对象参数说明：




| **参数名称** | **参数类型** | **参数说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数名称** | **参数类型** | **参数说明** |
| type | Integer | 性别。<br>  - 2：女<br>    <br>  - 3：男<br>    <br>  - 0：未识别出性别<br>    <br>其余结果为预留位，暂不开放。 |
| score | Float | 当前结果的置信度，取值范围：\[-1000.0,500.0\]。值越大表示置信度越高。 |


### 4. 结束识别

通知服务端语音数据发送完成，服务端识别结束后通知客户端检测完毕。

## 服务状态码

在服务的每一次响应中，都包含status字段，即服务状态码。通用错误码、网关错误码、配置错误码各种取值含义如下。

- 通用错误码




| **错误码** | **原因** | **解决办法** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **错误码** | **原因** | **解决办法** |
| 40000001 | 身份认证失败 | 检查使用的令牌是否正确，是否过期。 |
| 40000002 | 无效的消息 | 检查发送的消息是否符合要求。 |
| 40000004 | 空闲超时 | 确认是否长时间（10秒）没有发送数据到服务端。 |
| 40000005 | 请求数量过多 | 检查是否超过了并发连接数或者每秒钟请求数。如果超过并发数，建议从免费版升级到商用版，或者商用版扩容并发资源。 |
| 40000000 | 默认的客户端错误码 | 检查对应的错误消息。 |
| 40000010 | 新用户免费试用3个月已到期 | 继续使用需要付费商用，请前往 [控制台](https://nls-portal.console.aliyun.com/)，在 **服务管理与开通** 页面，单击目标服务右侧的 **升级为商用版**，进行付费使用。 |
| 41010120 | 客户端超时错误 | 客户端连续10秒及以上没有发送数据，导致客户端超时错误。 |
| 41160001 | 采样率参数错误 | 检查采样率参数设置。 |
| 41160002 | 音频格式参数设置错误 | 检查音频格式参数设置。 |
| 41160003 | 音频解码失败 | 检查音频格式是否正常。 |
| 41160004 | 音频时长过长 | 检查音频是否超过60秒。 |

- 网关错误码




| **错误码** | **原因** | **解决办法** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **错误码** | **原因** | **解决办法** |
| 40010001 | 不支持的接口 | 请升级到最新的SDK。 |
| 40010002 | 不支持的指令 | 请升级到最新的SDK。 |
| 40010003 | 无效的指令 | 请升级到最新的SDK。 |
| 40010004 | 客户端提前断开连接 | 检查是否在请求正常完成之前关闭了连接。 |
| 40010005 | 任务状态错误 | 发送了当前任务状态不能处理的指令。 |

- 配置错误码




| **错误码** | **原因** | **解决办法** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **错误码** | **原因** | **解决办法** |
| 40020105 | 应用不存在 | 解析路由时找不到应用。 |
| 40020106 | Appkey和Token不匹配 | 检查应用Appkey是否正确，是否与令牌归属同一个账号。 |
| 40020503 | RAM用户（子账号）鉴权失败 | 使用阿里云账号对调用的RAM用户（子账号）授权POP API的访问权限。 |