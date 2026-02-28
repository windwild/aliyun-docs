### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [表格存储](https://help.aliyun.com/zh/tablestore/)[操作指南](https://help.aliyun.com/zh/tablestore/user-guide-10/)[多元索引](https://help.aliyun.com/zh/tablestore/search-index-introduction-of-tablestore/)[基础查询](https://help.aliyun.com/zh/tablestore/basic-features/)排序和翻页

# 排序和翻页

更新时间：2025-03-10 03:09:01

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：嵌套类型查询](https://help.aliyun.com/zh/tablestore/nested-query-function)[下一篇：折叠（去重）](https://help.aliyun.com/zh/tablestore/collapse)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用场景

使用方式

索引预排序

查询时排序

ScoreSort

PrimaryKeySort

FieldSort

GeoDistanceSort

翻页方式

使用limit和offset翻页

使用token翻页

使用多元索引查询数据时，通过预先定义排序方式或者查询时指定排序方式，您可以按照指定排列方式获取到返回数据。当返回结果行数较多时，通过使用跳转翻页或者连续翻页可以快速定位到所需数据。

## 使用场景

| **分类** | **使用方式** | **功能** | **使用场景** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **分类** | **使用方式** | **功能** | **使用场景** |
| 排序 | 创建时指定排序方式 | [IndexSort（索引预排序）](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#section-lly-qlx-dgb "") | 多元索引默认按照设置的索引预排序（IndexSort）方式进行排序，用于确定数据的默认返回顺序。 |
| 查询时指定排序方式 | [ScoreSort（相关性分数排序）](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#502e7d3b95742 "") | 按照查询结果的相关性（BM25算法）分数进行排序，适用于有相关性的场景，例如全文检索等。 |
| [PrimaryKeySort（主键排序）](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#p-t3b-vvq-8mj "") | 按照主键进行排序，适用于按照事物标识排序的场景。 |
| [FieldSort（字段值排序）](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#p-vcn-42a-3fb "") | 按照字段值进行排序，适用于电商、社交媒资等按照事物属性排序的场景，例如商品销量、浏览量等。<br>数组类型、嵌套类型等多值字段可以使用此方式通过指定mode参数来控制参与排序的元素。 |
| [GeoDistanceSort（地理位置排序）](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#p-a7f-gch-inu "") | 根据地理点距离进行排序，适用于地图、物流等按照距离排序事物的场景，例如某个位置周边餐厅按距离排序等。 |
| 翻页 | 查询时指定翻页方式 | [使用limit和offset翻页](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#9e29b863f8x7w "") | 返回结果行数小于100000行时用于跳转翻页。 |
| [使用token翻页](https://help.aliyun.com/zh/tablestore/sorting-and-paging-function#aba0959637ikd "") | 用于连续翻页，默认只能向后翻页。由于在一次查询的翻页过程中token长期有效，您可以通过缓存并使用之前的token实现向前翻页。 |

## 使用方式

您可以使用如下语言的SDK实现排序和翻页。

- [Java SDK：排序和翻页](https://help.aliyun.com/zh/tablestore/developer-reference/sorting-and-paging-by-java-sdk#concept-slf-n3x-dgb "")

- [Go SDK：排序和翻页](https://help.aliyun.com/zh/tablestore/developer-reference/sorting-and-paging-by-go-sdk#concept-inv-hq5-hgb "")

- [Python SDK：排序和翻页](https://help.aliyun.com/zh/tablestore/developer-reference/sorting-and-paging-by-python-sdk#concept-yw3-cck-pgb "")

- [Node.js SDK：排序和翻页](https://help.aliyun.com/zh/tablestore/developer-reference/sorting-and-paging-by-nodejs-sdk#concept-j33-pyk-2gb "")

- [.NET SDK：排序和翻页](https://help.aliyun.com/zh/tablestore/developer-reference/sorting-and-paging-by-dotnet-sdk#concept-hpd-5sc-fgb "")

- [PHP SDK：排序和翻页](https://help.aliyun.com/zh/tablestore/developer-reference/sorting-and-paging-by-php-sdk#concept-473609 "")


## 索引预排序

多元索引默认按照设置的索引预排序（IndexSort）方式进行排序，使用多元索引查询数据时，IndexSort决定了数据的默认返回顺序。

在创建多元索引时，您可以自定义IndexSort，如果未自定义IndexSort，则IndexSort默认为主键排序。

**重要**

- 索引预排序只支持PrimaryKeySort （按照主键排序）和FieldSort（按照字段值排序）两种方式。

- 含有Nested类型字段的多元索引不支持索引预排序。

- 创建多元索引后，如果要修改多元索引的IndexSort，您可以使用 [动态修改schema](https://help.aliyun.com/zh/tablestore/dynamically-modify-schemas "") 功能实现。


## 查询时排序

只有enableSortAndAgg设置为true的字段才能进行排序。

在每次查询时，可以指定排序方式，多元索引支持如下四种排序方式（Sorter）。您也可以使用多个Sorter，实现先按照某种方式排序，再按照另一种方式排序的需求。

### ScoreSort

按照查询结果的相关性（BM25算法）分数进行排序，适用于有相关性的场景，例如全文检索等。

**重要**

- 如果需要按照相关性打分进行排序，必须手动设置ScoreSort，否则会按照索引设置的IndexSort进行排序。

- 在使用ScoreSort时，FuzzyKeyword类型的字段不参与排序，且weight参数在FuzzyKeyword类型的字段上无效。


```java
SearchQuery searchQuery = new SearchQuery();
searchQuery.setSort(new Sort(Arrays.asList(new ScoreSort())));
```

### PrimaryKeySort

按照主键进行排序。

```java
SearchQuery searchQuery = new SearchQuery();
searchQuery.setSort(new Sort(Arrays.asList(new PrimaryKeySort()))); //正序。
//searchQuery.setSort(new Sort(Arrays.asList(new PrimaryKeySort(SortOrder.DESC)))); //逆序。
```

### FieldSort

按照列值进行排序。

单列排序

多列排序

补偿排序

多值排序

按照某列的值进行排序。

```java
SearchQuery searchQuery = new SearchQuery();
searchQuery.setSort(new Sort(Arrays.asList(new FieldSort("col", SortOrder.ASC))));
```

先按照某列的值进行排序，再按照另一列的值进行排序。

```java
SearchQuery searchQuery = new SearchQuery();
searchQuery.setSort(new Sort(Arrays.asList(
    new FieldSort("col1", SortOrder.ASC), new FieldSort("col2", SortOrder.ASC))));
```

按照Long类型、Double类型或者Date类型的列值进行排序时，您可以通过设置missingField参数指定类型相同的其他列作为某行缺失该列时的补偿值来参与排序。

```java
/**
* 基于Col_Long列的值逆序排序。如果某行Col_Long列（Long类型）的数据缺失，则使用Col_Long_sec列（Long类型）的数据替换Col_Long列数据用于排序。
*/
SearchQuery searchQuery = new SearchQuery();
FieldSort fieldSort = new FieldSort("Col_Long");
//指定Col_Long_sec列的值作为某行缺失Col_Long列时的默认值来参与排序。
fieldSort.setMissingField("Col_Long_sec");
fieldSort.setOrder(SortOrder.DESC);
```

对于数组类型、嵌套类型等多值字段可以通过指定mode参数来控制参与排序的元素。

按照数组多值的指定列值进行排序。

```java
// 有doc1和doc2两行数据，其field1列为数组类型。doc1的field1列值为[2,3]，doc2的field1列值为[1,3,4]。
// 您可以通过设置mode参数来指定按照数组中的哪个值进行排序。
{
    // 当设置mode参数为SortMode.MAX时，排序结果为doc2（4参与排序）、doc1（3参与排序）。
    FieldSort fieldSort = new FieldSort("field1", SortOrder.DESC);
    fieldSort.setMode(SortMode.MAX);
}
{
    // 当设置mode参数为SortMode.MIN时，排序结果为doc1（2参与排序）、doc2（1参与排序）。
    FieldSort fieldSort = new FieldSort("field1", SortOrder.DESC);
    fieldSort.setMode(SortMode.MIN);
}
```

您也可以对Nested类型字段的子行进行排序。

```java
// 有doc1和doc2两行数据，其field1列为Nested类型。
// doc1的field1列值为[{"name":"b", "age":1},{"name":"a", "age":7}]。
// doc2的field1列值为[{"name":"a", "age":1},{"name":"c", "age":1},{"name":"d", "age":5}]

{
    // 对所有子行进行排序，通过设置mode参数来指定按照哪个值进行排序。
    // 当设置mode参数为SortMode.MAX时，按照age列排序的排序结果为doc1（7参与排序）、doc2（5参与排序）。
    FieldSort fieldSort = new FieldSort("field1.age", SortOrder.DESC);
    fieldSort.setMode(SortMode.MAX);
    String path = "field1";
    NestedFilter nestedFilter = new NestedFilter(path, QueryBuilders.matchAll().build());
    fieldSort.setNestedFilter(nestedFilter);
}
{
    // 仅对age=1的子行进行排序，通过设置mode参数来指定按照哪个值进行排序。
    {
        // 当设置mode参数为SortMode.MAX时，按照name列排序的排序结果为doc2（"a"参与排序）、doc1("b"参与排序)
        FieldSort fieldSort = new FieldSort("field1.name", SortOrder.DESC);
        fieldSort.setMode(SortMode.MAX);
        String path = "field1";
        NestedFilter nestedFilter = new NestedFilter(path, QueryBuilders.term("students.age",1).build());
        fieldSort.setNestedFilter(nestedFilter);
    }
    {
        // 当设置mode参数为SortMode.MIN时，按照name列排序的排序结果为doc1（"b"参与排序）、doc2（"a"参与排序）。
        FieldSort fieldSort = new FieldSort("field1.name", SortOrder.DESC);
        fieldSort.setMode(SortMode.MIN);
        String path = "field1";
        NestedFilter nestedFilter = new NestedFilter(path, QueryBuilders.term("students.age",1).build());
        fieldSort.setNestedFilter(nestedFilter);
    }
}
```

### GeoDistanceSort

根据地理点距离进行排序。

```java
SearchQuery searchQuery = new SearchQuery();
//geo列为Geopoint类型，按照此列的值距离"0,0"点的距离进行排序。
Sort.Sorter sorter = new GeoDistanceSort("geo", Arrays.asList("0, 0"));
searchQuery.setSort(new Sort(Arrays.asList(sorter)));
```

## 翻页方式

在获取返回结果时，可以使用limit和offset或者使用token进行翻页。

### 使用limit和offset翻页

当需要获取的返回结果行数小于100000行时，可以使用limit和offset进行翻页，即limit+offset<=100000，其中limit的最大值为100。

**说明**

如果需要提高limit的上限，请参见 [如何将多元索引 Search 接口查询数据的 limit 提高到 1000](https://help.aliyun.com/zh/tablestore/support/how-do-i-increase-the-value-of-the-limit-parameter-to-1000-when-i-call-the-search-operation-of-the-search-index-feature-to-query-data#concept-2515203 "")。

如果使用此方式进行翻页时未设置limit和offset，则limit的默认值为10，offset的默认值为0。

```java
SearchQuery searchQuery = new SearchQuery();
searchQuery.setQuery(new MatchAllQuery());
searchQuery.setLimit(100);
searchQuery.setOffset(100);
```

### 使用token翻页

由于使用token进行翻页时翻页深度无限制，当需要进行深度翻页时，推荐使用token进行翻页。

当符合查询条件的数据未读取完时，服务端会返回nextToken，此时可以使用nextToken继续读取后面的数据。

使用token进行翻页时默认只能向后翻页。由于在一次查询的翻页过程中token长期有效，您可以通过缓存并使用之前的token实现向前翻页。

**重要**

如果需要持久化nextToken或者传输nextToken给前端页面，您可以使用Base64编码将nextToken编码为String进行保存和传输。token本身不是字符串，直接使用`new String(nextToken)`将token编码为String会造成token信息丢失。

使用token翻页后的排序方式和上一次请求的一致，无论是系统默认使用IndexSort还是自定义排序，因此设置了token不能再设置Sort。另外使用token后不能设置offset，只能依次往后读取，即无法跳页。

**重要**

由于含有Nested类型字段的多元索引不支持索引预排序，如果使用含有Nested类型字段的多元索引查询数据且需要翻页，则必须在查询条件中指定数据返回的排序方式，否则当符合查询条件的数据未读取完时，服务端不会返回nextToken。

```java
private static void readMoreRowsWithToken(SyncClient client) {
    SearchQuery searchQuery = new SearchQuery();
    searchQuery.setQuery(new MatchAllQuery());
    searchQuery.setGetTotalCount(true);//设置返回匹配的总行数。
    // 依次配置数据表名称（例如sampleTable）和多元索引名称（例如sampleSearchIndex）。您可以在表格存储控制台的数据表的“索引管理”页签或者通过SDK列出多元索引列表获取所需多元索引名称。
    SearchRequest searchRequest = new SearchRequest("sampleTable", "sampleSearchIndex", searchQuery);

    SearchResponse resp = client.search(searchRequest);
    if (!resp.isAllSuccess()) {
        throw new RuntimeException("not all success");
    }
    List<Row> rows = resp.getRows();
    while (resp.getNextToken()!=null) { // 当读取到nextToken为null时，表示读出全部数据。
        // 获取nextToken。
        byte[] nextToken = resp.getNextToken();

        {
            // 如果需要持久化nextToken或者传输nextToken给前端页面，您可以使用Base64编码将nextToken编码为String进行保存和传输。
            // token本身不是字符串，直接使用new String(nextToken)将token编码为String会造成token信息丢失。
            String tokenAsString = Base64.toBase64String(nextToken);
            // 将String解码为byte。
            byte[] tokenAsByte = Base64.fromBase64String(tokenAsString);
        }

        // 将token设置到下一次请求中。
        searchRequest.getSearchQuery().setToken(nextToken);
        resp = client.search(searchRequest);
        if (!resp.isAllSuccess()) {
            throw new RuntimeException("not all success");
        }
        rows.addAll(resp.getRows());
    }
    System.out.println("RowSize: " + rows.size());
    System.out.println("TotalCount: " + resp.getTotalCount());// 打印匹配到的总行数，非返回行数。
}
```