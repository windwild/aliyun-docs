### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[管控API参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/management-api-reference/)[数据结构](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/data-structures/)Model

# Model

更新时间：2023-12-22 06:19:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：ABTestGroup](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/abtestgroup)[下一篇：ModelErrorCode](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/modelerrorcode)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

描述

示例

结构

## 描述

opensearch 应用算法模型

## 示例

```json
{
    "id": 113023,
    "groupId": "100297752",
    "groupName": "appGroupName",
    "type": "pop",
    "name": "pop_1212",
    "trainTarget": "ctr",
    "cron": "15 0 */2 * *",
    "cronEnabled": true,
    "behaviorEnabled": true,
    "behaviorFromGroupName": "DemoModelName",
    "lastTrainingTime": 1543233439000,
    "auc": 0.85,
    "status": "train_success",
    "progress": 69,
    "isAlreadyDeployed": true,
    "industry": "general",
    "filter": "user_id=1,level=1",
    "fields": [{\
            "name": "item_title",\
      "appFieldType": "title"\
        },\
        {\
            "name": "item_content"\
        },\
        {\
            "name": "item_title_keep",\
            "processType": "reserve"\
        }\
    ],
    "extend": {
        "useHotQuery": true,
        "useHistoryQuery": true
    }
}
```

## 结构

| 字段 | 类型 | 描述 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 字段 | 类型 | 描述 |
| id | Integer | 模型ID |
| groupId | String | 应用ID |
| groupName | String | 应用名称 |
| type | String | 算法类型\- pop 人气模型- cp 类目预测- hot 热词- hint 底纹- suggest 下拉提示 |
| name | String | 模型名称命名规则：/^(?!ops\_)\[a-zA-Z\]\\w{0,29}$/ |
| industry | String | 行业\- general 通用- ecommerce 电商- content 内容 |
| trainTarget | String | 模型的训练目标\- click 点击- buy 购买- cart 加入购物车- collect 收藏- like 点赞- comment 评论- share 分享- subscribe 关注- gift 礼物- download 下载- read 阅读- tip 打赏 |
| behaviorEnabled | Boolean | 是否使用行为数据默认 true，部分模型支持不使用行为数据 |
| behaviorFromGroupName | String | 使用另一个应用的行为数据源默认使用当前应用的行为数据 |
| cron | String | 定时训练的cron表达式参考：Linux crontab定时规则 |
| cronEnabled | Boolean | 是否启用定时训练默认 true |
| availableThreshold | Float | 模型是否可用的阈值取值范围：\[0-1\] |
| filter | String | 导数据的过滤条件目前支持的条件有<, >, =, !=, >=, <=，多个条件用’,’分隔 |
| fields\[\] | Object | 字段列表 |
| fields\[\].name | String | 字段名 |
| fields\[\].appFieldType | String | 该字段在app中的角色\- pk 主键- cate\_id 类目id- title 标题- cate\_name 类目名称- normal 普通字段 |
| fields\[\].processType | String | 对字段的处理类型\- reserve 原值保留- normal 普通 |
| lastTrainingTime | Integer | 上次任务完成时间 |
| lastModifyTime | Integer | 上次修改配置时间 |
| auc | Float | 模型的auc值 |
| status | String | 任务的执行状态\- train\_init 待训练- train\_pending 训练中- validate\_failed 数据异常- train\_failed 训练失败- train\_bad\_model 已训练未通过- train\_success 训练成功 |
| progress | Integer | 任务执行过程中的百分比进度 |
| isAlreadyDeployed | Boolean | 是否曾部署成功过，相同配置已有可用模型 |
| extend | Object | 模型的扩展配置 |
| extend.useHotQuery | Boolean | 是否使用热搜词支持的模型类型：suggest |
| extend.useHistoryQuery | Boolean | 是否使用搜索历史支持的模型类型：suggest |