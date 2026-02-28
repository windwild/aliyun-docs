### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) in\_polygon

# in\_polygon

更新时间：2023-12-19 01:33:12

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：动态与公告](https://help.aliyun.com/zh/open-search/announcements-and-updates)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能函数项

in\_polygon : 判断某个点是否在某个多边形范围内，一般用于配送范围判断

## 功能函数项

插件功能函数可以用在filter子句作为过滤和筛选条件，而返回值为数值型的功能函数在sort子句中，用来做排序。

**其中功能函数参数出现的文档字段需根据对应函数文档提示，创建为索引或属性**.

## in\_polygon : 判断某个点是否在某个多边形范围内，一般用于配送范围判断

1.详细用法：

in\_polygon(polygon\_field, user\_x\_coordinate, user\_y\_coordinate, has\_multi\_polygons=”false”)

2.参数：

- **polygon\_field**: 表示商家配送范围的字段名，类型必须为DOUBLE\_ARRAY, 字段值依次为配送多边形有序定点的x,y坐标（先x后y），顶点务必保证有序（顺时针、逆时针均可），如果有多个（N个）配送多边形，则第一个值表示多边形个数，第2~N+1的值表示后续每个多边形的顶点数（不是坐标数哦！！），第N+2值开始依次表示各多边形的顶点x,y坐标（ **N的值域为\[1,50\]**）


![1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0169941261/p275773.png)

- **user\_x\_coordinate**: 用户的x坐标, double类型

- **user\_y\_coordinate**: 用户的y坐标, double类型

- **has\_multi\_polygons**：表示polygon\_filed是否包含多个独立的多边形需要判断。默认为false，表示只有单一的多边形。


3.返回值：

int，在多边形内返回第几个多边形匹配, 否则返回0。

4.适用场景：

场景1：判断用户是否在商家的配送范围。如商家配送范围的字段为coordinates, 用户位置坐标为 (120.307234, 39.294245)，则过滤在配送范围内的商家查询可写为：

```sql
 query=default:’美食’&&filter=in_polygon(coordinates, 120.307234, 39.294245)>0
```

5.注意事项：

- 函数参数依赖字段需创建为属性

- 最多支持50个多边形，超过则跳过该文档的计算；

- 不支持有孔多边形，如环；

- 不支持多个分离部分的多边形；

- 坐标个数为0，表示没有坐标，返回0；

- 坐标个数为奇数个，则认为数据有误，返回0；

- 用户点位于多边形边上，则认为匹配成功，返回为1（或具体多边形下标）。

- 多边形插件计算量较大，对查询性能有影响，建议尽量控制顶点个数，具体值请根据自己实际情况进行测试得出。