### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)ABTestGroup

# ABTestGroup

更新时间：2023-12-21 21:29:29

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ABTestExperiment](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/abtestexperiment)[下一篇：Model](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/model)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

## 描述

ABTest实验组。

## 示例

```json
{
    "id": "13466",
    "name": "Group_2020-5-7_15:23:3",
    "status": 1,
    "created": 1588839490,
    "updated": 1588839490
}
```

## 结构

| 名称 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 名称 | 类型 | 描述 |
| id | String | 组ID |
| name | String | 组别名 |
| status | Integer | 状态\- 0 未生效- 1 生效 |
| created | Integer | 创建时间 |
| updated | Integer | 最后修改时间 |