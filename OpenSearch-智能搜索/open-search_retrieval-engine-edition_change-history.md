### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-召回引擎版](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/)[召回引擎传统版（停售）](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/recall-engine-legacy-edition/)[实例管理](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/instance-management/)[运维中心](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/operation-and-maintenance-center/)历史变更

# 历史变更

更新时间：2024-03-13 05:15:30

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：集群灰度切换](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/cluster-grayscale-switching)[下一篇：配置中心](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/recall-engine-tradition-configuration-center/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

常见变更进度查看

索引重建

变更说明

在召回引擎版实例管理页中，单击页面左侧菜单栏变更历史可以查看每一次运维操作的变更记录：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778129.png)

## 常见变更进度查看

### 索引重建

在索引重建流程中点击查看构建进度可查看索引数据处理的相应指标：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778136.png)

## 变更说明

| **变更范围** | **变更类型** | **允许重复触发** | **流程说明** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **变更范围** | **变更类型** | **允许重复触发** | **流程说明** |
| 索引表 | 新增索引表 | 是 | 新增数据源部署 -> 新增索引 -> 手动触发全量 -\> 订阅/取消订阅索引表<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778128.png) |
| 修改索引表 | 是 | 推送离线配置 -\> 手动触发全量<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9231230171/p778130.png) |
| 表的索引重建 | 是 | 手动触发全量<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778134.png) |
| 配置更新 | 是 | 推送离线配置 -\> 手动触发全量<br>![image.png](<Base64-Image-Removed>) |
| 从索引恢复数据 | 是 | 索引中恢复FSM<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778127.png) |
| 快速扩缩分片 | 是 | 快速扩缩列<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778125.png) |
| 实例操作 | 扩/缩容资源 | 是 | 在线资源<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778135.png) |
| 暂停开关 | 是 | 修改暂停策略<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8231230171/p778126.png) |
| 添加集群 | 是 | 新增在线部署<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9231230171/p778131.png) |
| 激活实例 | 购买实例后首次配置 | 否 | 激活服务 -> 新增在线部署 -\> 绑定配置到在线集群<br>![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9231230171/p778133.png) |