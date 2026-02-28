### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[多元索引](https://help.aliyun.com/zh/tablestore/search-index-introduction-of-tablestore/)[全文检索](https://help.aliyun.com/zh/tablestore/full-text-search-of-search-index/)摘要与高亮

# 摘要与高亮

更新时间：2024-12-19 02:42:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：分词](https://help.aliyun.com/zh/tablestore/tokenization-of-text-column-in-search-index)[下一篇：向量检索](https://help.aliyun.com/zh/tablestore/knn-vector-query-function/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

场景

功能概述

注意事项

接口

参数

Highlight参数

InnerHits参数

使用方式

计费说明

常见问题

相关文档

要使用查询摘要与高亮功能，您需要在创建多元索引时为Text类型的字段开启摘要与高亮（Highlight）功能，然后在查询数据时通过设置高亮参数，返回命中查询词的片段信息并对查询词进行高亮显示。

## **场景**

查询摘要与高亮功能可用于全文检索场景中抽取命中查询词附近的片段并高亮命中的查询词，适用于网页搜索、聊天记录检索、文档搜索等场景。

### 功能概述

查询摘要与高亮功能可用于在搜索结果中对与查询词匹配或相关的文本进行高亮显示，帮助用户快速识别到所需的相关查询内容，提高信息检索的效率。对于包含嵌套类型的复杂数据结构（例如JSON）也支持使用查询摘要与高亮功能来精准定位所需信息。表格存储默认使用`<em></em>`标签来标记匹配的查询词。

要使用查询摘要与高亮功能，您需要完成如下配置：

1. 在创建多元索引时，设置Text类型字段的enableHighlighting参数为True。具体操作，请参见 [创建多元索引](https://help.aliyun.com/zh/tablestore/create-search-indexes-by-using-console-cli-or-sdk "")。



**重要**





只支持为Text类型字段开启查询摘要与高亮功能。

2. 在数据查询中使用查询摘要与高亮功能时，通过指定高亮分片的编码方式、返回高亮分片的最大数量、前置Tag、后置Tag等参数来自定义高亮显示的样式。


假设创建多元索引时已为某个Text类型字段开启查询摘要与高亮功能，当该Text类型字段的值为`查询高亮测试`时，在通过MatchPhrase功能查询关键词`高亮`，并指定高亮参数后，可返回高亮片段`查询<em>高亮</em>测试`。

## **注意事项**

- 在MatchQuery和MatchPhraseQuery中使用查询摘要与高亮功能时，查询词可能会被多个preTag、postTag高亮显示。

- 如果Text字段的分词类型为最大语义分词，则使用MatchPhraseQuery功能进行数据查询时不支持使用查询摘要与高亮功能。

- 分片切分可能会将文本中的查询词分割，此时该查询词可能不会被高亮。


## 接口

查询摘要与高亮功能的接口为 [Search](https://help.aliyun.com/zh/tablestore/developer-reference/search "")，具体的Query类型支持 [TermQuery](https://help.aliyun.com/zh/tablestore/developer-reference/termquery "")、 [TermsQuery](https://help.aliyun.com/zh/tablestore/developer-reference/termsquery "")、 [MatchQuery](https://help.aliyun.com/zh/tablestore/developer-reference/matchquery "")、 [MatchPhraseQuery](https://help.aliyun.com/zh/tablestore/developer-reference/matchphrasequery "")、 [PrefixQuery](https://help.aliyun.com/zh/tablestore/developer-reference/prefixquery "")、 [WildcardQuery](https://help.aliyun.com/zh/tablestore/developer-reference/wildcardquery "") 和 [NestedQuery](https://help.aliyun.com/zh/tablestore/developer-reference/nestedquery "")。

## **参数**

使用查询摘要与高亮功能时，一般情况下通过Highlight参数设置高亮参数。对于嵌套类型的子列，则需要通过InnerHits参数设置高亮参数。

### **Highlight参数**

| **参数** | **说明** |
| --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数** | **说明** |
| highlightEncoder | 对高亮分片原文内容的编码方式。取值范围如下：<br>- PLAIN（默认）：原文展示，不进行编码。<br>  <br>- HTML：对高亮分片原文进行HTML转义，转义包括`<`转义为`&lt;`、`>`转义为`&gt;`、`"`转义为`&quot;`、`'`转义为`&#x27;`、`/`转义为`&#x2F;`，网页展示时推荐使用HTML格式。 |
| fieldHighlightParams | 字段高亮参数，仅支持设置SearchQuery中包含关键词查询的字段。 |
| HighlightParameter | numberOfFragments | 返回高亮分片的最大数量，推荐设置为1。 |
| fragmentSize | 每个分片的长度。默认值100。<br>**重要**<br>实际返回分片的长度不会与该值严格相等。 |
| preTag | 查询词高亮的前置Tag，例如`<em>`、`<b>`。默认值为`<em>`，您可以按需自定义前置Tag。preTag支持的字符集包括`< > " ' /`、`a-z`、`A-Z`、`0-9`。 |
| postTag | 查询词高亮的后置Tag，例如`</em>`、`</b>`。默认值为`</em>`，您可以按需自定义后置Tag。postTag支持的字符集包括`< > " ' /`、`a-z`、`A-Z`、`0-9`。 |
| highlightFragmentOrder | 当高亮字段返回多个分片时，分片的排序规则。<br>- TEXT\_SEQUENCE（默认）：片段在文本中出现的顺序。<br>  <br>- SCORE：根据命中查询词评分排序多个分片。 |

### **InnerHits参数**

| **参数** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **参数** | **说明** |
| sort | Nested子行返回时的排序规则。 |
| offset | 当Nested列包含多个子行时，子行返回的起始位置。 |
| limit | 当Nested列包含多个子行时，返回子行的数量。默认值为3。 |
| highlight | Nested子列高亮参数配置。具体配置说明请参见 [Highlight参数](https://help.aliyun.com/zh/tablestore/query-highlight#665274d6c375a "")。 |

## **使用方式**

**重要**

只支持通过SDK方式使用查询摘要与高亮功能。

进行高亮查询之前，您需要完成如下准备工作。

- 使用阿里云账号或者具有表格存储操作权限的RAM用户进行操作。如果需要为RAM用户授权表格存储操作权限，请参见 [通过RAM Policy为RAM用户授权](https://help.aliyun.com/zh/tablestore/configure-user-permissions "") 进行配置。

使用SDK方式进行操作时，如果当前无可用AccessKey，则需要为阿里云账号或者RAM用户创建AccessKey。具体操作，请参见 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "")。

- 已创建数据表。具体操作，请参见 [数据表操作](https://help.aliyun.com/zh/tablestore/table-operations "")。

- 已为数据表创建多元索引且为指定字段开启了高亮查询功能。具体操作，请参见 [创建多元索引](https://help.aliyun.com/zh/tablestore/create-search-indexes-by-using-console-cli-or-sdk "")。

- 使用SDK方式进行操作时，还需要完成初始化Client。具体操作，请参见 [初始化OTSClient](https://help.aliyun.com/zh/tablestore/tablestore-client-initiation-in-java "")。


您可以通过 [Java SDK](https://help.aliyun.com/zh/tablestore/developer-reference/query-highlight-by-using-java-sdk "")、 [Go SDK](https://help.aliyun.com/zh/tablestore/developer-reference/query-highlight-bu-using-go-sdk "")、 [Python SDK](https://help.aliyun.com/zh/tablestore/developer-reference/query-highlight-by-using-python-sdk "") 和 [Node.js SDK](https://help.aliyun.com/zh/tablestore/developer-reference/query-highlight-by-using-nodejs-sdk "") 使用查询摘要与高亮功能。此处以Java SDK为例介绍查询摘要与高亮功能的使用。

查询非嵌套类型字段时使用查询摘要与高亮

查询嵌套类型字段时使用查询摘要与高亮

以下示例用于使用MatchQuery功能查询表中Col\_Text列的值能够匹配`hangzhou shanghai`的数据，并在返回结果中对查询词进行高亮显示。其中Col\_Text列为Text类型。

```java
/**
 * MatchQuery查询摘要与高亮。
 */
public static void matchQueryWithHighlighting(SyncClient client) {
    SearchRequest searchRequest = SearchRequest.newBuilder()
            .tableName("<TABLE_NAME>")
            .indexName("<SEARCH_INDEX_NAME>")
            .returnAllColumnsFromIndex(true)
            .searchQuery(SearchQuery.newBuilder()
                    .limit(5)
                    .query(QueryBuilders.bool()
                            .should(QueryBuilders.match("Col_Text", "hangzhou shanghai")))
                    .highlight(Highlight.newBuilder()
                            .addFieldHighlightParam("Col_Text", HighlightParameter.newBuilder()
                                    .highlightFragmentOrder(HighlightFragmentOrder.TEXT_SEQUENCE)
                                    .preTag("<b>")
                                    .postTag("</b>")
                                    .build())
                            .build())
                    .build())
            .build();
    SearchResponse resp = client.search(searchRequest);

    // 打印查询和高亮结果。查询非嵌套类型字段时设置prefix为空即可。
    printSearchHit(resp.getSearchHits(), "");
}

/**
 * 打印searchHit内容。
 * @param searchHits searchHits
 * @param prefix Nested结构输出时，增加前缀以打印层次信息。
 */
private static void printSearchHit(List<SearchHit> searchHits, String prefix) {
    for (SearchHit searchHit : searchHits) {
        if (searchHit.getScore() != null) {
            System.out.printf("%s Score: %s\n", prefix, searchHit.getScore());
        }

        if (searchHit.getOffset() != null) {
            System.out.printf("%s Offset: %s\n", prefix, searchHit.getOffset());
        }

        if (searchHit.getRow() != null) {
            System.out.printf("%s Row: %s\n", prefix, searchHit.getRow().toString());
        }

        // 打印各字段高亮分片结果。
        if (searchHit.getHighlightResultItem() != null) {
            System.out.printf("%s Highlight: \n", prefix);
            StringBuilder strBuilder = new StringBuilder();
            for (Map.Entry<String, HighlightField> entry : searchHit.getHighlightResultItem().getHighlightFields().entrySet()) {
                strBuilder.append(entry.getKey()).append(":").append("[");\
                strBuilder.append(StringUtils.join(",", entry.getValue().getFragments())).append("]\n");
            }
            System.out.printf("%s   %s", prefix, strBuilder);
        }

        System.out.println();
    }
}
```

以下示例用于使用NestedQuery功能查询表中Col\_Nested嵌套类型字段中Level1\_Col1\_Nested子列的值能够匹配`hangzhou shanghai`的数据，并在返回结果中对查询词进行高亮显示。

```java
/**
 * NestedQuery查询摘要与高亮，通过innerHits设置参数。
 */
public static void nestedQueryWithHighlighting(SyncClient client) {
        SearchRequest searchRequest = SearchRequest.newBuilder()
                .tableName("<TABLE_NAME>")
                .indexName("<SEARCH_INDEX_NAME>")
                .returnAllColumnsFromIndex(true)
                .searchQuery(SearchQuery.newBuilder()
                        .limit(5)
                        .query(QueryBuilders.nested()
                                .path("Col_Nested")
                                .scoreMode(ScoreMode.Min)
                                .query(QueryBuilders.match("Col_Nested.Level1_Col1_Nested", "hangzhou shanghai"))
                                .innerHits(InnerHits.newBuilder()
                                        .highlight(Highlight.newBuilder()
                                                .addFieldHighlightParam("Col_Nested.Level1_Col1_Nested", HighlightParameter.newBuilder().build())
                                                .build())
                                        .build()))
                        .build())
                .build();
        SearchResponse resp = client.search(searchRequest);

        // 打印高亮结果。
        printSearchHit(resp.getSearchHits(), "");
}

/**
 * 打印searchHit内容。
 * @param searchHits searchHits
 * @param prefix Nested结构输出时，增加前缀以打印层次信息。
 */
private static void printSearchHit(List<SearchHit> searchHits, String prefix) {
    for (SearchHit searchHit : searchHits) {
        if (searchHit.getScore() != null) {
            System.out.printf("%s Score: %s\n", prefix, searchHit.getScore());
        }

        if (searchHit.getOffset() != null) {
            System.out.printf("%s Offset: %s\n", prefix, searchHit.getOffset());
        }

        if (searchHit.getRow() != null) {
            System.out.printf("%s Row: %s\n", prefix, searchHit.getRow().toString());
        }

        // 打印各字段高亮分片结果。
        if (searchHit.getHighlightResultItem() != null) {
            System.out.printf("%s Highlight: \n", prefix);
            StringBuilder strBuilder = new StringBuilder();
            for (Map.Entry<String, HighlightField> entry : searchHit.getHighlightResultItem().getHighlightFields().entrySet()) {
                strBuilder.append(entry.getKey()).append(":").append("[");\
                strBuilder.append(StringUtils.join(",", entry.getValue().getFragments())).append("]\n");
            }
            System.out.printf("%s   %s", prefix, strBuilder);
        }

        // 嵌套类型高亮结果。
        for (SearchInnerHit searchInnerHit : searchHit.getSearchInnerHits().values()) {
            System.out.printf("%s Path: %s\n", prefix, searchInnerHit.getPath());
            System.out.printf("%s InnerHit: \n", prefix);
            printSearchHit(searchInnerHit.getSubSearchHits(), prefix + "    ");
        }

        System.out.println();
    }
}
```

假设多层级嵌套类型字段Col\_Nested中包括Level1\_Col1\_Text（Text类型）和Level1\_Col2\_Nested（Nested类型）两列，其中Level1\_Col2\_Nested嵌套类型字段包括Level2\_Col1\_Text子列。

以下示例用于通过在NestedQuery中添加BoolQuery对Col\_Nested字段中的Level1\_Col1\_Text子列和Level1\_Col2\_Nested下的Level2\_Col1\_Text子列同时使用查询摘要与高亮功能。

```java
public static void nestedQueryWithHighlighting(SyncClient client) {
    SearchRequest searchRequest = SearchRequest.newBuilder()
            .tableName("<TABLE_NAME>")
            .indexName("<SEARCH_INDEX_NAME>")
            .returnAllColumnsFromIndex(true)
            .searchQuery(SearchQuery.newBuilder()
                    .limit(5)
                    .query(QueryBuilders.nested()
                            .path("Col_Nested")
                            .scoreMode(ScoreMode.Min)
                            .query(QueryBuilders.bool()
                                    .should(QueryBuilders.match("Col_Nested.Level1_Col1_Text", "hangzhou shanghai"))
                                    .should(QueryBuilders.nested()
                                            .path("Col_Nested.Level1_Col2_Nested")
                                            .scoreMode(ScoreMode.Min)
                                            .query(QueryBuilders.match("Col_Nested.Level1_Col2_Nested.Level2_Col1_Text", "hangzhou shanghai"))
                                            .innerHits(InnerHits.newBuilder()
                                                    .highlight(Highlight.newBuilder()
                                                            .addFieldHighlightParam("Col_Nested.Level1_Col2_Nested.Level2_Col1_Text", HighlightParameter.newBuilder().build())
                                                            .build())
                                                    .build())))
                            .innerHits(InnerHits.newBuilder()
                                    .sort(new Sort(Arrays.asList(
                                            new ScoreSort(),
                                            new DocSort()
                                    )))
                                    .highlight(Highlight.newBuilder()
                                            .addFieldHighlightParam("Col_Nested.Level1_Col1_Text", HighlightParameter.newBuilder().build())
                                            .build())
                                    .build()))
                    .build())
            .build();
    SearchResponse resp = client.search(searchRequest);
    // 打印高亮结果。
    printSearchHit(resp.getSearchHits(), "");
}

/**
 * 打印searchHit内容。
 * @param searchHits searchHits
 * @param prefix Nested结构输出时，增加前缀以打印层次信息。
 */
private static void printSearchHit(List<SearchHit> searchHits, String prefix) {
    for (SearchHit searchHit : searchHits) {
        if (searchHit.getScore() != null) {
            System.out.printf("%s Score: %s\n", prefix, searchHit.getScore());
        }

        if (searchHit.getOffset() != null) {
            System.out.printf("%s Offset: %s\n", prefix, searchHit.getOffset());
        }

        if (searchHit.getRow() != null) {
            System.out.printf("%s Row: %s\n", prefix, searchHit.getRow().toString());
        }

        // 打印各字段高亮分片结果。
        if (searchHit.getHighlightResultItem() != null) {
            System.out.printf("%s Highlight: \n", prefix);
            StringBuilder strBuilder = new StringBuilder();
            for (Map.Entry<String, HighlightField> entry : searchHit.getHighlightResultItem().getHighlightFields().entrySet()) {
                strBuilder.append(entry.getKey()).append(":").append("[");\
                strBuilder.append(StringUtils.join(",", entry.getValue().getFragments())).append("]\n");
            }
            System.out.printf("%s   %s", prefix, strBuilder);
        }

        // 嵌套类型高亮结果。
        for (SearchInnerHit searchInnerHit : searchHit.getSearchInnerHits().values()) {
            System.out.printf("%s Path: %s\n", prefix, searchInnerHit.getPath());
            System.out.printf("%s InnerHit: \n", prefix);
            printSearchHit(searchInnerHit.getSubSearchHits(), prefix + "    ");
        }

        System.out.println();
    }
}
```

## **计费说明**

在数据查询时使用查询摘要与高亮功能不影响现有计费规则。

使用VCU模式（原预留模式）时，使用多元索引查询数据会消耗VCU的计算资源。使用CU模式（原按量模式）时，使用多元索引查询数据会消耗读吞吐量。更多信息，请参见 [多元索引计量计费](https://help.aliyun.com/zh/tablestore/product-overview/billable-items-of-search-indexes-1 "")。

## **常见问题**

- [使用多元索引 Search 接口查不到数据](https://help.aliyun.com/zh/tablestore/what-do-i-do-if-no-data-can-be-found-by-calling-the-search-operation "")

- [如何将多元索引 Search 接口查询数据的 limit 提高到 1000](https://help.aliyun.com/zh/tablestore/support/how-do-i-increase-the-value-of-the-limit-parameter-to-1000-when-i-call-the-search-operation-of-the-search-index-feature-to-query-data "")

- [为什么使用多元索引翻页查询时 Token 失效了？](https://help.aliyun.com/zh/tablestore/why-does-a-token-become-invalid-when-pagination-is-used-in-a-search-index-based-query "")


## **相关文档**

- 多元索引查询类型包括 [精确查询](https://help.aliyun.com/zh/tablestore/term-query-function "")、 [多词精确查询](https://help.aliyun.com/zh/tablestore/terms-query-function "")、 [全匹配查询](https://help.aliyun.com/zh/tablestore/match-all-query-function "")、 [匹配查询](https://help.aliyun.com/zh/tablestore/match-query-function "")、 [短语匹配查询](https://help.aliyun.com/zh/tablestore/match-phrase-query-function "")、 [范围查询](https://help.aliyun.com/zh/tablestore/range-query-function "")、 [前缀查询](https://help.aliyun.com/zh/tablestore/prefix-query-function "")、 [后缀查询](https://help.aliyun.com/zh/tablestore/suffix-query "")、 [通配符查询](https://help.aliyun.com/zh/tablestore/wildcard-query-function "")、 [基于分词的通配符查询](https://help.aliyun.com/zh/tablestore/fuzzy-query "")、 [多条件组合查询](https://help.aliyun.com/zh/tablestore/boolean-query-function "")、 [地理位置查询](https://help.aliyun.com/zh/tablestore/geographical-location-query/ "")、 [嵌套类型查询](https://help.aliyun.com/zh/tablestore/nested-query-function "")、 [向量检索、](https://help.aliyun.com/zh/tablestore/vector-query-introduction-and-usage "") 和 [列存在性查询](https://help.aliyun.com/zh/tablestore/exists-query-function "")，您可以选择合适的查询类型进行多维度数据查询。

如果要对结果集进行排序或者翻页，您可以使用排序和翻页功能来实现。具体操作，请参见 [排序和翻页](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function "")。

如果要按照某一列对结果集做折叠，使对应类型的数据在结果展示中只出现一次，您可以使用折叠（去重）功能来实现。具体操作，请参见 [折叠（去重）](https://help.aliyun.com/zh/tablestore/collapse "")。

- 如果要进行数据分析，例如求最值、求和、统计行数等，您可以使用 Search 接口的统计聚合功能或者 SQL 查询来实现。具体操作，请参见 [统计聚合](https://help.aliyun.com/zh/tablestore/aggregation-of-tablestore "") 和 [SQL查询](https://help.aliyun.com/zh/tablestore/sql-query-introductions/ "")。

- 如果要快速导出数据，而不关心整个结果集的顺序时，您可以使用 ParallelScan 接口和 ComputeSplits 接口实现多并发导出数据。具体操作，请参见 [并发导出数据](https://help.aliyun.com/zh/tablestore/parallel-scan-2 "")。