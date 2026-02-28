Timestream数据存储包含元数据表和数据表。数据表可以有多个，您可以根据自身的场景需求将数据写入到不同的表中，例如按数据精度分表。元数据表只能有一个，所有数据表的元数据信息全部记录到同一张表中。Timestream提供了元数据表和数据表的创建和删除功能。

## 元数据表

创建元数据表时可以预定义需要建索引的Attributes以及对应的索引属性和类型。索引类型支持LONG、DOUBLE、BOOLEAN、KEYWORD、GEO\_POINT等类型，属性包含Index、Store和Array，其含义与多元索引相同。

**说明**

没有指定索引类型的Attributes不会创建索引，后续时间线检索时也就不能指定这类Attributes作为查询条件。


操作步骤及示例代码如下。

1. 创建不包含任何Attributes索引的元数据表。
















```abnf
           db.createMetaTable();
```

2. 创建指定Attributes索引的元数据表。
















```pgsql
           List<AttributeIndexSchema> indexSchemas = new ArrayList<AttributeIndexSchema>();
           indexSchemas.add(new AttributeIndexSchema("owner", AttributeIndexSchema.Type.KEYWORD).setIsArray(true));
           indexSchemas.add(new AttributeIndexSchema("number", AttributeIndexSchema.Type.LONG));
           indexSchemas.add(new AttributeIndexSchema("score", AttributeIndexSchema.Type.DOUBLE));
           indexSchemas.add(new AttributeIndexSchema("succ", AttributeIndexSchema.Type.BOOLEAN));
           indexSchemas.add(new AttributeIndexSchema("loc", AttributeIndexSchema.Type.GEO_POINT));
           db.createMetaTable(indexSchemas);
```

3. 删除元数据表。
















```abnf
           db.deleteMetaTable();
```


## 数据表

操作步骤及示例代码如下。

1. 创建数据表。
















```abnf
           db.createDataTable("datatable");
```

2. 删除数据表。
















```abnf
           db.deleteDataTable("datatable");
```


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 表操作

# 表操作

更新时间：2020-02-27 04:04:36

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)




<-help;script>$icmsDocProps={'productMethod':'created','language':'zh-CN',};<-help;/script>-help;

上一篇：无[下一篇：什么是表格存储](https://help.aliyun.com/zh/tablestore/product-overview/what-is-tablestore)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

元数据表

数据表