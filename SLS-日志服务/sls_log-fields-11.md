### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[日志数据采集（Log）](https://help.aliyun.com/zh/sls/sls-log-collection/)[云产品日志采集](https://help.aliyun.com/zh/sls/collection-of-alibaba-cloud-service-logs/)[RDS SQL审计日志](https://help.aliyun.com/zh/sls/rds-sql-execution-logs-usage-notes/)日志字段详情

# 日志字段详情

更新时间：2024-08-07 04:41:35

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

审计日志

慢日志

slow\_error\_log

本文介绍RDS相关日志的字段详情。

## 审计日志

| **字段名称** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段名称** | **说明** |
| \_\_topic\_\_ | 日志主题，固定为rds\_audit\_log。 |
| instance\_id | RDS实例ID。 |
| check\_rows | 扫描的行数。 |
| db | 数据库名。 |
| fail | SQL执行是否出错。 <br>- 如果是MySQL实例或SQL Server实例，则执行成功时，字段值为0，除0之外的其他值都表示失败。<br>- 如果是PostgreSQL实例，则执行成功时，字段值为0000，除0000之外的其他值都表示失败。 |
| client\_ip | 访问RDS实例的客户端IP地址。 |
| latency | 执行SQL操作后，多久返回结果，单位：微秒。 |
| origin\_time | 执行操作的时间点。 |
| return\_rows | 返回的行数。 |
| sql | 执行的SQL语句。 |
| thread\_id | 线程ID。 |
| user | 执行操作的用户名。 |
| update\_rows | 更新的行数。 |

## 慢日志

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| \_\_topic\_\_ | 日志主题。<br>- RDS MySQL慢日志的主题为rds\_slow\_log。<br>- RDS PostgreSQL慢日志的主题为rds\_slow\_log\_pg。 |
| db\_name | 数据库名称 |
| db\_type | 数据库类型，包括MySQL、PostgrepSQL。 |
| db\_version | 数据库版本 |
| instance\_id | 集群ID |
| lock\_time | 锁等待的耗时，单位：秒。 |
| owner\_id | 阿里云账号ID |
| query\_sql | 慢日志SQL语句 |
| query\_time | 查询耗时，单位：秒。 |
| region | RDS实例所在地域 |
| rows\_examined | 扫描的行数 |
| rows\_sent | 返回的行数 |
| start\_time | 开始执行的时间 |
| user\_host | 客户端信息 |

## slow\_error\_log

| **字段** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **说明** |
| \_\_topic\_\_ | 日志主题。<br>- RDS MySQL错误日志的主题为rds\_error\_log。<br>- RDS PostgreSQL错误日志的主题为rds\_error\_log\_pg。 |
| instance\_id | 集群ID |
| collect\_time | 采集时间 |
| db\_type | 数据库类型，包括MySQL、PostgrepSQL。 |
| db\_version | 数据库版本 |
| content | 日志内容 |
| eventType | 事件类型 |