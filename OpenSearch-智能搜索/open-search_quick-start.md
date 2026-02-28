### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 快速入门（工具）

# 快速入门（工具）

更新时间：2022-12-19 01:06:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：动态与公告](https://help.aliyun.com/zh/open-search/announcements-and-updates)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

环境准备

测试数据

查询示例

## 环境准备

```sql
cd /ha3_develop
git clone http://gitlab.alibaba-inc.com/isearch/ha3_manual_example.git
cd ha3_manual_example/sql
```

```sql
sh build.sh
```

```sql
sh stop.sh
sh start_search.sh
```

注：单机上（即使不同用户在不同的docker中）同时运行多个`ha3_manual_example` 实例时，可能遇到端口冲突导致启动失败的情况。可以编辑以下两个文件，修改其中的端口号再次尝试：

- `start_search.sh`

：修改qrs侦听端口号

- `search.sh`

：修改请求qrs用端口号，注意和上述端口号对应


## 测试数据

`ha3_manual_example` 项目一共提供了以下数据表：

- `phone`

：记录了电商场景中主流品牌的手机信息

- `goods`

（主表）：记录了本地生活场景中外卖的商品信息

- `goods.sub_goods`

（子表）：配合

`goods`

表使用，用于描述外卖商品的规格信息

- `store`

（主表）：记录了本地生活场景中外卖的店铺信息

- `store.sub_store`

（子表）：配合

`store`

表使用，用于描述外卖店铺的配送方案


实际的schema配置位于`ha3_manual_example/sql/config/offline/0/schemas` 中，用于索引的构建；online阶段的schema，会在启动前自动从该处复制

|     |     |
| --- | --- |
| 手机信息表 `phone` |
| 字段名 | 内容 |
| nid | 商品id |
| title | 商品标题 |
| price | 商品价格 |
| brand | 品牌 |
| size | 整机尺寸 |
| color | 颜色 |
| multi\_field\_str | 测试用多值字段，类型 `STRING` |
| multi\_field\_int32 | 测试用多值字段，类型 `INT32` |
| multi\_field\_double | 测试用多值字段，类型 `DOUBLE` |

|     |     |
| --- | --- |
| 商品主表 `goods` |
| 字段名 | 内容 |
| pid | 产品id |
| title | 商品标题 |
| store\_id | 店铺id |
| detail | 商品详情 |

|     |     |
| --- | --- |
| 商品子表 `goods.sub_goods` （详细规格和价格） |
| 字段名 | 内容 |
| sub\_good\_id | 子条目id |
| sub\_good\_type | 商品规格 |
| sub\_good\_price | 商品价格 |

|     |     |
| --- | --- |
| 店铺主表 `store` |
| 字段名 | 内容 |
| store\_id | 店铺id |
| name | 店铺名称 |
| address | 店铺地址 |
| desc | 店铺描述 |

|     |     |
| --- | --- |
| 店铺子表 `store.sub_store` （配送方案和价格） |
| 字段名 | 内容 |
| sub\_plan\_id | 配送方案id |
| sub\_plan\_name | 配送方案名称 |
| sub\_plan\_distance | 配送半径 |
| sub\_plan\_price | 配送价格 |

表的实际数据位于`ha3_manual_example/sql/data` 中，可以直接用文本编辑器打开，也可以等待 `start_search.sh` 完毕后使用`SELECT` 语句检索全表。

若需要手动修改表对应的数据（.data文件）和.schema文件，修改完毕后记得重新构建索引和启动

```sql
cd ha3_manual_example/sql
sh stop.sh
sh build.sh
sh start_search.sh
```

建议优先在现有表上增加数据。

## 查询示例

注：以下示例为了方便用户比对查询结果，均在查询的末尾增加了`ORDER BY` 和`LIMIT` 关键字，实际上使用中并非必要，各业务可以视具体需求决定是否使用。

我们提供了一个`./search.sh` 脚本，供用户和启动完毕的HA3 SQL进行交互查询

```sql
cd ha3_manual_example/sql
./search.sh -s "SELECT nid FROM phone"
```

如需在查询中使用 **kvpair机制** 控制查询行为，可以将kvpair的内容拼接在查询语句的尾部

```sql
./search.sh -s "SELECT nid FROM phone&&kvpair=trace:trace3"
```

如无特殊说明，以下例子中的SQL指令都使用`./search.sh` 发送

- 检索全表内容


```sql
SELECT * FROM phone ORDER BY nid LIMIT 1000
```

```sql
USE_TIME: 0.036, ROW_COUNT: 10

------------------------------- TABLE INFO ---------------------------
                 nid |               title |               price |               brand |                size |               color |
                   1 |                null |                3599 |              Huawei |                 5.9 |                null |
                   2 |                null |                4388 |              Huawei |                 5.5 |                null |
                   3 |                null |                 899 |              Xiaomi |                   5 |                null |
                   4 |                null |                2999 |                OPPO |                 5.5 |                null |
                   5 |                null |                1299 |               Meizu |                 5.5 |                null |
                   6 |                null |                 169 |               Nokia |                 1.4 |                null |
                   7 |                null |                3599 |               Apple |                 4.7 |                null |
                   8 |                null |                5998 |               Apple |                 5.5 |                null |
                   9 |                null |                4298 |               Apple |                 4.7 |                null |
                  10 |                null |                5688 |             Samsung |                 5.6 |                null |
```

注：title和color仅配置了Summary字段，而未配置Attribute字段，所以在本阶段查询中显示为null

子表（子文档）是HA3中原有的机制，详细信息可以参考HA3中的文档。这里主要介绍如何用HA3 SQL操作子表：

- 借助

`UNNEST`

关键字，将

`goods`

表进行子表展开


```sql
SELECT pid, title, sub_good_id, sub_good_type, sub_good_price FROM goods, UNNEST(goods.sub_goods) ORDER BY sub_good_id LIMIT 100
```

```sql
USE_TIME: 0.028, ROW_COUNT: 14

------------------------------- TABLE INFO ---------------------------
                  pid(int64) |           title(multi_char) |          sub_good_id(int64) |   sub_good_type(multi_char) |      sub_good_price(double) |
                           1 |             麻辣烫套餐 |                           1 |                         小 |                          13 |
                           1 |             麻辣烫套餐 |                           2 |                         中 |                          14 |
                           1 |             麻辣烫套餐 |                           3 |                         大 |                          15 |
                           2 |                      薯条 |                           4 |                         小 |                          10 |
                           2 |                      薯条 |                           5 |                         中 |                          12 |
                           2 |                      薯条 |                           6 |                         大 |                          14 |
                           3 |                      可乐 |                           7 |                         小 |                           8 |
                           3 |                      可乐 |                           8 |                         中 |                          10 |
                           3 |                      可乐 |                           9 |                         大 |                          12 |
                           4 |                      新地 |                          10 |                      标准 |                           9 |
                           5 |                   黄焖鸡 |                          11 |                小份加辣 |                          20 |
                           5 |                   黄焖鸡 |                          12 |                小份不辣 |                          20 |
                           5 |                   黄焖鸡 |                          13 |                大份加辣 |                          25 |
                           5 |                   黄焖鸡 |                          14 |                大份不辣 |                          25 |
```

- 子表展开中，子表字段也可以参与条件筛选。此处筛选出价格不超过10元的商品


```sql
SELECT pid, title, sub_good_id, sub_good_type, sub_good_price FROM goods, UNNEST(goods.sub_goods) WHERE sub_good_price <= 10 ORDER BY sub_good_id LIMIT 100
```

```sql
USE_TIME: 0.033, ROW_COUNT: 4

------------------------------- TABLE INFO ---------------------------
                  pid(int64) |           title(multi_char) |          sub_good_id(int64) |   sub_good_type(multi_char) |      sub_good_price(double) |
                           2 |                      薯条 |                           4 |                         小 |                          10 |
                           3 |                      可乐 |                           7 |                         小 |                           8 |
                           3 |                      可乐 |                           8 |                         中 |                          10 |
                           4 |                      新地 |                          10 |                      标准 |                           9 |
```

HA3 SQL对多表联合进行了支持，借助该机制，可以扩展出很多功能：

- 联合

`goods`

和

`store`

表，打印售卖商品的店铺名称


```sql
SELECT pid, title, name FROM goods INNER JOIN store ON goods.store_id = store.store_id ORDER BY pid LIMIT 100
```

```sql
USE_TIME: 0.032, ROW_COUNT: 5

------------------------------- TABLE INFO ---------------------------
                  pid(int64) |           title(multi_char) |            name(multi_char) |
                           1 |             麻辣烫套餐 |          杨国福麻辣烫 |
                           2 |                      薯条 |                   麦当劳 |
                           3 |                      可乐 |                   麦当劳 |
                           4 |                      新地 |                   麦当劳 |
                           5 |                   黄焖鸡 |          杨铭宇黄焖鸡 |
```

- 为所有

`phone`

中的条目查询对应的summary字段


先从`phone` 表检索出`nid` 的所有可能值，然后查询summary。借助Join机制，该需求可以在一条语句中完成。

```sql
SELECT nid, brand, price FROM phone_summary_ WHERE nid in (SELECT nid FROM phone) ORDER BY nid LIMIT 100
```

```sql
------------------------------- TABLE INFO ---------------------------                                                                                                       |
                  nid(int64) |           brand(multi_char) |               price(double) |                                                                                   |
                           1 |                      Huawei |                        3599 |                                                                                   |
                           2 |                      Huawei |                        4388 |                                                                                   |
                           3 |                      Xiaomi |                         899 |                                                                                   |
                           4 |                        OPPO |                        2999 |                                                                                   |
                           5 |                       Meizu |                        1299 |                                                                                   |
                           6 |                       Nokia |                         169 |                                                                                   |
                           7 |                       Apple |                        3599 |                                                                                   |
                           8 |                       Apple |                        5998 |                                                                                   |
                           9 |                       Apple |                        4298 |                                                                                   |
                          10 |                     Samsung |                        5688 |
```

- 使用sum函数统计每个品牌商品的总价


```sql
SELECT brand, sum(price) FROM phone GROUP BY (brand) ORDER BY brand LIMIT 1000
```

```sql
USE_TIME: 0.152, ROW_COUNT: 7

------------------------------- TABLE INFO ---------------------------
               brand |          SUM(price) |
               Apple |               13895 |
              Huawei |                7987 |
               Meizu |                1299 |
               Nokia |                 169 |
                OPPO |                2999 |
             Samsung |                5688 |
              Xiaomi |                 899 |
```

- 使用avg函数统计每个品牌最贵手机的价格，并按照最高价格降序排列


```sql
SELECT brand, max(price) AS price FROM phone GROUP BY (brand) ORDER BY price DESC LIMIT 1000
```

```sql
USE_TIME: 0.053, ROW_COUNT: 7

------------------------------- TABLE INFO ---------------------------
               brand |               price |
               Apple |                5998 |
             Samsung |                5688 |
              Huawei |                4388 |
                OPPO |                2999 |
               Meizu |                1299 |
              Xiaomi |                 899 |
               Nokia |                 169 |
```

更详细的内容参考 **UDAF文档**