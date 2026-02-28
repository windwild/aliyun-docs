### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[时序模型](https://help.aliyun.com/zh/tablestore/timeseries-model-introductions/)[物联网存储IoTstore](https://help.aliyun.com/zh/tablestore/iotstore-introduction/)[时序数据接入](https://help.aliyun.com/zh/tablestore/import-time-series-data/)Kafka数据接入

# Kafka数据接入

更新时间：2025-02-06 22:31:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：时序数据接入](https://help.aliyun.com/zh/tablestore/import-time-series-data/)[下一篇：EMQX数据接入](https://help.aliyun.com/zh/tablestore/import-emqx-data)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

注意事项

步骤一：创建目标服务资源

步骤二：创建Tablestore Sink Connector并启动

步骤三：测试Tablestore Sink Connector

通过创建Tablestore Sink Connector，将云消息队列 Kafka 版实例的数据源Topic导出到表格存储（Tablestore）。

## 背景信息

云消息队列 Kafka 版是阿里云提供的分布式、高吞吐、可扩展的消息队列。云消息队列 Kafka 版广泛用于日志收集、监控数据聚合、流式数据处理、在线和离线分析等大数据领域，已成为大数据生态中不可或缺的部分。更多信息，请参见 [什么是云消息队列 Kafka 版？](https://help.aliyun.com/zh/apsaramq-for-kafka/cloud-message-queue-for-kafka/product-overview/what-is-apsaramq-for-kafka-1#concept-1374972 "")。

**说明**

基于Tablestore Sink Connector，您也可以将Apache Kafka中的数据批量导入到表格存储的数据表或者时序表中。更多信息，请参见 [将Kafka数据同步到表格存储](https://help.aliyun.com/zh/tablestore/use-cases/synchronize-kafka-data-to-tablestore/#concept-2112567 "")。

## 前提条件

- 创建资源及授权策略，请参见 [创建前提](https://help.aliyun.com/zh/apsaramq-for-kafka/cloud-message-queue-for-kafka/user-guide/prerequisites#concept-2323967 "")。

- 创建Connector时生成的函数所在的服务角色需要手动添加`AliyunOTSFullAccess`权限策略，赋予此服务角色管理表格存储服务（OTS）的权限。具体操作， 请参见 [授予函数计算访问其他云服务的权限](https://help.aliyun.com/zh/functioncompute/fc-2-0/security-and-compliance/grant-function-compute-permissions-to-access-other-alibaba-cloud-services#section-1cx-1p6-zvp "")。


## **注意事项**

- 仅支持在同地域内，将数据从云消息队列 Kafka 版实例的数据源Topic导出至表格存储。Connector的限制说明，请参见 [使用限制](https://help.aliyun.com/zh/apsaramq-for-kafka/old-version-connector-overview#section-cgo-h01-5e3 "")。

- 创建Connector时，云消息队列 Kafka 版会为您自动创建服务关联角色。


  - 如果未创建服务关联角色，云消息队列 Kafka 版会为您自动创建一个服务关联角色，以便您使用云消息队列 Kafka 版导出数据至表格存储的功能。

  - 如果已创建服务关联角色，云消息队列 Kafka 版不会重复创建。


关于服务关联角色的更多信息，请参见 [服务关联角色](https://help.aliyun.com/zh/apsaramq-for-kafka/cloud-message-queue-for-kafka/security-and-compliance/service-linked-roles#task-1998690 "")。

- 目前仅支持将数据导出至表格存储的宽表模型，如有时序模型需求请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请。


## 步骤一：创建目标服务资源

1. 开通表格存储服务并创建实例。具体操作，请参见 [开通服务并创建实例](https://help.aliyun.com/zh/tablestore/product-overview/activate-service-and-create-a-instance "")。

2. 创建一个数据表，具体操作，请参见 [创建数据表](https://help.aliyun.com/zh/tablestore/product-overview/quick-start-of-widecolumn-model#section-tlv-x24-nfx "")。


本文以实例为ots-sink和数据表名为ots\_sink\_table的资源为例，创建数据表时设置pk1、pk2两个主键。![主键](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7741881861/p633865.png)

## 步骤二：创建Tablestore Sink Connector并启动

1. 登录 [云消息队列 Kafka 版控制台](https://kafka.console.aliyun.com/?spm=a2c4g.11186623.2.22.6bf72638IfKzDm)，在 **概览** 页面的 **资源分布** 区域，选择地域。

2. 在左侧导航栏，选择**Connector 生态集成** \> **任务列表**。

3. 在 **任务列表** 页面，单击 **创建任务**。

4. 在 **创建任务** 页面，设置 **任务名称** 和 **描述**，配置以下信息。


   - 任务创建


     1. 在 **Source（源）** 配置向导，选择 **数据提供方** 为 **消息队列 Kafka 版**，设置以下参数，然后单击 **下一步**。




        | **参数** | **说明** | **示例** |
        | --- | --- | --- |



        |     |     |     |
        | --- | --- | --- |
        | **参数** | **说明** | **示例** |
        | **地域** | 选择云消息队列 Kafka 版源实例所在的地域。 | 华北2（北京） |
        | **kafka 实例** | 选择生产云消息队列 Kafka 版消息的源实例。 | MQ\_INST\_115964845466\*\*\*\*\_ByBeUp3p |
        | **Topic** | 选择生产云消息队列 Kafka 版消息的Topic。 | topic |
        | **Group ID** | 选择源实例的消费组名称。<br>        - 快速创建。<br>          <br>          推荐方案，自动创建以 GID\_EVENTBRIDGE\_xxx 命名的 Group ID<br>          <br>        - 使用已有。<br>          <br>          请选择独立的 Group ID，不要和已有的业务混用，以免影响已有的消息收发 | 快速创建 |
        | **并发配额（消费者数）** | 选择源实例的消费者数。 | 1 |
        | **消费位点** | 选择开始消费消息的位点。 | 最新位点 |
        | **网络配置** | 选择路由消息的网络类型。 | 基础网络 |
        | **数据格式** | 数据格式是针对支持二进制传递的数据源端推出的指定内容格式的编码能力。<br>        - Json，Json 格式编码。<br>          <br>        - Text，默认文本格式编码。<br>          <br>        - Binary，二进制格式编码。<br>          <br>**说明**<br>支持多种数据格式编码，如无特殊编码诉求可将格式设置为 **Json**。 | Json |
        | **专有网络VPC** | 选择VPC ID。当 **网络配置** 设置为自建公网时需要设置此参数。 | vpc-bp17fapfdj0dwzjkd\*\*\*\* |
        | **交换机** | 选择vSwitch ID。当 **网络配置** 设置为自建公网时需要设置此参数。 | vsw-bp1gbjhj53hdjdkg\*\*\*\* |
        | **安全组** | 选择安全组。当 **网络配置** 设置为自建公网时需要设置此参数。 | alikafka\_pre-cn-7mz2\*\*\*\* |
        | **高级配置** | 批量推送可帮您批量聚合多个事件，当 **批量推送条数** 和 **批量推送间隔（单位：秒）** 两者条件达到其一时即会触发批量推送。<br>例如：您设置的推送条数为100 条，间隔时间为15 s，在10 s内消息条数已达到100条，那么该次推送则不会等15 s后再推送。 | 开启 |
        | **批量推送条数** | 调用函数发送的最大批量消息条数，当积压的消息数量到达设定值时才会发送请求，取值范围为 \[1,10000\]。 | 100 |
        | **批量推送间隔（单位：秒）** | 调用函数的间隔时间，系统每到间隔时间点会将消息聚合后发给函数计算，取值范围为\[0,15\]，单位为秒。0秒表示无等待时间，直接投递。 | 3 |

     2. 在 **Filtering（过滤）** 配置向导，设置数据 **模式内容** 过滤发送的请求。更多信息，请参见 [事件模式](https://help.aliyun.com/zh/apsaramq-for-kafka/cloud-message-queue-for-kafka/user-guide/message-filtering "")。

     3. 在 **Transform（转换）** 配置向导，设置数据清洗，实现分割、映射、富化及动态路由等繁杂数据加工能力。更多信息，请参见 [数据清洗](https://help.aliyun.com/zh/apsaramq-for-kafka/cloud-message-queue-for-kafka/user-guide/data-cleaning-1 "")。

     4. 在 **Sink（目标）** 配置向导，选择 **服务类型** 为 **表格存储TableStore**，配置以下参数。




        | **参数** | **说明** | **示例** |
        | --- | --- | --- |



        |     |     |     |
        | --- | --- | --- |
        | **参数** | **说明** | **示例** |
        | 实例名称 | 已创建的Tablestore实例名称。 | ost-sink |
        | 目标表 | 已创建的Tablestore数据表名称。 | ost\_sink\_table |
        | 表格存储模型 | 目前仅支持宽表模型，如有其他模型需求请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请。 | 宽表模型 |
        | 主键值 | Tablestore主键值生成方式，需定义每个主键内容的提取规则，提取规则通过JsonPath语法表达。 | 例如，主键名称为pk，数值提取规则配置为`$.data.value.pk` |
        | 属性列名称 | Tablestore数据表中属性列的名称。 | 无 |
        | 属性类型 | Tablestore数据表中属性列的类型。 | 无 |
        | 属性值 | 属性列值的生成方式，需定义每个属性列内容的提取规则，提取规则通过JsonPath语法表达。 | 例如，属性列名称为attr，数值提取规则配置为`$.data.value.attr` |
        | 存储格式 | 属性列值的存储格式。<br>        - 默认，内容转换为String类型后存储，<br>          <br>        - json，JSON中的每一个字段存储一列，列名为key\_{fieldName}。 | 默认 |
        | 写入模式 | 数据写入Tablestore的方式。<br>        - **put**：覆盖写入行。<br>          <br>        - **update**：更新写入行。 | put |
        | 网络配置 | - **专有网络**：通过专有网络VPC将Kafka消息投递到Tablestore。<br>          <br>        - **公网**：通过公网将Kafka消息投递到Tablestore。 | 公网 |
        | VPC | 选择VPC ID。仅当网络配置为 **专有网络** 时需配置此参数。 | vpc-bp17fapfdj0dwzjkd\*\*\*\* |
        | 交换机 | 选择vSwitch ID。仅当网络配置为 **专有网络** 时需配置此参数。 | vsw-bp1gbjhj53hdjdkg\*\*\*\* |
        | 安全组 | 选择安全组。仅当网络配置为 **专有网络** 时需配置此参数。 | test\_group |
        | 批量推送 | 批量推送可帮您批量聚合多个事件，当批量推送条数和批量推送间隔两个条件达到任意一个时即会触发批量推送。例如：您设置的推送条数为100条，间隔时间为15 s，在10 s内消息条数已达到100条，那么该次推送则不会等待15 s后再推送。<br>        - **开启**：开启批量推送功能。<br>          <br>        - **关闭**：关闭批量推送功能。默认每次仅投递给FC一条消息。 | 关闭 |
        | 批量推送条数 | 一次调用函数发送的最大批量消息条数，当积压的消息数量到达设定值时才会发送请求。取值范围为\[1,10000\]。仅当批量推送参数设置为 **开启** 时需要配置此参数。 | 100 |
        | 批量推送间隔 | 调用函数的间隔时间，系统每到间隔时间点会将消息聚合后发给函数计算。取值范围为\[0,15\]，单位：秒。取值为0表示没有等待时间，直接投递。仅当批量推送参数设置为 **开启** 时需要配置此参数。 | 10 |


   - 任务属性


     配置事件推送失败时的重试策略及错误发生时的处理方式。更多信息，请参见 [重试和死信](https://help.aliyun.com/zh/eventbridge/user-guide/retry-and-dead-letter "")。


5. 单击 **保存**，系统启动任务，并返回 **任务列表** 页面，



**说明**





启用任务后，会有30秒~60秒的延迟时间，您可以在 **任务列表** 页面的 **状态** 栏查看启动进度。


## 步骤三：测试Tablestore Sink Connector

1. 在 **任务列表** 页面，在任务的 **事件源** 列单击源Topic。

2. 在Topic详情页面，单击 **体验发送消息**。

3. 在 **快速体验消息收发** 面板，按照下图配置消息内容，然后单击 **确定**。



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6392083271/p831787.png)

4. 在 **任务列表** 页面，在Tablestore Sink Connector任务的 **事件目标** 列单击目标表名。

5. 在 **表管理** 页面，单击 **数据管理** 页签，然后单击 **查询数据**，设置 **查询范围**，单击 **确定**。



![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6392083271/p831788.png)