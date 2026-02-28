### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[常见问题](https://help.aliyun.com/zh/open-search/high-performance-searchedition/faq/)访问控制RAM

# 应用授权规则列表

更新时间：2025-03-05 08:23:06

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：服务条款](https://help.aliyun.com/zh/open-search/high-performance-searchedition/the-terms-of-service)[下一篇：授权资源类型](https://help.aliyun.com/zh/open-search/high-performance-searchedition/types-of-resources-that-can-be-authorized)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

管控API授权规则

流量API授权规则

本文为您介绍管控API授权规则与流量API授权规则。

## 管控API授权规则

| **POP Action** | Description | **RAM Action** | **Resource Pattern** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **POP Action** | Description | **RAM Action** | **Resource Pattern** |
| ListApps | 获取所有应用版本 | opensearch:ListApp | apps/\* |
| CreateAppGroup | 创建应用 | opensearch:CreateAppGroup | app-groups/\* |
| DescribeAppGroupDataReport | 查询应用的数据质量报告 | opensearch:DescribeApp | apps/$appGroupName |
| RemoveAppGroup | 删除应用 | opensearch:RemoveAppGroup | app-groups/$appGroupName |
| ListAppGroupErrors | 查询应用的错误日志 | opensearch:ListAppGroupErrors | app-groups/$appGroupName |
| ListAppGroups | 获取应用列表 | opensearch:ListAppGroup | app-groups/\* |
| ListAppGroupMetrics | 查询应用的数据报表 | opensearch:ListAppGroupMetric | app-groups/$appGroupName |
| RenewAppGroup | 为应用续费 | opensearch:UpdateApp | apps/$appGroupName |
| DescribeAppGroup | 获取应用详情 | opensearch:DescribeAppGroup | app-groups/$appGroupName |
| ReplaceAppGroupCommodityCode | 应用服务型转实例型 | opensearch:UpdateApp | apps/$appGroupName |
| ModifyAppGroup | 修改应用属性或切换线上版本 | opensearch:ModifyAppGroup | app-groups/$appGroupName |
| ModifyAppGroupQuota | 修改应用配额 | opensearch:updateAppGroupQuota | app-groups/$appGroupName |
| CreateApp | 创建应用版本 | opensearch:CreateApp | app-groups/$appGroupName |
| RemoveApp | 删除应用版本 | opensearch:RemoveApp | app-groups/$appGroupName |
| DescribeApps | 获取应用的版本列表 | opensearch:ListApp | app-groups/$appGroupName |
| DescribeApp | 查看应用版本详情 | opensearch:DescribeApp | app-groups/$appGroupName |
| DescribeAppStatistics | 获取应用版本的统计结果 | opensearch:DescribeAppStatistics | app-groups/$appGroupName |
| UpdateFetchFields | 更新应用版本的默认展示字段 | opensearch:UpdateApp | apps/$appGroupName |
| CreateFirstRank | 创建应用版本的粗排表达式配置 | opensearch:WriteFirstRank | apps/$appGroupName |
| RemoveFirstRank | 删除应用版本的粗排表达式配置 | opensearch:WriteFirstRank | apps/$appGroupName |
| ListFirstRanks | 获取应用版本的粗排表达式配置列表 | opensearch:ListFirstRank | apps/$appGroupName |
| DescribeFirstRank | 获取应用版本的粗排表达式配置详情 | opensearch:DescribeFirstRank | apps/$appGroupName |
| ModifyFirstRank | 修改应用版本的粗排表达式配置 | opensearch:WriteFirstRank | apps/$appGroupName |
| ListSlowQueryCategories | 获取优化大师慢查询优化建议清单 | opensearch:ListOptimizerSlowQueryCategories | apps/$appGroupName |
| StartSlowQueryAnalyzer | 立即进行慢查询分析 | opensearch:WriteOptimizerSlowQueryCategories | apps/$appGroupName |
| ListSlowQueryQueries | 列出优化大师慢查询Query清单 | opensearch:ListOptimizerSlowQueries | apps/$appGroupName |
| DisableSlowQuery | 禁用优化大师慢查询服务 | opensearch:WriteOptimizerSlowQuery | apps/$appGroupName |
| EnableSlowQuery | 启用优化大师慢查询服务 | opensearch:WriteOptimizerSlowQuery | apps/$appGroupName |
| DescribeSlowQueryStatus | 获取优化大师慢查询开通状态 | opensearch:DescribeOptimizerSlowQuery | apps/$appGroupName |
| CreateScheduledTask | 创建应用的定时任务 | opensearch:CreateScheduledTask | app-groups/$appGroupName |
| RemoveScheduledTask | 删除应用的定时任务 | opensearch:RemoveScheduledTask | app-groups/$appGroupName |
| ListScheduledTasks | 获取应用定时任务列表 | opensearch:ListScheduledTask | app-groups/$appGroupName |
| DescribeScheduledTask | 获取应用定时任务详情 | opensearch:DescribeScheduledTask | app-groups/$appGroupName |
| ModifyScheduledTask | 修改应用定时任务 | opensearch:ModifyScheduledTask | app-groups/$appGroupName |
| CreateSecondRank | 创建应用版本的精排表达式配置 | opensearch:WriteSecondRank | apps/$appGroupName |
| RemoveSecondRank | 删除应用版本的精排表达式配置 | opensearch:WriteSecondRank | apps/$appGroupName |
| ListSecondRanks | 获取应用版本的精排表达式配置列表 | opensearch:ListSecondRank | apps/$appGroupName |
| DescribeSecondRank | 获取应用版本的精排表达式配置详情 | opensearch:DescribeSecondRank | apps/$appGroupName |
| ModifySecondRank | 修改应用版本的精排表达式配置 | opensearch:WriteSecondRank | apps/$appGroupName |
| ListSortExpressions | 获取应用版本上的排序表达式列表 | opensearch:ListSortExpression | apps/$appGroupName |
| UpdateSummaries | 修改应用版本摘要 | opensearch:WriteSummary | apps/$appGroupName |
| PushUserAnalyzerEntries | 接收自定义分析器词条变更 | opensearch:WriteUserAnalyzer | user-analyzers/$analyzerName |
| ListUserAnalyzerEntries | 获取自定义分析器词条清单 | opensearch:DescribeUserAnalyzer | user-analyzers/$analyzerName |
| CreateUserAnalyzer | 创建自定义分析器 | opensearch:CreateUserAnalyzer | user-analyzers/$analyzerName |
| DeleteUserAnalyzer | 删除自定义分析器 | opensearch:DeleteUserAnalyzer | user-analyzers/$analyzerName |
| ListUserAnalyzers | 获取用户的自定义分词器列表 | opensearch:ListUserAnalyzers | user-analyzers/\* |
| DescribeUserAnalyzer | 获取自定义分析器详情 | opensearch:DescribeUserAnalyzer | user-analyzers/$analyzerName |

## 流量API授权规则

| **POP Action** | **Action Describe** | **RAM Action** | **Resource Pattern** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **POP Action** | **Action Describe** | **RAM Action** | **Resource Pattern** |
| PushDoc | 推送文档 | opensearch:PushDoc | acs:opensearch:$regionId:$accountId:apps/$appGroupName |
| SearchApp | 文档召回 | opensearch:SearchApp | acs:opensearch:$regionId:$accountId:apps/$appGroupName |