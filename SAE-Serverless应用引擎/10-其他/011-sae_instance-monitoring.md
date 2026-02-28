### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/)[专业版应用监控](https://help.aliyun.com/zh/sae/monitoring-on-application-professional-edition/)实例监控

# 实例监控

更新时间：2025-05-18 22:56:20

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：调用链分析](https://help.aliyun.com/zh/sae/trace-explorer)[下一篇：持续性能剖析](https://help.aliyun.com/zh/sae/continuous-performance-profiling)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

支持的框架

查看实例监控

查看实例详情

概览

JVM监控

线程池监控

连接池监控

容器监控

调用链分析

常见问题

应用级别的数据与单机的数据是什么关系

不同实例之间流量不均匀

Undertow一次请求被统计成了两次

容器监控中CPU/内存配额与Pod实际设置不一致

系统指标部分缺失、不准或者CPU使用率展示为100%

为什么应用刚启动会FullGC

VM Stack指标是如何计算的

JVM指标获取原理

为什么JVM最大堆内存值为-1

为什么JVM堆内存使用总量不等于设置的堆内存最大值

JVM GC的频率逐渐加快

线程池、连接池监控没有数据

HikariCP连接池获取的最大连接数与实际不符

池化监控指标展示数值是小数

线程池/连接池明明被打满了，但为什么监控上没有体现出来

线程池监控最大线程数不符合预期或者最大线程数为21亿

Tomcat 线程池监控各项指标均不符合预期

某个线程池/连接池在某个时间点前无数据

HTTPClient连接池无数据

ACK环境应用接入后无法看到容器监控数据

句柄打开率不为0，而文件句柄数为0

JVM进程的实际物理内存占用和JVM监控中的堆内存占用有较大差距

为什么连接池 Druid 实时的空闲连接数会超过设置的最大空闲连接数？

部分实例探针升级到了最新版本，但为什么没数据？

当专业版应用开启应用监控后，ARMS服务即可对应用进行监控，您可以在实例监控页面了解应用的基础监控、实例GC和JVM内存等信息。

## 支持的框架

- [支持的Java组件和框架](https://help.aliyun.com/zh/arms/application-monitoring/developer-reference/java-components-and-frameworks-supported-by-arms#section-rbj-qsg-qgb "")

- [支持的Golang组件和框架](https://help.aliyun.com/zh/arms/application-monitoring/developer-reference/go-components-and-frameworks-supported-by-arms-application-monitoring "")

- [支持的Python组件和框架](https://help.aliyun.com/zh/arms/application-monitoring/developer-reference/python-libriaries-supported-by-arms-application-monitoring "")


## 查看实例监控

在 **实例监控** 页签，您可在通过在快捷筛选区域（图示①）筛选需要查询的实例IP地址，在趋势图区域（图示②）可以查看实例的基础监控、实例GC和JVM内存的时序曲线，您也可以在服务列表区域（图示③）查看实例IP、CPU利用率、内存利用率、磁盘利用率、RED三指标（请求数、错误数、平均耗时）等信息。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8733267471/p948388.png)

- 在快捷筛选区域，您可以按主机地址对图表、实例列表进行筛选，此外，还可以查看对应主机的 **请求数量**、 **错误数** 和 **耗时**。


> 勾选目标实例IP地址，即可选择需要查询的IP地址。如果您不勾选IP地址，则默认查询所有IP地址的监控信息。

- 在趋势图区域（图示②），您可以查看实例的基础监控、实例GC和JVM内存的时序曲线。


  - 基础监控：应用在指定时间范围内CPU用量和内存用量趋势图。

  - 实例GC：应用在指定时间范围内Full GC和Young GC的趋势图。通过图表名称右侧的下拉框可以切换展示GC的次数和平均耗时。

  - JVM内存：应用在指定时间范围内堆内存已使用和最大值趋势图。通过图标名称右侧的下拉框可以切换展示非堆内存已使用和最大值趋势图。



    **说明**





    ARMS应用监控采集的数据来自JMX，其中非堆内存所包含的内存区域比Java进程中实际的非堆内存区域少，因此可能会出现监控中堆内存+非堆内存总和与通过`top`命令看到的RES大小存在一定差值，相关细节请参见 [JVM监控内存详情说明](https://help.aliyun.com/zh/arms/application-monitoring/developer-reference/jvm-monitoring-memory-details "")。


单击![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3245501071/p741973.png)图标，可以在弹出的对话框中查看该指标在某个时间段的统计情况或对比不同日期在同一时间段的统计情况，通过选择![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2245501071/p741972.png)图标可以切换柱状图、趋势图进行展示。

- 在实例列表区域（图示③），您可以查看实例IP、CPU用量、内存用量、负载、Full GC 次数、Young GC 次数、堆内存使用量、非堆内存使用量、RED三指标（请求数、错误数、平均耗时）等。

在实例列表区域，您可以执行以下操作：

  - 单击 **操作** 列的 **详情**、 **JVM监控**、 **线程池监控**、 **连接池监控** 或 **容器监控**，可查看实例更为详细的信息。更多信息，请参见 [查看实例详情](https://help.aliyun.com/zh/sae/instance-monitoring#a571e2c746oqa "")。

  - 单击 **操作** 列的 **调用链**，可以查看该实例的链路详情。更多信息，请参见 [调用链分析](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/call-chain-analysis "")。

## 查看实例详情

### 概览

**概览** 页签可以查看目标接口的请求数、错误数、平均耗时和慢调用信息。

![gIKeue4rPA](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8733267471/p951603.png)

### JVM监控

**JVM监控** 页签可以查看对应实例的GC、内存、线程、文件等信息。

![iyBdFJIV2d](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8733267471/p951604.png)

### 线程池监控

4.1.x及以上探针版本

4.1.x以下探针版本

**线程池监控** 页签可以查看应用所使用的线程池的各项指标，包括线程池初始化线程配置 **、** 线程池运行态线程情况 **、** 线程池任务执行情况。

在页签顶部可以按线程池类型和名称筛选需要查询的线程池。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6202310471/p915857.png)

展开查看线程池监控支持的框架

支持框架：

- java.util.ThreadPoolExecutor：一般用于Tomcat8~9.1、Dubbo、HSF、Vertx以及用户自定义线程池。

- org.apache.tomcat.util.threads.ThreadPoolExecutor：一般用于Tomcat9.1+。

- org.eclipse.jetty.util.thread.QueuedThreadPool：一般用于Jetty。

- org.xnio.XnioWorker：一般用于Undertow。


采集的指标如下：

|     |     |     |
| --- | --- | --- |
| **指标名** | **支持框架** | **指标描述** |
| arms\_thread\_pool\_core\_pool\_size | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+）<br>  <br>- XnioWorker<br>  <br>- QueuedThreadPool | 核心线程数，一般是静态配置，不会改变。 |
| arms\_thread\_pool\_max\_pool\_size | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+）<br>  <br>- XnioWorker<br>  <br>- QueuedThreadPool | 最大线程数，一般是静态配置，不会改变。 |
| arms\_thread\_pool\_active\_thread\_count | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+）<br>  <br>- XnioWorker<br>  <br>- QueuedThreadPool | 活跃线程数，即当前正在执行任务的线程。 |
| arms\_thread\_pool\_current\_thread\_count | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+）<br>  <br>- QueuedThreadPool | 当前线程数，包含活跃线程数和当前正在等待任务的线程数。 |
| arms\_thread\_pool\_max\_thread\_count | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+） | 线程池历史最大线程数。 |
| arms\_thread\_pool\_scheduled\_task\_count | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+） | 线程池调度任务数。 |
| arms\_thread\_pool\_completed\_task\_count | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+） | 线程池执行完成任务数。 |
| arms\_thread\_pool\_rejected\_task\_count | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+）<br>  <br>- QueuedThreadPool | 线程池拒绝任务数。 |
| arms\_thread\_pool\_queue\_size | - ThreadPoolExecutor（JDK）<br>  <br>- ThreadPoolExecutor（Tomcat 9.1+）<br>  <br>- XnioWorker<br>  <br>- QueuedThreadPool | 线程池任务队列大小。 |

**线程池监控** 页签可以查看应用所使用的线程池的核心线程数量、当前线程数量、最大线程数量、活跃线程数量、任务队列容量等指标。

![2025-02-12_18-18-45](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6202310471/p915867.png)

展开查看线程池监控支持的框架

线程池监控支持Tomcat、HSF、Dubbo、Vert.x和Undertow框架，其中，3.1.x及以下版本探针支持Undertow1.x～Undertow2.0.x版本线程池监控，3.2.x及以上版本探针支持Undertow所有版本线程池监控。

采集的指标如下：

|     |     |
| --- | --- |
| **指标名称** | **指标** |
| 线程池核心线程数 | arms\_threadpool\_core\_size |
| 线程池最大线程数 | arms\_threadpool\_max\_size |
| 线程池活跃线程数 | arms\_threadpool\_active\_size |
| 线程池队列大小 | arms\_threadpool\_queue\_size |
| 线程池当前大小 | arms\_threadpool\_current\_size |

线程池监控支持SchedulerX框架，采集的指标如下：

|     |     |
| --- | --- |
| **指标名称** | **指标** |
| 线程池活跃线程数 | arms\_threadpool\_active\_size |

### 连接池监控

4.1.x及以上探针版本

4.1.x以下探针版本

**连接池监控** 页签可以查看应用所使用的连接池的各项指标，包括连接池初始化线程配置和连接池运行态线程情况。

在页签顶部可以按连接池类型筛选需要查询的连接池。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6202310471/p915861.png)

展开查看连接池监控支持的框架

支持框架：DBCP（>2.0）、Vibur DBCP（>11.0）、c3p0（>0.9.2）、Druid、HikariCP（>3.0）、Jedis（>3.0）、Lettuce（>5.0）、Redisson（>3.0）、tomcat-dbcp（>8.0）、tomcat-jdbc（>8.0）。

采集的指标如下：

|     |     |     |
| --- | --- | --- |
| **指标名** | **支持框架** | **指标描述** |
| arms\_connection\_pool\_connection\_count | DBCP、c3p0、Vibur DBCP、Druid、Hikaricp、Jedis、Lettuce、Redisson、tomcat-dbcp、tomcat-jdbc | 连接数，可通过State区分Active和Idle连接数。 |
| arms\_connection\_pool\_connection\_min\_idle\_count | DBCP、Jedis、Druid、HikariCP、Lettuce、tomcat-dbcp、tomcat-jdbc | 最小空闲连接数，一般是静态配置，不会改变。 |
| arms\_connection\_pool\_connection\_max\_idle\_count | DBCP、Jedis、Druid、Lettuce、tomcat-dbcp、tomcat-jdbc | 最大空闲连接数，一般是静态配置，不会改变。 |
| arms\_connection\_pool\_connection\_max\_count | DBCP、Druid、Vibur DBCP、HikariCP、tomcat-dbcp、tomcat-jdbc | 最大连接数，一般是静态配置，不会改变。 |
| arms\_connection\_pool\_pending\_request\_count | c3p0、HikariCP、Jedis、tomcat-dbcp、tomcat-jdbc | 阻塞的连接请求数。 |

**连接池监控** 页签可以查看应用所使用的连接池的最大连接数和活跃连接数指标。

![2025-02-12_18-18-58](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6202310471/p915868.png)

展开查看连接池监控支持的框架

连接池监控支持okHttp2、okHttp3框架，采集的指标如下：

|     |     |
| --- | --- |
| **指标名称** | **指标** |
| 连接池活跃连接数 | arms\_threadpool\_active\_size |
| 连接池当前连接数 | arms\_threadpool\_current\_size |

连接池监控支持Apache HTTPClient框架，采集的指标如下：

|     |     |
| --- | --- |
| **指标名称** | **指标** |
| 连接池当前连接数 | arms\_threadpool\_current\_size |
| 连接池最大连接数 | arms\_threadpool\_max\_size |
| 连接池等待队列数 | arms\_threadpool\_queue\_size |

连接池监控支持Druid框架，采集的指标如下：

|     |     |
| --- | --- |
| **指标名称** | **指标** |
| 连接池活跃连接数 | arms\_threadpool\_active\_size |
| 连接池最大连接数 | arms\_threadpool\_max\_size |

连接池监控支持Hikaricp框架，采集的指标如下：

|     |     |
| --- | --- |
| **指标名称** | **指标** |
| 连接池活跃连接数 | arms\_threadpool\_active\_size |
| 连接池最大连接数 | arms\_threadpool\_max\_size |

### **容器监控**

**容器监控** 页签可以查看容器视角的CPU、内存、网络流量的时序曲线。更多信息，请参见 [Java应用实例监控](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/instance-monitoring#ad3d818d8eckt "")、 [Golang应用实例监控](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/golang-application-instance-monitoring#3659526d90tvh "") 或 [Python应用实例监控](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/python-application-instance-monitoring "")。

![fbD6ZxpXcF](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8733267471/p951607.png)

### **调用链分析**

调用链分析功能基于已存储的全量链路明细数据，通过自由组合筛选条件与聚合维度进行实时分析，可以满足不同场景的自定义诊断需求。更多信息，请参见 [调用链分析](https://help.aliyun.com/zh/sae/trace-explorer "")。![Span数据信息](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0640706271/p337406.png)

## **常见问题**

### **应用级别的数据与单机的数据是什么关系**

- RED（请求数、错误数、延迟）指标：

  - 请求数、慢调用次数、HTTP状态码次数：应用级别的数据是单机级别数据的汇总。

  - 响应时间：应用级别的数据是单机级别数据的平均值。
- JVM指标：

  - GC次数、GC耗时：应用级别的数据是单机级别数据的汇总。

  - 堆内存数据、线程数：应用级别的数据是单机级别数据取最大值。
- 线程池/连接池指标

所有指标：应用级别的数据是单机级别数据的平均值。

- 系统指标

所有指标：应用级别的数据是单机级别数据取最大值。

- SQL/NSQL调用：同RED指标，对于次数类指标，应用级别的数据是单机级别数据的汇总；对于其余指标，应用级别的数据是单机级别数据的平均值。

- 异常指标：应用级别的数据是单机级别数据的汇总。


### **不同实例之间流量不均匀**

在3.x版本探针中，如果打开了内存优化开关，可能会导致部分指标统计丢失。该问题已在4.x版本探针中修复。

### **Undertow一次请求被统计成了两次**

3.2.x版本之前探针埋点方法在使用DeferredResult场景下一次调用中会被执行两次。该问题已在3.2.x及以上版本中修复。

### **容器监控中CPU/内存配额与Pod实际设置不一致**

请检查您的Pod中是否定义了多个Container，该指标会统计所有Container加起来的总配额。

### **系统指标部分缺失、不准或者CPU使用率展示为100%**

4.x之前版本探针不支持Windows环境下系统指标采集，4.x及以后版本探针已经修复。

### **为什么应用刚启动会FullGC**

一般是因为用户没有配置元空间大小，默认的元空间大小约为20 MB，应用在刚启动的时候可能会进行元空间的扩容从而触发FullGC，可通过`-XX:MetaspaceSize`参数和`-XX:MaxMetaspaceSize`参数设置初始元空间和最大元空间大小。

### **VM Stack指标是如何计算的**

该指标是通过线程数×1 MB得到的，其中1 MB是线程堆栈默认大小。如果通过`-Xss`参数重新指定了线程堆栈大小，则该数据与实际情况会有差异。

### **JVM指标获取原理**

ARMS展示的JVM指标均是通过标准的JDK接口获取的，对应接口如下：

内存相关指标：

- ManagementFactory.getMemoryPoolMXBeans

- java.lang.management.MemoryPoolMXBean#getUsage


GC相关指标：

- ManagementFactory.getGarbageCollectorMXBeans

- java.lang.management.GarbageCollectorMXBean#getCollectionCount

- java.lang.management.GarbageCollectorMXBean#getCollectionTime


### **为什么JVM最大堆内存值为-1**

-1代表未设置最大堆内存大小。

### **为什么JVM堆内存使用总量不等于设置的堆内存最大值**

根据JVM内存分配机制，`-Xms`参数指定初始堆内存分配，当空余堆内存不足后扩容，直到达到`-Xmx`参数设置的最大值，总量与最大量不一致说明还没触发扩容，使用量是当前实际用量。

### **JVM GC的频率逐渐加快**

可能是使用了JDK 8默认的GC算法ParallelGC，该算法默认开启了`-XX:+UseAdaptiveSizePolicy`，其作用是自动调整堆的大小，包括新生代大小、SurvivorRatio等参数，为了满足GC的停顿时间，当Young GC比较频繁时，可能会动态缩小Survivor区的大小，这时候Survivor区的对象很容易晋升到Old区，导致Old区空间涨幅过快，从而触发Full GC的频率也加快。更多信息，请参见 [Java官方文档](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gc-ergonomics.html)。

### **线程池、连接池监控没有数据**

1. 在 **自定义配置** 页面的 **高级设置** 区域确认是否已经开启线程池、连接池监控开关。

2. 检查框架是否在支持的范围内，具体内容，请参见 [线程池和连接池监控](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/thread-pool-monitoring#section-x3a-n5n-521 "")。


### **HikariCP连接池获取的最大连接数与实际不符**

3.2.x版本之前的探针获取最大连接数代码有误，3.2.x及以上版本已经修复。

### **池化监控指标展示数值是小数**

探针每隔15s采集一次，因此一分钟会采集4个点的数据，控制台会根据采集信息展示一个时间段的平均值。例如：一分钟采集的4个数据点为0、 0、 1、 0，理论上平均值为0.25。

### **线程池/连接池明明被打满了，但为什么监控上没有体现出来**

如果您的日志或其他记录中确实看到线程池/连接池被打满，但是ARMS控制台却看不到相关指标的增长，有可能是由于指标采样时间点与打满的时间点错开导致的。目前ARMS自动采集线程池/连接池状态指标的时间间隔为15s，发生在这个时间段内的瞬时冲高可能不会被采集到。

### **线程池监控最大线程数不符合预期** 或者最大线程数为21亿

ARMS最大线程池是直接调用线程池对象的获取最大线程数方法得到的，一般不会出错。如果不符合用户预期可能是用户设置的最大线程数未生效。

如果最大线程数为21亿，通常是调度线程池，在调度线程池中，默认设置的最大线程数是`Integer.MAX_VALUE`，如下图所示。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3312891371/p872598.png)

### Tomcat **线程池监控各项指标均不符合预期**

ARMS线程池指标是直接调用线程池对象的相应方法得到的，一般不会出错。如果几个维度都匹配不上（最大线程数、活跃线程数、核心线程数等），请先确认您的应用是否通过多个端口对外提供了 Tomcat 服务（如 spring-actuator 这类组件也会开放一个端口暴露指标），这种情况下探针会由于维度收敛机制将多个线程池的数据混在一起统计。如果数据混在一起，可以将探针版本升级到 4.1.10 及以上，并在**应用配置** \> **自定义配置**页面的 **池化监控配置** 区域，修改 **线程池线程名模式提取策略** 为`替换结尾数字字符为*`来解决。

### **某个线程池/连接池在某个时间点前无数据**

由业务自行触发了定时任务，任务初始化时产生了线程池/连接池数据，而定时任务被触发前则没有对应的线程池/连接池。流量型数据通常也会存在此类问题，例如某个接口的请求数。

### **HTTPClient连接池无数据**

从ARMS 4.x版本探针开始，ARMS不再支持okHttp3、Apache HTTPClient等框架的连接池监控，主要考虑此类框架会为当前应用的每一个外部访问域名创建一个连接池对象，当访问外部域名较多时，整体开销较高，存在稳定性风险，因此不再支持。

### **ACK环境应用接入后无法看到容器监控数据**

可能原因是创建ACK集群的阿里云账号与接入ARMS的阿里云账号不同，ARMS目前仅支持展示同一阿里云账号下的容器监控数据。

### **句柄打开率不为0，而文件句柄数为0**

请确认应用环境是否为JDK 9+，且ARMS探针版本为3.x，如果是，是由于相关指标采集逻辑在该环境存在兼容性问题，该问题已在4.2.2+版本探针中修复，建议 [升级探针](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/update-the-arms-agent-for-java-applications "") 到对应版本。

### **JVM进程的实际物理内存占用和JVM监控中的堆内存占用有较大差距**

这种情况一般是因为JVM进程有较大的堆外内存占用，ARMS目前仅能监控到JVM进程的堆内内存以及部分堆外内存占用，具体一个JVM占用内存中哪些可以被ARMS监控到哪些无法被监控到请参见 [JVM监控内存详情说明](https://help.aliyun.com/zh/arms/application-monitoring/developer-reference/jvm-monitoring-memory-details "")，如果出现较大的堆外内存占用，可以参见该文档的堆外内存泄露分析章节自行分析。

### **为什么连接池 Druid 实时的空闲连接数会超过设置的最大空闲连接数？**

[MaxIdle](https://github.com/alibaba/druid/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98#16-druid%E4%B8%AD%E7%9A%84maxidle%E4%B8%BA%E4%BB%80%E4%B9%88%E6%98%AF%E6%B2%A1%E7%94%A8%E7%9A%84) 是Druid为了方便DBCP用户迁移而增加的，实际上不会生效。

### **部分实例探针升级到了最新版本，但为什么没数据？**

若探针是从4.1.x以下版本升级上来的，则需要将全部实例对应的探针升级到最新版本，页面才能自动适配并进行数据展示。