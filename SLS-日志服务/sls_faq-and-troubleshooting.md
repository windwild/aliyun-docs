### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[使用第三方工具查询与分析](https://help.aliyun.com/zh/sls/use-third-party-tools-to-query-and-analyze-log-service-data/)常见问题和错误排查

# 常见问题和错误排查

更新时间：2026-01-05 01:59:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Kibana Dashboard迁移](https://help.aliyun.com/zh/sls/kibana-dashboard-migration)[下一篇：使用PostgreSQL协议接入SLS](https://help.aliyun.com/zh/sls/use-the-postgresql-protocol-to-access-sls)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

常见问题

常见错误

本文介绍日志服务所提供的Elasticsearch兼容接口的常见问题和错误排查方法。

**重要**

本文档为阿里云原创文档，知识产权归阿里云所有，由于本文档旨在介绍阿里云与第三方产品交互的服务能力，因此可能会提及第三方公司或产品等名称。

## **常见问题**

Q：使用Elasticsearch兼容接口时，Elasticsearch是否需要执行Index滚动？

A：不需要。一般情况下，Elasticsearch按天滚动Index，产生新的Index，从而避免单个Index过大问题。但是日志服务的LogStore容量上限较高，Elasticsearch不需要执行Index滚动。

## **常见错误**

| **错误信息** | **错误说明** | **处理方法** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **错误信息** | **错误说明** | **处理方法** |
| index config doesn't exist | 对应的LogStore没有开启索引配置。 | 为目标LogStore创建索引，并且为需要分析的字段设置字段索引。具体操作，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes "")。 |
| xxx is not configed in index | 在日志服务中，没有为xxx字段配置字段索引。 | 为需要分析的字段设置字段索引。具体操作，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes "")。 |
| logstore xxx does not exist" | 对应的LogStore不存在。 | 检查Elasticsearch的索引模式名称是否配置正确。该名称的正确命名规则为`${日志服务Project名称}.${Logstore名称}`。 |
| please set user/password, use Aliyun accessKeyId/accessKeySecret as user/password | 鉴权认证失败。 | 检查请求Elasticsearch兼容接口时，是否正确配置了BasicAuth的UserName和Password。 |