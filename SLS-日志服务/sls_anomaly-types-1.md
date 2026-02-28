### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[智能异常分析](https://help.aliyun.com/zh/sls/intelligent-anomaly-analysis/)[文本分析](https://help.aliyun.com/zh/sls/text-analysis/)异常类型说明

# 异常类型说明

更新时间：2026-01-09 04:05:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：算法说明](https://help.aliyun.com/zh/sls/algorithms-1)[下一篇：时序预测](https://help.aliyun.com/zh/sls/time-series-forecasting/)

该文章对您有帮助吗？

反馈

本文介绍文本分析结果的异常类型。

文本分析结果数据保存在名为internal-ml-log的LogStore中，您可以通过该数据中的result.type字段和result.anomaly\_type字段分析异常类型。更多信息，请参见 [结果字段说明](https://help.aliyun.com/zh/sls/result-fields#task-2149388 "")。

| **判断条件** | **异常类型说明** |
| --- | --- |

|     |     |
| --- | --- |
| **判断条件** | **异常类型说明** |
| - result.type字段值为anomaly\_info<br>  <br>- result.anomaly\_type字段值为N\_CLUSTER\_EVENT\_ANOMALY | 日志类别中的日志数量异常。 |
| - result.type字段值为anomaly\_info<br>  <br>- result.anomaly\_type字段值为NEW\_CLUSTER\_ANOMALY | 出现新的日志类别。<br>出现新的日志类别有如下两种情况。<br>- 该日志类别第一次出现。<br>  <br>- 该日志类别已出现过，但在出现后的很长时间内（最大的静默时间，通过算法参数进行设置）未再次出现。 |
| - result.type字段值为anomaly\_info<br>  <br>- result.anomaly\_type字段值为RARE\_CLUSTER\_ANOMALY | 该日志类别出现的频率较低。 |