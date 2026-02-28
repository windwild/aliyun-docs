日志服务采用三副本机制为您提供高可靠性。

日志服务底层存储采用三副本机制来保证数据的可靠性，即每份数据都有3个副本，副本按照一定的分布式存储算法保存在集群中的不同机器。通过该机制，存储系统确保3个数据副本分布在不同服务器的不同物理磁盘上，单个硬件设备的故障不会造成数据丢失，同时确保3个数据副本之间的数据强一致性。

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据存储](https://help.aliyun.com/zh/sls/data-storage/)数据可靠性

# 数据可靠性

更新时间：2022-03-22 03:22:14

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：数据防篡改](https://help.aliyun.com/zh/sls/data-tamper-proof)[下一篇：查询与分析快速指引](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis)

该文章对您有帮助吗？

反馈