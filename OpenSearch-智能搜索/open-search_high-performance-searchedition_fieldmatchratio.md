### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/) [OpenSearch-高性能检索版](https://help.aliyun.com/zh/open-search/high-performance-searchedition/) [开发指南](https://help.aliyun.com/zh/open-search/high-performance-searchedition/development-guide/) [排序插件 Cava](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-a-language-for-developing-sort-plug-ins/) [Cava Lib](https://help.aliyun.com/zh/open-search/high-performance-searchedition/cava-lib/) [com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/high-performance-searchedition/com-aliyun-opensearch-cava/) FieldMatchRatio

# FieldMatchRatio

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：FieldLength](https://help.aliyun.com/zh/open-search/high-performance-searchedition/fieldlength)[下一篇：FieldTermMatchCount](https://help.aliyun.com/zh/open-search/high-performance-searchedition/fieldtermmatchcount)

该文章对您有帮助吗？

反馈

## 简介

计算查询词和字段的匹配程度，计算逻辑为查询词在字段上匹配的分词词组个数与该字段总词组个数的比值。例子：假设字段title分词之后为：`fieldmatchratio使用手册`，查询词分词后为：`OpenSearch使用手册`。那么查询词在title字段上的FieldMatchRatio计算得分为2（匹配的词组个数）/5（field总词组个数）= 0.4。

## 函数列表

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| FieldMatchRatio create(OpsScorerInitParams params, CString indexName, CString fieldName) | 创建一个FieldMatchRatio对象 |
| void setGroupScoreMergeOp(CString opName) | 设置多个query group结果的merge方式，可以是sum和max，默认为sum。 |
| double evaluate(OpsScoreParams params) | 计算查询词和字段的匹配度 |

## 函数详情

**FieldMatchRatio create(OpsScorerInitParams params, CString indexName, CString fieldName)**

工厂函数，构造FieldMatchRatio对象，需要指定待匹配的索引名称和字段名称。参数列表：params — 初始化输入参数，详情请参考OpsScorerInitParams手册。indexName — 待匹配的索引名，分词类型为中文基础分词、自定义分词、单字分词、英文分词、模糊分词，必须是常量。fieldName — 待匹配的字段名，该字段需要为TEXT或者SHORT\_TEXT，必须是常量。

**void setGroupScoreMergeOp(CString opName)**

设置有多个query group时，多个group的分数如何计算。需要在init函数中调用。参数列表：opName — 算子名称，目前支持的算子名称：sum 和 max。sum: 表示求和，max: 表示求最大值。默认为sum。

**double evaluate(OpsScoreParams params)**

计算查询词和字段的匹配度。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。返回值：返回查询词和字段的匹配程度，取值范围为\[0, 1\]。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.features.similarity.fieldmatch.FieldMatchRatio;

class BasicSimilarityScorer {
    FieldMatchRatio _fieldMathcRatio;
    boolean init(OpsScorerInitParams params) {
        _fieldMatchRatio = FieldMatchRatio.create(params, "title_index", "title");
        _fieldMatchRatio.setGroupScoreMergeOp("max");
        return true;
    }

    double score(OpsScoreParams params) {
        return _fieldMathcRatio.evaluate(params);
    }
}
```