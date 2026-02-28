### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[操作指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/operation-guide/)[功能扩展](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/industry-feature-extensions-1/)数据采集2.0

# 数据采集2.0

更新时间：2025-03-27 04:39:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：搜索测试](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/run-search-tests)[下一篇：数据采集2.0 SDK](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdks-for-data-collection-2-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

行为数据上报给用户带来什么好处？

注意事项

上报行为数据

查看数据报告

## 行为数据上报给用户带来什么好处？

- 可以了解终端用户对搜索结果的反应（浏览、点击、停留、点赞、分享、收藏、购买等行为），从而为优化搜索效果提供指引方向。

- 可以在搜索应用的数据统计功能中，看到为该应用统计的各种搜索报表（如PV, IPV, CTR等），为用户的运营工作带来帮助。

- 通过开放搜索为用户提供的算法平台，可以将这些搜索行为反馈数据应用在搜索排序算法模型训练中，不断地提升搜索效果。


## 注意事项

- 数据采集功能会在实例应用创建完成后自动开通

- 数据，目前主要指终端用户对搜索结果的行为反馈数据

- 采集， **目前主要指通过开放搜索SDK上报搜索行为数据（Server端），App端、Web暂不支持**，敬请期待

- **数据采集2.0相较于老的数据采集功能，在传参上更简单更便于理解，SDK使用上也更便捷。新用户如果有需求，请直接使用此文档中的行为数据上报字段进行传参。**（ **注**：以及支持数据采集2.0功能。）


## 上报行为数据

**说明**：用户在开放搜索控制台开通行为采集功能之后，建议通过SDK手动上传行为数据。下文详细介绍了行为数据包含的字段类型与含义。 **步骤**：

1. **SDK上报有8个必须字段**：imei 或 user\_id（注：二者不能同时为空）、biz\_id、trace\_id、rn、bhv\_type、bhv\_time、item\_id、item\_type

2. **API上报**： 除了上面的必须字段之外，外加1个reach\_time

3. SDK/API上报行为数据demo可 [点击此处](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdks-for-data-collection-2-0) 进行查看。


**行为数据字段定义**

| ID | 字段名 | 字段类型 | 字段含义 | 字段值 | 是否必须 |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| ID | 字段名 | 字段类型 | 字段含义 | 字段值 | 是否必须 |
| 1 | app\_version | STRING | 业务侧网站或移动APP的版本号 |  | 非必须 |
| 2 | sdk\_type | STRING | 数据上报使用的SDK类型。该字段是开放搜索为了区分服务端上报和移动端采集的SDK而设置的 |  | 非必须如果是通过开放搜索SDK做上报，会默认设置该值为”opensearch\_sdk” |
| 3 | sdk\_version | STRING | 数据上报使用的SDK版本号 |  | 非必须如果是通过开放搜索SDK做上报，会默认设置该值 |
| 4 | login | STRING | 终端用户在业务侧网站或移动APP上是否是登录状态 | 取值为0或1。含义为：0（未登录）， 1（登录） | 非必须 |
| 5 | user\_id | STRING | 用于唯一标识终端用户的一个ID。 |  | 非必须但 **imei,user\_id不能同时为空** |
| 6 | imei | STRING | 终端用户设备ID（值可以为：imei,device\_id,idfa） |  | 非必须但 **imei,user\_id不能同时为空** |
| 7 | biz\_id | STRING | 业务侧用于区分不同业务的一个数值ID。一般是搜索入口，例如有Web端和ios，安卓，就可以分多个biz\_id，后续可以通过biz\_id来切分流量统计或做实验 | 如果用户没有分业务场景，就建议填一个default；如果有区分业务场景，就可以填pc, ios, android等 | 必须 |
| 8 | trace\_id | STRING | 用于区分行为针对的doc是来自哪个搜索服务商输出的结果 | 如果是来自开放搜索的结果，该字段值设置为 **Alibaba**，如果是来自其他服务商的结果，业务侧可以自己取名字 | 必须 |
| 9 | trace\_info | STRING | 该值来自开放搜索在搜索结果中返回ops\_request\_misc的值，原样回传即可 |  | 非必须<br>注：trace\_id为Alibaba时必须要回传，内部用于核对是由开放搜索输出的结果 |
| 10 | rn | STRING | 用于标识一个搜索pv。 该值来自开放搜索在搜索结果中返回的request\_id的值，原样回传即可。 |  | 必须 |
| 11 | item\_id | STRING | doc的主键值。 该值为开放搜索应用中主表主键值 |  | 必须 |
| 12 | item\_type | STRING | doc的业务类型 | 可设置的值见下文【 **关于item\_type定义**】 | 必须 |
| 13 | bhv\_type | STRING | 行为类型，例如曝光、停留、浏览、收藏、下载等 | 可设置的值见下文【 **常用行为类型**】 | 必须 |
| 14 | bhv\_value | STRING | 行为数量，例如停留时长，购买件数等 | 可设置的值见下文【 **常用行为类型**】 | 非必须 |
| 15 | bhv\_time | STRING | 行为发生的时间戳，单位s |  | **必须** |
| 16 | bhv\_detail | STRING | 对行为的一些详细描述。 | 格式：key=value{,key=value} 表示可以是1个或多个key=value对 | 非必须 |
| 17 | ip | STRING | 行为发生的手机或终端的ip |  | 非必须建议设置 |
| 18 | longitude | STRING | 行为发生位置的经度 |  | 非必须建议设置 |
| 19 | latitude | STRING | 行为发生位置的纬度 |  | 非必须建议设置 |
| 20 | session\_id | STRING | 用户的一次会话id |  | 非必须建议设置 |
| 21 | spm | STRING | 提供给业务用来跟踪行为所在的页面模块的位置 | 编码格式为a.b.c.d, 分别代表站点ID，页面ID, 模块ID, 位置ID。 | 非必须 |
| 22 | report\_src | STRING | 用于区分上报来源 | 取值为1,2,3,patch\_data。含义：<br>- 1（通过开放搜索SDK上报），<br>  <br>- 2（通过移动端SDK采集），<br>  <br>- 3（通过开放搜索API上报）<br>  <br>- patch\_data（用户有历史数据或其他渠道的数据需要同步时上报） | 非必须 |
| 23 | mac | STRING | 手机或终端设备的网卡MAC地址 |  | 非必须 |
| 24 | brand | STRING | 手机或终端的品牌 |  | 非必须建议设置 |
| 25 | device\_model | STRING | 手机或终端的机型 |  | 非必须 |
| 26 | resolution | STRING | 手机或终端的屏幕分辨率 |  | 非必须 |
| 27 | carrier | STRING | 手机或终端的移动运营商 |  | 非必须 |
| 28 | access | STRING | 手机或终端连接的网络 |  | 非必须 |
| 29 | access\_subtype | STRING | 手机或终端连接的网络类型 |  | 非必须 |
| 30 | os | STRING | 手机或终端的操作系统 |  | 非必须 |
| 31 | os\_version | STRING | 手机或终端操作系统的版本 |  | 非必须 |
| 32 | language | STRING | 手机或终端设置的语言类型 |  | 非必须 |
| 33 | phone\_md5 | STRING | 用户手机号的md5值 |  | 非必须 |
| 34 | reserve1 | STRING | 预留字段 |  | 非必须 |
| 35 | reserve2 | STRING | 预留字段，当report\_src='patch\_data'时，reserve2须填写raw\_query对应值（必填） |  | 非必须 |
| 36 | reach\_time | BIGINT | 该数据到达服务端的时间，格式：时间戳，单位：秒。 |  | 必须，如果是通过开放搜索SDK做上报，SDK会自动设置, 如果是通过开放搜索API做上报，需要设置 |

**关于item\_type定义**

| ID | item\_type | 业务含义 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| ID | item\_type | 业务含义 |
| 1 | goods | 物品、商品 |
| 2 | article | 文章、博客、小说 |
| 3 | ask | 问答 |
| 4 | bbs | 论坛帖子 |
| 5 | download | 下载 |
| 6 | image | 图片 |
| 7 | media | 多媒体（包括电影、电视、音乐等） |
| 8 | recipe | 美食、菜谱 |
| 9 | news | 新闻资讯 |
| 10 | institution | 组织机构 |
| 11 | other | 其他 |

**常用行为类型**

| ID | bhv\_type | 含义 | bhv\_value | bhv\_detail |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| ID | bhv\_type | 含义 | bhv\_value | bhv\_detail |
| 1 | expose | 曝光 | 置空 | 置空 |
| 2 | stay | 停留 | 停留时长（单位秒） | 置空 |
| 3 | click | 点击 | 点击次数。默认值： 1 | 置空 |
| 4 | cart | 加入购物车，加入书架，加入歌单 | 置空 | 置空 |
| 5 | buy | 购买 | 购买件数。默认值： 1 | 例：buy\_price=12,price\_unit=RMB<br>- buy\_price表示购买（即：下单）时候的物品价格, 默认<br>  <br>- price\_unit（价格单位）是RMB |
| 6 | collect | 收藏 | 置空 | 置空 |
| 7 | like | 点赞 | 点赞次数默认值：1 | 置空 |
| 8 | dislike | 点衰 | 点衰次数默认值：1 | 置空 |
| 9 | comment | 评论 | 评论次数默认值：1 | 置空 |
| 10 | share | 分享、转发 | 分享/转发次数默认值：1 | 置空 |
| 11 | subscribe | 关注、订阅 | 置空 | 置空 |
| 12 | gift | 送礼物 | 置空 | 置空 |
| 13 | download | 下载 | 置空 | 置空 |
| 14 | read | 阅读 | 置空 | 置空 |
| 15 | tip | 打赏 | 置空 | 置空 |
| 16 | complain | 投诉 | 置空 | 置空 |

## 查看数据报告

当数据采集服务开通后，并上传了一定量的行为数据，可在数据采集页中查看数据状态和数据质量：

![验证报告](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4141746161/p248487.jpg)

**数据状态**

数据状态分为“正常，可用”和“异常，不可用”，正常是指数据质量部分无任何报错，即所有校验皆通过，如果有报错则是“异常，不可用”；

**当数据状态为“异常，不可用”时，可能会影响人气模型、类目预测的创建与训练**。

**数据异常状态**：

![5](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635314161/p209723.png)

**数据正常状态**：

![6](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635314161/p209724.png)

**数据质量**

数据质量验证用于输出后台校验项有错误时，控制台会显示对应的错误信息，但校验项没有错误时不在控制台显示：![7](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1635314161/p209725.png) **注意**：上图抽样检查的数据是每整点抽样展示前一个小时用户同步过来的行为数据。