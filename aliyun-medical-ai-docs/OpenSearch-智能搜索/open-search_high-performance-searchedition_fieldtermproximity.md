### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/)[开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-a-language-for-developing-sort-plug-ins/)[Cava Lib](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-lib/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/high-performance-searchedition/com-aliyun-opensearch-cava/)FieldTermProximity

# FieldTermProximity

更新时间：2025-03-13 01:29:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：FieldTermMatchCount](https://help.aliyun.com/zh/open-search/high-performance-searchedition/fieldtermmatchcount)[下一篇：FirstPhaseScore](https://help.aliyun.com/zh/open-search/high-performance-searchedition/firstphasescore)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

函数列表

本文主要介绍FieldTermProximity包含的函数原型以及使用方式。

## 简介

计算查询词分词词组在指定索引和字段上分布的紧密程度。紧密度可以在一定程度上衡量查询词和字段的相关性，比如查询词为：用户手册，字段1的内容为：`开放搜索用户手册`，字段2的内容为：`用户使用开放搜索手册解决问题`。这时候查询词在字段1上的紧密度要大于字段2上的紧密度，而且从字面上可以判断出来查询词和字段1的相关性更好。另外通过紧密度分数我们也能判断出来查询词是否在字段上是连续紧密分布的。

## 函数列表

| 函数原型 | 函数简介 | 函数详情 |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| 函数原型 | 函数简介 | 函数详情 |
| FieldTermProximity create(OpsScorerInitParams params, CString indexName, CString fieldName) | 构造FieldTermProximity。 | 构造FieldTermProximity对象，需要指定待匹配的字段名称。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。indexName — 指定的索引名，必须是常量。fieldName — 待匹配的字段名，该字段需要为TEXT或者SHORT\_TEXT，并且分词类型为中文基础分词、自定义分词、单字分词、英文分词、模糊分词必须是常量。 |
| void setGroupScoreMergeOp(CString opName) | 设置多个query group结果的merge方式，可以是sum和max，默认为sum。 | 设置有多个query group时，多个group的分数如何计算。需要在init函数中调用。参数列表：opName — 算子名称，目前支持的算子名称：sum 和 max。sum：表示求和，max：表示求最大值。默认为sum。 |
| double evaluate(OpsScoreParams params) | 计算查询词分词词组在字段上分布的紧密程度。 | 计算查询词分词词组在字段上分布的紧密程度。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。返回值：返回查询词在字段上的紧密度，取值范围为\[0, 1\]。代码示例请参见下文。 |

代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.similarity.distribution.FieldTermProximity;

class BasicSimilarityScorer {
    FieldTermProximity _proximity;
    boolean init(OpsScorerInitParams params) {
        _proximity = FieldTermProximity.create(params, "text_index","text");
        _proximity.setGroupScoreMergeOp("max");
        return true;
    }

    double score(OpsScoreParams params) {
        return _proximity.evaluate(params);
    }
}
```