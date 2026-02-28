### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 初始化

# 初始化

更新时间：2024-03-05 02:47:04

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/ots)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

配置环境变量

示例代码

TimestreamDBClient是Timestream的客户端，您可以使用TimestreamDBClient进行建表、删表以及读写数据/时间线等操作。

![初始化](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5335328071/p44394.png)

上图为TimeStream模型的结构示意图，其中时序数据是存储到数据表中，时间线是存储到元数据表（Meta表）中。数据表可以根据业务需求创建多个，但元数据表只能有一个。所有数据表的时间线元数据写入到同一个元数据表中，您通过TimestreamDBConfiguration配置元数据表的表名。 伴随数据的写入，后台默认不断更新时间线的lastUpdateTime，您可以通过设置TimestreamDBConfiguration中的dumpMeta来控制是否需要打开后台更新时间线以及设置intervalDumpMeta来控制时间线更新的频率。

## 配置环境变量

请根据使用的操作系统执行相应的操作配置环境变量。

表格存储使用OTS\_AK\_ENV环境变量名表示阿里云账号或者RAM用户的AccessKey ID，使用OTS\_SK\_ENV环境变量名表示对应AccessKey Secret，请根据实际配置。

- Linux和macOS系统配置方法

执行如下命令配置环境变量。其中`<ACCESS_KEY_ID>`请替换为已准备好的AccessKey ID，`<ACCESS_KEY_SECRET>`请替换为对应的AccessKey Secret。















```shell
export OTS_AK_ENV=<ACCESS_KEY_ID>
export OTS_SK_ENV=<ACCESS_KEY_SECRET>
```

- Windows系统配置方法

通过图形化界面方式在 **环境变量** 对话框的 **系统变量** 区域中分别添加环境变量OTS\_AK\_ENV和OTS\_SK\_ENV，并将环境变量分别配置为已准备好的AccessKey ID和AccessKey Secret，然后保存配置即可。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6264269071/p772924.png)


## 示例代码

1. 使用默认Writer配置创建TimestreamDBClient。

















```java
final String endpoint = "";
String accessKeyId = System.getenv("OTS_AK_ENV");
String accessKeySecret = System.getenv("OTS_SK_ENV");
final String instance = "";
AsyncClient asyncClient = new AsyncClient(endpoint, accessKeyId, accessKeySecret, instance);
// 设置元数据表的表名。
TimestreamDBConfiguration conf = new TimestreamDBConfiguration("metaTableName");
// 设置后台更新时间线的最大间隔。
conf.setIntervalDumpMeta(10, TimeUnit.MINUTES);
TimestreamDBClient db = new TimestreamDBClient(asyncClient, conf);
```

2. 使用自定义Writer配置创建TimestreamDBClient。

















```java
// 自定义TableStoreWriter callback实现。
class DefaultCallback implements TableStoreCallback<RowChange, ConsumedCapacity> {
     private AtomicLong succeedCount = new AtomicLong();
     private AtomicLong failedCount = new AtomicLong();

     public void onCompleted(final RowChange req, final ConsumedCapacity res) {
       succeedCount.incrementAndGet();
     }

     public void onFailed(final RowChange req, final Exception ex) {
       System.out.println("Got error:" + ex.getMessage());
       dirtyLog.info(gson.toJson(req));
       failedCount.incrementAndGet();
     }
}

AsyncClient asyncClient = new AsyncClient(endpoint, accessKeyId, accessKeySecret, instance, clientConfiguration);
// 设置元数据表的表名。
TimestreamDBConfiguration conf = new TimestreamDBConfiguration("metaTableName");

DefaultCallback callback = new DefaultCallback();

// TableStoreWriter配置。
WriterConfig writerConfig = new WriterConfig();
// 设置writer的buffer为4096行。
writerConfig.setBufferSize(4096);

TimestreamDBClient db = new TimestreamDBClient(asyncClient, config, new WriterConfig(), callback);
```