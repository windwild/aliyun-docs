### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[资源管理](https://help.aliyun.com/zh/sls/resource-management/)管理Shard

# 管理Shard

更新时间：2025-10-16 01:46:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：管理EventStore](https://help.aliyun.com/zh/sls/manage-an-eventstore)[下一篇：资源流控及解决方案](https://help.aliyun.com/zh/sls/expansion-of-resources)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

基本概念

Shard范围

Shard的读写能力

Shard状态

分裂与合并

分裂Shard

控制台操作

命令行操作

查看Shard

控制台操作

自动分裂Shard

合并Shard

删除Shard

Shard接口

日志服务使用Shard控制Logstore、EventStore、MetricStore的读写数据的能力，数据必定保存在某一个Shard中。通过分裂、合并操作控制活跃的Shard数量来调整日志服务提供的最大读写能力。分裂Shard可以自动触发，但合并Shard必须手动执行。

## 基本概念

### **Shard范围**

每个Shard均有范围，为MD5左闭右开区间\[BeginKey,EndKey)。每个Shard范围不会相互覆盖，且属于整个MD5范围内\[00000000000000000000000000000000,ffffffffffffffffffffffffffffffff）。在创建Logstore或MetricStore时指定Shard个数，日志服务将自动平均划分整个MD5范围。\
\
- BeginKey：指定Shard范围的起始值，Shard范围中包含该值。\
\
- EndKey：指定Shard范围的结束值，Shard范围中不包含该值。\
\
\
例如Logstore A中包含4个Shard，各个Shard范围如下：\
\
表 1\. Shard范围\
\
|     |     |\
| --- | --- |\
| **Shard ID** | **范围** |\
| Shard0 | \[00000000000000000000000000000000,40000000000000000000000000000000) |\
| Shard1 | \[40000000000000000000000000000000,80000000000000000000000000000000) |\
| Shard2 | \[80000000000000000000000000000000,c0000000000000000000000000000000) |\
| Shard3 | \[c0000000000000000000000000000000,ffffffffffffffffffffffffffffffff) |\
\
在Shard读写数据过程中，读数据时必须指定Shard ID，写数据时可通过负载均衡模式或者指定Hash Key的模式。\
\
- 负载均衡模式：每个数据包随机写入当前可用的Shard中。\
\
如果写入流量大于单Shard的服务能力，建议采用负载均衡模式。\
\
- 指定Hash Key模式：指定MD5的Key值，数据将被写入包含该Key值的Shard中。\
\
例如 [Shard范围](https://help.aliyun.com/zh/sls/shard#table-nff-jx8-wjo "") 所示，当写入数据时指定MD5的Key值为5F时，则数据将被写入包含5F的Shard1上；当写入数据时指定MD5的Key值为8C时，则数据将被写入包含8C的Shard2上。\
\
\
### **Shard的读写能力**\
\
每个Shard提供一定的服务能力，具体请参见 [数据读写](https://help.aliyun.com/zh/sls/data-read-and-write "")。\
\
根据实际数据流量规划Shard个数。当数据流量超出读写能力时，及时分裂Shard以增加Shard个数，从而达到更大的读写能力。当数据流量远未达到Shard的最大读写能力时，及时合并Shard以减少Shard个数，从而降低活跃Shard租用费用。\
\
**重要**\
\
- 当写入数据的API持续报告403或者500错误时，通过Logstore云监控查看流量和状态码判断是否需要增加Shard。\
\
- 超过Shard服务能力的读写，日志服务会尽可能服务，但不保证服务质量。\
\
\
### **Shard状态**\
\
Shard状态包括readwrite（读写）和readonly（只读）。\
\
创建Shard时，所有Shard状态均为readwrite状态。执行分裂或合并操作后，Shard状态变更为readonly，并生成新的readwrite状态的Shard。Shard状态不影响其数据读取的性能。readwrite状态的Shard可保证数据写入性能，readonly状态的Shard不提供数据写入服务。\
\
### **分裂与合并**\
\
日志服务支持分裂和合并Shard。\
\
- 分裂操作是指将一个Shard分裂为另外两个Shard，即分裂后Shard数量增加2。两个新生成的Shard的状态为readwrite，排列在原Shard之后且两个Shard的MD5范围覆盖原Shard的MD5范围。\
\
分裂Shard时，需指定一个处于readwrite状态的Shard。分裂完成后，原Shard状态由readwrite变为readonly，该Shard中的数据仍可被消费，但该Shard不支持写入新数据。\
\
- 合并操作是指将两个Shard合并为一个Shard。新生成的Shard的状态为readwrite，排列在原Shard之后且其MD5范围覆盖原来两个Shard的MD5范围。\
\
合并Shard时，需指定一个处于readwrite状态且未排列在最后一个的Shard，日志服务自动找到所指定Shard右侧相邻的Shard，并进行合并。合并完成后，原来两个Shard的状态由readwrite变为readonly，这两个Shard中的数据仍可被消费，但这两个Shard不支持写入新数据。\
\
\
## 分裂Shard\
\
建议您根据实际业务数据流量规划Shard个数。每个Shard支持5MB/s或500次/s的数据写入、10MB/s或100次/s的数据读取。此限制非硬性限制，超出限制时，系统会尽可能提供服务，但是不保证服务质量。当数据读写流量超出Shard读写能力时，需要及时分裂Shard以增加Shard个数，从而提供更高的读写能力。\
\
**说明**\
\
当写入数据的API持续报告403或者500错误时，您可以通过Logstore云监控查看流量和状态码判断是否需要增加Shard。\
\
### **控制台操作**\
\
1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。\
\
2. 在Project列表区域，单击目标Project。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8797827471/p955209.png)\
\
3. 单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6586464571/p995244.png)日志存储，在日志库中，将鼠标悬浮在目标Logstore上，选择**![修改日志库](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0478559951/p52318.png)** \> **修改**。\
\
4. 在 **Logstore属性** 页面中，单击 **修改**。\
\
5. 选择待分裂的Shard，单击 **分裂**。\
\
\
\
\
\
**重要**\
\
\
\
\
\
分裂Shard时，需要选择一个处于readwrite状态的Shard。\
\
\
\
\
\
\
\
![分裂分区](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0167745951/p2594.png)\
\
6. 选择分裂数量，单击 **确定**。\
\
7. 单击 **保存**。\
\
\
### **命令行操作**\
\
您也可以通过日志服务命令行工具CLI一次性分裂Shard到指定数量。更多信息，请参见 [使用CLI配置Shard](https://aliyun-log-cli.readthedocs.io/en/latest/tutorials/tutorial_split_shard.html)。\
\
## **查看Shard**\
\
### 控制台操作\
\
1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。\
\
2. 在Project列表区域，单击目标Project。\
\
![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8797827471/p955209.png)\
\
3. 单击![image](<Base64-Image-Removed>)日志存储，在日志库中，将鼠标悬浮在目标Logstore上，选择**![修改日志库](<Base64-Image-Removed>)** \> **修改**。\
\
4. 在 **Logstore属性** 页面中，查看当前Logstore的Shard列表。\
\
![image](<Base64-Image-Removed>)\
\
\
## 自动分裂Shard\
\
日志服务支持自动分裂Shard，帮助您自动处理业务流量超出预估值的场景。自动分裂Shard需要满足以下几个条件。\
\
- 开启了 **自动分裂Shard** 开关。\
\
- 当写入数据量超出当前Shard的 [写入服务能力](https://help.aliyun.com/zh/sls/data-read-and-write#concept-afx-g3h-hfb "") 且持续5分钟以上。\
\
- Logstore中readwrite状态的Shard数目未超过设定的最大Shard总数。\
\
\
**说明**\
\
最近15分钟内分裂出来的新Shard不会自动分裂。\
\
您可以在创建或修改Logstore时开启自动分裂Shard，并设定Shard的最大分裂数。\
\
- 自动分裂Shard\
\
例如原本存在4个Shard，日志服务会独立判断各个Shard是否满足分裂条件。满足分裂条件的Shard会各自进行分裂，分裂总数不会超过您所设定的最大分裂数。\
\
- 最大分裂数\
\
Shard自动分裂的最大总数目。开启自动分裂Shard功能后，最多支持自动分裂至256个readwrite状态的Shard。\
\
\
## 合并Shard\
\
当数据读写流量远达不到Shard的最大读写能力时，建议您合并Shard，降低活跃Shard租用费用。您可以通过合并操作减少Shard数量，日志服务会找到指定Shard右侧相邻的Shard，并将两个Shard合并。合并Shard只支持手动操作，无法自动合并。\
\
**重要**\
\
合并Shard时，必须指定一个处于readwrite状态的Shard，且不能是最后一个readwrite状态的Shard。\
\
1. 单击![image](<Base64-Image-Removed>)日志存储，在日志库中，将鼠标悬浮在目标Logstore上，选择**![修改日志库](<Base64-Image-Removed>)** \> **修改**。\
\
2. 在 **Logstore属性** 页面中，单击 **修改**。\
\
3. 选择待合并的Shard，单击 **合并**。\
\
\
\
![合并分区](<Base64-Image-Removed>)\
\
4. 单击 **保存**。\
\
\
\
合并完成后，所指定的Shard及其右侧相邻Shard的状态变成readonly。同时新生成一个readwrite状态的Shard，新Shard的MD5范围覆盖原来两个Shard的范围。\
\
\
## 删除Shard\
\
**警告**\
\
删除Shard后，无法恢复，请谨慎操作。\
\
- 自动删除\
\
如果您在创建Logstore时设置了数据保存时间，那么Shard及Shard中的数据超出保存时间后会被自动删除。\
\
- 手动删除\
\
如果您在创建Logstore时开启了永久保存，建议您通过删除Logstore的方式删除Logstore中的Shard和数据。更多信息，请参见 [停止计费/删除Logstore](https://help.aliyun.com/zh/sls/manage-a-logstore#section-ezq-vjx-ndb "")。\
\
\
## Shard接口\
\
| **操作** | **接口** |\
| --- | --- |\
\
|     |     |\
| --- | --- |\
| **操作** | **接口** |\
| 分裂Shard | [SplitShard](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-splitshard "") |\
| 合并Shard | [MergeShard](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-mergeshard "") |\
| 查询Shard | [ListShards](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-listshards "") |