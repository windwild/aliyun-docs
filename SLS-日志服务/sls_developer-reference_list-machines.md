### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[开发参考](https://help.aliyun.com/zh/sls/developer-reference/)[日志服务CLI](https://help.aliyun.com/zh/sls/developer-reference/cli-reference/)[使用CLI](https://help.aliyun.com/zh/sls/developer-reference/use-of-cli/)[Logtail机器组管理](https://help.aliyun.com/zh/sls/developer-reference/machine-group-management/)list\_machines

# list\_machines

更新时间：2024-08-28 06:21:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：list\_machine\_group](https://help.aliyun.com/zh/sls/developer-reference/list-machine-group)[下一篇：update\_machine\_group](https://help.aliyun.com/zh/sls/developer-reference/update-machine-group)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

请求语法

请求参数

示例

错误码

API参考

调用CLI命令查询指定机器组中的机器信息。

## 请求语法

```shell
aliyunlog log list_machines --project_name=<value> --group_name=<value> [--offset=<value>] [--size=<value>] [--access-id=<value>] [--access-key=<value>] [--sts-token=<value>] [--region-endpoint=<value>] [--client-name=<value>] [--jmes-filter=<value>] [--format-output=<value>] [--decode-output=<value>]
```

## 请求参数

该命令的必选和特有参数描述如下。

| **参数名称** | **数值类型** | **是否必选** | **示例值** | **描述** |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **参数名称** | **数值类型** | **是否必选** | **示例值** | **描述** |
| --project\_name | String | 是 | aliyun-test-project | Project名称。 |
| --group\_name | String | 是 | test-group | 机器组名称。 |
| --offset | Integer | 否 | 0 | 指定从某一行开始读取查询结果。默认值为0。 |
| --size | Integer | 否 | 5 | 分页查询时，设置的每页行数。最大值为500。 |

关于该命令的全局参数，请参见 [全局参数](https://help.aliyun.com/zh/sls/developer-reference/global-parameters#concept-2083388 "")。

## 示例

- 请求示例



查询默认账号下机器组test-group的机器信息。

















```shell
aliyunlog log list_machines --project_name="aliyun-test-project" --group_name="test-group" --offset=0 --size=5
```

- 返回示例















```json
{
    "count": 1,
    "machines": [\
      {\
        "binary": "1.8.7",\
        "ip": "203.0.*.*",\
        "lastHeartbeatTime": 1622106889,\
        "machine-uniqueid": "26964724-6767-443c-a5fc-5d7b8e4fd06c",\
        "userdefined-id": ""\
      }\
    ],
    "total": 1
}
```


## 错误码

如果返回报错信息，请参见具体接口的错误码处理。更多信息，请参见 [错误码](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-listmachines#api-detail-45 "")。

## API参考

[ListMachines](https://help.aliyun.com/zh/sls/developer-reference/api-sls-2020-12-30-listmachines "")