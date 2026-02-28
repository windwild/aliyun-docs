### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用运维](https://help.aliyun.com/zh/sae/application-operations-maintenance-new/)弹性可观测

# 弹性可观测

更新时间：2025-02-25 04:44:47

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用Webshell实现文件上传下载](https://help.aliyun.com/zh/sae/use-the-webshell-feature-to-upload-and-download-files-2-0)[下一篇：查看应用事件](https://help.aliyun.com/zh/sae/view-application-events-2-0)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

为了帮助您更好地管理和优化云资源使用效率，实例数随弹性指标变化趋势图允许您直观地监控其应用在不同时间段内根据预设规则自动调整计算资源的过程及结果。

## **前提条件**

- 已部署应用。具体操作，请参见 [应用部署](https://help.aliyun.com/zh/sae/sae-application-deployment/ "") 目录下的文档。

- 已创建弹性伸缩策略，当前正在启动中。具体操作，请参见 [配置弹性伸缩策略](https://help.aliyun.com/zh/sae/configure-auto-scaling-new "")。


## 操作步骤

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在应用 **基础信息** 页面，单击 **弹性伸缩** 页签。

3. 在 **弹性伸缩** 页签的 **实例数随弹性指标变化趋势** 区域，设置查询时间范围，查看指定时间范围内的变化趋势。

   - **CPU使用率**

     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5604793371/p884134.png)

     上述图表展示了该时间段内CPU使用率的综合视图。主要包含以下6个参数：


     - CPU使用率：指CPU资源被占用的程度，是衡量系统负载的一个重要指标。

     - 应用实例数：指的是为了支持应用程序运行而部署的服务的数量。

     - 扩容区间：当CPU使用率超过预设的阈值时，可以增加的应用实例的最大数量。

     - 缩容区间：当CPU使用率下降到预设的阈值时，允许减少的应用实例的最大数量。

     - 目标值：指HPA设置的扩缩容阈值。

     - 弹性事件：实例数变动原因说明。


**说明**

     - 这些参数是您在配置HPA时所设定的。如果没有设定，则不会出现在趋势图中。

     - 如果其他指标也配置了HPA，则效果亦是相同的。


   - **内存使用率**

     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5604793371/p884741.png)

     上述图表展示了该时间段内内存使用率的综合视图。其中内存使用率指的是当前正在被使用的内存量与总可用内存量之间的比率。

   - **TCP活跃连接数**

     ![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5604793371/p884670.png)

     上述图表展示了该时间段内CPU使用率的综合视图。其中TCP活跃连接数指的是某一时间段内服务器或应用程序正在处理的TCP（传输控制协议）连接的数量。

- **服务请求量**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5604793371/p884671.png)

上述图表展示了该时间段内服务请求量的综合视图。其中服务请求量指的是应用程序或服务接收到的请求数量。

- **平均响应时间**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5604793371/p884672.png)

上述图表展示了该时间段内平均响应时间的综合视图。其中平均响应时间指的是服务对请求做出响应的平均所需时间。