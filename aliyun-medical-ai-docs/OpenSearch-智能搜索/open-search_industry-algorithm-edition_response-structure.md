### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)OpenApi 响应结构

# OpenApi 响应结构

更新时间：2023-12-25 22:19:46

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：统计报表指标释义](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/metrics-in-statistical-reports)[下一篇：错误码定义](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/error-codes-2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

正确返回

错误返回

## 正确返回

**示例**

```json
{
    "requestId": "D77D0DAF-790D-F5F5-A9C0-133738165014",
    "result": （Array|Object） // 返回数据
}
```

**结构**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| requestId | String | 请求ID |
| result | Array/Object | 返回数据 |

## 错误返回

**示例**

```json
{
    "requestId": "BD1EA715-DF6F-06C2-004C-C1FA0D3A9820",
  "httpCode": 404,
    "code": "App.NotFound",
    "message": "App not found"
}
```

**结构**

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| requestId | String | 请求ID |
| httpCode | Integer | 响应码 |
| code | String | 错误代码 |
| message | String | 错误信息 |

参考： [错误码定义](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/error-codes-2)