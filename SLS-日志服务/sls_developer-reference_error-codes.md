### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[开发参考](https://help.aliyun.com/zh/sls/developer-reference/)[API参考附录](https://help.aliyun.com/zh/sls/developer-reference/api-reference-appendix/)错误码

# 错误码

更新时间：2026-01-04 03:55:10

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：请求签名](https://help.aliyun.com/zh/sls/developer-reference/request-signatures)[下一篇：概览](https://help.aliyun.com/zh/sls/developer-reference/overview-5)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

业务错误码

通用错误码

在调用API接口过程中，若服务端返回结果中包含错误信息，则表示调用API接口失败。您可以根据本文错误码对照表查找对应的解决方法。

## 概述

当API请求发生错误的时候，服务端会返回错误信息，包括HTTP的Status Code和响应Body中的具体错误细节。其中响应Body中的错误细节为如下格式：

```plaintext
{
"errorCode" : <ErrorCode>,
"errorMessage" : <ErrorMessage>
}
```

您可以参考本文档指导进行处理，也可以参考API错误码中心，查看错误码详情。更多信息，请参见 [日志服务API错误码中心](https://error-center.aliyun.com/status/product/sls?)。

## 业务错误码

业务错误码即各API接口特有的错误码。每个API所独有的错误码会在对应API文档中单独描述，请查看具体API接口文档。

## 通用错误码

通用错误码适用于大部分API接口，它们会出现在多个API错误响应信息中。下表描述API错误响应信息中的通用错误码。

**说明**

日志服务提供查询与分析日志的常见报错，便于您排查查询与分析报错。更多信息，请参见 [查询与分析日志的常见报错](https://help.aliyun.com/zh/sls/resolve-common-errors-that-may-occur-when-i-query-and-analyze-logs#concept-kfn-cn1-hfb "")。

| **HTTP状态码（Status Code）** | **错误码（Error Code）** | **错误消息（Error Message）** | **描述（Description）** | **处理建议** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **HTTP状态码（Status Code）** | **错误码（Error Code）** | **错误消息（Error Message）** | **描述（Description）** | **处理建议** |
| 400 | RequestTimeExpired | Request time _requestTime_has been expired while server time is _server time_. | 请求时间和服务端时间差别超过15分钟。 | 请您检查请求端时间，稍后重试。 |
| 400 | InvalidRequestTime | Request time _requestTime_not follow RFC822 spec. | 请求头中Date的值不符合RFC822标准。 | 请您检查请求头，确认Date取值符合RFC822标准。 |
| 400 | InvalidHost | Host header _Host_ is invalid. | 请求头中Host不合法。 | 请您检查请求头，调试请求头中Host格式。 |
| 400 | ProjectAlreadyExist | Project _ProjectName_ already exist. | Project名称已存在。 | Project名称在阿里云地域内全局唯一。请您更换Project名称后重试。 |
| 400 | PostBodyInvalid | The request body is not valid JSON object. | 请求Body不是JSON格式。 | 请重新调整请求Body之后再发起请求。 |
| 400 | InvalidContentType | Content-Type _type_ is unsupported. | 不支持该类型的Content-Type。 | 请您检查Content-Type定义是否正确。 |
| 400 | ParameterInvalid | Http extend authorization : _authorization_ pair is invalid. | 不合法的请求头authorization。 | 请您检查请求头authorization定义是否正确。 |
| Http extend x-log-bodyrawsize : _x-log-bodyrawsize_ pair is invalid. | 不合法的请求头x-log-bodyrawsize。 | 请您检查请求头x-log-bodyrawsize定义是否正确。 |
| Http extend x-log-compresstype : _x-log-compresstype_ pair is invalid. | 不合法的请求头x-log-compresstype。 | 请您检查请求头x-log-compresstype定义是否正确。 |
| x-log-signaturemethod: _x-log-signaturemethod_ pair is invalid. | x-log-signaturemethod不合法。 | 请您检查请求头x-log-signaturemethod是否正确。 |
| 400 | MissingParameter | Missing query key : _parameter_. | 缺少必需的请求参数。 | 请补充缺少请求参数后重试。请求签名的构成和生成流程，请参见 [请求签名](https://help.aliyun.com/zh/sls/developer-reference/request-signatures#reference-chp-ptq-12b "")。 |
| Missing http extend header key : authorization. | 缺少请求头authorization。 | 请补充请求头authorization参数后重试。请求签名的构成和生成流程，请参见 [请求签名](https://help.aliyun.com/zh/sls/developer-reference/request-signatures#reference-chp-ptq-12b "")。 |
| Missing http extend header key : x-log-bodyrawsize. | 缺少请求头x-log-bodyrawsize。 | 请补充请求头x-log-bodyrawsize参数后重试。请求签名的构成和生成流程，请参见 [请求签名](https://help.aliyun.com/zh/sls/developer-reference/request-signatures#reference-chp-ptq-12b "")。 |
| Missing http extend header key : x-log-date. | 缺少请求头x-log-date。 | 请补充请求头x-log-date参数后重试。请求签名的构成和生成流程，请参见 [请求签名](https://help.aliyun.com/zh/sls/developer-reference/request-signatures#reference-chp-ptq-12b "")。 |
| Missing http extend header key : x-log-signaturemethod. | 缺少请求头x-log-signaturemethod。 | 请补充请求头x-log-signaturemethod参数后重试。请求签名的构成和生成流程，请参见 [请求签名](https://help.aliyun.com/zh/sls/developer-reference/request-signatures#reference-chp-ptq-12b "")。 |
| 401 | SignatureNotMatch | Signature _signature_ not matched. | 请求的数字签名不匹配。 | 请您重试或更换AccessKey后重试。可能存在原因包括：<br>- AccessKey或STS Token已过期。请确认其是否有效。<br>  <br>- 部署的日志服务SDK版本过旧。您可以登录GitHub来获取开放的源码和参考。更多信息，请参见 [SDK参考概述](https://help.aliyun.com/zh/sls/developer-reference/overview-of-log-service-sdk#reference-n3h-2sq-zdb "")。<br>  <br>请求签名的构成和生成流程，请参见 [请求签名](https://help.aliyun.com/zh/sls/developer-reference/request-signatures#reference-chp-ptq-12b "")。 |
| 401 | Unauthorized | The AccessKeyId is unauthorized. | 提供的AccessKey ID值未授权。 | 请确认您的AccessKey ID有访问日志服务权限。为RAM用户授予日志服务操作权限，请参见 [创建RAM用户及授权](https://help.aliyun.com/zh/sls/create-a-ram-user-and-authorize-the-ram-user-to-access-log-service#task-xsk-ttc-ry "")。 |
| The security token you provided is invalid. | STS Token不合法。 | 请检查您的STS接口请求，确认STS Token是合法有效的。 |
| The security token you provided has expired. | STS Token已经过期。 | 请重新申请STS Token后发起请求。 |
| AccessKeyId not found: _AccessKey ID_ | AccessKey ID不存在。 | 请检查您的AccessKey ID，重新获取后再发起请求。 |
| AccessKeyId is disabled: _AccessKey ID_ | AccessKey ID是禁用状态。 | 请检查您的AccessKey ID，确认为已启用状态后重新发起请求。 |
| Your SLS service has been forbidden. | 日志服务已经被禁用。 | 请检查您的日志服务状态，例如是否已欠费。 |
| The project does not belong to you. | Project不属于当前访问用户。 | - 请更换Project或者访问用户后重试。<br>  <br>- 请确保您使用的AccessKey状态为已启用。具体操作，请参见 [查看RAM用户的AccessKey信息](https://help.aliyun.com/zh/ram/user-guide/view-the-accesskey-pairs-of-a-ram-user#task-187540 "")。 |
| 401 | InvalidAccessKeyId | The access key id you provided is invalid: _AccessKey ID_. | AccessKey ID不合法。 | 请检查您的AccessKey ID，确认AccessKey ID是合法有效的。 |
| Your SLS service has not opened. | 日志服务没有开通。 | 请登录日志服务控制台或者通过API开通日志服务后，重新发起请求。更多信息，请参见 [什么是日志服务](https://help.aliyun.com/zh/sls/what-is-log-service#section-crs-2p5-bal "")。 |
| 403 | WriteQuotaExceed | Write quota is exceeded. | 超过写入日志限额。 | 请您优化写入日志请求，减少写入日志数量。更多信息，请参见 [使用限制](https://help.aliyun.com/zh/sls/basic-resources#concept-abm-gdd-p2b "")。 |
| 403 | ReadQuotaExceed | Read quota is exceeded. | 超过读取日志限额。 | 请您优化读取日志请求，减少读取日志数量。更多信息，请参见 [使用限制](https://help.aliyun.com/zh/sls/basic-resources#concept-abm-gdd-p2b "")。 |
| 403 | MetaOperationQpsLimitExceeded | Qps limit for the meta operation is exceeded. | 超出默认设置的QPS阈值。 | 请您优化资源操作请求，减少资源操作次数。建议您延迟几秒后重试。<br>日志服务对以下管控类API进行QPS限制：<br>- Project操作<br>  <br>- LogStore操作<br>  <br>- 索引类操作<br>  <br>- 其他非数据写入、读取操作<br>  <br>更多信息，请参见 [使用限制](https://help.aliyun.com/zh/sls/basic-resources#concept-abm-gdd-p2b "")。 |
| 403 | ProjectForbidden | Project _ProjectName_ has been forbidden. | Project已经被禁用。 | 请检查Project状态，您的Project当前可能已经欠费。 |
| 404 | ProjectNotExist | The Project does not exist : _name_ | 日志项目（Project）不存在。 | 请您检查Project名称，确认已存在该Project或者地域是否正确。 |
| 405 | InvalidMethod | Invalid request method : _request URI_ | 请求消息中method为不支持的接口。 | 请您检查method取值后重试。 |
| 413 | PostBodyTooLarge | Body size _bodysize_ must little than 10485760. | 请求消息体body不能超过10M。 | 请您调整请求消息体的大小后重试。 |
| 500 | InternalServerError | Internal server error message. | 服务器内部错误。 | 请您稍后重试。 |
| 500 | RequestTimeout | The request is timeout. Please try again later. | 请求处理超时。 | 请您稍后重试。 |
| 503 | ServerBusy | The server is busy, please try again later. | 服务器正忙。 | 请您稍后重试。 |

**说明**

错误消息中斜体部分为出错相关的具体信息。例如，ProjectNotExist错误消息中name，表示错误消息中该部分会被具体的Project名称替换。