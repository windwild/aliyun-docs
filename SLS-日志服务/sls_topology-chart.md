### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据监控](https://help.aliyun.com/zh/sls/data-monitoring/)[可视化](https://help.aliyun.com/zh/sls/visualization-2/)[统计图表](https://help.aliyun.com/zh/sls/statistical-charts/)拓扑图

# 拓扑图

更新时间：2024-11-29 04:20:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：雷达图](https://help.aliyun.com/zh/sls/radar-chart)[下一篇：交叉表](https://help.aliyun.com/zh/sls/cross-table)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

产品试用

配置示例

通用配置

节点指标配置

连线指标配置

交互事件

拓扑图主要用于帮助您直观地理解系统架构、服务间的依赖关系以及数据流的方向。本文介绍拓扑图的相关配置。

## 简介

拓扑图是一种全局系统级别的观测视图，用于直观地描述模块或应用之间的依赖关系以及总体概况信息。

日志服务采集到拓扑数据后，会解析数据并将其结构化，拓扑数据样例如下图所示。您可以通过child、parent字段粗略获得不同模块或应用之间的依赖关系，但并不直观。

![拓扑图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0967709561/p472828.png)

针对上述拓扑数据，日志服务支持您通过查询和分析语句获取描述拓扑关系的字段，例如通过`* | SELECT child, parent, child_type, parent_type FROM log`语句获取child、child\_type、parent和child\_type。提取字段后，日志服务会根据这些字段生成拓扑图，并支持通过 **力导向布局**、 **层次布局** 或 **环形布局** 展示。

![拓扑图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3658339561/p472848.png)

添加拓扑图的入口，请参见 [添加统计图表到仪表盘](https://help.aliyun.com/zh/sls/add-a-chart-to-a-dashboard#task-2141885 "")。

## **产品试用**

SLS Playground已内置拓扑图Demo，便于您快速了解及体验功能。您可以单击如下链接，进行试用。

- [基础拓扑图](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/charts-demo/dashboard/dashboard-1690440496106-807811%3FisShare%3Dtrue)

- [拓扑图-不同布局方式](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/charts-demo/dashboard/dashboard-1690440967318-198936%3FisShare%3Dtrue)



**重要**





SLS Playground中的数据为演示数据，请勿用于生产环境。


## 配置示例

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。在Project列表区域，单击目标Project。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4136568071/p768895.png)

2. 在左侧导航栏中，选择**仪表盘** \> **仪表盘列表**。在 **仪表盘** 列表中，单击目标仪表盘。在目标仪表盘右上角，单击 **编辑**。在仪表盘编辑模式下，单击**添加** \> **添加新图表**。

3. 参考下图，在页面右侧配置 **拓扑配置** 和 **布局配置**，在页面左侧配置查询时间范围、Logstore、查询分析语句。然后单击页面上方的 **应用** 查看图表配置效果。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0911540371/p860915.png)

获取child\_service、parent\_service和type的查询分析语句如下。提取字段后，日志服务根据这些字段生成拓扑图。















```sql
version: service | select child_service, parent_service, 'SERVER' as type from log
```


## 通用配置

通用配置用于对拓扑图进行全局配置。

- 基本配置




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **标题** | 设置图表的标题。 |
| **显示标题** | 打开 **显示标题** 开关后，将在图表中显示标题。 |
| **显示边框** | 打开 **显示边框** 开关后，将在图表中显示边框。 |
| **显示背景** | 打开 **显示背景** 开关后，将在图表中显示背景颜色。 |
| **显示时间** | 打开 **显示时间** 开关后，将在图表中显示查询时间。 |
| **固定时间** | 打开 **固定时间** 开关后，将固定查询分析的时间，不受仪表盘全局时间的影响。 |

- 拓扑配置




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **Child节点类型** | 选择代表子节点类型的字段。 |
| **Child节点ID** | 选择代表子节点ID的字段。 |
| **Parent节点类型** | 选择代表父节点类型的字段。 |
| **Parent节点ID** | 选择代表父节点ID的字段。 |





**说明**





  - 日志服务拓扑图中已内置13种不同类型的节点图标，分别表示Server、Database、WEB、MQ、SLB、WAF、OSS、DNS、Switch、Router、Android、iOS、Windows节点。

  - 如果您不指定节点类型（不配置 **Child节点类型** 和 **Parent节点类型**），则日志服务将默认使用Server节点的图标展示节点。


- 变量替换




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **变量替换** | 变量替换相当于为单个统计图表添加变量类型的过滤器。您在 **通用配置** 中设置了变量替换后，日志服务将在当前统计图表的左上边添加一个过滤器。您可以在过滤器中选择对应的值，日志服务会自动将查询和分析语句中的变量替换为您所选择的变量值，执行一次查询和分析操作。配置示例，请参见 [示例2：设置变量替换](https://help.aliyun.com/zh/sls/user-guide/variables#section-kpb-7oz-0v8 "")。 |


## 节点指标配置

完成通用配置后，日志服务将生成拓扑图，但仅展示各个节点的依赖关系，无指标数据。此时您可以通过节点指标配置，在拓扑图中添加节点指标信息。

指标数据样例如下图所示。其中，node字段表示节点，对应拓扑数据中的child、parent字段，因此您可以通过node字段关联指标数据和拓扑数据，为拓扑图补充节点指标信息。![拓扑图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5278809561/p472916.png)

日志服务支持对不同类型的节点配置不同的指标，此处以WEB类型的节点为例（ **A > WEB**）。

在 **A > WEB** 中选择指标数据所在的Project和Logstore，再输入查询和分析语句获取指标字段，然后添加指标字段的配置。例如metric\_1表示延迟时间，您可以通过`* | SELECT max(metric_1) AS maxLantency, min(metric_1) AS minLantency, node FROM log GROUP BY node`语句计算其最大值和最小值获取节点的最大延迟和最小延迟。

配置完成后，您将鼠标悬浮在拓扑图的节点上，即可查看该节点的指标数据。单击该节点，系统将隐藏不相关的节点和连线。

![拓扑图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5278809561/p472920.png)

## 连线指标配置

拓扑图中的节点依赖关系由分析语句和字段确定，不同类型的连线对应不同的分析语句。如果您要配置连线指标，需要在提取拓扑节点的查询和分析语句中指定代表连线指标的字段。

拓扑数据中包含连线指标数据，例如拓扑数据中的metric\_1表示响应时间，metric\_2表示延迟时间。您可以通过查询分析A提取指标字段metric\_1和metric\_2，然后在 **连线指标配置** 中，添加这两个字段的配置。

配置完成后，您将鼠标悬浮在拓扑图的连线上，即可查看对应的指标数据。单击该连线，系统将隐藏不相关的节点和连线。

![拓扑图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4248051661/p472948.png)

## 交互事件

拓扑图中的交互事件用于对节点进行下钻分析，加深数据分析的维度。交互事件包括打开日志库、打开快速查询、打开仪表盘、打开Trace分析、打开Trace详情和自定义HTTP链接。更多信息，请参见 [为仪表盘添加交互事件实现下钻分析](https://help.aliyun.com/zh/sls/drill-down-events#concept-v5f-zk4-x2b "")。

例如 **A > SERVER** 表示对查询分析A中的SERVER节点设置交互事件。将SERVER节点的交互事件设置为 **自定义HTTP链接**，则您右键单击拓扑图中的SERVER节点，然后单击 **自定义HTTP链接**，将跳转到您所设置的链接中。

![拓扑图](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5278809561/p472987.png)