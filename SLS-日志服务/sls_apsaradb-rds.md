### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[日志审计（旧版）](https://help.aliyun.com/zh/sls/log-audit-service/)[日志字段详情](https://help.aliyun.com/zh/sls/log-fields-34/)云数据库RDS

# 云数据库RDS

更新时间：2024-07-26 02:45:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：对象存储](https://help.aliyun.com/zh/sls/oss)[下一篇：PolarDB云原生数据库](https://help.aliyun.com/zh/sls/polardb-for-mysql)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

审计日志

慢日志

性能日志

错误日志

本文介绍云数据库RDS SQL审计日志、慢日志、错误日志和性能日志的字段详情。

## 审计日志

| **日志字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为rds\_audit\_log。 |
| owner\_id | 阿里云账号ID |
| region | RDS实例所在地域 |
| instance\_name | RDS实例名 |
| instance\_id | RDS实例ID |
| db\_type | 数据库类型 |
| db\_version | 数据库引擎版本 |
| check\_rows | 扫描的行数 |
| db | 数据库名 |
| fail | SQL执行是否出错。<br>其中，0表示成功，除0之外的其他值都表示失败。 |
| client\_ip | 访问RDS实例的客户端IP地址 |
| threat\_client\_ip | 访问RDS实例的客户端IP地址的威胁情报。更多信息，请参见 [威胁情报字段](https://help.aliyun.com/zh/sls/generate-threat-intelligence#section-ghm-rcz-m63 "")。 |
| latency | 执行SQL操作后，多久返回结果，单位：微秒。 |
| origin\_time | 执行操作的时间点 |
| return\_rows | 返回的行数 |
| sql | 执行的SQL语句 |
| thread\_id | 线程ID |
| user | 执行SQL的用户名 |
| update\_rows | 更新行数 |
| hash | 哈希值 |

## 慢日志

| **日志字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题。<br>- RDS MySQL慢日志的主题为rds\_slow\_log。<br>  <br>- RDS PostgreSQL慢日志的主题为rds\_slow\_log\_pg。 |
| owner\_id | 阿里云账号ID |
| region | RDS实例所在地域 |
| instance\_name | RDS实例名 |
| instance\_id | RDS实例ID |
| db\_type | RDS实例类型 |
| db\_version | RDS实例版本号 |
| db\_name | 数据库名 |
| rows\_examined | 扫描的行数 |
| rows\_sent | 返回的行数 |
| start\_time | 开始执行的时间 |
| query\_time | 执行的耗时，单位：秒。 |
| lock\_time | 锁等待的耗时，单位：秒。 |
| user\_host | 客户端信息 |
| query\_sql | 慢日志SQL语句 |

## 性能日志

| **指标名称** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **指标名称** | **说明** |
| mysql\_perf\_active\_session | 活跃连接数，单位：个。 |
| mysql\_perf\_com\_delete | 平均每秒Delete语句执行次数 |
| mysql\_perf\_com\_insert | 平均每秒Insert语句执行次数 |
| mysql\_perf\_com\_insert\_select | 平均每秒Insert Select语句执行次数 |
| mysql\_perf\_com\_replace | 平均每秒Replace语句执行次数 |
| mysql\_perf\_com\_replace\_select | 平均每秒Replace Select语句执行次数 |
| mysql\_perf\_com\_select | 平均每秒Select语句执行次数 |
| mysql\_perf\_com\_update | 平均每秒Update语句执行次数 |
| mysql\_perf\_conn\_usage | RDS实例连接使用率，单位：百分比。 |
| mysql\_perf\_cpu\_usage | RDS实例CPU使用率，单位：百分比。 |
| mysql\_perf\_data\_size | RDS实例的数据空间使用量，单位：MB。 |
| mysql\_perf\_disk\_usage | RDS实例磁盘使用率，单位：百分比。 |
| mysql\_perf\_ibuf\_dirty\_ratio | 缓冲池脏块的百分率，单位：百分比。 |
| mysql\_perf\_ibuf\_read\_hit | 缓冲池的读命中率 |
| mysql\_perf\_ibuf\_request\_r | 平均每秒钟从InnoDB缓冲池的读次数 |
| mysql\_perf\_ibuf\_request\_w | 平均每秒钟向InnoDB缓冲池的写次数 |
| mysql\_perf\_ibuf\_use\_ratio | 缓冲池的利用率，单位：百分比。 |
| mysql\_perf\_inno\_data\_read | InnoDB平均每秒钟读取的数据量，单位：KB。 |
| mysql\_perf\_inno\_data\_written | InnoDB平均每秒钟写入的数据量，单位：KB。 |
| mysql\_perf\_inno\_row\_delete | 平均每秒从InnoDB表删除的行数 |
| mysql\_perf\_inno\_row\_insert | 平均每秒从InnoDB表插入的行数 |
| mysql\_perf\_inno\_row\_readed | 平均每秒从InnoDB表读取的行数 |
| mysql\_perf\_inno\_row\_update | 平均每秒从InnoDB表更新的行数 |
| mysql\_perf\_innodb\_log\_write\_requests | 平均每秒日志写请求数 |
| mysql\_perf\_innodb\_log\_writes | 平均每秒向日志文件的物理写次数 |
| mysql\_perf\_innodb\_os\_log\_fsyncs | 平均每秒向日志文件完成的fsync()写数量 |
| mysql\_perf\_ins\_size | RDS实例磁盘使用量，单位：MB。 |
| mysql\_perf\_iops | IOPS，单位：次/秒。 |
| mysql\_perf\_iops\_usage | RDS实例IOPS使用率，单位：百分比。 |
| mysql\_perf\_kbytes\_received | 平均每秒钟的输入流量，单位：KB。 |
| mysql\_perf\_kbytes\_sent | 平均每秒钟的输出流量，单位：KB。 |
| mysql\_perf\_log\_size | Binlog占用的数据空间，单位：MB。 |
| mysql\_perf\_mem\_usage | RDS实例内存使用率，单位：百分比。 |
| mysql\_perf\_open\_tables | 当前打开表数量 |
| mysql\_perf\_other\_size | RDS实例其他空间使用量，单位：MB。 |
| mysql\_perf\_qps | 平均每秒SQL语句执行次数 |
| mysql\_perf\_slow\_queries | 平均每秒慢查询数量 |
| mysql\_perf\_tb\_tmp\_disk | MySQL执行语句时每秒在磁盘上自动创建的临时表的数量 |
| mysql\_perf\_threads\_connected | MySQL线程连接数 |
| mysql\_perf\_threads\_running | MySQL活跃线程 |
| mysql\_perf\_tmp\_size | RDS实例临时空间使用量，单位：MB。 |
| mysql\_perf\_total\_session | 总连接数，单位：个。 |
| mysql\_perf\_tps | 平均每秒事务数 |

## 错误日志

| **日志字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **日志字段** | **说明** |
| \_\_topic\_\_ | 日志主题。<br>- RDS MySQL错误日志的主题为rds\_error\_log。<br>  <br>- RDS PostgreSQL错误日志的主题为rds\_error\_log\_pg。 |
| collect\_time | 采集时间 |
| content | 日志内容 |
| db\_type | RDS实例类型 |
| db\_version | RDS实例版本号 |
| event\_type | 事件类型 |
| instance\_id | RDS实例ID |
| instance\_name | RDS实例名 |
| region | RDS实例所属地域 |
| db\_name | 数据库名 |
| file | 失败信息 |
| port | 数据库端口号 |
| user | 用户 |
| user\_ip | 用户IP地址 |
| user\_port | 用户端口号 |