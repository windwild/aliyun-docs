### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[域名管理](https://help.aliyun.com/zh/cdn/user-guide/domain-name-management/)设置报警

# 设置报警

更新时间：2025-10-22 08:35:56

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：跨账号迁移CDN域名](https://help.aliyun.com/zh/cdn/user-guide/domain-name-transfer)[下一篇：使用标签管理域名](https://help.aliyun.com/zh/cdn/user-guide/use-tags-to-manage-accelerated-domain-names)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

报警规则配置示例

当您需要监控CDN域名的使用情况时，可以创建报警规则。如果资源的监控指标达到报警条件，云监控自动发送报警通知，帮助您及时得知异常监控数据，并快速处理。

## 前提条件

- 已成功添加域名，具体请参见 [添加加速域名](https://help.aliyun.com/zh/cdn/add-a-domain-name "")。

- 已开通云监控服务。尚未开通的用户可登录[云监控产品首页](https://www.aliyun.com/product/jiankong)开通服务。


## 操作步骤

1. 进入云监控控制台。

   - **方式一：** 登录[云监控控制台](https://cloudmonitornext.console.aliyun.com/)。

   - **方式二**：

     1. 登录 [CDN控制台](https://cdn.console.aliyun.com/)。

     2. 在左侧导航栏，单击 **域名管理**。

     3. 在 **域名管理** 页面，单击页面右上角的 **监控告警设置**，跳转到云监控控制台。
2. 在左侧导航栏，选择**云资源监控** \> **云产品监控**。

3. 筛选并进入CDN监控页面。

4. 单击 **创建报警规则**。

5. 在 **创建报警规则** 面板中，设置下表中的报警规则相关参数，其他参数保持默认即可。如果您需要了解其他参数配置情况，请参见 [创建报警规则](https://help.aliyun.com/zh/cms/cloudmonitor-1-0/user-guide/create-an-alert-rule "")。




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **产品** | 选择 **CDN**。 |
| **资源范围** | 报警规则作用的资源范围。取值：<br>   - **全部资源**：报警规则作用于CDN所有域名上，对于新添加的域名生效。<br>     <br>   - **应用分组**：报警规则作用于CDN的指定应用分组内的全部域名上，对于新添加的域名生效。<br>     <br>   - **实例**：报警规则作用于CDN的指定域名。 |
| **规则描述** | 报警规则的主体。当监控数据满足报警条件时，触发报警规则。规则描述的设置方法如下：<br>   1. 单击 **添加规则**，在下滑菜单中选择合适的指标类型。<br>      <br>   2. 在 **设置规则描述** 面板，先输入 **规则名称**，再设置规则条件。<br>      <br>      - **简** **单指标**：先选择监控指标，再为其设置阈值和报警级别。<br>        <br>      - **组合指标**：先选择报警级别，再配置多指标报警描述为两个或两个以上的监控指标设置报警条件。<br>        <br>        <br>        <br>        **说明**<br>        <br>        <br>        <br>        <br>        <br>        如果设置了多个指标报警规则，则目标资源必须在每个指标上均有数据，只有在满足条件后才能够正常触发报警。例如：在多指标报警规则中，如果包含公网的监控指标，而ECS主机资源并未配置公网IP，则将无法正常触发报警。<br>        <br>      - **表达式**：先选择报警级别，再配置报警表达式。<br>        <br>      - **智能阈值**：关于智能阈值的更多信息，请参见 [概览](https://help.aliyun.com/zh/cms/cloudmonitor-1-0/user-guide/overview-alert "") 和 [创建智能阈值报警规则](https://help.aliyun.com/zh/cms/cloudmonitor-1-0/user-guide/create-a-dynamic-threshold-alarm-rule "")。<br>   3. 单击 **确定**。<br>      <br>**说明**<br>关于如何设置复杂的报警条件，请参见 [报警规则表达式说明](https://help.aliyun.com/zh/cms/cloudmonitor-1-0/user-guide/alert-rule-expressions#concept-2276873 "")。 |
| **通道沉默周期** | 报警发生后未恢复正常，间隔多久重复发送一次报警通知。取值：5分钟、15分钟、30分钟、60分钟、3小时、6小时、12小时和24小时。<br>某监控指标达到报警阈值时发送报警，如果监控指标在通道沉默周期内持续超过报警阈值，在通道沉默周期内不会重复发送报警通知；如果监控指标在通道沉默周期后仍未恢复正常，则云监控再次发送报警通知。<br>例如：当 **通道沉默周期** 选择 **12小时** 时，如果报警未恢复正常，则间隔12小时后，云监控会再次发送报警通知。 |
| **生效时间** | 报警规则的生效时间。报警规则仅在生效期内才会发送报警通知。<br>**说明**<br>当报警规则不在生效期时，不会发送报警通知，但是报警历史记录仍然会显示在报 **警历史列表** 中。 |
| **报警联系人组** | 发送报警的联系人组。<br>应用分组的报警通知会发送给该报警联系人组中的报警联系人。报警联系人组是一组报警联系人，可以包含一个或多个报警联系人。<br>关于如何创建报警联系人和报警联系人组，请参见 [创建报警联系人或报警联系人组](https://help.aliyun.com/zh/cms/cloudmonitor-1-0/user-guide/create-an-alert-contact-or-alert-contact-group#task-2514452 "")。 |
| **标签** | 报警规则的标签。包括标签名称和标签值。<br>**说明**<br>您最多可设置6组标签。 |

6. 单击 **确认**。


## 报警规则配置示例

您可以参照以下示例为CDN域名配置报警规则，及时得知异常监控数据并快速处理。

配置单个指标监控

配置多个指标监控

例如：当指定域名下行流量的 **最小值** 大于等于500 Mbytes，连续3个周期触发 **紧急** 报警；当下行流量的 **最大值** 大于等于300 Mbytes，连续3个周期触发 **警告** 报警。资源范围和规则描述的配置项建议如下。

- 资源范围：实例。

- 关联资源：选择目标域名`example.aliyundoc.com`。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5971818171/p809883.png)

- 规则描述

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5556311671/p809885.png)


|     |     |
| --- | --- |
| **参数** | **示例值** |
| **指标类型** | **简单指标** |
| **监控指标** | **实例维度** \> **下行流量** |
| **阈值及报警级别** | - 周期均选择 **连续3个周期（1周期=1分钟）**。<br>    <br>  - 报警级别： **紧急**，最小值大于等于500 Mbytes。<br>    <br>  - 报警级别： **警告**，最大值大于等于300 Mbytes。<br>    <br>  - 报警级别： **普通**，平均值大于等于100 Mbytes。 |


例如：当指定域名下行流量的 **最大** 阈值大于等于300 Mbps，或回源状态码502占比最大阈值大于等于1%，任意一个指标连续3个周期触发 **警告** 报警。资源范围和规则描述的配置项建议如下。

- 资源范围：实例。

- 关联资源：选择目标域名`example.aliyundoc.com`。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5971818171/p809883.png)

- 规则描述

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5556311671/p809887.png)


|     |     |
| --- | --- |
| **参数** | **示例值** |
| **指标类型** | **组合指标** |
| **报警级别** | **警告（Warn）** |
| **指标类型** | **标准创建** |
| **多指标报警描述** | 1. 单击 **添加指标**，在 **监控指标** 下拉框中选择**实例维度** \> **下行流量**。<br>     <br>  2. 设置最大值大于等于300 Mbytes。<br>     <br>  3. 然后参照以上步骤依次设置**实例维度** \> **回源状态码502占比**指标，最大值大于等于1%。<br>     <br>**说明**<br>关于如何设置复杂的报警条件，请参见 [报警规则表达式说明](https://help.aliyun.com/zh/cms/cloudmonitor-1-0/user-guide/alert-rule-expressions#concept-2276873 "")。 |
| **多指标关系** | **有一个满足条件就报警（\|\|）** |
| **发出报警需要满足达到阈值的次数** | **连续3个周期（1周期=1分钟）** |