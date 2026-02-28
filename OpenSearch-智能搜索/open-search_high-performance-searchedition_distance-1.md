### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-a-language-for-developing-sort-plug-ins/)[Cava Lib](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-lib/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/high-performance-searchedition/com-aliyun-opensearch-cava/)Distance

# Distance

更新时间：2024-01-07 21:46:06

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Popularity](https://help.aliyun.com/zh/open-search/high-performance-searchedition/popularity)[下一篇：TagMatch](https://help.aliyun.com/zh/open-search/high-performance-searchedition/tagmatch)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

函数列表

函数详情

## 简介

Distance用户计算两个点之间的球面距离，主要用于按照距离远近进行排序或者根据距离进行不同处理。参与Distance计算的两个点，一个来自于文档，一个来自于请求中的自定义参数。自定义参数是指在构造查询请求时在kvpairs中添加的参数，可以通过opensearch的SDK或者手动构造kvpairs子句来添加自定义参数。

## 函数列表

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| Distance create(OpsScorerInitParams params,CString longitudeAFieldName, CString latitudeAFieldName, CString longitudeBRequestKeyName,CString latitudeBRequestKeyName) | 使用A、B两个点的坐标构造Distance对象 |
| Distance create(OpsScorerInitParams params,CString longitudeAFieldName, CString latitudeAFieldName, CString longitudeBRequestKeyName, CString latitudeBRequestKeyName, CString outputName) | 使用A、B两个点的坐标构造Distance对象，并在文档中通过outputName输出距离值 |
| Distance create(OpsScorerInitParams params,CString geoPointAFieldName, CString geoPointBRequestKeyName) | 使用A、B两个GEO\_POINT类型的点构造Distance对象 |
| Distance create(OpsScorerInitParams params,CString geoPointAFieldName, CString geoPointBRequestKeyName, CString outputName) | 使用A、B两个GEO\_POINT类型的点构造Distance对象，并在文档中通过outputName输出距离值 |
| Distance create(OpsScorerInitParams params,CString geoPointAFieldName, CString geoPointBRequestKeyName, CString outputName, float defaultValue) | 使用A、B两个GEO\_POINT类型的点构造Distance对象，并在文档中通过outputName输出距离值 |
| double evaluate(OpsScoreParams params) | 计算两点之间的球面距离 |

## 函数详情

**Distance create(OpsScorerInitParams params, CString longitudeAFieldName, CString latitudeAFieldName, CString longitudeBRequestKeyName, CString latitudeBRequestKeyName)**

创建Distance对象，需要分别指定A、B两个点的经度和纬度，其中点A的经度和纬度来自于文档中的指定字段，点B的经度和纬度来自于查询请求中自定义参数。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。longitudeAFieldName — 属性字段名称，代表点A的经度，必须是常量。latitudeAFieldName — 属性字段名称，代表点A的纬度，必须是常量。longitudeBRequestKeyName — 自定义参数名称，代码点B的经度，必须是常量。latitudeBRequestKeyName — 自定义参数名称，代码点B的纬度，必须是常量。

代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Distance;

class BasicSimilarityScorer {
    Distance _distance;

    boolean init(OpsScorerInitParams params) {
        _distance = Distance.create(params, "longitudeInDoc", "latitudeInDoc",
                                    "longitudeInRequest", "latitudeInRequest");
        return true;
    }

    double score(OpsScoreParams params) {
        return _distance.evaluate(params);
    }
}
```

**Distance create(OpsScorerInitParams params, CString longitudeAFieldName, CString latitudeAFieldName, CString longitudeBRequestKeyName, CString latitudeBRequestKeyName, CString outputName)**

创建Distance对象，需要分别指定A、B两个点的经度和纬度，其中点A的经度和纬度来自于文档中的指定字段，点B的经度和纬度来自于查询请求中自定义参数。Distance计算之后，会在文档中新增一个outputName字段来存储计算结果。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。longitudeAFieldName — 属性字段名称，代表点A的经度，必须是常量。latitudeAFieldName — 属性字段名称，代表点A的纬度，必须是常量。longitudeBRequestKeyName — 自定义参数名称，代码点B的经度，必须是常量。latitudeBRequestKeyName — 自定义参数名称，代码点B的纬度，必须是常量。outputName — distance分数输出在文档中的字段名称，必须是常量。

代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Distance;

class BasicSimilarityScorer {
    Distance _distance;

    boolean init(OpsScorerInitParams params) {
        _distance = Distance.create(params, "longitudeInDoc", "latitudeInDoc",
                                    "longitudeInRequest", "latitudeInRequest", "output");
        return true;
    }

    double score(OpsScoreParams params) {
        return _distance.evaluate(params);
    }
}
```

**Distance create(OpsScorerInitParams params, CString geoPointAFieldName, CString geoPointBRequestKeyName)**

创建Distance对象，需要以GEO\_POINT的形式指定A、B两个点的坐标，其中A点为文档中的GEO\_POINT字段，B点为请求中自定义的参数。在定义B时，经度和维度需要使用空格分开，经度在前，维度在后，例如pointB:12.0 34.5。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。geoPointAFieldName — GEO\_POINT类型的属性字段名称，代表点A的坐标，必须是常量。geoPointBRequestKeyName — 请求中自定义参数名称，代码点B的坐标，必须是常量。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Distance;

class BasicSimilarityScorer {
    Distance _distance;
    boolean init(OpsScorerInitParams params) {
        _distance = Distance.create(params, "location", "locationInRequest");
        return true;
    }

    double score(OpsScoreParams params) {
        return _distance.evaluate(params);
    }
}
```

**Distance create(OpsScorerInitParams params, CString geoPointAFieldName, CString geoPointBRequestKeyName, CString outputName)**

创建Distance对象，需要以GEO\_POINT的形式指定A、B两个点的坐标，其中A点为文档中的GEO\_POINT字段，B点为请求中自定义的参数。在定义B时，经度和维度需要使用空格分开，经度在前，维度在后，例如pointB:12.0 34.5。Distance计算之后，会在文档中新增一个outputName字段来存储计算结果。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。geoPointAFieldName — GEO\_POINT类型的属性字段名称，代表点A的坐标，必须是常量。geoPointBRequestKeyName — 请求中自定义参数名称，代码点B的坐标，必须是常量。outputName — distance分数输出在文档中的字段名称，必须是常量。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Distance;

class BasicSimilarityScorer {
    Distance _distance;
    boolean init(OpsScorerInitParams params) {
        _distance = Distance.create(params, "location", "locationInRequest", "output");
        return true;
    }

    double score(OpsScoreParams params) {
        return _distance.evaluate(params);
    }
}
```

**Distance create(OpsScorerInitParams params, CString geoPointAFieldName, CString geoPointBRequestKeyName, CString outputName, float defaultValue)**

创建Distance对象，需要以GEO\_POINT的形式指定A、B两个点的坐标，其中A点为文档中的GEO\_POINT字段，B点为请求中自定义的参数。在定义B时，经度和维度需要使用空格分开，经度在前，维度在后，例如pointB:12.0 34.5。Distance计算之后，会在文档中新增一个outputName字段来存储计算结果。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。geoPointAFieldName — GEO\_POINT类型的属性字段名称，代表点A的坐标，必须是常量。geoPointBRequestKeyName — 请求中自定义参数名称，代码点B的坐标，必须是常量。outputName — distance分数输出在文档中的字段名称，必须是常量。defaultValue — 如果输入的A、B坐标非法，返回该值。

代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Distance;

class BasicSimilarityScorer {
    Distance _distance;
    boolean init(OpsScorerInitParams params) {
        _distance = Distance.create(params, "location", "locationInRequest", "output", 100.0);
        return true;
    }

    double score(OpsScoreParams params) {
        return _distance.evaluate(params);
    }
}
```

**double evaluate(OpsScoreParams params)**

Distance的算分接口，返回两点间的球面距离。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。返回值：返回两点间的球面距离。