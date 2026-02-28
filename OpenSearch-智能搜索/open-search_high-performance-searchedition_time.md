### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-a-language-for-developing-sort-plug-ins/)[Cava Lib](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-lib/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/high-performance-searchedition/com-aliyun-opensearch-cava/)Time

# Time

更新时间：2024-01-12 04:24:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：KeyWordsMatched](https://help.aliyun.com/zh/open-search/high-performance-searchedition/keywordsmatched)[下一篇：Util](https://help.aliyun.com/zh/open-search/high-performance-searchedition/util)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

函数列表

函数详情

## 简介

Time类提供了一系列与时间操作相关的函数，用户可以通过这些函数获取当前时间，判断一个文档的新旧程度。

## 函数列表

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| static long now() | 获取当前时间，返回从1970-01-01 00:00:00到现在的秒数 |
| static float timeliness(long pubTime) | 计算时效性分数 |
| static float timelinessMs(long pubTime) | 计算时效性分数 |

## 函数详情

**static long now()**

获取当前时间。返回值：返回从1970-01-01 00:00:00到现在的秒数。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Time;

class BasicSimilarityScorer {
    boolean init(OpsScorerInitParams params) {
        return true;
    }

    double score(OpsScoreParams params) {
        long current = Time.now();
        params.getDoc().trace(current);
        return current;
    }
}
```

**static float timeliness(long pubTime)**

计算文档的时效性分数，用于衡量文档的新旧程度。pubTime越靠近当前时间，时效性分数越大，表示文档越新。参数列表：pubTime — 文档更新时间，时间单位为秒。返回值：返回文档的失效分，取值范围为\[0, 1\]，如果pubTime小于0或者大于（或者等于）当前时间返回0。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Time;

class BasicSimilarityScorer {
    boolean init(OpsScorerInitParams params) {
        return true;
    }

    double score(OpsScoreParams params) {
        long current = Time.now() - 1;
        double score = Time.timeliness(current);
        return score;
    }
}
```

**static float timelinessMs(long pubTime)**

计算文档的时效性分数，用于衡量文档的新旧程度。pubTime越靠近当前时间，时效性分数越大，表示文档越新。参数列表：pubTime — 文档更新时间，时间单位为毫秒。返回值：返回文档的失效分，取值范围为\[0, 1\]，如果pubTime小于0或者大于（或者等于）当前时间返回0。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.Time;

class BasicSimilarityScorer {
    boolean init(OpsScorerInitParams params) {
        return true;
    }

    double score(OpsScoreParams params) {
        long current = (Time.now() - 1) * 1000;
        double score = Time.timelinessMs(current);
        return score;
    }
}
```