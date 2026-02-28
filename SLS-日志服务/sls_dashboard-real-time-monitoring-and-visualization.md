### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据监控](https://help.aliyun.com/zh/sls/data-monitoring/)[可视化](https://help.aliyun.com/zh/sls/visualization-2/)[仪表盘](https://help.aliyun.com/zh/sls/dashboard/)使用仪表盘

# 使用仪表盘

更新时间：2026-01-05 00:52:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：快速创建仪表盘](https://help.aliyun.com/zh/sls/dashboard-overview)[下一篇：使用仪表盘快速发现异常指标](https://help.aliyun.com/zh/sls/use-dashboards-to-quickly-discover-abnormal-metrics)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

预期效果

查看仪表盘列表

仪表盘列表

演示列表

仪表盘模式

显示模式

编辑模式

使用仪表盘

刷新仪表盘

查询仪表盘

分享仪表盘

订阅仪表盘

为仪表盘添加过滤器

播放仪表盘

下钻分析

支持的图表类型

表格（Pro版本）

线图（Pro版本）

柱状图（Pro版本）

统计图（Pro版本）

饼图（Pro版本）

地图（Pro版本）

相关文档

日志服务可视化是将系统、应用或服务生成的原始日志数据转换成图形化界面展示的过程。本文介绍如何使用仪表盘。

## **预期效果**

日志服务仪表盘包含丰富的图表类型，可以灵活地设置图表样式，以满足各类场景对展示数据的不同需求。

![shybp.gif](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4528923371/p882938.gif)

## 查看仪表盘列表

在日志服务中，![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p845001.png)图标代表 **仪表盘**，![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9747026271/p845005.png)图标代表 **仪表盘列表**，![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9747026271/p845009.png)图标代表 **演示列表**。

### **仪表盘列表**

单击**仪表盘** \> **仪表盘列表**，查看当前Project下的所有仪表盘。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4474517271/p852254.png)

### **演示列表**

单击**仪表盘** \> **演示列表**，查看当前Project下的所有演示列表。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4474517271/p852518.png)

## 仪表盘模式

### **显示模式**

查看仪表盘时，系统默认呈现显示模式，允许您浏览该仪表盘下的所有统计图表。此外，日志服务还提供了在显示模式下对仪表盘进行刷新、订阅及分享等操作的功能。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p847648.png)

显示模式操作说明

