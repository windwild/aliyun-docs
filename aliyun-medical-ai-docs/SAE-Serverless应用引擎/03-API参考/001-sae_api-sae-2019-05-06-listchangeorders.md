### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[开发参考](https://help.aliyun.com/zh/sae/developer-reference/)[API参考指南](https://help.aliyun.com/zh/sae/api-reference-guide/)[API目录](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir/)[微服务应用](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-microservice-applications/)[应用生命周期](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-application-lifecycle/)ListChangeOrders - 获取变更单列表

# ListChangeOrders - 获取变更单列表

更新时间：2026-01-13 21:20:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DescribeApplicationStatus - 获取应用的状态信息](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-describeapplicationstatus)[下一篇：DescribeChangeOrder - 查询变更单信息](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-describechangeorder)

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

获取变更单列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/sae/2019-05-06/ListChangeOrders)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)\\
调试](https://api.aliyun.com/api/sae/2019-05-06/ListChangeOrders)

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
| sae:ListChangeOrders | get | \*全部资源<br>`*` | 无 | 无 |

## 请求语法

```plaintext
GET /pop/v1/sam/changeorder/ListChangeOrders HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **必填** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **必填** | **描述** | **示例值** |
| AppId | string | 是 | 应用 ID。 | 145341c-9708-4967-b3ec-24933767\*\*\*\* |
| CurrentPage | integer | 否 | 当前分页。 | 1 |
| PageSize | integer | 否 | 分页大小。 | 20 |
| Key | string | 否 | 发布单描述信息模糊查询（包含这此 **key** 的都会返回）。 | test |
| CoType | string | 否 | 变更单类型。取值说明如下：<br>- **CoBindSlb**：绑定 SLB。<br>  <br>- **CoUnbindSlb**：解绑 SLB。<br>  <br>- **CoCreateApp**：创建应用。<br>  <br>- **CoDeleteApp**：删除应用。<br>  <br>- **CoDeploy**：部署应用。<br>  <br>- **CoRestartApplication**：重启应用。<br>  <br>- **CoRollback**：回滚应用。<br>  <br>- **CoScaleIn**：应用缩容。<br>  <br>- **CoScaleOut**：应用扩容。<br>  <br>- **CoStartApplication**：启动应用。<br>  <br>- **CoStopApplication**：停止应用。<br>  <br>- **CoRescaleApplicationVertically**：修改实例规格。<br>  <br>- **CoDeployHistroy**：回退历史版本。<br>  <br>- **CoBindNas**：绑定 NAS。<br>  <br>- **CoUnbindNas**：解绑 NAS。<br>  <br>- **CoBatchStartApplication**：批量启动应用。<br>  <br>- **CoBatchStopApplication**：批量停止应用。<br>  <br>- **CoRestartInstances**：重启实例。<br>  <br>- **CoDeleteInstances**：删除实例。<br>  <br>- **CoScaleInAppWithInstances**：指定实例缩容。 | CoCreateApp |
| CoStatus | string | 否 | 变更单状态。取值说明如下：<br>- **0**：准备。<br>  <br>- **1**：执行中。<br>  <br>- **2**：执行成功。<br>  <br>- **3**：执行失败。<br>  <br>- **6**：终止。<br>  <br>- **8**：等待手工确认分批。<br>  <br>- **9**：等待自动确认分批。<br>  <br>- **10**：系统异常执行失败。<br>  <br>- **11**：等待审批。<br>  <br>- **12**：审批通过，等待执行。 | 2 |
| OrderBy | string | 否 |  |  |
| Reverse | boolean | 否 |  |  |

## **返回参数**

| **名称** | **类型** | **描述** | **示例值** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **描述** | **示例值** |
|  | object | 返回数据。 |  |
| RequestId | string | 请求 ID。 | 65E1F-43BA-4D0C-8E61-E4D1337F\*\*\*\* |
| Message | string | 调用结果的附加信息。 | success |
| TraceId | string | 调用链 ID，用于精确查询调用信息。 | 0bb6f815638568884597879d\*\*\*\* |
| Data | object | 变更单列表信息。 |  |
| CurrentPage | integer | 当前分页。 | 1 |
| TotalSize | integer | 变更单总数。 | 1 |
| ChangeOrderList | array<object> | 变更单列表。 |  |
|  | object | 变更单列表信息。 |  |
| Status | integer | 变更单状态。取值说明如下：<br>- **0**：准备。<br>  <br>- **1**：执行中。<br>  <br>- **2**：执行成功。<br>  <br>- **3**：执行失败。<br>  <br>- **6**：终止。<br>  <br>- **8**：等待手工确认分批。<br>  <br>- **9**：等待自动确认分批。<br>  <br>- **10**：系统异常执行失败。<br>  <br>- **11**：等待审批。<br>  <br>- **12**：审批通过，等待执行。 | 2 |
| FinishTime | string | 结束时间。 | 2019-07-11 20:12:58 |
| CreateTime | string | 创建时间。 | 2019-07-11 15:54:49 |
| UserId | string | 用户 ID。 | sae-beta-test |
| Source | string | 变更单操作入口来源。 | console |
| BatchCount | integer | 分批数。 | 1 |
| CreateUserId | string | 创建用户 ID。 | sae-beta-test |
| CoTypeCode | string | 变更类型 Code。取值说明如下：<br>- **CoBindSlb**：绑定 SLB。<br>  <br>- **CoUnbindSlb**：解绑 SLB。<br>  <br>- **CoCreateApp**：创建应用。<br>  <br>- **CoDeleteApp**：删除应用。<br>  <br>- **CoDeploy**：部署应用。<br>  <br>- **CoRestartApplication**：重启应用。<br>  <br>- **CoRollback**：回滚应用。<br>  <br>- **CoScaleIn**：应用缩容。<br>  <br>- **CoScaleOut**：应用扩容。<br>  <br>- **CoStartApplication**：启动应用。<br>  <br>- **CoStopApplication**：停止应用。<br>  <br>- **CoRescaleApplicationVertically**：修改实例规格。<br>  <br>- **CoDeployHistroy**：回退历史版本。<br>  <br>- **CoBindNas**：绑定 NAS。<br>  <br>- **CoUnbindNas**：解绑 NAS。<br>  <br>- **CoBatchStartApplication**：批量启动应用。<br>  <br>- **CoBatchStopApplication**：批量停止应用。<br>  <br>- **CoRestartInstances**：重启实例。<br>  <br>- **CoDeleteInstances**：删除实例。<br>  <br>- **CoScaleInAppWithInstances**：指定实例缩容。 | CoCreateApp |
| ChangeOrderId | string | 变更单 ID。 | 7fa5c0-9ebb-4bb4-b383-1f885447\*\*\*\* |
| BatchType | string | 分批类型。取值说明如下：<br>- **auto**：自动。<br>  <br>- **manual**：手动。 | auto |
| GroupId | string | 分组 ID。 | c9ecd2-cf6c-46c3-9f20-525de202\*\*\*\* |
| Description | string | 描述信息。 | 版本：1.0 \| 镜像名称：nginx |
| CoType | string | 变更类型，是对 **CoTypeCode** 的描述。 | 创建应用 |
| AppId | string | 应用 ID。 | 164341c-9708-4967-b3ec-24933767\*\*\*\* |
| PageSize | integer | 分页大小。 | 20 |
| ErrorCode | string | 错误码。取值说明如下：<br>- 请求成功：不返回 **ErrorCode** 字段。<br>  <br>- 请求失败：返回 **ErrorCode** 字段。具体信息，请参见本文的 **错误码** 列表。 | 空 |
| Code | string | 接口状态或 POP 错误码。取值说明如下：<br>- **2xx**：成功。<br>  <br>- **3xx**：重定向。<br>  <br>- **4xx**：请求错误。<br>  <br>- **5xx**：服务器错误。 | 200 |
| Success | boolean | 获取变更单列表是否成功。取值说明如下：<br>- **true**：获取成功。<br>  <br>- **false**：获取失败。 | true |

## 示例

正常返回示例

`JSON`格式

```json
{
  "RequestId": "65E1F-43BA-4D0C-8E61-E4D1337F****",
  "Message": "success",
  "TraceId": "0bb6f815638568884597879d****",
  "Data": {
    "CurrentPage": 1,
    "TotalSize": 1,
    "ChangeOrderList": [\
      {\
        "Status": 2,\
        "FinishTime": "2019-07-11 20:12:58",\
        "CreateTime": "2019-07-11 15:54:49",\
        "UserId": "sae-beta-test",\
        "Source": "console",\
        "BatchCount": 1,\
        "CreateUserId": "sae-beta-test",\
        "CoTypeCode": "CoCreateApp",\
        "ChangeOrderId": "7fa5c0-9ebb-4bb4-b383-1f885447****",\
        "BatchType": "auto",\
        "GroupId": "c9ecd2-cf6c-46c3-9f20-525de202****",\
        "Description": "版本：1.0 | 镜像名称：nginx",\
        "CoType": "创建应用",\
        "AppId": "164341c-9708-4967-b3ec-24933767****"\
      }\
    ],
    "PageSize": 20
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
| 400 | InvalidParameter.NotEmpty | You must specify the parameter %s. | 不合法的参数：%s不能为空。 |
| 400 | Resouce.no.permission | You are not authorized to operate on the specified resources. | 没有权限操作资源。 |
| 404 | InvalidAppId.NotFound | The specified AppId does not exist. | 指定的AppId不存在。 |

访问[错误中心](https://api.aliyun.com/document/sae/2019-05-06/errorCode)查看更多错误码。

## **变更历史**

更多信息，参考[变更详情](https://api.aliyun.com/document/sae/2019-05-06/ListChangeOrders#workbench-doc-change-demo)。