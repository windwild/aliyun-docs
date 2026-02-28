### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据监控](https://help.aliyun.com/zh/sls/data-monitoring/)[可视化](https://help.aliyun.com/zh/sls/visualization-2/)[统计图表](https://help.aliyun.com/zh/sls/statistical-charts/)[统计图](https://help.aliyun.com/zh/sls/single-value-chart/)配置趋势图

# 配置趋势图

更新时间：2025-09-14 22:45:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：统计图](https://help.aliyun.com/zh/sls/single-value-chart/)[下一篇：设置统计图表阈值](https://help.aliyun.com/zh/sls/set-statistics-chart-threshold)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

效果概览

步骤一：查询和分析

步骤二：配置趋势图

1\. 添加趋势图

2\. 配置标题

3\. 配置趋势图

4\. 配置对比值

5\. 保存趋势图和仪表盘

日志服务支持配置趋势图，帮助您分析日志数据的变化趋势，本文介绍如何配置趋势图。

## 前提条件

- 已采集数据。具体操作，请参见 [采集主机文本日志](https://help.aliyun.com/zh/sls/collect-host-logs "")。

- 已创建索引。具体操作，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#task-jqz-v55-cfb "")。

- 已创建仪表盘。具体操作，请参见 [快速创建仪表盘](https://help.aliyun.com/zh/sls/dashboard-overview "")。


## **效果概览**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5434097571/p1004979.png)

1. **查询和分析**：在控制台中统计网页PV值，确保日志数据的完整性和准确性。

2. **配置趋势图**：添加名为`statistical-chart`的趋势图，并为其配置对比值，最后将趋势图添加到目标仪表盘中。


## 步骤一：查询和分析

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。在Project列表区域，单击目标Project。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4136568071/p768895.png)

2. 在控制台左侧，单击 **日志存储**，在 **日志库** 列表中单击目标Logstore。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7260561371/p868223.png)

3. 输入如下查询和分析语句，统计网页PV值。然后单击 **查询/分析**，查看日志。















```sql
*| select diff[1] as pv, diff[2] as previous_day_pv, (diff[1] - diff[2])/diff[2] as growth
from (
       select compare(pv, 86400) as diff
       from (
           select count(1) as pv
           from log
       )
)
```


## **步骤二：** 配置趋势图

### **1\. 添加趋势图**

在左侧导航栏中，选择**仪表盘** \> **仪表盘列表**。在 **仪表盘** 列表中，单击目标仪表盘。在目标仪表盘右上角，单击 **编辑**。在仪表盘编辑模式下，单击**添加** \> **添加新图表**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7260561371/p868298.png)

### **2\.** 配置 **标题**

在页面右侧选择**通用配置** \> **图表类型** \> **![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4338522371/p874204.png)**，选择**通用配置** \> **基本配置** \> **标题**配置统计图表为`statistical-chart`。

![image](<Base64-Image-Removed>)

### **3\. 配置趋势图**

在页面右侧，设置**通用配置** \> **图表样式** \> **颜色模式**为 **背景** 和**通用配置** \> **图表样式** \> **图像模式**为 **趋势图**。

- **通用配置** \> **图表样式** \> **颜色模式**：选择 **背景**，表示为背景和趋势图设置颜色，系统默认为绿色。

- **通用配置** \> **图表样式** \> **图像模式**：统计图以 **趋势图** 展示。


![image](<Base64-Image-Removed>)

### 4\. 配置对比值

参考下图，在页面右侧 **通用配置** 页签下配置 **查询分析设置**，在页面左侧配置查询时间范围、Logstore和查询分析语句，然后单击页面上方的 **应用** 查看图表配置效果。

- **通用配置** \> **查询分析设置** \> **显示字段**：选择查询分析语句A中的`PV`字段在趋势图中显示。

- **通用配置** \> **查询分析设置** \> **对比字段**：选择`growth`字段表示变化值。

- **通用配置** \> **查询分析设置** \> **对比值描述**：输入`同比昨天`作为对比值的描述。

- **通用配置** \> **查询分析设置** \> **对比值格式化**：`growth`表示变化率，因此设置对比值的显示格式为`percent(1-100)`。

- **通用配置** \> **查询分析设置** \> **小数点后位数**：设置小数点后保留两位。


![image](<Base64-Image-Removed>)

### 5\. 保存趋势图和仪表盘

1. 在统计图表的编辑页面的右上角，单击 **确定**。

![image](<Base64-Image-Removed>)

2. 在仪表盘的编辑页面的右上角，单击 **保存**。

![image](<Base64-Image-Removed>)