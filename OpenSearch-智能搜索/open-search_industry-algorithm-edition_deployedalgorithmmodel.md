### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)DeployedAlgorithmModel

# DeployedAlgorithmModel

更新时间：2023-12-22 06:19:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：DeployedAlgorithm](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/deployedalgorithm)[下一篇：DataCollection](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/datacollection)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

## 描述

OpenSearch 应用部署成功的算法模型。

## 示例

```json
{
    "modelName": "popV2",
    "modelId": 363,
    "progress": 100,
    "status": "IN_SERVICE",
    "projectId": 1747,
    "algorithmType": "POP"
}
```

## 结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| modelName | String | 模型名称 |
| modelId | Integer | 模型ID |
| progress | Integer | 预测进度，百分比 |
| status | String | 部署状态参考： [DeployedAlgorithm](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/deployedalgorithm) 的 status |
| projectId | Integer | 算法工程ID |
| algorithmType | String | 算法类型\- POP 人气模型- CP 类目预测 |