[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [操作指南](https://help.aliyun.com/zh/sae/user-guide/) [运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/) [应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/) [专业版应用监控](https://help.aliyun.com/zh/sae/monitoring-on-application-professional-edition/) [应用诊断](https://help.aliyun.com/zh/sae/application-diagnosis/) 持续性能剖析

# 持续性能剖析

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：应用诊断](https://help.aliyun.com/zh/sae/application-diagnosis/)[下一篇：智能洞察](https://help.aliyun.com/zh/sae/intelligent-insights)

该文章对您有帮助吗？

反馈

持续剖析可以有效发现应用中因为CPU、内存和IO导致的瓶颈问题，并且按照方法名称、类名称和行号进行细分统计，最终协助开发者优化程序、降低延迟、增加吞吐、节约成本。本文介绍如何开通ARMS持续剖析功能以及如何查看持续剖析数据。

## **开启持续性能剖析**

持续性能剖析功能是默认关闭的，如果您需要使用该功能，请前往**应用配置** \> **自定义配置**页面开启该功能。

![amqlGp35Qs](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8853267471/p951644.png)

开通后该功能需要等1~2分钟才会有数据，如果长时间无数据表示当前状态下未采集到数据，请检查是否满足以下条件。

### **前提条件**

- 将Agent版本更新至v2.7.3.5或以上版本。升级探针的操作，请参见 [升级ARMS探针](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/update-the-arms-agent-for-java-applications "")。

- 如果应用所部署环境的VPC网络配置了可访问阿里云对象存储OSS的Bucket限制策略，由于该功能会将应用实例所采集数据上传到ARMS统一的OSS Bucket中进行存储与处理，如果配置相关策略但未将ARMS统一的OSS Bucket配置在其中会导致数据无法被有效采集。需要将持续剖析功能相关的Bucket（arms-profiling-<regionId>）配置在您的策略规则中。请将<regionId>换成对应的地域ID，例如您应用部署在cn-hangzhou地域，Bucket则对应为arms-profiling-cn-hangzhou。

- 持续剖析功能当前仅支持OpenJDK和Oracle JDK，不支持IBM OpenJ9和Oracle GraalVM JDK。


### **使用限制**

**操作系统内核限制：**

Linux 2.6.32-431.23.3.el6.x86\_64及以上。

**说明**

通过`uname -r`命令可以查询当前内核版本。

**JDK版本限制：**

ARMS的持续剖析功能使用Java虚拟机工具接口（Java Virtual Machine Tool Interface，简称 [JVM TI](https://docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html)）获取应用的方法栈，从而获得应用运行期间的CPU以及内存使用详情。JVM TI存在已知的 [Crash问题](https://bugs.openjdk.org/browse/JDK-8283849)，可能导致应用崩溃，这个问题在OpenJDK 8u352/11.0.17/17.0.5，Oracle JDK 11.0.21/17.0.9版本中已经得到了修复。对于问题修复之前的JDK版本，ARMS团队进行了多次测试，发现问题的触发依赖特殊的场景，发生概率极低。因此，在JDK版本不能满足要求的情况下，ARMS不会强制关闭持续剖析能力，您可以根据需要，临时打开持续剖析功能，并通过应用IP限制生效范围。但为了应用运行稳定，我们强烈建议您按照要求升级JDK版本，在低版本的JDK上使用持续剖析功能，存在应用崩溃的风险。

持续剖析功能主要依赖于JDK中存在调试符号（debug symbols），Alpine基础镜像为了控制体积而去除了JDK调试符号导致功能使用受影响，如需使用相关功能建议优先考虑使用非Alpine基础镜像。

持续剖析建议JDK版本：

|     |     |
| --- | --- |
| **JDK类型** | **版本** |
| OpenJDK | - OpenJDK 8u352+<br>  <br>- OpenJDK 11.0.17+<br>  <br>- OpenJDK 17.0.5+ |
| Oracle JDK | - Oracle JDK 11.0.21+<br>  <br>- Oracle JDK 17.0.9+ |

## **功能入口**

1. 在 **应用监控** 页面，单击**应用诊断** \> **持续性能剖析**，即可查看具体信息。

2. 在左侧实例列表中选择目标实例，然后在右侧页面设置数据展示时间。

3. 在右侧 **查询** 页签，您可以执行以下操作筛选数据并查看聚合分析。


![gZe113LpOO](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8853267471/p951658.png)

## **查看持续剖析数据**

- **选择快照时间范围：**

在 **查询** 页签的 **时间窗口大小** 区域，选择快照时间大小，支持 **1分钟**、 **5分钟** 和 **15分钟**，选择好快照时间大小后，可在曲线图上通过鼠标拖拽选择快照时间范围。

- **选择数据类型：**

在 **查询** 页签的 **时间窗口大小** 区域下方，单击下拉框选择数据类型，即可查看目标资源的曲线图。


  - Java应用支持选择的数据类型：cpu情况、jvm heap、jvm gc。

  - Golang应用支持选择的数据类型：cpu、go heap、goroutine、mutex、block。


![ET1GdgCYsV](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8853267471/p951700.png)

- **查看目标资源的快照详情：**

在查询页签，按照选择的快照时间范围列出了快照时间可快照大小。

![yu7Ol6Kvki](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8853267471/p951699.png)

- **聚合分析：**

单击 **聚合分析** 可以查看快照详情。


## 性能分析



您可以在 **性能分析类型** 对应的下拉框中选择指标类型。



![4nv4VCpame](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8853267471/p951717.png)



  - **Self** 列表示方法在自身的调用栈中所消耗的时间或资源，不包括其子方法调用所消耗的时间或资源。可以用于识别哪些方法在自身内部花费了大量的时间或资源。

  - **Total** 列包含方法自身消耗的时间或资源，及其所有子方法调用所消耗的时间或资源。可以帮助了解整个方法调用栈中哪些方法贡献了最多的时间或资源。


如需排查具体的热点代码逻辑，可以通过重点关注Self列或直接查看右侧火焰图中底部的较宽火苗从中定位到高耗时的业务方法，较宽火苗是引发上层耗时高的根源，一般是系统性能的瓶颈所在，您可以重点关注。

## 指标列表

在 **指标列表** 页签，可查看CPU、JVM线程数堆内存详情等指标的曲线图。

**说明**

Golang应用不支持查看指标列表。

![72v7ux2BsZ](<Base64-Image-Removed>)

## 快照列表

  - **快照大小：** 表示每分钟快照采集的数据量。

  - **CPU CORES：** 表示当前系统使用的CPU核心数。

  - **内存分配次数：** 表示单位时间内对象分配的次数。

  - **内存（TLAB）：** 表示线程本地分配缓冲区（Thread-Local Allocation Buffer）的使用情况。


![ZzmZeQRHsA](<Base64-Image-Removed>)

## **相关文档**

您可以使用持续剖析功能排查CPU和内存使用率较高的问题，具体操作如下：

- [通过火焰图定位性能瓶颈](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/how-to-locate-performance-bottlenecks-via-flame-chart "")

- [使用代码热点诊断Java应用慢调用问题](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/use-code-hotspots-to-diagnose-code-level-problems "")

- [使用CPU热点诊断CPU消耗高的问题](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/using-cpu-hotspots-to-diagnose-high-cpu-consumption "")

- [使用内存热点诊断堆内存使用高的问题](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/using-memory-hotspots-to-diagnose-high-heap-memory-usage "")


持续剖析功能使用过程中的常见问题，请参见 [常见问题](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/continuous-profiling-faq "")。