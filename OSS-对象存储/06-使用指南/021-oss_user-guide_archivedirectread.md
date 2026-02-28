### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据湖](https://help.aliyun.com/zh/oss/user-guide/oss-data-lake/)[OSS-HDFS服务](https://help.aliyun.com/zh/oss/user-guide/oss-hdfs/)[数据管理](https://help.aliyun.com/zh/oss/user-guide/manage-osshdfs-data/)[常用Shell命令](https://help.aliyun.com/zh/oss/user-guide/common-shell-commands-used-for-oss-hdfs/)ArchiveDirectRead（归档直读）

# 无需解冻直接实时读取OSS-HDFS服务归档文件

更新时间：2025-09-15 23:54:12

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

使用限制

费用说明

操作步骤

后续步骤

相关文档

归档直读是指直接访问OSS-HDFS服务中归档存储类型的文件，而无需先对其解冻。归档直读适用于实时读取极少需要访问的数据场景。

## **前提条件**

- 已创建ECS实例。具体步骤，请参见 [选购ECS实例](https://help.aliyun.com/zh/ecs/getting-started/create-and-manage-an-ecs-instance-by-using-the-ecs-console#section-ucc-o12-trs "")。

- 已开通OSS-HDFS服务。具体步骤，请参见 [开通OSS-HDFS服务](https://help.aliyun.com/zh/oss/user-guide/enable-oss-hdfs-service "")。

- 阿里云账号默认拥有为Bucket开启归档直读功能的权限。如果您希望通过RAM用户的方式为Bucket开启归档直读功能，RAM用户需要具备对应的权限要求，详情请参见 [授权RAM用户通过非EMR集群接入OSS-HDFS服务](https://help.aliyun.com/zh/oss/user-guide/authorize-access-to-oss-hdfs-services#7e4e949833p67 "")。


## 使用限制

归档直读仅适用于OSS-HDFS服务Bucket中归档存储类型的文件，不适用于其他存储类型的文件。

## **费用说明**

- 为Bucket开启归档直读后，直接读取Bucket中未解冻的归档存储类型文件，会产生归档直读数据取回容量（RetrievalDataArchiveDirect）费用，请求产生的归档直读取回容量通过日志字段`archive_direct_read_size`的值来表示。对于已解冻的归档存储类型文件，直接读取不会产生归档直读数据取回容量费用。详情请参见 [数据处理费用](https://help.aliyun.com/zh/oss/data-processing-fees "")。

- 归档直读数据取回量取决于与HTTP建立连接时请求头中指定的数据读取范围。传输连接的提前断开不会影响已发起请求的归档直读数据取回容量。例如，实际读取1字节数据后中断连接，但是请求范围为100 MB~200 MB，将按照100 MB~200 MB计算归档直读数据取回容量。


## **操作步骤**

1. 连接ECS实例。具体操作，请参见 [连接ECS实例](https://help.aliyun.com/zh/ecs/getting-started/create-and-manage-an-ecs-instance-by-using-the-ecs-console#section-fqu-flq-xvv "")。

2. 下载 [Jindofs SDK](https://jindodata-binary.oss-cn-shanghai.aliyuncs.com/release/6.2.5/jindofs-sdk-6.2.5-linux.tar.gz)。

3. 配置访问密钥和环境变量。

1. 进入已安装的Jindofs JAR包下的bin目录。

      以下以`jindofs-sdk-x.x.x-linux`为例，如使用其他版本的JindoSDK，请替换为对应的JAR包名称。















      ```shell
      cd jindofs-sdk-x.x.x-linux/bin/
      ```

2. 在bin目录下新建配置文件jindofs.cfg，并配置阿里云账号的访问密钥（包括Accesskey ID和Accesskey Secret），或者满足权限要求的RAM用户的访问密钥。















      ```shell
      [client]
      fs.oss.accessKeyId = <key>
      fs.oss.accessKeySecret = <secret>
      ```

3. 设置环境变量。



      **说明**





      <JINDOSDK\_CONF\_DIR>填写`jindofs.cfg`配置文件所在的绝对路径。



















      ```shell
      export JINDOSDK_CONF_DIR=<JINDOSDK_CONF_DIR>
      ```
4. 为Bucket开启归档直读功能。

以下示例用于为华东（上海）地域的examplebucket开启归档直读功能。其他地域的Bucket，请对应替换Region和Bucket名称。















```shell
./jindofs admin -putConfig -dlsUri oss://examplebucket.cn-shanghai.oss-dls.aliyuncs.com/ -conf namespace.archive.directread.enable=true
```

5. 查看Bucket归档直读配置信息。















```shell
./jindofs admin -getConfig -dlsUri oss://examplebucket.cn-shanghai.oss-dls.aliyuncs.com/ -name namespace.archive.directread.enable
```



返回信息如下，说明Bucket已开启归档直读功能。















```shell
namespace.archive.directread.enable: true
```


## **后续步骤**

为Bucket开启归档直读后，您无需解冻Bucket中的归档存储类型文件，就可以直接对其进行涉及读取的操作，包括下载文件、查看文件信息、拷贝文件的操作。

## 相关文档

如果您未开启归档直读，需要先解冻，才能读取归档存储类型文件。如何解冻归档文件，请参见 [临时解冻归档文件](https://help.aliyun.com/zh/oss/user-guide/enable-the-automatic-storage-tiering-feature-for-the-oss-hdfs-service#d39c083dd0vz6 "")。