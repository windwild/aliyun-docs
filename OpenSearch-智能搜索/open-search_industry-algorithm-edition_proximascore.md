### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[排序插件 Cava](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava/)[Cava Lib](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/cava-lib-1/)[com.aliyun.opensearch.cava.features](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/com-aliyun-opensearch-cava-features/)ProximaScore

# ProximaScore

更新时间：2024-01-07 22:28:09

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Util](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/util)[下一篇：basicSimilarityScore](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/basicsimilarityscorer)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

构造函数

函数列表

函数详情

ProximaScore create(OpsScorerInitParams params, CString indexName)

double evaluate(OpsScoreParams params)

获取查询中向量索引的相似度分数。

## 构造函数

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| ProximaScore create(OpsScorerInitParams params, CString indexName) | 构造ProximaScore。 |

## 函数列表

| 函数原型 | 函数简介 |
| --- | --- |

|     |     |
| --- | --- |
| 函数原型 | 函数简介 |
| double evaluate(OpsScoreParams params) | 获取指定索引的相似度分数。 |

## 函数详情

### ProximaScore create(OpsScorerInitParams params, CString indexName)

工厂函数，构造ProximaScore对象。

params -- 初始化输入参数，详情请参考 [OpsScoreParams](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams "") 手册。

indexName -- 向量索引的名称，必须是查询中出现的向量索引名。

### double evaluate(OpsScoreParams params)

计算向量相似度分数。

参数列表：

params --算分输入参数，详情请参考 [OpsScoreParams](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/opsscoreparams "") 手册。

返回值：

返回指定索引的向量相似度分数。

代码示例：

```javascript
package users.scorer;
import com.aliyun.opensearch.cava.framework.OpsScoreParams;
import com.aliyun.opensearch.cava.framework.OpsScorerInitParams;
import com.aliyun.opensearch.cava.framework.OpsRequest;
import com.aliyun.opensearch.cava.framework.OpsDoc;
import com.aliyun.opensearch.cava.features.similarity.ProximaScore;

class BasicSimilarityScorer {
    ProximaScore _f1;
    boolean init(OpsScorerInitParams params) {
        _f1 = ProximaScore.create(params, "vector_index");
        return true;
    }

    double score(OpsScoreParams params) {
        OpsDoc doc = params.getDoc();
        float s1 = _f1.evaluate(params);
        return s1;
    }
};
```