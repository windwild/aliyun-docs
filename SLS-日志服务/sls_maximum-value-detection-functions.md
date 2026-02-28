### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)[机器学习语法](https://help.aliyun.com/zh/sls/machine-learning-syntax/)[时序SQL](https://help.aliyun.com/zh/sls/time-series-sql-function/)极大值检测函数

# 极大值检测函数

更新时间：2024-06-06 01:23:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：变点检测函数](https://help.aliyun.com/zh/sls/change-point-detection-functions)[下一篇：预测与异常检测函数](https://help.aliyun.com/zh/sls/prediction-and-anomaly-detection-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

ts\_find\_peaks

极大值检测函数用于在指定窗口中寻找序列的局部极大值。

## ts\_find\_peaks

函数格式：


```plaintext
select ts_find_peaks(x, y, winSize)
```

参数说明如下：


| **参数** | **说明** | **取值** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **说明** | **取值** |
| _x_ | 时间列，从小到大排列。 | 格式为Unixtime时间戳，单位为秒。 |
| _y_ | 数值列，对应某时刻的数据。 | - |
| _winSize_ | 指定最小的检测窗口长度。 | long类型，取值范围为大于等于1，小于等于数值的实际长度。建议指定该参数的值为数据实际长度的十分之一。 |

示例：


- 查询分析：
















```plaintext
* and h : nu2h05202.nu8 and m: NET |  select ts_find_peaks(stamp, value, 30) from (select '("__time__" - ("__time__" % 10))' as stamp, avg(v) as value from log GROUP  BY  stamp order by stamp)
```

- 输出结果：![输出结果](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1340559951/p33817.png)


显示项如下：


| **显示项** | **说明** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **显示项** | **说明** |
| 横轴 | unixtime | 数据的时间戳，单位为秒，例如1537071480。 |
| 纵轴 | src | 未滤波前的数据，例如1956092.7647745228。 |
| peak\_flag | 该点是否为极大值，其中： <br> <br>- 1.0：表示该点为极大值。<br>  <br>- 0.0：表示该点不是极大值。 |