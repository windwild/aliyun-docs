### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[开发参考](https://help.aliyun.com/zh/sls/developer-reference/)[日志服务CLI](https://help.aliyun.com/zh/sls/developer-reference/cli-reference/)[使用CLI](https://help.aliyun.com/zh/sls/developer-reference/use-of-cli/)[Logstore管理](https://help.aliyun.com/zh/sls/developer-reference/logstore-management/)copy\_logstore

# copy\_logstore

更新时间：2026-01-05 02:56:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：list\_project](https://help.aliyun.com/zh/sls/developer-reference/list-project)[下一篇：create\_logstore](https://help.aliyun.com/zh/sls/developer-reference/create-logstore)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

复制说明

请求语法

请求参数

示例

调用CLI命令将源LogStore复制到目标LogStore。

## **复制说明**

该命令支持将日志服务的如下配置复制到其他日志库，不会将数据复制到其他日志库。

- 日志库

- 索引配置

- Logtail配置


## 请求语法

```shell
aliyunlog log copy_logstore --from_project=<value> --from_logstore=<value> --to_logstore=<value> [--to_project=<value>] [--to_client=<value>] [--to_region_endpoint=<value>] [--access-id=<value>] [--access-key=<value>] [--sts-token=<value>] [--region-endpoint=<value>] [--client-name=<value>] [--jmes-filter=<value>] [--format-output=<value>] [--decode-output=<value>]
```

## 请求参数

该命令的必选和特有参数描述如下。

| **参数名称** | **数值类型** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数名称** | **数值类型** | **是否必选** | **示例值** | **描述** |
| --from\_project | String | 是 | project-a | 源Project名称。 |
| --from\_logstore | String | 是 | logstore-a | 源LogStore名称。 |
| --to\_logstore | String | 是 | logstore-b | 目标LogStore名称。 |
| --to\_project | String | 否 | project-b | 目标Project名称。 |
| --to\_client | String | 否 | test | 拥有操作目标Project的账号信息。如何配置该账号信息，请参见 [配置CLI](https://help.aliyun.com/zh/sls/developer-reference/configure-log-service-cli#task-2085812 "")。 |

关于该命令的全局参数，请参见 [全局参数](https://help.aliyun.com/zh/sls/developer-reference/global-parameters#concept-2083388 "")。

## 示例

- 请求示例



将默认账号下的源logstore-a复制到test账号的logstore-b。

















```plaintext
aliyunlog log copy_logstore --from_project="project-a" --from_logstore="logstore-a" --to_logstore="logstore-b" --to_project="project-b " --to_client="test"
```

- 返回示例

命令执行成功后，无响应消息。