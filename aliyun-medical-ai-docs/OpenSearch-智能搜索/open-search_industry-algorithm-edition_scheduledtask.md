### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)ScheduledTask

# ScheduledTask

更新时间：2023-12-22 06:19:58

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Summary](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/summary)[下一篇：ScheduledTask 定时规则](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cron-field-in-scheduledtask)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

## 描述

opensearch 应用的定时索引重建任务

## 示例

```json
{
    "id": "cfd5ebe9-bcdd-11ea-a58d-98039b07e4ec",
    "progress": 0,
    "status": 3,
    "lastRanTimestamp": null,
    "type": "wipe",
    "running": false,
    "paused": false,
    "finished": false,
    "idle": true,
    "created": 1593747144,
    "updated": 1593747144,
    "cron": "0 0 * * 1,2,3,4,5,6,7",
    "enabled": true,
  "appId": null,
  "appGroupId": "100303899",
  "ownerId": "84",
    "lastScheduledTimestamp": null,
    "forkedAppId": "",
  "appGroup": {
    "id": "100303899"
  },
  "owner": {
    "id": "84"
  },
    "filter": {
        "field": "title",
        "days": 30,
        "unit": "s"
    }
}
```

## 结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| id | String | 任务ID |
| progress | Integer | 任务运行进度 |
| status | Integer | 任务状态\- 0 运行中- 1 暂停- 2 完成- 3 空闲 |
| lastRanTimestamp | Integer/null | 最近运行时间戳 |
| type | String | 定时任务类型\- wipe 数据清理- fork 导入数据加索引重建 -reindex 索引重建 - clear 清空数据 |
| running | Boolean | 是否在运行中 |
| paused | Boolean | 是否暂停 |
| finished | Boolean | 是否完成 |
| idle | Boolean | 是否空闲 |
| cron | String | 定时配置参考： [ScheduledTask 定时规则](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cron-field-in-scheduledtask) |
| enabled | Boolean | 是否开启定时任务 |
| appId | String | 版本ID |
| appGroupId | String | 应用ID |
| ownerId | String | 用户ID |
| lastScheduledTimestamp | Integer/null | 最近调度时间戳 |
| forkedAppId | String | 来源版本ID |
| appGroup.id | String | 应用ID |
| owner.id | String | 用户ID |
| filter | Object | 数据清理条件 |
| filter.days | Integer | 过期天数获取范围：\[7-180\] |
| filter.unit | String | 过期时间单位\- s 秒- ms 毫秒 |
| filter.field | String | 过期字段 |