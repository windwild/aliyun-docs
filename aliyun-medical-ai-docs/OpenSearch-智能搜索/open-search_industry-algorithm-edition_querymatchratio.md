### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava/)[Cava Lib](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava-lib-1/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/com-aliyun-opensearch-cava-features/)QueryMatchRatio

# QueryMatchRatio

更新时间：2023-12-26 21:04:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：FirstPhaseScore](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/firstphasescore)[下一篇：QueryMinSlideWindow](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/queryminslidewindow)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

函数列表

函数详情

## 简介

计算查询词中命中的词组与总词组的比值。OpenSearch支持一个索引中包含多个字段，检索时只要查询词在其中一个字段上命中文档就可以返回。因此QueryMatchRatio有两种计算方式，一种是查询词中在被检索索引包含的所有字段上命中的词与总词组的比值，一种是查询词中在被检索索引包含的某一个字段上命中的词与总词组的比值。比如default索引包含title和body两个字段，查询词为`default:'使用手册'`，我们可以计算查询词中在default索引下所有字段上（title和body）命中的词组与总词组个数的比值，也可以计算查询词只在title或者body上命中的词组与总词组的比值。

## 函数列表

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| QueryMatchRatio create(OpsScorerInitParams params) | 构造QueryMatchRatio，计算查询词中在检索索引下所有字段上命中的词与总词组的比值 |
| QueryMatchRatio create(OpsScorerInitParams params, CString indexName) | 构造QueryMatchRatio，计算查询词中在指定索引下所有字段上命中的词与总词组的比值 |
| QueryMatchRatio create(OpsScorerInitParams params, CString indexName, CString fieldName) | 构造QueryMatchRatio，计算查询词中在指定索引下某个字段上命中的词与总词组的比值 |
| void setGroupScoreMergeOp(CString opName) | 设置多个query group结果的merge方式，可以是sum和max，默认为sum。 |
| double evaluate(OpsScoreParams params) | 计算查询词中命中的词组与总词组的比值 |

## 函数详情

**QueryMatchRatio(OpsScorerInitParams params)**

构造QueryMatchRatio对象，计算查询词中在检索索引下所有字段上命中的词与总词组的比值。参数列表：params — 初始化输入参数，详情请参考OpsScorerInitParams手册。

**QueryMatchRatio(OpsScorerInitParams params, CString indexName)**

构造QueryMatchRatio对象，计算查询词中在检索索引下某一索引上命中的词与总词组的比值。参数列表：params — 初始化输入参数，详情请参考OpsScorerInitParams手册。indexName — 待匹配的索引名，分词类型为中文基础分词、自定义分词、单字分词、英文分词、模糊分词，必须是常量。

**QueryMatchRatio(OpsScorerInitParams params, CString indexName, CString fieldName)**

构造QueryMatchRatio对象，计算查询词中在检索索引下某一索引下的一个字段上命中的词与总词组的比值。参数列表：params — 初始化输入参数，详情请参考 [OpsScorerInitParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscorerinitparams)。indexName — 待匹配的索引名，分词类型为中文基础分词、自定义分词、单字分词、英文分词、模糊分词，必须是常量。fieldName — 待匹配的字段名，该字段包含在索引indexName中。必须是常量。

**void setGroupScoreMergeOp(CString opName)**

设置多个查询分组之间分数组合规则，目前仅支持max、sum，如果没有设置默认多个group分数进行sum。该函数必须在算分插件初始化阶段调用。查询分组是指经过查询分析处理之后对原始查询词进行的扩展，默认只有一个查询分组。参数列表：opName — 多个查询分组分数组合规则，目前支持max与sum。

**double evaluate(OpsScoreParams params)**

计算查询词中命中的词组与总词组的比值。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。返回值：返回查询词中命中的词组与总词组的比值，取值范围为\[0, 1\]。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.similarity.querymatch.QueryMatchRatio;

class BasicSimilarityScorer {
    QueryMatchRatio _f1;
    QueryMatchRatio _f2;
    boolean init(OpsScorerInitParams params) {
        _f1 = QueryMatchRatio.create(params, "title_index");
        _f2 = QueryMatchRatio.create(params);
        return true;
    }

    double score(OpsScoreParams params) {
        return _f1.evaluate(params) + _f2.evaluate(params);
    }
}
```