|     |     |
| --- | --- |
| **区域** | **操作说明** |
| 仪表盘列表区域 | 单击**仪表盘** \> **仪表盘列表**，可以看到当前Project下所有的仪表盘。单击目标仪表盘，进入到显示模式。 |
| 操作区域 | - **时间选择**：您可以 [设置仪表盘的查询时间](https://help.aliyun.com/zh/sls/dashboard-real-time-monitoring-and-visualization#3793479e38iyg "")，设置后，所有统计图表展示的是同一时段的查询和分析结果。<br>  <br>- **SQL增强**：您可以运行SQL增强，用于优化查询分析语句。<br>  <br>- **刷新**：您可以通过 [手动刷新或自动刷新](https://help.aliyun.com/zh/sls/dashboard-real-time-monitoring-and-visualization#a15ac7b9bdamu "") 两种方式刷新仪表盘。<br>  <br>- **重置**：重置所有图表的查询时间范围，恢复至默认时间范围，用于改变时间范围后还原到初始状态的场景。<br>  <br>- **告警**：您可以为图表 [创建告警规则](https://help.aliyun.com/zh/sls/configure-an-alert-monitoring-rule-in-log-service#task-2053407 "")。<br>  <br>- **订阅**： [订阅仪表盘](https://help.aliyun.com/zh/sls/dashboard-real-time-monitoring-and-visualization#0be096f5aepci "") 后，您可以定期将仪表盘渲染为图片，通过邮件、钉钉等方式发送给指定人员。<br>  <br>- **另存为**：复制并保存为目标仪表板的新独立版本，完成后刷新页面，在仪表盘列表中查看。<br>  <br>- **分享**：您可以将仪表盘 [免密分享](https://help.aliyun.com/zh/sls/secret-free-sharing-and-integrated-dashboard "") 给其他人。<br>  <br>- **全屏**：您可以选择 **显示器全屏** 或者 **窗口全屏**，当您不需要全屏展示时，您可以按Esc键退出全屏。<br>  <br>- **仪表盘体验调研**：反馈您宝贵的意见。<br>  <br>- **编辑**：进入仪表盘编辑模式。 |
| 过滤器 | 当您为仪表盘 [添加过滤器](https://help.aliyun.com/zh/sls/user-guide/add-a-filter "") 后，仪表盘会显示您创建的过滤器。 |
| 图表区域 | 单击 **![配置监控与告警](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2453749951/p104976.png)** 对单个图表可以进行窗口放大 **查看**、 **创建免密分享**、 **预览查询语句**、 **选择时间范围**、 **另存为告警**、以PNG图片格式 **下载图表** 或者以CSV格式 **下载图表数据**。 |

### **编辑模式**

单击仪表盘页面的 **编辑** 进入编辑模式后，您能够进行如下操作：修改仪表盘名称、添加新图表、调整布局、编辑现有图表以及导入图表等。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9747026271/p847647.png)

编辑模式操作说明

|     |     |
| --- | --- |
| **区域** | **操作说明** |
| 仪表盘列表区域 | 单击**仪表盘** \> **仪表盘列表**，可以看到当前Project下所有的仪表盘。单击目标仪表盘，在仪表盘右上角单击 **编辑** 进入编辑模式。 |
| 操作区域 | - **撤销**：取消最近一次对图表的修改，恢复到上一次保存或操作的状态。<br>  <br>- **重做**：撤销后的反向操作，恢复最近一次被撤销的修改。<br>  <br>- **层级置顶**：将选中的图表提升到所有元素之上，确保它显示在最前面。<br>  <br>- **层级置底**：将选中的图表放置到所有元素之下，使其显示在最底层。<br>  <br>- **设置对齐方式**：调整图表的对齐方式，如左对齐、右对齐等。<br>  <br>- **设置图表位置和大小**：调整图表左边距、上边距、高度和宽度。<br>  <br>- **过滤器**：通过 [添加过滤器](https://help.aliyun.com/zh/sls/dashboard-real-time-monitoring-and-visualization#35f47c5ec57pf "") 可对整个仪表盘进行查询过滤。<br>  <br>- **删除**：当您选中一个或多个图表时，可批量删除。<br>  <br>- **添加**：您可以为仪表盘添加 **图表**、 **连线** 和 **图形**。<br>  <br>  <br>  - **图表**：单击 **添加新图表**，为仪表盘添加 [统计图表（Pro版本）](https://help.aliyun.com/zh/sls/user-guide/overview-of-charts "") 或 [统计图表](https://help.aliyun.com/zh/sls/chart-overview "")。<br>    <br>  - **连线**：选择 **连线类型**、 **线条样式**、 **线宽** 及 **线条颜色**。您可以为图表间添加并设置连线，<br>    <br>  - **图形**：为仪表盘添加 **矩形**、 **菱形**、 **文本** 或 **自定义SVG**。<br>    <br>- **导入图表**：向当前仪表盘导入新图表。<br>  <br>- **切换布局**：日志服务中仪表盘支持 **网格布局** 和 **自由布局** 两种布局模式，您可以自由切换。<br>  <br>- **历史版本**：您可以查看仪表盘的历史操作，如果您误操作了仪表盘，则可以使用此功能将其恢复到历史版本。<br>  <br>  <br>  <br>  **重要**<br>  <br>  <br>  <br>  <br>  <br>  - 支持最多保存20个历史版本。<br>    <br>  - 不支持通过API方式操作历史版本。<br>    <br>  - 恢复操作将覆盖当前仪表盘内容，请谨慎操作。<br>    <br>- **设置**：在仪表盘设置页面，可以恢复旧版本、修改仪表盘JSON和管理过滤器。<br>  <br>- **保存**：编辑模式下的所有操作，都必须保存后才会生效。<br>  <br>- **取消**：退出编辑模式。 |
| 图表区域 | 单击 **![配置监控与告警](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2453749951/p104976.png)** 对单个图表进行编辑、复制和删除。 |

## 使用仪表盘

### 刷新仪表盘

您可以通过手动或自动两种方式刷新仪表盘，具体操作如下所示。

![sx-ch.gif](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9747026271/p845702.gif)

- 在仪表盘页面的右上方，选择**刷新** \> **仅一次**，表示立即刷新一次仪表盘。

- 在仪表盘页面的右上方，选择**刷新** \> **自动刷新**，表示按照指定的时间间隔自动刷新仪表盘。时间间隔可设置为15秒、60秒、5分钟或15分钟。


### 查询仪表盘

您可以全局设置仪表盘的查询时间范围，设置后，所有统计图表展示的是同一时段的查询和分析结果。

**重要**

选定的查询时间范围仅供临时查看结果，系统不会保存。下次查看仪表盘时，系统仍使用默认的时间范围。

- **时间选择**

在仪表盘页面的上方，单击 **时间选择**，选择时间范围。选择时间范围后，将鼠标放在时间上，可查看具体的时间范围。




| **时间选择** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **时间选择** | **说明** |
| 相对时间 | 表示查询距离当前时间1分钟、5分钟、15分钟等时间区间的日志数据。例如当前时间为19:20:31，设置相对时间1小时，表示查询18:20:31~19:20:31的日志数据。 |
| 整点时间 | 表示查询最近整点1分钟、15分钟等时间区间的日志数据。例如当前时间为19:20:31，设置整点时间1小时，表示查询18:00:00~19:00:00的日志数据。 |
| 自定义时间 | 表示查询指定时间范围的日志数据。 |

- **查看特定条件的仪表盘**

在仪表盘页面的上方，单击 **时间选择**，选择时间范围后，再单击仪表盘过滤器，添加过滤条件，表示查询指定时间和指定条件下的日志数据。例如当前是2024-09-06日，设置时间为 **昨天（相对）**，添加`method`为`GET`，`status`为`200`的过滤条件，表示查询2024-09-05 00:00:00 ~ 2024-09-06 00:00:00内`method`为`GET`，`status`为`200`的日志数据。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p845741.png)


### **分享仪表盘**

创建仪表盘后，您可以分享到钉钉、企业微信或阿里云账号，也可以将仪表盘嵌入钉钉文档。具体操作，请参见 [免密分享与集成仪表盘](https://help.aliyun.com/zh/sls/secret-free-sharing-and-integrated-dashboard "")。

### **订阅仪表盘**

创建仪表盘后，您可以定期将仪表盘渲染为图片，通过邮件、钉钉等方式发送给指定人员。

**重要**

订阅仪表盘，有如下限制：

- 每个仪表盘只能创建一个订阅任务。

- 每天最多给每个邮箱发送50封邮件。

- 每个Project中订阅任务和告警任务的总数最多100个。如果有特殊需求，请提[工单](https://selfservice.console.aliyun.com/ticket/category/sls/today)申请调整限额。

- 如果表格分页显示，订阅仪表盘时，仅支持发送表格第一页的数据截图。

- 跨Project数据不支持订阅，如果仪表盘所查询的数据来源于另一个Project，订阅功能无法获取到这些数据。


![dy-ch.gif](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p845778.gif)

参数说明

|     |     |
| --- | --- |
| **参数** | **说明** |
| **订阅名称** | 订阅任务的名称。 |
| **频率** | 订阅仪表盘后，发送通知的频率。 <br>- **每小时**：每小时发送一次订阅通知。<br>  <br>- **每天**：在每天的某个固定时间点发送一次订阅通知。<br>  <br>- **每周**：在周几的某个固定时间点发送一次订阅通知。<br>  <br>- **固定间隔**：按固定间隔发送订阅通知，单位为天。<br>  <br>- **Cron**：通过Cron表达式指定时间间隔，Cron表达式最小单位为分钟，但建议设置间隔为1小时以上。例如Cron表达式为\\* 0/1 \* \* \*，表示从0点开始，每隔1小时发送一次。 |
| **全局时间** | - **预设**：发送订阅报表时，对应的查询时间范围为仪表盘中统计图表的查询时间范围。<br>  <br>  <br>  <br>  **说明**<br>  <br>  <br>  <br>  <br>  <br>  - 在仪表盘显示模式下，所有的查询时间范围都是临时的，仅供您动态查阅不同时间段的图表数据。<br>    <br>  - 在仪表盘编辑模式下，双击目标统计图表，然后在编辑页面，修改其查询时间范围。系统会保存该时间范围，即您下次查看该统计图表时，仍为该时间范围。<br>    <br>- **自定义**：发送订阅报表时，对应的查询时间范围为您在此处设置的自定义时间范围。 |
| **添加水印** | 在生成的图片上添加水印，水印内容为通知渠道地址，例如邮箱地址。 |
| **通知列表** | 订阅仪表盘的通知方式包括邮件、Webhook-钉钉机器人、Webhook-飞书机器人、Webhook-企业微信机器人和自定义Webhook。<br>- 邮件<br>  <br>  - 在 **收件人** 中填写邮箱地址，多个邮箱地址之间用英文逗号（,）分隔。<br>    <br>  - 在 **主题** 中配置邮件主题。如果没有配置主题，日志服务将使用默认主题（日志服务报表）。<br>- Webhook<br>  <br>  - 在 **请求地址** 中填写对应的WebHook地址。如何获取钉钉机器人的WebHook地址，请参见 [通知渠道说明](https://help.aliyun.com/zh/sls/notification-methods "")。<br>    <br>  - 在 **标题** 中配置通知标题。 |

### **为仪表盘添加过滤器**

为目标仪表盘添加过滤器后，您可以根据指定条件对仪表盘中的所有统计图表进行筛选，无需修改查询分析语句。具体操作，请参见 [添加过滤器](https://help.aliyun.com/zh/sls/add-filter#c6acaaadb5giz "")。

### 播放仪表盘

1. **创建演示列表**：当前Project中没有演示列表时，有2个入口可以创建，您可以单击 **立即创建** 或者![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1892252371/p877335.png)进行创建。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1892252371/p877333.png)

在 **创建演示列表** 对话框中，完成如下配置，然后单击 **确定**。




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **播放列表名称** | 设置播放列表的名称。 |
| **轮播间隔时间** | 设置仪表盘轮播的时间间隔。 |
| **目标仪表盘名称** | 添加目标仪表盘。支持跨Project添加仪表盘。 |

2. **播放仪表盘**：选择目标演示列表，单击右上角 **播放** 按钮，系统将根据您设置的时间间隔，自动播放您所添加的仪表盘。您也可以单击 **上一页**、 **下一页**，手动播放仪表盘。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6165929171/p813927.png)


### **下钻分析**

在仪表盘发现异常时，可以利用 [为仪表盘添加交互事件实现下钻分析](https://help.aliyun.com/zh/sls/drill-down-events "") 功能快速进行下钻分析，如在LogStore查询分析、Trace分析或访问其他仪表盘等，以实现定位异常根因。具体操作，请参见 [使用仪表盘下钻分析定位异常根因](https://help.aliyun.com/zh/sls/user-guide/use-instrument-cluster-drill-in-analysis-to-locate-the-root-cause "")。

## **支持的图表类型**

### **表格（Pro版本）**

表格由一组或多组单元格组成，表格中的项被组织为行和列，表格的第一行称为表头，指明表格每一列的内容和意义。例如查询每个`http_referer`对应的响应体总字节数，并用线图展示`body_bytes_sent`。

```sql
(*)| SELECT http_referer, array_agg(body_bytes_sent) as body_bytes_sent GROUP BY  http_referer
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p845910.png)

**使用场景**： [表格](https://help.aliyun.com/zh/sls/table/ "") 能够精确地展示每个数据项的具体数值。适用于数据分析、财务报表、科学实验记录等场景。

### **线图（Pro版本）**

线图属于趋势类分析图表，一般用于表示一组数据在一个有序数据类别（多为连续时间间隔）上的变化情况，用于直观分析数据变化趋势。例如查询每个时间点的页面访问量（PV），并设置上下浮动范围展示。

```sql
(*)| select __time__ - __time__ % 60 as time, COUNT(*) as pv, COUNT(*) + 50 as pv2, COUNT(*) - 50 as pv3 GROUP BY time order by time
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p845905.png)

**使用场景**： [线图](https://help.aliyun.com/zh/sls/line-chart/ "") 主要用于展示数据随时间或其他连续变量的变化趋势。适用于分析时间序列数据，如股票价格、气温变化、销售数据等场景。在线图中，可以清晰地观测到数据在某一个周期内的变化，例如：

- 递增性或递减性

- 增减的速率情况

- 增减的规律（如周期变化）

- 峰值和谷值


### **柱状图（Pro版本）**

柱状图使用垂直的柱子显示类别之间的数值比较，用于描述分类数据，并统计每一个分类中的数量。例如展示UV最高的前5个`host`及其页面访问量（PV）。

```sql
(*)| select host, COUNT(*) as pv, approx_distinct(remote_addr) as uv GROUP BY host ORDER BY uv desc LIMIT 5
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p845918.png)

**使用场景**： [柱状图](https://help.aliyun.com/zh/sls/column-chart "") 主要用于比较不同类别或不同时间点的数据大小。适用于展示分类数据，如不同产品的销售量、不同地区的人口数量等。

### **统计图（Pro版本）**

统计图可包含一个或多个单值图，单值图可用于突出显示单个数值。例如展示最近15分钟页面访问量（PV）。

```sql
(*)| select COUNT(*) as PV
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9747026271/p845933.png)

**使用场景**： [统计图](https://help.aliyun.com/zh/sls/single-value-chart/ "") 主要用于直观展示单个关键指标的当前数值及其变化趋势，适用于需要了解业务状态或监控异常情况的场景。

### **饼图（Pro版本）**

饼图通过将一个圆饼按照分类的占比划分成多个区块，整个圆饼代表数据的总量，每个区块（圆弧）表示该分类占总体的比例大小，所有区块（圆弧）的加和等于 100%。比如统计每个`request_method`（请求方法，如GET、POST等）的次数。

```sql
(*)| SELECT request_method, arbitrary(request_length) as len, COUNT(*) as c  group by request_method
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8747026271/p845927.png)

**使用场景**： [饼图](https://help.aliyun.com/zh/sls/pie-chart/ "") 主要用于展示数据的占比关系。它适用于展示不同部分在整体中的比例，如不同产品的市场份额、各个部门的预算比例等。

### **地图（Pro版本）**

以地图作为背景，通过图形颜色、图像标记的方式展示地理数据信息。比如按国家分组统计每个国家的记录数（count）。

```sql
(*)| select  ip_to_country(remote_addr) as address, count(1) as count group by address order by count desc limit 10
```

**使用场景**： [地图](https://help.aliyun.com/zh/sls/maps/ "") 用于展示地理空间数据。适用于分析地理位置相关的数据，如人口分布、城市扩张、交通流量等。

选择更多图表，请参见 [流图](https://help.aliyun.com/zh/sls/flow-chart/ "")、 [计量图](https://help.aliyun.com/zh/sls/bar-gauge/ "")、 [直方图](https://help.aliyun.com/zh/sls/histogram#concept-2251235 "")、 [雷达图](https://help.aliyun.com/zh/sls/radar-chart#concept-2234790 "")、 [交叉表](https://help.aliyun.com/zh/sls/cross-table#concept-2250610 "")、 [散点图](https://help.aliyun.com/zh/sls/scatter-chart#concept-2250611 "")、 [拓扑图](https://help.aliyun.com/zh/sls/topology-chart#concept-2236574 "")、 [火焰图](https://help.aliyun.com/zh/sls/flame-graph "")、 [Markdown图表](https://help.aliyun.com/zh/sls/manage-a-markdown-chart "")、 [时间轴](https://help.aliyun.com/zh/sls/display-query-results-on-a-timeline-chart "")、 [词云](https://help.aliyun.com/zh/sls/display-query-results-on-a-word-cloud "")、 [桑基图](https://help.aliyun.com/zh/sls/display-query-results-in-a-sankey-diagram "")、 [高德地图](https://help.aliyun.com/zh/sls/gaud-map "")、 [轨迹图](https://help.aliyun.com/zh/sls/display-query-results-on-a-trail-map "")、 [矩形树图](https://help.aliyun.com/zh/sls/display-query-results-on-a-treemap-chart "")、 [时序状态图](https://help.aliyun.com/zh/sls/timing-state-diagram "")、 [漏斗图](https://help.aliyun.com/zh/sls/display-query-results-on-a-funnel-chart "")。

## **相关文档**

- 创建仪表盘请参见 [快速创建仪表盘](https://help.aliyun.com/zh/sls/dashboard-overview "")，分享仪表盘请参见 [免密分享与集成仪表盘](https://help.aliyun.com/zh/sls/secret-free-sharing-and-integrated-dashboard "")。

- 使用仪表盘发现异常指标，请参见 [使用仪表盘快速发现异常指标](https://help.aliyun.com/zh/sls/use-dashboards-to-quickly-discover-abnormal-metrics "")，对异常进行分析，请参见 [使用仪表盘下钻分析定位异常根因](https://help.aliyun.com/zh/sls/user-guide/use-instrument-cluster-drill-in-analysis-to-locate-the-root-cause "")。

- 日志服务支持通过统计图表的方式对查询分析结果进行可视化展示，具体请参见 [统计图表概述](https://help.aliyun.com/zh/sls/chart-overview "") 和 [统计图表概述](https://help.aliyun.com/zh/sls/user-guide/overview-of-charts "")。

- 日志服务支持将查询和分析结果通过图表形式保存到仪表盘中，具体操作请参见 [添加统计图表到仪表盘](https://help.aliyun.com/zh/sls/add-a-chart-to-a-dashboard-1 "") 和 [添加统计图表到仪表盘](https://help.aliyun.com/zh/sls/add-a-chart-to-a-dashboard "")。

- 关于过滤器类型过滤器的操作示例，请参见 [添加过滤器类型的过滤器](https://help.aliyun.com/zh/sls/add-a-filter-of-the-filter-type#task-2089032 "")。关于变量类型过滤器的操作示例，请参见 [添加变量类型的过滤器](https://help.aliyun.com/zh/sls/add-a-filter-of-the-replace-variable-type#task-2089032 "")。