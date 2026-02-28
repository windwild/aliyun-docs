### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-a-language-for-developing-sort-plug-ins/)[Cava Lib](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-lib/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/high-performance-searchedition/com-aliyun-opensearch-cava/)QueryMinSlideWindow

# QueryMinSlideWindow

更新时间：2024-01-24 02:23:31

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：QueryMatchRatio](https://help.aliyun.com/zh/open-search/high-performance-searchedition/querymatchratio)[下一篇：QueryTermCount](https://help.aliyun.com/zh/open-search/high-performance-searchedition/querytermcount)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

函数列表

函数详情

## 简介

计算查询词在某个字段上命中的分词词组个数与该词组在字段上的最小窗口的比值。在构建索引时，字段分词之后，OpenSearch会为每一个词组分配一个位置ID（每个字段都从0开始）。例如字段title的分词之后为：开放 搜索 用户 手册，位置ID分别为0、1、2、3。假设查询词分词之后为：搜索 手册，那么在计算QueryMinSlideWindow(title)时命中的词组个数为2，最小窗口为3。

## 函数列表

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| QueryMinSlideWindow create(OpsScorerInitParams params, CString indexName, CString fieldName) | 构造QueryMinSlideWindow对象 |
| QueryMinSlideWindow create(OpsScorerInitParams params, CString indexName, CString fieldName, boolean inOrder) | 构造QueryMinSlideWindow对象，并指定计算最小窗口时是否需要保序 |
| double evaluate(OpsScoreParams params) | 计算查询词中命中的词组与总词组的比值 |

## 函数详情

**QueryMinSlideWindow create(OpsScorerInitParams params, CString indexName, CString fieldName)**

构造QueryMinSlideWindow对象，计算查询词在某个字段上命中的分词词组个数与该词组在字段上的最小窗口的比值。参数列表：params — 算分输入参数，详情请参考OpsScorerInitParams.indexName — 指定的索引名，分词类型为中文基础分词、自定义分词、单字分词、英文分词、模糊分词，必须是常量。fieldName — 待匹配的字段名，该字段需要为TEXT或者SHORT\_TEXT，必须是常量。

**QueryMinSlideWindow create(OpsScorerInitParams params, CString indexName, CString fieldName, boolean inOrder)**

构造QueryMinSlideWindow对象，计算查询词在某个字段上命中的分词词组个数与该词组在字段上的最小窗口的比值，在计算最小窗口过程中可以指定窗口中的词组是否和查询词保持一致的顺序。参数列表：params — 算分输入参数，详情请参考OpsScorerInitParams.indexName — 指定的索引名，分词类型为中文基础分词、自定义分词、单字分词、英文分词、模糊分词，必须是常量。fieldName — 待匹配的字段名，该字段需要为TEXT或者SHORT\_TEXT，必须是常量。inOrder — 取值为false或者true，为false表示不要保序，为true表示需要保序。

**double evaluate(OpsScoreParams params)**

计算查询词在某个字段上命中的分词词组个数与该词组在字段上的最小窗口的比值。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。返回值：返回查询词在某个字段上命中的分词词组个数与该词组在字段上的最小窗口的比值，取值范围为\[0, 1\]。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.similarity.distribution.QueryMinSlideWindow;

class BasicSimilarityScorer {
    QueryMinSlideWindow _f1;
    QueryMinSlideWindow _f2;
    boolean init(OpsScorerInitParams params) {
        _f1 = QueryMinSlideWindow.create(params, "pack_index1", "text_field");
        _f2 = QueryMinSlideWindow.create(params, "pack_index1", "text_field", true);
        return true;
    }

    double score(OpsScoreParams params) {
        return _f1.evaluate(params) + _f2.evaluate(params);
    }
}
```