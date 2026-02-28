### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[时序模型](https://help.aliyun.com/zh/tablestore/timeseries-model-introductions/)时间线操作

# 时间线操作

更新时间：2025-04-03 03:28:48

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：时序数据生命周期](https://help.aliyun.com/zh/tablestore/time-series-data-lifecycle)[下一篇：时序数据操作](https://help.aliyun.com/zh/tablestore/basic-data-operations-of-timeseriestable/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能概述

操作步骤

开发集成

常见问题

时间线元数据也称为时间序列元数据，主要由时间线标识、属性和更新时间组成。本文将为您介绍如何管理时间线元数据。

## **功能概述**

写入时序数据前，您可以预先定义时间线。如果未预先新建时间线元数据，当写入时序数据时，系统会自动提取该时间线的元数据信息并自动构建索引。

时间线元数据生成后，您可以根据所需场景管理时间线元数据。

| **功能** | **描述** |
| --- | --- |

|     |     |
| --- | --- |
| **功能** | **描述** |
| 检索时间线 | 根据度量名称条件、数据源条件、标签条件、更新时间条件、属性条件或者多条件组合条件检索时间线。 |
| 更新时间线 | 更新时间线元数据的属性，目前仅在时间线元数据生命周期为-1（数据永不过期）时支持此操作。 |
| 删除时间线 | 批量删除时间线元数据。<br>**说明**<br>删除时间元数据时并不会删除时间线对应的时序表数据，通过指定时间线标识的方式仍然可以查询到这些时序数据。 |

## **操作步骤**

您可以使用控制台检索时间线或者更新时间线元数据。

检索时间线

更新时间线

删除时间线

1. 进入 **实例管理** 页面。

1. 登录 [表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择资源组和地域。

3. 在 **概览** 页面，单击实例别名或在实例 **操作** 列单击 **实例管理**。
2. 在 **实例详情** 页签，单击 **时序表列表** 页签。

3. 在 **时序表列表** 页签，单击时序表名称后选择 **数据管理** 页签或在时序表 **操作** 列单击 **数据管理**。

4. 在 **数据管理** 页签，单击右上角的 **查询时间线**。

5. 在 **查询数据** 对话框，根据实际需要输入度量名称、数据源以及单击对应区域的 **添加** 设置标签、属性或者更新时间的匹配条件。

下图中条件用于查询度量名称为cpu，标签中含有`os=Ubuntu16.10`的所有时间线。![fig_querytimeseries](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4357463471/p343180.png)

6. 单击 **确定**。

符合查询条件的数据将显示在 **数据管理** 页签。


1. 进入 **实例管理** 页面。

1. 登录 [表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择资源组和地域。

3. 在 **概览** 页面，单击实例别名或在实例 **操作** 列单击 **实例管理**。
2. 在 **实例详情** 页签，单击 **时序表列表** 页签。

3. 在 **时序表列表** 页签，单击时序表名称后选择 **数据管理** 页签或在时序表 **操作** 列单击 **数据管理**。

4. 在 **数据管理** 页签，单击时间线 **操作** 列的 **更新**。

5. 在 **更新时间线** 对话框，根据需要添加、删除或者修改时间线元数据属性。

6. 单击 **确定**。


目前仅支持使用SDK方式删除时间线。

## **开发集成**

| **功能** | **调用方式** |
| --- | --- |

|     |     |
| --- | --- |
| **功能** | **调用方式** |
| 检索时间线 | - 通过SDK： [Java](https://help.aliyun.com/zh/tablestore/developer-reference/retrieve-time-series-by-using-java-sdk "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/retrieve-time-series "")、 [Python](https://help.aliyun.com/zh/tablestore/developer-reference/retrieve-time-series-metadata-by-python-sdk "")<br>  <br>- 通过命令行工具： [检索时间线](https://help.aliyun.com/zh/tablestore/developer-reference/operations-on-time-series-data#section-uvy-5mr-wq3 "")、 [扫描时间线](https://help.aliyun.com/zh/tablestore/developer-reference/operations-on-time-series-data#section-cw4-maf-cqa "") |
| 更新时间线 | - 通过SDK： [Java](https://help.aliyun.com/zh/tablestore/developer-reference/update-time-series-metadata-by-using-java-sdk "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/update-time-series-metadata-by-using-go-sdk "")、 [Python](https://help.aliyun.com/zh/tablestore/developer-reference/update-time-series-metadata-by-python-sdk "")<br>  <br>- [通过命令行工具](https://help.aliyun.com/zh/tablestore/developer-reference/operations-on-time-series-data#section-4px-ppx-axo "") |
| 删除时间线 | 通过SDK： [Java](https://help.aliyun.com/zh/tablestore/developer-reference/delete-time-series-metadata-by-using-java-sdk "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/delete-time-series-metadata-by-using-go-sdk "")、 [Python](https://help.aliyun.com/zh/tablestore/developer-reference/delete-time-series-metadata-by-python-sdk "") |

## **常见问题**

[如何删除时序数据](https://help.aliyun.com/zh/tablestore/how-to-delete-data-in-a-time-series-table "")