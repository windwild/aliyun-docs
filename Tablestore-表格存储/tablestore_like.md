### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[多元索引](https://help.aliyun.com/zh/tablestore/search-index-introduction-of-tablestore/)[基础查询](https://help.aliyun.com/zh/tablestore/basic-features/)模糊查询

# 模糊查询

更新时间：2024-12-25 01:26:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：列存在性查询](https://help.aliyun.com/zh/tablestore/exists-query-function)[下一篇：通配符查询](https://help.aliyun.com/zh/tablestore/wildcard-query-function)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

查询类型

表格存储多元索引提供了通配符查询、前缀查询和后缀查询功能来满足用户不同场景的模糊查询需求，请根据实际业务需求选择合适的查询方式。本文介绍多元索引支持的模糊查询类型。

## **背景信息**

在业务开发过程中，经常需要用到模糊查询的功能，例如查询人名、电话号码、订单号等。在关系型数据库中，您可以使用like语法进行模糊查询。同样在表格存储的多元索引中也支持模糊查询功能。

## **查询类型**

目前多元索引中模糊查询功能可以按照查询功能分为以下三种：

- [通配符查询](https://help.aliyun.com/zh/tablestore/wildcard-query-function "")：类似于传统关系型数据库里面的like语法，支持星号（\*）和问号（?）两种通配符。要匹配的值中可以用星号（\*）代表任意字符序列，或者用问号（?）代表任意单个字符，且支持以星号（\*）或问号（?）开头。例如查询`table*e`，可以匹配到`tablestore`。

- [前缀查询](https://help.aliyun.com/zh/tablestore/prefix-query-function "")：通过指定前缀来查询，例如查询所有订单中以`H00`开始的订单。

- [后缀查询](https://help.aliyun.com/zh/tablestore/suffix-query "")：通过指定后缀来查询，例如查询所有手机号码中以`1234`结束的手机号。


模糊查询功能按照字段类型和实现可以分为以下三种：

- **Keyword类型：字符串匹配式模糊查询**：查询过程中需要逐个字符串进行匹配，查询性能会随着数据规模增加而下降，支持 [通配符查询](https://help.aliyun.com/zh/tablestore/wildcard-query-function "") 和 [前缀查询](https://help.aliyun.com/zh/tablestore/prefix-query-function "")。大小写敏感，最大支持的字段长度为4 KB。

- **FuzzyKeyword类型：面向模糊查询的专项优化**：相对于Keyword类型可以更快地查询到数据，并且查询性能比 Keyword 类型更稳定，基本不受数据规模影响，支持 [通配符查询](https://help.aliyun.com/zh/tablestore/wildcard-query-function "")、 [前缀查询](https://help.aliyun.com/zh/tablestore/prefix-query-function "") 和 [后缀查询](https://help.aliyun.com/zh/tablestore/suffix-query "")。大小写敏感，最大支持的字段长度为2 KB。

- **Text类型：分词模式**：使用FuzzyAnalyzer，更加自由可控，支持大小写敏感控制，功能上仅支持 `*ALI*`模式的 [基于分词的通配符查询](https://help.aliyun.com/zh/tablestore/fuzzy-query "")。在使用FuzzyAnalyzer时，最大支持的字段长度为1 KB。