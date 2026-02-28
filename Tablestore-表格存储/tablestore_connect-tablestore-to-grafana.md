### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[数据可视化](https://help.aliyun.com/zh/tablestore/data-visualization-tools/)对接Grafana

# 对接Grafana

更新时间：2025-10-22 22:47:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：数据可视化](https://help.aliyun.com/zh/tablestore/data-visualization-tools/)[下一篇：对接DataV-Board 7.0](https://help.aliyun.com/zh/tablestore/connect-tablestore-to-datav7-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

背景信息

注意事项

步骤一：安装表格存储插件

步骤二：配置数据源

步骤三：创建大盘面板

步骤四：查看监控数据

表格存储对接Grafana后，您可以通过Grafana可视化展示表格存储中的数据。

## 前提条件

- 在访问控制RAM服务侧完成如下操作：

已 [创建RAM用户](https://help.aliyun.com/zh/ram/create-a-ram-user-1 "") 并 [为RAM用户授予](https://help.aliyun.com/zh/ram/grant-permissions-to-a-ram-user "") 管理表格存储权限（AliyunOTSFullAccess）。



**警告**





阿里云账号AccessKey泄露会威胁您所有资源的安全。建议您使用RAM用户AccessKey进行操作，可以有效降低AccessKey泄露的风险。

- 在表格存储服务侧已完成如下操作：

  - [开通服务和创建实例](https://help.aliyun.com/zh/tablestore/product-overview/activate-service-and-create-a-instance "")。

  - 已创建 [数据表](https://help.aliyun.com/zh/tablestore/table-operations "") 和 [时序表](https://help.aliyun.com/zh/tablestore/operations-of-time-series-table "")。

  - 已 [创建表的映射关系](https://help.aliyun.com/zh/tablestore/create-mapping-tables-for-tables-of-sql-query#concept-2098376 "") 和 [创建多值模型映射关系](https://help.aliyun.com/zh/tablestore/use-sql-to-query-time-series-data-of-tablestore#section-0hm-38a-6uh "")。
- 已安装开源Grafana，且Grafana版本必须大于8.0.0，本文以 **Grafana v10.4.2** 为例进行介绍。关于安装Grafana的更多信息，请参见 [Grafana官方文档](http://docs.grafana.org/installation/)。



**说明**





您也可以使用阿里云可观测可视化 Grafana 版，默认已集成阿里云表格存储（Tablestore）。具体操作，请参见 [添加并使用Tablestore数据源](https://help.aliyun.com/zh/grafana/user-guide/add-and-use-a-tablestore-data-source#task-2112952 "")。


## 背景信息

Grafana是一款开源的可视化和分析平台，支持Prometheus、Graphite、OpenTSDB、InfluxDB、Elasticsearch、MySQL、PostgreSQL等多种数据源的数据查询、可视化等。更多信息，请参见 [Grafana官方文档](http://docs.grafana.org/installation/)。

表格存储的表数据接入Grafana后，Grafana可以根据表数据生成大盘面板，将数据实时展示给需要的用户。

## 注意事项

目前表格存储支持使用Grafana实现数据可视化功能的地域有华东1（杭州）、华东2（上海）、华北2（北京）、华北3（张家口）、华南1（深圳）和新加坡。

## 步骤一：安装表格存储插件

Windows

Mac/Linux

1. 下载表格存储Grafana插件包。具体下载路径为 [表格存储Grafana插件包](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20220527/ygdf/tablestore-grafana-plugin-1.0.0.zip)。

2. 解压表格存储Grafana插件包，并将表格存储Grafana插件包放到Grafana插件的plugins-bundled目录中。

3. 修改Grafana配置文件。

1. 使用文本编辑器工具打开Grafana插件conf目录中的配置文件defaults.ini。

2. 在配置文件的 **\[plugins\]** 节点中，设置allow\_loading\_unsigned\_plugins参数。

















      ```shell
      allow_loading_unsigned_plugins = aliyun-tablestore-grafana-datasource
      ```
4. 在任务管理器中重启grafana-server.exe进程。


1. 执行以下命令下载表格存储Grafana插件包。

















```shell
wget https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20220527/ygdf/tablestore-grafana-plugin-1.0.0.zip
```

2. 将表格存储Grafana插件包解压到Grafana插件目录。



根据Grafana的安装方式执行对应命令。



   - 使用YUM或RPM安装的Grafana（只适用于Linux平台）：unzip tablestore-grafana-plugin-1.0.0.zip -d /var/lib/grafana/plugins

   - 使用.zip文件安装的Grafana：unzip tablestore-grafana-plugin-1.0.0.zip -d {PATH\_TO}/grafana-{VERSION}/data/plugins



     **说明**





     其中`{PATH_TO}/grafana-{VERSION}`为Grafana的安装路径，`{VERSION}`为Grafana的版本号。


3. 修改Grafana配置文件。

1. 进入文件目录打开配置文件。



      - 使用YUM或RPM安装的Grafana（只适用于Linux平台）：/etc/grafana/grafana.ini

      - 使用.zip文件安装的Grafana：{PATH\_TO}/grafana-{VERSION}/conf/defaults.ini



        **说明**





        其中`{PATH_TO}/grafana-{VERSION}`为Grafana的安装路径，`{VERSION}`为Grafana的版本号。


2. 在配置文件的 **\[plugins\]** 节点中，设置allow\_loading\_unsigned\_plugins参数。

















      ```shell
      allow_loading_unsigned_plugins = aliyun-tablestore-grafana-datasource
      ```
4. 重启Grafana。

1. 使用kill命令终止Grafana进程。

2. 执行以下命令启动Grafana。



      - 使用YUM或RPM安装的Grafana（只适用于Linux平台）：systemctl restart grafana-server

      - 使用.zip文件安装的Grafana：./bin/grafana-server web

## 步骤二：配置数据源

1. 登录Grafana。

1. 在浏览器中输入`http://<x.x.x.x>:3000/`，进入Grafana登录界面。



      **说明**





      `<x.x.x.x>`代表Grafana的IP地址。以Grafana安装在Windows环境为例，登录地址为`http://localhost:3000`。

2. 输入Email or username和Password，单击 **Log in**。



      **说明**





      Grafana默认初始登录用户名和密码均为admin。首次登录时，请根据系统提示修改初始密码。
2. 在Grafana首页，单击页面左上角的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5002963271/p834449.png)图标。

3. 在Grafana左侧导航栏，选择**Connections** \> **Data sources**。

4. 在 **Data sources** 页面，单击 **\+ Add new data source**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5002963271/p834485.png)

5. 在 **Add data source** 页面的Others区域，单击 **aliyun-tablestore-grafana-datasource**。

6. 在 **Settings** 页面，根据下表说明配置相关参数。




| **参数** | **示例值** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **示例值** | **说明** |
| Name | aliyun-tablestore-grafana-datasource | 数据源名称，可自定义。默认为aliyun-tablestore-grafana-datasource。 |
| Endpoint | https://myinstance.cn-hangzhou.ots.aliyuncs.com | 表格存储实例的服务地址，请根据访问的表格存储实例填写。更多信息，请参见 [服务地址](https://help.aliyun.com/zh/tablestore/product-overview/endpoints#concept-bsx-btj-bfb "")。 |
| Instance | myinstance | Tablestore实例名称。 |
| AccessId | \\*\\*\\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* | 拥有表格存储访问权限的阿里云账号或者RAM用户的AccessKey ID。 |
| AccessKey | \\*\\*\\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* | 拥有表格存储访问权限的阿里云账号或者RAM用户的AccessKey Secret。 |

7. 单击 **Save & test**。


连接成功后，界面会显示 **Data source is working** 信息。



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5002963271/p834459.png)


## 步骤三：创建大盘面板

1. 在Grafana首页，单击页面左上角的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5002963271/p834449.png)图标。

2. 在Grafana左侧导航栏，单击 **Dashboards**

3. 在 **Dashboards** 页面，单击 **New**，然后选择 **New dashboard**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5002963271/p834465.png)

4. 在 **New dashboard** 页面，单击 **\+ Add visualization**。

5. 在 **Select data source** 对话框，选择配置完成的TableStore数据源。

![image](<Base64-Image-Removed>)

6. 在 **Edit** 页面 **Query** 区域配置查询条件。



配置参数说明请参见下表。






| **参数** | **示例** | **说明** |
| --- | --- | --- |



|     |     |     |
| --- | --- | --- |
| **参数** | **示例** | **说明** |
| Query | `SELECT * FROM your_table WHERE $__unixMicroTimeRangeFilter(_time)AND _m_name = "your_measurement" AND tag_value_at(_tags, "your_tag")="your_tag_value"LIMIT 1000` | SQL查询语句。更多信息，请参见 [查询数据](https://help.aliyun.com/zh/tablestore/query-data#concept-2098388 "")。<br>**重要**<br>   - 在WHERE子句中要通过预定义宏过滤时间范围，即示例中的`$__unixMicroTimeRangeFilter`。更多的时间宏函数请单击配置页面中的“Show Help”查看。<br>     <br>   - 如果以时序图形式展示，则需要返回以数字时间戳形式表示的时间列，并配置时间列的列名。 |
| Format As | Timeseries | 结果处理形式。取值范围如下：<br>   - Timeseries（默认）：普通时序图。<br>     <br>   - FlowGraph：多维图表展示。<br>     <br>   - Table：普通表格形式。 |
| Time Column | \_time | 返回数据中时间列的列名，时间列会作为时序图的横坐标。当选择Format As为 **Timeseries** 或者 **FlowGraph** 时可配置。 |
| Aggregation Column | \_field\_name#:#\_double\_value | 将同一时间点的多行单列数据转换为同一时间点的单行多列数据，适用于将Tablestore时序SQL产生的单值模型数据转换为多值模型数据。当选择Format As为 **FlowGraph** 时可配置。格式为`<数据点名称列>#:#<数值列>`。 |

7. 单击 **Run SQL**，执行SQL语句查看数据和调试。

8. 设置并保存大盘面板。

1. 在右侧设置监控图表的名称、类型、展示样式等。



      ![fig_20220426_dashboard](<Base64-Image-Removed>)

2. 单击右上角的 **Apply**。

3. 单击右上角的 **Save**，在 **Save dashboard** 对话框，设置Title、Description和大盘归属的Folder后，然后单击 **Save**。

## 步骤四：查看监控数据

1. 在Grafana首页，单击页面左上角的![image](<Base64-Image-Removed>)图标。

2. 在Grafana左侧导航栏，选择 **Dashboards**，单击目标目录下的监控大盘，即可查看目标大盘上的所有监控图表。