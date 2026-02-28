### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)[SQL分析语法与功能](https://help.aliyun.com/zh/sls/sql-syntax-and-functions/)[SQL函数](https://help.aliyun.com/zh/sls/sql-function/)地理函数

# 地理函数

更新时间：2023-12-27 01:06:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：空间几何函数](https://help.aliyun.com/zh/sls/geospatial-functions)[下一篇：颜色函数](https://help.aliyun.com/zh/sls/color-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

geohash函数

语法

参数说明

返回值类型

示例

本文介绍地理函数的基本语法及示例。

日志服务支持如下地理函数。

**重要**

在日志服务分析语句中，表示字符串的字符必须使用单引号（''）包裹，无符号包裹或被双引号（""）包裹的字符表示字段名或列名。例如：'status'表示字符串status，status或"status"表示日志字段status。

| **函数名称** | **语法** | **说明** | 支持SQL | 支持SPL |
| --- | --- | --- | --- | --- |

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **函数名称** | **语法** | **说明** | 支持SQL | 支持SPL |
| [geohash函数](https://help.aliyun.com/zh/sls/geo-functions#section-v65-fai-y9f "") | geohash(_x_) | 对纬度和经度进行geohash编码。<br>**说明**<br>日志服务支持将IP地址转换为国家、省份、城市、运营商或经纬度等信息。更多信息，请参见 [IP函数](https://help.aliyun.com/zh/sls/ip-functions#concept-wmd-slq-zdb "")。 | √ | × |

## geohash函数

geohash函数用于对纬度和经度进行geohash编码。

### 语法

```plaintext
geohash(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为string类型。内容为经纬度，例如`ip_to_geo(经度,纬度)`。 |

### 返回值类型

string类型。

### 示例

使用ip\_to\_geo函数将client\_ip字段值转换为经纬度形式，再使用geohash函数进行编码。

- 查询和分析语句















```plaintext
* | SELECT geohash(ip_to_geo(client_ip)) AS hash
```

- 查询和分析结果![geohash](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9313887261/p300313.png)