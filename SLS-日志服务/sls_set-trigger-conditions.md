### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据监控](https://help.aliyun.com/zh/sls/data-monitoring/)[告警](https://help.aliyun.com/zh/sls/sls-alerting/)设置触发条件

# 设置触发条件

更新时间：2024-12-24 02:11:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：设置分组评估](https://help.aliyun.com/zh/sls/use-the-group-evaluation-feature)[下一篇：设置评估表达式](https://help.aliyun.com/zh/sls/syntax-of-evaluate-expressions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概览

配置触发条件

相关文档

日志服务支持您在配置触发告警的条件时使用评估表达式。例如您配置 **触发条件** 为 **有数据匹配** 和评估表达式，则表示查询和分析结果中存在数据满足评估表达式就触发告警。

## **概览**

您查询语句的执行结果将作为输入，集合操作结果的字段作为变量，当评估表达式条件为真，则触发告警。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6824205371/CAEQSBiBgMDFmuyWhRkiIGE4Y2JkNTk0YzUzNDRkNTRiM2YxMjE4N2Q0ZTRlNTMz4524787_20240711175152.248.svg)

## 配置触发条件

告警监控规则在评估集合操作结果时，如果集合操作结果满足触发条件，则表示评估通过，生成一条告警。触发条件包括如下选项：

- **有数据**：对集合操作结果中的数据条数进行判断，只要有1条数据，就满足触发条件。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9130371271/p820490.png)

- **有特定条数据**：对集合操作结果中的数据条数进行判断，支持的运算符包括大于、小于、等于等。当数据条数满足特定条数据时，满足触发条件。例如集合操作结果中有4条数据，触发条件为 **有特定条数据>10条**，则表示集合操作结果未满足触发条件，不会生成告警。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9130371271/p820496.png)

- **有数据匹配**：对集合操作结果中的数据内容进行判断，只要有1条数据的内容匹配评估表达式，就满足触发条件。例如集合操作结果为1条数据（pv=900），触发条件为 **有数据匹配，pv > 1000**，则表示集合操作结果未满足触发条件，不会生成告警。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9130371271/p820493.png)

- **有特定条数据匹配**：对集合操作结果中的数据条数和数据内容进行判断。当有特定条数据的内容匹配评估表达式时，才会触发告警。例如集合操作结果中有4条数据（pv=900、pv=1100、pv=1200、pv=1001），触发条件为 **有特定条数据>3条，pv > 1000**，则表示集合操作结果满足触发条件，生成告警。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9130371271/p820494.png)


## 相关文档

- [设置评估表达式](https://help.aliyun.com/zh/sls/syntax-of-evaluate-expressions "")

- [设置告警严重度](https://help.aliyun.com/zh/sls/specify-severity-levels-for-alerts "")

- [配置告警写入事件库的权限](https://help.aliyun.com/zh/sls/configure-permissions-for-writing-alarms-to-the-event-library "")