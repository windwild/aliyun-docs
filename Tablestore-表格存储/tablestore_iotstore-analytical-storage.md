### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[时序模型](https://help.aliyun.com/zh/tablestore/timeseries-model-introductions/)[物联网存储IoTstore](https://help.aliyun.com/zh/tablestore/iotstore-introduction/)分析存储

# 分析存储

更新时间：2025-04-24 01:09:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：SQL查询](https://help.aliyun.com/zh/tablestore/sql-query)[下一篇：SQL查询样例](https://help.aliyun.com/zh/tablestore/sql-in-iotstore-analytical-storage)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能特性

核心优势

注意事项

准备工作

操作步骤

创建分析存储

SQL查询分析

查询分析存储描述信息

更新分析存储数据生命周期

删除分析存储

开发集成

计费说明

分析存储功能主要用于时序数据长期存储和分析场景。使用分析存储（Analytical Store）功能，您可以低成本存储时序数据以及快速查询和分析时序数据。

## **功能特性**

分析存储是表格存储针对时序场景进行定制优化的一种低成本存储引擎，具备高效的数据压缩存储能力和强大的查询分析功能，非常适合处理大规模数据分析任务。

该存储引擎具备自动同步时序表数据的能力。在数据写入速率稳定的情况下，同步操作的延迟通常控制在10分钟以内。当业务压力过大时，分析存储将优先保障存储的稳定性，因此同步延迟可能会略微增加。分析存储与时序表的数据存储相互独立，允许用户自定义数据的生命周期（TTL），对分析存储进行的查询操作不会影响时序表的读写性能。

分析存储支持的功能特性请参见下表。

| **功能特性** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **功能特性** | **说明** |
| 创建分析存储 | 您可以在创建时序表的同时为其配置分析存储，也可以为已有的时序表创建分析存储。在创建分析存储时，支持为其配置生命周期TTL以及同步方式（包括存量同步和增量同步）。 |
| SQL查询分析 | 分析存储支持通过SQL进行查询操作，在SQL中可以使用不同条件进行聚合分析操作。 |
| 查询分析存储描述信息 | 查询分析存储的配置信息、同步状态和存储数据大小。 |
| 更新分析存储数据生命周期 | 修改分析存储的数据生命周期TTL，以延长数据的保存时间或清理分析存储中的历史数据。 |
| 删除分析存储 | 您可以删除不再使用的分析存储，从而节省存储成本。 |

## 核心优势

- **低成本数据存储**

  - 冷热数据分层存储：针对于时序热数据，采用行列混合的宽表存储方式；而对于时序全量历史数据，则采用列存储方式。

  - 高数据压缩率存储：列存储能够更有效地利用数据的重复性，通过结合RLE、DICTIONARY、DELTA、BIT-PACKING等压缩编码方法，对数据进行压缩，从而提高存储空间的利用率，进而降低存储成本。
- **海量数据的实时分析**

  - 针对时序的热数据，采用表格存储行列混合的宽表存储方式，以支持海量数据的实时自增写、覆盖和查询。

  - 针对时序全量历史数据，采用列存储方式。在进行数据查询或分析时，仅读取所需的列数据，从而提高查询效率和数据处理速度。
- **灵活分层的TTL设置**

在同一张时序表上，对时序数据存储和分析存储采用了不同的数据生命周期管理策略。


## **注意事项**

- 一个时序表只能创建1个分析存储。

- 一个时序表的Lastpoint索引与分析存储的数量总和不得超过10个。


## **准备工作**

[创建时序模型实例](https://help.aliyun.com/zh/tablestore/create-instances-of-timeseries-model "")。

**说明**

支持分析存储功能的地域包括华东1（杭州）、华东2（上海）、华北2（北京）和华北3（张家口）。

## **操作步骤**

### **创建分析存储**

创建时序表时创建分析存储

为已有时序表创建分析存储

[创建时序表](https://help.aliyun.com/zh/tablestore/operations-of-time-series-table#527fab7ef6edy "") 时，系统默认已选中创建分析存储选项。

1. 进入 **实例管理** 页面。

1. 登录 [表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择资源组和地域。

3. 在 **概览** 页面，单击实例别名或者单击实例 **操作** 的 **实例管理**。
2. 在 **实例管理** 页面的 **实例详情** 页签，单击 **时序表列表** 页签。

3. 在 **时序表列表** 页签，单击时序表名。

4. 在 **基本详情** 页签的 **分析存储** 区域，单击 **创建分析存储**。

5. 在 **创建分析存储** 对话框，根据下表说明配置分析存储信息。


|     |     |
| --- | --- |
| **参数** | **说明** |
| 分析存储名称 | 分析存储的名称。分析存储的命名规范与时序表的命名规范一致。 |
| 生命周期 | 分析存储中数据的过期时间，单位为秒。取值必须为-1（数据永不过期）或者必须大于等于2592000秒（即30天）的int32正整数。<br>当系统判断当前时间减去用户传入数据列的时间已经超过设置的数据生命周期时，系统会自动清理超过数据生命周期的数据。<br>**说明**<br>   - 在分析存储中，系统判断数据产生时间以用户传入的时间列为准，并非数据写入表中的时间。<br>     <br>   - 分析存储的生命周期与时序表的数据生命周期互不影响。 |
| 同步方式 | 分析存储同步时序表中数据的方式。取值范围如下：<br>   - 全量同步：同步时序表中的存量数据和增量数据。<br>     <br>   - 增量同步：同步分析存储创建后时序表中增量变化的数据。<br>     <br>**重要**<br>同步方式设置后不支持修改，请谨慎选择。 |

6. 单击 **确定**。


### **SQL查询分析**

1. 进入 **时序表管理** 页面。

1. 登录 [表格存储控制台](https://otsnext.console.aliyun.com/)。

2. 在页面上方，选择资源组和地域。

3. 在 **概览** 页面，单击实例名称或者单击实例 **操作** 的 **实例管理**。

4. 在 **实例管理** 页面的 **实例详情** 页签，单击 **时序表列表** 页签。

5. 在 **时序表列表** 页签，单击时序表名称。
2. 创建分析存储的映射关系。

1. 在 **时序表管理** 页面的 **SQL查询** 页签，单击![fig_createtablevitural](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8030506561/p297541.png)图标。

2. 在 **创建映射表** 对话框中，根据下表说明配置参数。




      | **参数** | **描述** |
      | --- | --- |



      |     |     |
      | --- | --- |
      | **参数** | **描述** |
      | 表类型 | 指的表的类型。请选择 **时序表**。 |
      | 表名 | 时序表名称。 |
      | 映射表表名 | 映射表标识，支持自定义命名。<br>**说明**<br>时序表映射为sql会自动在映射表名前添加`时序表名::`前缀 |
      | 使用分析存储查询 | 打开 **使用分析存储查询** 开关，以使用分析存储引擎。 |

3. 单击 **生成SQL**。

4. 单击 **执行SQL(F8)**。

      在页面左侧区域将显示创建的时序表映射关系。
3. 使用SQL查询数据。

1. 在 **SQL查询** 页签，输入SELECT语句查询所需数据。

      有关SQL查询样例和支持的函数，请参见 [SQL查询样例](https://help.aliyun.com/zh/tablestore/sql-in-iotstore-analytical-storage "") 和 [SQL支持函数](https://help.aliyun.com/zh/tablestore/sql-function-in-iotstore-analytical-storage "")。

2. 单击 **执行SQL(F8)**。

      符合条件的数据会显示在 **执行结果** 区域。查询结果支持以列表、折线图和直方图形式展示。

### **查询分析存储描述信息**

1. 在 **实例管理** 页面的 **实例详情** 页签，单击 **时序表列表** 页签。

2. 在 **时序表列表** 页签，单击时序表名。

3. 在 **基本详情** 页签的 **分析存储** 区域，您可以查看分析存储名称、生命周期、同步方式、同步状态、存储大小、同步时间等。


### **更新分析存储数据生命周期**

1. 在 **实例管理** 页面的 **实例详情** 页签，单击 **时序表列表** 页签。

2. 在 **时序表列表** 页签，单击时序表名。

3. 在 **基本详情** 页签的 **分析存储** 区域，单击分析存储 **操作** 列的 **编辑** **。**

4. 在 **更新分析存储** 对话框，修改分析存储生命周期。

5. 单击 **确定**。


### **删除分析存储**

1. 在 **实例管理** 页面的 **实例详情** 页签，单击 **时序表列表** 页签。

2. 在 **时序表列表** 页签，单击时序表名。

3. 在 **基本详情** 页签的 **分析存储** 区域，单击分析存储 **操作** 列的 **删除** **。**

4. 在弹出的对话框中，配置 **删除分析存储SQL映射表** 项，单击 **确定**。

   - 如果未创建 **使用分析存储查询** 的SQL映射表， **删除分析存储SQL映射表** 开关保持默认配置即可。

   - 如果已创建 **使用分析存储查询** 的SQL映射表，请确保打开 **删除分析存储SQL映射表** 开关。在删除分析存储时，系统自动级联删除相应的SQL映射表。

## **开发集成**

| **功能** | **调用方式** |
| --- | --- |

|     |     |
| --- | --- |
| **功能** | **调用方式** |
| 创建分析存储 | SDK： [Java](https://help.aliyun.com/zh/tablestore/developer-reference/create-analyticalstore-by-using-java-sdk "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/create-analyticalstore-by-using-go-sdk "") |
| SQL查询分析 | SDK： [Java](https://help.aliyun.com/zh/tablestore/sql-query-6 "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/sql-query-by-go-sdk/ "")、 [Python](https://help.aliyun.com/zh/tablestore/developer-reference/sql-query-by-python-sdk/ "")、 [Node.js](https://help.aliyun.com/zh/tablestore/developer-reference/sql-query-by-nodejs-sdk/ "")、 [.NET](https://help.aliyun.com/zh/tablestore/developer-reference/sql-query-by-dotnet-sdk/ "")、 [PHP](https://help.aliyun.com/zh/tablestore/developer-reference/sql-query-by-php-sdk/ "") |
| 更新分析存储数据生命周期 | SDK： [Java](https://help.aliyun.com/zh/tablestore/developer-reference/update-analyticalstore-configuration-information-of-tablestore "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/update-configuration-information-for-the-analyticalstore-by-using-go-sdk "") |
| 查询分析存储描述信息 | SDK： [Java](https://help.aliyun.com/zh/tablestore/developer-reference/analytical-storage-description-information-by-using-java-sdk "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/analytical-storage-description-information-by-using-go-sdk "") |
| 删除分析存储 | SDK： [Java](https://help.aliyun.com/zh/tablestore/developer-reference/delete-analytical-store-by-using-java-sdk "")、 [Go](https://help.aliyun.com/zh/tablestore/developer-reference/delete-analytical-store-by-using-go-sdk "") |

## **计费说明**

分析存储的计费项包括数据存储、按量写吞吐量和按量读吞吐量。更多信息，请参见 [时序模型计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-the-timeseries-model-1 "")。