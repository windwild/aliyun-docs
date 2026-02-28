### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据监控](https://help.aliyun.com/zh/sls/data-monitoring/)[可视化](https://help.aliyun.com/zh/sls/visualization-2/)[统计图表](https://help.aliyun.com/zh/sls/statistical-charts/)统计图表属性

# 统计图表属性

更新时间：2024-12-24 21:23:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：添加统计图表到仪表盘](https://help.aliyun.com/zh/sls/add-a-chart-to-a-dashboard)[下一篇：查询分析](https://help.aliyun.com/zh/sls/statistical-charts-query-and-analysis)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

通用配置

字段配置

通用配置和字段配置的区别

统计图表支持对图表进行全局配置，也支持对单个查询分析结果或单个查询分析结果中的单列数据进行个性化设置。

## 通用配置

通用配置用于对统计图表进行全局配置，即您在 **通用配置** 中设置的图表属性，将对整个统计图表生效。

通用配置包括统计图表的基本配置、标准配置以及不同统计图表的不同属性配置。更多信息，请参见如下文档。

- [表格](https://help.aliyun.com/zh/sls/table/#task-2133734 "")

- [线图](https://help.aliyun.com/zh/sls/line-chart/#task-2133736 "")

- [流图](https://help.aliyun.com/zh/sls/flow-chart/#task-2134807 "")

- [柱状图](https://help.aliyun.com/zh/sls/column-chart#concept-2170547 "")

- [统计图](https://help.aliyun.com/zh/sls/single-value-chart/#concept-2209384 "")

- [计量图](https://help.aliyun.com/zh/sls/bar-gauge/#concept-2215599 "")

- [饼图](https://help.aliyun.com/zh/sls/pie-chart/#concept-2217286 "")

- [雷达图](https://help.aliyun.com/zh/sls/radar-chart#concept-2234790 "")

- [拓扑图](https://help.aliyun.com/zh/sls/topology-chart#concept-2236574 "")

- [交叉表](https://help.aliyun.com/zh/sls/cross-table#concept-2250610 "")

- [散点图](https://help.aliyun.com/zh/sls/scatter-chart#concept-2250611 "")

- [直方图](https://help.aliyun.com/zh/sls/histogram#concept-2251235 "")

- [高德地图](https://help.aliyun.com/zh/sls/gaud-map "")

- [桑基图](https://help.aliyun.com/zh/sls/display-query-results-in-a-sankey-diagram "")

- [词云](https://help.aliyun.com/zh/sls/display-query-results-on-a-word-cloud "")

- [矩形树图](https://help.aliyun.com/zh/sls/display-query-results-on-a-treemap-chart "")

- [漏斗图](https://help.aliyun.com/zh/sls/display-query-results-on-a-funnel-chart "")


通用配置用于对图表进行全局配置。

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

- 标准配置




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **格式化** | 设置数字的显示格式。 |
| **单位** | 设置数字的单位。 |
| **小数点后位数** | 设置数字的小数点后的位数。 |
| **显示名** | 设置显示字段的名称。<br>设置了显示名后，该图表中显示字段的名称都将变更为该值。如果您要修改某个名称，可以使用字段配置。 |
| **颜色方案** | 选择图表的颜色方案。<br>  - **内置**：使用内置颜色。<br>    <br>  - **单色**：选择一个颜色。<br>    <br>  - **阈值**：通过阈值的配置显示颜色。 |

- 阈值




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| 阈值模式 | 设置阈值的显示方式。 |
| **阈值** | 设置数据的阈值。<br>如果设置 **颜色方案** 为 **阈值** 且在此处设置了阈值，则系统将以对应的阈值颜色展示图表。 |

- 值映射




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **值映射** | 您可以使用单词或图标替换图表中的值。<br>例如设置 **值** 为 **200**， **映射类型** 为 **文本**， **映射值** 为 **成功**。则图表中的 **200** 将被替换为 **成功**。 |

- 变量替换




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **变量替换** | 变量替换相当于为单个统计图表添加变量类型的过滤器。您在 **通用配置** 中设置了变量替换后，日志服务将在当前统计图表的左上边添加一个过滤器。您可以在过滤器中选择对应的值，日志服务会自动将查询和分析语句中的变量替换为您所选择的变量值，执行一次查询和分析操作。配置示例，请参见 [示例2：设置变量替换](https://help.aliyun.com/zh/sls/user-guide/variables#section-kpb-7oz-0v8 "")。 |

- 文档链接




| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **添加文档链接** | 支持自定义设置文档链接或描述信息。设置后，相关信息将被展示在图表的右上角 |


## 字段配置

字段配置用于对单个查询分析结果或单个查询分析结果中的单列数据进行个性化的可视化设置，即您在 **字段配置** 中设置的图表属性，只对您所选择的目标查询分析结果所涉及的图形、目标查询分析结果中的单列数据所涉及的图形生效。

不同统计图表的字段配置说明及示例，请参见如下文档。

- [表格](https://help.aliyun.com/zh/sls/table/#task-2133734 "")

- [线图](https://help.aliyun.com/zh/sls/line-chart/#task-2133736 "")

- [流图](https://help.aliyun.com/zh/sls/flow-chart/#task-2134807 "")

- [柱状图](https://help.aliyun.com/zh/sls/column-chart#concept-2170547 "")

- [统计图](https://help.aliyun.com/zh/sls/single-value-chart/#concept-2209384 "")

- [计量图](https://help.aliyun.com/zh/sls/bar-gauge/#concept-2215599 "")

- [雷达图](https://help.aliyun.com/zh/sls/radar-chart#concept-2234790 "")

- [交叉表](https://help.aliyun.com/zh/sls/cross-table#concept-2250610 "")

- [散点图](https://help.aliyun.com/zh/sls/scatter-chart#concept-2250611 "")

- [直方图](https://help.aliyun.com/zh/sls/histogram#concept-2251235 "")

- [高德地图](https://help.aliyun.com/zh/sls/gaud-map "")

- [桑基图](https://help.aliyun.com/zh/sls/display-query-results-in-a-sankey-diagram "")

- [词云](https://help.aliyun.com/zh/sls/display-query-results-on-a-word-cloud "")

- [矩形树图](https://help.aliyun.com/zh/sls/display-query-results-on-a-treemap-chart "")

- [漏斗图](https://help.aliyun.com/zh/sls/display-query-results-on-a-funnel-chart "")


![字段配置](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9733927361/p355009.png)

## 通用配置和字段配置的区别

字段配置和通用配置的配置项基本相同，但适用的对象不同。通用配置针对整个统计图表，字段配置针对单个查询分析结果或单个查询分析结果中的单列数据。

例如在一个线图中展示当前1小时内两个网站的访问数量，并通过颜色和图例进行区分。如果在 **通用配置** 中设置 **显示名** 和 **颜色方案**，则两条线段的颜色和图例名都相同，无法满足需求。此时您可以通过字段配置，分别针对两个查询分析的结果进行个性化的可视化设置。

- 通用配置

设置 **颜色方案** 为 **单色**， **显示名** 为 **访问数量** 后，两条线的颜色和图例名相同。

![图表属性](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9093015561/p355231.png)

- 字段配置


  - **A > pv** 中的配置针对查询分析A结果中的PV列数据相关的线段。将该线段设置为红色，图例名为 **网站A的访问数量**。

  - **B > pv** 中的配置针对查询分析B结果中的PV列数据相关的线段。将该线段设置为黄色，图例名为 **网站B的访问数量**。


![图表属性](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9093015561/p355237.png)