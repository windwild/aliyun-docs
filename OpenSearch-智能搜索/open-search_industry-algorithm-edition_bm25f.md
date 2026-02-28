### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava/)[Cava Lib](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava-lib-1/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/com-aliyun-opensearch-cava-features/)BM25F

# BM25F

更新时间：2023-11-30 02:44:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：BM25](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/bm25)[下一篇：KeyWordsMatched](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/keywordsmatched)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

简介

函数列表

函数详情

## 简介

BM25F是在BM25的基础上，计算查询词在多个字段上的文本相关性。每个字段可以设置不同的权重，BM25F对多个字段的BM25分数进行整合。BM25F的计算公式可以表示如下：![1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9461288161/p265475.png)![2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9461288161/p265476.png)

## 函数列表

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| BM25F create(OpsScorerInitParams params,CString indexName) | 工厂函数，创建BM25F对象，指定索引名称 |
| BM25F create(OpsScorerInitParams params,CString indexName, CString\[\] fields) | 工厂函数，创建BM25F对象，指定索引名称以及该索引下的字段名称。 |
| void setGroupScoreMergeOp(CString opName) | 设置多个query group结果的merge方式，可以是sum和max，默认为sum。 |
| void setParamK(double paramK) | 设置参数K |
| void setFieldParamB(CString fieldName, double paramB) | 设置某个字段的参数B |
| void setTotalDocNum(long totalDocNum) | 设置总文档数 |
| void setFieldAvgLength(CString fieldName, int avgFieldLength) | 设置某个字段的平均长度 |
| void setFieldWeight(CString fieldName, double fieldWeight) | 设置某个字段的权重 |
| double evaluate(OpsScoreParams params) | 计算查询词在指定字段上的匹配度 |

## 函数详情

**BM25F create(OpsScorerInitParams params,CString indexName)**

创建BM25F对象，需要指定待匹配的索引名称。没有指定字段名时，默认该索引下的所有字段都参与BM25F的计算。参数列表：params — 初始化输入参数，详情请参考 [OpsScorerInitParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscorerinitparams)。indexName — 索引名，必须是常量。

**BM25F create(OpsScorerInitParams params,CString indexName, CString\[\] fields)**

创建BM25F对象，需要指定待匹配的索引名称与参与计算的字段列表。参数列表：params — 初始化输入参数，详情请参考 [OpsScorerInitParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscorerinitparams)。indexName — 索引名，必须是常量。fields — 需要参与BM25F计算的字段列表。

**void setGroupScoreMergeOp(CString opName)**

设置多个查询分组之间分数组合规则，目前仅支持max、sum，如果没有设置默认多个group分数进行sum。该函数必须在算分插件初始化阶段调用。查询分组是指经过查询分析处理之后对原始查询词进行的扩展，默认只有一个查询分组。参数列表：opName — 多个查询分组分数组合规则，目前支持max与sum。

**void setParamK(double paramK)**

设置参数![1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0561288161/p265477.png)的值，该函数必须在算分插件初始化阶段调用。参数列表：paramK — ![1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0561288161/p265478.png)的值，默认为2.0。

**void setFieldParamB(CString fieldName, double paramB)**

设置计算字段BM25时参数B的值，该函数必须在算分插件初始化阶段调用。参数列表：fieldName — 字段名称，字段需要为指定索引中含有的字段，如果在创建BM25F对象是指定了字段列表，fieldName需要在字段列表中出现，需要为字符串常量。paramB — b的值，默认为0.1。

**void setTotalDocNum(long totalDocNum)**

设置应用的文档个数，该函数必须在算分插件初始化阶段调用。参数列表：totalDocNum — 文档个数，默认为92000000。

**void setFieldAvgLength(CString fieldName, int avgFieldLength)**

设置字段的平均长度，该函数必须在算分插件初始化阶段调用。参数列表：fieldName — 字段名称，字段需要为指定索引中含有的字段，如果在创建BM25F对象是指定了字段列表，fieldName需要在字段列表中出现，需要为字符串常量。avgFieldLength — 字段的平均长度，默认为20。

**void setFieldWeight(CString fieldName, double fieldWeight)**

设置字段的权重，该函数必须在算分插件初始化阶段调用。参数列表：fieldName — 字段名称，字段需要为指定索引中含有的字段，如果在创建BM25F对象是指定了字段列表，fieldName需要在字段列表中出现，需要为字符串常量。fieldWeight — 字段的权重，默认为1.0。

**double evaluate(OpsScoreParams params)**

计算BM25F的值。参数列表：params — 算分输入参数，详情请参考 [OpsScoreParams手册](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams)。返回值：BM25F分数，取值范围为\[0, 1\]。代码示例：

```java
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.features.similarity.fieldmatch.BM25F;

class BasicSimilarityScorer {
    BM25F _f1;
    boolean init(OpsScorerInitParams params) {
        CString[] fields1 = {"title", "body"};
        _f1 = BM25F.create(params, "default", fields1);
        _f1.setFieldAvgLength("title", 10);
        _f1.setFieldWeight("title", 10D);
        _f1.setFieldParamB("title", 0.6);

        _f1.setFieldAvgLength("body", 100);
        _f1.setFieldWeight("body", 2D);
        _f1.setFieldParamB("body", 0.5);
        return true;
    }

    double score(OpsScoreParams params) {
        return _f1.evaluate(params);
    }
};
```