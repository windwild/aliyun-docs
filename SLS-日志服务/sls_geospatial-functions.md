### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[查询与分析](https://help.aliyun.com/zh/sls/index-and-query/)[查询与分析语法说明](https://help.aliyun.com/zh/sls/query-and-analysis-syntax-description/)[SQL分析语法与功能](https://help.aliyun.com/zh/sls/sql-syntax-and-functions/)[SQL函数](https://help.aliyun.com/zh/sls/sql-function/)空间几何函数

# 空间几何函数

更新时间：2023-12-27 01:07:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：位运算函数](https://help.aliyun.com/zh/sls/bitwise-functions)[下一篇：地理函数](https://help.aliyun.com/zh/sls/geo-functions)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

空间几何概念

函数列表

ST\_AsText函数

语法

参数说明

返回值类型

示例

ST\_GeometryFromText函数

语法

参数说明

返回值类型

示例

ST\_LineFromText函数

语法

参数说明

返回值类型

示例

ST\_Polygon函数

语法

参数说明

返回值类型

示例

ST\_Point函数

语法

参数说明

返回值类型

示例

ST\_Boundary函数

语法

参数说明

返回值类型

示例

ST\_Buffer函数

语法

参数说明

返回值类型

示例

ST\_Difference函数

语法

参数说明

返回值类型

示例

ST\_Envelope函数

语法

参数说明

返回值类型

示例

ST\_ExteriorRing函数

语法

参数说明

返回值类型

示例

ST\_Intersection函数

语法

参数说明

返回值类型

示例

ST\_SymDifference函数

语法

参数说明

返回值类型

示例

ST\_Contains函数

语法

参数说明

返回值类型

示例

ST\_Crosses函数

语法

参数说明

返回值类型

示例

ST\_Disjoint函数

语法

参数说明

返回值类型

示例

ST\_Equals函数

语法

参数说明

返回值类型

示例

ST\_Intersects函数

语法

参数说明

返回值类型

示例

ST\_Overlaps函数

语法

参数说明

返回值类型

示例

ST\_Relate函数

语法

参数说明

返回值类型

示例

ST\_Touches函数

语法

参数说明

返回值类型

示例

ST\_Within函数

语法

参数说明

返回值类型

示例

ST\_Area函数

语法

参数说明

返回值类型

示例

ST\_Centroid函数

语法

参数说明

返回值类型

示例

ST\_CoordDim函数

语法

参数说明

返回值类型

示例

ST\_Dimension函数

语法

参数说明

返回值类型

示例

ST\_Distance函数

语法

参数说明

返回值类型

示例

ST\_EndPoint函数

语法

参数说明

返回值类型

示例

ST\_IsClosed函数

语法

参数说明

返回值类型

示例

ST\_IsEmpty函数

语法

参数说明

返回值类型

示例

ST\_IsRing函数

语法

参数说明

返回值类型

示例

ST\_Length函数

语法

参数说明

返回值类型

示例

ST\_NumPoints函数

语法

参数说明

返回值类型

示例

ST\_NumInteriorRing函数

语法

参数说明

返回值类型

示例

ST\_StartPoint函数

语法

参数说明

返回值类型

示例

ST\_X函数

语法

参数说明

返回值类型

示例

ST\_XMax函数

语法

参数说明

返回值类型

示例

ST\_XMin函数

语法

参数说明

返回值类型

示例

ST\_Y函数

语法

参数说明

返回值类型

示例

ST\_YMax函数

语法

参数说明

返回值类型

示例

ST\_YMin函数

语法

参数说明

返回值类型

示例

bing\_tile函数

语法

参数说明

返回值类型

示例

bing\_tile\_at函数

语法

参数说明

返回值类型

示例

bing\_tile\_coordinates函数

语法

参数说明

返回值类型

示例

bing\_tile\_polygon函数

语法

参数说明

返回值类型

示例

bing\_tile\_quadkey函数

语法

参数说明

返回值类型

示例

bing\_tile\_zoom\_level函数

语法

参数说明

返回值类型

示例

本文介绍空间几何函数的基本语法及示例。

## 空间几何概念

以ST\_前缀开头的空间几何函数支持SQL/MM标准并符合开放地理空间联盟 (OGC) 的OpenGIS规范。空间几何函数使用Well-Known Text（WKT）格式描述空间几何体（例如点、线段、多边形等），详细说明如下表所示。

| **空间几何体** | **Well-Known Text（WKT）格式** |
| --- | --- |

|     |     |
| --- | --- |
| **空间几何体** | **Well-Known Text（WKT）格式** |
| 点 | POINT (0 0) |
| 线段 | LINESTRING (0 0, 1 1, 1 2) |
| 多边形 | POLYGON((0 0, 4 0, 4 4, 0 4, 0 0), (1 1, 2 1, 2 2, 1 2, 1 1)) |
| 多点 | MULTIPOINT(0 0, 1 2) |
| 多线段 | MULTILINESTRING((0 0, 1 1, 1 2), (2 3, 3 2, 5 4)) |
| 多个多边形 | MULTIPOLYGON(((0 0, 4 0, 4 4, 0 4, 0 0), (1 1, 2 1, 2 2, 1 2, 1 1)), ((-1 -1, -1 -2, -2 -2, -2 -1, -1 -1))) |
| 空间几何体集合 | GEOMETRYCOLLECTION(POINT(2 3), LINESTRING(2 3, 3 4)) |

## 函数列表

| **分类** | **函数名称** | **语法** | **说明** | 支持SQL | 支持SPL |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **分类** | **函数名称** | **语法** | **说明** | 支持SQL | 支持SPL |
| 构造空间实体 | [ST\_AsText函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-uf9-ooi-du2 "") | ST\_AsText(_x_) | 将一个空间几何体转变为WKT格式的文本。 | √ | × |
| [ST\_GeometryFromText函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-48m-m4j-06b "") | ST\_GeometryFromText(_x_) | 根据输入的WKT文本构造一个空间几何体。 | √ | × |
| [ST\_LineFromText函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-8m7-og8-h4e "") | ST\_LineFromText(_x_) | 根据输入的WKT文本构造一条线段。 | √ | × |
| [ST\_Polygon函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-cm1-cek-75m "") | ST\_Polygon(_x_) | 根据输入的WKT文本构造一个多边形。 | √ | × |
| [ST\_Point函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-rlo-dkw-8bj "") | ST\_Point(_x_, _y_) | 根据输入的WKT文本构造一个点。 | √ | × |
| 运算符 | [ST\_Boundary函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-bot-4rj-c7w "") | ST\_Boundary(_x_) | 返回空间几何体的边界。 | √ | × |
| [ST\_Buffer函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-f6n-liv-3xh "") | ST\_Buffer(_x_, _distance_) | 返回距离指定空间几何体一定距离的空间几何体。 | √ | × |
| [ST\_Difference函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-dqo-a0n-w1f "") | ST\_Difference(_x_, _y_) | 返回两个空间几何体不同点的集合。 | √ | × |
| [ST\_Envelope函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-qcu-yqo-xo7 "") | ST\_Envelope(_x_) | 返回空间几何体的最小边界框。 | √ | × |
| [ST\_ExteriorRing函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-5e0-e34-uct "") | ST\_ExteriorRing(_x_) | 返回空间几何体的外环（线段形式）。 | √ | × |
| [ST\_Intersection函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-whq-rb9-eo4 "") | ST\_Intersection(_x_, _y_) | 返回两个空间几何体的交集点。 | √ | × |
| [ST\_SymDifference函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-5ym-66t-xom "") | ST\_SymDifference(_x_, _y_) | 返回两个空间几何体的不同点，然后组成一个新的空间几何体。 | √ | × |
| 空间关系判断 | [ST\_Contains函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-bwh-0yi-d6k "") | ST\_Contains(_x_, _y_) | 判断第一个空间几何体是否包含第二个空间几何体（边界可存在交集）。如果包含，则返回true。 | √ | × |
| [ST\_Crosses函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-3dz-03v-q35 "") | ST\_Crosses(_x_, _y_) | 判断两个空间几何体是否存在相同的内部点。如果存在，则返回true。 | √ | × |
| [ST\_Disjoint函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-b65-y0a-140 "") | ST\_Disjoint(_x_, _y_) | 判断两个空间几何体是否没有任何交集。 如果没有，则返回true。 | √ | × |
| [ST\_Equals函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-8do-nhl-2uh "") | ST\_Equals(_x_, _y_) | 判断两个空间几何体是否完全相同。如果是，则返回true。 | √ | × |
| [ST\_Intersects函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-l5z-7sj-s8l "") | ST\_Intersects(_x_, _y_) | 判断两个空间几何体的平面投影是否存在共同点。如果是，则返回true。 | √ | × |
| [ST\_Overlaps函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-htm-799-jbx "") | ST\_Overlaps(_x_, _y_) | 判断两个空间几何体的维度是否相同。如果两个空间几何体的维度相同且不是包含关系，则返回true。 | √ | × |
| [ST\_Relate函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-euf-ym7-sg7 "") | ST\_Relate(_x_, _y_,_patternMatrix string_) | 判断两个空间几何体是否相关。如果是，则返回true。 | √ | × |
| [ST\_Touches函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-akl-aqy-hmu "") | ST\_Touches(_x_, _y_) | 判断两个空间几何体是否只有边界存在关联，没有共同的内部点。如果是，则返回true。 | √ | × |
| [ST\_Within函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-1cr-ecg-owu "") | ST\_Within(_x_, _y_) | 判断第一个空间几何体是否完全在第二个空间几何体内部（边界无交集）。如果是，则返回true。 | √ | × |
| Accessors | [ST\_Area函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-8s0-ka8-0os "") | ST\_Area(_x_) | 使用欧几里得测量法计算空间几何体在二维平面上的投影面积。 | √ | × |
| [ST\_Centroid函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-ge2-pko-nu9 "") | ST\_Centroid(_x_) | 返回空间几何实体的中心点。 | √ | × |
| [ST\_CoordDim函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-nqn-1a7-z02 "") | ST\_CoordDim(_x_) | 返回空间几何体的坐标维度。 | √ | × |
| [ST\_Dimension函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-vtn-hlz-pqn "") | ST\_Dimension(_x_) | 返回空间几何实体的固有维度，必须小于或等于坐标维度。 | √ | × |
| [ST\_Distance函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-qk5-p6p-406 "") | ST\_Distance(_x_, _y_) | 计算两个空间几何体之间的最小距离。 | √ | × |
| [ST\_EndPoint函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-vod-0jn-1by "") | ST\_EndPoint(_x_) | 返回线段中的最后一个点。 | √ | × |
| [ST\_IsClosed函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-gp6-nhp-wf6 "") | ST\_IsClosed(_x_) | 判断输入的空间几何体是否封闭。如果是，则返回true。 | √ | × |
| [ST\_IsEmpty函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-w0e-bpe-zdt "") | ST\_IsEmpty(_x_) | 判断输入的空间几何体是否为空。如果是，则返回true。 | √ | × |
| [ST\_IsRing函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-vyq-1f8-6jr "") | ST\_IsRing(_x_) | 判断输入的空间几何体是否为闭合的简单线段（环）。如果是，则返回true。 | √ | × |
| [ST\_Length函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-f0k-9qv-413 "") | ST\_Length(_x_) | 使用欧几里得测量法计算线段的二维投影长度。如果存在多条线段，则返回所有线段的长度之和。 | √ | × |
| [ST\_NumPoints函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-hff-e0e-7cr "") | ST\_NumPoints(_x_) | 返回空间几何体中点的个数。 | √ | × |
| [ST\_NumInteriorRing函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-209-wyy-8xk "") | ST\_NumInteriorRing(_x_) | 计算空间几何体中内部环的数量。 | √ | × |
| [ST\_StartPoint函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-erh-jm1-h6w "") | ST\_StartPoint(_x_) | 返回线段中的第一个点。 | √ | × |
| [ST\_X函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-ntz-66g-q2w "") | ST\_X(_x_) | 返回输入点的第一个X轴坐标。 | √ | × |
| [ST\_XMax函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-imm-d1d-7y9 "") | ST\_XMax(_x_) | 返回空间几何体的第一个最大的X轴坐标。 | √ | × |
| [ST\_XMin函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-ypd-gr0-y7z "") | ST\_XMin(_x_) | 返回空间几何体的第一个最小的X轴坐标。 | √ | × |
| [ST\_Y函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-zsp-j85-b7e "") | ST\_Y(_x_) | 返回输入点的第一个Y轴坐标。 | √ | × |
| [ST\_YMax函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-8k6-97u-weu "") | ST\_YMax(_x_) | 返回空间几何体的第一个最大的Y轴坐标。 | √ | × |
| [ST\_YMin函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-6mk-z79-5jg "") | ST\_YMin(_x_) | 返回几何体的第一个最小的Y轴坐标。 | √ | × |
| Bing图块 | [bing\_tile函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-lnq-1qa-6gi "") | bing\_tile(_x_, _y_, _zoom\_level_) | 通过X坐标、Y坐标和缩放级别构造一个Bing图块。 | √ | × |
| bing\_tile(_quadKey_) | 通过四叉树键构造一个Bing图块。 | √ | × |
| [bing\_tile\_at函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-a72-l72-134 "") | bing\_tile\_at(_x_, _y_,_zoom\_level_) | 通过经纬度和缩放级别构造一个Bing图块。 | √ | × |
| [bing\_tile\_coordinates函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-5ly-1yr-thl "") | bing\_tile\_coordinates(_x_) | 返回目标Bing图块对应的X坐标和Y坐标。 | √ | × |
| [bing\_tile\_polygon函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-o76-del-7dd "") | bing\_tile\_polygon(_x_) | 返回目标Bing图块的多边形格式。 | √ | × |
| [bing\_tile\_quadkey函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-kup-fo0-d4n "") | bing\_tile\_quadkey(_x_) | 返回目标Bing图块的四叉树键。 | √ | × |
| [bing\_tile\_zoom\_level函数](https://help.aliyun.com/zh/sls/geospatial-functions#section-lly-hw4-8vo "") | bing\_tile\_zoom\_level(_x_) | 返回目标Bing图块的缩放级别。 | √ | × |

## ST\_AsText函数

ST\_AsText函数用于将一个空间几何体转变成WKT文本。

### 语法

```plaintext
ST_AsText(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

varchar类型。

### 示例

将一个点转变成WKT格式的文本。

- 查询和分析语句















```plaintext
* | SELECT ST_AsText(ST_Point(1,1))
```

- 查询和分析结果![ST_AsText](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8583439261/p304082.png)


## ST\_GeometryFromText函数

ST\_GeometryFromText函数会根据您输入的WKT文本构造一个空间几何体。

### 语法

```plaintext
ST_GeometryFromText(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为varchar类型。 |

### 返回值类型

geometry类型。

### 示例

构造多个多边形。

- 查询和分析语句















```plaintext
* | SELECT ST_GeometryFromText('multipolygon(((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))')
```

- 查询和分析结果![ST_GeometryFromText](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8208969261/p304085.png)


## ST\_LineFromText函数

ST\_LineFromText函数会根据您输入的WKT文本构造一条线段。

### 语法

```plaintext
ST_LineFromText(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为varchar类型。 |

### 返回值类型

linestring类型。

### 示例

构造一条线段。

- 查询和分析语句















```plaintext
* | SELECT ST_LineFromText('linestring(10 10,20 20)')
```

- 查询和分析结果![ST_LineFromText](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8208969261/p304089.png)


## ST\_Polygon函数

ST\_Polygon函数会根据您输入的WKT文本构造一个多边形。

### 语法

```plaintext
ST_Polygon(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为varchar类型。 |

### 返回值类型

polygon类型。

### 示例

构造一个多边形。

- 查询和分析语句















```plaintext
* | SELECT ST_Polygon('polygon((10 10,10 20,20 20,20 15,10 10))')
```

- 查询和分析结果![ST_Polygon](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8208969261/p304095.png)


## ST\_Point函数

ST\_Point函数会根据您输入的WKT文本构造一个点。

### 语法

```plaintext
ST_Point(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

point类型。

### 示例

构造一个点。

- 查询和分析语句















```plaintext
* | SELECT ST_Point(0,0)
```

- 查询和分析结果![ST_Point](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8208969261/p308878.png)


## ST\_Boundary函数

ST\_Boundary函数用于返回空间几何体的边界。

- 点的边界为空，即返回POINT EMPTY。

- 线段的边界由线段的端点组成。

- 多边形的边界由构成多边形的外环及其所有内环的线段组成。


### 语法

```plaintext
ST_Boundary(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geography类型。 |

### 返回值类型

geography类型。

### 示例

使用ST\_Polygon函数构造一个多边形，然后使用ST\_Boundary返回多边形的边界。

- 查询和分析语句















```plaintext
* | SELECT  ST_Boundary(ST_Polygon('polygon((10 10,10 20,20 20,20 15,10 10))'))
```

- 查询和分析结果![ST_Boundary](<Base64-Image-Removed>)


## ST\_Buffer函数

ST\_Buffer函数用于返回距离指定空间几何体一定距离的空间几何体。

### 语法

```plaintext
ST_Buffer(x, distance)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _distance_ | 距离。 |

### 返回值类型

geometry类型。

### 示例

使用ST\_Point函数构造一个点，然后使用ST\_Buffer函数返回距离该点一定距离的多边形。

- 查询和分析语句















```plaintext
* | SELECT ST_Buffer(ST_Point(1,1),1)
```

- 查询和分析结果![ST_Buffer](<Base64-Image-Removed>)


## ST\_Difference函数

ST\_Difference函数用于返回两个空间几何体不同点的集合。

### 语法

```plaintext
ST_Difference(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

geometry类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Difference函数返回两个空间几何体不同点的集合。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Difference(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,0 15,0 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    ) AS "Difference"
```

- 查询和分析结果![ST_Difference](<Base64-Image-Removed>)


## ST\_Envelope函数

ST\_Envelope函数用于返回空间几何体的最小边界框。

### 语法

```plaintext
ST_Envelope(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

geometry类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_Envelope函数返回该空间几何体的最小边界框。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Envelope(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_Envelope](<Base64-Image-Removed>)


## ST\_ExteriorRing函数

ST\_ExteriorRing函数用于返回空间几何体的外环（线段形式）。

### 语法

```plaintext
ST_ExteriorRing(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

geometry类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_ExteriorRing函数返回该空间几何体的外环。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_ExteriorRing(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_ExteriorRing](<Base64-Image-Removed>)


## ST\_Intersection函数

ST\_Intersection函数用于返回两个空间几何体的交集点。

### 语法

```plaintext
ST_Intersection(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

geometry类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Intersection函数返回两个空间几何体的交集点。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Intersection(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ST_Intersection](<Base64-Image-Removed>)


## ST\_SymDifference函数

ST\_SymDifference函数用于返回两个空间几何体的不同点，然后组成一个新的空间几何体。

### 语法

```plaintext
ST_SymDifference(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

geometry类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_SymDifference函数返回两个空间几何体的不同点，组成一个新的空间几何体。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_SymDifference(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ST_SymDifference](<Base64-Image-Removed>)


## ST\_Contains函数

ST\_Contains函数用于判断第一个空间几何体是否包含第二个空间几何体（边界可存在交集）。如果包含，则返回true。

### 语法

```plaintext
ST_Contains(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Contains函数判断第一个空间几何体是否包含第二个空间几何体（边界可存在交集）。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Contains(
      ST_GeometryFromText(
        'polygon((10 10,10 20,20 20,20 15,10 10))'
      ),
      ST_GeometryFromText(
        'point(11 11)'
      )
    )
```

- 查询和分析结果![ ST_Contains](<Base64-Image-Removed>)


## ST\_Crosses函数

ST\_Crosses函数用于判断两个空间几何体是否存在相同的内部点。如果存在，则返回true。

### 语法

```plaintext
ST_Crosses(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Crosses函数判断两个空间几何体是否存在相同的内部点。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Crosses(
      ST_GeometryFromText(
        'multipolygon (((10 10, 10 20, 20 20, 20 15 , 10 10), (50 40, 50 50, 60 50, 60 40, 50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10, 10 20, 20 20, 20 15 , 10 10), (50 40, 50 50, 60 50, 60 40, 50 50)))'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_Disjoint函数

ST\_Disjoint函数用于判断两个空间几何体是否没有任何交集。 如果没有，则返回true。

### 语法

```plaintext
ST_Disjoint(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Disjoint函数判断两个空间几何体是否存在交集。

- 查询和分析语句















```plaintext
* |
SELECT
     ST_Disjoint(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_Equals函数

ST\_Equals函数用于判断两个空间几何体是否完全相同。如果是，则返回true。

### 语法

```plaintext
ST_Equals(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Equals函数判断两个空间几何体是否完全相同。

- 查询和分析语句















```plaintext
* |
SELECT
     ST_Equals(
      ST_GeometryFromText(
        'multipolygon(((10 10,10 20,20 20,20 15,10 10),(50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon(((10 10,10 20,20 20,20 15,10 10),(50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_Intersects函数

ST\_Intersects函数用于判断两个空间几何体的平面投影是否存在共同点。如果是，则返回true。

### 语法

```plaintext
ST_Intersects(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Intersects函数判断两个空间几何体的平面投影是否存在共同点。

- 查询和分析语句















```plaintext
* |
SELECT
     ST_Intersects(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ ST_Contains](<Base64-Image-Removed>)


## ST\_Overlaps函数

ST\_Overlaps函数用于判断两个空间几何体的维度是否相同。如果两个空间几何体的维度相同且不是包含关系，则返回true。

### 语法

```plaintext
ST_Overlaps(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Overlaps函数判断两个空间几何体的维度是否相同。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Overlaps(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_Relate函数

ST\_Relate函数用于判断两个空间几何体是否相关（内部或边界以任何方式相关）。如果是，则返回true。

### 语法

```plaintext
ST_Relate(x, y, patternMatrix string)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |
| _patternMatrix string_ | DE-9IM模式矩阵字符串，参数值为varchar类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Relate函数判断两个空间几何体是否相关。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Relate(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      ),  '****T****'
    )
```

- 查询和分析结果![ ST_Contains](<Base64-Image-Removed>)


## ST\_Touches函数

ST\_Touches函数用于判断两个空间几何体是否只有边界存在关联，没有共同的内部点。如果是，则返回true。

### 语法

```plaintext
ST_Touches(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Touches函数判断两个空间几何体是否只有边界存在关联，没有共同的内部点。

- 查询和分析语句















```plaintext
* |
SELECT
     ST_Touches(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_Within函数

ST\_Within函数用于判断第一个空间几何体是否完全在第二个空间几何体内部（边界无交集）。如果是，则返回true。

### 语法

```plaintext
ST_Within(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Within函数判断第一个空间几何体是否完全在第二个空间几何体内部。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Within(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_Area函数

ST\_Area函数使用欧几里得测量法计算空间几何体在二维平面上的投影面积。

### 语法

```plaintext
ST_Area(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_Area函数计算该空间几何体在二维平面上的投影面积。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Area(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_Area](<Base64-Image-Removed>)


## ST\_Centroid函数

ST\_Centroid函数用于返回空间几何体的中心点。

### 语法

```plaintext
ST_Centroid(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

geometry类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_Centroid函数返回该空间几何体的中心点。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Centroid(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_Centroid](<Base64-Image-Removed>)


## ST\_CoordDim函数

ST\_CoordDim函数用于返回空间几何体的坐标维度。

### 语法

```plaintext
ST_CoordDim(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

bigint类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_CoordDim函数返回该空间几何体的坐标维度。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_CoordDim(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_CoordDim](<Base64-Image-Removed>)


## ST\_Dimension函数

ST\_Dimension函数用于返回空间几何体的固有维度，必须小于或等于坐标维度。

### 语法

```plaintext
ST_Dimension(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。<br>- _x_为点或空的空间几何体时，返回值为0。<br>  <br>- _x_为线段时，返回值为1。<br>  <br>- _x_为多边形时，返回值为2。<br>  <br>- _x_为空间几何体时，返回值为集合的最大维度。 |

### 返回值类型

bigint类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_Dimension函数返回该空间几何体的固有维度。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Dimension(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_Dimension](<Base64-Image-Removed>)


## ST\_Distance函数

ST\_Distance函数用于计算两个空间几何体之间的最小距离。

### 语法

```plaintext
ST_Distance(x, y)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |
| _y_ | 参数值为geometry类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_GeometryFromText函数构造两个空间几何体，然后使用ST\_Distance函数计算两个空间几何体之间的最小距离。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Distance(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 50)))'
      ),
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_Distance](<Base64-Image-Removed>)


## ST\_EndPoint函数

ST\_EndPoint函数用于返回线段中的最后一个点。

### 语法

```plaintext
ST_EndPoint(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

point类型。

### 示例

使用ST\_LineFromText函数构造一条线段，然后使用ST\_EndPoint函数返回线段中的最后一个点。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_EndPoint(
      ST_LineFromText(
        'linestring (10 10,20 20)'
      )
    )
```

- 查询和分析结果![ST_EndPoint](<Base64-Image-Removed>)


## ST\_IsClosed函数

ST\_IsClosed函数用于判断空间几何体是否封闭。如果是，则返回true。

### 语法

```plaintext
ST_IsClosed(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_LineFromText函数构造一条线段，然后使用ST\_IsClosed函数判断该线段是否封闭。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_IsClosed(
      ST_LineFromText(
        'linestring (10.05 10.28 , 20.95 20.89 )'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_IsEmpty函数

ST\_IsEmpty函数用于判断输入的空间几何体是否为空。如果是，则返回true。

### 语法

```plaintext
ST_IsEmpty(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_Point函数构造一个点，然后使用ST\_IsEmpty函数判断该点是否为空。

- 查询和分析语句















```plaintext
* | SELECT ST_IsEmpty(ST_Point(1,1))
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_IsRing函数

ST\_IsRing函数用于判断输入的空间几何体是否为闭合的简单线段（环）。如果是，则返回true。

### 语法

```plaintext
ST_IsRing(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

boolean类型。

### 示例

使用ST\_LineFromText函数构造一条线段，然后使用ST\_IsRing函数判断该线段是否为一个环。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_IsRing(
      ST_LineFromText(
        'linestring (10.05 10.28,20.95 20.89 )'
      )
    )
```

- 查询和分析结果![ST_Crosses](<Base64-Image-Removed>)


## ST\_Length函数

ST\_Length函数使用欧几里得测量法计算线段的二维投影长度。如果存在多条线段，则返回所有线段的长度之和。

### 语法

```plaintext
ST_Length(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_LineFromText函数构造一条线段，然后使用ST\_Length函数计算线段的长度。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_Length(
      ST_LineFromText(
        'linestring (10.05 10.28,20.95 20.89)'
      )
    )
```

- 查询和分析结果![ST_Length](<Base64-Image-Removed>)


## ST\_NumPoints函数

ST\_NumPoints函数用于返回空间几何体中点的个数。

### 语法

```plaintext
ST_NumPoints(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

bigint类型。

### 示例

使用ST\_LineFromText函数构造一条线段，然后使用ST\_NumPoints函数返回线段中点的个数。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_NumPoints(
      ST_LineFromText('linestring (10 10,20 20)')
    )
```

- 查询和分析结果![ST_NumPoints](<Base64-Image-Removed>)


## ST\_NumInteriorRing函数

ST\_NumInteriorRing函数用于计算空间几何体中内部环的数量。

### 语法

```plaintext
ST_NumInteriorRing(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

bigint类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_NumInteriorRing函数返回该几何体中内部环的数量。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_NumInteriorRing(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_NumInteriorRing](<Base64-Image-Removed>)


## ST\_StartPoint函数

ST\_StartPoint函数用于返回线段中的第一个点。

### 语法

```plaintext
ST_StartPoint(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

point类型。

### 示例

使用ST\_LineFromText函数构造一条线段，然后使用ST\_StartPoint函数返回该线段中的第一个点。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_StartPoint(
      ST_LineFromText(
        'linestring (10 10,20 20 )'
      )
    )
```

- 查询和分析结果![ST_StartPoint](<Base64-Image-Removed>)


## ST\_X函数

ST\_X函数用于返回输入点的X轴坐标。

### 语法

```plaintext
ST_X(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为point类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_Point函数构造一个点，然后使用ST\_X函数返回该点的X轴坐标。

- 查询和分析语句















```plaintext
* | SELECT ST_X(ST_Point(1,3))
```

- 查询和分析结果![ST_X](<Base64-Image-Removed>)


## ST\_XMax函数

ST\_XMax函数用于返回空间几何体的第一个最大的X轴坐标。

### 语法

```plaintext
ST_XMax(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_XMax函数返回该空间几何体的第一个最大的X轴坐标。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_XMax(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_XMax](<Base64-Image-Removed>)


## ST\_XMin函数

ST\_XMin函数用于返回空间几何体的第一个最小的X轴坐标。

### 语法

```plaintext
ST_XMin(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_XMin函数返回该空间几何体的第一个最小的X轴坐标。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_XMin(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_XMin](<Base64-Image-Removed>)


## ST\_Y函数

ST\_Y函数用于返回输入点的Y轴坐标。

### 语法

```plaintext
ST_Y(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为point类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_Point函数构造一个点，然后使用ST\_Y函数返回该点的Y轴坐标。

- 查询和分析语句















```plaintext
* | SELECT ST_Y(ST_Point(1,3))
```

- 查询和分析结果![ST_Y](<Base64-Image-Removed>)


## ST\_YMax函数

ST\_YMax函数用于返回空间几何体的第一个最大的Y轴坐标。

### 语法

```plaintext
ST_YMax(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_YMax函数返回该空间几何体的第一个最大的Y轴坐标。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_YMax(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_YMax](<Base64-Image-Removed>)


## ST\_YMin函数

ST\_YMin函数用于返回空间几何体的第一个最小的Y轴坐标。

### 语法

```plaintext
ST_YMin(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为geometry类型。 |

### 返回值类型

double类型。

### 示例

使用ST\_GeometryFromText函数构造一个空间几何体，然后使用ST\_YMin函数返回空间几何体的第一个最小的Y轴坐标。

- 查询和分析语句















```plaintext
* |
SELECT
    ST_YMin(
      ST_GeometryFromText(
        'multipolygon (((10 10,10 20,20 20,20 15,10 10), (50 40,50 50,60 50,60 40,50 40)))'
      )
    )
```

- 查询和分析结果![ST_YMin](<Base64-Image-Removed>)


## bing\_tile函数

bing\_tile函数用于构造一个Bing图块。

### 语法

- 通过X坐标、Y坐标和缩放级别构造一个Bing图块。















```plaintext
bing_tile(x, y, zoom_level)
```

- 通过四叉树键构造一个Bing图块。















```plaintext
bing_tile(quadKey)
```


### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | X坐标，参数值为integer类型。 |
| _y_ | Y坐标，参数值为integer类型。 |
| _zoom\_level_ | 缩放级别，取值范围为\[1,23\]，参数值为integer类型。 |
| _quadKey_ | 四叉树键。 |

### 返回值类型

BingTile类型。

### 示例

- 示例1：通过X坐标、Y坐标和缩放级别构造一个Bing图块。

  - 查询和分析语句















    ```plaintext
    * | SELECT bing_tile(10, 20, 20)
    ```

  - 查询和分析结果![bing_tile](<Base64-Image-Removed>)
- 示例2：通过四叉树键构造一个Bing图块。

  - 查询和分析语句















    ```plaintext
    * | SELECT bing_tile(bing_tile_quadkey(bing_tile(10, 20, 20)))
    ```

  - 查询和分析结果![bing_tile](<Base64-Image-Removed>)

## bing\_tile\_at函数

bing\_tile\_at函数通过经纬度和缩放级别构造一个Bing图块。

### 语法

```plaintext
bing_tile_at(x, y, zoom_level)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 纬度，取值范围为\[-85.05112878,85.05112878\]，参数值为double类型。 |
| _y_ | 经度，取值范围为\[-180,180\]，参数值为double类型。 |
| _zoom\_level_ | 缩放级别，取值范围为\[1,23\]，参数值为integer类型。 |

### 返回值类型

BingTile类型。

### 示例

创建一个Bing图块。

- 查询和分析语句















```plaintext
* | SELECT bing_tile_at(47.265511, -122.465691, 12)
```

- 查询和分析结果![bing_tile_at](<Base64-Image-Removed>)


## bing\_tile\_coordinates函数

bing\_tile\_coordinates函数用于返回目标Bing图块对应的X坐标和Y坐标。

### 语法

```plaintext
bing_tile_coordinates(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为BingTile类型。 |

### 返回值类型

array(integer,integer)类型。

### 示例

通过输入的Bing图块返回对应的X坐标和Y坐标。

- 查询和分析语句















```plaintext
* | SELECT bing_tile_coordinates(bing_tile_at(47.265511, -122.465691, 12))
```

- 查询和分析结果![bing_tile_coordinates](<Base64-Image-Removed>)


## bing\_tile\_polygon函数

bing\_tile\_polygon函数用于返回目标Bing图块的多边形格式。

### 语法

```plaintext
bing_tile_polygon(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为BingTile类型。 |

### 返回值类型

polygon类型。

### 示例

返回Bing图块的多边形格式。

- 查询和分析语句















```plaintext
* | SELECT bing_tile_polygon(bing_tile_at(30.26, 120.19, 12))
```

- 查询和分析结果![bing_tile_polygon](<Base64-Image-Removed>)


## bing\_tile\_quadkey函数

bing\_tile\_quadkey函数用于返回目标Bing图块的四叉树键。

### 语法

```plaintext
bing_tile_quadkey(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为BingTile类型。 |

### 返回值类型

varchar类型。

### 示例

返回目标Bing图块的四叉树键。

- 查询和分析语句















```plaintext
* | SELECT bing_tile_quadkey(bing_tile(10, 20, 20))
```

- 查询和分析结果![bing_tile_quadkey](<Base64-Image-Removed>)


## bing\_tile\_zoom\_level函数

bing\_tile\_zoom\_level函数用于返回目标Bing图块的缩放级别。

### 语法

```plaintext
bing_tile_zoom_level(x)
```

### 参数说明

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| _x_ | 参数值为BingTile类型。 |

### 返回值类型

double类型。

### 示例

返回目标Bing图块的缩放级别。

- 查询和分析语句















```plaintext
* | SELECT bing_tile_zoom_level(bing_tile(10, 20, 20))
```

- 查询和分析结果![bing_tile_zoom_level](<Base64-Image-Removed>)