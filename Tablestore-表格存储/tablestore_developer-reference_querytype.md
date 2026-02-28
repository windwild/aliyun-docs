### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储 Tablestore](https://help.aliyun.com/zh/tablestore/) [开发参考](https://help.aliyun.com/zh/tablestore/developer-reference/) [API参考（数据管理）](https://help.aliyun.com/zh/tablestore/developer-reference/api-reference/) [DataType定义](https://help.aliyun.com/zh/tablestore/developer-reference/ablestore-datatype-definition/) QueryType

# QueryType

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：QueryOperator](https://help.aliyun.com/zh/tablestore/developer-reference/queryoperator)[下一篇：Range](https://help.aliyun.com/zh/tablestore/developer-reference/range)

该文章对您有帮助吗？

反馈

QueryType数据类型定义，表示多元索引的查询类型。

## **枚举取值列表**

- MATCH\_QUERY表示匹配查询。

- MATCH\_PHRASE\_QUERY表示短语匹配查询。

- TERM\_QUERY表示精确查询。

- RANGE\_QUERY表示范围查询。

- PREFIX\_QUERY表示前缀查询。

- BOOL\_QUERY表示多条件组合查询。

- CONST\_SCORE\_QUERY表示使用固定分数的相关性查询。

- FUNCTION\_SCORE\_QUERY表示使用自定义分数算法的相关性查询。

- NESTED\_QUERY表示嵌套查询。

- WILDCARD\_QUERY表示通配符查询。

- MATCH\_ALL\_QUERY表示全匹配查询。

- GEO\_BOUNDING\_BOX\_QUERY表示地理长方形范围查询。

- GEO\_DISTANCE\_QUERY表示地理距离查询。

- GEO\_POLYGON\_QUERY表示地理多边形范围查询。

- TERMS\_QUERY表示多词精确查询。

- EXISTS\_QUERY表示列存在性查询。

- KNN\_VECTOR\_QUERY表示向量检索。

- FUNCTIONS\_SCORE\_QUERY表示函数评分查询。

- SUFFIX\_QUERY表示后缀查询。


```protobuf
enum QueryType {
    MATCH_QUERY = 1;
    MATCH_PHRASE_QUERY = 2;
    TERM_QUERY = 3;
    RANGE_QUERY = 4;
    PREFIX_QUERY = 5;
    BOOL_QUERY = 6;
    CONST_SCORE_QUERY = 7;
    FUNCTION_SCORE_QUERY = 8;
    NESTED_QUERY = 9;
    WILDCARD_QUERY = 10;
    MATCH_ALL_QUERY = 11;
    GEO_BOUNDING_BOX_QUERY = 12;
    GEO_DISTANCE_QUERY = 13;
    GEO_POLYGON_QUERY = 14;
    TERMS_QUERY = 15;
    EXISTS_QUERY = 16;
    KNN_VECTOR_QUERY = 17;
    FUNCTIONS_SCORE_QUERY = 18;
    SUFFIX_QUERY = 19;
}
```