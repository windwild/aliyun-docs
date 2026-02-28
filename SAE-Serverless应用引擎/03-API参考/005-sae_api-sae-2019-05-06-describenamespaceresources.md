### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [开发参考](https://help.aliyun.com/zh/sae/developer-reference/) [API参考指南](https://help.aliyun.com/zh/sae/api-reference-guide/) [API目录](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir/) [服务通用管理](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-common-service-management/) [命名空间和VPC](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-namespaces-and-vpcs/) DescribeNamespaceResources - 查询命名空间内的资源信息

# DescribeNamespaceResources - 查询命名空间内的资源信息

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ListNamespaceChangeOrders - 获取命名空间发布单列表](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-listnamespacechangeorders)[下一篇：DescribeIngress - 查询ingress配置详情](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-describeingress)

该文章对您有帮助吗？

反馈

查询命名空间内的资源信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/sae/2019-05-06/DescribeNamespaceResources)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)\\
调试](https://api.aliyun.com/api/sae/2019-05-06/DescribeNamespaceResources)

## **授权信息**

下表是API对应的授权信息，可以在RAM权限策略语句的`Action`元素中使用，用来给RAM用户或RAM角色授予调用此API的权限。具体说明如下：

- 操作：是指具体的权限点。

- 访问级别：是指每个操作的访问级别，取值为写入（Write）、读取（Read）或列出（List）。

- 资源类型：是指操作中支持授权的资源类型。具体说明如下：

  - 对于必选的资源类型，用前面加 \* 表示。

  - 对于不支持资源级授权的操作，用`全部资源`表示。
- 条件关键字：是指云产品自身定义的条件关键字。

- 关联操作：是指成功执行操作所需要的其他权限。操作者必须同时具备关联操作的权限，操作才能成功。


|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **操作** | **访问级别** | **资源类型** | **条件关键字** | **关联操作** |
| sae:DescribeNamespaceResources | get | \*全部资源<br>`*` | 无 | 无 |

## 请求语法

```plaintext
GET /pop/v1/sam/namespace/describeNamespaceResources HTTP/1.1
```

## 请求参数

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **必填** | **描述** | **示例值** |
| NamespaceId | string | 否 | 长版命名空间 ID。如果设置了该参数会继续生效而忽略 NameSpaceShortId，该参数是为了兼容保留，推荐使用短版命名空间 ID，简化参数。 | cn-shanghai:test |
| NameSpaceShortId | string | 否 | 短版命名空间 ID，不需要带上 region，推荐。 | test |

## **返回参数**

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **描述** | **示例值** |
|  | object | 返回数据。 |  |
| RequestId | string | 请求 ID。 | 91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\* |
| Message | string | 附加信息。取值说明如下：<br>- 请求正常，返回 **success**。<br>  <br>- 请求异常，返回具体异常错误码。 | success |
| TraceId | string | 调用链 ID，用于精确查询调用信息。 | 0a98a02315955564772843261e\*\*\*\* |
| Data | object | 返回结果。 |  |
| VpcId | string | VPC ID。 | vpc-2ze0i263cnn311nvj\*\*\*\* |
| LastChangeOrderId | string | 发布单 ID。 | afedb3c4-63f8-4a3d-aaa3-2c30363f\*\*\*\* |
| BelongRegion | string | 命名空间所属地域。 | cn-shanghai |
| NamespaceId | string | 命名空间 ID。 | cn-shangha:test |
| SecurityGroupId | string | 安全组 ID。 | sg-wz969ngg2e49q5i4\*\*\*\* |
| UserId | string | 用户 ID。 | test@aliyun.com |
| NamespaceName | string | 命名空间名称。 | test |
| LastChangeOrderStatus | string | 最近一次发布单状态。取值说明如下：<br>- **READY**：最近一次发布单准备就绪。<br>  <br>- **RUNNING**：最近一次发布单处于执行中。<br>  <br>- **SUCCESS**：最近一次发布单发布成功。<br>  <br>- **FAIL**：最近一次发布单发布失败。<br>  <br>- **ABORT**：最近一次发布单中止运行。<br>  <br>- **WAIT\_BATCH\_CONFIRM**：最近一次发布单等待手工批量确认。<br>  <br>- **AUTO\_BATCH\_WAIT**：最近一次发布单处于自动批量等待状态。<br>  <br>- **SYSTEM\_FAIL**：系统故障。<br>  <br>- **WAIT\_APPROVAL**：最近一次发布单等待审批。<br>  <br>- **APPROVED**：最近一次发布单处于审批通过的待执行状态。 | SUCCESS |
| VpcName | string | VPC 名称。 | test |
| VSwitchId | string | vSwitch ID。 | vsw-2ze559r1z1bpwqxwp\*\*\*\* |
| Description | string | 命名空间描述信息。 | decs |
| LastChangeOrderRunning | boolean | 命名空间是否有发布单运行。取值说明如下：<br>- **true**：有发布单运行。<br>  <br>- **false**：没有发布单运行。 | true |
| AppCount | integer | 应用个数。 | 1 |
| VSwitchName | string | vSwitch 名称。 | test |
| NotificationExpired | boolean | 发布单通知是否过期。取值说明如下：<br>- **true**：发布单已过期。<br>  <br>- **false**：发布单没有过期。 | true |
| TenantId | string | SAE 命名空间租户 ID。 | 838cad95-973f-48fe-830b-2a8546d7\*\*\*\* |
| JumpServerAppId | string | 跳板机应用 ID。 | 5ec46468-6b26-4a3c-9f7c-bf88761a\*\*\*\* |
| JumpServerIp | string | 跳板机 IP 地址。 | 120.78.XXX.XX |
| NameSpaceShortId | string | 短版命名空间 ID。 | test |
| ApmJavaAgentVersion | string |  |  |
| SlsConfigs | string |  |  |
| ErrorCode | string | 错误码。取值说明如下：<br>- 请求成功：不返回 **ErrorCode** 字段。<br>  <br>- 请求失败：返回 **ErrorCode** 字段。具体信息，请参见本文的 **错误码** 列表。 | 空 |
| Code | string | 接口状态或 POP 错误码。取值说明如下：<br>- **2xx**：成功。<br>  <br>- **3xx**：重定向。<br>  <br>- **4xx**：请求错误。<br>  <br>- **5xx**：服务器错误。 | 200 |
| Success | boolean | 查询命名空间资源信息是否成功。取值说明如下：<br>- **true**：查询成功。<br>  <br>- **false**：查询失败。 | true |

## 示例

正常返回示例

`JSON`格式

```json
{
  "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message": "success",
  "TraceId": "0a98a02315955564772843261e****",
  "Data": {
    "VpcId": "vpc-2ze0i263cnn311nvj****",
    "LastChangeOrderId": "afedb3c4-63f8-4a3d-aaa3-2c30363f****",
    "BelongRegion": "cn-shanghai",
    "NamespaceId": "cn-shangha:test",
    "SecurityGroupId": "sg-wz969ngg2e49q5i4****",
    "UserId": "test@aliyun.com",
    "NamespaceName": "test",
    "LastChangeOrderStatus": "SUCCESS",
    "VpcName": "test",
    "VSwitchId": "vsw-2ze559r1z1bpwqxwp****",
    "Description": "decs",
    "LastChangeOrderRunning": true,
    "AppCount": 1,
    "VSwitchName": "test",
    "NotificationExpired": true,
    "TenantId": "838cad95-973f-48fe-830b-2a8546d7****",
    "JumpServerAppId": "5ec46468-6b26-4a3c-9f7c-bf88761a****",
    "JumpServerIp": "120.78.XXX.XX",
    "NameSpaceShortId": "test",
    "ApmJavaAgentVersion": "",
    "SlsConfigs": ""
  },
  "ErrorCode": "空",
  "Code": "200",
  "Success": true
}
```

## 错误码

| **HTTP status code** | **错误码** | **错误信息** | **描述** |
| --- | --- | --- | --- |
| 400 | InvalidParameter.Obviously | The specified parameter is invalid {%s}. | 不合法的参数{%s}。 |

访问[错误中心](https://api.aliyun.com/document/sae/2019-05-06/errorCode)查看更多错误码。

## **变更历史**

更多信息，参考[变更详情](https://api.aliyun.com/document/sae/2019-05-06/DescribeNamespaceResources#workbench-doc-change-demo)。