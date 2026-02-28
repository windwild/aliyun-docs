### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)AppGroup

# AppGroup

更新时间：2023-12-25 22:19:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：错误码定义](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/error-codes-2)[下一篇：App](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/app)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

## 描述

应用的数据结构

## 示例

```json
{
    "id": "100302881",
    "name": "lsh_test_1",
    "currentVersion": "100302903",
    "switchedTime": 1590486386,
    "quota": {
        "docSize": 1,
        "computeResource": 20,
        "spec": "opensearch.share.common"
    },
    "chargingWay": 1,
    "type": "enhanced",
    "versions": [\
        "100302903",\
        "100303063"\
    ],
    "projectId": "",
    "chargeType": "POSTPAY",
    "expireOn": "",
    "instanceId": "",
    "commodityCode": "opensearch",
    "processingOrderId": "",
    "firstRankAlgoDeploymentId": 0,
    "secondRankAlgoDeploymentId": 0,
    "pendingSecondRankAlgoDeploymentId": 0,
    "description": "",
    "produced": 1,
    "lockedByExpiration": 0,
    "hasPendingQuotaReviewTask": 0,
    "created": 1590139542,
    "updated": 1590978265,
    "status": "normal",
    "lockMode": "Unlock"
}
```

## 结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| id | String | 应用ID |
| name | String | 应用名称 |
| currentVersion | String | 当前在线版本 |
| switchedTime | Integer | 在线版本切换时间戳 |
| quota | Object | 应用配额信息参考： [Quota](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/quota) |
| chargingWay | Integer | 计费类型- 1：计算资源- 2：qps |
| type | String | 应用类型- standard 标准版- advance 老高级版（新应用不支持此类型）- enhanced 新高级版 |
| versions | Array | 版本集合 |
| projectId | String | abtest project 名称 |
| chargeType | String | 付费类型- POSTPAY 后付费（按量付费）- PREPAY 预付费（包年包月） |
| expireOn | String | 过期时间（格式："yyyy-mm-dd hh:mm:ss"） |
| instanceId | String | 实例ID |
| commodityCode | String | 商品CODE |
| processingOrderId | String | 未结束订单号 |
| firstRankAlgoDeploymentId | Integer | 粗排部署ID |
| secondRankAlgoDeploymentId | Integer | 精排部署ID |
| pendingSecondRankAlgoDeploymentId | Integer | 部署中的精排部署ID |
| description | String | 应用描述 |
| produced | Integer | 是否生产完成- 0：生产中- 1：生产完成 |
| hasPendingQuotaReviewTask | Integer | 是否配额审批中- 0：正常- 1：配额审批中 |
| created | Integer | 创建时间戳 |
| updated | Integer | 更新时间戳 |
| status | String | 应用状态- producing 生产中- review\_pending 生产审批中- config\_pending 待配置- normal 正常- frozen 已冻结 |
| lockMode | String | 锁定状态- Unlock 正常- LockByExpiration 实例过期自动锁定- ManualLock 手动触发锁定 |