### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-召回引擎版](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/)[召回引擎传统版（停售）](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/recall-engine-legacy-edition/)实例管理

# 实例详情

更新时间：2025-03-07 04:20:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：OpenSearch-召回引擎版服务关联角色](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/opensearch-recall-engine-version-service-association-role)[下一篇：运维管理](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/operation-and-maintenance-management/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

列表页介绍

基本信息

网络信息

API入口

集群信息

## 列表页介绍

![image..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675364.png)

实例管理页面展示用户所购买的所有实例，并且可在列表中操作栏进行相应操作：

- 管理，默认跳转到实例的详情页；

- [查询测试](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/recall-engine-tradition-query-test "")，可对线上正在提供服务的实例进行简单的搜索测试；

- [扩缩容](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/purchase-opensearch-recall-engine-instance#h2-p71-027-hn7 "")，可对实例进行使用资源的调整；


## 基本信息

在召回引擎版--->实例管理页面，找到对应实例，点击右侧操作栏中的“管理”，进入实例详情页面：

![image..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675365.png)

| **实例列表名称** | **含义** |
| --- | --- |

|     |     |
| --- | --- |
| **实例列表名称** | **含义** |
| 实例名称/实例ID | 用户实例的名称，默认实例名称为实例ID，同一用户的实例名称可以重复/用户购买应用完成后自动生成的实例ID |
| 实例状态 | 当前实例的售卖状态，包含正常、已冻结（按量付费欠费） |
| 创建时间 | 用户创建实例时的时间 |
| 计费类型 | 按量付费 |
| 查询节点数 | 用户购买的查询节点的数量 |
| 查询节点规格 | 用户购买的查询节点的规格 |
| 数据节点数 | 用户购买的数据节点的数量 |
| 数据节点规格 | 用户购买的数据节点的规格 |
| 地域 | 用户购买实例所处位置 |
| 实例描述 | 用户对当前实例的补充描述 |

## 网络信息

**专有网络**、 **虚拟交换机ID、公网访问**：用户在售卖页选择的用于实例访问的同区域的专有网络、虚拟交换机和公网访问详情如下图所示：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1542320861/p613794.png)

**添加公网访问白名单**，公网访问默认是关闭状态，如下图：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675361.png)

用户可手动打开，打开后会展示白名单配置入口：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675362.png)

点击【公网访问白名单】可对白名单内容进行增删编辑，编辑状态下未保存退出界面需要进行二次确认，退出后编辑内容不会保存。

**添加白名单：** 手动填入IP地址，多个IP使用逗号分隔，如图：![image.png](<Base64-Image-Removed>)

**验证白名单添加成功**：可以登录已添加白名单的机器上，通过ping API入口的API域名，以下添加本机IP为例： 添加本机IP`30.197.xxx.xxx`：![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675358.png)

API入口获取域名，点击`API域名`复制，

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675360.png)

域名需要添加 **public** 才可进行访问`ha-cn-5yd35gift03.public.ha.aliyuncs.com`，

本机通过ping API域名，ping通说明白名单添加成功，如图：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675359.png)

## API入口

又称Endpoint（同区域（含VPC）环境下的ECS可用）。 每个地域的API域名不同，使用API或者SDK访问OpenSearch的时候需要根据此处给出的API入口进行访问。请根据实际部署情况选择合适的域名，使用前请先ping下，确定可访问。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5500025661/p499341.png)

**用户名、密码**：用户在售卖页输入的用于实例访问的用户名、密码，点击 **已设置** 按钮，可以修改当前实例对应的用户名、密码详情如下图所示：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5500025661/p499342.png)

**修改密码相关限制：**

- 用户名：长度为0-30字符，可包含大小写字母、下划线和数字，字母开头

- 密码：小写字母、数字组成，长度为6~8位；


PS: 仅支持在「网络信息-专有网络」中使用，如需公网API域名，请联系我们。

- [文档搜索 Demo](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/document-search-demo-4 "")；

- [数据推送 Demo](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/data-push-demo-4 "")；


## 集群信息

**集群信息** 展示各个集群的 **查询节点**、 **数据节点** 的状态信息，点击各个集群名称，可分别展示不同集群的状态信息，详情如下图所示：

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5500025661/p499340.png)

查询节点状态信息包含：

**服务状态**：服务中或服务更新中。

**配置状态**：配置完成或配置更新中。

数据节点状态信息包含：

**服务状态**：服务中或服务更新中。

**配置状态**：配置完成或配置更新中。

**数据状态**：需展示每个索引表对应的数据状态，包含索引表、数据状态、索引版本、全量切换时间、增量更新时间字段。

![image..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675366.png)

**集群数据状态**：如果存在数据异常的索引表，则为数据异常（会展示具体的异常详情）；如果存在数据更新中的索引表，则为数据更新中，进度为所有索引表进度的平均值；如果索引表状态都为正常，则为正常。

![image..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675367.png)

**索引表详情如下图所示：**

![image..png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2728805861/p675368.png)

**索引表相关名词解释：**

- 索引表：集群中包含的索引表名。

- 数据状态：包含正常、数据更新中（需展示进度）、数据异常（需展示具体的异常详情）。

- 索引表大小：索引表占用的存储大小。

- 索引版本：索引表正在使用的索引版本。

- 全量切换时间：索引表的最后一次全量切换时间。

- 增量更新时间：索引表的最后一次增量更新时间。


[**运维管理**](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/operation-and-maintenance-management/)：召回引擎版为用户提供了自主运维集群的功能，包括部署新集群、更新在线资源，修改离线索引配置等需要推送配置的操作的一键推送配置、手动索引重建、历史版本回滚的功能。

[部署管理](https://help.aliyun.com/zh/open-search/retrieval-engine-edition/deployment-management/ "")：部署管理页面可查看用户当前实例的集群拓扑，并做一些变更在线配置。