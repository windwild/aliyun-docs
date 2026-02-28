### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava/)[Cava Lib](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava-lib-1/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/com-aliyun-opensearch-cava-features/)TextRelevance

# TextRelevance

更新时间：2023-12-26 21:50:12

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：QueryTermMatchCount](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/querytermmatchcount)[下一篇：TextRelevanceLLM](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/textrelevancellm-cava)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

函数列表

函数详情

## 简介

计算查询词在指定索引和字段上的文本相关性。TextRelevance主要从下面几个维度衡量相关性：命中词在查询词中所占比重；命中词在字段中所占比重；命中词在字段中出现的频率；字段中命中词之间的顺序关系与查询词中命中词之间的顺序关系。分数越大表名查询词语字段越相关。从实现上讲，TextRelevance是 [FieldMatchWeighted](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/fieldmatchweighted)、 [BM25](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/bm25)、 [FieldTermProximity](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/fieldtermproximity) 三个feature的组合，可以通TextRelevance提供的接口对这些feature的权重进行调整，从而定制自己的TextRelevance。

## 函数列表

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| TextRelevance create(OpsScorerInitParams params,CString indexName, CString fieldName) | 创建TextRelevance |
| void setGroupScoreMergeOp(CString opName) | 设置多个query group结果的merge方式，可以是sum和max，默认为sum。 |
| void setFieldBm25Weight(double weight) | 设置bm25的权重 |
| void setFieldMatchWeightedWeight(double weight) | 设置FieldMatchWeighted的权重 |
| void setFieldTermProximityWeight(double weight) | 设置FieldTermProximity的权重 |
| double evaluate(OpsScoreParams params) | 计算查询词在指定字段上的文本相关性 |

## 函数详情

**TextRelevance create(OpsScorerInitParams params,CString indexName, CString fieldName)**

创建TextRelevance对象，用于计算查询词与指定索引下的指定字段的相关性。参数列表：params — 算分输入参数，详情请参考 [OpsScorerInitParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscorerinitparams)。indexName — 指定的索引名，必须是常量。fieldName — 索引下的字段名，该字段需要为TEXT或者SHORT\_TEXT，并且分词类型为中文基础分词、自定义分词、单字分词、英文分词、模糊分词，必须是常量。

**void setGroupScoreMergeOp(CString opName)**

设置多个查询分组之间分数组合规则，目前仅支持max、sum，如果没有设置默认多个group分数进行sum。该函数必须在算分插件初始化阶段调用。查询分组是指经过查询分析处理之后对原始查询词进行的扩展，默认只有一个查询分组。参数列表：opName — 多个查询分组分数组合规则，目前支持max与sum。

**void setFieldBm25Weight(double weight)**

设置Bm25的权重，必须在算分插件初始化阶段调用，默认权重为0.5。参数列表：weight — 权重值。

**void setFieldMatchWeightedWeight(double weight)**

设置MatchWeighted权重，必须在算分插件初始化阶段调用，默认权重为5。参数列表：weight — 权重值。

**void setFieldTermProximityWeight(double weight)**

设置TermProximity权重，必须在算分插件初始化阶段调用，默认权重为9。参数列表：weight — 权重值。

**double evaluate(OpsScoreParams params)**

计算查询词在指定索引的指定字段上的文本相关性。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。返回值：返回查询词在字段上的文本相关性，取值范围为\[0, 1\]。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.similarity.TextRelevance;

class BasicSimilarityScorer {
    TextRelevance _f1;
    boolean init(OpsScorerInitParams params) {
        _f1 = TextRelevance.create(params, "text_index", "text");
        _f1.setGroupScoreMergeOp("max");
        _f1.setFieldBm25Weight(2);
        _f1.setFieldMatchWeightedWeight(3);
        _f1.setFieldTermProximityWeight(4);
        return true;
    }

    double score(OpsScoreParams params) {
        return _f1.evaluate(params);
    }
}
```