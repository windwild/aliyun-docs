### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[HBase支持](https://help.aliyun.com/zh/tablestore/comparison-between-tablestore-and-hbase/)Tablestore HBase Client介绍

# Tablestore HBase Client介绍

更新时间：2024-12-26 21:42:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：HBase支持](https://help.aliyun.com/zh/tablestore/comparison-between-tablestore-and-hbase/)[下一篇：Tablestore HBase Client快速入门](https://help.aliyun.com/zh/tablestore/quick-start-of-tablestore-hbase-client)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

适用版本

获取方式

使用说明

计费说明

相关文档

除了使用表格存储SDK以及Restful API来访问表格存储，表格存储还提供了Tablestore HBase Client。使用开源HBase API的Java应用可以通过Tablestore HBase Client来直接访问表格存储服务。

## **适用版本**

Tablestore HBase Client基于表格存储4.2.x以上版本Java SDK实现，支持1.x.x版本（适配HBase 1.2.0）和2.x.x版本（适配HBase 2.5.10）的开源HBase API。

## **获取方式**

Tablestore HBase Client的获取方式根据适配的HBase API版本不同存在差异。由于HBase Client 2.x.x与HBase Client 1.x.x版本存在接口变化，请根据要使用的HBase Client版本选择Tablestore HBase Client版本。

- 如需使用HBase Client 2.x.x版本，请使用Tablestore HBase Client 2.x.x版本。

- 如需使用HBase Client 1.x.x版本，请使用Tablestore HBase Client 1.x.x版本。

- 如需使用HBase Client 0.x.x版本，请参见 [如何兼容Hbase 1.0以前的版本](https://help.aliyun.com/zh/tablestore/make-tablestore-hbase-client-compatible-with-hbase-versions-earlier-than-1-0#concept-50166-zh "")。


适配HBase Client 2.x.x版本

适配HBase Client 1.x.x版本

您可以通过如下方式获取Tablestore HBase Client。

- 从GitHub下载 [tablestore-hbase-client项目](https://github.com/aliyun/aliyun-tablestore-hbase-client)。

- 直接下载 [tablestore-hbase-client-2.0.12.zip](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20241218/pvirvn/tablestore-hbase-client-2.0.12.zip)

- Maven

Tablestore HBase Client 2.0.12版本依赖了HBase Client 2.5.10版本和Tablestore Java SDK 5.17.4版本。在Maven项目pom.xml文件中加入如下依赖：















```xml
<dependencies>
      <dependency>
          <groupId>com.aliyun.openservices</groupId>
          <artifactId>tablestore-hbase-client</artifactId>
          <version>2.0.12</version>
      </dependency>
</dependencies>
```



如果需要使用其它版本的HBase Client或Tablestore Java SDK，可以使用exclusion标签。如下示例中使用HBase Client 2.5.0版本和Tablestore Java SDK 5.17.0版本。















```xml
<dependencies>
      <dependency>
          <groupId>com.aliyun.openservices</groupId>
          <artifactId>tablestore-hbase-client</artifactId>
          <version>2.0.12</version>
          <exclusions>
              <exclusion>
                  <groupId>com.aliyun.openservices</groupId>
                  <artifactId>tablestore</artifactId>
              </exclusion>
              <exclusion>
                  <groupId>org.apache.hbase</groupId>
                  <artifactId>hbase-client</artifactId>
              </exclusion>
          </exclusions>
      </dependency>
      <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>2.5.0</version>
      </dependency>
      <dependency>
          <groupId>com.aliyun.openservices</groupId>
          <artifactId>tablestore</artifactId>
          <classifier>jar-with-dependencies</classifier>
          <version>5.17.0</version>
      </dependency>
</dependencies>
```


您可以通过如下方式获取Tablestore HBase Client。

- 从GitHub下载 [tablestore-hbase-client项目](https://github.com/alibaba-archive/aliyun-tablestore-hbase-client)。

- 直接下载 [tablestore-hbase-client-1.2.0.zip](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20220527/dvue/tablestore-hbase-client-1.2.0.zip)。

- Maven

Tablestore HBase Client 1.2.0版本依赖了HBase Client 1.2.0版本和Tablestore Java SDK 4.2.1版本。在Maven项目pom.xml文件中加入如下依赖：















```xml
<dependencies>
      <dependency>
          <groupId>com.aliyun.openservices</groupId>
          <artifactId>tablestore-hbase-client</artifactId>
          <version>1.2.0</version>
      </dependency>
</dependencies>
```



如果需要使用其他版本的HBase Client或Tablestore Java SDK，可以使用exclusion标签。下面示例中使用HBase Client 1.2.1版本和Tablestore Java SDK 4.2.0版本。















```xml
<dependencies>
      <dependency>
          <groupId>com.aliyun.openservices</groupId>
          <artifactId>tablestore-hbase-client</artifactId>
          <version>1.2.0</version>
          <exclusions>
              <exclusion>
                  <groupId>com.aliyun.openservices</groupId>
                  <artifactId>tablestore</artifactId>
              </exclusion>
              <exclusion>
                  <groupId>org.apache.hbase</groupId>
                  <artifactId>hbase-client</artifactId>
              </exclusion>
          </exclusions>
      </dependency>
      <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.2.1</version>
      </dependency>
      <dependency>
          <groupId>com.aliyun.openservices</groupId>
          <artifactId>tablestore</artifactId>
          <classifier>jar-with-dependencies</classifier>
          <version>4.2.0</version>
      </dependency>
</dependencies>
```


## **使用说明**

将HBase数据迁移到表格存储后，使用Tablestore HBase Client时，您无需关心HBase Server的相关事项，只需要通过Client提供的接口进行表或数据操作即可。表格存储为您屏蔽了数据表分裂、Dump、Compact、Region Server等底层相关的细节，您只需要关心数据的使用。

- 通过Tablestore HBase Client快速对表格存储数据进行读写的流程，请参见 [快速入门](https://help.aliyun.com/zh/tablestore/quick-start-of-tablestore-hbase-client "")。

- 如需使用Tablestore HBase Client操作表格存储的数据，请参见 [从HBase Client迁移到Tablestore HBase Client](https://help.aliyun.com/zh/tablestore/migrate-data-from-hbase-to-tablestore#concept-50127-zh "")。


## **计费说明**

通过Tablestore HBase Client读写数据时会产生数据写入、数据读取和数据存储费用。更多信息，请参见 [计费概述](https://help.aliyun.com/zh/tablestore/product-overview/billing-overview/ "")。

## **相关文档**

虽然表格存储与HBase在数据模型及功能上相近，Tablestore HBase Client与原生的HBase API仍然有一些区别。具体差异请参见 [Tablestore HBase Client支持的功能](https://help.aliyun.com/zh/tablestore/features-of-tablestore-hbase-client "")。