### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[服务支持](https://help.aliyun.com/zh/tablestore/support/)[常见问题](https://help.aliyun.com/zh/tablestore/support/faq-4/)[一般性问题](https://help.aliyun.com/zh/tablestore/support/general-faq/)如何理解数据表的主键、数据分区和数据分区键

# 如何理解数据表的主键、数据分区和数据分区键

更新时间：2024-07-14 21:52:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是表格存储](https://help.aliyun.com/zh/tablestore/product-overview/what-is-tablestore)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

主键

数据分区和分区键

**说明**

更多信息，请参见 [宽表模型介绍](https://help.aliyun.com/zh/tablestore/overview-of-widecolumn/ "")。

## 主键

表中的每一行由主键（Primary Key）唯一确定。在创建表时，您必须指定组成主键的列，这些列称为主键列。主键列必须有值。您必须确保主键列的值的组合能够唯一地确定一行数据。在后续使用过程中，主键列的类型不能改变。

## 数据分区和分区键

表格存储会自动把表分成不同的数据分区，以达到对其存储数据的负载均衡。数据分区的划分粒度为主键的第一列，该列即为数据分区键。

具有相同数据分区键的行会在同一个数据分区中。表格存储能够保证对具有同一数据分区键的数据进行更改操作的一致性。

下图是一个电子邮件系统的邮件表的一部分。该表的主键和数据分区键信息如下：

- UserID、ReceiveTime、FromAddr列分别表示邮件用户的ID、接收时间、发送人，这些列为主键列，用于唯一确定一封邮件。其中UserID列为数据分区键。

- ToAddr、MailSize、Subject、Read列分别表示收件人、邮件大小、邮件主题和邮件是否已读，这些为普通的列，用于存储邮件的相关信息。


如下图所示表格存储把UserID为U0001和U0002的用户信息划在一个数据分区中，而把UserID为U0003和U0004的用户信息划分在另一个数据分区中。

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/38572/cn_zh/1512466746845/38572-01.png)