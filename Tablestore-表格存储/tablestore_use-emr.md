### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[数据湖投递](https://help.aliyun.com/zh/tablestore/data-lake-delivery-introductions/)[数据湖计算分析](https://help.aliyun.com/zh/tablestore/data-lake-based-computing-and-analysis/)使用EMR

# 使用EMR

更新时间：2024-12-31 05:25:54

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：通过SDK投递数据到OSS](https://help.aliyun.com/zh/tablestore/use-sdks-of-data-delivery)[下一篇：监控与报警](https://help.aliyun.com/zh/tablestore/overview-of-monitor-and-alarm/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

前提条件

操作步骤

使用EMR的JindoFS缓存模式连接OSS数据湖。

## 背景信息

您可以使用EMR的JindoFS缓存模式或者JindoFS块模式连接OSS数据湖。

- 缓存模式（Cache）主要兼容原生OSS存储方式，文件以对象的形式存储在OSS上，每个文件根据实际访问情况会在本地进行缓存，提升EMR集群内访问OSS的效率，同时兼容了OSS原有文件形式，数据访问上能够与其他OSS客户端完全兼容。详情请参见 [JindoFS缓存模式使用说明](https://help.aliyun.com/zh/emr/emr-on-ecs/user-guide/use-jindofs-in-cache-mode-7#task-1946324 "")。

- 块存储模式（Block）提供了最为高效的数据读写能力和元数据访问能力。数据以Block形式存储在后端存储OSS上，本地提供缓存加速，元数据则由本地Namespace服务维护，提供高效的元数据访问性能。详情请参见 [JindoFS块存储模式使用说明](https://help.aliyun.com/zh/emr/emr-on-ecs/user-guide/use-jindofs-in-block-storage-mode-7#task-1946284 "")。


## 前提条件

- 已创建EMR集群，详情请参见 [创建集群](https://help.aliyun.com/zh/emr/emr-on-ecs/getting-started/quick-start-for-emr#section-55q-jmm-3ts "")。

创建集群时，请注意如下事项：

  - 创建EMR集群和OSS属于同一个阿里云账号，且建议EMR集群和OSS Bucket处于同一地域。

  - 创建集群时，请打开 **挂载公网** 和 **远程登录** 开关，将集群挂载到公网，用于Shell远程登录服务器。

  - bigboot与smartdata为后续配置相关服务，如果默认未选中，请选中bigboot与smartdata服务。
- 已创建数据投递任务，详情请参见 [快速入门](https://help.aliyun.com/zh/tablestore/deliver-data-to-oss-by-tablestore-console#topic-2636550 "")。


## 操作步骤

1. 使用EMR的jindoFS缓存模式连接OSS和启用缓存，详情请参见 [JindoFS缓存模式使用说明](https://help.aliyun.com/zh/emr/emr-on-ecs/user-guide/use-jindofs-in-cache-mode-7#task-1946324 "")。

启用缓存会利用本地磁盘对访问的热数据块进行缓存，默认状态为禁用，即所有OSS读取都直接访问OSS上的数据。缓存启用后，Jindo服务会自动管理本地缓存备份，通过水位清理本地缓存，请根据需求配置一定的比例用于缓存。

2. 启动spark SQL。

1. 通过远程登录工具（例如PuTTY）登录EMR Header服务器。

2. 执行如下命令运行Spark SQL。















      ```shell
      spark-sql --master yarn --num-executors 5 --executor-memory 1g --executor-cores 2
      ```
3. 使用SQL语句创建指向OSS数据目录的外表。

请使用通过表格存储控制台获取的SQL语句，如下SQL语句示例仅供参考。















```sql
CREATE EXTERNAL TABLE  lineitem (l_orderkey bigint,l_linenumber bigint,l_receiptdate string,l_returnflag string,l_tax double,l_shipmode string,l_suppkey bigint,l_shipdate string,l_commitdate string,l_partkey bigint,l_quantity double,l_comment string,l_linestatus string,l_extendedprice double,l_discount double,l_shipinstruct string) PARTITIONED BY (`year` int, `month` int) STORED AS PARQUET  LOCATION  'jfs://test/' ;
```



![fig001](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4001190061/p169744.png)

通过表格存储控制台获取SQL语句的方法如下：

在实例的 **数据湖投递** 页面，单击投递任务 **操作** 列的 **建表语句**，可以查看和复制SQL语句，如下图所示。

![pic002](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4001190061/p169745.png)

4. 执行如下SQL语句，加载OSS数据源中实际的数据分区。

其中lineitem为创建的外表名称。















```sql
msck repair table lineitem;
```



![load](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4001190061/p169641.png)

5. 查询数据。















```sql
select * from lineitem limit 1;
```



![pic003](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4001190061/p169746.png)