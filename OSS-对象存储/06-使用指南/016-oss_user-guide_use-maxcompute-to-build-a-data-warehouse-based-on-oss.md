### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据湖](https://help.aliyun.com/zh/oss/user-guide/oss-data-lake/)[数据湖生态接入](https://help.aliyun.com/zh/oss/user-guide/connect-oss-to-data-lake-ecosystems/)[阿里云生态](https://help.aliyun.com/zh/oss/user-guide/alibaba-cloud-ecosystem/)通过MaxCompute查询和分析OSS数据

# 通过MaxCompute查询和分析OSS数据

更新时间：2024-01-23 01:15:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Impala以EMR集群的方式查询OSS-HDFS服务中的数据](https://help.aliyun.com/zh/oss/user-guide/use-impala-on-an-emr-cluster-to-query-data-stored-in-oss-hdfs)[下一篇：使用OSS中的数据作为机器学习的训练样本](https://help.aliyun.com/zh/oss/user-guide/use-oss-data-as-training-sample-for-machine-learning)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

常见问题

报错：Accessing project '<projectname>' failed: ODPS-0420095: Access Denied - Authorization Failed \[4002\], You don't exist in project <projectname>.如何解决？

相关文档

部分应用可能每天都有大量的数据上传至OSS，这些数据可能涉及超大文本文件的结构化分析。您可以通过MaxCompute的外部表查询功能，将OSS存储的数据加载到MaxCompute进行分析。MaxCompute的数据查询和分析工作效率可提升至分钟级，帮助您更高效、更低成本地挖掘海量数据的价值。

## 前提条件

- 已创建OSS Bucket。具体操作，请参见 [创建Bucket](https://help.aliyun.com/zh/oss/user-guide/create-a-bucket-4#concept-ntj-wx1-5db "")。


- 已授权MaxCompute访问OSS。

您可以在登录阿里云账号后， [单击此处完成一键授权](https://ram.console.aliyun.com/role/authorization?request=%7B%22Services%22%3A%5B%7B%22Service%22%3A%22ODPS%22%2C%22Roles%22%3A%5B%7B%22RoleName%22%3A%22AliyunODPSDefaultRole%22%2C%22TemplateId%22%3A%22DefaultRole%22%7D%5D%7D%5D%2C%22ReturnUrl%22%3A%22https%3A%2F%2Fram.console.aliyun.com%2F%22%7D)。

- 已创建MaxCompute项目。具体操作，请参见 [创建MaxCompute项目](https://help.aliyun.com/zh/maxcompute/getting-started/create-a-maxcompute-project#task-zl2-mtx-5db "")。

- 已安装并配置MaxCompute客户端。具体操作，请参见 [安装并配置MaxCompute客户端](https://help.aliyun.com/zh/maxcompute/user-guide/maxcompute-client#section-vd2-4me-7uu "")。


## 操作步骤

1. 将物联网采集的数据上传到OSS。

1. 准备数据。

      本地创建vehicle.csv文件，文件包含的示例数据如下：















      ```shell
      1,1,51,1,46.81006,-92.08174,9/14/2014 0:00,S
      1,2,13,1,46.81006,-92.08174,9/14/2014 0:00,NE
      1,3,48,1,46.81006,-92.08174,9/14/2014 0:00,NE
      1,4,30,1,46.81006,-92.08174,9/14/2014 0:00,W
      1,5,47,1,46.81006,-92.08174,9/14/2014 0:00,S
      1,6,9,1,46.81006,-92.08174,9/14/2014 0:00,S
      1,7,53,1,46.81006,-92.08174,9/14/2014 0:00,N
      1,8,63,1,46.81006,-92.08174,9/14/2014 0:00,SW
      1,9,4,1,46.81006,-92.08174,9/14/2014 0:00,NE
      1,10,31,1,46.81006,-92.08174,9/14/2014 0:00,N
      ```

2. 将vehicle.csv文件上传至华东1（杭州）地域examplebucket的demo/目录下。具体操作，请参见 [上传文件](https://help.aliyun.com/zh/oss/upload-download-and-manage-objects-upload-objects#task-zx1-4p4-tdb "")。
2. 运行MaxCompute客户端。

具体操作，请参见 [运行MaxCompute客户端](https://help.aliyun.com/zh/maxcompute/user-guide/maxcompute-client#section-5ad-gj6-hku "")。

3. 通过MaxCompute创建外部表。具体操作，请参见 [创建表](https://help.aliyun.com/zh/maxcompute/getting-started/create-tables-1 "")。

创建非分区表data\_csv\_external，示例如下。















```shell
CREATE EXTERNAL TABLE IF NOT EXISTS data_csv_external
(
       vehicleId int,
       recordId int,
       patientId int,
       calls int,
       locationLatitute double,
       locationLongtitue double,
       recordTime string,
       direction string
       )
       STORED BY 'com.aliyun.odps.CsvStorageHandler'
       LOCATION 'oss://oss-cn-hangzhou-internal.aliyuncs.com/examplebucket/demo/';
```

4. 通过MaxCompute查询外部表。

执行如下SQL语句：















```shell
select recordId, patientId, direction from data_csv_external where patientId > 25;
```



输出结果如下：















```shell
+------------+------------+-----------+
| recordId   | patientId  | direction |
+------------+------------+-----------+
| 1          | 51         | S         |
| 3          | 48         | NE        |
| 4          | 30         | W         |
| 5          | 47         | S         |
| 7          | 53         | N         |
| 8          | 63         | SW        |
| 10         | 31         | N         |
+------------+------------+-----------+
```


## **常见问题**

### **报错：**`Accessing project '<projectname>' failed: ODPS-0420095: Access Denied - Authorization Failed [4002], You don't exist in project <projectname>.` **如何解决？**

- 可能原因：

当前使用的AccessKey对应的阿里云账号或RAM用户未添加到目标项目中。

- 解决方法：

需要您联系项目所有者将对应的阿里云账号或RAM用户添加到目标项目中，操作详情请参见 [添加阿里云账号用户（项目级别）](https://help.aliyun.com/zh/maxcompute/user-guide/user-planning-and-management#section-qg5-xtz-vdb "") 和 [添加RAM用户（项目级别）](https://help.aliyun.com/zh/maxcompute/user-guide/user-planning-and-management#section-udf-j5z-vdb "")。


## **相关文档**

- MaxCompute支持您在项目中创建OSS外部表，与OSS上的目录建立映射关系，您可以通过OSS外部表访问OSS目录下的非结构化数据，或者将MaxCompute项目中的数据写入OSS。更多信息，请参见 [创建OSS外部表](https://help.aliyun.com/zh/maxcompute/user-guide/orc-external-tables "")。

- 如果您需要将MaxCompute表中的数据导出到本地，便于离线查看数据。请参见 [运行SQL命令并导出结果数据](https://help.aliyun.com/zh/maxcompute/getting-started/execute-sql-statements-and-export-the-result-data "")。

- 如果您不再需要保留表数据或MaxCompute项目，可以删除表或MaxCompute项目，以免产生不必要的资源浪费及账单费用。请参见 [删除表或MaxCompute项目](https://help.aliyun.com/zh/maxcompute/getting-started/delete-a-table-or-a-maxcompute-project "")。