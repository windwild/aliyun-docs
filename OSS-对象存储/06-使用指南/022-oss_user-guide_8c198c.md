### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据湖](https://help.aliyun.com/zh/oss/user-guide/oss-data-lake/)[数据湖生态接入](https://help.aliyun.com/zh/oss/user-guide/connect-oss-to-data-lake-ecosystems/)[开源生态](https://help.aliyun.com/zh/oss/user-guide/open-source-ecosystem/)[通过OSS SDK接入开源生态](https://help.aliyun.com/zh/oss/user-guide/use-oss-sdks-to-connect-to-the-open-source-ecosystem/)Apache Impala（CDH6）查询OSS数据

# Apache Impala（CDH6）查询OSS数据

更新时间：2024-02-23 04:04:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Spark使用OSS Select加速数据查询](https://help.aliyun.com/zh/oss/user-guide/spark-uses-oss-select-to-speed-up-data-queries)[下一篇：通过HDP 2.6 Hadoop读取和写入OSS数据](https://help.aliyun.com/zh/oss/user-guide/use-hdp-2-6-based-hadoop-to-read-and-write-oss-data)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

步骤一：增加OSS配置

步骤二：配置Apache Impala

步骤三：验证配置

相关文档

CDH是Cloudera提供的包含Apache Hadoop核心组件的企业级大数据发行版，已支持Hadoop 3.0.0。本文将详解如何配置CDH6环境下的Hadoop、Hive、Spark、Impala等组件，以实现对接阿里云OSS存储服务进行数据查询操作。

## 前提条件

已搭建CDH6 集群。具体操作，请参见 [安装指南](https://www.cloudera.com/documentation/enterprise/6/6.0/topics/installation.html)。本文以CDH6.0.1版本为例。

## 步骤一：增加OSS配置

1. 通过集群管理工具CM来增加配置。



若没有CM管理的集群，可以修改core-site.xml。以CM为例，需要增加如下配置：![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6454449951/p33147.png)






| **配置项** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **配置项** | **说明** |
| **fs.oss.endpoint** | 填写需要连接的OSS的Endpoint，示例值为oss-cn-zhangjiakou-internal.aliyuncs.com。 |
| **fs.oss.accessKeyId** | 填写访问密钥中的AccessKeyId，访问密钥要求拥有访问OSS的权限。 |
| **fs.oss.accessKeySecret** | 填写访问密钥中的AccessKeySecret，访问密钥要求拥有访问OSS的权限。 |
| **fs.oss.impl** | Hadoop OSS文件系统实现类。固定值为`org.apache.hadoop.fs.aliyun.oss.AliyunOSSFileSystem`。 |
| **fs.oss.buffer.dir** | 填写临时文件目录。 建议值为`/tmp/oss`。 |
| **fs.oss.connection.secure.enabled** | 是否开启 HTTPS。开启HTTPS可能会影响性能。 建议值为`false`。 |
| **fs.oss.connection.maximum** | 与OSS的连接数。建议值为`2048`。 |





更多参数解释，请参见 [Hadoop-Aliyun module](https://github.com/apache/hadoop/blob/trunk/hadoop-tools/hadoop-aliyun/src/site/markdown/tools/hadoop-aliyun/index.md)。

2. 根据CM提示重启集群。

3. 测试读写OSS。



   - 测试读：















     ```shell
     hadoop fs -ls oss://${your-bucket-name}/
     ```

   - 测试写：















     ```shell
     hadoop fs -mkdir oss://${your-bucket-name}/hadoop-test
     ```



     若测试可以读写OSS，则配置成功。若无法读写OSS，请检查配置。



     **说明**





     本文中所有 ${} 的内容为环境变量，请根据您实际的环境修改。


## 步骤二：配置Apache Impala

为了使CDH6版本中的Impala能够支持OSS，您需要手动将OSS的相关JAR包添加到所有Impala节点的CLASSPATH环境变量中。具体操作步骤如下：

1. 进入${CDH\_HOME}/lib/impala目录，创建符号链接：

















```shell
[root@cdh-master impala]# cd lib/
[root@cdh-master lib]# ln -s ../../../jars/hadoop-aliyun-3.0.0-cdh6.0.1.jar hadoop-aliyun.jar
[root@cdh-master lib]# ln -s ../../../jars/aliyun-sdk-oss-2.8.3.jar aliyun-sdk-oss-2.8.3.jar
[root@cdh-master lib]# ln -s ../../../jars/jdom-1.1.jar jdom-1.1.jar
```

2. 进入${CDH\_HOME}/bin目录，修改impalad、statestored、catalogd三个文件，在文件最后一行exec命令前增加如下内容：

















```shell
export CLASSPATH=${CLASSPATH}:${IMPALA_HOME}/lib/hadoop-aliyun.jar:${IMPALA_HOME}/lib/aliyun-sdk-oss-2.8.3.jar:${IMPALA_HOME}/lib/jdom-1.1.jar
```

3. 重启所有节点的Impala相关进程。


## 步骤三：验证配置

尝试使用Apache Impala查询OSS，并且运行TPC-DS的查询语句。更多信息，请参见 [Apache Impala介绍](http://impala.apache.org/) 和 [TPC-DS查询](https://github.com/hortonworks/hive-testbench/tree/hive14)。

**说明**

TPC-DS设计了一系列基于Hive QL的复杂查询场景。考虑到Impala SQL与Hive QL之间具有较高的兼容性，大部分TPC-DS查询可以直接在Impala上执行。然而，由于两者间仍存在一些细微差异，部分TPC-DS查询可能因兼容性问题无法直接在Impala环境中运行。

以下以选取大量能在Impala中顺利执行的TPC-DS查询作为实验案例，通过这些案例来观察并分析Impala在大规模数据处理上的性能表现。

1. 生成sample数据到OSS。

















```shell
[root@cdh-master ~]# git clone https://github.com/hortonworks/hive-testbench.git
[root@cdh-master ~]# cd hive-testbench
[root@cdh-master hive-testbench]# git checkout hive14
[root@cdh-master hive-testbench]# ./tpcds-build.sh
[root@cdh-master hive-testbench]# FORMAT=textfile ./tpcds-setup.sh 50 oss://{your-bucket-name}/
```

2. 建表。



Benchmark的建表语句与Apache Impala的建表语句兼容。您只需要复制ddl-tpcds/text/alltables.sql中的建表语句，然后修改${LOCATION}即可。

















```plaintext
[root@cdh-master hive-testbench]# impala-shell -i cdh-slave01 -d default
Starting Impala Shell without Kerberos authentication
Connected to cdh-slave01:21000
Server version: impalad version 3.0.0-cdh6.0.1 RELEASE(build9a74a5053de5f7b8dd983802e6d75e58d31472db)
***********************************************************************************
Welcome to the Impala shell.
(Impala Shell v3.0.0-cdh6.0.1(9a74a50) built on Wed Sep 1911:27:37 PDT 2018)

Want to know what version of Impala you're connected to? Run the VERSION command to
find out!
***********************************************************************************
Query: use `default`
[cdh-slave01:21000] default> create external table call_center(
                              >       cc_call_center_sk         bigint
                              > ,     cc_call_center_id         string
                              > ,     cc_rec_start_date        string
                              > ,     cc_rec_end_date          string
                              > ,     cc_closed_date_sk         bigint
                              > ,     cc_open_date_sk           bigint
                              > ,     cc_name                   string
                              > ,     cc_class                  string
                              > ,     cc_employees              int
                              > ,     cc_sq_ft                  int
                              > ,     cc_hours                  string
                              > ,     cc_manager                string
                              > ,     cc_mkt_id                 int
                              > ,     cc_mkt_class              string
                              > ,     cc_mkt_desc               string
                              > ,     cc_market_manager         string
                              > ,     cc_division               int
                              > ,     cc_division_name          string
                              > ,     cc_company                int
                              > ,     cc_company_name           string
                              > ,     cc_street_number          string
                              > ,     cc_street_name            string
                              > ,     cc_street_type            string
                              > ,     cc_suite_number           string
                              > ,     cc_city                   string
                              > ,     cc_county                 string
                              > ,     cc_state                  string
                              > ,     cc_zip                    string
                              > ,     cc_country                string
                              > ,     cc_gmt_offset             double
                              > ,     cc_tax_percentage         double
                              > )
                              > row format delimited fields terminated by '|'
                              > location 'oss://{your-bucket-name}/50/call_center';
Query: create external table call_center(
         cc_call_center_sk         bigint
,     cc_call_center_id         string
,     cc_rec_start_date        string
,     cc_rec_end_date          string
,     cc_closed_date_sk         bigint
,     cc_open_date_sk           bigint
,     cc_name                   string
,     cc_class                  string
,     cc_employees              int
,     cc_sq_ft                  int
,     cc_hours                  string
,     cc_manager                string
,     cc_mkt_id                 int
,     cc_mkt_class              string
,     cc_mkt_desc               string
,     cc_market_manager         string
,     cc_division               int
,     cc_division_name          string
,     cc_company                int
,     cc_company_name           string
,     cc_street_number          string
,     cc_street_name            string
,     cc_street_type            string
,     cc_suite_number           string
,     cc_city                   string
,     cc_county                 string
,     cc_state                  string
,     cc_zip                    string
,     cc_country                string
,     cc_gmt_offset             double
,     cc_tax_percentage         double
)
row format delimited fields terminated by '|'
location 'oss://{your-bucket-name}/50/call_center'
+-------------------------+
| summary                 |
+-------------------------+
| Table has been created. |
+-------------------------+
Fetched 1 row(s) in 4.10s
```

3. 检查建表内容。















```shell
[cdh-slave01:21000] default> show tables;
Query: show tables
+------------------------+
| name                   |
+------------------------+
| call_center            |
| catalog_page           |
| catalog_returns        |
| catalog_sales          |
| customer               |
| customer_address       |
| customer_demographics  |
| date_dim               |
| household_demographics |
| income_band            |
| inventory              |
| item                   |
| promotion              |
| reason                 |
| ship_mode              |
| store                  |
| store_returns          |
| store_sales            |
| time_dim               |
| warehouse              |
| web_page               |
| web_returns            |
| web_sales              |
| web_site               |
+------------------------+
Fetched 24 row(s) in 0.03s
```

4. 在Impala上执行TPC-DS查询，已经可以正常查询OSS的数据。


1. 进入待查询的SQL所在的 sample-queries-tpcds目录。















      ```shell
      [root@cdh-master hive-testbench]# ls sample-queries-tpcds
      query12.sql  query20.sql  query27.sql  query39.sql  query46.sql  query54.sql  query64.sql  query71.sql  query7.sql   query87.sql  query93.sql  README.md
      query13.sql  query21.sql  query28.sql  query3.sql   query48.sql  query55.sql  query65.sql  query72.sql  query80.sql  query88.sql  query94.sql  testbench.settings
      query15.sql  query22.sql  query29.sql  query40.sql  query49.sql  query56.sql  query66.sql  query73.sql  query82.sql  query89.sql  query95.sql  testbench-withATS.settings
      query17.sql  query24.sql  query31.sql  query42.sql  query50.sql  query58.sql  query67.sql  query75.sql  query83.sql  query90.sql  query96.sql
      query18.sql  query25.sql  query32.sql  query43.sql  query51.sql  query60.sql  query68.sql  query76.sql  query84.sql  query91.sql  query97.sql
      query19.sql  query26.sql  query34.sql  query45.sql  query52.sql  query63.sql  query70.sql  query79.sql  query85.sql  query92.sql  query98.sql
      ```

2. 执行TPC-DS查询 query13.sql。















      ```shell
      [root@cdh-master hive-testbench]# impala-shell -i cdh-slave01 -d default -f sample-queries-tpcds/query13.sql
      Starting Impala Shell without Kerberos authentication
      Connected to cdh-slave01:21000
      Server version: impalad version 3.0.0-cdh6.0.1 RELEASE(build9a74a5053de5f7b8dd983802e6d75e58d31472db)
      Query: use`default`Query: selectavg(ss_quantity)
             ,avg(ss_ext_sales_price)
             ,avg(ss_ext_wholesale_cost)
             ,sum(ss_ext_wholesale_cost)
       from store_sales
           ,store
           ,customer_demographics
           ,household_demographics
           ,customer_address
           ,date_dim
       where store.s_store_sk = store_sales.ss_store_sk
       and  store_sales.ss_sold_date_sk = date_dim.d_date_sk and date_dim.d_year = 2001and((store_sales.ss_hdemo_sk=household_demographics.hd_demo_sk
        and customer_demographics.cd_demo_sk = store_sales.ss_cdemo_sk
        and customer_demographics.cd_marital_status = 'M'and customer_demographics.cd_education_status = '4 yr Degree'and store_sales.ss_sales_price between100.00and150.00and household_demographics.hd_dep_count = 3
           )or
          (store_sales.ss_hdemo_sk=household_demographics.hd_demo_sk
        and customer_demographics.cd_demo_sk = store_sales.ss_cdemo_sk
        and customer_demographics.cd_marital_status = 'D'and customer_demographics.cd_education_status = 'Primary'and store_sales.ss_sales_price between50.00and100.00and household_demographics.hd_dep_count = 1
           ) or
          (store_sales.ss_hdemo_sk=household_demographics.hd_demo_sk
        and customer_demographics.cd_demo_sk = ss_cdemo_sk
        and customer_demographics.cd_marital_status = 'U'and customer_demographics.cd_education_status = 'Advanced Degree'and store_sales.ss_sales_price between150.00and200.00and household_demographics.hd_dep_count = 1
           ))
       and((store_sales.ss_addr_sk = customer_address.ca_address_sk
        and customer_address.ca_country = 'United States'and customer_address.ca_state in('KY', 'GA', 'NM')
        and store_sales.ss_net_profit between100and200
           ) or
          (store_sales.ss_addr_sk = customer_address.ca_address_sk
        and customer_address.ca_country = 'United States'and customer_address.ca_state in('MT', 'OR', 'IN')
        and store_sales.ss_net_profit between150and300
           ) or
          (store_sales.ss_addr_sk = customer_address.ca_address_sk
        and customer_address.ca_country = 'United States'and customer_address.ca_state in('WI', 'MO', 'WV')
        and store_sales.ss_net_profit between50and250
           ))
      Query submitted at: 2018-10-3011:44:47(Coordinator: http://cdh-slave01:25000)
      Query progress can be monitored at: http://cdh-slave01:25000/query_plan?query_id=ff4b3157eddfc3c4:8a31c6500000000
      +-------------------+-------------------------+----------------------------+----------------------------+
      | avg(ss_quantity)  | avg(ss_ext_sales_price) | avg(ss_ext_wholesale_cost) | sum(ss_ext_wholesale_cost) |
      +-------------------+-------------------------+----------------------------+----------------------------+
      | 30.87106918238994 | 2352.642327044025       | 2162.600911949685          | 687707.09                  |
      +-------------------+-------------------------+----------------------------+----------------------------+
      Fetched 1 row(s) in 353.16s
      ```


本次查询涉及到6张表：store、store\_sales、customer\_demographics、household\_demographics、customer\_address、date\_dim。

```shell
[cdh-slave01:21000] default> showtable STATS store;
Query: showtable STATS store
+-------+--------+---------+--------------+-------------------+--------+-------------------+-------------------------------------------+
| #Rows | #Files | Size    | Bytes Cached | CacheReplication | Format | Incremental stats | Location                                  |
+-------+--------+---------+--------------+-------------------+--------+-------------------+-------------------------------------------+
| -1    | 1      | 37.56KB | NOT CACHED   | NOT CACHED        | TEXT   | false             | oss://{your-bucket-name}/50/store |
+-------+--------+---------+--------------+-------------------+--------+-------------------+-------------------------------------------+
Fetched 1 row(s) in 0.01s
[cdh-slave01:21000] default> showtable STATS store_sales;
Query: showtable STATS store_sales
+-------+--------+---------+--------------+-------------------+--------+-------------------+-------------------------------------------------+
| #Rows | #Files | Size    | Bytes Cached | CacheReplication | Format | Incremental stats | Location                                        |
+-------+--------+---------+--------------+-------------------+--------+-------------------+-------------------------------------------------+
| -1    | 50     | 18.75GB | NOT CACHED   | NOT CACHED        | TEXT   | false             | oss://{your-bucket-name}/50/store_sales |
+-------+--------+---------+--------------+-------------------+--------+-------------------+-------------------------------------------------+
Fetched 1 row(s) in 0.01s
[cdh-slave01:21000] default> showtable STATS customer_demographics;
Query: showtable STATS customer_demographics
+-------+--------+---------+--------------+-------------------+--------+-------------------+-----------------------------------------------------------+
| #Rows | #Files | Size    | Bytes Cached | CacheReplication | Format | Incremental stats | Location                                                  |
+-------+--------+---------+--------------+-------------------+--------+-------------------+-----------------------------------------------------------+
| -1    | 50     | 76.92MB | NOT CACHED   | NOT CACHED        | TEXT   | false             | oss://{your-bucket-name}/50/customer_demographics |
+-------+--------+---------+--------------+-------------------+--------+-------------------+-----------------------------------------------------------+
Fetched 1 row(s) in 0.01s
[cdh-slave01:21000] default> showtable STATS household_demographics;
Query: showtable STATS household_demographics
+-------+--------+----------+--------------+-------------------+--------+-------------------+------------------------------------------------------------+
| #Rows | #Files | Size     | Bytes Cached | CacheReplication | Format | Incremental stats | Location                                                   |
+-------+--------+----------+--------------+-------------------+--------+-------------------+------------------------------------------------------------+
| -1    | 1      | 148.10KB | NOT CACHED   | NOT CACHED        | TEXT   | false             | oss://{your-bucket-name}/50/household_demographics |
+-------+--------+----------+--------------+-------------------+--------+-------------------+------------------------------------------------------------+
Fetched 1 row(s) in 0.01s
[cdh-slave01:21000] default> showtable STATS customer_address;
Query: showtable STATS customer_address
+-------+--------+---------+--------------+-------------------+--------+-------------------+------------------------------------------------------+
| #Rows | #Files | Size    | Bytes Cached | CacheReplication | Format | Incremental stats | Location                                             |
+-------+--------+---------+--------------+-------------------+--------+-------------------+------------------------------------------------------+
| -1    | 1      | 40.54MB | NOT CACHED   | NOT CACHED        | TEXT   | false             | oss://{your-bucket-name}/50/customer_address |
+-------+--------+---------+--------------+-------------------+--------+-------------------+------------------------------------------------------+
Fetched 1 row(s) in 0.01s
[cdh-slave01:21000] default> showtable STATS date_dim;
Query: showtable STATS date_dim
+-------+--------+--------+--------------+-------------------+--------+-------------------+----------------------------------------------+
| #Rows | #Files | Size   | Bytes Cached | CacheReplication | Format | Incremental stats | Location                                     |
+-------+--------+--------+--------------+-------------------+--------+-------------------+----------------------------------------------+
| -1    | 1      | 9.84MB | NOT CACHED   | NOT CACHED        | TEXT   | false             | oss://{your-bucket-name}/50/date_dim |
+-------+--------+--------+--------------+-------------------+--------+-------------------+----------------------------------------------+
Fetched 1 row(s) in 0.01s
```

## 相关文档

- [Hadoop支持集成OSS](https://yq.aliyun.com/articles/292792?spm=a2c4e.11155435.0.0.7ccba82fbDwfhK)

- [Hadoop](https://github.com/apache/hadoop/blob/trunk/hadoop-tools/hadoop-aliyun/src/site/markdown/tools/hadoop-aliyun/index.md)

- [通过CDH5 Hadoop读写OSS](https://help.aliyun.com/zh/oss/user-guide/a53b05#concept-ixz-d1w-wfb "")

- [通过HDP2.6 Hadoop读写OSS](https://help.aliyun.com/zh/oss/user-guide/use-hdp-2-6-based-hadoop-to-read-and-write-oss-data#concept-xdd-lcr-wfb "")

- [EMR集群接入OSS-HDFS服务快速入门](https://help.aliyun.com/zh/oss/user-guide/connect-emr-clusters-to-oss-hdfs "")