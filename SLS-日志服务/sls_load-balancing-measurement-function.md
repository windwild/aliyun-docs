### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)[机器学习语法](https://help.aliyun.com/zh/sls/machine-learning-syntax/)[机器学习函数](https://help.aliyun.com/zh/sls/machine-learning-functions/)负载均衡测量函数

# 负载均衡测量函数

更新时间：2024-09-25 01:58:24

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：分类判别分析函数（Classification）](https://help.aliyun.com/zh/sls/classification-discriminant-analysis-function-classification)[下一篇：多变量模式识别函数](https://help.aliyun.com/zh/sls/multivariable-pattern-recognition-function)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

负载均衡度函数列表

how\_balanced函数

使用示例

在执行操作实现负载均衡前，需要准确衡量分布式系统负载均衡状况。本文介绍负载均衡测量函数的基本语法和示例。

## **背景信息**

- 负载均衡测量函数示例的日志包含六个字段索引（集群ID、服务器ID、时间、CPU负载、内存负载和网络带宽负载）。更多信息，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes "")。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5841186271/p850661.png)

- 日志样例如下：















```json
{"cluster_id":"C001","cpu_load":"0.1","network_load":"0.6","ram_load":"0.7","server_id":"S001","time_period":"2024-01-01 00:00:00"}
{"cluster_id":"C001","cpu_load":"0.2","network_load":"0.5","ram_load":"0.8","server_id":"S002","time_period":"2024-01-01 00:01:00"}
{"cluster_id":"C001","cpu_load":"0.1","network_load":"0.6","ram_load":"0.7","server_id":"S001","time_period":"2024-01-01 00:02:00"}
{"cluster_id":"C001","cpu_load":"0.2","network_load":"0.5","ram_load":"0.8","server_id":"S002","time_period":"2024-01-01 00:03:00"}
{"cluster_id":"C001","cpu_load":"0.1","network_load":"0.6","ram_load":"0.7","server_id":"S001","time_period":"2024-01-01 00:04:00"}
{"cluster_id":"C001","cpu_load":"0.2","network_load":"0.5","ram_load":"0.8","server_id":"S002","time_period":"2024-01-01 00:05:00"}
{"cluster_id":"C001","cpu_load":"0.1","network_load":"0.6","ram_load":"0.7","server_id":"S001","time_period":"2024-01-01 00:06:00"}
{"cluster_id":"C001","cpu_load":"0.2","network_load":"0.5","ram_load":"0.8","server_id":"S002","time_period":"2024-01-01 00:07:00"}
{"cluster_id":"C001","cpu_load":"0.1","network_load":"0.6","ram_load":"0.7","server_id":"S001","time_period":"2024-01-01 00:08:00"}
{"cluster_id":"C001","cpu_load":"0.2","network_load":"0.5","ram_load":"0.8","server_id":"S002","time_period":"2024-01-01 00:09:00"}
```


## 负载均衡度函数列表

| **函数名称** | **语法** | **说明** | **返回值类型** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **函数名称** | **语法** | **说明** | **返回值类型** |
| [how\_balanced函数](https://help.aliyun.com/zh/sls/load-balancing-measurement-function#e54ba4c82cvgt "") | how\_balanced(array(array(double)) load\_matrix) | 结合 [array\_agg函数](https://help.aliyun.com/zh/sls/array-functions-and-operators#section-vj9-7pe-r2d "")，测量分布式系统负载均衡度。返回值表示负载均衡的程度，范围在`(0,1]`之间。数值越接近1，表示负载越均衡，其中1表示完全平衡状态。 | double |

## **how\_balanced函数**

结合 [array\_agg函数](https://help.aliyun.com/zh/sls/array-functions-and-operators#section-vj9-7pe-r2d "")，测量分布式系统负载均衡度。

```sql
double how_balanced(array(array(double)) load_matrix)
```

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| `load_matrix` | 一个负载矩阵，每一行代表了单个服务器的负载时间序列向量。 |

### **使用示例**

- 查询和分析语句















```sql
* | with server_time_series as
(
      select cluster_id,
          server_id,
          array_agg(to_unixtime(date_parse(time_period, '%Y-%m-%d %H:%i:%s'))) as time_periods,
          array_agg(cpu_load + ram_load + network_load) as metric_values
      from log
      where time_period >= '2024-01-01 00:00:00'
        and time_period < '2024-01-02 00:00:00'
      group by cluster_id, server_id
),

imputed_server_series as
(
      select cluster_id,
          server_id,
          ts_fill_missing(
              time_periods,
              metric_values,
              to_unixtime(date_parse('2024-01-01 00:00:00', '%Y-%m-%d %H:%i:%s')),
              to_unixtime(date_parse('2024-01-02 00:00:00', '%Y-%m-%d %H:%i:%s')),
              '1 minute', 'value=0') as imputed_time_series
      from server_time_series
)

select cluster_id,
      how_balanced(array_agg(imputed_time_series[2])) as balance
from imputed_server_series
group by cluster_id
```

- 返回结果

`balance`表示负载均衡的程度，范围在`(0,1]`之间。数值越接近1，表示负载越均衡，其中1表示完全平衡状态。




| **cluster\_id** | **balance** |
| --- | --- |



|     |     |
| --- | --- |
| **cluster\_id** | **balance** |
| G1 | 0.5 |