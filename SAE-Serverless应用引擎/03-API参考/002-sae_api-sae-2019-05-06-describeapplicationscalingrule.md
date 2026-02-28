### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[开发参考](https://help.aliyun.com/zh/sae/developer-reference/)[API参考指南](https://help.aliyun.com/zh/sae/api-reference-guide/)[API目录](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir/)[微服务应用](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-microservice-applications/)[应用伸缩规则](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-dir-apply-scaling-rules/)DescribeApplicationScalingRule - 查询应用的单个弹性伸缩策略

# DescribeApplicationScalingRule - 查询应用的单个弹性伸缩策略

更新时间：2026-01-13 21:11:39

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：UpdateApplicationScalingRule - 修改弹性策略](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-updateapplicationscalingrule)[下一篇：DescribeApplicationScalingRules - 查询应用弹性伸缩策略](https://help.aliyun.com/zh/sae/api-sae-2019-05-06-describeapplicationscalingrules)

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

s接口查询应用的单个弹性伸缩策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/api/sae/2019-05-06/DescribeApplicationScalingRule)

[![](https://img.alicdn.com/tfs/TB16JcyXHr1gK0jSZR0XXbP8XXa-24-26.png)\\
调试](https://api.aliyun.com/api/sae/2019-05-06/DescribeApplicationScalingRule)

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
| sae:DescribeApplicationScalingRule | get | \*全部资源<br>`*` | 无 | 无 |

## 请求语法

```plaintext
GET /pop/v1/sam/scale/applicationScalingRule HTTP/1.1
```

## 请求参数

| **名称** | **类型** | **必填** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **名称** | **类型** | **必填** | **描述** | **示例值** |
| AppId | string | 是 | 应用 ID。 | a0d2e04c-159d-40a8-b240-d2f2c263\*\*\*\* |
| ScalingRuleName | string | 是 | 弹性伸缩策略名称。 | test |

## **返回参数**

| **名称** | **类型** | **描述** | **示例值** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **名称** | **类型** | **描述** | **示例值** |
|  | object | 返回信息。 |  |
| RequestId | string | 请求 ID。 | 73404D3D-EE4F-4CB2-B197-5C46F6A1\*\*\*\* |
| TraceId | string | 调用链 ID，用于精确查询调用信息。 | 0b57ff7e16243300839193068e\*\*\*\* |
| Data | object | 返回结果。 |  |
| Timer | object | 定时弹性伸缩。 |  |
| EndDate | string | 定时弹性伸缩策略的短期结束日期。取值说明如下：<br>- 当 **BeginDate** 和 **EndDate** 取值均为 **null** 时，表示长期执行，为默认值。<br>  <br>- 当取值为具体日期时，例如 **BeginDate** 为 **2021-03-25**， **EndDate** 为 **2021-04-25**，表示执行有效期为 1 个月。 | 2021-04-25 |
| BeginDate | string | 定时弹性伸缩策略的短期起始日期。取值说明如下：<br>- 当 **BeginDate** 和 **EndDate** 取值均为 **null** 时，表示长期执行，为默认值。<br>  <br>- 当取值为具体日期时，例如 **BeginDate** 为 **2021-03-25**， **EndDate** 为 **2021-04-25**，表示执行有效期为 1 个月。 | 2021-03-25 |
| Schedules | array<object> | 单天内触发时间点。 |  |
|  | object | 时间点数据。 |  |
| AtTime | string | 时间点。格式： **时:分**。 | 08:00 |
| TargetReplicas | integer | 目标实例数。 | 2 |
| MinReplicas | integer | 最小实例数。 | 1 |
| MaxReplicas | integer | 最大实例数。 | 10 |
| Period | string | 执行定时弹性伸缩策略的周期。取值说明如下：<br>- **\\* \\* \\***：每天指定时间执行定时策略。<br>  <br>- **\\* \\* Fri,Mon**：每周指定天数的指定时间执行定时策略，支持多选，GMT+8 时区。取值说明如下：<br>  - **Sun**：星期日<br>    <br>  - **Mon**：星期一<br>    <br>  - **Tue**：星期二<br>    <br>  - **Wed**：星期三<br>    <br>  - **Thu**：星期四<br>    <br>  - **Fri**：星期五<br>    <br>  - **Sat**：星期六<br>- **1,2,3,28,31 \* \***：每月指定日期的指定时间执行定时策略，支持多选。取值范围\[1,31\]。若当月无 31 日，则跳过该日期执行定时策略。 | \\* \\* \\* |
| UpdateTime | integer | 弹性伸缩策略更新时间。单位：毫秒。 | 1624330075827 |
| AppId | string | 应用 ID。 | a0d2e04c-159d-40a8-b240-d2f2c263\*\*\*\* |
| CreateTime | integer | 弹性伸缩策略创建时间。单位：毫秒。 | 1624329843790 |
| LastDisableTime | integer | 最近一次禁用弹性伸缩策略的时间。 | 1641882854484 |
| ScaleRuleEnabled | boolean | 弹性伸缩策略是否启用。取值说明如下：<br>- **true**：启用状态。<br>  <br>- **false**：禁用状态。 | true |
| ScaleRuleType | string | 弹性伸缩策略类型。取值说明如下：<br>- **timing**：定时弹性。<br>  <br>- **metric**：监控指标弹性。<br>  <br>- **mix**：混合弹性。 | timing |
| Metric | object | 监控指标弹性伸缩。 |  |
| Metrics | array<object> | 监控指标弹性伸缩列表。 |  |
|  | object | 监控指标数据。 |  |
| MetricTargetAverageUtilization | integer | 监控指标的目标值。<br>- CPU 使用率目标值，单位为百分比。<br>  <br>- 内存使用率目标值，单位为百分比。<br>  <br>- QPS，单位为秒。<br>  <br>- 响应时间，单位为毫秒。<br>  <br>- TCP 活跃连接数平均值，单位为个/秒。<br>  <br>- 公网 SLB QPS，单位为秒。<br>  <br>- 公网 SLB 响应时间，单位为毫秒。<br>  <br>- 私网 SLB QPS，单位为秒。<br>  <br>- 私网 SLB 响应时间，单位为毫秒。 | 20 |
| MetricType | string | 监控指标的触发条件。取值说明如下：<br>- **CPU**：CPU 使用率。<br>  <br>- **MEMORY**：内存使用率。<br>  <br>- **QPS**：JAVA 应用 1 分钟内单个实例的平均 QPS。<br>  <br>- **RT**：JAVA 应用 1 分钟内应用所有服务接口平均 RT 值。<br>  <br>- **tcpActiveConn**：30 秒内单个实例的平均 TCP 活跃连接数。<br>  <br>- **SLB\_QPS**：15 秒内单个实例的平均公网 SLB QPS。<br>  <br>- **SLB\_RT**：15 秒内公网 SLB 平均响应时间。<br>  <br>- **INTRANET\_SLB\_QPS**：15 秒内单个实例的平均私网 SLB QPS。<br>  <br>- **INTRANET\_SLB\_RT**：15 秒内私网 SLB 平均响应时间。 | CPU |
| SlbProject | string | SLB 访问日志 Project。 | test |
| SlbLogstore | string | SLB 访问日志 Logstore。 | test |
| Vport | string | SLB 实例端口。 | 80 |
| SlbId | string | SLB 实例 ID。 | lb-xxx |
| MetricsStatus | object | 监控指标弹性状态。 |  |
| DesiredReplicas | integer | 目标实例数。 | 2 |
| NextScaleTimePeriod | integer | 下一次监控指标弹性的周期。 | 3 |
| CurrentReplicas | integer | 当前实例数。 | 2 |
| LastScaleTime | string | 最近一次弹性扩缩的时间。 | 2022-01-11T08:14:32Z |
| CurrentMetrics | array<object> | 当前监控指标弹性数据。 |  |
|  | object | 监控指标数据。 |  |
| Type | string | 数据类型。与监控指标关联。<br>- **Resource**： **cpu**、 **memory** 的指标取值。<br>  <br>- **Pods**： **tcpActiveConn** 的指标取值。<br>  <br>- **External**： **arms**、 **slb** 的指标取值。 | Resource |
| CurrentValue | integer | 当前值。 | 0 |
| Name | string | 触发条件的名称。<br>- **cpu**：CPU 使用率。<br>  <br>- **memory**：内存使用率。<br>  <br>- **arms\_incall\_rt**：JAVA 应用 1 分钟内单个实例的平均 QPS。<br>  <br>- **arms\_incall\_rt**：JAVA 应用 1 分钟内应用所有服务接口平均 RT 值。<br>  <br>- **tcpActiveConn**：TCP 活跃连接数。<br>  <br>- **slb\_incall\_qps**：公网 SLB QPS。<br>  <br>- **slb\_incall\_rt**：公网 SLB 响应时间。<br>  <br>- **intranet\_slb\_incall\_qps**：私网 SLB QPS。<br>  <br>- **intranet\_slb\_incall\_rt**：私网 SLB 响应时间。 | cpu |
| NextScaleMetrics | array<object> | 下一次监控指标弹性列表。 |  |
|  | object | 监控指标数据。 |  |
| NextScaleOutAverageUtilization | integer | 下一次触发扩容条件的监控指标弹性的百分比数值。 | 21 |
| NextScaleInAverageUtilization | integer | 下一次触发缩容条件的监控指标弹性的百分比数值。 | 10 |
| Name | string | 触发条件的名称。<br>- **cpu**：CPU 使用率。<br>  <br>- **memory**：内存使用率。<br>  <br>- **arms\_incall\_rt**：JAVA 应用 1 分钟内单个实例的平均 QPS。<br>  <br>- **arms\_incall\_rt**：JAVA 应用 1 分钟内应用所有服务接口平均 RT 值。<br>  <br>- **tcpActiveConn**：TCP 活跃连接数。<br>  <br>- **slb\_incall\_qps**：公网 SLB QPS。<br>  <br>- **slb\_incall\_rt**：公网 SLB 响应时间。<br>  <br>- **intranet\_slb\_incall\_qps**：私网 SLB QPS。<br>  <br>- **intranet\_slb\_incall\_rt**：私网 SLB 响应时间。 | cpu |
| MaxReplicas | integer | 最大实例数。 | 3 |
| MinReplicas | integer | 最小实例数。 | 1 |
| ScaleUpRules | object | 应用扩容规则。 |  |
| Step | integer | 弹性扩容步长。单位时间内最多扩容的实例数。 | 100 |
| StabilizationWindowSeconds | integer | 扩容冷却时间。取值范围\[0, 3600\]，单位为秒。默认为 0 秒。 | 300 |
| Disabled | boolean | 是否禁止缩容。取值说明如下：<br>- **true**：开启。<br>  <br>- **false**：关闭。<br>  <br>**说明**<br>开启后将永远不会缩容该应用的实例，能有效防止在流量高峰期缩容造成业务风险。默认关闭。 | false |
| ScaleDownRules | object | 应用缩容规则。 |  |
| Step | integer | 弹性缩容步长。单位时间内最多缩容的实例数。 | 100 |
| StabilizationWindowSeconds | integer | 缩容冷却时间。取值范围\[0, 3600\]，单位为秒。默认为 0 秒。 | 300 |
| Disabled | boolean | 是否禁止缩容。取值说明如下：<br>- **true**：开启。<br>  <br>- **false**：关闭。<br>  <br>**说明**<br>开启后将永远不会缩容该应用的实例，能有效防止在流量高峰期缩容造成业务风险。默认关闭。 | false |
| ScaleRuleName | string | 弹性伸缩策略名称。 | test |
| MinReadyInstances | integer | 最小存活实例数。取值说明如下：<br>- 如果设置为 **0**，应用在升级过程中将会中断业务。<br>  <br>- 如果设置为\*\*-1\*\*，最小存活实例数将使用系统推荐值，即取现有实例数的 25%。如果当前为 5 个实例，5×25%=1.25，向上取整后，最小存活实例数为 2。<br>  <br>**说明**<br>每次滚动部署最小存活的实例数建议≥1，保证业务不中断。 | 1 |
| MinReadyInstanceRatio | integer | 最小存活实例数百分比。取值说明如下：<br>- **-1**：初始化值，表示不采用百分比。<br>  <br>- **0~100**：单位为百分比，向上取整。例如设置为 50%，如果当前为 5 个实例，则最小存活实例数为 3。<br>  <br>**说明**<br>当和 **MinReadyInstanceRatio** 同时传递时，且 **MinReadyInstanceRatio** 的取值非\*\*-1\*\*时，以 **MinReadyInstanceRatio** 参数为准。假设 **MinReadyInstances** 取值为 **5**， **MinReadyInstanceRatio** 取值为 **50**，则会用 **50** 来计算最小存活实例数。 | -1 |
| Message | string | 附加信息。取值说明如下：<br>- 请求正常，返回 **success**。<br>  <br>- 请求异常，返回具体异常错误码。 | success |
| ErrorCode | string | 错误码。取值说明如下：<br>- 请求成功：不返回 **ErrorCode** 字段。<br>  <br>- 请求失败：返回 **ErrorCode** 字段。具体信息，请参见本文的 **错误码** 列表。 | 空 |
| Code | string | 接口状态或 POP 错误码。取值说明如下：<br>- **2xx**：成功。<br>  <br>- **3xx**：重定向。<br>  <br>- **4xx**：请求错误。<br>  <br>- **5xx**：服务器错误。 | 200 |
| Success | boolean | 重启应用实例是否成功。取值说明如下：<br>- **true**：重启成功。<br>  <br>- **false**：重启失败。 | true |

## 示例

正常返回示例

`JSON`格式

```json
{
  "RequestId": "73404D3D-EE4F-4CB2-B197-5C46F6A1****",
  "TraceId": "0b57ff7e16243300839193068e****",
  "Data": {
    "Timer": {
      "EndDate": "2021-04-25",
      "BeginDate": "2021-03-25",
      "Schedules": [\
        {\
          "AtTime": "08:00",\
          "TargetReplicas": 2,\
          "MinReplicas": 1,\
          "MaxReplicas": 10\
        }\
      ],
      "Period": "* * *"
    },
    "UpdateTime": 1624330075827,
    "AppId": "a0d2e04c-159d-40a8-b240-d2f2c263****",
    "CreateTime": 1624329843790,
    "LastDisableTime": 1641882854484,
    "ScaleRuleEnabled": true,
    "ScaleRuleType": "timing",
    "Metric": {
      "Metrics": [\
        {\
          "MetricTargetAverageUtilization": 20,\
          "MetricType": "CPU",\
          "SlbProject": "test",\
          "SlbLogstore": "test",\
          "Vport": "80",\
          "SlbId": "lb-xxx"\
        }\
      ],
      "MetricsStatus": {
        "DesiredReplicas": 2,
        "NextScaleTimePeriod": 3,
        "CurrentReplicas": 2,
        "LastScaleTime": "2022-01-11T08:14:32Z",
        "CurrentMetrics": [\
          {\
            "Type": "Resource",\
            "CurrentValue": 0,\
            "Name": "cpu"\
          }\
        ],
        "NextScaleMetrics": [\
          {\
            "NextScaleOutAverageUtilization": 21,\
            "NextScaleInAverageUtilization": 10,\
            "Name": "cpu"\
          }\
        ]
      },
      "MaxReplicas": 3,
      "MinReplicas": 1,
      "ScaleUpRules": {
        "Step": 100,
        "StabilizationWindowSeconds": 300,
        "Disabled": false
      },
      "ScaleDownRules": {
        "Step": 100,
        "StabilizationWindowSeconds": 300,
        "Disabled": false
      }
    },
    "ScaleRuleName": "test",
    "MinReadyInstances": 1,
    "MinReadyInstanceRatio": -1
  },
  "Message": "success",
  "ErrorCode": "空",
  "Code": "200",
  "Success": true
}
```

## 错误码

访问[错误中心](https://api.aliyun.com/document/sae/2019-05-06/errorCode)查看更多错误码。

## **变更历史**

更多信息，参考[变更详情](https://api.aliyun.com/document/sae/2019-05-06/DescribeApplicationScalingRule#workbench-doc-change-demo)。