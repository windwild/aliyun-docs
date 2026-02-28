### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)[查询语法与功能](https://help.aliyun.com/zh/sls/query-syntax/)短语查询

# 短语查询

更新时间：2025-04-10 22:58:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查询语法与功能](https://help.aliyun.com/zh/sls/query-syntax/)[下一篇：LiveTail](https://help.aliyun.com/zh/sls/livetail)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

语法

使用限制

翻页说明

示例

本文介绍短语查询的语法、使用限制和示例。

## 概述

日志服务查询采用的是分词法，例如查询语句为`abc def`，将匹配所有包含`abc`和`def`的日志，不区分先后顺序，无法精准匹配目标短语。现在日志服务推出短语查询，用于精准匹配一段短语。

日志服务接收到短语查询请求后，执行流程主要分为如下两步：

1. 先执行对应的非短语查询语句进行日志查询。例如执行`#"abc def"`语句，实际先执行`"abc def"`语句。



**说明**





为避免查询量太大，目前执行短语查询时，限制步骤1最多返回10,000条结果。

2. 在上述查询结果中再挑选符合短语查询条件的日志，并返回最终的查询结果。


## 语法

**说明**

[Copilot：AI辅助SQL语句自动生成](https://help.aliyun.com/zh/sls/copilot-automatic-generation-of-ai-assisted-sql-statements "")：日志服务提供AI智能辅助SQL语句的使用，支持自然语言生成SQL、解释复杂SQL、优化SQL语句。

- 字段查询















```sql
key:#"abc def"
```

- 全文查询















```sql
#"abc def"
```


## 使用限制

- 短语查询的结果只支持向前、向后的连续翻页，不支持随机跳转。

- 执行短语查询后，日志分布直方图展示的是非短语查询的结果。

- 短语查询不支持搭配模糊查询。

- 短语查询语句中必须添加半角双引号（""）。

- 短语查询语句中不支持搭配not语句，即不支持`not #"abc def"`。

- 短语查询语句中不支持搭配分析语句，即不支持`#"abc" | select ***`。因此使用短语查询时，也不支持快速分析功能。


## 翻页说明

当您执行一次翻页操作时，日志服务会对应执行一次短语查询操作，用于保证查询结果的连续性。

短语查询每次最多查询10,000条日志，在翻页过程中，可能出现某页中显示的日志数量少于 **每页显示** 对应的数量，但仍支持向后翻页。即表示当前查询的10,000条日志中，满足短语查询条件的日志数量少于 **每页显示** 对应的数量。

例如日志总数为20,000条，每页支持显示100条，当您执行一次短语查询后，只返回89条且向后翻页功能可用，此时说明前10,000条日志中只有89条日志满足短语查询条件。您可以执行翻页操作，日志服务会自动在后10,000条日志中，执行第二次短语查询，并返回符合条件的日志。

![翻页说明](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6699414561/p446403.png)

## 示例

1. 例如您要查询包含`redo_index/1`的日志。


   - 使用非短语查询语句`"redo_index/1"`，日志服务将根据全文索引匹配部分关键词。![非短语查询](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8887147461/p416723.png)

   - 使用短语查询语句`#"redo_index/1"`，日志服务将匹配完整的短语`redo_index/1`。![短语查询](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8887147461/p416459.png)


2. 例如您要查询包含`02/Mar`的日志（ [调试](https://sls.aliyun.com/doc/playground/demo.html?dest=/lognext/project/nginx-demo-log/logsearch/nginx-access-log%3FslsRegion%3Dcn-shanghai%26isShare%3Dtrue%26queryString%3Drequest_time%20in%20%5B50%20100%5D)）。


   - 使用非短语查询语句time\_local: 02/Mar，日志服务将根据全文索引匹配部分关键词。

     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4773990471/p923129.png)

   - 使用短语查询语句`time_local: #"02/Mar"`，日志服务将匹配完整的短语`02/Mar`。

     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4773990471/p923130.png)