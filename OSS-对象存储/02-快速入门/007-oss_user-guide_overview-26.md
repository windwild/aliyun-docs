### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[服务支持](https://help.aliyun.com/zh/oss/user-guide/support/)[白皮书](https://help.aliyun.com/zh/oss/user-guide/whitepapers/)阿里云存储服务概述

# 阿里云各类存储服务的特性和使用场景

更新时间：2024-11-28 06:00:37

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

阿里云提供针对各种存储资源（块、文件和对象）的低成本、高可靠、高可用的存储服务，涵盖数据备份、归档、容灾等场景。本文介绍阿里云各类存储服务及特性的适用场景、性能、安全、接口和费用模型等，帮助您选择最适合您业务场景和需求的云存储服务。

有关阿里云存储服务的详细介绍、客户案例、解决方案等，请参见 [阿里云存储产品家族](https://www.aliyun.com/storage/storage)。

|     |     |
| --- | --- |
| [对象存储OSS](https://help.aliyun.com/zh/oss/user-guide/oss-overview#concept-2547936 "") | 对象存储OSS是一款海量、安全、低成本、高可靠的云存储服务，其容量和处理能力弹性扩展，提供多种存储类型供选择，覆盖从热到冷的各种数据存储场景，帮助您全面优化存储成本。 |
| [块存储](https://help.aliyun.com/zh/oss/user-guide/block-storage#concept-2547939 "") | 块存储是阿里云为云服务器ECS提供的块设备，高性能、低时延、随机读写。您可以像使用物理硬盘一样格式化并建立文件系统来使用块存储。 |
| [文件存储NAS](https://help.aliyun.com/zh/oss/user-guide/apsara-file-storage-nas#concept-2547938 "") | 文件存储NAS是一款面向阿里云ECS实例、E-HPC和容器服务等计算节点的高可靠、高性能的分布式文件系统，可共享访问、弹性扩展。NAS基于POSIX文件接口，天然适配原生操作系统。 |
| [文件存储CPFS](https://help.aliyun.com/zh/oss/user-guide/cpfs-file-systems#concept-2548158 "") | 文件存储CPFS是一款并行文件系统，其数据存储在集群中的多个数据节点，多个客户端可以同时访问，满足大型高性能计算机集群的高IOPS、高吞吐、低时延的数据存储需求。 |
| [文件存储HDFS版](https://help.aliyun.com/document_detail/207144.html#concept-2545035 "") | 文件存储HDFS版是一款面向阿里云ECS实例及容器服务等计算资源的文件存储服务，满足以Hadoop为代表的分布式计算业务类型对分布式存储性能、容量和可靠性的多方面要求。 |
| [表格存储](https://help.aliyun.com/zh/oss/user-guide/tablestore#concept-2549749 "") | 表格存储是阿里云自研的结构化数据存储，提供海量结构化数据存储以及快速的查询和分析服务，具备PB级存储、千万TPS以及毫秒级延迟的服务能力。 |
| [云存储网关](https://help.aliyun.com/zh/oss/user-guide/cloud-storage-gateway#concept-2548519 "") | 云存储网关是一款可以部署在用户IDC和阿里云上的网关产品，以阿里云对象存储OSS为后端存储，为云上和云下应用提供业界标准的文件服务（NFS和SMB）和块存储服务（iSCSI）。 |