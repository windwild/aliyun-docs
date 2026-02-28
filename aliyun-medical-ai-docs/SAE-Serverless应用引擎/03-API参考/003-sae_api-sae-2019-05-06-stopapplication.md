### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[开发参考](https://help.aliyun.com/zh/sae/developer-reference/)[API参考指南](https://help.aliyun.com/zh/sae/api-reference-guide/)[API目录](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir/)[微服务应用](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-microservice-applications/)[应用生命周期](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-application-lifecycle/)StopApplication - 停止应用

# StopApplication - 停止应用

更新时间：2026-01-13 21:23:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DeleteInstances - 删除实例](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-deleteinstances)[下一篇：StartApplication - 启动应用](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-startapplication)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

调试

授权信息

请求语法

请求参数

返回参数

示例

错误码

变更历史

停止应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/sae/2019-05-06/StopApplication)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)\\
调试](https://api.aliyun.com/api/sae/2019-05-06/StopApplication)

## **授权信息**

下表是API对应的授权信息，可以在RAM权限策略语句的`Action`元素中使用，用来给RAM用户或RAM角色授予调用此API的权限。具体说明如下：

- 操作：是指具体的权限点。

- 访问级别：是指每个操作的访问级别，取值为写入（Write）、读取（Read）或列出（List）。

- 资源类型：是指操作中支持授权的资源类型。具体说明如下：

  - 对于必选的资源类型，用前面加 \* 表示。

  - 对于不支持资源级授权的操作，用`全部资源`表示。
- 条件关键字：是指云产品自身定义的条件关键字。

- 关联操作：是指成功执行操作所需要的其他权限。操作者必须同时具备关联操作的权限，操作才能成功。


| **操作** | **访问级别** | **资源类型** | **条件关键字** | **关联操作** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **操作** | **访问级别** | **资源类型** | **条件关键字** | **关联操作** |
| sae:StopApplication | update | \*Application<br>`acs:sae:{#regionId}:{#accountId}:application/{#namespaceid}/{#appid}` | 无 | 无 |

## 请求语法

```plaintext
PUT /pop/v1/sam/app/stopApplication HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **必填** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **必填** | **描述** | **示例值** |
| AppId | string | 是 | 目标应用 ID。 | 0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\* |

## **返回参数**

| **名称** | **类型** | **描述** | **示例值** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **描述** | **示例值** |
|  | object | 返回数据。 |  |
| RequestId | string | 请求 ID。 | 91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\* |
| Message | string | 附加信息。取值说明如下：<br>- 请求正常，返回 **success**。<br>  <br>- 请求异常，返回具体异常错误码。 | success |
| TraceId | string | 调用链 ID，用于精确查询调用信息。 | 0bc3b6e215637275918588187d\*\*\*\* |
| Data | object | 返回结果。 |  |
| ChangeOrderId | string | 发布单 ID。 | 4a815998-b468-4bea-b7d8-59f52a44\*\*\*\* |
| ErrorCode | string | 错误码。取值说明如下：<br>- 请求成功：不返回 **ErrorCode** 字段。<br>  <br>- 请求失败：返回 **ErrorCode** 字段。具体信息，请参见本文的 **错误码** 列表。 | 空 |
| Code | string | 接口状态或 POP 错误码。取值说明如下：<br>- **2xx**：成功。<br>  <br>- **3xx**：重定向。<br>  <br>- **4xx**：请求错误。<br>  <br>- **5xx**：服务器错误。 | 200 |
| Success | boolean | 停止应用是否成功。取值说明如下：<br>- **true**：停止成功。<br>  <br>- **false**：停止失败。 | true |

## 示例

正常返回示例

`JSON`格式

```json
{
  "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message": "success",
  "TraceId": "0bc3b6e215637275918588187d****",
  "Data": {
    "ChangeOrderId": "4a815998-b468-4bea-b7d8-59f52a44****"
  },
  "ErrorCode": "空",
  "Code": "200",
  "Success": true
}
```

## 错误码

| **HTTP status code** | **错误码** | **错误信息** | **描述** |
| --- | --- | --- | --- |

| **HTTP status code** | **错误码** | **错误信息** | **描述** |
| --- | --- | --- | --- |
| 400 | InvalidApplication.NotFound | The current application does not exist. | 找不到当前应用。 |
| 400 | InvalidParameter.NotEmpty | You must specify the parameter %s. | 不合法的参数：%s不能为空。 |
| 400 | InvalidParameter.Obviously | The specified parameter is invalid {%s}. | 不合法的参数{%s}。 |
| 400 | InvalidParameter.WithMessage | The parameter is invalid {%s}: %s | 不合法的参数{%s}：%s。 |
| 400 | System.Upgrading | The system is being upgraded. Please try again later. | 系统正在升级，请稍后操作。 |
| 400 | Application.ChangerOrderRunning | An application change process is in progress. Please try again later. | 应用有变更流程正在执行，请稍后重试。 |
| 400 | Application.InvalidStatus | The application status is abnormal. Please try again later. | 应用状态异常，请稍后重试。 |
| 400 | Application.NotDeployYet | The application has not been deployed. Please deploy it and try again. | 应用没有部署，请部署后重试。 |

访问[错误中心](https://api.aliyun.com/document/sae/2019-05-06/errorCode)查看更多错误码。

## **变更历史**

更多信息，参考[变更详情](https://api.aliyun.com/document/sae/2019-05-06/StopApplication#workbench-doc-change-demo)。