### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[服务支持](https://help.aliyun.com/zh/sae/support/)[Web应用文档合集（文档停止维护）](https://help.aliyun.com/zh/sae/web-application-documentation/)[Web应用操作指南](https://help.aliyun.com/zh/sae/web-application-new/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-web/)[监控管理](https://help.aliyun.com/zh/sae/monitoring-management-web/)查看应用监控

# 查看应用监控

更新时间：2024-09-02 11:42:59

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查看基础监控数据](https://help.aliyun.com/zh/sae/view-basic-monitoring-data-web)[下一篇：日志管理（SLS）](https://help.aliyun.com/zh/sae/log-management-sls)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

查看应用监控

Serverless 应用引擎集成了应用实时监控服务的功能，提供了全面的监测能力。在SAE中，开启ARMS应用监控能力后，可以帮助您快速识别错误和性能低下的接口，检测内存泄露，以及揭示系统瓶颈，从而显著提高在线问题诊断的效率。本文主要介绍在SAE应用中查看应用监控。

## **前提条件**

- 创建Web应用并在创建时开启应用监控功能。具体步骤，请参见 [应用部署](https://help.aliyun.com/zh/sae/sae-2-web-only-application-deployment/ "") 和 [在创建应用时开启应用监控功能](https://help.aliyun.com/zh/sae/set-up-application-monitoring#74c7f9a2c49h4 "")。

- 如果在创建应用时未开启应用监控功能，请在创建Web应用成功后开启应用监控功能。具体操作，请参见 [在已创建的应用中开启应用监控功能](https://help.aliyun.com/zh/sae/set-up-application-monitoring#aac9a23810pdw "")。


## **查看应用监控**

1. 登录 [SAE控制台](http://saenext.console.aliyun.com/)。

2. 在左侧导航栏，选择**应用管理** \> **Web应用**，在顶部菜单栏选择地域。

3. 在 **应用列表** 页面，单击目标应用名称。

4. 查看目标应用的应用监控。

   - 在左侧导航栏，单击 **应用监控**，然后单击 **应用总览**。


     在应用总览页面上展示的有以下关键数据：



     - 选定时间内的总请求量、平均响应时间、实例数、问题数、Full GC次数和慢SQL次数，以及这些指标和上周、上一天的同比升降幅度。

     - 应用相关事件：应用相关的事件，比如0-1报警（如死锁、OOM和应用启动等）、应用监控报警和K8s集群事件等。将鼠标悬浮于柱状图上可以查看对应时间点的事件列表，更多信息，请参见 [事件中心](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/event-center#task-2389626 "")。

     - 应用提供服务：应用提供服务的请求量和平均响应时间的时序曲线。

     - 应用依赖服务：应用依赖服务的请求量、平均响应时间、应用实例数的时序曲线，以及HTTP-状态码统计。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p814878.png)

   - 在左侧导航栏，单击应用详情。


     在 **应用详情** 页面，单击以下页签，可以查看对应页签的详细信息：



     - **概览** 页签：可以查看应用的到请求数、响应时间、慢调用次数、HTTP状态码等信息。具体信息，请参见 [概览](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/overview-12 "")。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815043.png)

     - **拓扑视图** 页签：可以查看应用在指定时间段的内部服务的调用关系拓扑图。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815040.png)

     - **JVM监控** 页签：此功能主要监控应用的JVM指标，包括GC（Garbage Collection）瞬时指标、堆内存指标、非堆内存指标、元空间指标、直接缓冲区指标、JVM线程数等。具体信息，请参见 [JVM监控](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/jvm-monitoring "")。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815047.png)

     - **线程池监控** 页签：此功能用于监控应用所使用的线程池的各项指标，包括核心线程数量、当前线程数量、最大线程数量、活跃线程数量、任务队列容量。线程池支持的框架，请参见 [线程池支持的框架](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/thread-pool-monitoring#section-x3a-n5n-521 "")。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815048.png)

     - **连接池监控** 页签：此功能用于监控应用所使用的链接池的各项指标，包括最大线程数量和活跃线程数量。连接池支持的框架，请参见 [连接池支持的框架](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/thread-pool-monitoring#section-lgh-24l-op5 "")。



       **说明**





       - 该功能需要升级到2.7.1.3及以上探针版本，具体操作，请参见 [升级ARMS探针](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/update-the-arms-agent-for-java-applications#concept-1305370 "")。

       - 该功能在2.7.3.5以下版本需要在控制台单击 **开启开关** 手动开启 **线程池、连接池监控** 开关。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815213.png)

     - **SQL调用分析** 页签：该功能主要统计每分钟SQL的调用情况。具体信息，请参见 [SQL调用统计](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/sql-analysis#section-sh1-unx-jop "")。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815214.png)

     - **异常分析** 页签：通过查看该功能，可以了解应用的异常情况。具体信息，请参见 [异常分析](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/exception-analysis "")。

     - **上游应用** 页签：通过此功能可以查看上游应用向该应用发送数据的具体情况，包括响应时间、请求数和错误数等信息。具体信息，请参见 [上游应用](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/upstream-applications "")。

     - **下游应用** 页签：通过此功能可以查看到该应用向下游应用发送数据的具体情况，包括响应时间、请求数和错误数等信息。

     - **错误分析** 页签：单击 **错误分析** 页签，会跳转到ARMS控制台的 **调用链分析** 页面，此功能可以帮助您查看目标应用产生的错误信息，具体信息，请参见 [错误分析](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/error-analysis "")。

     - **调用链路查询** 页签：单击 **调用链路查询** 页签，会跳转到ARMS控制台的 **调用链分析** 页面，此功能可以帮助您了解目标应用的所有接口被调用的情况，包括产生时间、耗时、状态等信息。具体信息，请参见 [调用链查询](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/query-traces "")。


   - 在左侧导航栏，单击 **接口调用**。


     在 **接口调用** 页面，单击以下页签，可以查看对应页签的详细信息，具体信息，请参见 [接口调用](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/api-monitoring "")。



     - **概览** 页签：通过此功能可以查看目标接口的请求数、响应时间、错误数和HTTP-状态码统计的时序曲线。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815289.png)

     - **拓扑视图** 页签：可以查看应用在指定时间段的内部服务的调用关系拓扑图。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815294.png)

     - **SQL调用分析** 页签：此页签展示了左侧选中服务的代码段内所发起的SQL请求列表。此功能可以帮助您找出是哪一个SQL造成某个服务过慢。您还可以单击某个SQL的 **调用链查询** 来查看一个SQL执行逻辑所处的完整代码链路。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815303.png)

     - **异常分析** 页签：此页签展示了左侧选中服务的代码段内所抛出的Java异常。您还可以单击某个异常中的 **调用链查询** 来查看异常堆栈所处的完整代码链路。

       ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6972073271/p815327.png)

     - **链路上游** 页签：此页签展示应用上游（调用应用的一方）的接口及其调用性能指标，包括响应时间、请求次数和错误数。

     - 链路下游页签：此页签展示应用下游（被应用调用的一方）的接口及其调用性能指标，包括响应时间、请求次数和错误数。

     - **错误分析** 页签：单击 **错误分析** 页签，会跳转到ARMS控制台的 **调用链分析** 页面。此功能可以帮助您查看目标应用产生的错误信息。

     - **调用链查询** 页签：单击 **调用链路查询** 页签，会跳转到ARMS控制台的 **调用链分析** 页面，此功能可以帮助您了解目标应用的所有接口被调用的情况，包括产生时间、耗时、状态等信息。